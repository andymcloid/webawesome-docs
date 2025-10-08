# Popup

A utility component for creating positioned popup elements relative to anchors.

## Overview

The `<wa-popup>` component provides an advanced positioning system for floating elements like dropdowns, tooltips, popovers, and menus. It uses Floating UI under the hood to intelligently position content relative to an anchor element, with automatic collision detection and boundary awareness.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/popup/popup.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic popup -->
<wa-popup active>
  <span slot="anchor">Hover me</span>
  <div>This is a popup!</div>
</wa-popup>

<!-- With custom placement -->
<wa-popup placement="top" active>
  <button slot="anchor">Click me</button>
  <div class="popup-content">
    Popup content appears above
  </div>
</wa-popup>
```

## Placement Options

The popup can be positioned in 12 different locations relative to the anchor:

```html
<!-- Top placements -->
<wa-popup placement="top" active>
  <button slot="anchor">Top</button>
  <div>Above center</div>
</wa-popup>

<wa-popup placement="top-start" active>
  <button slot="anchor">Top Start</button>
  <div>Above left-aligned</div>
</wa-popup>

<wa-popup placement="top-end" active>
  <button slot="anchor">Top End</button>
  <div>Above right-aligned</div>
</wa-popup>

<!-- Bottom placements -->
<wa-popup placement="bottom" active>
  <button slot="anchor">Bottom</button>
  <div>Below center</div>
</wa-popup>

<wa-popup placement="bottom-start" active>
  <button slot="anchor">Bottom Start</button>
  <div>Below left-aligned</div>
</wa-popup>

<wa-popup placement="bottom-end" active>
  <button slot="anchor">Bottom End</button>
  <div>Below right-aligned</div>
</wa-popup>

<!-- Right placements -->
<wa-popup placement="right" active>
  <button slot="anchor">Right</button>
  <div>Right center</div>
</wa-popup>

<wa-popup placement="right-start" active>
  <button slot="anchor">Right Start</button>
  <div>Right top-aligned</div>
</wa-popup>

<wa-popup placement="right-end" active>
  <button slot="anchor">Right End</button>
  <div>Right bottom-aligned</div>
</wa-popup>

<!-- Left placements -->
<wa-popup placement="left" active>
  <button slot="anchor">Left</button>
  <div>Left center</div>
</wa-popup>

<wa-popup placement="left-start" active>
  <button slot="anchor">Left Start</button>
  <div>Left top-aligned</div>
</wa-popup>

<wa-popup placement="left-end" active>
  <button slot="anchor">Left End</button>
  <div>Left bottom-aligned</div>
</wa-popup>
```

## Positioning Strategy

### Absolute Positioning (Default)

```html
<!-- Absolute positioning - positioned relative to nearest positioned ancestor -->
<wa-popup placement="bottom" strategy="absolute" active>
  <button slot="anchor">Absolute</button>
  <div>Uses absolute positioning</div>
</wa-popup>
```

### Fixed Positioning

```html
<!-- Fixed positioning - positioned relative to viewport -->
<wa-popup placement="bottom" strategy="fixed" active>
  <button slot="anchor">Fixed</button>
  <div>Uses fixed positioning (stays in place when scrolling)</div>
</wa-popup>
```

## Distance and Skidding

```html
<!-- Custom distance (gap between anchor and popup) -->
<wa-popup placement="top" distance="20" active>
  <button slot="anchor">Distance 20</button>
  <div>20px gap from anchor</div>
</wa-popup>

<!-- Skidding (offset along the anchor) -->
<wa-popup placement="top" skidding="50" active>
  <button slot="anchor">Skidding 50</button>
  <div>Offset 50px to the right</div>
</wa-popup>

<!-- Combined distance and skidding -->
<wa-popup placement="bottom" distance="15" skidding="-20" active>
  <button slot="anchor">Custom Position</button>
  <div>15px below, 20px left</div>
</wa-popup>
```

## Arrow

Add an arrow pointing to the anchor element:

```html
<!-- Popup with arrow -->
<wa-popup placement="top" arrow active>
  <button slot="anchor">With Arrow</button>
  <div style="padding: 1rem; background: white; border-radius: 4px;">
    This popup has an arrow!
  </div>
</wa-popup>

<!-- Arrow with custom styling -->
<wa-popup placement="right" arrow active class="custom-arrow">
  <button slot="anchor">Custom Arrow</button>
  <div style="padding: 1rem; background: #1e293b; color: white; border-radius: 4px;">
    Custom styled arrow
  </div>
</wa-popup>

<style>
  .custom-arrow::part(arrow) {
    fill: #1e293b;
  }
