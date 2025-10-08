# Slider

Sliders allow users to select a numeric value from a specified range using an intuitive dragging interface.

## Overview

The `<wa-slider>` component provides a customizable range input control that allows users to select numeric values by dragging a thumb along a track. It supports single values, custom steps, labels, and disabled states.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/slider/slider.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default slider (0-100) -->
<wa-slider></wa-slider>

<!-- Slider with initial value -->
<wa-slider value="50"></wa-slider>

<!-- Slider with label -->
<wa-slider label="Volume"></wa-slider>

<!-- Disabled slider -->
<wa-slider value="30" disabled></wa-slider>
```

## Range Configuration

Set the minimum, maximum, and step values:

```html
<!-- Custom range (0-10) -->
<wa-slider min="0" max="10" value="5"></wa-slider>

<!-- Price range ($0-$1000) -->
<wa-slider min="0" max="1000" value="500" label="Price"></wa-slider>

<!-- Custom step increment -->
<wa-slider min="0" max="100" step="5" value="25"></wa-slider>

<!-- Decimal values -->
<wa-slider min="0" max="1" step="0.1" value="0.5"></wa-slider>
```

## Labels and Help Text

Provide context for the slider:

```html
<!-- With label -->
<wa-slider label="Brightness" value="75"></wa-slider>

<!-- With help text -->
<wa-slider label="Volume" help-text="Adjust the audio volume level"></wa-slider>

<!-- Display current value -->
<wa-slider id="volumeSlider" label="Volume" value="50"></wa-slider>
<div id="valueDisplay">Volume: 50%</div>

<script>
  const slider = document.getElementById('volumeSlider');
  const display = document.getElementById('valueDisplay');

  slider.addEventListener('wa-input', (e) => {
    display.textContent = `Volume: ${e.target.value}%`;
  });
</script>
```

## States

### Disabled State

```html
<wa-slider label="Volume" value="60" disabled></wa-slider>
```

### Required State

```html
<wa-slider label="Priority Level" required></wa-slider>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `min` | number | `0` | No | Minimum value of the slider |
| `max` | number | `100` | No | Maximum value of the slider |
| `step` | number | `1` | No | The interval between selectable values |
| `value` | number | `0` | No | The current value of the slider |
| `label` | string | - | No | Label text for the slider |
| `help-text` | string | - | No | Help text displayed below the slider |
| `disabled` | boolean | `false` | No | Disables the slider |
| `required` | boolean | `false` | No | Makes the slider required in forms |
| `name` | string | - | No | Name attribute for form submission |

## Examples

### Volume Control

```html
<wa-slider id="volumeControl" label="Volume" min="0" max="100" value="75"></wa-slider>
<wa-icon id="volumeIcon" name="volume-high"></wa-icon>

<script>
  const slider = document.getElementById('volumeControl');
  const icon = document.getElementById('volumeIcon');

  slider.addEventListener('wa-change', (e) => {
    const value = e.target.value;

    if (value === 0) {
      icon.name = 'volume-mute';
    } else if (value < 50) {
      icon.name = 'volume-low';
    } else {
      icon.name = 'volume-high';
    }
  });
</script>
```

### Price Range Filter

```html
<wa-slider
  id="priceRange"
  label="Maximum Price"
  min="0"
  max="1000"
  step="10"
  value="500">
</wa-slider>

<div id="priceDisplay">$0 - $500</div>

<script>
  const slider = document.getElementById('priceRange');
  const display = document.getElementById('priceDisplay');

  slider.addEventListener('wa-input', (e) => {
    const value = e.target.value;
    display.textContent = `$0 - $${value}`;
  });
</script>
```

### Color Picker RGB Values

