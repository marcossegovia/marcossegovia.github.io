# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal website for Marcos Segovia (msegovia.dev) built with Hugo and the Blowfish theme. The site features a modern, responsive design with dark/light mode support and is optimized for personal branding and professional presentation.

## Architecture

- **Hugo Static Site Generator**: Uses Hugo v0.148.2+ with extended features
- **Theme**: Blowfish theme (git submodule in `themes/blowfish/`)
- **Configuration**: Split into multiple TOML files in `config/_default/`
- **Content Structure**: Markdown-based content with YAML front matter
- **Responsive Design**: Built with Tailwind CSS through the theme
- **Multi-language Ready**: Currently configured for English but supports i18n

## Key Files & Directories

- `config/_default/` - Hugo configuration split into logical files:
  - `hugo.toml` - Main Hugo settings, baseURL, taxonomies, and related content
  - `params.toml` - Theme-specific parameters and layout settings
  - `languages.en.toml` - Site title, author information, and social links
  - `menus.en.toml` - Navigation menu structure
  - `markup.toml` - Markdown rendering configuration
  - `module.toml` - Hugo module configuration for the theme
- `content/` - All site content in Markdown format:
  - `_index.md` - Homepage content
  - `authors/msegoviadev/_index.md` - Author profile with social links
- `themes/blowfish/` - Theme files (installed as git submodule, do not edit directly)
- `static/` - Static assets served directly
- `public/` - Generated site output (ignored in git)

## Development Commands

Essential commands for development:

```bash
# Start development server with draft content and log to file
hugo server --buildDrafts > logs/hugo-server.log 2>&1 &

# Start development server (production-like)
hugo server

# Build site for production
hugo

# Update theme submodule
git submodule update --remote --merge

# Check Hugo version (requires v0.87.0+)
hugo version

# View server logs in real-time
tail -f logs/hugo-server.log
```

## Development Server Logs

The Hugo development server logs are captured in `logs/hugo-server.log` when running with the recommended command. The frontend-improvement-lead agent monitors this file for:
- Build errors and warnings
- Template compilation issues
- Asset processing problems
- Performance metrics
- Hot-reload status

## Specialized Agents

This repository is configured to work with specialized Claude Code agents that should be used for specific tasks:

### frontend-improvement-lead
Use this agent for:
- **Implementing new features and improvements** - Adding sections, pages, or functionality
- **Fixing frontend issues** - Layout problems, responsive design issues, theme configuration
- **Content structure improvements** - Organizing and optimizing site content
- **Theme customization and styling** - Working within Blowfish theme constraints

## Theme Configuration

- **Homepage Layout**: Currently set to "profile" layout in `params.toml`
- **Color Scheme**: Uses "blowfish" color scheme with auto-switching appearance
- **Social Links**: Configured in `languages.en.toml` under `[params.author]`
- **SEO**: Built-in optimization with customizable meta tags and social sharing
- **Analytics**: Supports multiple analytics providers (currently disabled)

## Content Management

### Author Profile
The main author profile is in `content/authors/msegoviadev/_index.md` and `config/_default/languages.en.toml`. Update both locations to maintain consistency:
- Personal bio and headline
- Social media links (GitHub, LinkedIn, email)
- Profile image reference

### Adding Content
- **Blog Posts**: Create in `content/posts/` directory
- **Pages**: Create in appropriate content subdirectories
- **Authors**: Add to `content/authors/` for multi-author support

## Deployment

The site deploys to GitHub Pages using the custom domain msegovia.dev (configured in CNAME file). After making changes:
1. Test locally with `hugo server --buildDrafts`
2. Build with `hugo` to ensure no errors
3. Commit and push to master branch
4. GitHub Pages will automatically rebuild and deploy

## Theme Documentation

Full Blowfish theme documentation: https://blowfish.page/docs/