# Image Comparer

Compare two images side-by-side with an interactive slider.

## Overview

The `<wa-image-comparer>` component provides an intuitive way to compare two images using a draggable slider. It's perfect for before/after comparisons, design iterations, image processing results, and any scenario where you need to visually compare two similar images.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/image-comparer/image-comparer.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-image-comparer>
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>
```

## Slider Position

Control the initial position of the divider:

```html
<!-- Start at 25% -->
<wa-image-comparer position="25">
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>

<!-- Start at 75% -->
<wa-image-comparer position="75">
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>

<!-- Default position (50%) -->
<wa-image-comparer>
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>
```

## Custom Handle

Customize the slider handle appearance:

```html
<wa-image-comparer>
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">

  <div slot="handle">
    <wa-icon name="arrows-expand"></wa-icon>
  </div>
</wa-image-comparer>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `position` | number | `50` | No | Initial position of the divider (0-100) |

## Slots

| Slot | Description |
|------|-------------|
| `before` | The "before" image (shown on the left) |
| `after` | The "after" image (shown on the right) |
| `handle` | Custom content for the slider handle |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the slider position changes | `{ position: number }` |

### Event Examples

```javascript
const comparer = document.querySelector('wa-image-comparer');

// Listen for position changes
comparer.addEventListener('wa-change', (event) => {
  console.log('Slider position:', event.detail.position);
});
```

## Examples

### Before/After Photo Editing

```html
<wa-image-comparer>
  <img
    slot="before"
    src="/images/photo-original.jpg"
    alt="Original photo">
  <img
    slot="after"
    src="/images/photo-edited.jpg"
    alt="Edited photo">
</wa-image-comparer>

<div style="text-align: center; margin-top: 1rem;">
  <strong>Drag the slider to compare</strong>
</div>
```

### Design Mockup Comparison

```html
<wa-image-comparer position="30">
  <img
    slot="before"
    src="/images/mockup-v1.jpg"
    alt="Design Version 1">
  <img
    slot="after"
    src="/images/mockup-v2.jpg"
    alt="Design Version 2">

  <div slot="handle" style="
    background: white;
    padding: 0.5rem;
    border-radius: 50%;
    box-shadow: 0 2px 8px rgba(0,0,0,0.2);
  ">
    <wa-icon name="arrows-left-right"></wa-icon>
  </div>
</wa-image-comparer>

<div style="display: flex; justify-content: space-between; margin-top: 0.5rem;">
  <span>Version 1</span>
  <span>Version 2</span>
</div>
```

### Image Filter Comparison

```html
<wa-image-comparer>
  <img
    slot="before"
    src="/images/photo.jpg"
    alt="Without filter">
  <img
    slot="after"
    src="/images/photo.jpg"
    alt="With filter"
    style="filter: grayscale(100%);">
</wa-image-comparer>

<style>
  wa-image-comparer {
    max-width: 600px;
    margin: 0 auto;
  }
</style>
```

### Responsive Image Comparison

```html
<wa-image-comparer
  id="responsiveComparer"
  style="width: 100%; max-width: 800px;">
  <img
    slot="before"
    src="/images/before.jpg"
    alt="Before"
    style="width: 100%; height: auto;">
  <img
    slot="after"
    src="/images/after.jpg"
    alt="After"
    style="width: 100%; height: auto;">
</wa-image-comparer>
```

### Color Correction Comparison

```html
<div class="comparison-container">
  <h3>Color Correction Results</h3>

  <wa-image-comparer>
    <img
      slot="before"
      src="/images/uncorrected.jpg"
      alt="Before color correction">
    <img
      slot="after"
      src="/images/corrected.jpg"
      alt="After color correction">
  </wa-image-comparer>

  <div class="comparison-labels">
    <wa-badge variant="neutral">Before</wa-badge>
    <wa-badge variant="primary">After</wa-badge>
  </div>
</div>

<style>
  .comparison-container {
    max-width: 700px;
    margin: 2rem auto;
  }

  .comparison-labels {
    display: flex;
    justify-content: space-between;
    margin-top: 1rem;
  }
</style>
```

### Interactive Gallery

