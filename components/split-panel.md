# Split Panel

Resizable split views for dividing interface areas with adjustable boundaries.

## Overview

The `<wa-split-panel>` component creates a resizable split view that divides content into two adjustable panels. It supports both horizontal and vertical orientations, with optional snapping behavior and constraints for minimum and maximum sizes.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/split-panel/split-panel.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Horizontal split (default) -->
<wa-split-panel>
  <div slot="start">
    Left panel content
  </div>
  <div slot="end">
    Right panel content
  </div>
</wa-split-panel>

<!-- Vertical split -->
<wa-split-panel vertical>
  <div slot="start">
    Top panel content
  </div>
  <div slot="end">
    Bottom panel content
  </div>
</wa-split-panel>
```

## Orientation

### Horizontal Split

The default orientation divides content left and right:

```html
<wa-split-panel>
  <div slot="start">
    <h3>Sidebar</h3>
    <p>Navigation or sidebar content</p>
  </div>
  <div slot="end">
    <h3>Main Content</h3>
    <p>Primary content area</p>
  </div>
</wa-split-panel>
```

### Vertical Split

Use the `vertical` attribute to divide content top and bottom:

```html
<wa-split-panel vertical>
  <div slot="start">
    <h3>Header/Preview</h3>
    <p>Top section content</p>
  </div>
  <div slot="end">
    <h3>Details</h3>
    <p>Bottom section content</p>
  </div>
</wa-split-panel>
```

## Position

Control the initial divider position with the `position` attribute (in pixels or percentage):

```html
<!-- Start panel at 200px wide -->
<wa-split-panel position="200">
  <div slot="start">200px wide</div>
  <div slot="end">Remaining space</div>
</wa-split-panel>

<!-- Start panel at 30% of container -->
<wa-split-panel position="30%">
  <div slot="start">30% width</div>
  <div slot="end">70% width</div>
</wa-split-panel>
```

## Snapping

Enable snap-to-position behavior with the `snap` and `snap-threshold` attributes:

```html
<!-- Snap to edges within 50px -->
<wa-split-panel snap="0% 100%" snap-threshold="50">
  <div slot="start">
    Drag the divider near the edges to snap
  </div>
  <div slot="end">
    Content panel
  </div>
</wa-split-panel>

<!-- Snap to multiple positions -->
<wa-split-panel snap="0% 25% 50% 75% 100%" snap-threshold="30">
  <div slot="start">
    Snaps to quartiles
  </div>
  <div slot="end">
    Content panel
  </div>
</wa-split-panel>
```

## Disabled

Prevent resizing with the `disabled` attribute:

```html
<wa-split-panel position="300" disabled>
  <div slot="start">
    Fixed 300px panel
  </div>
  <div slot="end">
    Cannot resize
  </div>
</wa-split-panel>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `position` | number \| string | `50` | No | Initial position of the divider (px or percentage) |
| `vertical` | boolean | `false` | No | Render as vertical split (top/bottom) instead of horizontal (left/right) |
| `disabled` | boolean | `false` | No | Disable resizing |
| `snap` | string | - | No | Space-separated list of snap positions (e.g., "0% 50% 100%") |
| `snap-threshold` | number | `12` | No | Distance in pixels within which snapping occurs |

## Examples

### File Explorer Layout

```html
<wa-split-panel position="250">
  <div slot="start" style="padding: 1rem; background: #f5f5f5;">
    <h3>Files</h3>
    <wa-tree>
      <wa-tree-item>
        Documents
        <wa-tree-item>Project.docx</wa-tree-item>
        <wa-tree-item>Notes.txt</wa-tree-item>
      </wa-tree-item>
      <wa-tree-item>
        Images
        <wa-tree-item>Photo.jpg</wa-tree-item>
      </wa-tree-item>
    </wa-tree>
  </div>
  <div slot="end" style="padding: 1rem;">
    <h3>Preview</h3>
    <p>Select a file to preview its contents here.</p>
  </div>
</wa-split-panel>
```

### Code Editor with Console

