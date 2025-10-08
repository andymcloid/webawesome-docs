# Progress Ring

A circular progress indicator for displaying task completion or loading states.

## Overview

The `<wa-progress-ring>` component displays progress as a circular ring, making it ideal for dashboard widgets, loading indicators, skill levels, and statistics. It provides a visually appealing alternative to traditional linear progress bars.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/progress-ring/progress-ring.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic progress ring (50% complete) -->
<wa-progress-ring value="50"></wa-progress-ring>

<!-- Different completion values -->
<wa-progress-ring value="0"></wa-progress-ring>
<wa-progress-ring value="25"></wa-progress-ring>
<wa-progress-ring value="75"></wa-progress-ring>
<wa-progress-ring value="100"></wa-progress-ring>
```

## Sizes

Control the ring size with the `size` attribute:

```html
<!-- Small ring -->
<wa-progress-ring value="60" size="64"></wa-progress-ring>

<!-- Medium ring (default) -->
<wa-progress-ring value="60" size="128"></wa-progress-ring>

<!-- Large ring -->
<wa-progress-ring value="60" size="256"></wa-progress-ring>

<!-- Custom size -->
<wa-progress-ring value="60" size="180"></wa-progress-ring>
```

## Stroke Width

Customize the thickness of the ring:

```html
<!-- Thin stroke -->
<wa-progress-ring value="60" stroke-width="2"></wa-progress-ring>

<!-- Default stroke -->
<wa-progress-ring value="60" stroke-width="4"></wa-progress-ring>

<!-- Thick stroke -->
<wa-progress-ring value="60" stroke-width="8"></wa-progress-ring>

<!-- Very thick stroke -->
<wa-progress-ring value="60" stroke-width="16"></wa-progress-ring>
```

## Labels

Add text inside the progress ring:

```html
<!-- Percentage label -->
<wa-progress-ring value="60" label="60%"></wa-progress-ring>

<!-- Custom label -->
<wa-progress-ring value="75" label="3/4"></wa-progress-ring>

<!-- Text label -->
<wa-progress-ring value="100" label="Done"></wa-progress-ring>

<!-- Dynamic label with value -->
<wa-progress-ring value="45" label="45 of 100"></wa-progress-ring>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | number | `0` | No | Progress value (0-100) |
| `size` | number | `128` | No | Diameter of the ring in pixels |
| `stroke-width` | number | `4` | No | Width of the ring stroke |
| `label` | string | `''` | No | Text label displayed inside the ring |

### Properties

```javascript
const ring = document.querySelector('wa-progress-ring');

// Get current value
console.log(ring.value); // 50

// Set progress value
ring.value = 75;

// Update label
ring.label = '75%';

// Change size
ring.size = 200;

// Adjust stroke width
ring.strokeWidth = 6;
```

## Examples

### Loading Indicator

```html
<div style="text-align: center;">
  <wa-progress-ring id="loadingRing" value="0" size="128" label="0%"></wa-progress-ring>
  <p>Loading data...</p>
</div>

<script>
  const ring = document.getElementById('loadingRing');
  let progress = 0;

  const interval = setInterval(() => {
    progress += 10;
    ring.value = progress;
    ring.label = `${progress}%`;

    if (progress >= 100) {
      clearInterval(interval);
      ring.label = 'Complete!';
    }
  }, 500);
</script>
```

### Skill Level Display

```html
<div style="display: flex; gap: 2rem; flex-wrap: wrap;">
  <div style="text-align: center;">
    <wa-progress-ring value="90" size="100" stroke-width="6" label="90%"></wa-progress-ring>
    <p><strong>JavaScript</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="75" size="100" stroke-width="6" label="75%"></wa-progress-ring>
    <p><strong>React</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="85" size="100" stroke-width="6" label="85%"></wa-progress-ring>
    <p><strong>CSS</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="60" size="100" stroke-width="6" label="60%"></wa-progress-ring>
    <p><strong>Node.js</strong></p>
  </div>
</div>
```

### File Upload Progress

```html
<wa-card style="max-width: 400px;">
  <div slot="header">
    <strong>Uploading Files</strong>
  </div>

  <div style="display: flex; align-items: center; gap: 1rem;">
    <wa-progress-ring id="uploadRing" value="0" size="80" label="0%"></wa-progress-ring>
    <div style="flex: 1;">
      <p style="margin: 0;"><strong id="fileName">document.pdf</strong></p>
      <p style="margin: 0; font-size: 0.875rem; color: #64748b;" id="fileStatus">
        Uploading...
      </p>
    </div>
  </div>
</wa-card>

<script>
  const uploadRing = document.getElementById('uploadRing');
  const fileStatus = document.getElementById('fileStatus');

  // Simulate upload
  let uploaded = 0;
  const total = 1024; // KB

  const uploadInterval = setInterval(() => {
    uploaded += 102.4; // 10% per tick
    const percent = Math.min(Math.round((uploaded / total) * 100), 100);

    uploadRing.value = percent;
    uploadRing.label = `${percent}%`;
    fileStatus.textContent = `${Math.round(uploaded)} KB / ${total} KB`;

    if (percent >= 100) {
      clearInterval(uploadInterval);
      fileStatus.textContent = 'Upload complete!';
    }
  }, 200);
</script>
```

