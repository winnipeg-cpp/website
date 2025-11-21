# Winnipeg C++ Developers

Welcome to the Winnipeg C++ Developers user group website repository! This is the source code for our community website where we share meetup announcements, technical articles, and resources for C++ developers in Winnipeg.

💻 **GitHub:** [github.com/winnipeg-cpp](https://github.com/winnipeg-cpp)


## About This Repository

This website is built with [Hugo](https://gohugo.io/), a fast static site generator. The site features:

- Monthly meetup announcements
- Technical articles and tutorials
- Community resources
- Event photos and recaps

## Contributing

We welcome contributions! Here's how you can help:

### Adding Content

**For meetup organizers and contributors:**

1. **Clone the repository:**
   ```bash
   git clone https://github.com/winnipeg-cpp/website.git
   cd website
   ```

2. **Create a branch:**
   ```bash
   git checkout -b content/your-content-name
   ```

3. **Create a new post:**
   ```bash
   # Monthly meetup announcement
   hugo new --kind meetup posts/2025/2025-12/2025-12-meetup.md
   
   # Technical article
   hugo new --kind technical posts/2025/2025-12/2025-12-15-article-title.md
   ```

4. **Preview your changes:**
   ```bash
   hugo server -D
   ```
   Open http://localhost:1313/ to see your changes

5. **Submit a pull request:**
   ```bash
   git add .
   git commit -m "Add December meetup announcement"
   git push -u origin content/your-content-name
   ```

See **[docs/CONTENT_GUIDE.md](docs/CONTENT_GUIDE.md)** for detailed content creation instructions.

### Development Setup

**Prerequisites:**
- [Hugo Extended](https://gohugo.io/installation/) (latest version)
- Git

**Quick Start:**
```bash
# Clone and preview
git clone https://github.com/winnipeg-cpp/website.git
cd website
hugo server
```

## Documentation

- **[docs/CONTENT_GUIDE.md](docs/CONTENT_GUIDE.md)** - How to create and organize posts
- **[docs/NEWSLETTER_SETUP.md](docs/NEWSLETTER_SETUP.md)** - How to set up email newsletter subscriptions
- **[AGENTS.md](AGENTS.md)** - Repository conventions and guidelines

## Project Structure

```
website/
├── content/posts/        # Blog posts organized by year/month
├── static/images/        # Images and media files
├── archetypes/           # Post templates (meetup, announcement, technical)
├── docs/                 # Documentation
├── hugo.toml             # Site configuration
└── themes/PaperMod/      # Hugo theme
```
