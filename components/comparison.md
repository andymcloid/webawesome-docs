# Comparison

A side-by-side image comparison component with an interactive draggable slider.

## Overview

The `<wa-comparison>` component provides an intuitive way to compare two images by displaying them side-by-side with a draggable divider. Users can slide to reveal more or less of each image, making it perfect for before/after comparisons, design mockups, and visual changes.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/comparison/comparison.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic image comparison -->
<wa-comparison>
  <img slot="before" src="before.jpg" alt="Before" />
  <img slot="after" src="after.jpg" alt="After" />
</wa-comparison>

<!-- With custom starting position (50% default) -->
<wa-comparison position="30">
  <img slot="before" src="original.jpg" alt="Original" />
  <img slot="after" src="edited.jpg" alt="Edited" />
</wa-comparison>
```

## Use Cases

### Before/After Photo Editing

```html
<wa-comparison position="50">
  <img
    slot="before"
    src="photo-original.jpg"
    alt="Original photo"
  />
  <img
    slot="after"
    src="photo-edited.jpg"
    alt="Edited photo with filters"
  />
</wa-comparison>
```

### Design Mockups

```html
<wa-comparison position="25">
  <img
    slot="before"
    src="design-v1.jpg"
    alt="Design version 1"
  />
  <img
    slot="after"
    src="design-v2.jpg"
    alt="Design version 2"
  />
</wa-comparison>
```

### Product Variants

```html
<wa-comparison position="50">
  <img
    slot="before"
    src="product-color-red.jpg"
    alt="Product in red"
  />
  <img
    slot="after"
    src="product-color-blue.jpg"
    alt="Product in blue"
  />
</wa-comparison>
```

### Responsive Comparisons

```html
<wa-comparison style="max-width: 800px; margin: 0 auto;">
  <img
    slot="before"
    src="mobile-before.jpg"
    alt="Before optimization"
    style="width: 100%; height: auto;"
  />
  <img
    slot="after"
    src="mobile-after.jpg"
    alt="After optimization"
    style="width: 100%; height: auto;"
  />
</wa-comparison>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `position` | number | `50` | No | Starting position of the divider (0-100) as percentage |

### Properties

```javascript
const comparison = document.querySelector('wa-comparison');

// Get current position
console.log(comparison.position); // 50

// Set position programmatically
comparison.position = 75;
```

## Examples

### Dynamic Position Control

```html
<wa-comparison id="photoComparison">
  <img slot="before" src="before.jpg" alt="Before" />
  <img slot="after" src="after.jpg" alt="After" />
</wa-comparison>

<wa-range
  id="positionSlider"
  min="0"
  max="100"
  value="50"
  label="Divider Position"
></wa-range>

<script>
  const comparison = document.getElementById('photoComparison');
  const slider = document.getElementById('positionSlider');

  slider.addEventListener('wa-input', (event) => {
    comparison.position = event.target.value;
  });

  // Sync slider when user drags divider
  comparison.addEventListener('wa-change', () => {
    slider.value = comparison.position;
  });
</script>
```

### With Labels

```html
<div style="position: relative;">
  <wa-comparison position="50">
    <img slot="before" src="before.jpg" alt="Before" />
    <img slot="after" src="after.jpg" alt="After" />
  </wa-comparison>

  <div style="position: absolute; top: 10px; left: 10px;
              background: rgba(0,0,0,0.7); color: white;
              padding: 0.5rem; border-radius: 4px;">
    Before
  </div>

  <div style="position: absolute; top: 10px; right: 10px;
              background: rgba(0,0,0,0.7); color: white;
              padding: 0.5rem; border-radius: 4px;">
    After
  </div>
</div>
```

### Image Gallery Comparison

```html
<div class="comparison-gallery">
  <h3>Summer vs Winter</h3>
  <wa-comparison position="50">
    <img slot="before" src="summer.jpg" alt="Summer scene" />
    <img slot="after" src="winter.jpg" alt="Winter scene" />
  </wa-comparison>

  <h3>Day vs Night</h3>
  <wa-comparison position="50">
    <img slot="before" src="day.jpg" alt="Daytime" />
    <img slot="after" src="night.jpg" alt="Nighttime" />
  </wa-comparison>
</div>
```

### Animated Position Change

```html
<wa-comparison id="animatedComparison" position="50">
  <img slot="before" src="before.jpg" alt="Before" />
  <img slot="after" src="after.jpg" alt="After" />
</wa-comparison>

<wa-button-group>
  <wa-button id="showBefore">Show Before</wa-button>
  <wa-button id="showAfter">Show After</wa-button>
  <wa-button id="showMiddle">Show Middle</wa-button>
</wa-button-group>

<script>
  const comparison = document.getElementById('animatedComparison');

  // Smooth transition with CSS
  comparison.style.setProperty('--divider-transition', 'transform 0.3s ease');

  document.getElementById('showBefore').addEventListener('click', () => {
    comparison.position = 10;
  });

  document.getElementById('showAfter').addEventListener('click', () => {
    comparison.position = 90;
  });

  document.getElementById('showMiddle').addEventListener('click', () => {
    comparison.position = 50;
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the divider handle | `void` |
| `blur()` | Removes focus from the divider handle | `void` |

### Method Examples

```javascript
const comparison = document.querySelector('wa-comparison');

// Focus the divider handle
comparison.focus();

