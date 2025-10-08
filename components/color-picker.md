# Color Picker

Color pickers allow users to select colors using an intuitive visual interface with support for multiple color formats.

## Overview

The `<wa-color-picker>` component provides a fully-featured color selection interface with support for multiple color formats (hex, RGB, HSL, HSV), opacity control, predefined swatches, and both inline and dropdown display modes.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/color-picker/color-picker.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default color picker -->
<wa-color-picker></wa-color-picker>

<!-- With initial color -->
<wa-color-picker value="#3b82f6"></wa-color-picker>

<!-- With label -->
<wa-color-picker label="Theme Color"></wa-color-picker>

<!-- Disabled -->
<wa-color-picker value="#ec4899" disabled></wa-color-picker>
```

## Color Formats

The color picker supports multiple color format outputs:

```html
<!-- Hexadecimal (default) -->
<wa-color-picker format="hex" value="#3b82f6"></wa-color-picker>

<!-- RGB -->
<wa-color-picker format="rgb" value="rgb(59, 130, 246)"></wa-color-picker>

<!-- HSL -->
<wa-color-picker format="hsl" value="hsl(217, 91%, 60%)"></wa-color-picker>

<!-- HSV -->
<wa-color-picker format="hsv" value="hsv(217, 76%, 96%)"></wa-color-picker>
```

## Opacity Control

Enable opacity (alpha channel) selection:

```html
<!-- With opacity slider -->
<wa-color-picker opacity value="#3b82f6"></wa-color-picker>

<!-- RGB with alpha -->
<wa-color-picker format="rgb" opacity value="rgba(59, 130, 246, 0.5)"></wa-color-picker>

<!-- HEX with alpha -->
<wa-color-picker format="hex" opacity value="#3b82f680"></wa-color-picker>
```

## Swatches

Provide predefined color swatches for quick selection:

```html
<!-- With color swatches -->
<wa-color-picker
  swatches="
    #ef4444;
    #f59e0b;
    #10b981;
    #3b82f6;
    #8b5cf6;
    #ec4899;
    #000000;
    #ffffff
  ">
</wa-color-picker>

<!-- Brand color swatches -->
<wa-color-picker
  label="Brand Color"
  swatches="
    #1e40af;
    #3b82f6;
    #60a5fa;
    #93c5fd;
    #dbeafe
  ">
</wa-color-picker>
```

## Display Modes

### Dropdown Mode (Default)

The color picker appears in a dropdown when clicked:

```html
<wa-color-picker label="Select Color"></wa-color-picker>
```

### Inline Mode

Display the color picker interface inline:

```html
<wa-color-picker inline></wa-color-picker>

<!-- Inline with swatches -->
<wa-color-picker
  inline
  swatches="#ef4444; #f59e0b; #10b981; #3b82f6">
</wa-color-picker>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | `#ffffff` | No | The current color value in the specified format |
| `format` | string | `'hex'` | No | Color format: `hex`, `rgb`, `hsl`, `hsv` |
| `swatches` | string | - | No | Semicolon-separated list of preset colors |
| `opacity` | boolean | `false` | No | Enable opacity/alpha channel control |
| `inline` | boolean | `false` | No | Display picker inline instead of in dropdown |
| `disabled` | boolean | `false` | No | Disable the color picker |
| `label` | string | - | No | Label text for the color picker |
| `help-text` | string | - | No | Help text displayed below the picker |
| `name` | string | - | No | Name attribute for form submission |
| `required` | boolean | `false` | No | Makes the color picker required in forms |
| `size` | string | `'medium'` | No | Trigger button size: `small`, `medium`, `large` |

## Examples

### Theme Customizer

