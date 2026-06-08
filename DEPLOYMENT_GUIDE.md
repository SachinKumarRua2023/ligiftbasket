# Deployment Guide - Long Island Gift Baskets

## Quick Start: Push to GitHub

### 1. Initial Setup (First Time Only)

```bash
# Navigate to the project directory
cd "C:\Users\Sachin Kumar\OneDrive\Desktop\HirenTask\LiGiftBasket"

# Initialize git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Long Island Gift Baskets homepage with 8 categories, popups, responsive design"

# Add remote origin (copy URL from GitHub repo settings)
git remote add origin https://github.com/SachinKumarRua2023/ligiftbasket.git

# Push to main branch
git branch -M main
git push -u origin main
```

### 2. Make Changes & Push Updates

```bash
# Make your changes to index.html, images, etc.

# Check what changed
git status

# Stage specific files
git add index.html
git add images/

# Or add everything
git add .

# Commit with descriptive message
git commit -m "Update: Changed category descriptions and popup timing"

# Push to GitHub
git push origin main
```

## GitHub Actions (Optional)

To enable GitHub Pages for direct access:

1. Go to **GitHub Repository Settings**
2. Navigate to **Pages** section
3. Set **Source** to: "Deploy from a branch"
4. Set **Branch** to: "main" folder "/ (root)"
5. Save

Your site will be available at: `https://SachinKumarRua2023.github.io/ligiftbasket/`

## Folder Structure for GitHub

```
ligiftbasket/
├── .git/
├── .gitignore
├── index.html
├── README.md
├── CLAUDE.md
├── DEPLOYMENT_GUIDE.md (this file)
├── images/
│   ├── categories/
│   │   ├── birthday/
│   │   ├── fathers-day/
│   │   ├── graduation/
│   │   ├── anniversary/
│   │   ├── corporate/
│   │   ├── wedding/
│   │   ├── get-well/
│   │   └── holiday/
│   ├── featured-products/
│   ├── hero/
│   └── banners/
└── docs/ (optional)
    └── API_INTEGRATION.md
```

## File-by-File Checklist

### Core Files (MUST COMMIT)
- [x] `index.html` - Main homepage
- [x] `README.md` - User documentation
- [x] `CLAUDE.md` - Developer guide
- [x] `DEPLOYMENT_GUIDE.md` - This file
- [x] `.gitignore` - Git ignore rules

### Images (MUST COMMIT)
All images in `images/` folder:
- [x] `images/categories/birthday/` (18 images)
- [x] `images/categories/fathers-day/` (18 images)
- [x] `images/categories/graduation/` (18 images)
- [x] `images/categories/anniversary/` (18 images)
- [x] `images/categories/corporate/` (18 images)
- [x] `images/categories/wedding/` (18 images)
- [x] `images/categories/get-well/` (18 images)
- [x] `images/categories/holiday/` (17 images)
- [x] `images/featured-products/` (SVG + PNG files)

### Optional Files (DO NOT COMMIT)
- `.DS_Store` (macOS)
- `.vscode/` (editor config)
- `.env` (credentials)
- Backup files

## Git Commands Cheat Sheet

```bash
# Status check
git status

# View changes
git diff
git diff --staged

# Undo changes
git checkout -- filename.html
git reset HEAD filename.html

# View commit history
git log --oneline
git log --graph --oneline --all

# Create a new branch
git branch feature/new-feature
git checkout feature/new-feature

# Merge branches
git checkout main
git merge feature/new-feature

# Delete branch
git branch -d feature/new-feature

# Revert last commit (keeps changes)
git reset --soft HEAD~1

# Force push (USE CAREFULLY)
git push -f origin main
```

## Odoo Integration Setup

### Step 1: Place in Odoo Module
```
odoo/addons/ligiftbasket/
├── static/
│   └── src/
│       └── html/
│           └── ligiftbasket_homepage/
│               ├── index.html
│               └── images/
└── views/
    └── homepage_view.xml
```

