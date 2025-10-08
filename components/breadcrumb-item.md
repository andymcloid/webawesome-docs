# Breadcrumb Item

Breadcrumb items represent individual levels in a breadcrumb navigation trail.

## Overview

The `<wa-breadcrumb-item>` component is used inside `<wa-breadcrumb>` to create individual navigation points in a hierarchical trail. Items can be rendered as links or plain text.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/breadcrumb-item/breadcrumb-item.js';
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
  <wa-breadcrumb-item>Subcategory</wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Links

Use the `href` attribute to make items clickable:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products">Products</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products/electronics">Electronics</wa-breadcrumb-item>
  <wa-breadcrumb-item>Current Product</wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Prefix Icons

Add icons before the label:

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
  <wa-breadcrumb-item>
    <wa-icon slot="prefix" name="file"></wa-icon>
    Report.pdf
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Suffix Icons

Add icons after the label:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/dashboard">
    Dashboard
    <wa-icon slot="suffix" name="external-link"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>Analytics</wa-breadcrumb-item>
</wa-breadcrumb>
```

## Icon Only

Create icon-only breadcrumb items:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/" aria-label="Home">
    <wa-icon slot="prefix" name="home"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/settings" aria-label="Settings">
    <wa-icon slot="prefix" name="settings"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item aria-label="Profile">
    <wa-icon slot="prefix" name="user"></wa-icon>
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

## Custom Separator

Override the default separator for specific items:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products">Products</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/products/electronics">
    Electronics
    <wa-icon slot="separator" name="arrow-right"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>Laptop</wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Badges

Add badges to show counts or status:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
    Home
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/inbox">
    <wa-icon slot="prefix" name="inbox"></wa-icon>
    Inbox
    <wa-badge slot="suffix" variant="primary" pill>12</wa-badge>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    Unread Messages
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

## With Dropdowns

Embed dropdowns for complex navigation:

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
        <wa-menu-item value="web">Web Projects</wa-menu-item>
        <wa-menu-item value="mobile">Mobile Projects</wa-menu-item>
        <wa-menu-item value="api">API Projects</wa-menu-item>
      </wa-menu>
    </wa-dropdown>
  </wa-breadcrumb-item>

  <wa-breadcrumb-item href="/projects/web/ecommerce">E-commerce Site</wa-breadcrumb-item>
  <wa-breadcrumb-item>Dashboard</wa-breadcrumb-item>
</wa-breadcrumb>
```

## External Links

Mark external links with visual indicators:

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">Home</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/docs">Documentation</wa-breadcrumb-item>
  <wa-breadcrumb-item href="https://example.com" target="_blank" rel="noopener noreferrer">
    External Resource
    <wa-icon slot="suffix" name="external-link"></wa-icon>
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `href` | string | - | No | When set, renders the item as a link |
| `target` | string | - | No | Link target (requires `href`) |
| `rel` | string | - | No | Link relationship (requires `href`) |

## Slots

| Slot | Description |
|------|-------------|
| (default) | The breadcrumb item label |
| `prefix` | Content before the label (typically icons) |
| `suffix` | Content after the label (typically icons or badges) |
| `separator` | Custom separator for this specific item |

## Examples

### File System Breadcrumb

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/drive">
    <wa-icon slot="prefix" name="hard-drive"></wa-icon>
    My Drive
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/drive/documents">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Documents
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/drive/documents/projects">
    <wa-icon slot="prefix" name="folder"></wa-icon>
    Projects
    <wa-badge slot="suffix" variant="primary" pill>4</wa-badge>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    <wa-icon slot="prefix" name="file-text"></wa-icon>
    proposal.docx
  </wa-breadcrumb-item>
  <wa-icon slot="separator" name="chevron-right"></wa-icon>
</wa-breadcrumb>
```

### E-commerce Navigation

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="home"></wa-icon>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop">
    <wa-icon slot="prefix" name="shopping-bag"></wa-icon>
    Shop
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop/clothing">
    Clothing
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/shop/clothing/mens">
    Men's
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    Cotton T-Shirt
    <wa-badge slot="suffix" variant="success">Sale</wa-badge>
  </wa-breadcrumb-item>
</wa-breadcrumb>
```

### Admin Dashboard Navigation

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/admin">
    <wa-icon slot="prefix" name="shield"></wa-icon>
    Admin
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/admin/users">
    <wa-icon slot="prefix" name="users"></wa-icon>
    Users
    <wa-badge slot="suffix" variant="primary" pill>1,234</wa-badge>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/admin/users/active">
    Active Users
    <wa-badge slot="suffix" variant="success" pill>892</wa-badge>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>User Details</wa-breadcrumb-item>
</wa-breadcrumb>
```

### Documentation Site

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/">
    <wa-icon slot="prefix" name="book-open"></wa-icon>
    Documentation
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/components">
    <wa-icon slot="prefix" name="box"></wa-icon>
    Components
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/components/navigation">
    <wa-icon slot="prefix" name="compass"></wa-icon>
    Navigation
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>
    <wa-icon slot="prefix" name="link"></wa-icon>
    Breadcrumb
  </wa-breadcrumb-item>
  <wa-icon slot="separator" name="slash"></wa-icon>
</wa-breadcrumb>
```

### With Status Indicators

