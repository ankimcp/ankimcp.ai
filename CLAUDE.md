# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site for documenting the Anki MCP Desktop project, hosted at `ankimcp.ai`.

**What is Anki MCP?** A Model Context Protocol (MCP) server that enables AI assistants (like Claude) to interact with Anki flashcard decks - create cards, search content, and manage reviews through natural language. This website documents the desktop application; the actual MCP server code lives at https://github.com/anki-mcp/anki-mcp-desktop.

The site uses the Hextra theme via Hugo Modules and deploys to GitHub Pages (with plans to self-host later).

**Important**: "Anki" is a registered trademark of Ankitects Pty Ltd. This is an independent community project NOT affiliated with Ankitects. Always include trademark disclaimers when adding content.

## Technology Stack

- **Hugo** (extended version required) - Static site generator
- **Hextra theme** - Installed as Hugo Module (NOT git submodule)
- **Go** - Required for Hugo Modules functionality
- **GitHub Actions** - Automated deployment to GitHub Pages

## Development Commands

### Local Development
```bash
# Start development server with drafts
hugo server --buildDrafts

# Start development server (published content only)
hugo server

# Build site for production
hugo --minify

# Clean Hugo module cache (if issues)
hugo mod clean
```

### Module Management
```bash
# Update Hextra theme to latest version
hugo mod get -u github.com/imfing/hextra

# Tidy module dependencies
hugo mod tidy

# Initialize module (only needed once)
hugo mod init github.com/anki-mcp/ankimcp.ai
```

### Content Creation
```bash
# Create new content page
hugo new content/docs/your-page.md

# Create new blog post
hugo new content/blog/your-post.md
```

## Architecture

### Module-Based Theme
This site uses **Hugo Modules** (not git submodules) to manage the Hextra theme. The theme is declared in `hugo.yaml` under `module.imports` and downloaded to Go's module cache on first build.

**Why Modules?**
- Cleaner dependency management
- Easy updates with `hugo mod get -u`
- Recommended by Hextra documentation
- Avoids git submodule complexity

### Configuration Strategy
Start with minimal `hugo.yaml` config and add features incrementally. Test after each addition. Hextra provides sensible defaults - only override what's necessary.

**Banner System**: The site uses a key-based banner system (see `params.banner.key` in hugo.yaml). When you update the banner message, **always change the key value** (e.g., from `release-v0.6.0` to `release-v0.7.0`). This forces the banner to reappear for users who previously dismissed it.

### Content Structure
```
content/
├── _index.md              # Homepage
├── docs/                  # Documentation section
│   ├── _index.md
│   ├── getting-started/
│   ├── tools-reference/
│   └── development/
└── blog/                  # Blog posts (optional)
    └── _index.md
```

## Deployment

### GitHub Pages
- Automated via GitHub Actions workflow (`.github/workflows/`)
- Builds on push to `main` branch
- Publishes to `gh-pages` branch
- Custom domain configured via DNS

### DNS (Porkbun)
- A records point to GitHub Pages IPs
- CNAME for www subdomain
- HTTPS enabled via GitHub Pages

## Content Guidelines

### Target Audience
- **Primary**: End-users (non-developers) wanting to install and use Anki MCP
- **Secondary**: Developers contributing to the project

### Writing Style
- Non-technical, beginner-friendly for getting started guides
- Link to GitHub for in-depth developer documentation
- Keep explanations simple and visual where possible

### Trademark Compliance
Always include disclaimers when referencing Anki:
- Correct wording: "Anki® is a registered trademark of Ankitects Pty Ltd. This is an independent community project not affiliated with Ankitects Pty Ltd."
- Include in footer and prominently on homepage

## Common Issues

### Theme Styling Not Working
1. Verify Hugo extended version: `hugo version`
2. Check module is installed: `hugo mod graph`
3. Clear module cache: `hugo mod clean`
4. Rebuild: `hugo server`

### Module Not Found
```bash
hugo mod get github.com/imfing/hextra
hugo mod tidy
```

### Go Not Available
Hugo Modules requires Go installed. Install from https://go.dev/

## File Organization

- `/content/` - All markdown content (docs, blog posts, pages)
- `/static/` - Static assets (images, downloads, etc.)
- `/layouts/` - Custom layout overrides (only if needed)
- `/assets/` - Custom CSS/JS (only if needed)
- `hugo.yaml` - Main site configuration
- `.claude-draft/` - Planning documents (excluded from git)
- `go.mod`, `go.sum` - Hugo module dependencies (auto-generated)

## Testing Before Deployment

1. Run `hugo server --buildDrafts` locally
2. Verify all pages render correctly
3. Check mobile responsiveness
4. Test search functionality
5. Verify all links work
6. Build with `hugo --minify` to catch errors
