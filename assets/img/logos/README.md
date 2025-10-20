# Logo Assets

Place your logo files in this directory:

## Required Files

- `openmoss-logo.png` - Main logo for header (144x72px recommended)
- `group-photo-2024.jpg` - Lab group photo for homepage

## Image Guidelines

### Logo
- **Format**: PNG with transparency preferred
- **Size**: 144 x 72 pixels (or proportional)
- **Background**: Transparent or white
- **Colors**: Should match the site's red color scheme

### Group Photo
- **Format**: JPG or PNG
- **Size**: 1200px width recommended (will scale responsively)
- **Aspect Ratio**: 16:9 or 4:3 recommended
- **Quality**: High resolution for clarity

## Adding Images

1. Place image files in this directory
2. Reference them in Markdown or HTML:

```markdown
![Alt text](/assets/img/logos/filename.png)
```

Or with relative_url filter in templates:

```html
<img src="{{ '/assets/img/logos/filename.png' | relative_url }}" alt="Description">
```

## Current Usage

- `openmoss-logo.png`: Used in header navigation (`_includes/header.html`)
- `group-photo-2024.jpg`: Used on homepage (`_layouts/home.html`)
