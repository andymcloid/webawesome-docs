# Icon

Icons provide visual representations of actions, objects, or concepts.

## Overview

The `<wa-icon>` component renders icons from various icon libraries. It supports Font Awesome, Bootstrap Icons, and custom icon libraries, with flexible sizing and labeling options.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/icon/icon.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default icon -->
<wa-icon name="gear"></wa-icon>

<!-- Icon with specific size -->
<wa-icon name="heart" size="32px"></wa-icon>

<!-- Icon with accessibility label -->
<wa-icon name="search" label="Search"></wa-icon>

<!-- Icon from specific library -->
<wa-icon name="arrow-right" library="bootstrap"></wa-icon>
```

## Icon Libraries

### Font Awesome (Default)

Font Awesome icons are available by default:

```html
<!-- Regular style -->
<wa-icon name="house"></wa-icon>
<wa-icon name="user"></wa-icon>
<wa-icon name="gear"></wa-icon>
<wa-icon name="heart"></wa-icon>

<!-- Solid style (prefix with 'fas-') -->
<wa-icon name="fas-star"></wa-icon>
<wa-icon name="fas-circle-check"></wa-icon>

<!-- Brand icons (prefix with 'fab-') -->
<wa-icon name="fab-github"></wa-icon>
<wa-icon name="fab-twitter"></wa-icon>
<wa-icon name="fab-facebook"></wa-icon>
```

### Bootstrap Icons

Use Bootstrap Icons by specifying the library:

```html
<wa-icon name="check-circle" library="bootstrap"></wa-icon>
<wa-icon name="exclamation-triangle" library="bootstrap"></wa-icon>
<wa-icon name="info-circle" library="bootstrap"></wa-icon>
<wa-icon name="x-circle" library="bootstrap"></wa-icon>
```

### Custom Icon Libraries

Register custom icon libraries for your own icon sets:

```html
<script type="module">
  import { registerIconLibrary } from 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/utilities/icon-library.js';

  // Register a custom SVG sprite library
  registerIconLibrary('custom', {
    resolver: name => `/assets/icons/${name}.svg`,
    mutator: svg => svg.setAttribute('fill', 'currentColor')
  });
</script>

<!-- Use custom library icons -->
<wa-icon name="my-icon" library="custom"></wa-icon>
```

## Sizes

Control icon size with the `size` attribute:

```html
<!-- Specific pixel size -->
<wa-icon name="star" size="16px"></wa-icon>
<wa-icon name="star" size="24px"></wa-icon>
<wa-icon name="star" size="32px"></wa-icon>
<wa-icon name="star" size="48px"></wa-icon>
<wa-icon name="star" size="64px"></wa-icon>

<!-- Relative sizes -->
<wa-icon name="heart" size="1em"></wa-icon>
<wa-icon name="heart" size="2em"></wa-icon>
<wa-icon name="heart" size="3em"></wa-icon>

<!-- Responsive size -->
<wa-icon name="gear" size="clamp(16px, 5vw, 64px)"></wa-icon>
```

### Inline with Text

Icons scale with text when using relative units:

```html
<style>
  .text-with-icon {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 1rem;
  }

  .text-with-icon.large {
    font-size: 2rem;
  }
</style>

<div class="text-with-icon">
  <wa-icon name="info-circle" size="1em"></wa-icon>
  <span>Information message</span>
</div>

<div class="text-with-icon large">
  <wa-icon name="warning" size="1em"></wa-icon>
  <span>Large warning</span>
</div>
```

## Colors

Icons inherit the current text color by default:

```html
<!-- Inherit color from parent -->
<div style="color: red;">
  <wa-icon name="heart"></wa-icon>
</div>

<!-- Direct color styling -->
<wa-icon name="star" style="color: gold;"></wa-icon>
<wa-icon name="check-circle" style="color: green;"></wa-icon>
<wa-icon name="info-circle" style="color: blue;"></wa-icon>

