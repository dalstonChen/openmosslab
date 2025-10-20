# OpenMoss Lab Website

This is the official website for the OpenMoss Lab at Fudan University, built with Jekyll static site generator.

## Architecture

This website uses a clean separation between content and presentation:

- **Content**: All page content is stored in Markdown files in the `_content/` directory and `index.md`
- **Layout**: HTML templates are in `_layouts/` and reusable components in `_includes/`
- **Styling**: CSS is in `assets/css/main.css`
- **Configuration**: Site settings are in `_config.yml`

## Directory Structure

```
openmosslab/
├── _config.yml              # Jekyll configuration
├── _layouts/                # HTML templates
│   ├── default.html         # Base template
│   ├── home.html           # Homepage template
│   └── page.html           # Content page template
├── _includes/              # Reusable components
│   ├── header.html         # Navigation bar
│   └── footer.html         # Footer
├── _content/               # Markdown content files
│   ├── people.md
│   ├── resources.md
│   ├── career.md
│   └── join.md
├── index.md                # Homepage content
├── assets/
│   ├── css/
│   │   └── main.css       # Custom styles
│   ├── js/                # JavaScript files
│   └── img/               # Images
├── .github/
│   └── workflows/
│       └── deploy.yml     # GitHub Actions deployment
├── Gemfile                 # Ruby dependencies
└── README.md              # This file
```

## Editing Content

### To update page content:

1. Navigate to the appropriate Markdown file in `_content/` or edit `index.md` for the homepage
2. Edit the content using standard Markdown syntax
3. Commit and push your changes
4. GitHub Actions will automatically rebuild and deploy the site

### Adding new pages:

1. Create a new Markdown file in `_content/` with front matter:
   ```yaml
   ---
   layout: page
   title: Your Page Title
   permalink: /your-url/
   ---
   ```
2. Add your content below the front matter
3. Add a link to the navigation in `_config.yml` under the `navigation` section

### Updating faculty/people information:

Edit `_content/people.md` to update the people listings.

### Updating career opportunities:

Edit `_content/career.md` to update job postings and recruitment information.

## Local Development

### Prerequisites:
- Ruby 3.0 or higher
- Bundler

### Setup:

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# View at http://localhost:4000
```

### Building the site:

```bash
bundle exec jekyll build
```

The generated site will be in the `_site/` directory.

## Deployment

This site uses GitHub Actions for automatic deployment:

1. Push changes to the `main` branch
2. GitHub Actions automatically builds the site
3. The built site is deployed to GitHub Pages

### Deployment triggers:
- Any changes to content files in `_content/`
- Changes to `index.md`
- Changes to layouts, includes, or assets
- Changes to `_config.yml`

## Customization

### Colors and Styling

Edit `assets/css/main.css` to customize:
- Color scheme (CSS variables at the top)
- Typography
- Layout and spacing
- Component styles

### Navigation

Edit the `navigation` section in `_config.yml` to add/remove menu items.

### Site Information

Edit `_config.yml` to update:
- Site title and description
- Organization information
- Social media links
- Other site-wide settings

## Design

The design is based on the Stanford Natural Language Processing Group website, featuring:
- Clean, academic aesthetic
- Responsive layout
- Bootstrap 3 grid system
- Red color scheme inspired by Stanford branding
- Professional typography using Open Sans

## License

Content and design © OpenMoss Lab, Fudan University

## Contact

For questions or issues, contact: xpqiu@fudan.edu.cn
