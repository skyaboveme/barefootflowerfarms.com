# Admin Backend Implementation Plan

## Overview
Build an admin section that allows managing flowers, plants, and seeds in the shop.

## Current State
- Astro static site deployed to GitHub Pages
- Products are hardcoded in `src/pages/products.astro`
- No backend or database currently exists

## Proposed Solution: JSON File + Admin Panel

Since this is a static site on GitHub Pages, I recommend a **client-side admin panel with JSON file storage**. This approach:
- Requires no external database or server costs
- Works with the existing GitHub Pages hosting
- Stores product data in a JSON file that the shop page reads

### Architecture

```
/public/data/products.json    <- Product data (readable by anyone)
/src/pages/admin.astro        <- Admin panel (password protected)
```

### Features

**Admin Panel (`/admin`):**
1. Password protection (simple client-side password)
2. View all products in a table
3. Add new products (name, description, price, unit, category, image URL)
4. Edit existing products
5. Delete products
6. Export/download updated JSON file

**How Updates Work:**
1. Admin makes changes in the panel
2. Admin downloads the updated `products.json` file
3. Admin commits the file to GitHub (manually or via GitHub web interface)
4. Site rebuilds automatically via GitHub Actions

### Alternative: localStorage-only (Simplest)
Products stored in browser localStorage. Data persists only on that device/browser.

### Alternative: External API (More Complex)
Use a service like:
- **Supabase** (free tier) - PostgreSQL database
- **Firebase** (free tier) - NoSQL database
- **Airtable** (free tier) - Spreadsheet-like database

This would require API integration and environment variables.

## Recommended Implementation

**Option 1: JSON File Export** (Recommended for simplicity)
- Admin edits products in browser
- Downloads JSON file
- Commits to GitHub

**Option 2: Supabase Integration** (Recommended for real-time updates)
- Free PostgreSQL database
- Real-time product updates without manual commits
- Requires Astro SSR mode or client-side fetching

## Questions for User
1. Do you want products to update immediately (requires external database)?
2. Or is downloading/committing a JSON file acceptable?
3. Do you have a Supabase/Firebase account, or would you like to set one up?

## Implementation Steps (JSON File Approach)

1. Create `/public/data/products.json` with current products
2. Update `products.astro` to fetch from JSON file
3. Create `/src/pages/admin.astro` with:
   - Password login screen
   - Product listing table
   - Add/Edit/Delete product forms
   - Export JSON button
4. Style admin panel to match site theme
5. Add instructions for updating products

## Files to Create/Modify

- `public/data/products.json` (new)
- `src/pages/products.astro` (modify to read JSON)
- `src/pages/admin.astro` (new)
- `src/components/AdminPanel.astro` (new)
