# Deployment Configuration Guide

## GitHub Pages Deployment Types

GitHub Pages supports two types of sites, each requiring different configuration in `_config.yml`.

### 1. Project Site (Current Configuration)

**Use case**: Repository is named something other than `username.github.io`

**Example**: `https://dalstonchen.github.io/openmosslab`

**Configuration in `_config.yml`**:
```yaml
baseurl: "/openmosslab"  # Must match repository name
url: "https://dalstonchen.github.io"
```

**Repository Setup**:
- Repository name: `openmosslab` (or any name)
- Branch: `main`
- GitHub Pages source: GitHub Actions

**Live URL**: `https://yourusername.github.io/repository-name`

---

### 2. User/Organization Site

**Use case**: Repository is named `username.github.io`

**Example**: `https://dalstonchen.github.io`

**Configuration in `_config.yml`**:
```yaml
baseurl: ""  # Empty for user/org sites
url: "https://dalstonchen.github.io"
```

**Repository Setup**:
- Repository name: `dalstonchen.github.io` (must match username)
- Branch: `main`
- GitHub Pages source: GitHub Actions

**Live URL**: `https://yourusername.github.io`

---

## Current Site Configuration

This site is configured as a **Project Site**:

```yaml
# _config.yml
baseurl: "/openmosslab"
url: "https://dalstonchen.github.io"
```

**Repository**: `openmosslab`
**Live URL**: https://dalstonchen.github.io/openmosslab

---

## How Links Work

### With Liquid Filters (Templates)

In HTML templates (`_layouts/` and `_includes/`), always use the `relative_url` filter:

```liquid
<!-- Navigation links -->
<a href="{{ '/people/' | relative_url }}">People</a>

<!-- Images -->
<img src="{{ '/assets/img/logo.png' | relative_url }}" alt="Logo">

<!-- CSS -->
<link rel="stylesheet" href="{{ '/assets/css/main.css' | relative_url }}">
```

**Result for Project Site**:
- `/people/` becomes `/openmosslab/people/`
- `/assets/img/logo.png` becomes `/openmosslab/assets/img/logo.png`

**Result for User Site** (baseurl: ""):
- `/people/` stays `/people/`
- `/assets/img/logo.png` stays `/assets/img/logo.png`

### In Markdown Content

In Markdown files (`*.md`), Jekyll automatically handles relative links:

```markdown
Check out our [join page](/join/) for more info.
```

**Result**: Jekyll automatically prepends the `baseurl`, so this works correctly for both project and user sites.

### Absolute URLs

For external links or when you need the full URL:

```liquid
{{ site.url }}{{ site.baseurl }}/people/
```

**Result**: `https://dalstonchen.github.io/openmosslab/people/`

---

## Switching Deployment Types

### From Project Site to User Site

1. **Rename repository** to `username.github.io`
2. **Update `_config.yml`**:
   ```yaml
   baseurl: ""
   url: "https://username.github.io"
   ```
3. **Commit and push**
4. **Wait for deployment** (2-3 minutes)

### From User Site to Project Site

1. **Create new repository** or rename to project name
2. **Update `_config.yml`**:
   ```yaml
   baseurl: "/repository-name"
   url: "https://username.github.io"
   ```
3. **Commit and push**
4. **Wait for deployment** (2-3 minutes)

---

## Custom Domain

If using a custom domain (e.g., `openmosslab.org`):

**Configuration in `_config.yml`**:
```yaml
baseurl: ""  # Empty for custom domains
url: "https://openmosslab.org"
```

**GitHub Pages Setup**:
1. Go to repository Settings → Pages
2. Under "Custom domain", enter your domain
3. Add DNS records with your domain registrar:
   ```
   Type: A
   Name: @
   Value: 185.199.108.153
   Value: 185.199.109.153
   Value: 185.199.110.153
   Value: 185.199.111.153

   Type: CNAME
   Name: www
   Value: username.github.io
   ```

---

## Troubleshooting

### Links Not Working After Deployment

**Problem**: Links go to `yourusername.github.io/page` instead of `yourusername.github.io/repository/page`

**Solution**:
1. Check `baseurl` in `_config.yml` matches repository name
2. Verify all links in templates use `| relative_url` filter
3. Clear browser cache and hard refresh (Ctrl+F5)

### Styles Not Loading

**Problem**: CSS not applied to pages

**Solution**:
1. Check `<link>` tags use `| relative_url` filter
2. Verify `baseurl` is correct
3. Check browser console for 404 errors
4. Rebuild and redeploy

### Images Not Displaying

**Problem**: Images show as broken

**Solution**:
1. Check image paths use `| relative_url` filter
2. Verify images are in `assets/img/` directory
3. Check image file names (case-sensitive)
4. Verify images were committed and pushed to repository

### Homepage Works But Subpages Don't

**Problem**: Main page loads but `/people/` shows 404

**Solution**:
1. Verify `permalink` in front matter: `permalink: /people/`
2. Check file is in `_content/` or root directory
3. Verify GitHub Actions deployment succeeded
4. Wait 2-3 minutes for CDN propagation

---

## Testing Locally with Different Configurations

### Test as Project Site

```bash
# In _config.yml, set:
# baseurl: "/openmosslab"

bundle exec jekyll serve --baseurl /openmosslab
```

Visit: `http://localhost:4000/openmosslab`

### Test as User Site

```bash
# In _config.yml, set:
# baseurl: ""

bundle exec jekyll serve
```

Visit: `http://localhost:4000`

---

## Best Practices

1. **Always use `relative_url` filter** in templates for internal links
2. **Keep `baseurl` and `url` updated** in `_config.yml`
3. **Test locally** with the correct baseurl before deploying
4. **Clear cache** after configuration changes
5. **Wait for full deployment** (2-3 minutes) before testing changes

---

## Quick Reference

| Deployment Type | baseurl | url | Example URL |
|----------------|---------|-----|-------------|
| Project Site | `/repo-name` | `https://username.github.io` | `https://username.github.io/repo-name` |
| User Site | `""` (empty) | `https://username.github.io` | `https://username.github.io` |
| Custom Domain | `""` (empty) | `https://yourdomain.com` | `https://yourdomain.com` |

---

## Current Configuration Summary

- **Type**: Project Site
- **Repository**: `openmosslab`
- **baseurl**: `/openmosslab`
- **url**: `https://dalstonchen.github.io`
- **Live URL**: https://dalstonchen.github.io/openmosslab

All navigation links, assets, and internal links are configured to work correctly with this setup.
