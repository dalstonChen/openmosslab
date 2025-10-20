# OpenMoss Lab Website - Project Summary

## Overview

A static website for the OpenMoss Lab at Fudan University, built with Jekyll and automatically deployed via GitHub Actions. The design replicates the Stanford NLP Group website with complete separation between content and presentation.

## Key Features

### 1. Content-Presentation Separation
- **Content**: All text stored in Markdown files (`_content/*.md` and `index.md`)
- **Presentation**: HTML templates in `_layouts/` and `_includes/`
- **Styling**: CSS in `assets/css/main.css`
- **Configuration**: Site settings in `_config.yml`

### 2. Easy Content Management
- Edit Markdown files to update content
- No HTML or CSS knowledge required for content updates
- Version controlled with Git for full history and rollback capability

### 3. Automatic Deployment
- GitHub Actions workflow triggers on content changes
- Builds and deploys to GitHub Pages automatically
- Typical deployment time: 2-3 minutes

### 4. Modern Static Site Architecture
- Fast loading times (static HTML)
- Secure (no server-side code)
- SEO-friendly (semantic HTML, clean URLs)
- Responsive design (mobile-friendly)

## Project Structure

```
openmosslab/
│
├── _config.yml                 # Jekyll configuration and site settings
├── index.md                    # Homepage content (Markdown)
│
├── _content/                   # Content files (Markdown)
│   ├── people.md              # Faculty and students page
│   ├── publications.md        # Publications page
│   ├── software.md            # Software and tools page
│   ├── resources.md           # Resources page
│   ├── career.md              # Career opportunities page
│   └── join.md                # Join the lab page
│
├── _layouts/                   # HTML templates
│   ├── default.html           # Base layout (header, footer, structure)
│   ├── home.html              # Homepage-specific layout
│   └── page.html              # Standard page layout
│
├── _includes/                  # Reusable HTML components
│   ├── header.html            # Navigation bar
│   └── footer.html            # Footer with contact info
│
├── assets/                     # Static assets
│   ├── css/
│   │   └── main.css           # Custom styles (Stanford NLP inspired)
│   ├── js/                    # JavaScript files
│   └── img/                   # Images
│       └── logos/             # Logo files
│           └── README.md      # Logo guidelines
│
├── .github/
│   └── workflows/
│       └── deploy.yml         # GitHub Actions deployment workflow
│
├── Gemfile                     # Ruby dependencies
├── .gitignore                 # Git ignore patterns
├── README.md                  # Project documentation
├── SETUP.md                   # Detailed setup and deployment guide
└── PROJECT_SUMMARY.md         # This file
```

## Technology Stack

### Core
- **Jekyll 4.3.3**: Static site generator
- **Liquid**: Template language
- **Kramdown**: Markdown processor
- **Bootstrap 3**: CSS framework
- **jQuery**: JavaScript library

### Build & Deploy
- **Ruby 3.x**: Programming language
- **Bundler**: Dependency management
- **GitHub Actions**: CI/CD pipeline
- **GitHub Pages**: Hosting platform

### Styling
- **Custom CSS**: Based on Stanford NLP design
- **Google Fonts**: Open Sans typography
- **Font Awesome**: Icons
- **Responsive Design**: Mobile-first approach

## Design Philosophy