```html
<div class="color-picker">
  <wa-slider id="redSlider" label="Red" min="0" max="255" value="255"></wa-slider>
  <wa-slider id="greenSlider" label="Green" min="0" max="255" value="0"></wa-slider>
  <wa-slider id="blueSlider" label="Blue" min="0" max="255" value="0"></wa-slider>

  <div id="colorPreview" style="width: 100px; height: 100px; margin-top: 1rem;"></div>
</div>

<script>
  const redSlider = document.getElementById('redSlider');
  const greenSlider = document.getElementById('greenSlider');
  const blueSlider = document.getElementById('blueSlider');
  const preview = document.getElementById('colorPreview');

  function updateColor() {
    const r = redSlider.value;
    const g = greenSlider.value;
    const b = blueSlider.value;
    preview.style.backgroundColor = `rgb(${r}, ${g}, ${b})`;
  }

  redSlider.addEventListener('wa-input', updateColor);
  greenSlider.addEventListener('wa-input', updateColor);
  blueSlider.addEventListener('wa-input', updateColor);

  // Initialize color
  updateColor();
</script>
```

### Temperature Control

```html
<wa-slider
  id="tempSlider"
  label="Temperature"
  min="60"
  max="85"
  step="0.5"
  value="72">
</wa-slider>

<div id="tempDisplay">72°F</div>

<script>
  const slider = document.getElementById('tempSlider');
  const display = document.getElementById('tempDisplay');

  slider.addEventListener('wa-input', (e) => {
    display.textContent = `${e.target.value}°F`;
  });

  slider.addEventListener('wa-change', (e) => {
    // Save temperature setting
    console.log('Temperature set to:', e.target.value);
  });
</script>
```

### Zoom Level Control

```html
<wa-button-group>
  <wa-button id="zoomOut">
    <wa-icon name="zoom-out"></wa-icon>
  </wa-button>
  <wa-slider
    id="zoomSlider"
    min="25"
    max="200"
    step="25"
    value="100"
    style="width: 200px;">
  </wa-slider>
  <wa-button id="zoomIn">
    <wa-icon name="zoom-in"></wa-icon>
  </wa-button>
</wa-button-group>

<div id="zoomDisplay">100%</div>

<script>
  const slider = document.getElementById('zoomSlider');
  const display = document.getElementById('zoomDisplay');
  const zoomIn = document.getElementById('zoomIn');
  const zoomOut = document.getElementById('zoomOut');

  slider.addEventListener('wa-input', (e) => {
    display.textContent = `${e.target.value}%`;
  });

  zoomIn.addEventListener('click', () => {
    slider.value = Math.min(slider.max, slider.value + 25);
    slider.dispatchEvent(new Event('wa-input'));
  });

  zoomOut.addEventListener('click', () => {
    slider.value = Math.max(slider.min, slider.value - 25);
    slider.dispatchEvent(new Event('wa-input'));
  });
</script>
```

### Form Integration

```html
<form id="settingsForm">
  <wa-slider
    name="brightness"
    label="Brightness"
    min="0"
    max="100"
    value="80">
  </wa-slider>

  <wa-slider
    name="contrast"
    label="Contrast"
    min="0"
    max="100"
    value="50">
  </wa-slider>

  <wa-slider
    name="saturation"
    label="Saturation"
    min="0"
    max="100"
    value="60">
  </wa-slider>

  <wa-button type="submit" variant="primary">Apply Settings</wa-button>
</form>

<script>
  const form = document.getElementById('settingsForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const formData = new FormData(form);
    const settings = {
      brightness: formData.get('brightness'),
      contrast: formData.get('contrast'),
      saturation: formData.get('saturation')
    };

    console.log('Settings:', settings);
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the slider | `void` |
| `blur()` | Removes focus from the slider | `void` |
| `stepUp()` | Increases the value by one step | `void` |
| `stepDown()` | Decreases the value by one step | `void` |

### Method Examples

```javascript
const slider = document.querySelector('wa-slider');

// Focus the slider
slider.focus();

// Increase value by one step
slider.stepUp();

// Decrease value by one step
slider.stepDown();

// Remove focus
slider.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the slider value changes and the user stops dragging | `{ value: number }` |
| `wa-input` | Emitted continuously as the slider value changes during dragging | `{ value: number }` |
| `wa-focus` | Emitted when the slider gains focus | - |
| `wa-blur` | Emitted when the slider loses focus | - |

### Event Examples