```html
<wa-split-panel vertical position="60%" style="height: 500px;">
  <div slot="start" style="padding: 1rem; background: #1e1e1e; color: white;">
    <h4>Code Editor</h4>
    <pre><code>function hello() {
  console.log('Hello, World!');
}</code></pre>
  </div>
  <div slot="end" style="padding: 1rem; background: #252526; color: white;">
    <h4>Console</h4>
    <pre>Hello, World!</pre>
  </div>
</wa-split-panel>
```

### Nested Split Panels

```html
<wa-split-panel position="200" style="height: 400px;">
  <!-- Left sidebar -->
  <div slot="start" style="padding: 1rem; background: #f0f0f0;">
    <h4>Sidebar</h4>
    <ul>
      <li>Navigation Item 1</li>
      <li>Navigation Item 2</li>
      <li>Navigation Item 3</li>
    </ul>
  </div>

  <!-- Right side with nested vertical split -->
  <wa-split-panel slot="end" vertical position="50%">
    <div slot="start" style="padding: 1rem;">
      <h4>Top Panel</h4>
      <p>Main content area</p>
    </div>
    <div slot="end" style="padding: 1rem; background: #fafafa;">
      <h4>Bottom Panel</h4>
      <p>Additional details or tools</p>
    </div>
  </wa-split-panel>
</wa-split-panel>
```

### Dashboard with Collapsible Sidebar

```html
<wa-split-panel
  id="dashboardSplit"
  position="300"
  snap="0 300"
  snap-threshold="50"
  style="height: 600px;">
  <div slot="start" style="padding: 1rem; background: #2c3e50; color: white;">
    <h3>Dashboard Menu</h3>
    <nav>
      <ul>
        <li><a href="#overview">Overview</a></li>
        <li><a href="#analytics">Analytics</a></li>
        <li><a href="#reports">Reports</a></li>
        <li><a href="#settings">Settings</a></li>
      </ul>
    </nav>
  </div>
  <div slot="end" style="padding: 1rem;">
    <div style="margin-bottom: 1rem;">
      <wa-button id="toggleSidebar">Toggle Sidebar</wa-button>
    </div>
    <h2>Main Dashboard</h2>
    <p>Content area with charts and data visualizations</p>
  </div>
</wa-split-panel>

<script>
  const splitPanel = document.getElementById('dashboardSplit');
  const toggleBtn = document.getElementById('toggleSidebar');

  toggleBtn.addEventListener('click', () => {
    // Toggle between collapsed (0) and expanded (300px)
    splitPanel.position = splitPanel.position === 0 ? 300 : 0;
  });
</script>
```

### Responsive Split with Min/Max Constraints

```html
<wa-split-panel
  position="400"
  style="height: 400px; --min: 200px; --max: 600px;">
  <div slot="start" style="padding: 1rem; background: #ecf0f1;">
    <h4>Constrained Panel</h4>
    <p>This panel has min width of 200px and max width of 600px</p>
  </div>
  <div slot="end" style="padding: 1rem;">
    <h4>Content Area</h4>
    <p>Adjusts to fill remaining space</p>
  </div>
</wa-split-panel>

<style>
  wa-split-panel::part(divider) {
    background-color: #3498db;
  }
</style>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `getPosition()` | Gets the current position of the divider | `number` |

### Method Examples

```javascript
const splitPanel = document.querySelector('wa-split-panel');

// Get current divider position
const currentPos = splitPanel.getPosition();
console.log('Current position:', currentPos);

// Set new position programmatically
splitPanel.position = 350;

// Animate position change
function animateSplit(targetPosition, duration = 300) {
  const startPosition = splitPanel.getPosition();
  const distance = targetPosition - startPosition;
  const startTime = performance.now();

  function update(currentTime) {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / duration, 1);

    splitPanel.position = startPosition + (distance * progress);

    if (progress < 1) {
      requestAnimationFrame(update);
    }
  }

  requestAnimationFrame(update);
}

// Usage
animateSplit(500);
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-reposition` | Emitted when the divider position changes | `{ position: number }` |

### Event Examples

```javascript
const splitPanel = document.querySelector('wa-split-panel');

