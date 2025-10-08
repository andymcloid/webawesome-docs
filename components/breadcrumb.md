# Breadcrumb

Breadcrumbs show the current location within a navigation hierarchy.

## Overview

The `<wa-breadcrumb>` component displays a hierarchical navigation trail showing the user's location within the site structure. It works together with `<wa-breadcrumb-item>` components to create a navigational path.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/breadcrumb/breadcrumb.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-breadcrumb>
  <wa-breadcrumb-item>Home</wa-breadcrumb-item>
  <wa-breadcrumb-item>Category</wa-breadcrumb-item>
  <wa-breadcrumb-item>Product</wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Links

Make breadcrumb items clickable with the `href` attribute:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products">Products</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products/electronics">Electronics</wa-breadcrumb-item>
  <wa-breadcrumb-item>Laptop</wa-breadcrumb-item>
</wa-breadcrumb>
```

## Custom Separator

Change the separator between items:

```html
<!-- Arrow separator -->
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/docs">Documentation</wa-breadcrumb-item>
  <wa-breadcrumb-item>Components</wa-breadcrumb-item>
  <span slot="separator">→</span>
</wa-breadcrumb>

<!-- Dot separator -->
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/blog">Blog</wa-breadcrumb-item>
  <wa-breadcrumb-item>Article</wa-breadcrumb-item>
  <span slot="separator">•</span>
</wa-breadcrumb>

<!-- Icon separator -->
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/projects">Projects</wa-breadcrumb-item>
  <wa-breadcrumb-item>Current Project</wa-breadcrumb-item>
  <wa-icon slot="separator" name="chevron-right"></wa-icon>
</wa-breadcrumb>
```

## With Icons

Add icons to breadcrumb items:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
    Home
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/documents">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Documents
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/documents/reports">
    <wa-icon slot="prefix" name="file-text"></wa-icon>
    Reports
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    <wa-icon slot="prefix" name="file"></wa-icon>
    Annual Report 2024
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

## Icon Only Home

Common pattern with icon-only home link:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/settings">Settings</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/settings/profile">Profile</wa-breadcrumb-item>
  <wa-breadcrumb-item>Edit</wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Dropdown

Use dropdowns for complex hierarchies:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
    Home
  </wa-breadcrumb-item>

  <wa-breadcrumb-item>
    <wa-dropdown>
      <wa-button slot="trigger" size="small" variant="neutral">
        Projects
        <wa-icon slot="end" name="chevron-down"></wa-icon>
      </wa-button>
      <wa-menu>
        <wa-menu-item href="/projects/web">Web Projects</wa-menu-item>
        <wa-menu-item href="/projects/mobile">Mobile Projects</wa-menu-item>
        <wa-menu-item href="/projects/archived">Archived Projects</wa-menu-item>
      </wa-menu>
    </wa-dropdown>
  </wa-breadcrumb-item>

  <wa-breadcrumb-item href="/projects/web/portfolio">Portfolio Site</wa-breadcrumb-item>
  <wa-breadcrumb-item>Dashboard</wa-breadcrumb-item>
</wa-breadcrumb>
```

## Page Navigation

Complete page navigation example:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
    Home
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop">Shop</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop/clothing">Clothing</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop/clothing/mens">Men's</wa-breadcrumb-item>
  <wa-breadcrumb-item>T-Shirts</wa-breadcrumb-item>
</wa-breadcrumb>
```

## E-commerce Navigation

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/categories">All Categories</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/categories/electronics">
    <wa-icon slot="prefix" name="monitor"></wa-icon>
    Electronics
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/categories/electronics/computers">
    <wa-icon slot="prefix" name="laptop"></wa-icon>
    Computers
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>Gaming Laptop XPS 15</wa-breadcrumb-item>
</wa-breadcrumb>
```

## Documentation Site Navigation

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="book"></wa-icon>
    Docs
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/components">Components</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/components/navigation">Navigation</wa-breadcrumb-item>
  <wa-breadcrumb-item>Breadcrumb</wa-breadcrumb-item>
</wa-breadcrumb>
```

## File System Navigation

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/files">
    <wa-icon slot="prefix" name="hard-drive"></wa-icon>
    My Drive
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/files/documents">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Documents
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/files/documents/work">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Work
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/files/documents/work/projects">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Projects
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    <wa-icon slot="prefix" name="file"></wa-icon>
    proposal.pdf
  </wa-breadcrumb-item>
  <wa-icon slot="separator" name="chevron-right"></wa-icon>
</wa-breadcrumb>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `label` | string | `'Breadcrumb'` | No | Accessible label for the breadcrumb navigation |

## Slots

| Slot | Description |
|------|-------------|
| (default) | Breadcrumb items |
| `separator` | Custom separator to use between items (applies to all items) |

## Examples

### Responsive Breadcrumb

```html
<wa-breadcrumb id="responsiveBreadcrumb">
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
    <span class="breadcrumb-text">Home</span>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/level1">
    <span class="breadcrumb-text">Level 1</span>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/level1/level2">
    <span class="breadcrumb-text">Level 2</span>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/level1/level2/level3">
    <span class="breadcrumb-text">Level 3</span>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>Current Page</wa-breadcrumb-item>
</wa-breadcrumb>

<style>
  @media (max-width: 768px) {
    #responsiveBreadcrumb wa-breadcrumb-item:not(:first-child):not(:last-child) {
      display: none;
    }

    /* Show ellipsis when items are hidden */
    #responsiveBreadcrumb wa-breadcrumb-item:first-child::after {
      content: '...';
      padding: 0 0.5rem;
    }
  }