```html
<div class="theme-customizer">
  <wa-color-picker
    id="primaryColor"
    label="Primary Color"
    format="hex"
    swatches="#3b82f6; #8b5cf6; #ec4899; #10b981; #f59e0b"
    value="#3b82f6">
  </wa-color-picker>

  <wa-color-picker
    id="secondaryColor"
    label="Secondary Color"
    format="hex"
    swatches="#64748b; #475569; #334155; #1e293b; #0f172a"
    value="#64748b">
  </wa-color-picker>

  <div class="preview" id="themePreview">
    <h3>Preview</h3>
    <wa-button variant="primary" id="previewButton">Primary Button</wa-button>
    <wa-button id="secondaryButton">Secondary Button</wa-button>
  </div>
</div>

<script>
  const primaryPicker = document.getElementById('primaryColor');
  const secondaryPicker = document.getElementById('secondaryColor');
  const preview = document.getElementById('themePreview');
  const primaryButton = document.getElementById('previewButton');
  const secondaryButton = document.getElementById('secondaryButton');

  primaryPicker.addEventListener('wa-change', (e) => {
    primaryButton.style.setProperty('--primary-color', e.target.value);
  });

  secondaryPicker.addEventListener('wa-change', (e) => {
    secondaryButton.style.setProperty('--secondary-color', e.target.value);
  });
</script>
```

### Design Tool Color Selection

```html
<div class="color-tool">
  <wa-color-picker
    id="fillColor"
    label="Fill Color"
    format="rgb"
    opacity
    inline
    value="rgba(59, 130, 246, 1)">
  </wa-color-picker>

  <wa-color-picker
    id="strokeColor"
    label="Stroke Color"
    format="rgb"
    opacity
    inline
    value="rgba(0, 0, 0, 1)">
  </wa-color-picker>

  <canvas id="canvas" width="400" height="300"></canvas>
</div>

<script>
  const fillPicker = document.getElementById('fillColor');
  const strokePicker = document.getElementById('strokeColor');
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');

  function drawShape() {
    ctx.fillStyle = fillPicker.value;
    ctx.strokeStyle = strokePicker.value;
    ctx.lineWidth = 3;

    ctx.beginPath();
    ctx.rect(50, 50, 200, 150);
    ctx.fill();
    ctx.stroke();
  }

  fillPicker.addEventListener('wa-change', drawShape);
  strokePicker.addEventListener('wa-change', drawShape);

  // Initial draw
  drawShape();
</script>
```

### Text Color Editor

```html
<div class="text-editor">
  <wa-color-picker
    id="textColor"
    label="Text Color"
    format="hex"
    size="small"
    swatches="#000000; #374151; #6b7280; #9ca3af; #ffffff">
  </wa-color-picker>

  <wa-color-picker
    id="bgColor"
    label="Background"
    format="hex"
    size="small"
    opacity
    swatches="#ffffff; #f3f4f6; #e5e7eb; #d1d5db; #000000">
  </wa-color-picker>

  <div id="textPreview" style="padding: 2rem; border-radius: 0.5rem;">
    <h2>Sample Heading</h2>
    <p>This is sample text that will change color based on your selection.</p>
  </div>
</div>

<script>
  const textPicker = document.getElementById('textColor');
  const bgPicker = document.getElementById('bgColor');
  const preview = document.getElementById('textPreview');

  textPicker.addEventListener('wa-change', (e) => {
    preview.style.color = e.target.value;
  });

  bgPicker.addEventListener('wa-change', (e) => {
    preview.style.backgroundColor = e.target.value;
  });

  // Initialize
  preview.style.color = '#000000';
  preview.style.backgroundColor = '#ffffff';
</script>
```

### Brand Color Palette Builder

```html
<form id="paletteForm">
  <div class="palette-builder">
    <wa-color-picker
      name="color1"
      label="Primary"
      format="hex"
      value="#3b82f6">
    </wa-color-picker>

    <wa-color-picker
      name="color2"
      label="Secondary"
      format="hex"
      value="#8b5cf6">
    </wa-color-picker>

    <wa-color-picker
      name="color3"
      label="Accent"
      format="hex"
      value="#ec4899">
    </wa-color-picker>

    <wa-color-picker
      name="color4"
      label="Success"
      format="hex"
      value="#10b981">
    </wa-color-picker>

    <wa-color-picker
      name="color5"
      label="Warning"
      format="hex"
      value="#f59e0b">
    </wa-color-picker>

    <wa-color-picker
      name="color6"
      label="Danger"
      format="hex"
      value="#ef4444">
    </wa-color-picker>
  </div>

  <wa-button type="submit" variant="primary">Save Palette</wa-button>
</form>

<script>
  const form = document.getElementById('paletteForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const formData = new FormData(form);
    const palette = {
      primary: formData.get('color1'),
      secondary: formData.get('color2'),
      accent: formData.get('color3'),
      success: formData.get('color4'),
      warning: formData.get('color5'),
      danger: formData.get('color6')
    };

    console.log('Brand Palette:', palette);
    // Save to backend or localStorage
  });
</script>
```