<!-- Using CSS classes -->
<style>
  .icon-primary { color: #0066cc; }
  .icon-success { color: #28a745; }
  .icon-danger { color: #dc3545; }
</style>

<wa-icon name="info" class="icon-primary"></wa-icon>
<wa-icon name="check" class="icon-success"></wa-icon>
<wa-icon name="exclamation" class="icon-danger"></wa-icon>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `name` | string | - | Yes | The name of the icon to display |
| `size` | string | - | No | Size of the icon (accepts any valid CSS size value) |
| `library` | string | `'default'` | No | The icon library to use |
| `label` | string | - | No | Accessibility label for the icon |

## Examples

### Icon Buttons

```html
<wa-button circle>
  <wa-icon name="gear" label="Settings"></wa-icon>
</wa-button>

<wa-button circle variant="primary">
  <wa-icon name="plus" label="Add item"></wa-icon>
</wa-button>

<wa-button circle variant="danger">
  <wa-icon name="trash" label="Delete"></wa-icon>
</wa-button>

<!-- Button with icon and text -->
<wa-button>
  <wa-icon slot="start" name="download"></wa-icon>
  Download
</wa-button>

<wa-button variant="success">
  <wa-icon slot="start" name="check"></wa-icon>
  Save Changes
</wa-button>
```

### Icon Grid

```html
<style>
  .icon-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
    gap: 1rem;
    padding: 1rem;
  }

  .icon-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    padding: 1rem;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    text-align: center;
  }
</style>

<div class="icon-grid">
  <div class="icon-item">
    <wa-icon name="house" size="32px"></wa-icon>
    <small>house</small>
  </div>
  <div class="icon-item">
    <wa-icon name="user" size="32px"></wa-icon>
    <small>user</small>
  </div>
  <div class="icon-item">
    <wa-icon name="gear" size="32px"></wa-icon>
    <small>gear</small>
  </div>
  <div class="icon-item">
    <wa-icon name="heart" size="32px"></wa-icon>
    <small>heart</small>
  </div>
  <div class="icon-item">
    <wa-icon name="star" size="32px"></wa-icon>
    <small>star</small>
  </div>
  <div class="icon-item">
    <wa-icon name="bell" size="32px"></wa-icon>
    <small>bell</small>
  </div>
</div>
```

### Status Icons

```html
<style>
  .status-list {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .status-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .status-success { color: #28a745; }
  .status-warning { color: #ffc107; }
  .status-error { color: #dc3545; }
  .status-info { color: #17a2b8; }
</style>

<div class="status-list">
  <div class="status-item">
    <wa-icon name="check-circle" class="status-success" size="20px"></wa-icon>
    <span>All systems operational</span>
  </div>
  <div class="status-item">
    <wa-icon name="exclamation-triangle" class="status-warning" size="20px"></wa-icon>
    <span>Minor service degradation</span>
  </div>
  <div class="status-item">
    <wa-icon name="exclamation-circle" class="status-error" size="20px"></wa-icon>
    <span>Service outage detected</span>
  </div>
  <div class="status-item">
    <wa-icon name="info-circle" class="status-info" size="20px"></wa-icon>
    <span>Scheduled maintenance</span>
  </div>
</div>
```

### Animated Icons

```html
<style>
  @keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
  }

  .spin {
    display: inline-block;
    animation: spin 2s linear infinite;
  }

  .pulse {
    display: inline-block;
    animation: pulse 2s ease-in-out infinite;
  }
</style>

<!-- Spinning loading icon -->
<wa-icon name="spinner" size="32px" class="spin"></wa-icon>

<!-- Pulsing notification icon -->
<wa-icon name="bell" size="32px" class="pulse" style="color: #dc3545;"></wa-icon>

<!-- Loading with text -->
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <wa-icon name="spinner" size="20px" class="spin"></wa-icon>
  <span>Loading...</span>
</div>
```

### Icon with Badge

```html
<style>
  .icon-with-badge {
    position: relative;
    display: inline-block;
  }

  .icon-badge {
    position: absolute;
    top: -4px;
    right: -4px;
    background: #dc3545;
    color: white;
    border-radius: 50%;
    padding: 2px 6px;
    font-size: 10px;
    font-weight: bold;
  }
</style>

<div class="icon-with-badge">
  <wa-icon name="bell" size="32px"></wa-icon>
  <span class="icon-badge">5</span>
</div>

<div class="icon-with-badge">
  <wa-icon name="envelope" size="32px"></wa-icon>
  <span class="icon-badge">12</span>
</div>
```

### Navigation Menu

```html
<style>
  .nav-menu {
    display: flex;
    gap: 1rem;
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.25rem;
    padding: 0.5rem;
    cursor: pointer;
    color: #666;
    transition: color 0.2s;
  }

  .nav-item:hover,
  .nav-item.active {
    color: #0066cc;
  }
</style>

<ul class="nav-menu">
  <li class="nav-item active">
    <wa-icon name="house" size="24px"></wa-icon>
    <small>Home</small>
  </li>
  <li class="nav-item">
    <wa-icon name="search" size="24px"></wa-icon>
    <small>Search</small>
  </li>
  <li class="nav-item">
    <wa-icon name="user" size="24px"></wa-icon>
    <small>Profile</small>
  </li>
  <li class="nav-item">
    <wa-icon name="gear" size="24px"></wa-icon>
    <small>Settings</small>
  </li>
</ul>
```

## CSS Parts

Use CSS parts to style internal icon elements:

```css
/* Style the SVG element */
wa-icon::part(svg) {
  filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.2));
}

/* Style the icon wrapper */
wa-icon::part(base) {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

## Customization

### Custom Icon Color and Effects

```css
/* Gradient icon */
wa-icon.gradient::part(svg) {
  fill: url(#icon-gradient);
}

/* Shadow effect */
wa-icon.shadow::part(svg) {
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
}

/* Hover effect */
wa-icon.hover-scale {
  transition: transform 0.2s;
  cursor: pointer;
}

wa-icon.hover-scale:hover {
  transform: scale(1.2);
}
```

## Best Practices

- ✅ Always provide a `label` for icons without accompanying text
- ✅ Use consistent icon libraries throughout your application
- ✅ Match icon size to surrounding text for better visual balance
- ✅ Choose icons that clearly represent their function
- ✅ Use color to enhance meaning (green for success, red for danger)
- ❌ Don't use too many different icon styles in one interface
- ❌ Avoid decorative icons that don't add meaning
- ❌ Don't make icons too small to recognize (minimum 16px recommended)

## Accessibility

- Always provide a `label` attribute for standalone icons
- The label is used for screen readers via `aria-label`
- Icons used purely for decoration should have `aria-hidden="true"`
- Icons within buttons inherit the button's accessible name

```html
<!-- Accessible standalone icon -->
<wa-icon name="search" label="Search"></wa-icon>

<!-- Decorative icon (hidden from screen readers) -->
<wa-icon name="star" aria-hidden="true"></wa-icon>

<!-- Icon in button (button provides accessible name) -->
<wa-button aria-label="Settings">
  <wa-icon name="gear"></wa-icon>
</wa-button>

<!-- Icon with text (icon can be decorative) -->
<wa-button>
  <wa-icon name="download" aria-hidden="true"></wa-icon>
  Download
</wa-button>
```

## Troubleshooting

### Icon Not Displaying

**Problem:** Icon doesn't appear or shows a missing icon placeholder

**Solution:** Verify the icon name is correct for the library being used

```html
<!-- ✅ Correct Font Awesome icon -->
<wa-icon name="house"></wa-icon>

<!-- ❌ Wrong name -->
<wa-icon name="home"></wa-icon>

<!-- Check available icons in the library documentation -->
```

### Icon Size Issues

**Problem:** Icon appears too large or too small

**Solution:** Specify an explicit size or use relative units

```html
<!-- Explicit size -->
<wa-icon name="star" size="24px"></wa-icon>

<!-- Relative to font size -->
<wa-icon name="star" size="1em"></wa-icon>

<!-- CSS size -->
<wa-icon name="star" style="font-size: 24px;"></wa-icon>
```

### Custom Library Not Working

**Problem:** Custom icon library icons don't display

**Solution:** Ensure library is registered before icons are used

```javascript
import { registerIconLibrary } from 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/utilities/icon-library.js';

// Register before using icons
registerIconLibrary('custom', {
  resolver: name => `/assets/icons/${name}.svg`
});
```

## Related

- [Button](./button.md)
- [Icon Button](./icon-button.md)
- [Badge](./badge.md)
- [Icon Library Guide](../guides/icon-libraries.md)
