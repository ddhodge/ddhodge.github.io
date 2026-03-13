---
layout: default
title: Just the Docs Cheat Sheet
nav_order: 5
parent: Welcome          # Change to match your actual home page title
has_children: false
toc: true
toc_sticky: true
---

# Just the Docs – 5-Step Quick Reference

A minimal cheat sheet for getting started with Just the Docs on GitHub Pages (remote_theme).

## 1. _config.yml Essentials

Place this in `/docs/_config.yml`

```yaml
title: Your Project Docs
description: Documentation hub

remote_theme: just-the-docs/just-the-docs
plugins:
  - jekyll-remote-theme

color_scheme: dark                # or light / custom
search_enabled: true
heading_anchors: true

aux_links:
  "GitHub": "https://github.com/yourusername/your-repo"

logo: "/assets/images/logo.png"   # optional
```

## 2. Page Front Matter (for Navigation)

Every page needs this YAML at the top to appear in the left sidebar.yaml

```yaml
---
layout: default
title: Page Name                  # Required
nav_order: 3                      # 1 = top, higher numbers lower
parent: Home                      # Exact title of parent page
has_children: true                # Only on parents with children
permalink: /custom-url/           # Optional
toc: true                         # Right-side TOC
---
```

Navigation rules

- `nav_order` → controls order  
- `parent` → nests under another page  
- `has_children`: true → shows arrow / collapsible

### 3. Navigation Hierarchy Example

```yaml
# Home (index.md)
nav_order: 1
has_children: true

# Guides (guides.md)
parent: Home
nav_order: 2
has_children: true

# Example Guide (guides/example.md)
parent: Guides
nav_order: 1
```

## 4. Colors & Theme Customization

Quick changes in _config.yml:

```yaml
color_scheme: dark          # Built-in options: light, dark
```

Custom scheme (advanced):

1. Create `/docs/_sass/color_schemes/mybrand.scss`
1. Override variables (example):

    ```scss
    $body-bg-color: #0d1117;
    $link-color: #58a6ff;
    $sidebar-bg-color: #161b22;
    ```

1. Then set:

    ```yaml
    color_scheme: mybrand
    ```

## 5. Must-Know Gotchas & Tips

- Pages without `nav_order` → do not appear in sidebar  
- `parent` must match exact `title` of parent page (case-sensitive)  
- No automatic nav from folders — all manual via front matter  
- Check Actions tab after push for build errors  
- Test search: type in the top-right search bar  
- Callouts: `{: .note }`, `{: .warning }`, `{: .important }` after paragraphs  
- Mermaid diagrams: enable with `mermaid: enabled: true` in config