### Statistics Dashboard

```html
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 2rem;">
  <div style="text-align: center;">
    <wa-progress-ring value="87" size="120" stroke-width="8" label="87%"></wa-progress-ring>
    <p style="margin-top: 1rem;"><strong>Customer Satisfaction</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="92" size="120" stroke-width="8" label="92%"></wa-progress-ring>
    <p style="margin-top: 1rem;"><strong>On-Time Delivery</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="78" size="120" stroke-width="8" label="78%"></wa-progress-ring>
    <p style="margin-top: 1rem;"><strong>Quality Score</strong></p>
  </div>

  <div style="text-align: center;">
    <wa-progress-ring value="95" size="120" stroke-width="8" label="95%"></wa-progress-ring>
    <p style="margin-top: 1rem;"><strong>Uptime</strong></p>
  </div>
</div>
```

### Task Completion

```html
<wa-card style="max-width: 300px;">
  <div style="text-align: center;">
    <wa-progress-ring id="taskRing" value="66" size="150" stroke-width="10" label="4/6"></wa-progress-ring>
    <h3 style="margin-top: 1.5rem;">Project Tasks</h3>
    <p style="color: #64748b;">4 of 6 tasks completed</p>
  </div>

  <wa-divider></wa-divider>

  <div style="display: flex; flex-direction: column; gap: 0.5rem;">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox checked disabled></wa-checkbox>
      <span>Design mockups</span>
    </div>
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox checked disabled></wa-checkbox>
      <span>API integration</span>
    </div>
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox checked disabled></wa-checkbox>
      <span>Database schema</span>
    </div>
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox checked disabled></wa-checkbox>
      <span>User authentication</span>
    </div>
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox></wa-checkbox>
      <span>Testing</span>
    </div>
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <wa-checkbox></wa-checkbox>
      <span>Deployment</span>
    </div>
  </div>
</wa-card>
```

### Animated Progress

```html
<wa-progress-ring id="animatedRing" value="0" size="150" label="Start"></wa-progress-ring>
<br>
<wa-button-group>
  <wa-button id="startBtn">Start</wa-button>
  <wa-button id="pauseBtn">Pause</wa-button>
  <wa-button id="resetBtn">Reset</wa-button>
</wa-button-group>

<script>
  const ring = document.getElementById('animatedRing');
  const startBtn = document.getElementById('startBtn');
  const pauseBtn = document.getElementById('pauseBtn');
  const resetBtn = document.getElementById('resetBtn');

  let animationInterval = null;
  let progress = 0;

  startBtn.addEventListener('click', () => {
    if (animationInterval) return; // Already running

    animationInterval = setInterval(() => {
      progress += 1;
      ring.value = progress;
      ring.label = `${progress}%`;

      if (progress >= 100) {
        clearInterval(animationInterval);
        animationInterval = null;
        ring.label = 'Done!';
      }
    }, 50);
  });

  pauseBtn.addEventListener('click', () => {
    if (animationInterval) {
      clearInterval(animationInterval);
      animationInterval = null;
    }
  });

  resetBtn.addEventListener('click', () => {
    if (animationInterval) {
      clearInterval(animationInterval);
      animationInterval = null;
    }
    progress = 0;
    ring.value = 0;
    ring.label = 'Start';
  });
</script>
```

### With Custom Content

```html
<wa-progress-ring value="68" size="180" stroke-width="12">
  <div style="text-align: center;">
    <div style="font-size: 2rem; font-weight: bold;">68%</div>
    <div style="font-size: 0.875rem; color: #64748b;">Battery</div>
    <wa-icon name="battery-charging" style="font-size: 1.5rem; margin-top: 0.5rem;"></wa-icon>
  </div>
</wa-progress-ring>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| N/A | This component has no public methods | - |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| N/A | This component emits no events | - |

## Slots

| Slot | Description |
|------|-------------|
| (default) | Custom content to display inside the ring (overrides `label`) |

### Slot Examples

```html
<!-- Custom HTML content -->
<wa-progress-ring value="75" size="150">
  <div style="text-align: center;">
    <strong style="font-size: 1.5rem;">75%</strong>
    <br>
    <span style="font-size: 0.875rem;">Complete</span>
  </div>
</wa-progress-ring>

<!-- With icon -->
<wa-progress-ring value="100" size="120">
  <wa-icon name="check-circle" style="font-size: 3rem; color: #16a34a;"></wa-icon>
</wa-progress-ring>