```javascript
const slider = document.querySelector('wa-slider');

// Fired continuously while dragging
slider.addEventListener('wa-input', (e) => {
  console.log('Current value:', e.target.value);
  // Update UI in real-time
});

// Fired when user releases the slider
slider.addEventListener('wa-change', (e) => {
  console.log('Final value:', e.target.value);
  // Save or submit the value
});

// Focus and blur events
slider.addEventListener('wa-focus', () => {
  console.log('Slider focused');
});

slider.addEventListener('wa-blur', () => {
  console.log('Slider blurred');
});
```

## Slots

| Slot | Description |
|------|-------------|
| `label` | Custom label content |
| `help-text` | Custom help text content |

## CSS Parts

Use CSS parts to style internal slider elements:

```css
/* Style the base container */
wa-slider::part(base) {
  padding: 1rem;
}

/* Style the label */
wa-slider::part(label) {
  font-weight: bold;
  color: #333;
}

/* Style the slider track */
wa-slider::part(track) {
  background-color: #e2e8f0;
  height: 6px;
}

/* Style the filled portion of the track */
wa-slider::part(track-active) {
  background-color: #3b82f6;
}

/* Style the slider thumb */
wa-slider::part(thumb) {
  width: 20px;
  height: 20px;
  background-color: #3b82f6;
  border: 2px solid white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

/* Style the help text */
wa-slider::part(help-text) {
  color: #64748b;
  font-size: 0.875rem;
}
```

## Customization

### Custom Track Colors

```css
/* Custom color scheme */
wa-slider::part(track) {
  background-color: #f1f5f9;
}

wa-slider::part(track-active) {
  background: linear-gradient(to right, #8b5cf6, #ec4899);
}

wa-slider::part(thumb) {
  background-color: #ec4899;
  border-color: white;
}
```

### Custom Thumb Size

```css
/* Larger thumb for touch interfaces */
wa-slider.touch::part(thumb) {
  width: 32px;
  height: 32px;
}

wa-slider.touch::part(track) {
  height: 8px;
}
```

### Vertical Slider

```html
<wa-slider
  class="vertical-slider"
  label="Volume"
  value="70">
</wa-slider>

<style>
  .vertical-slider {
    height: 200px;
    writing-mode: bt-lr;
    -webkit-appearance: slider-vertical;
  }
</style>
```

## Best Practices

- Use `wa-input` for real-time updates (e.g., live previews)
- Use `wa-change` for actions that should occur after user interaction completes
- Provide clear labels that describe what the slider controls
- Display the current value when the numeric value is important
- Use appropriate `min`, `max`, and `step` values for the context
- Consider adding buttons for precise adjustments alongside sliders
- Show visual feedback (e.g., color changes, icons) based on slider values
- Don't use sliders for values that require precise input - use number inputs instead

## Accessibility

- Sliders automatically include appropriate ARIA roles and attributes
- Use the `label` attribute to provide accessible labels
- Sliders are keyboard accessible:
  - Arrow keys: Adjust value by one step
  - Page Up/Down: Adjust value by larger increments
  - Home: Set to minimum value
  - End: Set to maximum value
- The current value is announced to screen readers
- Use `help-text` to provide additional context for assistive technologies

## Troubleshooting

### Slider Value Not Updating

**Problem:** Value doesn't change when dragging

**Solution:** Ensure the slider isn't disabled and check for JavaScript errors

```javascript
slider.disabled = false;
```

### Step Values Not Working

**Problem:** Slider doesn't snap to expected values

**Solution:** Verify that your step value divides evenly into the range

```html
<!-- Will work correctly -->
<wa-slider min="0" max="100" step="5"></wa-slider>

<!-- May have unexpected behavior -->
<wa-slider min="0" max="100" step="7"></wa-slider>
```

### Events Not Firing

**Problem:** `wa-change` or `wa-input` events not triggered

**Solution:** Use the correct WebAwesome event names, not standard HTML events

```javascript
// Correct
slider.addEventListener('wa-input', handler);

// Won't work
slider.addEventListener('input', handler);
```

## Related

- [Range](./range.md)
- [Input](./input.md)
- [Color Picker](./color-picker.md)
- [Form Controls Guide](../guides/form-controls.md)
