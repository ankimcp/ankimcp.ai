# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for documenting the Anki MCP Desktop project, hosted at `ankimcp.ai`. The actual MCP server code lives at https://github.com/ankimcp/anki-mcp-server.

**Important**: "Anki" is a registered trademark of Ankitects Pty Ltd. This is an independent community project NOT affiliated with Ankitects. Always include trademark disclaimers when adding content.

## Technology Stack

- **Hugo** v0.151.0 extended (production) - Static site generator
- **Hextra theme** v0.11.1 - Installed as Hugo Module (NOT git submodule)
- **Go** 1.21 (CI/CD), 1.24.4 (go.mod) - Required for Hugo Modules
- **GitHub Actions** - Deploys to GitHub Pages with custom domain
- **Umami Analytics** - Self-hosted at analytics.anatoly.dev
- **MailerLite** - Newsletter integration (Form ID: `ZGJ6BF`)

## Development Commands

```bash
# Local development
hugo server --buildDrafts     # Include draft content
hugo server                   # Published content only
hugo --minify                 # Build for production

# Module management
hugo mod get -u github.com/imfing/hextra  # Update theme
hugo mod tidy                              # Clean dependencies
hugo mod clean                             # Clear cache if issues

# Content creation
hugo new content/docs/your-page.md        # New docs page
hugo new content/blog/your-post.md        # New blog post
```

## Critical Configuration

### ⚠️ JS Minification MUST Stay Disabled
- `minify.disableJS: true` in hugo.yaml is **REQUIRED**
- JS minification breaks MailerLite newsletter popup
- Never enable under any circumstances

### Banner System
- Uses key-based dismissal (`params.banner.key` in hugo.yaml)
- Stores dismissal state in localStorage
- **Always change key** when updating message (e.g., `release-v0.6.0` → `release-v0.7.0`)
- This forces banner to reappear for users who dismissed previous version

### Custom Layouts
Key overrides in `/layouts/`:
- `partials/custom/head-end.html` - Contains:
  - Canonical URLs (SEO)
  - MailerLite universal script
  - Schema.org structured data (SoftwareApplication, Organization, etc.)
  - Performance hints (preconnect, dns-prefetch)
- `blog/single.html` - Custom blog layout with author attribution for E-E-A-T SEO
- `partials/footer.html` - Newsletter/contact links
- `shortcodes/newsletter.html` - Newsletter shortcode

## Release Process

When announcing new versions:
1. Create blog post: `content/blog/vX.Y.Z-feature-name-release.md`
2. Update banner in `hugo.yaml`:
   - Change `params.banner.key` to new version
   - Update message and links
3. **Update Schema.org** in `layouts/partials/custom/head-end.html`:
   - Update `softwareVersion` field
   - Update `releaseNotes` URL to new blog post

## Content Standards

### Frontmatter Requirements
Required:
- `title` - Page title
- `description` - Meta description (150-160 chars ideal)

Recommended:
- `keywords` - SEO keywords array
- `sitemap_priority` - 0.0-1.0 (Homepage: 1.0, Important docs: 0.8, Blog: 0.6)
- `weight` - Navigation order (lower = first)

Blog-specific:
- `author` - Defaults to "Anatoly"
- `author_link` - Defaults to https://anatoly.dev
- `date` - Publication date

### Writing Guidelines
- **Primary audience**: Non-technical end users
- Keep explanations simple and visual
- Link to GitHub for developer documentation
- Include Anki trademark disclaimer on homepage and footer

## Testing Checklist

Before deployment:
1. Run `hugo server --buildDrafts` locally
2. Test mobile responsiveness
3. Verify MailerLite popup works (click newsletter button)
4. Build with `hugo --minify` to catch errors
5. Validate structured data with [Google's Rich Results Test](https://search.google.com/test/rich-results)

## Troubleshooting

### Port Already in Use
```bash
killall hugo               # Kill existing processes
hugo server -p 1314        # Or use different port
```

### Module Issues
```bash
hugo mod clean             # Clear cache
hugo mod tidy             # Clean dependencies
hugo mod get -u           # Re-fetch modules
```

### Theme Not Working
1. Verify Hugo extended: `hugo version`
2. Check module: `hugo mod graph`
3. Clear and rebuild: `hugo mod clean && hugo server`