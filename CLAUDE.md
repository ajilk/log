# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo-based personal blog/log website deployed to GitHub Pages at https://log.ajilk.com/. The site features posts, fragments (quotes/short thoughts), and a life visualization page showing weeks lived.

## Development Commands

### Build and Preview
```bash
# Start local development server (default: http://localhost:1313)
hugo server

# Start with draft content visible
hugo server -D

# Build the site for production (outputs to ./public)
hugo --gc --minify
```

### Content Management
```bash
# Create a new post
hugo new content/my-post-name.md

# Create a new fragment (quote/short thought)
hugo new content/fragments/fragment-name.md --kind fragment
```

All new posts are created with `draft = true` by default. Fragments are created with `draft = false`.

## Content Structure

The site has three main content sections:

1. **Posts** (`content/*.md`): Long-form blog posts and essays
2. **Life** (`content/life.md`): Interactive life visualization showing weeks lived
3. **Fragments** (`content/fragments/`): Short quotes and thoughts with optional author attribution

### Fragment Format

Fragments have special metadata:
- `author`: Set to "self" for personal thoughts, or the quote author's name
- `source`: Optional field for external quotes (e.g., book name)
- If `author` is blank, the fragment renders without attribution

## Architecture

### Layout System

Hugo uses a template hierarchy where layouts inherit from `layouts/_default/baseof.html`:

- **baseof.html**: Base template with header, footer, and Google Analytics
- **single.html**: Default single post layout with table of contents and back navigation
- **list.html**: Default list page layout
- **life.html**: Custom layout with JavaScript for life visualization (80 years × 52 weeks grid)
- **fragments.html**: Custom layout that displays all fragments in chronological order with dividers

### Custom Layouts

The site uses custom layouts for special pages:
- `/life` → uses `life.html` (interactive weeks-lived calculator with localStorage persistence)
- `/fragments` → uses `fragments.html` (displays all fragments in a single view)

### Archetypes

Two content archetypes define front matter templates:
- `archetypes/default.md`: Standard posts with title, date, and draft status
- `archetypes/fragment.md`: Fragments with author and source fields

## Deployment

The site auto-deploys via GitHub Actions (`.github/workflows/hugo.yaml`) on push to main:
- Hugo version: 0.152.2 (extended)
- Dart Sass version: 1.93.2
- Builds with `--gc --minify` flags
- Deploys to GitHub Pages

## Configuration

Site configuration in `hugo.toml`:
- Base URL: https://log.ajilk.com/
- Three main menu items: about, life, fragments
- Author metadata for site-wide use
