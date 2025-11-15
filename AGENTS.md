# AGENTS.md

## Build/Lint/Test Commands
- **Build site**: `hugo`
- **Dev server**: `hugo server --buildDrafts`
- **Theme assets**: `cd themes/blowfish && npm run build`
- **Format code**: `cd themes/blowfish && npx prettier --write .`
- **No tests**: This is a static site with no test suite

## Code Style Guidelines
- **Formatting**: Prettier with custom config (2 spaces, double quotes, semicolons)
- **Hugo templates**: Go template syntax with bracket spacing
- **Markdown**: Standard with TOML front matter (+++ delimiters)
- **Naming**: kebab-case for files, camelCase for JS variables
- **Imports**: Group by type, standard library first
- **Error handling**: Graceful degradation in templates
- **Comments**: Minimal, self-documenting code preferred