```html
<div class="comparer-gallery">
  <wa-button-group style="margin-bottom: 1rem;">
    <wa-button data-before="/images/edit1-before.jpg" data-after="/images/edit1-after.jpg">
      Edit 1
    </wa-button>
    <wa-button data-before="/images/edit2-before.jpg" data-after="/images/edit2-after.jpg">
      Edit 2
    </wa-button>
    <wa-button data-before="/images/edit3-before.jpg" data-after="/images/edit3-after.jpg">
      Edit 3
    </wa-button>
  </wa-button-group>

  <wa-image-comparer id="galleryComparer">
    <img
      id="beforeImage"
      slot="before"
      src="/images/edit1-before.jpg"
      alt="Before">
    <img
      id="afterImage"
      slot="after"
      src="/images/edit1-after.jpg"
      alt="After">
  </wa-image-comparer>
</div>

<script>
  const buttons = document.querySelectorAll('.comparer-gallery wa-button');
  const beforeImage = document.getElementById('beforeImage');
  const afterImage = document.getElementById('afterImage');

  buttons.forEach(button => {
    button.addEventListener('click', () => {
      beforeImage.src = button.dataset.before;
      afterImage.src = button.dataset.after;
    });
  });
</script>
```

### Position Indicator

```html
<wa-image-comparer id="positionComparer">
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>

<div style="text-align: center; margin-top: 0.5rem;">
  <wa-badge id="positionBadge">50%</wa-badge>
</div>

<script>
  const comparer = document.getElementById('positionComparer');
  const badge = document.getElementById('positionBadge');

  comparer.addEventListener('wa-change', (event) => {
    badge.textContent = `${Math.round(event.detail.position)}%`;
  });
</script>
```

## CSS Parts

Use CSS parts to style internal elements:

```css
/* Style the container */
wa-image-comparer::part(container) {
  border: 2px solid #e5e7eb;
  border-radius: 8px;
}

/* Style the divider line */
wa-image-comparer::part(divider) {
  background-color: #6366f1;
  width: 3px;
}

/* Style the handle */
wa-image-comparer::part(handle) {
  background-color: #6366f1;
  width: 48px;
  height: 48px;
  border-radius: 50%;
}
```

## Customization

### Custom Sizing

```html
<!-- Fixed dimensions -->
<wa-image-comparer style="width: 800px; height: 600px;">
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>

<!-- Responsive with aspect ratio -->
<wa-image-comparer style="width: 100%; aspect-ratio: 16/9;">
  <img slot="before" src="/images/before.jpg" alt="Before">
  <img slot="after" src="/images/after.jpg" alt="After">
</wa-image-comparer>
```

### Styled Handle

```css
/* Custom handle styling */
wa-image-comparer::part(handle) {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  border: 3px solid white;
}

/* Custom divider */
wa-image-comparer::part(divider) {
  background: linear-gradient(to bottom, #667eea, #764ba2);
  width: 4px;
}
```

## Best Practices

- ✅ Use images with the same dimensions for best results
- ✅ Provide clear labels for "before" and "after"
- ✅ Use descriptive alt text for both images
- ✅ Optimize image file sizes for faster loading
- ✅ Consider using lazy loading for multiple comparers
- ✅ Make the slider handle visually prominent
- ❌ Don't compare images with drastically different aspect ratios
- ❌ Avoid using very large images that slow down performance
- ❌ Don't rely on color alone to distinguish before/after

## Accessibility

- Always provide descriptive `alt` text for both images
- Ensure the slider handle is keyboard accessible
- Use arrow keys to control the slider position:

```javascript
const comparer = document.querySelector('wa-image-comparer');

comparer.addEventListener('keydown', (event) => {
  if (event.key === 'ArrowLeft') {
    comparer.position = Math.max(0, comparer.position - 5);
  } else if (event.key === 'ArrowRight') {
    comparer.position = Math.min(100, comparer.position + 5);
  }
});
```

- Provide text labels to indicate which image is before/after
- Ensure sufficient color contrast for the handle and divider

## Troubleshooting

### Images Don't Align

**Problem:** Before and after images don't line up properly

**Solution:** Ensure both images have the same dimensions

```html
<!-- ✅ Correct - same dimensions -->
<wa-image-comparer>
  <img slot="before" src="/images/before.jpg" alt="Before" width="800" height="600">
  <img slot="after" src="/images/after.jpg" alt="After" width="800" height="600">
</wa-image-comparer>
```

### Slider Not Moving

**Problem:** The slider handle doesn't respond to dragging

**Solution:** Ensure the component is fully loaded and not overlapped by other elements

```javascript
// Wait for component to be ready
customElements.whenDefined('wa-image-comparer').then(() => {
  const comparer = document.querySelector('wa-image-comparer');
  // Component is ready
});
```

### Images Loading Slowly

**Problem:** Large images cause slow initial render

**Solution:** Optimize image sizes and use lazy loading

```html
<wa-image-comparer>
  <img
    slot="before"
    src="/images/before.jpg"
    alt="Before"
    loading="lazy">
  <img
    slot="after"
    src="/images/after.jpg"
    alt="After"
    loading="lazy">
</wa-image-comparer>
```

## Related

- [Image](./image.md)
- [Animated Image](./animated-image.md)
- [Carousel](./carousel.md)
- [Card](./card.md)
