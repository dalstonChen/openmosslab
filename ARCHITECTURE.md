# OpenMoss Lab Website - Architecture Overview

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Content Authors                          │
│              (Edit Markdown files in _content/)              │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ Edit & Commit
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Git Repository                            │
│                   (GitHub: main branch)                      │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ Push triggers
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                  GitHub Actions Workflow                     │
│  ┌───────────────────────────────────────────────────────┐  │
│  │  1. Checkout repository                               │  │
│  │  2. Setup Ruby environment                            │  │
│  │  3. Install Jekyll & dependencies (bundle install)    │  │
│  │  4. Build site (jekyll build)                         │  │
│  │  5. Generate static HTML in _site/                    │  │
│  │  6. Deploy to GitHub Pages                            │  │
│  └───────────────────────────────────────────────────────┘  │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ Deploy
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    GitHub Pages (CDN)                        │
│              (Static HTML hosted globally)                   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ Access via HTTPS
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                      End Users                               │
│              (View website in browser)                       │
└─────────────────────────────────────────────────────────────┘
```

## File Processing Flow

```
Content (Markdown) ──┐
                     │
Layouts (HTML) ──────┤
                     ├──> Jekyll Engine ──> Static HTML ──> _site/
Config (YAML) ───────┤
                     │
Assets (CSS/JS) ─────┘
```

## Directory Structure Explained

```
openmosslab/
│
├── Configuration Layer
│   ├── _config.yml           # Site-wide settings
│   ├── Gemfile               # Ruby dependencies
│   └── .gitignore            # Version control exclusions
│
├── Content Layer (Markdown)
│   ├── index.md              # Homepage content
│   └── _content/             # All other page content
│       ├── people.md
│       ├── publications.md
│       ├── software.md
│       ├── resources.md
│       ├── career.md
│       └── join.md
│
├── Presentation Layer (HTML/Liquid)
│   ├── _layouts/             # Page templates
│   │   ├── default.html      # Base template
│   │   ├── home.html         # Homepage template
│   │   └── page.html         # Content page template
│   │
│   └── _includes/            # Reusable components
│       ├── header.html       # Navigation bar
│       └── footer.html       # Footer
│
├── Style Layer (CSS)
│   └── assets/
│       └── css/
│           └── main.css      # Custom styles
│
├── Media Layer
│   └── assets/
│       └── img/              # Images and logos
│
├── Deployment Layer
│   └── .github/
│       └── workflows/
│           └── deploy.yml    # CI/CD pipeline
│
└── Documentation Layer
    ├── README.md             # Quick overview
    ├── SETUP.md              # Detailed setup guide
    ├── QUICKSTART.md         # Quick start checklist
    ├── PROJECT_SUMMARY.md    # Comprehensive summary
    └── ARCHITECTURE.md       # This file
```

## Component Interaction

### 1. Content to HTML Flow

```
┌──────────────┐
│ Markdown     │
│ (.md files)  │
└──────┬───────┘
       │
       │ Front matter specifies layout
       ▼
┌──────────────┐
│ Layout       │
│ (HTML+Liquid)│
└──────┬───────┘
       │
       │ Includes components
       ▼
┌──────────────┐
│ Includes     │
│ (header,     │
│  footer)     │
└──────┬───────┘
       │
       │ Jekyll processes
       ▼
