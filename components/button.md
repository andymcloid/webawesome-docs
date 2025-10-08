# Button

Buttons represent actions that are available to the user.

## Overview

The `<wa-button>` component provides a fully customizable button element with multiple variants, sizes, and states. It supports icons, loading states, and can render as either a button or a link.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/button/button.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default button -->
<wa-button>Button</wa-button>

<!-- Primary button -->
<wa-button variant="primary">Primary</wa-button>

<!-- Button with icon -->
<wa-button>
  <wa-icon slot="start" name="gear"></wa-icon>
  Settings
</wa-button>

<!-- Disabled button -->
<wa-button disabled>Disabled</wa-button>
```

## Variants

Buttons support multiple visual variants:

```html
<wa-button variant="default">Default</wa-button>
<wa-button variant="primary">Primary</wa-button>
<wa-button variant="success">Success</wa-button>
<wa-button variant="neutral">Neutral</wa-button>
<wa-button variant="warning">Warning</wa-button>
<wa-button variant="danger">Danger</wa-button>
```

### Outline Buttons

Add the `outline` attribute for outlined variants:

```html
<wa-button variant="primary" outline>Primary Outline</wa-button>
<wa-button variant="success" outline>Success Outline</wa-button>
<wa-button variant="danger" outline>Danger Outline</wa-button>
```

## Sizes

Control button size with the `size` attribute:

```html
<wa-button size="small">Small</wa-button>
<wa-button size="medium">Medium (default)</wa-button>
<wa-button size="large">Large</wa-button>
```

## Shapes

### Pill Buttons

Make buttons rounded with the `pill` attribute:

```html
<wa-button pill>Pill Button</wa-button>
<wa-button variant="primary" pill>Primary Pill</wa-button>
```

### Circle Buttons

Create circular icon buttons with the `circle` attribute:

```html
<wa-button circle>
  <wa-icon name="gear"></wa-icon>
</wa-button>

<wa-button variant="primary" circle>
  <wa-icon name="plus"></wa-icon>
</wa-button>
```

## Button as Link

Set the `href` attribute to render the button as a link:

```html
<!-- Button renders as <a> -->
<wa-button href="https://example.com">Visit Website</wa-button>

<!-- With target and rel attributes -->
<wa-button href="https://example.com" target="_blank" rel="noopener noreferrer">
  External Link
</wa-button>

<!-- Download link -->
<wa-button href="/files/document.pdf" download="document.pdf">
  Download PDF
</wa-button>
```

## Icons

Use the `start` and `end` slots for icons:

```html
<!-- Icon before text -->
<wa-button>
  <wa-icon slot="start" name="gear"></wa-icon>
  Settings
</wa-button>

<!-- Icon after text -->
<wa-button>
  Next
  <wa-icon slot="end" name="arrow-right"></wa-icon>
</wa-button>

<!-- Icons on both sides -->
<wa-button>
  <wa-icon slot="start" name="arrow-left"></wa-icon>
  Previous
  <wa-icon slot="end" name="arrow-right"></wa-icon>
</wa-button>
```

## Loading State

Show a loading spinner with the `loading` attribute:

```html
<wa-button loading>Loading</wa-button>
<wa-button variant="primary" loading>Processing</wa-button>
```

### Dynamic Loading State

```html
<wa-button id="saveButton">Save Changes</wa-button>

<script>
  const button = document.getElementById('saveButton');

  button.addEventListener('click', async () => {
    button.loading = true;

    try {
      await saveData(); // Your async operation
      button.loading = false;
    } catch (error) {
      button.loading = false;
    }
  });
</script>
```

## Button Groups

Use `<wa-button-group>` to group related buttons:

```html
<wa-button-group>
  <wa-button>Left</wa-button>
  <wa-button>Center</wa-button>
  <wa-button>Right</wa-button>
</wa-button-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `variant` | string | `'default'` | No | Button variant: `default`, `primary`, `success`, `neutral`, `warning`, `danger` |
| `size` | string | `'medium'` | No | Button size: `small`, `medium`, `large` |
| `outline` | boolean | `false` | No | Render button as outlined |
| `pill` | boolean | `false` | No | Render button with rounded ends |
| `circle` | boolean | `false` | No | Render button as a circle (for icon-only buttons) |
| `disabled` | boolean | `false` | No | Disable the button |
| `loading` | boolean | `false` | No | Show loading spinner and disable interaction |
| `type` | string | `'button'` | No | Button type: `button`, `submit`, `reset` |
| `name` | string | - | No | Name attribute (for forms) |
| `value` | string | - | No | Value attribute (for forms) |
| `href` | string | - | No | When set, renders button as `<a>` link |
| `target` | string | - | No | Link target (requires `href`) |
| `rel` | string | - | No | Link relationship (requires `href`) |
| `download` | string | - | No | Download attribute (requires `href`) |

## Examples

### Form Submit Button

```html
<form id="myForm">
  <wa-input name="email" label="Email" type="email" required></wa-input>
  <wa-button type="submit" variant="primary">Submit</wa-button>
</form>
```

