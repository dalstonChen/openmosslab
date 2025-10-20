# GitHub Actions Workflow Fix

## Problem Identified

When pushing commits to the repository, **two GitHub Actions workflows** were being triggered:

1. **"Deploy Jekyll site to GitHub Pages"** (custom workflow) - ❌ **FAILING**
2. **"pages build and deployment"** (GitHub's automatic workflow) - ✅ **SUCCEEDING**

## Root Cause

The repository had a **conflict between two deployment methods**:

- **Custom GitHub Actions workflow** (`.github/workflows/deploy.yml`) - Attempting to build and deploy
- **GitHub Pages' built-in Jekyll deployment** - Already configured and working

GitHub Pages was configured to deploy automatically, making the custom workflow redundant and causing it to fail due to permission conflicts.

## Solution Applied

### 1. Removed Custom Workflow

**Action:** Deleted `.github/workflows/deploy.yml`

**Reason:** GitHub Pages' built-in deployment is already working perfectly. The custom workflow was:
- Redundant
- Causing permission conflicts
- Failing on every commit

### 2. How Deployment Works Now

Going forward, when you push commits:

✅ **Only ONE workflow will run:** "pages build and deployment"

This is GitHub's automatic Jekyll build and deployment system, which:
- Detects changes to your repository
- Automatically builds the Jekyll site
- Deploys to GitHub Pages
- Handles all permissions correctly

### Expected Behavior After Fix

**Before:**
```
Commit pushed
├── "Deploy Jekyll site to GitHub Pages" ❌ FAILS
└── "pages build and deployment" ✅ SUCCEEDS
```

**After:**
```
Commit pushed
└── "pages build and deployment" ✅ SUCCEEDS
```

## Configuration Changes Made

### 1. Lab Name & Address Updated

**File:** `_config.yml`

**Changes:**
```yaml
organization:
  name: "OpenMoss Lab"
  full_name: "OpenMoss Lab"
  location1: "3 Lane 699, Huafa Road, Xuhui District"
  location2: "Building 2X, No. 2005 Songhu Road, Yangpu District"
  city: "Shanghai, China"
  email: "xpqiu@fudan.edu.cn"
```

### 2. Footer Updated

**File:** `_includes/footer.html`

**Changes:** Updated to use the new location fields (`location1`, `location2`, `city`) instead of the old single `location` field.

```html
<h4>{{ site.organization.name }}</h4>
{% if site.organization.location1 %}{{ site.organization.location1 }}<br>{% endif %}
{% if site.organization.location2 %}{{ site.organization.location2 }}<br>{% endif %}
{% if site.organization.city %}{{ site.organization.city }}<br>{% endif %}
<a href="mailto:{{ site.organization.email }}">Contact</a>
```

## How GitHub Pages Deployment Works

### Current Configuration

**GitHub Pages Source:** Deploy from a branch (automatic Jekyll build)
**Branch:** `main`
**Build System:** GitHub's built-in Jekyll

### What Triggers a Deployment

Any push to the `main` branch will automatically:
1. Trigger GitHub Pages to build the site
2. Build Jekyll site from source
3. Deploy to `https://dalstonchen.github.io/openmosslab`

### No Custom Workflow Needed

GitHub Pages handles everything automatically:
- ✅ Detects Jekyll configuration
- ✅ Installs dependencies from `Gemfile`
- ✅ Builds the site with correct `baseurl`
- ✅ Deploys to GitHub Pages CDN
- ✅ Updates the live site

## Verification

### Check Deployment Status

1. Go to your repository on GitHub
2. Click the **"Actions"** tab
3. You should see **only ONE workflow** per commit:
   - "pages build and deployment" ✅

### Check Live Site

After the workflow completes (typically 30-60 seconds):
- Visit: https://dalstonchen.github.io/openmosslab
- Footer should show the new addresses:
  - 3 Lane 699, Huafa Road, Xuhui District
  - Building 2X, No. 2005 Songhu Road, Yangpu District
  - Shanghai, China

## Future Changes

### To Update Content

Simply edit Markdown files and push:

```bash
# Edit content
git add .
git commit -m "Update content"
git push origin main

# GitHub Pages will automatically build and deploy
# Wait 30-60 seconds and your site is updated
```

### To Customize Deployment (If Needed Later)

If you need custom deployment in the future:
1. Go to repository Settings → Pages
2. Change "Source" from "Deploy from a branch" to "GitHub Actions"
3. Create a custom workflow file
4. Make sure it doesn't conflict with automatic deployment

## Summary of Files Changed

| File | Change | Reason |
|------|--------|--------|
| `.github/workflows/deploy.yml` | **Deleted** | Redundant, causing failures |
| `_config.yml` | Updated organization info | New lab addresses |
| `_includes/footer.html` | Updated to use new location fields | Display correct addresses |

## Commit and Deploy

**Next steps:**

```bash
cd "/Users/dalstonchen/Library/CloudStorage/GoogleDrive-dalstonchen@gmail.com/My Drive/Job/fudan/projects/openmosslab"

# Check what changed
git status

# Add all changes
git add .

# Commit
git commit -m "Fix: Remove redundant workflow and update lab addresses"

# Push
git push origin main
```

**Expected result:**
- ✅ Only one workflow runs: "pages build and deployment"
- ✅ Workflow succeeds
- ✅ Site deploys with updated addresses

## Troubleshooting

### If Deployment Still Fails

1. **Check GitHub Pages settings:**
   - Go to repository Settings → Pages
   - Ensure "Source" is set correctly

2. **Check Gemfile:**
   - Make sure `Gemfile` exists in repository root
   - Should contain Jekyll dependencies

3. **Check _config.yml:**
   - Ensure `baseurl: "/openmosslab"` is correct
   - Ensure no syntax errors in YAML

### If Site Doesn't Update

1. **Clear browser cache:**
   - Hard refresh: Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)

2. **Check workflow logs:**
   - Go to Actions tab
   - Click on the workflow run
   - Check for any error messages

3. **Wait for CDN propagation:**
   - GitHub Pages uses a CDN
   - Changes may take 1-2 minutes to appear

---

**Status:** ✅ Fixed

**Date:** October 21, 2025

**Changes:** Removed redundant workflow, updated lab information, fixed footer template
