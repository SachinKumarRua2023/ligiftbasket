# Long Island Gift Baskets - Homepage

A premium, responsive gift basket e-commerce homepage built with HTML5, CSS3, and vanilla JavaScript. Designed to be embedded in Odoo via iframe.

## Features

✨ **Design Features**
- Responsive design (desktop, tablet, mobile)
- Modern gradient-based color scheme (gold/bronze theme)
- Smooth animations and transitions
- Accessibility optimized

🎯 **Functional Features**
- **Dropdown Category Navigation**: Easy access to all gift basket categories
- **Category-Based Routing**: Click categories to navigate to `/shop/search?category=name`
- **Special Occasion Popups**: Automatic popups highlighting graduation, father's day, and birthday celebrations
- **Featured Products Section**: Showcase top gift baskets
- **Why Choose Us Section**: Trust indicators and value propositions
- **Mobile Responsive**: Fully functional on all devices

## Directory Structure

```
LiGiftBasket/
├── index.html                          # Main homepage
├── images/
│   ├── categories/
│   │   ├── birthday/                   # 18 birthday gift images
│   │   ├── fathers-day/                # 18 father's day gift images
│   │   ├── graduation/                 # 18 graduation gift images
│   │   ├── anniversary/                # 18 anniversary gift images
│   │   ├── corporate/                  # 18 corporate gift images
│   │   ├── wedding/                    # 18 wedding gift images
│   │   ├── get-well/                   # 18 get-well gift images
│   │   └── holiday/                    # 17 holiday gift images
│   ├── featured-products/              # Featured product images
│   ├── hero/                           # Hero section images
│   └── banners/                        # Banner images
├── README.md                           # This file
└── CLAUDE.md                           # Development guide
```

## Categories

The homepage includes 8 main gift basket categories:

1. **Birthday Gifts** - Celebrate special birthdays
2. **Father's Day** - Premium gifts for dads
3. **Graduation Gifts** - Celebrate academic achievements
4. **Anniversary** - Romantic gift baskets
5. **Wedding Gifts** - Luxurious wedding presents
6. **Corporate** - Professional business gifts
7. **Get Well** - Thoughtful recovery gifts
8. **Holiday** - Seasonal celebrations

## Special Occasion Features

### Automatic Popups
- Displays after 3 seconds on page load
- Randomly shows graduation, father's day, or birthday promotions
- Includes call-to-action button directing to category search
- Can be dismissed by user

### Category Search
When a category is clicked:
1. Homepage passes category name via query parameter
2. URL format: `/shop/search?category={category-name}`
3. For Odoo integration: The parent frame receives the navigation

## Odoo Integration

### Embedding via Iframe

```html
<iframe 
    src="/path/to/LiGiftBasket/index.html" 
    width="100%" 
    height="1500" 
    frameborder="0"
    scrolling="auto"
></iframe>
```

### Category Search Routing

The homepage is designed to work with Odoo's product search:

- **Graduation**: `/shop/search?category=graduation`
- **Father's Day**: `/shop/search?category=fathers-day`
- **Birthday**: `/shop/search?category=birthday`
- **Anniversary**: `/shop/search?category=anniversary`
- **Wedding**: `/shop/search?category=wedding`
- **Corporate**: `/shop/search?category=corporate`
- **Get Well**: `/shop/search?category=get-well`
- **Holiday**: `/shop/search?category=holiday`

These can be customized in Odoo to map to your actual product categories.

## Customization

### Colors
Edit the CSS variables in the style section:
- Primary color: `#c19a6b` (tan/gold)
- Secondary color: `#8b5a3c` (brown)
- Background: `#f5f5f5` (light gray)

### Contact Information
Update in the header and footer:
- Phone: `+1 (888) 440-9787`
- Email: `info@ligiftbasket.com`
- Hours: `Monday - Sunday: 9am - 6pm EST`

### Images
Replace placeholder images with your actual product photos:
1. Hero image: `images/categories/birthday/product-1.jpg`
2. Category images: First product image in each category folder
3. Featured products: `images/featured-products/` folder

### Text Content
All text can be customized directly in the HTML:
- Section titles
- Category descriptions
- Product descriptions
- Company taglines

## Performance

- **No external dependencies**: Pure HTML/CSS/JavaScript
- **Optimized animations**: GPU-accelerated transforms
- **Responsive images**: Native lazy loading support
- **Fast load time**: <50KB HTML file

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Android)

## Features Summary

| Feature | Status | Notes |
|---------|--------|-------|
| Responsive Design | ✅ | Mobile-first approach |
| Category Navigation | ✅ | Dropdown with 8 categories |
| Search Integration | ✅ | Query parameter routing |
| Special Popups | ✅ | Auto-trigger + manual dismiss |
| Featured Products | ✅ | 3 showcase items |
| Footer | ✅ | Links and contact info |
| Accessibility | ✅ | Semantic HTML |

## GitHub Repository

Repository: https://github.com/SachinKumarRua2023/ligiftbasket.git

### To Deploy:

```bash
# Clone repository
git clone https://github.com/SachinKumarRua2023/ligiftbasket.git

# Navigate to project
cd ligiftbasket

# Push any updates
git add .
git commit -m "Update: [description]"
git push origin main
```

## Support

For questions or customization needs:
- Email: info@ligiftbasket.com
- Phone: +1 (888) 440-9787

---

**Version**: 1.0.0  
**Last Updated**: June 8, 2026  
**Created by**: Claude Code with Hiren Kumar Digital Transformation Project
