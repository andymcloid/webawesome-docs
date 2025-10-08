# Divider

Dividers visually separate content into distinct sections.

## Overview

The `<wa-divider>` component provides a horizontal or vertical line to create visual separation between content sections. It's perfect for organizing content in menus, layouts, and complex interfaces.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/divider/divider.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Horizontal divider (default) -->
<div>Section 1</div>
<wa-divider></wa-divider>
<div>Section 2</div>

<!-- Vertical divider -->
<div style="display: flex; align-items: center; gap: 1rem;">
  <span>Item 1</span>
  <wa-divider vertical></wa-divider>
  <span>Item 2</span>
  <wa-divider vertical></wa-divider>
  <span>Item 3</span>
</div>
```

## Horizontal Divider

The default orientation is horizontal, which creates a line that spans the full width of its container:

```html
<div>
  <p>First paragraph of content.</p>
  <wa-divider></wa-divider>
  <p>Second paragraph of content.</p>
</div>
```

## Vertical Divider

Use the `vertical` attribute to create a vertical divider:

```html
<div style="display: flex; align-items: center; gap: 1rem;">
  <wa-button>Edit</wa-button>
  <wa-divider vertical></wa-divider>
  <wa-button>Delete</wa-button>
  <wa-divider vertical></wa-divider>
  <wa-button>Share</wa-button>
</div>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `vertical` | boolean | `false` | No | When true, renders divider vertically instead of horizontally |

## Examples

### Menu Separator

```html
<wa-menu>
  <wa-menu-item>
    <wa-icon slot="start" name="file"></wa-icon>
    New File
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    New Folder
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-item>
    <wa-icon slot="start" name="upload"></wa-icon>
    Upload
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="download"></wa-icon>
    Download
  </wa-menu-item>
</wa-menu>
```

### Content Section Separator

```html
<article>
  <section>
    <h2>Introduction</h2>
    <p>This is the introduction to our article...</p>
  </section>

  <wa-divider></wa-divider>

  <section>
    <h2>Main Content</h2>
    <p>Here is the main content of the article...</p>
  </section>

  <wa-divider></wa-divider>

  <section>
    <h2>Conclusion</h2>
    <p>In conclusion, we have discussed...</p>
  </section>
</article>
```

### Toolbar with Vertical Dividers

```html
<div class="toolbar" style="display: flex; align-items: center; gap: 0.5rem; padding: 0.5rem;">
  <wa-button-group>
    <wa-button>
      <wa-icon name="text-bold"></wa-icon>
    </wa-button>
    <wa-button>
      <wa-icon name="text-italic"></wa-icon>
    </wa-button>
    <wa-button>
      <wa-icon name="text-underline"></wa-icon>
    </wa-button>
  </wa-button-group>

  <wa-divider vertical></wa-divider>

  <wa-button-group>
    <wa-button>
      <wa-icon name="text-align-left"></wa-icon>
    </wa-button>
    <wa-button>
      <wa-icon name="text-align-center"></wa-icon>
    </wa-button>
    <wa-button>
      <wa-icon name="text-align-right"></wa-icon>
    </wa-button>
  </wa-button-group>

  <wa-divider vertical></wa-divider>

  <wa-button>
    <wa-icon name="link"></wa-icon>
  </wa-button>
</div>
```

### Card with Sections

```html
<wa-card>
  <div slot="header">
    <h3>User Profile</h3>
  </div>

  <div style="padding: 1rem;">
    <p><strong>Name:</strong> Jane Doe</p>
    <p><strong>Email:</strong> jane@example.com</p>
  </div>

  <wa-divider></wa-divider>

  <div style="padding: 1rem;">
    <p><strong>Role:</strong> Administrator</p>
    <p><strong>Department:</strong> Engineering</p>
  </div>

  <wa-divider></wa-divider>

  <div slot="footer">
    <wa-button variant="primary">Edit Profile</wa-button>
  </div>
</wa-card>
```

### Inline List with Separators

```html
<div style="display: flex; align-items: center; gap: 1rem; flex-wrap: wrap;">
  <a href="/about">About</a>
  <wa-divider vertical style="height: 1rem;"></wa-divider>
  <a href="/contact">Contact</a>
  <wa-divider vertical style="height: 1rem;"></wa-divider>
  <a href="/privacy">Privacy</a>
  <wa-divider vertical style="height: 1rem;"></wa-divider>
  <a href="/terms">Terms</a>
</div>
```

## CSS Parts

Use CSS parts to customize the divider appearance:

```css
/* Style the divider line */
wa-divider::part(base) {
  border-color: #e5e7eb;
  border-width: 2px;
}

/* Dashed divider */
wa-divider.dashed::part(base) {
  border-style: dashed;
}

/* Dotted divider */
wa-divider.dotted::part(base) {
  border-style: dotted;
}
```

## Customization

### Custom Color

```css
/* Red divider */
wa-divider.red::part(base) {
  border-color: #ef4444;
}

/* Success divider */
wa-divider.success::part(base) {
  border-color: #10b981;
}
```

### Custom Thickness

```css
/* Thick divider */
wa-divider.thick::part(base) {
  border-width: 3px;
}

/* Thin divider */
wa-divider.thin::part(base) {
  border-width: 1px;
}
```

### Custom Spacing

```html
<!-- Add margin for spacing -->
<wa-divider style="margin: 2rem 0;"></wa-divider>

<!-- Compact spacing -->
<wa-divider style="margin: 0.5rem 0;"></wa-divider>
```

### Gradient Divider

```css
wa-divider.gradient::part(base) {
  border: none;
  height: 2px;
  background: linear-gradient(to right, transparent, #6366f1, transparent);
}
```

## Best Practices

- ✅ Use horizontal dividers to separate content sections
- ✅ Use vertical dividers in toolbars and inline navigation
- ✅ Ensure vertical dividers are within flex containers
- ✅ Adjust spacing around dividers for visual hierarchy
- ❌ Don't overuse dividers; white space can be sufficient
- ❌ Avoid using dividers when list styles can provide separation
- ❌ Don't use dividers as primary navigation elements

## Accessibility

- Dividers use the `separator` ARIA role by default
- Purely decorative and do not require additional ARIA labels
- Screen readers typically ignore dividers or announce them briefly
- Semantic HTML structure (headings, sections) is more important for accessibility than visual dividers

## Troubleshooting

### Vertical Divider Not Showing

**Problem:** Vertical divider is invisible or has no height

**Solution:** Ensure the parent container uses flexbox and has explicit height or content to define the height context

```html
<!-- ✅ Correct -->
<div style="display: flex; align-items: center; min-height: 40px;">
  <span>Item</span>
  <wa-divider vertical></wa-divider>
  <span>Item</span>
</div>

<!-- ❌ Won't display properly -->
<div>
  <span>Item</span>
  <wa-divider vertical></wa-divider>
  <span>Item</span>
</div>
```

### Divider Width Issues

**Problem:** Horizontal divider doesn't span full width

**Solution:** Ensure the parent container has defined width and the divider isn't inside an inline context

```css
/* Make parent block-level */
.container {
  display: block;
  width: 100%;
}
```

## Related

- [Menu](./menu.md)
- [Card](./card.md)
- [Toolbar](./toolbar.md)
- [Layout Guide](../guides/layout.md)
