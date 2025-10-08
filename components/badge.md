# Badge

Badges are used to draw attention to important information or status indicators.

## Overview

The `<wa-badge>` component provides a compact way to display small amounts of information, counts, or status indicators. It supports multiple variants, pill shapes, and pulse animations.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/badge/badge.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default badge -->
<wa-badge>Badge</wa-badge>

<!-- Badge with variant -->
<wa-badge variant="primary">Primary</wa-badge>

<!-- Pill badge -->
<wa-badge pill>Pill</wa-badge>

<!-- Pulsing badge -->
<wa-badge variant="danger" pulse>5</wa-badge>
```

## Variants

Badges support multiple visual variants to convey different meanings:

```html
<wa-badge variant="primary">Primary</wa-badge>
<wa-badge variant="success">Success</wa-badge>
<wa-badge variant="neutral">Neutral</wa-badge>
<wa-badge variant="warning">Warning</wa-badge>
<wa-badge variant="danger">Danger</wa-badge>
```

## Pill Shape

Make badges rounded with the `pill` attribute:

```html
<wa-badge variant="primary" pill>Primary</wa-badge>
<wa-badge variant="success" pill>Success</wa-badge>
<wa-badge variant="neutral" pill>Neutral</wa-badge>
<wa-badge variant="warning" pill>Warning</wa-badge>
<wa-badge variant="danger" pill>Danger</wa-badge>
```

## Pulse Animation

Add the `pulse` attribute to create an attention-grabbing animation:

```html
<wa-badge variant="primary" pulse>1</wa-badge>
<wa-badge variant="success" pulse>2</wa-badge>
<wa-badge variant="danger" pulse>9+</wa-badge>
```

### Pulse with Pill

```html
<wa-badge variant="danger" pill pulse>New</wa-badge>
<wa-badge variant="warning" pill pulse>Hot</wa-badge>
<wa-badge variant="success" pill pulse>Live</wa-badge>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `variant` | string | `'primary'` | No | Badge variant: `primary`, `success`, `neutral`, `warning`, `danger` |
| `pill` | boolean | `false` | No | Render badge with rounded ends |
| `pulse` | boolean | `false` | No | Add pulsing animation to draw attention |

## Examples

### Notification Counts

```html
<style>
  .icon-with-badge {
    position: relative;
    display: inline-block;
  }

  .badge-overlay {
    position: absolute;
    top: -8px;
    right: -8px;
  }
</style>

<div class="icon-with-badge">
  <wa-icon name="bell" size="24px"></wa-icon>
  <wa-badge variant="danger" pill pulse class="badge-overlay">5</wa-badge>
</div>

<div class="icon-with-badge">
  <wa-icon name="envelope" size="24px"></wa-icon>
  <wa-badge variant="primary" pill class="badge-overlay">12</wa-badge>
</div>

<div class="icon-with-badge">
  <wa-icon name="shopping-cart" size="24px"></wa-icon>
  <wa-badge variant="success" pill class="badge-overlay">3</wa-badge>
</div>
```

### Status Indicators

```html
<style>
  .status-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
  }
</style>

<div class="status-item">
  <span>Online</span>
  <wa-badge variant="success" pill>Active</wa-badge>
</div>

<div class="status-item">
  <span>Server Status</span>
  <wa-badge variant="warning" pill>Maintenance</wa-badge>
</div>

<div class="status-item">
  <span>Database</span>
  <wa-badge variant="danger" pill pulse>Offline</wa-badge>
</div>

<div class="status-item">
  <span>API</span>
  <wa-badge variant="neutral" pill>Idle</wa-badge>
</div>
```

### List Items with Badges

```html
<style>
  .list-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.75rem;
    border-bottom: 1px solid #e0e0e0;
  }

  .list-item-content {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }

  .list-item-title {
    font-weight: 600;
  }

  .list-item-subtitle {
    font-size: 0.875rem;
    color: #666;
  }
</style>

<div class="list-item">
  <div class="list-item-content">
    <div class="list-item-title">Project Alpha</div>
    <div class="list-item-subtitle">Due in 3 days</div>
  </div>
  <wa-badge variant="warning" pill>In Progress</wa-badge>
</div>

<div class="list-item">
  <div class="list-item-content">
    <div class="list-item-title">Project Beta</div>
    <div class="list-item-subtitle">Completed yesterday</div>
  </div>
  <wa-badge variant="success" pill>Complete</wa-badge>
</div>

<div class="list-item">
  <div class="list-item-content">
    <div class="list-item-title">Project Gamma</div>
    <div class="list-item-subtitle">Overdue by 2 days</div>
  </div>
  <wa-badge variant="danger" pill pulse>Urgent</wa-badge>
</div>
```

### Tag Collection

```html
<style>
  .tag-collection {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }
</style>

<div class="tag-collection">
  <wa-badge variant="primary" pill>JavaScript</wa-badge>
  <wa-badge variant="primary" pill>TypeScript</wa-badge>
  <wa-badge variant="success" pill>HTML</wa-badge>
  <wa-badge variant="success" pill>CSS</wa-badge>
  <wa-badge variant="neutral" pill>Web Components</wa-badge>
  <wa-badge variant="warning" pill>Beta</wa-badge>
</div>
```

### Button with Badge

```html
<wa-button>
  Notifications
  <wa-badge variant="danger" pill pulse style="margin-left: 0.5rem;">9+</wa-badge>
</wa-button>

<wa-button variant="primary">
  Messages
  <wa-badge variant="neutral" pill style="margin-left: 0.5rem;">3</wa-badge>
</wa-button>

<wa-button variant="success">
  Cart
  <wa-badge variant="warning" pill style="margin-left: 0.5rem;">5</wa-badge>
</wa-button>
```

