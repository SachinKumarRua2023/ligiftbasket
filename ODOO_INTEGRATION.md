# Odoo Integration Guide - Long Island Gift Baskets

## 🎯 Quick Integration (3 Steps)

### Step 1: Copy the Sub-Header HTML

From `odoo-subheader.html`, copy the entire content:
- The `<style>` section
- The `<div class="gift-basket-subheader">` section  
- The `<script>` section

### Step 2: Paste into Odoo Homepage

In your Odoo website builder:
1. Go to **Website** → **Home** page
2. Click **Edit**
3. Add a new **Custom HTML** block (or Code block)
4. Paste the sub-header code
5. Place it **BELOW** your existing header but **ABOVE** the hero section

### Step 3: Save & Test

1. Click **Save**
2. Visit the homepage
3. Test the dropdown menu
4. Click categories to verify routing

---

## 📍 Exact Placement

Your current page structure:
```
┌─────────────────────────────────┐
│  ODOO TOP BANNER                │  (Free shipping, phone, delivery)
├─────────────────────────────────┤
│  ODOO HEADER                    │  (Logo, Nav, Phone, Contact button)
├─────────────────────────────────┤
│  ⭐ INSERT SUB-HEADER HERE ⭐   │  ← Add our dropdown menu here
├─────────────────────────────────┤
│  HERO SECTION                   │  (Gift Basket Paradise)
│  (Shop Now button)              │
├─────────────────────────────────┤
│  CATEGORIES SECTION             │
│  (Browse gift baskets grid)     │
├─────────────────────────────────┤
│  FOOTER                         │
└─────────────────────────────────┘
```

---

## 🎨 Design Matching

The sub-header matches your existing site:
- ✅ Same tan/gold color (#c19a6b)
- ✅ Same white background
- ✅ Same font styling
- ✅ Same border color
- ✅ Same spacing and padding
- ✅ Brown buttons and links match
- ✅ Mobile responsive

---

## 📋 How It Works

### Categories Dropdown:
```
All Categories ▼
├── 🎂 Birthday Gifts
├── 👨 Father's Day
├── 🎓 Graduation
├── 💍 Anniversary
├── 💒 Wedding
├── 💼 Corporate
├── 🌸 Get Well
└── 🎄 Holiday
```

### What Happens When User Clicks:
1. User clicks a category (e.g., "Graduation")
2. Dropdown function calls: `handleCategory('graduation')`
3. Redirects to: `/shop/search?category=graduation`
4. Odoo product search filters by category

---

## 🔧 Odoo Configuration

For the category routing to work, you need to:

### In Odoo Shop Settings:
1. Go to **eCommerce** → **Products** → **Categories**
2. Create or verify these categories exist:
   - Birthday
   - Fathers Day (or Father's Day)
   - Graduation
   - Anniversary
   - Wedding
   - Corporate
   - Get Well
   - Holiday

3. Make sure each product is tagged with the correct category

### In Odoo Shop Search:
1. Verify `/shop/search?category=X` endpoint works
2. Test: `/shop/search?category=birthday`
3. It should filter products by that category

---

## 🚀 Alternative: Full Embedded Page

If you want the ENTIRE page (with hero, categories, etc.) embedded:

Use `embedded.html` instead:

```html
<iframe 
    src="https://raw.githubusercontent.com/SachinKumarRua2023/ligiftbasket/master/embedded.html"
    width="100%" 
    height="2500" 
    frameborder="0"
    style="border: none;"
></iframe>
```

This gives you:
- Sub-header dropdown
- Hero section
- Category cards
- Featured products
- Special offers section

---

## 📱 Mobile Behavior

On mobile devices:
- Sub-header stacks vertically
- Dropdown becomes click-to-toggle
- Full-width layout
- Touch-friendly buttons

---

## 🎯 Files Available

| File | Purpose | Use Case |
|------|---------|----------|
| `odoo-subheader.html` | Just the dropdown menu | Add to existing Odoo page |
| `embedded.html` | Full page section | Replace entire page content |
| `index.html` | Standalone homepage | Use on GitHub Pages |

---

## ✅ Testing Checklist

After integration, test:

- [ ] Sub-header appears below Odoo header
- [ ] Color matches existing site (tan/gold)
- [ ] Dropdown menu opens on hover
- [ ] All 8 categories visible in dropdown
- [ ] Click category → redirects to shop search
- [ ] Mobile: menu toggle works
- [ ] Mobile: dropdown collapses properly
- [ ] No styling conflicts with Odoo theme
- [ ] Responsive on tablet (768px)
- [ ] Responsive on phone (375px)

---

## 🐛 Troubleshooting

### Sub-header not showing?
- Check that custom HTML block is inserted
- Verify CSS is not being overridden
- Check browser console (F12) for errors

### Colors don't match?
- Your Odoo theme might use different colors
- Edit the `--color: #c19a6b;` values in the `<style>`
- Match to your brand colors

### Dropdown not working?
- Check JavaScript is enabled
- Verify no JavaScript conflicts
- Check browser console for errors

### Categories not filtering products?
- Verify Odoo categories exist with exact names
- Check product category assignments
- Test search URL manually: `/shop/search?category=birthday`

---

## 📞 Support

**Files location**: `/LiGiftBasket/`

**GitHub**: https://github.com/SachinKumarRua2023/ligiftbasket/

**Contact Info**:
- Phone: (917) 338-7086
- Email: info@ligiftbasket.com

---

**Last Updated**: June 8, 2026
**Version**: 1.0
**Status**: Ready for Integration