// Listen for position changes
splitPanel.addEventListener('wa-reposition', (event) => {
  console.log('New position:', event.detail.position);

  // Update UI or save preference
  localStorage.setItem('splitPosition', event.detail.position);
});

// Restore saved position on load
window.addEventListener('load', () => {
  const savedPosition = localStorage.getItem('splitPosition');
  if (savedPosition) {
    splitPanel.position = parseInt(savedPosition);
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| `start` | Content for the first panel (left or top) |
| `end` | Content for the second panel (right or bottom) |
| `divider` | Custom divider content (optional) |

### Custom Divider

```html
<wa-split-panel>
  <div slot="start">Left panel</div>

  <div slot="divider" style="display: flex; align-items: center; justify-content: center;">
    <wa-icon name="grip-vertical"></wa-icon>
  </div>

  <div slot="end">Right panel</div>
</wa-split-panel>
```

## CSS Parts

Use CSS parts to style internal split panel elements:

```css
/* Style the container */
wa-split-panel::part(panel) {
  border: 1px solid #ddd;
}

/* Style the divider */
wa-split-panel::part(divider) {
  background-color: #3498db;
  width: 4px;
}

/* Style the start panel */
wa-split-panel::part(start) {
  background-color: #f8f9fa;
}

/* Style the end panel */
wa-split-panel::part(end) {
  background-color: #ffffff;
}
```

## Customization

### Custom Divider Styles

```css
/* Thicker divider with hover effect */
wa-split-panel::part(divider) {
  background-color: #e0e0e0;
  width: 8px;
  transition: background-color 0.2s;
}

wa-split-panel::part(divider):hover {
  background-color: #3498db;
}

/* Divider with border */
wa-split-panel[vertical]::part(divider) {
  border-top: 2px solid #ccc;
  border-bottom: 2px solid #ccc;
}
```

### CSS Custom Properties

```css
/* Set minimum and maximum panel sizes */
wa-split-panel {
  --min: 150px;
  --max: 800px;
}

/* Divider size */
wa-split-panel {
  --divider-width: 6px;
}
```

## Best Practices

- ✅ Set a specific height on horizontal split panels
- ✅ Use snap positions for common layouts (collapsed/expanded states)
- ✅ Save user's preferred position to localStorage
- ✅ Provide visual feedback on the divider for draggability
- ✅ Set reasonable min/max constraints to prevent awkward layouts
- ❌ Don't nest too many split panels (max 2-3 levels)
- ❌ Avoid very small minimum sizes that make content unusable
- ❌ Don't forget to set container height for split panels to work properly

## Accessibility

- The divider is keyboard accessible with arrow key navigation
- Divider has appropriate ARIA role and labels
- Screen readers announce position changes
- Respects `prefers-reduced-motion` for animations

```html
<!-- Provide accessible labels -->
<wa-split-panel aria-label="Main content splitter">
  <div slot="start" role="navigation" aria-label="Sidebar navigation">
    Navigation content
  </div>
  <div slot="end" role="main" aria-label="Main content">
    Main content
  </div>
</wa-split-panel>
```

## Troubleshooting

### Split Panel Not Visible

**Problem:** Split panel doesn't show or has zero height

**Solution:** Ensure the parent container has a defined height

```html
<!-- ❌ Won't work without height -->
<wa-split-panel>
  <div slot="start">Content</div>
  <div slot="end">Content</div>
</wa-split-panel>

<!-- ✅ Set explicit height -->
<wa-split-panel style="height: 500px;">
  <div slot="start">Content</div>
  <div slot="end">Content</div>
</wa-split-panel>
```

### Divider Not Draggable

**Problem:** Cannot resize panels by dragging

**Solution:** Check if the component is disabled

```javascript
// Enable resizing
splitPanel.disabled = false;
```

### Content Overflow Issues

**Problem:** Content overflows panel boundaries

**Solution:** Add overflow handling to slot content

```css
wa-split-panel [slot="start"],
wa-split-panel [slot="end"] {
  overflow: auto;
  height: 100%;
}
```

## Related

- [Resize Observer](./resize-observer.md)
- [Drawer](./drawer.md)
- [Card](./card.md)
- [Layout Guide](../guides/layout.md)