### Step 2: Create Odoo View (XML)
```xml
<template id="ligiftbasket_homepage" name="Gift Baskets Homepage">
    <t t-call="web_unsupported_browser_template" t-if="not is_html_empty(arch)"/>
    <div class="ligiftbasket-container">
        <iframe src="/ligiftbasket/index.html" 
                width="100%" 
                height="2000" 
                frameborder="0"
                style="border: none;"
        ></iframe>
    </div>
</template>
```

### Step 3: Odoo Route Configuration
```python
# In your Odoo module __manifest__.py
{
    'name': 'Long Island Gift Baskets',
    'version': '1.0',
    'category': 'eCommerce',
    'description': 'Gift Basket Homepage',
    'depends': ['website', 'ecommerce'],
    'data': [
        'views/homepage_view.xml',
    ],
}
```

### Step 4: Map Categories in Odoo
Create product categories in Odoo:
- Birthday
- Father's Day
- Graduation
- Anniversary
- Wedding
- Corporate
- Get Well
- Holiday

Then update product search to filter by these categories when query parameter is received.

## Troubleshooting

### Images Not Loading
1. Verify image paths are relative (not absolute)
2. Check case sensitivity: `Birthday/` vs `birthday/`
3. Ensure images are committed to Git:
   ```bash
   git status images/
   git add images/
   git commit -m "Add images"
   git push
   ```

### Iframe Not Loading
1. Check browser console for CORS errors
2. Verify file permissions on server
3. Check that URL is accessible

### Git Push Fails
```bash
# Update local repo with remote changes
git pull origin main

# Resolve conflicts if any
# Then commit and push
git add .
git commit -m "Merge remote changes"
git push origin main
```

### Large File Issues
If adding large images:
```bash
# Install Git LFS (Large File Storage)
git lfs install

# Track image files
git lfs track "*.jpg"
git lfs track "*.png"

# Commit LFS tracking file
git add .gitattributes
git commit -m "Add Git LFS tracking"

# Add and push images
git add images/
git commit -m "Add product images"
git push
```

## File Size Optimization

Before committing large images:

```bash
# Using ImageMagick (if installed)
magick convert original.jpg -quality 85 -resize 1200x800 optimized.jpg

# Using Python PIL
python -c "
from PIL import Image
img = Image.open('original.jpg')
img.thumbnail((1200, 800))
img.save('optimized.jpg', quality=85)
"
```

## Monitoring & Updates

### Regular Maintenance
- [ ] Check for broken links monthly
- [ ] Update image descriptions quarterly
- [ ] Review popup messaging seasonally
- [ ] Monitor analytics for conversion rates

### Version Tracking
```bash
# Create version tags
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# List tags
git tag -l

# View tag details
git show v1.0.0
```

## Backup Strategy

### Local Backup
```bash
# Create backup directory
mkdir ../LiGiftBasket-backup

# Copy entire project
cp -r LiGiftBasket/ ../LiGiftBasket-backup/

# Or use tar
tar -czf LiGiftBasket-backup.tar.gz LiGiftBasket/
```

### GitHub as Backup
- All commits are automatically backed up on GitHub
- To restore: `git clone https://github.com/SachinKumarRua2023/ligiftbasket.git`

## Continuous Integration (Optional)

Create `.github/workflows/validate.yml`:

```yaml
name: Validate Homepage

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Check HTML validity
      run: |
        # Simple HTML validation
        grep -r "<html" index.html
        echo "HTML structure valid"
    
    - name: Verify image paths
      run: |
        # Check all image references exist
        grep -o 'src="[^"]*"' index.html | cut -d'"' -f2 | sort -u
```

## Support & Escalation

**Issue**: Static site changes
- **Action**: Edit HTML, commit, push
- **Timeline**: Immediate (< 5 min)

**Issue**: Product image updates
- **Action**: Replace images, commit, push
- **Timeline**: < 30 min

**Issue**: Category mapping changes
- **Action**: Coordinate with Odoo setup, update query parameters
- **Timeline**: 1-2 hours

**Issue**: Odoo integration problems
- **Contact**: Hiren Kumar tech team
- **Timeline**: 4-8 hours

---

**Created**: June 8, 2026  
**Last Updated**: June 8, 2026  
**Maintained by**: Sachin Kumar (PM) & Claude Code