</style>
```

## Flip and Shift

Enable automatic repositioning when the popup would overflow:

```html
<!-- Flip: Changes placement when there's not enough space -->
<wa-popup placement="top" flip active>
  <button slot="anchor" style="margin-top: 10px;">Flip Enabled</button>
  <div>Will flip to bottom if no space on top</div>
</wa-popup>

<!-- Shift: Slides along the axis to stay in view -->
<wa-popup placement="top" shift active>
  <button slot="anchor" style="margin-left: 10px;">Shift Enabled</button>
  <div>Will shift horizontally to stay in viewport</div>
</wa-popup>

<!-- Both flip and shift -->
<wa-popup placement="top" flip shift active>
  <button slot="anchor">Smart Positioning</button>
  <div>Will flip and shift to stay visible</div>
</wa-popup>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `active` | boolean | `false` | No | Shows or hides the popup |
| `placement` | string | `'bottom'` | No | Placement: `top`, `top-start`, `top-end`, `right`, `right-start`, `right-end`, `bottom`, `bottom-start`, `bottom-end`, `left`, `left-start`, `left-end` |
| `strategy` | string | `'absolute'` | No | Positioning strategy: `absolute` or `fixed` |
| `distance` | number | `0` | No | Distance in pixels from the anchor (gap) |
| `skidding` | number | `0` | No | Offset in pixels along the anchor axis |
| `arrow` | boolean | `false` | No | Shows an arrow pointing to the anchor |
| `flip` | boolean | `false` | No | Flips placement when there's not enough space |
| `shift` | boolean | `false` | No | Shifts the popup along the axis to stay in view |

### Properties

```javascript
const popup = document.querySelector('wa-popup');

// Show/hide popup
popup.active = true;
popup.active = false;

// Change placement
popup.placement = 'top-start';

// Adjust positioning
popup.distance = 10;
popup.skidding = 20;

// Enable features
popup.arrow = true;
popup.flip = true;
popup.shift = true;

// Change strategy
popup.strategy = 'fixed';
```

## Examples

### Interactive Popup

```html
<wa-popup id="interactivePopup" placement="bottom" arrow>
  <wa-button slot="anchor" id="popupTrigger">Toggle Popup</wa-button>
  <wa-card style="width: 300px;">
    <strong slot="header">Popup Menu</strong>
    <wa-menu>
      <wa-menu-item>Profile Settings</wa-menu-item>
      <wa-menu-item>Preferences</wa-menu-item>
      <wa-divider></wa-divider>
      <wa-menu-item>Logout</wa-menu-item>
    </wa-menu>
  </wa-card>
</wa-popup>

<script>
  const popup = document.getElementById('interactivePopup');
  const trigger = document.getElementById('popupTrigger');

  trigger.addEventListener('click', () => {
    popup.active = !popup.active;
  });

  // Close when clicking outside
  document.addEventListener('click', (event) => {
    if (!popup.contains(event.target) && popup.active) {
      popup.active = false;
    }
  });
</script>
```

### Tooltip Using Popup

```html
<wa-popup id="tooltip" placement="top" distance="8" arrow>
  <wa-icon-button slot="anchor" name="info-circle" id="tooltipAnchor"></wa-icon-button>
  <div style="background: #1e293b; color: white; padding: 0.5rem 0.75rem;
              border-radius: 4px; font-size: 0.875rem; max-width: 200px;">
    This is helpful information about the feature
  </div>
</wa-popup>

<script>
  const tooltip = document.getElementById('tooltip');
  const anchor = document.getElementById('tooltipAnchor');

  anchor.addEventListener('mouseenter', () => tooltip.active = true);
  anchor.addEventListener('mouseleave', () => popup.active = false);
</script>
```

### Context Menu

```html
<div id="contextArea" style="padding: 2rem; background: #f3f4f6; border-radius: 8px;">
  Right-click anywhere in this area
</div>

<wa-popup id="contextMenu" strategy="fixed" placement="bottom-start">
  <div slot="anchor" id="contextAnchor"></div>
  <wa-card style="min-width: 200px;">
    <wa-menu>
      <wa-menu-item>
        <wa-icon slot="prefix" name="copy"></wa-icon>
        Copy
      </wa-menu-item>
      <wa-menu-item>
        <wa-icon slot="prefix" name="cut"></wa-icon>
        Cut
      </wa-menu-item>
      <wa-menu-item>
        <wa-icon slot="prefix" name="clipboard"></wa-icon>
        Paste
      </wa-menu-item>
      <wa-divider></wa-divider>
      <wa-menu-item>
        <wa-icon slot="prefix" name="trash"></wa-icon>
        Delete
      </wa-menu-item>
    </wa-menu>
  </wa-card>
</wa-popup>

<script>
  const area = document.getElementById('contextArea');
  const menu = document.getElementById('contextMenu');
  const anchor = document.getElementById('contextAnchor');

  area.addEventListener('contextmenu', (event) => {
    event.preventDefault();

    // Position anchor at mouse coordinates
    anchor.style.position = 'fixed';
    anchor.style.left = event.clientX + 'px';
    anchor.style.top = event.clientY + 'px';

    menu.active = true;
  });

  document.addEventListener('click', () => {
    menu.active = false;
  });
</script>
```