┌──────────────┐
│ Static HTML  │
│ in _site/    │
└──────────────┘
```

### 2. Layout Hierarchy

```
default.html (base template)
    │
    ├── Includes: header.html
    │
    ├── Content area:
    │   │
    │   ├── home.html (extends default)
    │   │   └── index.md content
    │   │
    │   └── page.html (extends default)
    │       └── _content/*.md files
    │
    └── Includes: footer.html
```

### 3. Navigation System

```
_config.yml (navigation array)
         │
         ▼
_includes/header.html (loops through navigation)
         │
         ▼
Generated nav menu on every page
```

## Build Process Details

### Local Development Build

```bash
bundle exec jekyll serve
```

1. **Read Configuration**: Load `_config.yml`
2. **Process Content**: Convert Markdown to HTML
3. **Apply Layouts**: Wrap content in templates
4. **Render Liquid**: Process template variables and logic
5. **Copy Assets**: Move CSS, JS, images to `_site/`
6. **Generate Site**: Create complete static site
7. **Serve Locally**: Run development server
8. **Watch Files**: Auto-rebuild on changes

### Production Build (GitHub Actions)

```yaml
# .github/workflows/deploy.yml
jobs:
  build:
    - Checkout code
    - Setup Ruby
    - Install dependencies
    - Build with Jekyll
    - Upload artifact

  deploy:
    - Deploy to GitHub Pages
```

## Data Flow

### User Request Flow

```
User Browser
    │
    │ HTTPS GET request
    ▼
GitHub Pages CDN
    │
    │ Serve static HTML
    ▼
HTML Page
    │
    ├── Load CSS from assets/
    ├── Load JS from CDN (Bootstrap, jQuery)
    ├── Load images from assets/
    └── Load fonts from Google Fonts
    │
    ▼
Rendered Page in Browser
```

### Content Update Flow

```
Author edits Markdown
    │
    ▼
Git commit & push
    │
    ▼
GitHub detects push to main
    │
    ▼
Trigger GitHub Actions workflow
    │
    ▼
Run Jekyll build
    │
    ▼
Deploy to GitHub Pages
    │
    ▼
CDN updates (2-3 minutes)
    │
    ▼
Users see updated content
```

## Security Model

```
┌─────────────────────────────────────────┐
│ No Server-Side Code                      │
│ ✓ No PHP, no Node.js, no Python          │
│ ✓ Static HTML only                       │
│ ✓ No database queries                    │
│ ✓ No user input processing               │
└─────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ GitHub Infrastructure                    │
│ ✓ HTTPS enforced                         │
│ ✓ DDoS protection                        │
│ ✓ Automatic security updates            │
└─────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ Content Security                         │
│ ✓ Version controlled                     │
│ ✓ Review via pull requests              │
│ ✓ Audit trail in Git history            │
└─────────────────────────────────────────┘
```

## Performance Optimizations

### Static Generation
- **No runtime processing**: HTML pre-generated
- **Fast delivery**: Static files from CDN
- **Caching friendly**: Content rarely changes

### Asset Delivery
- **CDN resources**: Bootstrap, jQuery from CDNs
- **Optimized CSS**: Single custom CSS file
- **Lazy loading**: Images load on demand

### Build Optimization
- **Incremental builds**: Only changed files rebuild (local dev)
- **Compressed output**: Minified HTML in production
- **Parallel processing**: Jekyll uses multiple cores

## Scalability

### Traffic Handling
- **GitHub Pages CDN**: Globally distributed
- **Static content**: No server load
- **Unlimited reads**: No query limits

### Content Growth
- **Unlimited pages**: Add as many as needed
- **Large files**: Images, PDFs supported
- **Build time**: Scales linearly with content

## Deployment Strategies

### Current: Continuous Deployment
```
Edit → Commit → Push → Auto-deploy
```

### Alternative: Staging Environment
```
Edit → Commit → Push to 'staging' branch
Test staging site
Merge to 'main' → Deploy to production
```

### Alternative: Manual Approval
```
Edit → Commit → Push → Create PR
Review → Approve → Merge → Deploy
```

## Backup & Recovery

### Version Control
- **Full history**: Git tracks all changes
- **Rollback capability**: Revert to any previous version
- **Branch protection**: Prevent accidental deletions

### Recovery Process
```bash
# View history
git log

# Revert to previous version
git revert <commit-hash>

# Or reset to specific commit
git reset --hard <commit-hash>
git push --force
```

## Monitoring

### Build Status
- GitHub Actions provides build logs
- Email notifications on failure
- Badge in README shows status

### Site Availability
- GitHub Pages uptime: 99.9%+
- Status page: https://www.githubstatus.com

### Analytics (Optional)
- Add Google Analytics to `_layouts/default.html`
- Track page views, user behavior
- Monitor performance metrics

## Development Workflow

### Feature Development
```
main branch (production)
    │
    └── feature branch
          │
          ├── develop locally
          ├── test changes
          ├── commit
          └── create PR
                │
                └── review → merge → deploy
```

### Content Updates
```
main branch
    │
    ├── edit _content/*.md
    ├── commit with message
    └── push → auto-deploy
```

## Technology Stack Details

### Core Technologies
- **Jekyll 4.3.3**: Static site generator
- **Ruby 3.x**: Programming language
- **Liquid**: Template language
- **Kramdown**: Markdown processor

### Front-end
- **Bootstrap 3**: CSS framework
- **jQuery 1.12.4**: JavaScript library
- **Font Awesome 4.7**: Icon library
- **Google Fonts**: Typography

### Build Tools
- **Bundler**: Ruby dependency management
- **GitHub Actions**: CI/CD pipeline

### Hosting
- **GitHub Pages**: Static site hosting
- **GitHub CDN**: Global content delivery

## Extension Points

### Adding Features
1. **New page type**: Create new layout in `_layouts/`
2. **Custom component**: Add to `_includes/`
3. **Style variations**: Extend `assets/css/main.css`
4. **JavaScript**: Add to `assets/js/`

### Plugins
Jekyll supports plugins via `_plugins/` directory or Gemfile:
```ruby
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
end
```

### Third-party Integrations
- **Analytics**: Google Analytics, Plausible
- **Search**: Algolia, Lunr.js
- **Forms**: Formspree, Netlify Forms
- **Comments**: Disqus, utterances

## Best Practices

### Content Organization
- One topic per file
- Consistent naming conventions
- Logical directory structure

### Code Organization
- Reusable components in `_includes/`
- Template inheritance via layouts
- CSS variables for theming

### Version Control
- Descriptive commit messages
- Atomic commits (one logical change)
- Branch for significant changes

### Performance
- Optimize images before uploading
- Use CDN for common libraries
- Minimize custom CSS/JS

## Troubleshooting Guide

### Build Fails
1. Check syntax in Markdown files
2. Validate YAML front matter
3. Test locally: `bundle exec jekyll build`
4. Review GitHub Actions logs

### Style Issues
1. Hard refresh browser (Ctrl+F5)
2. Check CSS syntax
3. Verify file paths
4. Test in multiple browsers

### Content Not Updating
1. Verify changes committed
2. Check build success in Actions
3. Wait for CDN propagation
4. Clear browser cache

---

This architecture provides a solid foundation for a maintainable, scalable, and performant academic lab website with clean separation of concerns and automated deployment.
