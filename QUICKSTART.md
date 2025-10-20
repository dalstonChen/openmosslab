# Quick Start Checklist

Follow these steps to get your OpenMoss Lab website live on GitHub Pages.

## ✅ Pre-Deployment Checklist

### 1. Prepare Your Content
- [ ] Add your lab logo to `assets/img/logos/openmoss-logo.png`
- [ ] Add group photo to `assets/img/logos/group-photo-2024.jpg`
- [ ] Update `_config.yml` with your actual URLs and contact info
- [ ] Review and customize content in `_content/` directory
- [ ] Update homepage content in `index.md`

### 2. Set Up GitHub Repository
- [ ] Create a new GitHub repository (e.g., `openmosslab-website`)
- [ ] Initialize Git and add remote:
  ```bash
  cd openmosslab
  git init
  git add .
  git commit -m "Initial commit: OpenMoss Lab website"
  git branch -M main
  git remote add origin https://github.com/yourusername/openmosslab-website.git
  git push -u origin main
  ```

### 3. Enable GitHub Pages
- [ ] Go to repository Settings
- [ ] Navigate to "Pages" section
- [ ] Under "Source", select "GitHub Actions"
- [ ] Save the settings

### 4. First Deployment
- [ ] Push your code to `main` branch
- [ ] Go to the "Actions" tab in your repository
- [ ] Watch the deployment workflow run
- [ ] Once complete (green checkmark), visit your site at:
  - User/Org Pages: `https://yourusername.github.io/`
  - Project Pages: `https://yourusername.github.io/repository-name/`

## 🚀 Local Development Setup

### One-Time Setup
```bash
# 1. Install Ruby (if not already installed)
# macOS:
brew install ruby

# Ubuntu/Debian:
sudo apt-get install ruby-full

# Windows: Use RubyInstaller from https://rubyinstaller.org/

# 2. Install Bundler
gem install bundler

# 3. Install dependencies
cd openmosslab
bundle install
```

### Daily Development Workflow
```bash
# Start local server
bundle exec jekyll serve

# View site at http://localhost:4000
# Press Ctrl+C to stop the server
```

## 📝 Content Update Workflow

### Making Changes
```bash
# 1. Pull latest changes
git pull origin main

# 2. Edit content files
# - Edit Markdown files in _content/
# - Or edit index.md for homepage

# 3. Test locally (optional but recommended)
bundle exec jekyll serve

# 4. Commit and push
git add .
git commit -m "Update [description of changes]"
git push origin main

# 5. Wait 2-3 minutes for automatic deployment
```

## 🔧 Common Customizations

### Change Site Colors
Edit `assets/css/main.css`:
```css
:root {
  --primary-color: #8C1515;  /* Change this */
  --primary-dark: #6B0F0F;   /* And this */
}
```

### Update Navigation Menu
Edit `_config.yml`:
```yaml
navigation:
  - title: "people"
    url: "/people/"
  - title: "your new page"
    url: "/newpage/"
```

### Add New Page
1. Create `_content/newpage.md`
2. Add front matter:
   ```yaml
   ---
   layout: page
   title: New Page
   permalink: /newpage/
   ---
   ```
3. Add content below front matter
4. Add to navigation in `_config.yml`
5. Commit and push

## 🐛 Troubleshooting

### Build Fails on GitHub Actions
- Check the Actions tab for error messages
- Common issues:
  - YAML syntax error in front matter
  - Missing front matter in Markdown files
  - Invalid permalink format
- Test locally first: `bundle exec jekyll build`

### Site Not Updating
- Hard refresh browser (Ctrl+F5 or Cmd+Shift+R)
- Check Actions tab for deployment status
- Verify changes were pushed to `main` branch
- Wait full 3 minutes for propagation

### Local Server Won't Start
```bash
# Update dependencies
bundle update

# Clean build
bundle exec jekyll clean
bundle exec jekyll serve
```

### "Command not found" Errors
- Ensure Ruby is installed: `ruby --version`
- Ensure Bundler is installed: `bundle --version`
- Reinstall if needed: `gem install bundler`

## 📋 Regular Maintenance

### Weekly
- [ ] Review and merge pull requests
- [ ] Update news or announcements
- [ ] Add new publications

### Monthly
- [ ] Update dependencies: `bundle update`
- [ ] Check for broken links
- [ ] Review analytics (if configured)

### Quarterly
- [ ] Update people listings
- [ ] Refresh group photo
- [ ] Review and update all content

## 📚 Resources

### Essential Documentation
- **This Project**: See `SETUP.md` for detailed guide
- **Jekyll**: https://jekyllrb.com/docs/
- **Markdown**: https://www.markdownguide.org/
- **GitHub Pages**: https://docs.github.com/en/pages

### Getting Help
- **Project Issues**: Create issue on GitHub repository
- **Jekyll Questions**: https://talk.jekyllrb.com/
- **Lab Contact**: xpqiu@fudan.edu.cn

## 🎯 Next Steps

After completing the checklist above:

1. **Customize Content**: Update all pages with your actual lab information
2. **Add Images**: Upload logo and photos to `assets/img/`
3. **Test Everything**: Click through all pages locally
4. **Share with Team**: Get feedback on content and design
5. **Promote**: Share your new website URL

## ⚡ Pro Tips

- **Test locally before pushing**: Catch errors early
- **Use descriptive commit messages**: "Add spring 2025 publications" not "update"
- **Keep content in Markdown**: Don't mix HTML unless necessary
- **Backup regularly**: Git is your friend
- **Document customizations**: Add notes for future reference

---

**Ready to launch?** Start with step 1 of the Pre-Deployment Checklist above! 🚀
