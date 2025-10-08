# Alert

Alerts display important messages or notifications to users.

## Overview

The `<wa-alert>` component provides a way to display contextual feedback messages to users. It supports multiple variants, can be dismissible, and includes auto-hide functionality with customizable duration.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/alert/alert.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default alert -->
<wa-alert open>
  This is a basic alert message.
</wa-alert>

<!-- Primary alert -->
<wa-alert variant="primary" open>
  This is a primary alert.
</wa-alert>

<!-- Alert with icon -->
<wa-alert variant="success" open>
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  Operation completed successfully!
</wa-alert>

<!-- Closable alert -->
<wa-alert variant="warning" open closable>
  This alert can be dismissed.
</wa-alert>
```

## Variants

Alerts support multiple visual variants to convey different types of messages:

```html
<wa-alert variant="primary" open>
  <wa-icon slot="icon" name="info-circle"></wa-icon>
  <strong>Primary</strong><br />
  This is a primary alert for general information.
</wa-alert>

<wa-alert variant="success" open>
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  <strong>Success</strong><br />
  Your changes have been saved successfully.
</wa-alert>

<wa-alert variant="neutral" open>
  <wa-icon slot="icon" name="gear"></wa-icon>
  <strong>Neutral</strong><br />
  This is a neutral alert for system messages.
</wa-alert>

<wa-alert variant="warning" open>
  <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
  <strong>Warning</strong><br />
  Please review the following information carefully.
</wa-alert>

<wa-alert variant="danger" open>
  <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
  <strong>Danger</strong><br />
  An error occurred while processing your request.
</wa-alert>
```

## Closable Alerts

Add the `closable` attribute to allow users to dismiss alerts:

```html
<wa-alert variant="primary" open closable>
  <wa-icon slot="icon" name="info-circle"></wa-icon>
  This alert can be closed by the user.
</wa-alert>
```

### Handling Close Events

```html
<wa-alert id="myAlert" variant="success" open closable>
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  This alert will log when closed.
</wa-alert>

<script>
  const alert = document.getElementById('myAlert');

  alert.addEventListener('wa-after-hide', () => {
    console.log('Alert was closed');
  });
</script>
```

## Auto-Hide

Use the `duration` attribute to automatically hide alerts after a specified time (in milliseconds):

```html
<!-- Auto-hide after 3 seconds -->
<wa-alert variant="success" open duration="3000">
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  This alert will disappear in 3 seconds.
</wa-alert>

<!-- Auto-hide with closable -->
<wa-alert variant="primary" open closable duration="5000">
  <wa-icon slot="icon" name="info-circle"></wa-icon>
  Auto-hide in 5 seconds, or close manually.
</wa-alert>
```

### Dynamic Duration

```html
<wa-button id="showAlert">Show Temporary Alert</wa-button>

<wa-alert id="tempAlert" variant="success">
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  Your action was successful!
</wa-alert>

<script>
  const button = document.getElementById('showAlert');
  const alert = document.getElementById('tempAlert');

  button.addEventListener('click', () => {
    alert.duration = 3000;
    alert.show();
  });
</script>
```

## Programmatic Control

Control alert visibility using methods:

```html
<wa-button id="showBtn">Show Alert</wa-button>
<wa-button id="hideBtn">Hide Alert</wa-button>

<wa-alert id="controlledAlert" variant="primary">
  <wa-icon slot="icon" name="info-circle"></wa-icon>
  This alert is controlled programmatically.
</wa-alert>

<script>
  const alert = document.getElementById('controlledAlert');
  const showBtn = document.getElementById('showBtn');
  const hideBtn = document.getElementById('hideBtn');

  showBtn.addEventListener('click', () => alert.show());
  hideBtn.addEventListener('click', () => alert.hide());
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `variant` | string | `'primary'` | No | Alert variant: `primary`, `success`, `neutral`, `warning`, `danger` |
| `open` | boolean | `false` | No | Show or hide the alert |
| `closable` | boolean | `false` | No | Show a close button |
| `duration` | number | `Infinity` | No | Auto-hide duration in milliseconds. Set to `Infinity` to disable auto-hide |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Shows the alert | `Promise<void>` |
| `hide()` | Hides the alert | `Promise<void>` |
| `toast()` | Displays the alert as a toast notification | `Promise<void>` |

### Method Examples

```javascript
const alert = document.querySelector('wa-alert');

// Show the alert
await alert.show();

// Hide the alert
await alert.hide();

// Show as toast
await alert.toast();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the alert starts to show | - |
| `wa-after-show` | Emitted after the alert has finished showing and animations are complete | - |
| `wa-hide` | Emitted when the alert starts to hide | - |
| `wa-after-hide` | Emitted after the alert has finished hiding and animations are complete | - |

### Event Examples

```javascript
const alert = document.querySelector('wa-alert');

alert.addEventListener('wa-show', () => {
  console.log('Alert is showing');
});

alert.addEventListener('wa-after-show', () => {
  console.log('Alert is now visible');
});

alert.addEventListener('wa-hide', () => {
  console.log('Alert is hiding');
});