// Remove focus
comparison.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Fired when the position changes (after drag ends) | `{ position: number }` |
| `wa-input` | Fired continuously while dragging | `{ position: number }` |

### Event Examples

```javascript
const comparison = document.querySelector('wa-comparison');

// Listen for position changes
comparison.addEventListener('wa-change', (event) => {
  console.log('Final position:', comparison.position);
});

// Listen for continuous updates while dragging
comparison.addEventListener('wa-input', (event) => {
  console.log('Current position:', comparison.position);
});

// Track user interaction
comparison.addEventListener('wa-change', () => {
  // Log analytics event
  analytics.track('comparison_slider_moved', {
    position: comparison.position
  });
});
```

## Slots

| Slot | Description |
|------|-------------|
| `before` | Content to display on the left/before side (typically an image) |
| `after` | Content to display on the right/after side (typically an image) |

### Slot Examples

```html
<!-- Images (most common) -->
<wa-comparison>
  <img slot="before" src="before.jpg" alt="Before" />
  <img slot="after" src="after.jpg" alt="After" />
</wa-comparison>

<!-- Videos -->
<wa-comparison>
  <video slot="before" src="before.mp4" autoplay loop muted></video>
  <video slot="after" src="after.mp4" autoplay loop muted></video>
</wa-comparison>

<!-- Canvas elements -->
<wa-comparison>
  <canvas slot="before" id="canvas-before"></canvas>
  <canvas slot="after" id="canvas-after"></canvas>
</wa-comparison>

<!-- Any HTML content -->
<wa-comparison>
  <div slot="before" style="background: linear-gradient(to right, red, yellow);">
    Before
  </div>
  <div slot="after" style="background: linear-gradient(to right, blue, green);">
    After
  </div>
</wa-comparison>
```

## CSS Parts

Use CSS parts to style internal comparison elements:

```css
/* Style the base container */
wa-comparison::part(base) {
  border-radius: 8px;
  overflow: hidden;
}

/* Style the divider line */
wa-comparison::part(divider) {
  background-color: #ff0000;
  width: 3px;
}

/* Style the handle (drag icon) */
wa-comparison::part(handle) {
  background-color: #ff0000;
  border-radius: 50%;
  width: 40px;
  height: 40px;
}
```

## Customization

### Custom Divider Colors

```css
/* Red divider theme */
wa-comparison.danger::part(divider) {
  background-color: #dc2626;
}

wa-comparison.danger::part(handle) {
  background-color: #dc2626;
  border: 2px solid white;
}

/* Success divider theme */
wa-comparison.success::part(divider) {
  background-color: #16a34a;
}

wa-comparison.success::part(handle) {
  background-color: #16a34a;
  border: 2px solid white;
}
```

### Custom Handle Size

```css
/* Larger handle for touch devices */
wa-comparison.touch::part(handle) {
  width: 60px;
  height: 60px;
}
```

### Custom Border and Shadow

```css
/* Styled comparison */
wa-comparison.styled::part(base) {
  border: 4px solid #e5e7eb;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}
```

## Best Practices

- ✅ Use images of the same dimensions for best results
- ✅ Ensure both images have the same aspect ratio
- ✅ Provide descriptive alt text for both images
- ✅ Use loading="lazy" for images below the fold
- ✅ Consider starting position based on what you want to emphasize
- ❌ Don't use drastically different sized images
- ❌ Avoid overly large images that may cause performance issues
- ❌ Don't forget alt text for accessibility

## Accessibility

- The divider handle is keyboard accessible (arrow keys to move)
- Ensure images have proper alt text for screen readers
- The component announces position changes to assistive technology
- Focus indicators are visible on the handle

```html
<!-- Accessible comparison with descriptive alt text -->
<wa-comparison>
  <img
    slot="before"
    src="room-before.jpg"
    alt="Living room before renovation with old furniture"
  />
  <img
    slot="after"
    src="room-after.jpg"
    alt="Living room after renovation with modern furniture"
  />
</wa-comparison>
```

### Keyboard Navigation

- **Arrow Keys (Left/Right)**: Move divider left or right
- **Home**: Move divider to far left (0%)
- **End**: Move divider to far right (100%)
- **Tab**: Focus/unfocus the handle

## Troubleshooting

### Images Don't Align Properly

**Problem:** Before and after images don't line up correctly

**Solution:** Ensure both images have identical dimensions and aspect ratios

```html
<!-- ✅ Correct - same dimensions -->
<wa-comparison>
  <img slot="before" src="before.jpg" width="800" height="600" alt="Before" />
  <img slot="after" src="after.jpg" width="800" height="600" alt="After" />
</wa-comparison>
```

### Divider Not Draggable

**Problem:** Can't drag the divider handle

**Solution:** Ensure the component has loaded properly and check for JavaScript errors

```javascript
// Verify component is defined
if (customElements.get('wa-comparison')) {
  console.log('Component loaded');
} else {
  console.error('Component not loaded');
}
```

### Position Not Updating

**Problem:** Setting position property doesn't update visually

**Solution:** Ensure you're setting a valid number between 0-100

```javascript
const comparison = document.querySelector('wa-comparison');

// ✅ Correct
comparison.position = 75;

// ❌ Wrong - out of range
comparison.position = 150; // Will be clamped to 100
```

## Related

- [Image](./image.md)
- [Range](./range.md)
- [Card](./card.md)