### Async Action with Loading State

```html
<wa-button id="loadData" variant="primary">Load Data</wa-button>

<script>
  const button = document.getElementById('loadData');

  button.addEventListener('click', async () => {
    button.loading = true;

    try {
      const response = await fetch('/api/data');
      const data = await response.json();
      console.log('Data loaded:', data);
    } catch (error) {
      console.error('Error:', error);
    } finally {
      button.loading = false;
    }
  });
</script>
```

### Confirmation Button

```html
<wa-button id="deleteButton" variant="danger">
  <wa-icon slot="start" name="trash"></wa-icon>
  Delete
</wa-button>

<wa-dialog id="confirmDialog" label="Confirm Deletion">
  <p>Are you sure you want to delete this item?</p>
  <wa-button slot="footer" id="cancelBtn">Cancel</wa-button>
  <wa-button slot="footer" variant="danger" id="confirmBtn">Delete</wa-button>
</wa-dialog>

<script>
  const deleteButton = document.getElementById('deleteButton');
  const dialog = document.getElementById('confirmDialog');
  const cancelBtn = document.getElementById('cancelBtn');
  const confirmBtn = document.getElementById('confirmBtn');

  deleteButton.addEventListener('click', () => dialog.show());
  cancelBtn.addEventListener('click', () => dialog.hide());
  confirmBtn.addEventListener('click', () => {
    // Perform delete action
    dialog.hide();
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `click()` | Simulates a click on the button | `void` |
| `focus(options?)` | Sets focus on the button | `void` |
| `blur()` | Removes focus from the button | `void` |

### Method Examples

```javascript
const button = document.querySelector('wa-button');

// Programmatically click the button
button.click();

// Focus the button
button.focus();

// Focus with options
button.focus({ preventScroll: true });

// Remove focus
button.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `click` | Fired when the button is clicked | - |
| `focus` | Fired when the button gains focus | - |
| `blur` | Fired when the button loses focus | - |
| `wa-focus` | Emitted when the button gains focus | - |
| `wa-blur` | Emitted when the button loses focus | - |

### Event Examples

```javascript
const button = document.querySelector('wa-button');

// Standard click event
button.addEventListener('click', () => {
  console.log('Button clicked');
});

// WebAwesome focus event
button.addEventListener('wa-focus', () => {
  console.log('Button focused');
});

// WebAwesome blur event
button.addEventListener('wa-blur', () => {
  console.log('Button blurred');
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Button label |
| `start` | Content before the label (typically icons) |
| `end` | Content after the label (typically icons) |

## CSS Parts

Use CSS parts to style internal button elements:

```css
/* Style the base button */
wa-button::part(base) {
  border-radius: 0;
}

/* Style the button label */
wa-button::part(label) {
  font-weight: bold;
}

/* Style the start slot container */
wa-button::part(start) {
  margin-right: 1rem;
}

/* Style the end slot container */
wa-button::part(end) {
  margin-left: 1rem;
}
```

## Customization

### Custom Colors

```css
/* Custom primary button colors */
wa-button[variant="primary"]::part(base) {
  background-color: #6366f1;
  border-color: #6366f1;
  color: white;
}

wa-button[variant="primary"]::part(base):hover {
  background-color: #4f46e5;
}
```

### Custom Sizes

```css
/* Extra large button */
wa-button.xl::part(base) {
  font-size: 1.25rem;
  padding: 1rem 2rem;
}
```

### Full Width Button

```html
<wa-button style="width: 100%;">Full Width Button</wa-button>
```

## Best Practices

- ✅ Use `type="button"` for non-submit buttons in forms
- ✅ Provide clear, action-oriented button labels
- ✅ Use appropriate variants for button importance
- ✅ Include icons to enhance clarity when appropriate
- ✅ Use loading state for async operations
- ❌ Don't use too many button variants on the same screen
- ❌ Avoid ambiguous labels like "Click here" or "OK"
- ❌ Don't nest buttons inside other interactive elements

## Accessibility

- Buttons automatically include appropriate ARIA roles
- Use descriptive button text for screen readers
- For icon-only buttons, provide an `aria-label`:

```html
<wa-button circle aria-label="Settings">
  <wa-icon name="gear"></wa-icon>
</wa-button>
```

- Disabled buttons are automatically excluded from tab order
- Loading state announces to screen readers

## Troubleshooting

### Button Not Clickable

**Problem:** Button doesn't respond to clicks

**Solution:** Check if button is disabled or in loading state

```javascript
button.disabled = false;
button.loading = false;
```

### Link Button Not Working

**Problem:** `href` attribute doesn't navigate

**Solution:** Ensure you're using the correct URL and the button isn't disabled

```html
<!-- ✅ Correct -->
<wa-button href="/page">Link</wa-button>

<!-- ❌ Won't work if disabled -->
<wa-button href="/page" disabled>Link</wa-button>
```

## Related

- [Button Group](./button-group.md)
- [Icon Button](./icon-button.md)
- [Icon](./icon.md)
- [Form Controls Guide](../guides/form-controls.md)