### Chart Color Customizer

```html
<div class="chart-customizer">
  <h3>Chart Colors</h3>

  <wa-color-picker
    id="chartColor1"
    label="Series 1"
    format="rgb"
    swatches="#3b82f6; #2563eb; #1d4ed8"
    value="rgb(59, 130, 246)">
  </wa-color-picker>

  <wa-color-picker
    id="chartColor2"
    label="Series 2"
    format="rgb"
    swatches="#10b981; #059669; #047857"
    value="rgb(16, 185, 129)">
  </wa-color-picker>

  <wa-color-picker
    id="chartColor3"
    label="Series 3"
    format="rgb"
    swatches="#f59e0b; #d97706; #b45309"
    value="rgb(245, 158, 11)">
  </wa-color-picker>

  <canvas id="chartCanvas" width="600" height="400"></canvas>
</div>

<script>
  const picker1 = document.getElementById('chartColor1');
  const picker2 = document.getElementById('chartColor2');
  const picker3 = document.getElementById('chartColor3');

  function updateChart() {
    const colors = [
      picker1.value,
      picker2.value,
      picker3.value
    ];

    // Update your chart library with new colors
    console.log('Chart colors updated:', colors);
  }

  picker1.addEventListener('wa-change', updateChart);
  picker2.addEventListener('wa-change', updateChart);
  picker3.addEventListener('wa-change', updateChart);
</script>
```

### Gradient Creator

```html
<div class="gradient-creator">
  <wa-color-picker
    id="gradientStart"
    label="Start Color"
    format="hex"
    value="#3b82f6"
    inline>
  </wa-color-picker>

  <wa-color-picker
    id="gradientEnd"
    label="End Color"
    format="hex"
    value="#8b5cf6"
    inline>
  </wa-color-picker>

  <div id="gradientPreview" style="height: 200px; border-radius: 0.5rem; margin-top: 1rem;"></div>

  <div id="gradientCode" style="margin-top: 1rem; padding: 1rem; background: #f3f4f6; border-radius: 0.5rem;">
    <code id="gradientCSS"></code>
  </div>
</div>

<script>
  const startPicker = document.getElementById('gradientStart');
  const endPicker = document.getElementById('gradientEnd');
  const preview = document.getElementById('gradientPreview');
  const codeDisplay = document.getElementById('gradientCSS');

  function updateGradient() {
    const start = startPicker.value;
    const end = endPicker.value;
    const gradient = `linear-gradient(to right, ${start}, ${end})`;

    preview.style.background = gradient;
    codeDisplay.textContent = `background: ${gradient};`;
  }

  startPicker.addEventListener('wa-change', updateGradient);
  endPicker.addEventListener('wa-change', updateGradient);

  // Initialize
  updateGradient();
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the color picker | `void` |
| `blur()` | Removes focus from the color picker | `void` |
| `getFormat()` | Returns the current color format | `string` |
| `setColor(color)` | Programmatically sets the color | `void` |

### Method Examples

```javascript
const picker = document.querySelector('wa-color-picker');

// Set a new color
picker.setColor('#ec4899');

// Get the current format
const format = picker.getFormat(); // 'hex', 'rgb', 'hsl', or 'hsv'

// Focus the picker
picker.focus();

// Remove focus
picker.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the color value changes and the user stops selecting | `{ value: string }` |
| `wa-input` | Emitted continuously as the color changes during selection | `{ value: string }` |
| `wa-focus` | Emitted when the color picker gains focus | - |
| `wa-blur` | Emitted when the color picker loses focus | - |

### Event Examples

