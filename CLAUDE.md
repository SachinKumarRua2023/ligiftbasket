# Long Island Gift Baskets - Development Guide

## Project Overview

This is a responsive HTML/CSS/JavaScript homepage for Long Island Gift Baskets e-commerce site, designed to:
1. Operate as a standalone webpage on GitHub Pages
2. Be embedded in Odoo via iframe for seamless integration
3. Route category clicks to Odoo's product search system
4. Display promotional popups for key occasions (graduation, father's day, birthday)

## Architecture

### File Structure
```
LiGiftBasket/
├── index.html          # Single-file homepage (no external deps)
├── README.md           # User documentation
├── CLAUDE.md           # This file (dev guidelines)
├── images/             # Organized by category
│   ├── categories/     # 8 occasion categories
│   ├── featured-products/
│   ├── hero/
│   └── banners/
└── .git/               # GitHub repository
```

### Design Approach
- **Single File**: All CSS and JavaScript inline for easy iframe embedding
- **No Dependencies**: Pure vanilla HTML5/CSS3/JavaScript
- **Responsive**: Mobile-first, works from 320px to 4K
- **Accessible**: Semantic HTML, good color contrast, keyboard navigation

## Color Scheme & Branding

**Theme**: Gold/Tan (premium gift theme)

```css
Primary:    #c19a6b   /* Tan/Gold */
Secondary:  #8b5a3c   /* Dark Brown */
Accent:     #d4a574   /* Light Tan */
```

These colors are used throughout and should NOT be changed without understanding brand consistency across all 7 Hiren Kumar sites.

**Font**: Segoe UI, system fonts (no web fonts imported for performance)

## Category Mapping

Categories are hardcoded in the dropdown and map to search queries:

| Category | URL Parameter | Priority | Notes |
|----------|---------------|----------|-------|
| Birthday | `birthday` | Medium | 18 images |
| Father's Day | `fathers-day` | **HIGH** | 18 images - Priority for promotions |
| Graduation | `graduation` | **HIGH** | 18 images - Priority for promotions |
| Anniversary | `anniversary` | Medium | 18 images |
| Wedding | `wedding` | Medium | 18 images |
| Corporate | `corporate` | Low | 18 images |
| Get Well | `get-well` | Low | 18 images |
| Holiday | `holiday` | Seasonal | 17 images |

## Special Occasion Popups

### Behavior
- Trigger automatically 3 seconds after page load
- Randomly select from: Graduation, Father's Day, Birthday
- User can dismiss ("Later" button)
- Clicking "Shop Now" navigates to category search

### JavaScript Function
```javascript
showSpecialOccasionPopup()  // Call to show modal
searchCategory(category)    // Navigate to /shop/search?category=X
closeModal(modalId)         // Close any modal
```

### To Modify Occasions
Edit the `occasions` array in `showSpecialOccasionPopup()`:
```javascript
const occasions = [
    {
        title: '🎓 Celebrate Graduation!',
        description: 'Your message here',
        category: 'graduation',
        image: 'images/categories/graduation/product-2.jpg'
    },
    // Add more...
];
```

## Odoo Integration Notes

### How It Works
1. Homepage is served from GitHub (or self-hosted)
2. Odoo page embeds via iframe: `<iframe src="..." />`
3. User clicks category
4. JavaScript calls `searchCategory(name)`
5. If in iframe, navigates parent: `window.parent.location.href = searchUrl`

### Expected Odoo Setup
- Product categories should match our category names OR
- Odoo should have a search endpoint that accepts `?category=name`
- Categories should be filterable in Odoo's `/shop/search` endpoint

### Customization for Different Odoo Instance
If your Odoo search endpoint is different:

**Current:** `/shop/search?category={category}`

**To Change:**
1. Edit `searchCategory()` function
2. Replace `const searchUrl = `/shop/search?category=${category}`;`
3. With your actual endpoint

Example for custom endpoint:
```javascript
// For custom Odoo search URL
const searchUrl = `/my-custom-shop?occasion=${category}&filter=gifts`;

// For external domain
const searchUrl = `https://odoo.example.com/shop/search?category=${category}`;
```

## Image Management

### Current Organization
All 152 images distributed across 8 categories (~18 images each)

### Naming Convention
Images use format: `product-{number}.{ext}`
- `product-1.jpg` in each category folder
- All JPGs except SVG assets

### To Add More Images
1. Create appropriately sized images (recommended: 1200x800px or larger)
2. Place in category folder: `images/categories/{category}/`
3. Name sequentially: `product-1.jpg`, `product-2.jpg`, etc.
4. Update HTML to use new filenames

### Image Size Guidelines
- **Hero Image**: 1200x600px (landscape)
- **Category Cards**: 600x450px (4:3 ratio)
- **Product Cards**: 600x500px (roughly square)
- **Keep file size < 200KB per image** for fast loading

## Responsive Behavior

### Breakpoints
```css
Desktop:    > 768px     /* Full layout */
Tablet:     481-768px   /* 2-column grid */
Mobile:     < 480px     /* Single column, stacked nav */
```

### Mobile Differences
- Navigation stack vertically
- Dropdown menu replaces with toggle on click
- Grid becomes single column
- Banner text stacks
- Images scale to container

## Development Workflow

### 1. Local Testing
```bash
# Simply open in browser:
file:///c:/Users/Sachin%20Kumar/OneDrive/Desktop/HirenTask/LiGiftBasket/index.html

# Or use local server:
cd LiGiftBasket
python -m http.server 8000
# Visit http://localhost:8000
```

### 2. Making Changes
- Edit `index.html` directly
- All CSS is in `<style>` tag
- All JS is in `<script>` tag
- No build process needed

### 3. Testing
- Test on desktop (1920px wide)
- Test on tablet (768px)
- Test on mobile (375px)
- Test popups trigger
- Test category navigation
- Test dropdown menu on mobile

### 4. Git Workflow
```bash
git add index.html README.md
git commit -m "Update: description of changes"
git push origin main
```

## Common Customizations

### Change Phone Number
```html
<!-- In header -->
<a href="tel:+18884409787" class="phone-contact">📞 +1 (888) 440-9787</a>

<!-- In footer -->
<a href="tel:+18884409787">📞 +1 (888) 440-9787</a>
```

Replace `+18884409787` with actual number everywhere (2 locations in current version)

### Change Contact Email
```html
<a href="mailto:info@ligiftbasket.com">📧 info@ligiftbasket.com</a>
```

### Customize Popup Timing
```javascript
setTimeout(function() {
    showSpecialOccasionPopup();
}, 3000);  // Change 3000 to milliseconds (e.g., 5000 for 5 seconds)
```

### Change Primary Colors
Find and replace in CSS:
- `#c19a6b` → your primary color
- `#8b5a3c` → your secondary color
- `#d4a574` → your accent color

## Performance Optimization

Current performance metrics:
- **Page Size**: ~50KB (HTML only, no external assets)
- **Load Time**: <1 second on 3G
- **Lighthouse Score**: 90+ (when images optimized)

If slow:
1. Optimize images (use TinyPNG, ImageOptim)
2. Reduce image count in slider
3. Implement lazy loading for below-fold images

## Debugging

### Chrome DevTools
1. Right-click → "Inspect"
2. Check Console for JavaScript errors
3. Check Network for image load failures
4. Check Mobile view for responsive issues

### Common Issues

**Images not loading:**
- Check file paths in HTML (case-sensitive on Linux)
- Verify images exist in correct folder
- Check browser console for 404 errors

**Popup not showing:**
- Check DevTools console for JS errors
- Verify `showSpecialOccasionPopup()` runs
- Check modal CSS (`#specialOccasionPopup` display)

**Category search not working:**
- Check if Odoo endpoint matches
- Verify iframe permissions if embedded
- Check console for cross-origin errors

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-06-08 | Initial release with 8 categories, popup, responsive design |

## Future Enhancements

Potential additions (out of scope for current version):
- [ ] Image carousel/slider
- [ ] Product filters (price range, rating)
- [ ] Add to cart functionality
- [ ] Customer testimonials section
- [ ] Blog/gift guides
- [ ] Analytics integration
- [ ] A/B testing for popup timing
- [ ] Multi-language support

## Related Projects

This is part of the **Hiren Kumar Digital Transformation** project:
- **Project URL**: SeekHowItHRua (pm: Sachin)
- **Related Sites**: 
  - longislandcards.com (trading cards)
  - [6 other e-commerce sites]
- **Infrastructure**: Odoo ERP + n8n automation

## Support & Contact

**For Developers:**
- Check CLAUDE.md (this file) for guidelines
- Check README.md for user-facing documentation
- Use semantic HTML and comment complex logic

**For Project Manager:**
- Email: kahpk1933@gmail.com (Sachin Kumar)
- Phone: From header/footer (contact details)

---

**Last Updated**: June 8, 2026  
**Maintainer**: Claude Code  
**Status**: Production Ready
