---
layout: default
title: Just the Docs Cheat Sheet
nav_order: 5
parent: Welcome          # Change to match your actual home page title
has_children: false
toc: true
toc_sticky: true
---

{:toc}


# Just the Docs – 5-Step Quick Reference

A minimal cheat sheet for getting started with Just the Docs on GitHub Pages (remote_theme).

## 1. _config.yml Essentials

Place this in `/docs/_config.yml`

```yaml
# Basics
title: Your Project Name          # Shown in header (unless logo overrides)
description: Short site description

remote_theme: just-the-docs/just-the-docs   # Required for remote setup
plugins:
  - jekyll-remote-theme

# Navigation / UI
color_scheme: light               # or "dark" (see section 3 below)
search_enabled: true              # Built-in Lunr.js search (highly recommended)
heading_anchors: true             # Anchor links on headings (¶ icon on hover)

# Top-right links (like Hugo's menu.extra)
aux_links:
  "GitHub Repo": "https://github.com/yourusername/your-repo"
aux_links_new_tab: true           # Open in new tab?

# Logo & favicon (paths relative to site root)
logo: "/assets/images/my-logo.png"   # Replaces title in header
favicon_ico: "/assets/images/favicon.ico"  # Or just place at /favicon.ico

# Footer "Edit on GitHub" links
gh_edit_link: true
gh_edit_link_text: "Edit this page on GitHub"
gh_edit_repository: "https://github.com/yourusername/your-repo"
gh_edit_branch: "main"
gh_edit_view_mode: "tree"         # "tree" = view file, "edit" = direct edit

# Other useful
last_edit_timestamp: true         # Shows "Last edited" if page has last_modified_date in front matter
mermaid:                          # If using diagrams
  enabled: true
```

## 2. Page Front Matter (for Navigation)

This is how JtD builds the left sidebar navigation (tree structure) — very similar to Hugo sections/taxonomies but done purely via front matter (no automatic folder-based hierarchy unless you use collections).

```yaml
---
layout: default               # Almost always this (JtD's main layout)

title: Page Title             # Required — shows in <title>, header, and sidebar

nav_order: 1                  # Integer: lower = higher in list (1 = top)
                              # Required for page to appear in sidebar

parent: Home                  # Exact title of parent page (creates nesting)
grand_parent: Section         # Optional deeper nesting (rarely needed)

has_children: true            # On parent pages: adds collapsible arrow + shows children
                              # Must be true even if children exist via front matter

permalink: /custom-url/       # Optional: overrides default /filename/ URL

last_modified_date: 2025-03-10  # For "Last edited" footer timestamp

# Optional extras
toc: true                     # Show right-side table of contents (headings)
toc_sticky: true              # TOC sticks when scrolling
---

# Your content...
```

Navigation rules

- `nav_order` → controls order  
- `parent` → nests under another page  
- `has_children`: true → shows arrow / collapsible

- A page only appears in the sidebar if it has `nav_order`.
- Children must point to the _exact_ `title` of the parent (case-sensitive).
- No automatic nav from folders — it's all explicit front matter (unlike Hugo's content tree).
- Use `has_children: true` on parents to make them collapsible.
- Sort is purely by `nav_order` within each level (no alphabetical fallback).

## 3. Navigation Hierarchy Example

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
    @import "./color_schemes/dark";   // Base on dark (or light)

    // Override variables (see full list in theme's _sass/support/_variables.scss)
    $body-bg-color: #0d1117;
    $link-color: #58a6ff;
    $sidebar-bg-color: #161b22;
    $header-bg-color: #010409;
    ```

1. Then set:

    ```yaml
    color_scheme: mybrand
    ```

## 5. Must-Know Gotchas & Tips

- GitHub Pages limitations — No custom plugins beyond the allowed list (remote_theme is fine, but no indexing plugins, etc.).
- Pages without `nav_order` → do not appear in sidebar
-Test locally (optional): bundle init, add gem "jekyll" and gem "just-the-docs", then bundle exec jekyll serve --source docs — but remote_theme works without this.
- `parent` must match exact `title` of parent page (case-sensitive)  
- No automatic nav from folders — all manual via front matter  
- Check Actions tab after push for build errors  
- Test search: type in the top-right search bar  
- Callouts: `{: .note }`, `{: .warning }`, `{: .important }` after paragraphs - customize colors in config
- Mermaid diagrams: enable with `mermaid: enabled: true` in config
- Print styles — Built-in and good (add @media print overrides if needed).
- Version pinning — If breakage worries you: remote_theme: just-the-docs/just-the-docs@v0.8.1 (check releases for latest stable).
Debug tip — Always check repo Actions tab for build logs if site looks wrong.

Start by setting color_scheme: dark, adding nav_order: 1 + has_children: true to your home page, and nav_order: 2 + parent: Home to a child page — push and watch the sidebar build.


## Key Differences from Hugo / Docsy

Since you're familiar with Hugo/Docsy:

| Aspect | Hugo / Docsy | Just the Docs (Jekyll) |
| --- | --- | --- |
| Navigation building | Automatic from content tree + menus config | Explicit via front matter (nav_order, parent) — no auto from folders |
| Sections hierarchy | Deep, folder-based + archetypes | Flat + manual nesting (parent/grand_parent) |
| Search | Lunr or Algolia (configurable) | Built-in Lunr.js (good enough, lightweight) |
| Themes / colors | SCSS vars + dark/light toggle often built-in | color_scheme: dark/light/custom + easy SCSS overrides |
| Custom shortcodes | Hugo shortcodes (very powerful) | Jekyll includes + Liquid tags (less flexible) |
| Diagrams / extras | Mermaid, diagrams.net via shortcodes | Built-in Mermaid support (enable in config) |
| Build speed / deps | Go-based (fast), few deps | Ruby/Jekyll (slower on large sites), GitHub limits plugins |
| GitHub Pages native | Not native (needs Netlify/others) | Native + remote_theme (zero local Ruby needed) |
| Learning curve if Hugo exp. | Familiar structure | More manual nav, but simpler config overall |

Docsy is heavier/more enterprise-feeling; JtD is lighter, cleaner for smaller-to-medium docs.


