---
title: "Custom scrollbar with CSS"
date: 2024-04-22
draft: false
slug: "css-custom-scrollbar"
description: "Minimal, cross-browser custom scrollbar using only CSS custom properties."
tags: ["scrollbar", "ux"]
language: "css"
---

```css
/* Works in Chrome, Edge, Safari */
:root {
  --scrollbar-width: 6px;
  --scrollbar-track: transparent;
  --scrollbar-thumb: oklch(60% 0.05 250);
  --scrollbar-thumb-hover: oklch(50% 0.08 250);
}

* {
  scrollbar-width: thin; /* Firefox */
  scrollbar-color: var(--scrollbar-thumb) var(--scrollbar-track);
}

*::-webkit-scrollbar {
  width: var(--scrollbar-width);
  height: var(--scrollbar-width);
}

*::-webkit-scrollbar-track {
  background: var(--scrollbar-track);
}

*::-webkit-scrollbar-thumb {
  background: var(--scrollbar-thumb);
  border-radius: 999px;
}

*::-webkit-scrollbar-thumb:hover {
  background: var(--scrollbar-thumb-hover);
}
```
