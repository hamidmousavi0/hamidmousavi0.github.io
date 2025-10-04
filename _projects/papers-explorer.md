---
layout: page
title: All-Conference Papers Explorer
description: Search NeurIPS, CVPR, ICML, ICLR, AAAI, and IJCAI papers from a single JSON.
permalink: /projects/papers-explorer/
img: /assets/projects/papers-explorer/cover.png   # shows as the card background on the Projects grid
# Optional categorization (shows tabs on your /projects/ page like “work”, “fun”)
category: work
# If you don’t want “Related posts” at the bottom:
related_posts: false
---

**Live demo:**  
<a class="btn btn-sm btn-primary" href="{{ site.baseurl }}/assets/projects/papers-explorer/index.html?data={{ site.baseurl }}/assets/projects/papers-explorer/all_2025_papers.json" target="_blank" rel="noopener">Open Papers Explorer</a>

**Source JSON:**  
`/assets/projects/papers-explorer/all_2025_papers.json`

**What it is**  
A static, client-side viewer that loads one JSON file and lets you search by title, authors, venue, and year, with lightweight relevance ranking and filters. Works on GitHub Pages (no backend).

**How to update the data**  
Drop a new JSON (e.g., `all_2026_papers.json`) in the same folder and link it with `?data=...` in the URL.
