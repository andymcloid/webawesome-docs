# Tooltip

Tooltips provide contextual information when users hover over or focus on an element.

## Overview

The `<wa-tooltip>` component displays a small popup with additional information about an element. It supports multiple placements, custom styling, and works with keyboard navigation for accessibility.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tooltip/tooltip.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default tooltip -->
<wa-tooltip content="This is a tooltip">
  <wa-button>Hover me</wa-button>
</wa-tooltip>

<!-- Tooltip on icon -->
<wa-tooltip content="Settings">
  <wa-icon name="gear" size="24px"></wa-icon>
</wa-tooltip>

<!-- Tooltip with HTML content -->
<wa-tooltip>
  <div slot="content">
    <strong>Bold text</strong><br />
    <small>Additional information</small>
  </div>
  <wa-button>Rich Content</wa-button>
</wa-tooltip>
```

## Placements

Control tooltip position with the `placement` attribute:

```html
<!-- Top placement (default) -->
<wa-tooltip content="Top tooltip" placement="top">
  <wa-button>Top</wa-button>
</wa-tooltip>

<!-- Right placement -->
<wa-tooltip content="Right tooltip" placement="right">
  <wa-button>Right</wa-button>
</wa-tooltip>

<!-- Bottom placement -->
<wa-tooltip content="Bottom tooltip" placement="bottom">
  <wa-button>Bottom</wa-button>
</wa-tooltip>

<!-- Left placement -->
<wa-tooltip content="Left tooltip" placement="left">
  <wa-button>Left</wa-button>
</wa-tooltip>
```

### Advanced Placements

```html
<!-- Top start -->
<wa-tooltip content="Top start" placement="top-start">
  <wa-button>Top Start</wa-button>
</wa-tooltip>

<!-- Top end -->
<wa-tooltip content="Top end" placement="top-end">
  <wa-button>Top End</wa-button>
</wa-tooltip>

<!-- Bottom start -->
<wa-tooltip content="Bottom start" placement="bottom-start">
  <wa-button>Bottom Start</wa-button>
</wa-tooltip>

<!-- Bottom end -->
<wa-tooltip content="Bottom end" placement="bottom-end">
  <wa-button>Bottom End</wa-button>
</wa-tooltip>

<!-- Left start -->
<wa-tooltip content="Left start" placement="left-start">
  <wa-button>Left Start</wa-button>
</wa-tooltip>

<!-- Right start -->
<wa-tooltip content="Right start" placement="right-start">
  <wa-button>Right Start</wa-button>
</wa-tooltip>
```

## Distance and Skidding

Fine-tune tooltip positioning:

```html
<!-- Increase distance from trigger -->
<wa-tooltip content="Farther away" distance="20">
  <wa-button>Distance 20px</wa-button>
</wa-tooltip>

<!-- Add skidding (horizontal offset) -->
<wa-tooltip content="Offset tooltip" skidding="20">
  <wa-button>Skidding 20px</wa-button>
</wa-tooltip>

<!-- Combine both -->
<wa-tooltip content="Custom position" distance="15" skidding="10">
  <wa-button>Custom</wa-button>
</wa-tooltip>
```

## Disabled State

Disable tooltips when needed:

```html
<wa-tooltip content="This won't show" disabled>
  <wa-button>Disabled Tooltip</wa-button>
</wa-tooltip>

<!-- Toggle tooltip dynamically -->
<wa-button id="toggleBtn">Toggle Tooltip</wa-button>

<wa-tooltip id="dynamicTooltip" content="Dynamic tooltip">
  <wa-button>Hover me</wa-button>
</wa-tooltip>

