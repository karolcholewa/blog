---
layout: post
title: "Useful Regex"
categories: Tip
---

Replace markup in Markdown from strong to a heading.
- Find any word that's marked with ** for example **My title not heading**
```
^\*{2}
```
- replace the two asterixes with ##