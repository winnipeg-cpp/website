# Repository Guidelines

## Project Structure & Module Organization
This Hugo site keeps Markdown source in `content/`, organized chronologically in year/month folders (e.g., `content/posts/2025/2025-11/`). New posts should use archetypes (`hugo new --kind <type> posts/YYYY/YYYY-MM/<filename>.md`), which pre-populate TOML front matter and content structure. Available archetypes: `meetup`, `announcement`, `technical`, and `default`. Theme-specific templates live in `themes/terminal/`; add custom overrides under `layouts/` instead of editing theme files directly. Static assets (images, downloads) belong in `static/` organized in subdirectories (e.g., `static/images/`, `static/downloads/`); reference them in posts with `/images/photo.jpg`. Pipeline-ready SCSS or JS goes in `assets/`. The `public/` directory is build output and should not be hand-edited; treat `resources/` as Hugo's cache.

## Build, Test, and Development Commands
- `hugo server -D`: Run the local preview with drafts enabled and live reload. Use `-p 1313` if you need a different port.
- `hugo server -D --buildFuture`: Preview drafts AND future-dated posts (useful before publishing scheduled content).
- `hugo`: Produce a production build into `public/` using the configuration in `hugo.toml`.
- `hugo --gc --minify`: Clean unused resources and emit a minified build before releasing.

**Note:** Hugo won't display posts with future dates by default. Set the site timezone in `hugo.toml` with `timeZone = 'America/Winnipeg'`.

## Coding Style & Naming Conventions
Keep Markdown headings incremental (`#`, `##`, …) and wrap paragraphs at ~100 characters for readability. Use TOML front matter delimited by `+++`, keeping keys alphabetical (`title`, `date`, `draft`, etc.) and dates in ISO-8601 with offset. 

**Post naming conventions:**
- Meetup posts: `YYYY-MM-meetup.md` (one per month)
- Announcements: `YYYY-MM-DD-announcement-<topic>.md`
- Technical posts: `YYYY-MM-DD-<slug>.md`

Posts live in year/month folders (`content/posts/2025/2025-11/`) but URLs remain clean (`/posts/2025-11-meetup/`). When authoring Go templates, prefer two-space indentation and rely on partials or blocks that already exist in the Terminal theme.

## Testing Guidelines
Run `hugo server` and inspect pages in multiple viewport sizes before opening a pull request. Check console output for warnings about missing shortcodes or layout errors. After `hugo --gc --minify`, spot-check the generated `public/index.html` and any new pages to confirm assets resolve and metadata is correct. If you add custom scripts or CSS, validate that the minified build still behaves as expected.

## Commit & Pull Request Guidelines
Follow the short, imperative style used in the history (`Add ...`, `Update ...`) and keep commits scoped to a single change. Reference related issues in the commit body or PR description using `Fixes #ID` when applicable. Pull requests should outline the change, list verification steps (commands run, browsers checked), and include screenshots for visual updates. Avoid committing generated output (`public/`, `resources/`) unless a release workflow explicitly requires it.

## Safety and secrets
- Never add secrets to git (tokens, passwords, private keys).
- If a secret is suspected in history, stop and rotate the secret before trying to "remove it from git".
- Avoid running untrusted scripts (especially curl-to-shell patterns).

## Content Workflow
Generate new posts with `hugo new --kind <type> posts/YYYY/YYYY-MM/<filename>.md` using the appropriate archetype (meetup, announcement, technical). Hugo creates the folder structure automatically and populates templates with placeholders. Edit the generated file to fill in bracketed placeholders. Toggle `draft = false` only once the copy, links, and assets have been proofed. For scheduled posts, set `publishDate` in the front matter so the page remains hidden until release.

When adding a new item, review the last 2-3 similar items in `content/` and stick with the established structure and tone.

For detailed instructions on creating content, see **[docs/CONTENT_GUIDE.md](docs/CONTENT_GUIDE.md)**.