### Dropdown Menu

```html
<wa-popup id="dropdown" placement="bottom-start" distance="4" flip shift>
  <wa-button slot="anchor" id="dropdownBtn">
    Options
    <wa-icon slot="end" name="chevron-down"></wa-icon>
  </wa-button>
  <wa-card style="width: 250px;">
    <wa-menu>
      <wa-menu-label>Account</wa-menu-label>
      <wa-menu-item>Profile</wa-menu-item>
      <wa-menu-item>Settings</wa-menu-item>
      <wa-menu-label>Actions</wa-menu-label>
      <wa-menu-item>Share</wa-menu-item>
      <wa-menu-item>Download</wa-menu-item>
      <wa-divider></wa-divider>
      <wa-menu-item variant="danger">Delete</wa-menu-item>
    </wa-menu>
  </wa-card>
</wa-popup>

<script>
  const dropdown = document.getElementById('dropdown');
  const btn = document.getElementById('dropdownBtn');

  btn.addEventListener('click', () => {
    dropdown.active = !dropdown.active;
  });

  // Close when clicking outside
  document.addEventListener('click', (event) => {
    if (!dropdown.contains(event.target) && dropdown.active) {
      dropdown.active = false;
    }
  });
</script>
```

### Date Picker Popup

```html
<wa-popup id="datePicker" placement="bottom-start" flip shift distance="4">
  <wa-input
    slot="anchor"
    id="dateInput"
    label="Select date"
    placeholder="Choose a date"
    readonly
  ></wa-input>
  <wa-card style="padding: 1rem;">
    <!-- Your custom date picker component here -->
    <div style="text-align: center;">
      <strong>December 2024</strong>
      <div style="display: grid; grid-template-columns: repeat(7, 1fr); gap: 0.5rem; margin-top: 1rem;">
        <!-- Days would be generated here -->
        <button style="padding: 0.5rem;">1</button>
        <button style="padding: 0.5rem;">2</button>
        <button style="padding: 0.5rem;">3</button>
        <!-- ... more days ... -->
      </div>
    </div>
  </wa-card>
</wa-popup>

<script>
  const datePicker = document.getElementById('datePicker');
  const dateInput = document.getElementById('dateInput');

  dateInput.addEventListener('click', () => {
    datePicker.active = true;
  });

  document.addEventListener('click', (event) => {
    if (!datePicker.contains(event.target) && datePicker.active) {
      datePicker.active = false;
    }
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `reposition()` | Recalculates and updates the popup position | `void` |

### Method Examples

```javascript
const popup = document.querySelector('wa-popup');

// Manually trigger repositioning (useful after content changes)
popup.reposition();

// Example: Reposition after dynamic content load
async function loadContent() {
  const content = await fetch('/api/content');
  popup.querySelector('.content').innerHTML = await content.text();
  popup.reposition(); // Update position after content changes
}
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-reposition` | Fired when the popup is repositioned | - |

### Event Examples

```javascript
const popup = document.querySelector('wa-popup');

// Listen for repositioning
popup.addEventListener('wa-reposition', () => {
  console.log('Popup was repositioned');
});

