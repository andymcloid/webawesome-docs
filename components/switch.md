# Switch

A toggle switch control for binary on/off states.

## Overview

The `<wa-switch>` component provides an intuitive toggle control for enabling or disabling options. It's commonly used in settings panels, feature toggles, and forms where users need to make binary choices. The component supports various states including checked, disabled, and required.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/switch/switch.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default switch (unchecked) -->
<wa-switch>Enable notifications</wa-switch>

<!-- Checked switch -->
<wa-switch checked>Dark mode</wa-switch>

<!-- Disabled switch -->
<wa-switch disabled>Unavailable option</wa-switch>

<!-- Required switch -->
<wa-switch required>Accept terms and conditions</wa-switch>
```

## States

### Checked State

```html
<!-- Unchecked by default -->
<wa-switch>Unchecked</wa-switch>

<!-- Checked by default -->
<wa-switch checked>Checked</wa-switch>
```

### Disabled State

```html
<!-- Disabled unchecked -->
<wa-switch disabled>Disabled unchecked</wa-switch>

<!-- Disabled checked -->
<wa-switch disabled checked>Disabled checked</wa-switch>
```

### Required State

```html
<form>
  <wa-switch required>I agree to the terms (required)</wa-switch>
  <wa-button type="submit">Submit</wa-button>
</form>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `checked` | boolean | `false` | No | Whether the switch is checked |
| `disabled` | boolean | `false` | No | Disable the switch |
| `required` | boolean | `false` | No | Make the switch required in forms |
| `name` | string | - | No | Name attribute for form submission |
| `value` | string | `'on'` | No | Value attribute for form submission |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the checked state changes | `{ checked: boolean }` |
| `wa-focus` | Emitted when the switch gains focus | - |
| `wa-blur` | Emitted when the switch loses focus | - |

### Event Examples

```javascript
const toggle = document.querySelector('wa-switch');

// Listen for state changes
toggle.addEventListener('wa-change', (event) => {
  console.log('Switch is now:', event.detail.checked ? 'ON' : 'OFF');
});

// Listen for focus
toggle.addEventListener('wa-focus', () => {
  console.log('Switch focused');
});

// Listen for blur
toggle.addEventListener('wa-blur', () => {
  console.log('Switch blurred');
});
```

## Examples

### Settings Panel

```html
<div style="max-width: 400px;">
  <h3>Settings</h3>

  <div style="margin-bottom: 1rem;">
    <wa-switch id="notifications" checked>
      Enable notifications
    </wa-switch>
  </div>

  <div style="margin-bottom: 1rem;">
    <wa-switch id="darkMode">
      Dark mode
    </wa-switch>
  </div>

  <div style="margin-bottom: 1rem;">
    <wa-switch id="autoSave" checked>
      Auto-save changes
    </wa-switch>
  </div>

  <div style="margin-bottom: 1rem;">
    <wa-switch id="analytics">
      Share analytics data
    </wa-switch>
  </div>
</div>

<script>
  const notifications = document.getElementById('notifications');
  const darkMode = document.getElementById('darkMode');
  const autoSave = document.getElementById('autoSave');
  const analytics = document.getElementById('analytics');

  // Handle dark mode toggle
  darkMode.addEventListener('wa-change', (e) => {
    document.body.classList.toggle('dark-theme', e.detail.checked);
  });

  // Handle auto-save toggle
  autoSave.addEventListener('wa-change', (e) => {
    if (e.detail.checked) {
      console.log('Auto-save enabled');
    } else {
      console.log('Auto-save disabled');
    }
  });
</script>
```

### Feature Toggle with Confirmation

```html
<wa-switch id="dangerousFeature">
  Enable experimental features
</wa-switch>

<wa-dialog id="confirmDialog" label="Confirm Action">
  <p>Experimental features may be unstable. Are you sure you want to enable them?</p>
  <wa-button slot="footer" id="cancelBtn">Cancel</wa-button>
  <wa-button slot="footer" variant="primary" id="confirmBtn">Enable</wa-button>
</wa-dialog>

<script>
  const toggle = document.getElementById('dangerousFeature');
  const dialog = document.getElementById('confirmDialog');
  const cancelBtn = document.getElementById('cancelBtn');
  const confirmBtn = document.getElementById('confirmBtn');

  toggle.addEventListener('wa-change', (e) => {
    if (e.detail.checked) {
      // Show confirmation dialog
      dialog.show();
    }
  });

  cancelBtn.addEventListener('click', () => {
    toggle.checked = false;
    dialog.hide();
  });

  confirmBtn.addEventListener('click', () => {
    console.log('Experimental features enabled');
    dialog.hide();
  });
</script>
```

### Form Integration

```html
<form id="preferencesForm">
  <h3>User Preferences</h3>

  <wa-switch name="newsletter" value="yes" checked>
    Subscribe to newsletter
  </wa-switch>

  <wa-switch name="marketing" value="yes">
    Receive marketing emails
  </wa-switch>

  <wa-switch name="privacy" value="yes" required>
    Accept privacy policy (required)
  </wa-switch>

  <wa-button type="submit" variant="primary" style="margin-top: 1rem;">
    Save Preferences
  </wa-button>
</form>

<script>
  const form = document.getElementById('preferencesForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(form);

    console.log('Form data:');
    for (let [key, value] of formData.entries()) {
      console.log(`${key}: ${value}`);
    }
  });
</script>
```

### Dependent Switches

