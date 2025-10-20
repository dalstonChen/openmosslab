# Design Changes: Logo and Color Scheme

## Changes Applied

### 1. ✅ Logo Dimensions Updated (Square Logo)

**Problem:** Logo was configured for a rectangular 144x72px image, but OpenMoss logo is square.

**Solution:** Updated logo dimensions to 72x72px (square)

**File Changed:** `_includes/header.html`

**Before:**
```html
<img class="navbar-brand navbar-left hidden-xs" width="144" height="72"
     src="{{ '/assets/img/logos/openmoss-logo.png' | relative_url }}"
     alt="{{ site.title }}">
```

**After:**
```html
<img class="navbar-brand navbar-left hidden-xs" width="72" height="72"
     src="{{ '/assets/img/logos/openmoss-logo.png' | relative_url }}"
     alt="{{ site.title }}">
```

**Logo Specifications:**
- **Size:** 72 x 72 pixels (square)
- **Format:** PNG with transparency
- **Path:** `assets/img/logos/openmoss-logo.png`

---

### 2. ✅ Color Scheme Changed from Red to Blue

**Problem:** Site was using Stanford's red color scheme

**Solution:** Changed all primary colors to blue `rgba(14, 65, 156)`

**File Changed:** `assets/css/main.css`

#### Color Variables Updated

**Before (Red Theme):**
```css
:root {
  --primary-color: #8C1515;      /* Stanford red */
  --primary-dark: #6B0F0F;       /* Darker red */
  --accent-color: #B83A4B;       /* Accent red */
}
```

**After (Blue Theme):**
```css
:root {
  --primary-color: rgba(14, 65, 156, 1);      /* OpenMoss blue */
  --primary-dark: rgba(10, 50, 120, 1);       /* Darker blue */
  --accent-color: rgba(14, 65, 156, 0.8);     /* Accent blue */
}
```

#### Elements Affected by Color Change

All these elements now display in blue instead of red:

1. **Navigation Bar**
   - Border under navbar: Blue line
   - Brand text "OpenMoss Lab": Blue
   - Active menu items: Blue
   - Hover states: Blue

2. **Page Titles**
   - "Welcome" heading: Blue
   - All h1 page titles: Blue

3. **Section Headers**
   - "OpenMoss Lab" heading: Blue
   - "People" page title: Blue
   - All major headings: Blue

4. **Links**
   - All hyperlinks: Blue
   - Link hover states: Darker blue

5. **Interactive Elements**
   - Navigation hover: Blue
   - Active states: Blue
   - Focus states: Blue

---

## Visual Changes Summary

| Element | Before (Red) | After (Blue) |
|---------|-------------|--------------|
| Navbar border | `#8C1515` | `rgba(14, 65, 156, 1)` |
| Page titles (h1) | `#8C1515` | `rgba(14, 65, 156, 1)` |
| Brand text | `#8C1515` | `rgba(14, 65, 156, 1)` |
| Links | `#8C1515` | `rgba(14, 65, 156, 1)` |
| Link hover | `#6B0F0F` | `rgba(10, 50, 120, 1)` |
| Logo size | 144x72px | 72x72px (square) |

---

## Files Modified

1. **`_includes/header.html`**
   - Changed logo width from 144px to 72px
   - Height remains 72px (now square)

2. **`assets/css/main.css`**
   - Updated CSS color variables
   - Changed from red theme to blue theme
   - All color references use CSS variables (automatic update)

3. **`assets/img/logos/README.md`**
   - Updated logo specifications
   - Changed recommended size to 72x72px
   - Updated color scheme reference

---

## CSS Variables System

The site uses CSS variables for consistent theming. All color references automatically update when the root variables change.

### How It Works

```css
/* Define colors once */
:root {
  --primary-color: rgba(14, 65, 156, 1);
}

/* Use throughout the site */
.navbar-brand h3 {
  color: var(--primary-color);  /* Uses blue */
}

.pagetitle h1 {
  color: var(--primary-color);  /* Uses blue */
}

a {
  color: var(--primary-color);  /* Uses blue */
}
```

**Benefit:** Change color once, updates everywhere automatically!

---

## Verification Checklist

After deploying these changes, verify:

- [ ] Logo appears as 72x72px square in header
- [ ] Navigation bar has blue bottom border (not red)
- [ ] "OpenMoss Lab" text in header is blue
- [ ] Page titles (Welcome, People, Career, etc.) are blue
- [ ] All links are blue (not red)
- [ ] Hover states show darker blue
- [ ] No red colors visible anywhere on site

---

## Preview of Changes

### Before
- **Logo:** 144x72px rectangle (stretched if square logo used)
- **Border:** Red line under navigation
- **Titles:** Red text
- **Links:** Red color
- **Theme:** Stanford red (#8C1515)

### After
- **Logo:** 72x72px square (perfect for square logo)
- **Border:** Blue line under navigation
- **Titles:** Blue text
- **Links:** Blue color
- **Theme:** OpenMoss blue (rgba(14, 65, 156))

---

## Adding Your Logo

To add your square logo:

1. Create a 72x72px square PNG image
2. Name it `openmoss-logo.png`
3. Save to: `assets/img/logos/openmoss-logo.png`
4. Commit and push

The header will automatically display your logo at the correct size.

---

## Future Color Adjustments

To adjust colors in the future, edit only the CSS variables in `assets/css/main.css`:

```css
:root {
  --primary-color: rgba(14, 65, 156, 1);  /* Main blue */
  --primary-dark: rgba(10, 50, 120, 1);   /* Darker blue for hover */
  --accent-color: rgba(14, 65, 156, 0.8); /* Lighter blue */
}
```

All site colors will update automatically!

---

## Commit and Deploy

**Next steps:**

```bash
cd "/Users/dalstonchen/Library/CloudStorage/GoogleDrive-dalstonchen@gmail.com/My Drive/Job/fudan/projects/openmosslab"

# Check changes
git status

# Add all changes
git add .

# Commit
git commit -m "Design: Update logo to square (72x72) and change color scheme to blue"

# Push
git push origin main
```

**Expected result:**
- ✅ Site deploys with blue color scheme
- ✅ Logo dimensions correct for square image
- ✅ All red elements now blue

---

**Status:** ✅ Complete

**Date:** October 21, 2025

**Changes:** Logo dimensions (square), Color scheme (red → blue)