```html
<wa-breadcrumb>
  <wa-breadcrumb-item href="/projects">Projects</wa-breadcrumb-item>
  <wa-breadcrumb-item href="/projects/website-redesign">
    Website Redesign
    <div slot="suffix" style="width: 8px; height: 8px; border-radius: 50%; background: var(--wa-color-success-600);"></div>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item href="/projects/website-redesign/tasks">
    Tasks
    <wa-badge slot="suffix" variant="warning" pill>5 pending</wa-badge>
  </wa-breadcrumb-item>
  <wa-breadcrumb-item>Task Details</wa-breadcrumb-item>
</wa-breadcrumb>
```

## CSS Parts

Use CSS parts to style internal breadcrumb item elements:

```css
/* Style the breadcrumb item base */
wa-breadcrumb-item::part(base) {
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  transition: background-color 0.2s;
}

/* Style linked items */
wa-breadcrumb-item[href]::part(base) {
  color: var(--wa-color-primary-600);
  text-decoration: none;
}

/* Style hovered links */
wa-breadcrumb-item[href]::part(base):hover {
  background-color: var(--wa-color-primary-50);
  color: var(--wa-color-primary-700);
}

/* Style the label */
wa-breadcrumb-item::part(label) {
  font-size: 0.875rem;
  font-weight: 500;
}

/* Style the prefix slot */
wa-breadcrumb-item::part(prefix) {
  margin-right: 0.5rem;
}

/* Style the suffix slot */
wa-breadcrumb-item::part(suffix) {
  margin-left: 0.5rem;
}

/* Style the separator */
wa-breadcrumb-item::part(separator) {
  margin: 0 0.5rem;
  color: var(--wa-color-neutral-400);
}
```

## Customization

### Custom Link Colors

```css
/* Custom link styling */
wa-breadcrumb-item[href]::part(base) {
  color: #6366f1;
}

wa-breadcrumb-item[href]::part(base):hover {
  color: #4f46e5;
  background-color: #eef2ff;
}

/* Current page styling */
wa-breadcrumb-item:not([href])::part(base) {
  color: var(--wa-color-neutral-700);
  font-weight: 600;
}
```

### Compact Items

```css
/* Compact breadcrumb items */
wa-breadcrumb-item.compact::part(base) {
  padding: 0.125rem 0.25rem;
}

wa-breadcrumb-item.compact::part(label) {
  font-size: 0.75rem;
}

wa-breadcrumb-item.compact::part(separator) {
  margin: 0 0.25rem;
}
```

### Custom Hover Effects

```css
/* Custom hover effect */
wa-breadcrumb-item[href]::part(base) {
  position: relative;
  transition: all 0.2s;
}

wa-breadcrumb-item[href]::part(base):hover {
  transform: translateY(-1px);
}

wa-breadcrumb-item[href]::part(base)::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--wa-color-primary-600);
  transform: scaleX(0);
  transition: transform 0.2s;
}

wa-breadcrumb-item[href]::part(base):hover::after {
  transform: scaleX(1);
}
```

## Best Practices

- Use `href` for all items except the current page
- Keep labels short and descriptive
- Use icons consistently across all items or not at all
- Ensure sufficient color contrast between links and text
- Add `aria-label` for icon-only items
- Use `target="_blank"` with `rel="noopener noreferrer"` for external links
- Don't make the current page clickable
- Use badges sparingly to show important counts or status

## Accessibility

- Items without `href` automatically have `aria-current="page"`
- Links are keyboard navigable with Tab
- Icon-only items should include `aria-label`
- Sufficient color contrast for text and links
- Screen readers announce links and current page
- Focus indicators are visible on keyboard navigation

```html
<!-- Good: accessible icon-only item -->
<wa-breadcrumb-item href="/" aria-label="Home">
  <wa-icon slot="prefix" name="home"></wa-icon>
</wa-breadcrumb-item>

<!-- Good: external link with proper attributes -->
<wa-breadcrumb-item
  href="https://example.com"
  target="_blank"
  rel="noopener noreferrer"
  aria-label="External documentation (opens in new tab)">
  External Docs
  <wa-icon slot="suffix" name="external-link"></wa-icon>
</wa-breadcrumb-item>

<!-- Good: clear current page -->
<wa-breadcrumb-item>Current Page</wa-breadcrumb-item>
```

## Troubleshooting

### Item Not Rendering as Link

**Problem:** Item displays as text even with `href` attribute

**Solution:** Ensure the `href` attribute has a valid value

```html
<!-- Correct -->
<wa-breadcrumb-item href="/page">Page</wa-breadcrumb-item>

<!-- Incorrect: empty href -->
<wa-breadcrumb-item href="">Page</wa-breadcrumb-item>
```

### Icon Not Showing

**Problem:** Icon doesn't appear in the breadcrumb item

**Solution:** Ensure icon is in the correct slot

```html
<!-- Correct: prefix slot -->
<wa-breadcrumb-item>
  <wa-icon slot="prefix" name="home"></wa-icon>
  Home
</wa-breadcrumb-item>

<!-- Incorrect: no slot -->
<wa-breadcrumb-item>
  <wa-icon name="home"></wa-icon>
  Home
</wa-breadcrumb-item>
```

### Separator Not Showing

**Problem:** Custom separator doesn't appear

**Solution:** Check separator is in the correct slot and only one separator is used

```html
<!-- Correct: one separator in separator slot -->
<wa-breadcrumb-item>
  Page
  <wa-icon slot="separator" name="chevron-right"></wa-icon>
</wa-breadcrumb-item>
```

## Related

- [Breadcrumb](./breadcrumb.md)
- [Icon](./icon.md)
- [Badge](./badge.md)
- [Dropdown](./dropdown.md)
- [Button](./button.md)