```javascript
const picker = document.querySelector('wa-color-picker');

// Fired when user completes selection
picker.addEventListener('wa-change', (e) => {
  console.log('Selected color:', e.target.value);
  // Save or apply the color
});

// Fired continuously during color selection
picker.addEventListener('wa-input', (e) => {
  console.log('Current color:', e.target.value);
  // Update live preview
});

// Focus and blur events
picker.addEventListener('wa-focus', () => {
  console.log('Color picker focused');
});

picker.addEventListener('wa-blur', () => {
  console.log('Color picker blurred');
});
```

## Slots

| Slot | Description |
|------|-------------|
| `label` | Custom label content |
| `help-text` | Custom help text content |

## CSS Parts

Use CSS parts to style internal color picker elements:

```css
/* Style the base container */
wa-color-picker::part(base) {
  border: 2px solid #e2e8f0;
}

/* Style the trigger button */
wa-color-picker::part(trigger) {
  border-radius: 0.5rem;
  border: 2px solid #cbd5e1;
}

/* Style the color preview in trigger */
wa-color-picker::part(preview) {
  border-radius: 0.25rem;
}

/* Style the dropdown panel */
wa-color-picker::part(panel) {
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

/* Style the color grid */
wa-color-picker::part(grid) {
  border-radius: 0.5rem;
}

/* Style the swatches container */
wa-color-picker::part(swatches) {
  padding: 1rem;
}

/* Style individual swatch */
wa-color-picker::part(swatch) {
  border-radius: 0.25rem;
  border: 2px solid transparent;
}

/* Style active swatch */
wa-color-picker::part(swatch):hover {
  border-color: #3b82f6;
}
```

## Customization

### Custom Trigger Size

```css
/* Larger trigger button */
wa-color-picker.large::part(trigger) {
  width: 60px;
  height: 60px;
}

/* Smaller trigger button */
wa-color-picker.small::part(trigger) {
  width: 24px;
  height: 24px;
}
```

### Custom Panel Width

```css
/* Wider color picker panel */
wa-color-picker::part(panel) {
  width: 400px;
}
```

### Custom Swatch Grid

```css
/* More swatches per row */
wa-color-picker::part(swatches) {
  grid-template-columns: repeat(10, 1fr);
  gap: 0.5rem;
}
```

## Best Practices

- Use appropriate color formats for your use case (hex for web, RGB for graphics)
- Provide swatches for commonly used colors to speed up selection
- Use `wa-change` for actions that should occur after selection completes
- Use `wa-input` for live previews during color selection
- Enable opacity control when transparency is needed
- Use inline mode for design tools where space permits
- Provide clear labels describing what the color controls
- Consider providing preset color palettes for brand consistency
- Test color contrast for accessibility when colors affect text

## Accessibility

- Color pickers automatically include appropriate ARIA roles and attributes
- Use the `label` attribute to provide accessible labels
- The color picker is keyboard accessible:
  - Arrow keys: Navigate the color grid
  - Enter/Space: Select a color
  - Tab: Move between controls (grid, sliders, swatches)
  - Escape: Close the picker dropdown
- Color values are announced to screen readers
- Don't rely on color alone to convey information
- Ensure sufficient contrast when colors are used for text or important UI elements

## Troubleshooting

### Color Value Not Updating

**Problem:** Selected color doesn't update the value

**Solution:** Ensure you're listening to the correct event

```javascript
// Use wa-change, not change
picker.addEventListener('wa-change', handler);
```

### Invalid Color Format

**Problem:** Color value is rejected or displays incorrectly

**Solution:** Ensure the value matches the specified format

```html
<!-- Correct -->
<wa-color-picker format="hex" value="#3b82f6"></wa-color-picker>

<!-- Incorrect - format mismatch -->
<wa-color-picker format="hex" value="rgb(59, 130, 246)"></wa-color-picker>
```

### Swatches Not Appearing

**Problem:** Swatches don't display

**Solution:** Use semicolons to separate colors and ensure valid color values

```html
<!-- Correct -->
<wa-color-picker swatches="#ff0000; #00ff00; #0000ff"></wa-color-picker>

<!-- Incorrect - using commas -->
<wa-color-picker swatches="#ff0000, #00ff00, #0000ff"></wa-color-picker>
```

## Related

- [Slider](./slider.md)
- [Input](./input.md)
- [Select](./select.md)
- [Form Controls Guide](../guides/form-controls.md)