<script>
  const toggleBtn = document.getElementById('toggleBtn');
  const tooltip = document.getElementById('dynamicTooltip');

  toggleBtn.addEventListener('click', () => {
    tooltip.disabled = !tooltip.disabled;
    toggleBtn.textContent = tooltip.disabled ? 'Enable Tooltip' : 'Disable Tooltip';
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `content` | string | - | No | The tooltip content (plain text) |
| `placement` | string | `'top'` | No | Tooltip position: `top`, `top-start`, `top-end`, `right`, `right-start`, `right-end`, `bottom`, `bottom-start`, `bottom-end`, `left`, `left-start`, `left-end` |
| `disabled` | boolean | `false` | No | Disable the tooltip |
| `distance` | number | `8` | No | Distance in pixels from the trigger element |
| `skidding` | number | `0` | No | Offset in pixels along the trigger element |
| `trigger` | string | `'hover focus'` | No | Trigger events: `hover`, `focus`, `click`, or combination |
| `hoist` | boolean | `false` | No | Hoist tooltip to body to break out of containers |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Shows the tooltip | `Promise<void>` |
| `hide()` | Hides the tooltip | `Promise<void>` |

### Method Examples

```javascript
const tooltip = document.querySelector('wa-tooltip');

// Show tooltip programmatically
await tooltip.show();

// Hide tooltip programmatically
await tooltip.hide();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the tooltip starts to show | - |
| `wa-after-show` | Emitted after the tooltip has finished showing and animations are complete | - |
| `wa-hide` | Emitted when the tooltip starts to hide | - |
| `wa-after-hide` | Emitted after the tooltip has finished hiding and animations are complete | - |

### Event Examples

```javascript
const tooltip = document.querySelector('wa-tooltip');

tooltip.addEventListener('wa-show', () => {
  console.log('Tooltip is showing');
});

tooltip.addEventListener('wa-after-show', () => {
  console.log('Tooltip is now visible');
});

tooltip.addEventListener('wa-hide', () => {
  console.log('Tooltip is hiding');
});

tooltip.addEventListener('wa-after-hide', () => {
  console.log('Tooltip is now hidden');
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The element that triggers the tooltip |
| `content` | The tooltip content (supports HTML) |

## Examples

### Icon Buttons with Tooltips

```html
<style>
  .icon-toolbar {
    display: flex;
    gap: 0.5rem;
  }
</style>

<div class="icon-toolbar">
  <wa-tooltip content="Save">
    <wa-button circle variant="primary">
      <wa-icon name="floppy-disk"></wa-icon>
    </wa-button>
  </wa-tooltip>

  <wa-tooltip content="Copy">
    <wa-button circle>
      <wa-icon name="copy"></wa-icon>
    </wa-button>
  </wa-tooltip>

  <wa-tooltip content="Delete">
    <wa-button circle variant="danger">
      <wa-icon name="trash"></wa-icon>
    </wa-button>
  </wa-tooltip>

  <wa-tooltip content="Settings">
    <wa-button circle>
      <wa-icon name="gear"></wa-icon>
    </wa-button>
  </wa-tooltip>
</div>
```

### Rich Content Tooltips

```html
<wa-tooltip>
  <div slot="content">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-icon name="info-circle" style="color: #0066cc;"></wa-icon>
      <strong>Additional Information</strong>
    </div>
    <p style="margin: 0.5rem 0 0 0; font-size: 0.875rem;">
      This tooltip contains rich HTML content with multiple elements.
    </p>
  </div>
  <wa-button>Rich Tooltip</wa-button>
</wa-tooltip>
```

### Help Text

```html
<style>
  .form-field {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }
</style>

<div class="form-field">
  <wa-input label="Username" name="username" style="flex: 1;"></wa-input>
  <wa-tooltip content="Username must be 3-20 characters and contain only letters, numbers, and underscores">
    <wa-icon name="circle-question" size="20px" style="color: #666; cursor: help;"></wa-icon>
  </wa-tooltip>
</div>

<div class="form-field">
  <wa-input label="Email" name="email" type="email" style="flex: 1;"></wa-input>
  <wa-tooltip content="We'll never share your email with anyone else">
    <wa-icon name="circle-question" size="20px" style="color: #666; cursor: help;"></wa-icon>
  </wa-tooltip>
</div>
```

### Truncated Text

```html
<style>
  .truncated {
    max-width: 200px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
</style>

<wa-tooltip content="This is a very long text that has been truncated to fit in a small space">
  <div class="truncated">
    This is a very long text that has been truncated to fit in a small space
  </div>
</wa-tooltip>
```

### Disabled Elements

```html
<!-- Tooltips work on disabled buttons when wrapped -->
<wa-tooltip content="This action is currently unavailable">
  <span tabindex="0">
    <wa-button disabled style="pointer-events: none;">
      Disabled Action
    </wa-button>
  </span>
</wa-tooltip>
```

### Click Trigger

```html
<wa-tooltip content="Tooltip shown on click" trigger="click">
  <wa-button>Click me</wa-button>
</wa-tooltip>
```

### Manual Control

```html
<wa-button id="showTooltipBtn">Show Tooltip</wa-button>
<wa-button id="hideTooltipBtn">Hide Tooltip</wa-button>

<br /><br />

<wa-tooltip id="manualTooltip" content="Manually controlled tooltip" trigger="">
  <wa-button>Target Element</wa-button>
</wa-tooltip>

<script>
  const tooltip = document.getElementById('manualTooltip');
  const showBtn = document.getElementById('showTooltipBtn');
  const hideBtn = document.getElementById('hideTooltipBtn');

  showBtn.addEventListener('click', () => tooltip.show());
  hideBtn.addEventListener('click', () => tooltip.hide());
</script>
```

### Conditional Tooltips

```html
<wa-button id="conditionalBtn">Hover me</wa-button>

<wa-tooltip id="conditionalTooltip" content="This tooltip appears conditionally">
  <wa-button>Conditional Target</wa-button>
</wa-tooltip>

<script>
  const tooltip = document.getElementById('conditionalTooltip');
  const button = document.getElementById('conditionalBtn');

  // Enable/disable tooltip based on some condition
  button.addEventListener('click', () => {
    const shouldShow = Math.random() > 0.5;
    tooltip.disabled = !shouldShow;
    button.textContent = shouldShow ? 'Tooltip Enabled' : 'Tooltip Disabled';
  });
</script>
```

## CSS Parts

Use CSS parts to style internal tooltip elements:

```css
/* Style the tooltip popup */
wa-tooltip::part(popup) {
  background-color: #2c3e50;
  color: white;
  border-radius: 4px;
  padding: 0.5rem 0.75rem;
  font-size: 0.875rem;
}

/* Style the arrow */
wa-tooltip::part(arrow) {
  fill: #2c3e50;
}

/* Style the base wrapper */
wa-tooltip::part(base) {
  display: inline-block;
}
```

## Customization

### Custom Styling

```css
/* Large tooltip */
wa-tooltip.large::part(popup) {
  padding: 1rem 1.5rem;
  font-size: 1rem;
  max-width: 300px;
}

/* Colorful tooltip */
wa-tooltip.success::part(popup) {
  background-color: #28a745;
}

wa-tooltip.success::part(arrow) {
  fill: #28a745;
}

wa-tooltip.danger::part(popup) {
  background-color: #dc3545;
}

wa-tooltip.danger::part(arrow) {
  fill: #dc3545;
}
```

### Animation Customization

```css
/* Custom show/hide animation */
wa-tooltip::part(popup) {
  transition: opacity 0.3s ease, transform 0.3s ease;
}
```

## Best Practices

- ✅ Keep tooltip content concise and scannable
- ✅ Use tooltips for supplementary information, not critical content
- ✅ Ensure tooltips are accessible via keyboard (focus)
- ✅ Position tooltips to avoid obscuring important content
- ✅ Use consistent placement throughout your application
- ❌ Don't hide essential information in tooltips
- ❌ Avoid long paragraphs in tooltips
- ❌ Don't nest interactive elements inside tooltips
- ❌ Avoid using tooltips on mobile (consider alternatives)

## Accessibility

- Tooltips automatically include appropriate ARIA attributes
- Keyboard users can trigger tooltips by focusing on the trigger element
- Screen readers announce tooltip content
- Ensure tooltip triggers are keyboard accessible:

```html
<!-- Button is naturally keyboard accessible -->
<wa-tooltip content="Accessible tooltip">
  <wa-button>Accessible</wa-button>
</wa-tooltip>

<!-- Make non-interactive elements focusable -->
<wa-tooltip content="Text tooltip">
  <span tabindex="0" style="cursor: help;">
    Hover or focus me
  </span>
</wa-tooltip>
```

- Use appropriate `aria-label` or `aria-describedby` when needed
- Ensure sufficient color contrast in custom styled tooltips

## Troubleshooting

### Tooltip Cut Off

**Problem:** Tooltip is clipped by parent container

**Solution:** Use the `hoist` attribute to append tooltip to body

```html
<wa-tooltip content="This tooltip won't be clipped" hoist>
  <wa-button>Hoisted</wa-button>
</wa-tooltip>
```

### Tooltip Not Showing

**Problem:** Tooltip doesn't appear on hover

**Solution:** Check if tooltip is disabled or trigger element is properly wrapped

```html
<!-- ✅ Correct -->
<wa-tooltip content="Works">
  <wa-button>Hover me</wa-button>
</wa-tooltip>

<!-- ❌ Missing content -->
<wa-tooltip>
  <wa-button>No content</wa-button>
</wa-tooltip>

<!-- ❌ Disabled -->
<wa-tooltip content="Won't show" disabled>
  <wa-button>Disabled</wa-button>
</wa-tooltip>
```

### Tooltip Position Issues

**Problem:** Tooltip appears in wrong position

**Solution:** Adjust `placement`, `distance`, or `skidding`

```html
<!-- Try different placement -->
<wa-tooltip content="Better position" placement="right" distance="12">
  <wa-button>Adjusted</wa-button>
</wa-tooltip>
```

### Mobile Issues

**Problem:** Tooltips don't work well on mobile

**Solution:** Consider using alternative UI patterns for mobile

```javascript
// Disable tooltips on mobile
const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
const tooltips = document.querySelectorAll('wa-tooltip');

if (isMobile) {
  tooltips.forEach(tooltip => {
    tooltip.disabled = true;
  });
}
```

## Related

- [Popup](./popup.md)
- [Dropdown](./dropdown.md)
- [Popover](./popover.md)
- [Accessibility Guide](../guides/accessibility.md)
