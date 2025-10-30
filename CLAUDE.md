# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site for documenting the Anki MCP Desktop project, hosted at `ankimcp.ai`.

**What is Anki MCP?** A Model Context Protocol (MCP) server that enables AI assistants (like Claude) to interact with Anki flashcard decks - create cards, search content, and manage reviews through natural language. This website documents the desktop application; the actual MCP server code lives at https://github.com/anki-mcp/anki-mcp-desktop.

The site uses the Hextra theme via Hugo Modules and deploys to GitHub Pages with a custom domain.

**Important**: "Anki" is a registered trademark of Ankitects Pty Ltd. This is an independent community project NOT affiliated with Ankitects. Always include trademark disclaimers when adding content.

## Technology Stack

- **Hugo** (extended version required) - Static site generator (production uses v0.151.0)
- **Hextra theme** - Installed as Hugo Module (NOT git submodule)
- **Go** - Required for Hugo Modules functionality (v1.21 in CI/CD)
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

**Critical Configuration Details**:

⚠️ **JS MINIFICATION MUST STAY DISABLED** ⚠️
- `minify.disableJS: true` in hugo.yaml is **REQUIRED** and **NON-NEGOTIABLE**
- JS minification breaks the MailerLite newsletter popup integration
- Never enable JS minification under any circumstances

**Banner System**:
- Uses a key-based dismissal system (`params.banner.key` in hugo.yaml)
- Hextra stores banner dismissal state in browser localStorage using the key
- **Always change the key value** when updating the message (e.g., `release-v0.6.0` → `release-v0.7.0`)
- Changing the key forces the banner to reappear for all users who dismissed the previous version
- Format: Use semantic versioning for releases, or descriptive keys for other announcements

**Analytics**: Site uses Umami analytics (self-hosted at analytics.anatoly.dev). Configuration is in `params.analytics.umami`.

**MailerLite Integration**: Newsletter popup is embedded directly in the homepage (`content/_index.md`) with an onclick handler. Do not modify this integration without testing the popup functionality.

### Content Structure
```
content/
├── _index.md              # Homepage (includes MailerLite popup integration)
├── docs/                  # Documentation section
│   ├── _index.md
│   ├── installation/      # Installation guides for different modes
│   │   ├── desktop.md    # Desktop mode (Claude Desktop)
│   │   ├── mcp-clients.md # STDIO mode (Cursor, Cline)
│   │   └── web.md        # Web mode (ChatGPT, Claude.ai)
│   ├── audio-flashcards.md
│   ├── prompts.md
│   └── getting-help.md
├── blog/                  # Release announcements and updates
│   └── _index.md
└── about/                 # About page
    └── _index.md
```

## Deployment

### GitHub Pages
- Automated via GitHub Actions workflow (`.github/workflows/hugo.yml`)
- Builds on push to `main` branch or manual dispatch
- Uses Hugo v0.151.0 extended and Go v1.21
- Uploads artifact to GitHub Pages deployment
- Custom domain: ankimcp.ai (configured via Porkbun DNS)

### DNS (Porkbun)
- A records point to GitHub Pages IPs
- CNAME for www subdomain
- HTTPS enabled via GitHub Pages

### Build Process
The CI/CD pipeline runs:
1. `hugo mod get` - Download Hugo modules
2. `hugo --gc --minify` - Build with garbage collection and minification (CSS/HTML only, JS excluded)

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

### Release Announcements
When announcing a new version:
1. Create a blog post in `content/blog/` following the naming pattern: `vX.Y.Z-feature-name-release.md`
2. Update the banner in `hugo.yaml`:
   - Change `params.banner.key` to match the version (e.g., `release-v0.7.0`)
   - Update the message with the new version number and blog post link
   - Include a download link to the GitHub release
3. Blog posts should highlight key features and link to GitHub release notes for full details

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