### Visual Design
- **Color Scheme**: Red theme inspired by Stanford (#8C1515 primary)
- **Typography**: Open Sans for readability
- **Layout**: Clean, academic aesthetic
- **Grid System**: Bootstrap 3 responsive grid
- **Components**: Cards for people, highlighted sections for content

### User Experience
- **Navigation**: Fixed top navbar with consistent menu
- **Hierarchy**: Clear page structure with semantic HTML
- **Accessibility**: Semantic markup, alt text, keyboard navigation
- **Performance**: Optimized static files, CDN resources

## Content Pages

### 1. Homepage (`index.md`)
- Welcome message
- Lab mission and achievements
- Research interests overview
- Call-to-action links

### 2. People (`_content/people.md`)
- Faculty listings with roles
- Research staff
- Current students
- Alumni with achievements

### 3. Publications (`_content/publications.md`)
- Recent publications
- Notable projects (MOSS, FudanNLP, etc.)
- Links to external profiles

### 4. Software (`_content/software.md`)
- Open source projects
- Research tools
- Documentation links
- Community information

### 5. Resources (`_content/resources.md`)
- Learning materials
- Technical guides
- Research resources
- Advising information

### 6. Career (`_content/career.md`)
- Postdoc positions
- Graduate admissions
- Research assistant positions
- Application instructions

### 7. Join (`_content/join.md`)
- Why join the lab
- Lab culture
- Application requirements
- How to apply

## Deployment Workflow

### Automatic Deployment Process

1. **Developer/Content Editor** makes changes to content files
2. **Commits and pushes** to `main` branch on GitHub
3. **GitHub Actions** detects changes to specified paths
4. **Build Job** runs:
   - Checks out repository
   - Sets up Ruby environment
   - Installs dependencies with Bundler
   - Runs Jekyll build
   - Generates static site in `_site/`
5. **Deploy Job** runs:
   - Uploads built site as artifact
   - Deploys to GitHub Pages
6. **Live Site** updates at configured URL

### Deployment Triggers

The workflow triggers on changes to:
- `_content/**` - Any content Markdown files
- `index.md` - Homepage content
- `_layouts/**` - Layout templates
- `_includes/**` - Reusable components
- `assets/**` - CSS, JS, images
- `_config.yml` - Site configuration
- `.github/workflows/deploy.yml` - Workflow itself

### Manual Deployment

Can also be triggered manually via GitHub Actions UI ("workflow_dispatch").

## Content Management Workflow

### For Content Editors (Non-Technical)

1. **Navigate** to `_content/` folder
2. **Edit** the relevant `.md` file
3. **Commit** with descriptive message
4. **Push** to `main` branch
5. **Wait** 2-3 minutes for deployment

### For Developers

1. **Create branch** for changes
2. **Test locally** with `bundle exec jekyll serve`
3. **Commit** changes
4. **Create pull request**
5. **Review and merge** to `main`
6. **Automatic deployment** follows

## Customization Guide

### Changing Colors

Edit CSS variables in `assets/css/main.css`:

```css
:root {
  --primary-color: #8C1515;
  --primary-dark: #6B0F0F;
  /* ... other colors ... */
}
```

### Modifying Navigation

Edit `_config.yml`:

```yaml
navigation:
  - title: "people"
    url: "/people/"
  - title: "new page"
    url: "/newpage/"
```

### Adding Pages

1. Create `_content/newpage.md`
2. Add front matter and content
3. Add to navigation in `_config.yml`
4. Commit and push

### Updating Layouts

Edit files in `_layouts/` and `_includes/` to change HTML structure.

## Advantages of This Architecture

### Content Management
✅ Non-technical users can edit content
✅ Markdown is easy to learn and use
✅ Version control provides history and rollback
✅ No database or CMS complexity

### Performance
✅ Static files load instantly
✅ CDN delivery for Bootstrap, jQuery, fonts
✅ No server-side processing
✅ Scalable to high traffic

### Security
✅ No server-side code to exploit
✅ No database vulnerabilities
✅ No plugin security issues
✅ HTTPS by default on GitHub Pages

### Maintenance
✅ Automatic deployments
✅ No server to maintain
✅ Free hosting on GitHub Pages
✅ Simple backup (Git repository)

### Development
✅ Local development environment
✅ Template reusability
✅ Clean separation of concerns
✅ Easy to customize

## Requirements

### For Content Editing
- Git (basic knowledge)
- Text editor
- GitHub account

### For Development
- Ruby 3.0+
- Bundler
- Git
- Text editor or IDE
- Command line familiarity

### For Deployment
- GitHub repository
- GitHub Pages enabled
- GitHub Actions enabled (default)

## Maintenance Tasks

### Regular
- Update content in Markdown files
- Add new publications, people, software
- Review and merge pull requests

### Periodic
- Update dependencies: `bundle update`
- Review and update documentation
- Check for broken links
- Update images and media

### Occasional
- Design updates (CSS changes)
- Add new features or pages
- Restructure content
- Performance optimization

## Best Practices

### Content
- Use descriptive commit messages
- Test locally before pushing
- Keep content organized and consistent
- Use proper Markdown formatting

### Development
- Create branches for major changes
- Test thoroughly before merging
- Document customizations
- Keep dependencies updated

### Collaboration
- Pull before making changes
- Use pull requests for review
- Communicate about deployments
- Maintain documentation

## Future Enhancements

### Potential Additions
- Publication database with filtering
- News/blog section
- Photo gallery
- Search functionality
- Multi-language support
- RSS feed for updates

### Technical Improvements
- Asset optimization pipeline
- Automated testing
- Performance monitoring
- Analytics integration
- SEO enhancements

## Support Resources

### Documentation
- [Jekyll Docs](https://jekyllrb.com/docs/)
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Bootstrap 3 Docs](https://getbootstrap.com/docs/3.4/)

### Project Files
- `README.md` - Project overview and quick start
- `SETUP.md` - Detailed setup and deployment guide
- `PROJECT_SUMMARY.md` - This comprehensive document

## License

© 2025 OpenMoss Lab, Fudan University

## Contact

For questions or support:
- Technical: Create GitHub issue
- Content: xpqiu@fudan.edu.cn
