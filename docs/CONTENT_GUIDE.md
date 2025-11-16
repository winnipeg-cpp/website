# Quick Reference: Creating New Posts

## Using Archetypes

Hugo archetypes are templates that pre-populate new content with the correct structure and front matter.

### Post Organization and Naming

Posts are organized in folders by year and month for easy management:

```
content/posts/
├── 2025/
│   ├── 2025-11/
│   │   ├── 2025-11-meetup.md
│   │   └── 2025-11-15-welcome-to-winnipeg-cpp.md
│   └── 2025-12/
│       └── 2025-12-meetup.md
└── 2026/
    └── 2026-01/
        └── 2026-01-meetup.md
```

**Naming convention:**
- **Meetup posts**: `YYYY-MM-meetup.md`
- **Announcements**: `YYYY-MM-DD-announcement-<topic>.md`
- **Technical posts**: `YYYY-MM-DD-<slug>.md`

This structure makes it easy to find and manage posts, even with hundreds of them.

### Available Archetypes

#### 1. Meetup Posts
For announcing monthly meetups:
```bash
hugo new --kind meetup posts/2025/2025-12/2025-12-meetup.md
```

This creates a post with:
- Pre-filled event structure (date, time, location, registration)
- Meetup and event tags
- All the standard sections you need

#### 2. Announcements
For general community announcements:
```bash
hugo new --kind announcement posts/2025/2025-11/2025-11-20-announcement-new-venue.md
```

#### 3. Technical Posts
For technical articles, tutorials, or code examples:
```bash
hugo new --kind technical posts/2025/2025-11/2025-11-15-modern-cpp-best-practices.md
```

This includes code block templates and technical tags.

#### 4. Default Posts
For generic content:
```bash
hugo new posts/2025/2025-11/2025-11-15-my-post.md
```

### Workflow

1. **Create the post** using the appropriate archetype in the year/month folder:
   ```bash
   hugo new --kind meetup posts/2026/2026-01/2026-01-meetup.md
   ```
   
   Hugo will automatically create the `2026/2026-01/` folders if they don't exist.

2. **Edit the file** in `content/posts/YYYY/YYYY-MM/` - fill in the placeholder text marked with `[brackets]`

3. **Preview locally**:
   ```bash
   hugo server -D
   ```
   Open http://localhost:1313/ in your browser

4. **Set draft status**:
   - `draft = false` - Post will be published
   - `draft = true` - Post is hidden (use `-D` flag to preview drafts)

5. **Build for production**:
   ```bash
   hugo --gc --minify
   ```

## Best Practices

- Use `kebab-case` for filenames (lowercase with hyphons)
- Meetup posts are just `YYYY-MM-meetup.md` (one per month, location goes in content)
- Hugo automatically creates folders - just use the full path
- URLs are clean and don't include folder structure: `/posts/2026-01-meetup/`
- Date format in front matter: `2025-11-15T21:00:00-06:00` (ISO-8601 with timezone)
- Keep front matter keys alphabetical
- Wrap paragraphs around 100 characters for readability

**Important:** Hugo will NOT display posts with future dates by default. If a post has a date in the future, it won't appear on the site until that date arrives. To preview future posts during development, use `hugo server -D --buildFuture`.

### Pinning Posts

To keep a post at the top of your posts list (like a welcome or important announcement), add `weight` to the front matter:

```toml
+++
date = '2025-11-15T12:00:00-06:00'
draft = false
title = 'Welcome Post'
weight = 1
+++
```

**How weight works:**
- Lower numbers appear first (e.g., `weight = 1` is higher priority than `weight = 10`)
- Posts with weight always appear before posts without weight
- Posts without weight are sorted by date (newest first)
- Use `weight = 1` for your most important pinned post

## Images and Media

Images should be placed in the `static/` directory. Hugo copies everything from `static/` to the root of your published site.

**Recommended structure:**
```
static/
├── images/
│   ├── event.jpeg
│   ├── 2025-11-meetup.jpg
│   └── logos/
│       └── cpp-logo.png
└── downloads/
    └── presentation.pdf
```

**Referencing images in posts:**
```markdown
![Event Photo](/images/event.jpeg)
![Meetup Photo](/images/2025-11-meetup.jpg)
```

The leading `/` refers to the root of your site. Files in `static/images/` are accessible at `/images/` on your website.

## Examples

**Create December 2025 meetup:**
```bash
hugo new --kind meetup posts/2025/2025-12/2025-12-meetup.md
```

**Create January 2026 announcement:**
```bash
hugo new --kind announcement posts/2026/2026-01/2026-01-15-announcement-speaker-call.md
```

**Create technical article:**
```bash
hugo new --kind technical posts/2025/2025-11/2025-11-20-smart-pointers-guide.md
```

**File paths → URLs:**
- `posts/2025/2025-11/2025-11-meetup.md` → `/posts/2025-11-meetup/`
- `posts/2025/2025-11/2025-11-15-announcement-speaker-call.md` → `/posts/2025-11-15-announcement-speaker-call/`
- `posts/2025/2025-12/2025-12-20-move-semantics-explained.md` → `/posts/2025-12-20-move-semantics-explained/`