<!-- Complex content -->
<wa-progress-ring value="45" size="200" stroke-width="10">
  <div style="text-align: center;">
    <div style="font-size: 2.5rem; font-weight: bold;">45</div>
    <div style="font-size: 0.75rem; text-transform: uppercase; letter-spacing: 1px;">
      Days Left
    </div>
    <wa-badge variant="warning" style="margin-top: 0.5rem;">Expiring Soon</wa-badge>
  </div>
</wa-progress-ring>
```

## CSS Parts

Use CSS parts to style internal progress ring elements:

```css
/* Style the base SVG */
wa-progress-ring::part(base) {
  /* SVG container styles */
}

/* Style the track (background circle) */
wa-progress-ring::part(track) {
  stroke: #e5e7eb;
  stroke-width: 4px;
}

/* Style the indicator (progress arc) */
wa-progress-ring::part(indicator) {
  stroke: #3b82f6;
  stroke-width: 4px;
}

/* Style the label */
wa-progress-ring::part(label) {
  font-size: 1rem;
  font-weight: 600;
  fill: #1e293b;
}
```

## Customization

### Custom Colors

```css
/* Success ring (green) */
wa-progress-ring.success::part(indicator) {
  stroke: #16a34a;
}

/* Warning ring (orange) */
wa-progress-ring.warning::part(indicator) {
  stroke: #f59e0b;
}

/* Danger ring (red) */
wa-progress-ring.danger::part(indicator) {
  stroke: #dc2626;
}

/* Custom gradient */
wa-progress-ring.gradient::part(indicator) {
  stroke: url(#gradient);
}
```

### Custom Track Color

```css
/* Light track */
wa-progress-ring.light::part(track) {
  stroke: #f3f4f6;
}

/* Dark track */
wa-progress-ring.dark::part(track) {
  stroke: #374151;
}

/* Transparent track */
wa-progress-ring.transparent::part(track) {
  stroke: transparent;
}
```

### Animated Ring

```css
/* Rotating animation */
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

wa-progress-ring.rotating::part(base) {
  animation: rotate 2s linear infinite;
}

/* Pulsing animation */
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

wa-progress-ring.pulsing::part(indicator) {
  animation: pulse 2s ease-in-out infinite;
}
```

### Rounded or Flat Ends

```css
/* Rounded ends (default) */
wa-progress-ring.rounded::part(indicator) {
  stroke-linecap: round;
}

/* Flat ends */
wa-progress-ring.flat::part(indicator) {
  stroke-linecap: butt;
}

/* Square ends */
wa-progress-ring.square::part(indicator) {
  stroke-linecap: square;
}
```

## Best Practices

- ✅ Use appropriate size for the context (larger for dashboards, smaller for inline)
- ✅ Provide clear labels for screen readers
- ✅ Use consistent colors for similar types of progress
- ✅ Consider animation for loading states
- ✅ Keep stroke width proportional to ring size
- ❌ Don't use extremely small rings (< 48px) with labels
- ❌ Avoid using too many progress rings on one screen
- ❌ Don't forget to update the label when value changes

## Accessibility

- Always provide a label or use the default slot for context
- The component automatically includes appropriate ARIA attributes
- Progress updates are announced to screen readers
- Consider adding additional text for important progress indicators

```html
<!-- Accessible progress ring -->
<div>
  <wa-progress-ring
    value="75"
    label="75%"
    role="progressbar"
    aria-valuenow="75"
    aria-valuemin="0"
    aria-valuemax="100"
    aria-label="Upload progress"
  ></wa-progress-ring>
  <p id="progress-description" class="sr-only">
    File upload is 75% complete
  </p>
</div>
```

## Troubleshooting

### Label Not Visible

**Problem:** Label text is not showing inside the ring

**Solution:** Ensure the ring is large enough to accommodate the label text

```html
<!-- ❌ Too small for label -->
<wa-progress-ring value="50" size="32" label="50%"></wa-progress-ring>

<!-- ✅ Appropriate size -->
<wa-progress-ring value="50" size="100" label="50%"></wa-progress-ring>
```

### Ring Appears Cut Off

**Problem:** Parts of the ring are not visible

**Solution:** Ensure parent container has enough space and doesn't have overflow: hidden

```css
/* Fix container */
.ring-container {
  display: inline-block;
  padding: 10px; /* Add padding for thick strokes */
}
```

### Value Not Updating

**Problem:** Setting value property doesn't update visually

**Solution:** Ensure you're setting a valid number between 0-100

```javascript
const ring = document.querySelector('wa-progress-ring');

// ✅ Correct
ring.value = 75;

// ❌ Wrong - out of range
ring.value = 150; // Will be clamped to 100

// ❌ Wrong - not a number
ring.value = '75'; // Should be: ring.value = 75
```

## Related

- [Progress Bar](./progress-bar.md)
- [Spinner](./spinner.md)
- [Badge](./badge.md)
- [Card](./card.md)