// Track popup visibility
popup.addEventListener('wa-reposition', () => {
  if (popup.active) {
    console.log('Popup is now visible at:', popup.placement);
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| `anchor` | The element that the popup is anchored to |
| (default) | The popup content |

### Slot Examples

```html
<!-- Basic slots -->
<wa-popup active>
  <button slot="anchor">Anchor Element</button>
  <div>Popup content</div>
</wa-popup>

<!-- Complex anchor -->
<wa-popup active>
  <div slot="anchor" style="display: inline-flex; align-items: center; gap: 0.5rem;">
    <wa-avatar image="user.jpg"></wa-avatar>
    <span>John Doe</span>
    <wa-icon name="chevron-down"></wa-icon>
  </div>
  <wa-card>
    <wa-menu>
      <wa-menu-item>Profile</wa-menu-item>
      <wa-menu-item>Logout</wa-menu-item>
    </wa-menu>
  </wa-card>
</wa-popup>

<!-- Rich content -->
<wa-popup active>
  <wa-button slot="anchor">Show Info</wa-button>
  <wa-card style="max-width: 400px;">
    <strong slot="header">Important Information</strong>
    <p>This is a detailed explanation of the feature.</p>
    <wa-button slot="footer" variant="primary">Got it</wa-button>
  </wa-card>
</wa-popup>
```

## CSS Parts

Use CSS parts to style internal popup elements:

```css
/* Style the popup container */
wa-popup::part(popup) {
  border-radius: 8px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

/* Style the arrow */
wa-popup::part(arrow) {
  fill: white;
}

/* Custom arrow border */
wa-popup::part(arrow) {
  fill: #1e293b;
  stroke: #0f172a;
  stroke-width: 1;
}
```

## Customization

### Custom Popup Styles

```css
/* Dark popup theme */
wa-popup.dark::part(popup) {
  background: #1e293b;
  color: white;
  border: 1px solid #334155;
}

wa-popup.dark::part(arrow) {
  fill: #1e293b;
  stroke: #334155;
  stroke-width: 1;
}

/* Elevated popup */
wa-popup.elevated::part(popup) {
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
              0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

/* Bordered popup */
wa-popup.bordered::part(popup) {
  border: 2px solid #e5e7eb;
  background: white;
}
```

### Animation

```css
/* Fade in animation */
wa-popup[active]::part(popup) {
  animation: fadeIn 0.2s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Scale animation */
wa-popup[active]::part(popup) {
  animation: scaleIn 0.15s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
```

## Best Practices

- ✅ Use `flip` and `shift` for better viewport awareness
- ✅ Set appropriate `distance` for visual separation
- ✅ Use `strategy="fixed"` for popups in scrollable containers
- ✅ Handle click-outside to close interactive popups
- ✅ Provide keyboard navigation (ESC to close)
- ❌ Don't nest popups inside each other
- ❌ Avoid extremely large popup content
- ❌ Don't forget to close popups when appropriate

## Accessibility

- Popups should be dismissible with the Escape key
- Interactive popups need proper focus management
- Use appropriate ARIA attributes for complex popups
- Ensure popup content is accessible to screen readers

```html
<!-- Accessible popup with ARIA -->
<wa-popup
  id="accessiblePopup"
  role="dialog"
  aria-labelledby="popup-title"
  aria-describedby="popup-desc"
>
  <wa-button slot="anchor">Open Dialog</wa-button>
  <wa-card>
    <h3 id="popup-title" slot="header">Confirmation</h3>
    <p id="popup-desc">Are you sure you want to continue?</p>
    <div slot="footer">
      <wa-button>Cancel</wa-button>
      <wa-button variant="primary">Confirm</wa-button>
    </div>
  </wa-card>
</wa-popup>

<script>
  const popup = document.getElementById('accessiblePopup');

  // Close on Escape key
  document.addEventListener('keydown', (event) => {
    if (event.key === 'Escape' && popup.active) {
      popup.active = false;
    }
  });

  // Trap focus within popup when open
  popup.addEventListener('wa-reposition', () => {
    if (popup.active) {
      const firstButton = popup.querySelector('wa-button');
      firstButton?.focus();
    }
  });
</script>
```

## Troubleshooting

### Popup Not Appearing

**Problem:** Popup is active but not visible

**Solution:** Check z-index stacking context and ensure parent elements don't have overflow: hidden

```css
/* Ensure popup appears above other content */
wa-popup::part(popup) {
  z-index: 1000;
}
```

### Incorrect Positioning

**Problem:** Popup appears in wrong location

**Solution:** Call `reposition()` after content changes or use `flip` and `shift`

```javascript
const popup = document.querySelector('wa-popup');

// After adding content
popup.querySelector('.content').innerHTML = 'New content';
popup.reposition();
```

### Anchor Not Found

**Problem:** Console error about missing anchor

**Solution:** Ensure anchor element is in the `anchor` slot

```html
<!-- ✅ Correct -->
<wa-popup>
  <button slot="anchor">Anchor</button>
  <div>Content</div>
</wa-popup>

<!-- ❌ Wrong - missing slot attribute -->
<wa-popup>
  <button>Anchor</button>
  <div>Content</div>
</wa-popup>
```

## Related

- [Dropdown](./dropdown.md)
- [Tooltip](./tooltip.md)
- [Menu](./menu.md)
- [Dialog](./dialog.md)
- [Popover](./popover.md)