</style>
```

### With Dynamic Content

```html
<wa-breadcrumb id="dynamicBreadcrumb">
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
</wa-breadcrumb>

<script>
  const breadcrumb = document.getElementById('dynamicBreadcrumb');

  function updateBreadcrumb(path) {
    // Clear existing items except home
    const items = breadcrumb.querySelectorAll('wa-breadcrumb-item');
    items.forEach((item, index) => {
      if (index > 0) item.remove();
    });

    // Add new items based on path
    const parts = path.split('/').filter(part => part);
    let currentPath = '';

    parts.forEach((part, index) => {
      currentPath += '/' + part;
      const item = document.createElement('wa-breadcrumb-item');

      // Last item should not be a link
      if (index < parts.length - 1) {
        item.href = currentPath;
      }

      item.textContent = part.charAt(0).toUpperCase() + part.slice(1);
      breadcrumb.appendChild(item);
    });
  }

  // Example usage
  updateBreadcrumb('/products/electronics/laptops');
</script>
```

### Breadcrumb with Actions

```html
<div style="display: flex; align-items: center; justify-content: space-between;">
  <wa-breadcrumb>
    <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
    <wa-breadcrumb-item href="/projects">Projects</wa-breadcrumb-item>
    <wa-breadcrumb-item>Website Redesign</wa-breadcrumb-item>
  </wa-breadcrumb>

  <div style="display: flex; gap: 0.5rem;">
    <wa-button size="small" variant="neutral">
      <wa-icon slot="start" name="star"></wa-icon>
      Favorite
    </wa-button>
    <wa-button size="small" variant="neutral">
      <wa-icon slot="start" name="share"></wa-icon>
      Share
    </wa-button>
  </div>
</div>
```

## CSS Parts

Use CSS parts to style internal breadcrumb elements:

```css
/* Style the breadcrumb container */
wa-breadcrumb::part(base) {
  padding: 0.5rem 1rem;
  background-color: var(--wa-color-neutral-50);
  border-radius: 4px;
}
```

## Customization

### Custom Breadcrumb Style

```css
/* Custom breadcrumb appearance */
wa-breadcrumb {
  padding: 0.75rem 1rem;
  background: linear-gradient(to right, #f8f9fa, #ffffff);
  border-bottom: 1px solid var(--wa-color-neutral-200);
}

wa-breadcrumb-item::part(base) {
  font-size: 0.875rem;
  font-weight: 500;
}

wa-breadcrumb-item[href]::part(base) {
  color: var(--wa-color-primary-600);
  text-decoration: none;
}

wa-breadcrumb-item[href]::part(base):hover {
  color: var(--wa-color-primary-700);
  text-decoration: underline;
}
```

### Compact Breadcrumb

```css
/* Compact style */
wa-breadcrumb.compact::part(base) {
  padding: 0.25rem 0.5rem;
}

wa-breadcrumb.compact wa-breadcrumb-item::part(base) {
  font-size: 0.75rem;
}
```

## Best Practices

- Always start with the home page or root level
- Keep breadcrumb labels short and clear
- Current page should not be a link
- Use consistent separators throughout the site
- Place breadcrumbs near the top of the page
- Don't use breadcrumbs for single-level sites
- Consider responsive behavior for mobile devices
- Use icons sparingly to avoid clutter
- Ensure breadcrumbs reflect the actual site hierarchy

## Accessibility

- Breadcrumbs are wrapped in a `<nav>` element
- Default ARIA label is "Breadcrumb"
- Current page has `aria-current="page"` automatically
- Links are keyboard navigable with Tab
- Sufficient color contrast for text and links
- Screen readers announce the navigation structure

```html
<!-- Good: accessible breadcrumb -->
<wa-breadcrumb label="Page navigation">
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products">Products</wa-breadcrumb-item>
  <wa-breadcrumb-item>Current Product</wa-breadcrumb-item>
</wa-breadcrumb>

<!-- Good: icon-only home with label -->
<wa-breadcrumb>
  <wa-breadcrumb-item href="/" aria-label="Home">
    <wa-icon slot="prefix" name="home"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/settings">Settings</wa-breadcrumb-item>
</wa-breadcrumb>
```

## Troubleshooting

### Breadcrumb Not Wrapping

**Problem:** Breadcrumbs overflow on small screens

**Solution:** Add responsive styles or truncate long text

```css
wa-breadcrumb {
  overflow: hidden;
}

wa-breadcrumb-item::part(base) {
  max-width: 150px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

@media (max-width: 768px) {
  wa-breadcrumb-item::part(base) {
    max-width: 100px;
  }
}
```

### Separator Not Showing

**Problem:** Custom separator doesn't appear

**Solution:** Ensure separator is in the correct slot

```html
<!-- Correct -->
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item>Page</wa-breadcrumb-item>
  <wa-icon slot="separator" name="chevron-right"></wa-icon>
</wa-breadcrumb>
```

### Links Not Working

**Problem:** Breadcrumb items don't navigate

**Solution:** Ensure `href` attribute is set on items that should be links

```html
<!-- Correct: with href -->
<wa-breadcrumb-item href="/page">Page</wa-breadcrumb-item>

<!-- Current page: no href -->
<wa-breadcrumb-item>Current Page</wa-breadcrumb-item>
```

## Related

- [Breadcrumb Item](./breadcrumb-item.md)
- [Icon](./icon.md)
- [Dropdown](./dropdown.md)
- [Menu](./menu.md)
