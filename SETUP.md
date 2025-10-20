# OpenMoss Lab Website - Setup and Deployment Guide

## Overview

This website is built using Jekyll, a static site generator that converts Markdown content into HTML. The key advantage is the complete separation of content from presentation:

- **Content editors** only need to edit Markdown files
- **Design changes** only require editing CSS and HTML templates
- **Automated deployment** via GitHub Actions whenever content changes

## Quick Start

### For Content Editors (Non-Technical)

If you only want to update content:

1. Navigate to the `_content/` folder or edit `index.md`
2. Edit the Markdown (.md) files
3. Commit and push changes to GitHub
4. Wait 2-3 minutes for automatic deployment

That's it! No need to touch HTML, CSS, or run any commands.

### For Developers

See the sections below for local development and customization.

## Prerequisites

Before you begin, ensure you have:

- **Git**: For version control
- **Ruby** (version 3.0 or higher): [Install Ruby](https://www.ruby-lang.org/en/documentation/installation/)
- **Bundler**: Ruby dependency manager (install with `gem install bundler`)
- **A text editor**: VS Code, Sublime Text, or any editor you prefer

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/openmosslab.git
cd openmosslab
```

### 2. Install Dependencies

```bash
bundle install
```

This installs Jekyll and all required plugins.

### 3. Run Local Development Server

```bash
bundle exec jekyll serve
```

The site will be available at `http://localhost:4000`

The server watches for file changes and automatically rebuilds (except for `_config.yml` changes, which require a restart).

### 4. Build for Production

```bash
bundle exec jekyll build
```

This generates the static site in the `_site/` directory.

## GitHub Pages Deployment

### Initial Setup

1. **Create a GitHub repository** for your website
2. **Push your code** to the repository
3. **Enable GitHub Pages**:
   - Go to repository Settings → Pages
   - Source: "GitHub Actions"
4. **First push** triggers the deployment workflow

### Automatic Deployment

The GitHub Actions workflow (`.github/workflows/deploy.yml`) automatically:

1. Detects changes to content files, layouts, or assets
2. Builds the Jekyll site
3. Deploys to GitHub Pages

**Deployment triggers when you modify:**
- Any Markdown content in `_content/`
- The homepage `index.md`
- Layouts in `_layouts/`
- Includes in `_includes/`
- Assets (CSS, JS, images)
- Site configuration `_config.yml`

**Typical deployment time:** 2-3 minutes after pushing to `main` branch

### Checking Deployment Status

1. Go to your repository on GitHub
2. Click the "Actions" tab
3. View the latest workflow run
4. Green checkmark = successful deployment
5. Red X = build failed (check logs for errors)

## Content Management

### File Structure

```
_content/
├── people.md         # Faculty and students
├── publications.md   # Research papers
├── software.md       # Open source projects
├── resources.md      # Learning resources
├── career.md         # Job postings
└── join.md          # Application info

index.md              # Homepage
```

### Editing Content

1. **Open the relevant Markdown file**
2. **Edit using Markdown syntax**:

```markdown
# Heading 1
## Heading 2
### Heading 3

**Bold text**
*Italic text*

- List item 1
- List item 2

[Link text](https://example.com)

![Image alt text](/path/to/image.jpg)
```

3. **Save and commit**:

```bash
git add _content/people.md
git commit -m "Update faculty list"
git push
```

4. **Wait for deployment** (2-3 minutes)

### Front Matter

Each Markdown file starts with front matter (YAML):

```yaml
---
layout: page
title: Page Title
permalink: /url-path/
---
```

- `layout`: Template to use (usually "page" or "home")
- `title`: Page title shown in the browser tab and page header
- `permalink`: URL path for the page

### Adding New Pages

1. **Create a new file** in `_content/`:

```bash
touch _content/newpage.md
```

2. **Add front matter and content**:

```markdown
---
layout: page
title: New Page
permalink: /newpage/
---

## Your Content Here

Add your content using Markdown.
```

3. **Add to navigation** in `_config.yml`:

```yaml
navigation:
  - title: "new page"
    url: "/newpage/"
```

4. **Commit and push**

## Design Customization

### Changing Colors

Edit `assets/css/main.css` at the top:

```css
:root {
  --primary-color: #8C1515;      /* Main brand color */
  --primary-dark: #6B0F0F;       /* Darker variant */
  --accent-color: #B83A4B;       /* Accent color */
  --text-color: #2e2d29;         /* Body text */
  --text-light: #5e5e5e;         /* Secondary text */
  --bg-light: #f7f7f7;           /* Light background */
  --bg-highlight: #fafafa;       /* Highlighted sections */
  --border-color: #e0e0e0;       /* Borders */
}
```

### Modifying Layout

Edit files in `_layouts/`:

- `default.html`: Base template (header, footer, structure)
- `home.html`: Homepage-specific layout
- `page.html`: Standard page layout

### Updating Header/Footer

- **Header**: Edit `_includes/header.html`
- **Footer**: Edit `_includes/footer.html`

### Adding Images

1. **Place images** in `assets/img/`
2. **Reference in Markdown**:

```markdown
![Description](/assets/img/filename.jpg)
```

Or in HTML templates:

```html
<img src="{{ '/assets/img/filename.jpg' | relative_url }}" alt="Description">
```

## Configuration

### Site Settings

Edit `_config.yml` to change:

```yaml
title: "OpenMoss Lab"
description: "Lab description"
url: "https://yourusername.github.io"
baseurl: ""  # Leave empty for user/org pages

organization:
  name: "OpenMoss Lab"
  email: "contact@example.com"
```

### Navigation Menu

```yaml
navigation:
  - title: "people"
    url: "/people/"
  - title: "publications"
    url: "/publications/"
```

## Troubleshooting

### Build Fails on GitHub Actions

1. **Check the Actions tab** for error messages
2. **Common issues**:
   - Syntax error in Markdown or YAML
   - Missing front matter
   - Invalid permalink
3. **Test locally** first with `bundle exec jekyll build`

### Changes Not Showing Up

1. **Hard refresh** your browser (Ctrl+F5 or Cmd+Shift+R)
2. **Check deployment status** in Actions tab
3. **Verify you pushed** to the correct branch
4. **Check for build errors** in workflow logs

### Local Server Not Working

```bash
# Update dependencies
bundle update

# Clean and rebuild
bundle exec jekyll clean
bundle exec jekyll serve
```

### Ruby Version Issues

```bash
# Check Ruby version
ruby --version

# Should be 3.0 or higher
# If not, install Ruby via rbenv or RVM
```

## Maintenance

### Regular Updates

```bash
# Update Jekyll and plugins
bundle update

# Commit the updated Gemfile.lock
git add Gemfile.lock
git commit -m "Update dependencies"
git push
```

### Backup

Your content is version-controlled with Git, so every change is backed up automatically. GitHub also maintains history of all changes.

## Content Workflow Example

### Scenario: Adding a New Faculty Member

1. **Edit** `_content/people.md`:

```markdown
### New Faculty Name
**Assistant Professor**
[Personal Website](https://example.com)
```

2. **Save and test locally**:

```bash
bundle exec jekyll serve
# Visit http://localhost:4000/people/
```

3. **Commit and push**:

```bash
git add _content/people.md
git commit -m "Add new faculty member"
git push origin main
```

4. **Monitor deployment**:
   - Go to GitHub Actions tab
   - Watch the workflow complete
   - Visit your live site to verify

## Best Practices

### Content Management

- **Use descriptive commit messages**: "Add Q2 2025 publications" not "update"
- **Test locally first**: Catch errors before pushing
- **Keep content organized**: One topic per file
- **Use consistent formatting**: Follow existing Markdown style

### Development

- **Never commit `_site/`**: It's generated automatically
- **Use branches** for major changes
- **Document custom features**: Add notes to README
- **Keep dependencies updated**: Run `bundle update` monthly

### Collaboration

- **Pull before editing**: Get latest changes first
- **Coordinate large changes**: Discuss with team
- **Review before merging**: Use pull requests for important updates
- **Communicate deployments**: Let team know when site will rebuild

## Support

### Getting Help

- **Jekyll Documentation**: https://jekyllrb.com/docs/
- **Markdown Guide**: https://www.markdownguide.org/
- **GitHub Pages Docs**: https://docs.github.com/en/pages
- **Bootstrap 3 Docs**: https://getbootstrap.com/docs/3.4/

### Contact

For questions about this website:
- **Technical issues**: Check GitHub Issues
- **Content questions**: Contact xpqiu@fudan.edu.cn

## License

© OpenMoss Lab, Fudan University