### Card Header with Badge

```html
<style>
  .card {
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 1.5rem;
    max-width: 400px;
  }

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  .card-title {
    font-size: 1.25rem;
    font-weight: 600;
  }

  .card-content {
    color: #666;
  }
</style>

<div class="card">
  <div class="card-header">
    <h3 class="card-title">New Features</h3>
    <wa-badge variant="success" pill pulse>3 New</wa-badge>
  </div>
  <div class="card-content">
    Check out the latest features and improvements in this release.
  </div>
</div>
```

### Dynamic Badge Updates

```html
<wa-button id="incrementBtn">Add Item</wa-button>
<wa-button id="decrementBtn">Remove Item</wa-button>
<wa-button id="resetBtn">Reset</wa-button>

<div style="margin-top: 1rem;">
  <div class="icon-with-badge">
    <wa-icon name="shopping-cart" size="32px"></wa-icon>
    <wa-badge id="cartBadge" variant="primary" pill class="badge-overlay">0</wa-badge>
  </div>
</div>

<script>
  const cartBadge = document.getElementById('cartBadge');
  const incrementBtn = document.getElementById('incrementBtn');
  const decrementBtn = document.getElementById('decrementBtn');
  const resetBtn = document.getElementById('resetBtn');

  let count = 0;

  function updateBadge() {
    cartBadge.textContent = count;

    if (count === 0) {
      cartBadge.variant = 'neutral';
      cartBadge.pulse = false;
    } else if (count <= 5) {
      cartBadge.variant = 'primary';
      cartBadge.pulse = false;
    } else if (count <= 10) {
      cartBadge.variant = 'warning';
      cartBadge.pulse = true;
    } else {
      cartBadge.variant = 'danger';
      cartBadge.pulse = true;
    }
  }

  incrementBtn.addEventListener('click', () => {
    count++;
    updateBadge();
  });

  decrementBtn.addEventListener('click', () => {
    if (count > 0) {
      count--;
      updateBadge();
    }
  });

  resetBtn.addEventListener('click', () => {
    count = 0;
    updateBadge();
  });
</script>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The badge's content |

## CSS Parts

Use CSS parts to style internal badge elements:

```css
/* Style the base badge */
wa-badge::part(base) {
  padding: 0.25rem 0.75rem;
  font-size: 0.875rem;
  font-weight: 600;
  letter-spacing: 0.5px;
}

/* Custom pulse animation */
@keyframes custom-pulse {
  0%, 100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(1.05);
  }
}

wa-badge[pulse]::part(base) {
  animation: custom-pulse 1.5s ease-in-out infinite;
}
```

## Customization

### Custom Badge Colors

```css
/* Custom brand badge */
wa-badge.brand::part(base) {
  background-color: #6366f1;
  color: white;
}

/* Custom info badge */
wa-badge.info::part(base) {
  background-color: #3b82f6;
  color: white;
}

/* Outline badge */
wa-badge.outline::part(base) {
  background-color: transparent;
  border: 2px solid currentColor;
  color: #6366f1;
}
```

### Size Variations

```css
/* Small badge */
wa-badge.small::part(base) {
  font-size: 0.625rem;
  padding: 0.125rem 0.5rem;
}

/* Large badge */
wa-badge.large::part(base) {
  font-size: 1rem;
  padding: 0.5rem 1rem;
}
```

## Best Practices

- ✅ Use badges for supplementary information, not primary content
- ✅ Keep badge text short (1-3 characters for counts, 1-2 words for labels)
- ✅ Use appropriate variants to convey meaning (danger for alerts, success for completion)
- ✅ Use pulse animation sparingly for high-priority notifications
- ✅ Ensure sufficient color contrast for readability
- ❌ Don't overuse badges - they lose impact when too common
- ❌ Avoid long text in badges - use tooltips or labels instead
- ❌ Don't use badges as the only indicator of important information

## Accessibility

- Badges automatically include appropriate semantic markup
- Ensure badge text is readable with sufficient contrast
- For icon-only badges or count badges, consider adding `aria-label`:

```html
<!-- Badge with accessible label -->
<div class="icon-with-badge" aria-label="5 unread notifications">
  <wa-icon name="bell" size="24px"></wa-icon>
  <wa-badge variant="danger" pill pulse class="badge-overlay">5</wa-badge>
</div>

<!-- Status badge with context -->
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <span id="status-label">Server Status:</span>
  <wa-badge variant="success" pill aria-labelledby="status-label">Online</wa-badge>
</div>
```

- Don't rely solely on color to convey information
- Pulsing badges should be used judiciously to avoid distracting users

## Troubleshooting

### Badge Too Small

**Problem:** Badge text is difficult to read

**Solution:** Increase font size or padding using CSS parts

```css
wa-badge::part(base) {
  font-size: 0.9rem;
  padding: 0.3rem 0.8rem;
}
```

### Badge Not Aligned

**Problem:** Badge doesn't align properly with surrounding content

**Solution:** Use flexbox or adjust positioning

```html
<style>
  .aligned-content {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
</style>

<div class="aligned-content">
  <span>Status</span>
  <wa-badge variant="success">Active</wa-badge>
</div>
```

### Pulse Animation Not Working

**Problem:** Pulse attribute doesn't create animation

**Solution:** Ensure the `pulse` attribute is set correctly

```html
<!-- ✅ Correct -->
<wa-badge pulse>Badge</wa-badge>
<wa-badge pulse="true">Badge</wa-badge>

<!-- ❌ Won't work -->
<wa-badge pulse="false">Badge</wa-badge>
```

## Related

- [Button](./button.md)
- [Icon](./icon.md)
- [Tag](./tag.md)
- [Status Indicators Guide](../guides/status-indicators.md)
