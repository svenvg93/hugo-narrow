---
title: "HTTP client with exponential backoff retry"
date: 2024-03-10
draft: false
slug: "go-http-retry"
description: "A reusable HTTP GET wrapper that retries on transient errors with exponential backoff."
tags: ["http", "retry", "networking"]
language: "go"
---

```go
package main

import (
	"fmt"
	"math"
	"net/http"
	"time"
)

func getWithRetry(url string, maxRetries int) (*http.Response, error) {
	client := &http.Client{Timeout: 10 * time.Second}

	for attempt := 0; attempt <= maxRetries; attempt++ {
		resp, err := client.Get(url)
		if err == nil && resp.StatusCode < 500 {
			return resp, nil
		}

		if attempt == maxRetries {
			return nil, fmt.Errorf("failed after %d attempts", maxRetries+1)
		}

		wait := time.Duration(math.Pow(2, float64(attempt))) * 100 * time.Millisecond
		time.Sleep(wait)
	}

	return nil, nil
}
```