alert.addEventListener('wa-after-hide', () => {
  console.log('Alert is now hidden');
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The alert's main content |
| `icon` | An icon to show before the content |

## Examples

### Form Validation Alert

```html
<form id="signupForm">
  <wa-alert id="errorAlert" variant="danger" closable style="margin-bottom: 1rem;">
    <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
    <span id="errorMessage"></span>
  </wa-alert>

  <wa-input name="email" label="Email" type="email" required></wa-input>
  <wa-input name="password" label="Password" type="password" required></wa-input>
  <wa-button type="submit" variant="primary">Sign Up</wa-button>
</form>

<script>
  const form = document.getElementById('signupForm');
  const errorAlert = document.getElementById('errorAlert');
  const errorMessage = document.getElementById('errorMessage');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();

    try {
      const formData = new FormData(form);
      const response = await fetch('/api/signup', {
        method: 'POST',
        body: formData
      });

      if (!response.ok) {
        const error = await response.json();
        errorMessage.textContent = error.message;
        errorAlert.show();
      }
    } catch (error) {
      errorMessage.textContent = 'An unexpected error occurred.';
      errorAlert.show();
    }
  });
</script>
```

### Success Notification

```html
<wa-button id="saveBtn" variant="primary">Save Changes</wa-button>

<wa-alert id="successAlert" variant="success" duration="3000">
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  Your changes have been saved successfully!
</wa-alert>

<script>
  const saveBtn = document.getElementById('saveBtn');
  const successAlert = document.getElementById('successAlert');

  saveBtn.addEventListener('click', async () => {
    saveBtn.loading = true;

    try {
      await saveData(); // Your save function
      successAlert.show();
    } catch (error) {
      console.error('Save failed:', error);
    } finally {
      saveBtn.loading = false;
    }
  });
</script>
```

### Warning with Action

```html
<wa-alert variant="warning" open closable>
  <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
  <strong>Your session will expire soon.</strong><br />
  <small>You have 5 minutes of inactivity remaining.</small>
  <br /><br />
  <wa-button size="small" variant="warning" outline>Extend Session</wa-button>
</wa-alert>
```

### Multiple Alerts

```html
<div id="alertContainer" style="display: flex; flex-direction: column; gap: 1rem;">
  <!-- Alerts will be added here dynamically -->
</div>

<wa-button id="addAlert">Add Alert</wa-button>

<script>
  const container = document.getElementById('alertContainer');
  const addButton = document.getElementById('addAlert');

  const variants = ['primary', 'success', 'neutral', 'warning', 'danger'];
  const messages = [
    'This is a primary message',
    'Operation successful!',
    'Neutral information',
    'Please be careful',
    'An error occurred'
  ];

  addButton.addEventListener('click', () => {
    const index = Math.floor(Math.random() * variants.length);
    const alert = document.createElement('wa-alert');

    alert.variant = variants[index];
    alert.open = true;
    alert.closable = true;
    alert.duration = 5000;
    alert.innerHTML = `
      <wa-icon slot="icon" name="info-circle"></wa-icon>
      ${messages[index]}
    `;

    container.appendChild(alert);
  });
</script>
```

## CSS Parts

Use CSS parts to style internal alert elements:

```css
/* Style the base alert */
wa-alert::part(base) {
  border-radius: 8px;
  border-width: 2px;
}

/* Style the icon container */
wa-alert::part(icon) {
  font-size: 1.5rem;
}

/* Style the message container */
wa-alert::part(message) {
  font-size: 0.95rem;
}

/* Style the close button */
wa-alert::part(close-button) {
  color: inherit;
}
```

## Customization

### Custom Styling

```css
/* Custom danger alert */
wa-alert[variant="danger"]::part(base) {
  background-color: #fee;
  border-color: #f00;
  color: #c00;
}

/* Custom icon size */
wa-alert::part(icon) {
  font-size: 2rem;
}
```

### Alert Stack

```html
<style>
  .alert-stack {
    position: fixed;
    top: 1rem;
    right: 1rem;
    z-index: 1000;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    max-width: 400px;
  }
</style>

<div class="alert-stack" id="alertStack"></div>
```

## Best Practices

- ✅ Use appropriate variants for message types (success, warning, danger)
- ✅ Include descriptive icons to enhance understanding
- ✅ Keep messages concise and actionable
- ✅ Use auto-hide for temporary notifications
- ✅ Make alerts closable for persistent messages
- ❌ Don't show too many alerts at once
- ❌ Avoid using alerts for every minor action
- ❌ Don't use danger variant for non-critical messages

## Accessibility

- Alerts automatically include appropriate ARIA roles (`role="alert"`)
- Use meaningful content that clearly describes the issue or message
- Ensure sufficient color contrast for all variants
- The close button includes proper ARIA labels
- Screen readers announce alert content when shown

```html
<!-- Accessible alert with clear message -->
<wa-alert variant="danger" open closable aria-live="assertive">
  <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
  <strong>Error:</strong> Password must be at least 8 characters long.
</wa-alert>
```

## Troubleshooting

### Alert Not Showing

**Problem:** Alert doesn't appear when `open` is set

**Solution:** Ensure the alert has content and check CSS display properties

```javascript
const alert = document.querySelector('wa-alert');
alert.open = true;
// Or use the show method
alert.show();
```

### Auto-Hide Not Working

**Problem:** Alert doesn't automatically hide

**Solution:** Verify duration is set correctly and is a number

```html
<!-- ✅ Correct -->
<wa-alert duration="3000" open>Message</wa-alert>

<!-- ❌ Won't work -->
<wa-alert duration="forever" open>Message</wa-alert>
```

### Events Not Firing

**Problem:** `wa-show` or `wa-hide` events aren't detected

**Solution:** Ensure event listeners are attached before showing/hiding

```javascript
const alert = document.querySelector('wa-alert');

// Attach listener first
alert.addEventListener('wa-after-show', () => {
  console.log('Alert shown');
});

// Then show the alert
alert.show();
```

## Related

- [Toast](./toast.md)
- [Dialog](./dialog.md)
- [Icon](./icon.md)
- [Notification Patterns Guide](../guides/notification-patterns.md)