```html
<div style="max-width: 400px;">
  <wa-switch id="masterSwitch">
    Enable all features
  </wa-switch>

  <div id="features" style="margin-left: 2rem; margin-top: 1rem; opacity: 0.5;">
    <wa-switch id="feature1" disabled>Feature 1</wa-switch>
    <wa-switch id="feature2" disabled>Feature 2</wa-switch>
    <wa-switch id="feature3" disabled>Feature 3</wa-switch>
  </div>
</div>

<script>
  const masterSwitch = document.getElementById('masterSwitch');
  const featuresContainer = document.getElementById('features');
  const featureSwitches = [
    document.getElementById('feature1'),
    document.getElementById('feature2'),
    document.getElementById('feature3')
  ];

  masterSwitch.addEventListener('wa-change', (e) => {
    const isEnabled = e.detail.checked;

    featureSwitches.forEach(toggle => {
      toggle.disabled = !isEnabled;
      if (!isEnabled) {
        toggle.checked = false;
      }
    });

    featuresContainer.style.opacity = isEnabled ? '1' : '0.5';
  });
</script>
```

### Toggle with Status Indicator

```html
<div style="display: flex; align-items: center; gap: 1rem;">
  <wa-switch id="statusToggle">
    Server status
  </wa-switch>
  <wa-badge id="statusBadge" variant="danger">Offline</wa-badge>
</div>

<script>
  const statusToggle = document.getElementById('statusToggle');
  const statusBadge = document.getElementById('statusBadge');

  statusToggle.addEventListener('wa-change', async (e) => {
    if (e.detail.checked) {
      statusBadge.textContent = 'Starting...';
      statusBadge.variant = 'warning';

      // Simulate server start
      await new Promise(resolve => setTimeout(resolve, 1000));

      statusBadge.textContent = 'Online';
      statusBadge.variant = 'success';
    } else {
      statusBadge.textContent = 'Stopping...';
      statusBadge.variant = 'warning';

      // Simulate server stop
      await new Promise(resolve => setTimeout(resolve, 1000));

      statusBadge.textContent = 'Offline';
      statusBadge.variant = 'danger';
    }
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the switch | `void` |
| `blur()` | Removes focus from the switch | `void` |
| `click()` | Simulates a click on the switch | `void` |

### Method Examples

```javascript
const toggle = document.querySelector('wa-switch');

// Programmatically toggle
toggle.click();

// Focus the switch
toggle.focus();

// Remove focus
toggle.blur();

// Set checked state
toggle.checked = true;

// Get checked state
console.log(toggle.checked); // true or false
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Label text for the switch |

## CSS Parts

Use CSS parts to style internal switch elements:

```css
/* Style the switch base */
wa-switch::part(base) {
  border: 2px solid currentColor;
}

/* Style the switch control */
wa-switch::part(control) {
  background-color: #e5e7eb;
}

/* Style the switch thumb */
wa-switch::part(thumb) {
  background-color: white;
}

/* Style the label */
wa-switch::part(label) {
  font-weight: 500;
}
```

## Customization

### Custom Colors

```css
/* Custom checked color */
wa-switch[checked]::part(control) {
  background-color: #10b981;
}

/* Custom unchecked color */
wa-switch::part(control) {
  background-color: #d1d5db;
}

/* Custom disabled color */
wa-switch[disabled]::part(control) {
  background-color: #f3f4f6;
  opacity: 0.5;
}
```

### Custom Size

```css
/* Larger switch */
wa-switch.large {
  font-size: 1.25rem;
}

/* Smaller switch */
wa-switch.small {
  font-size: 0.875rem;
}
```

## Best Practices

- Use switches for settings and preferences that take effect immediately
- Use checkboxes for options that require form submission
- Provide clear, concise labels that describe what the switch controls
- Place the label after the switch (right side) for consistency
- Use the checked state to indicate "on" or "enabled"
- Don't use switches for actions that require additional confirmation
- Group related switches together in settings panels
- Consider using disabled state for options that depend on other settings

## Accessibility

- Switches automatically include `role="switch"` and appropriate ARIA attributes
- The checked state is announced to screen readers
- Switches are keyboard accessible (Space to toggle)
- Disabled switches are automatically excluded from tab order
- Always provide a descriptive label:

```html
<wa-switch aria-label="Enable dark mode">Dark mode</wa-switch>
```

- For switches that control other content, use `aria-controls`:

```html
<wa-switch id="advancedToggle" aria-controls="advancedSettings">
  Show advanced settings
</wa-switch>

<div id="advancedSettings" hidden>
  <!-- Advanced settings content -->
</div>
```

## Troubleshooting

### Switch Not Toggling

**Problem:** Switch doesn't change state when clicked

**Solution:** Check if the switch is disabled

```javascript
toggle.disabled = false;
```

### State Not Persisting

**Problem:** Switch state resets after page reload

**Solution:** Save state to localStorage

```javascript
const toggle = document.getElementById('mySwitch');

// Load saved state
const savedState = localStorage.getItem('mySwitchState');
if (savedState !== null) {
  toggle.checked = savedState === 'true';
}

// Save state on change
toggle.addEventListener('wa-change', (e) => {
  localStorage.setItem('mySwitchState', e.detail.checked);
});
```

### Form Not Submitting Switch Value

**Problem:** Switch value not included in form submission

**Solution:** Ensure the switch has a `name` attribute

```html
<!-- Won't be submitted -->
<wa-switch checked>Option</wa-switch>

<!-- Will be submitted -->
<wa-switch name="myOption" checked>Option</wa-switch>
```

## Related

- [Checkbox](./checkbox.md)
- [Radio](./radio.md)
- [Form Controls Guide](../guides/form-controls.md)
- [Validation Guide](../guides/validation.md)
