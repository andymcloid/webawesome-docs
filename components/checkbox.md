# Checkbox

Checkboxes allow users to select one or more items from a set or toggle an option on or off.

## Overview

The `<wa-checkbox>` component provides a fully customizable checkbox input with support for checked, unchecked, and indeterminate states. It integrates seamlessly with forms and supports validation, custom styling, and accessibility features out of the box.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/checkbox/checkbox.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default checkbox -->
<wa-checkbox>Accept terms and conditions</wa-checkbox>

<!-- Checked checkbox -->
<wa-checkbox checked>Subscribe to newsletter</wa-checkbox>

<!-- Disabled checkbox -->
<wa-checkbox disabled>Disabled option</wa-checkbox>

<!-- Required checkbox -->
<wa-checkbox required>I agree to the terms</wa-checkbox>
```

## States

### Checked State

Use the `checked` attribute to set the checkbox as checked by default:

```html
<wa-checkbox checked>Selected by default</wa-checkbox>
```

### Indeterminate State

The indeterminate state represents a checkbox that is neither checked nor unchecked, commonly used for "select all" functionality:

```html
<wa-checkbox id="selectAll">Select All</wa-checkbox>

<script>
  const selectAll = document.getElementById('selectAll');
  selectAll.indeterminate = true;
</script>
```

### Disabled State

Disable checkbox interaction with the `disabled` attribute:

```html
<wa-checkbox disabled>Disabled unchecked</wa-checkbox>
<wa-checkbox checked disabled>Disabled checked</wa-checkbox>
<wa-checkbox id="disabledIndeterminate" disabled>Disabled indeterminate</wa-checkbox>

<script>
  document.getElementById('disabledIndeterminate').indeterminate = true;
</script>
```

## Sizes

Control checkbox size with the `size` attribute:

```html
<wa-checkbox size="small">Small checkbox</wa-checkbox>
<wa-checkbox size="medium">Medium checkbox (default)</wa-checkbox>
<wa-checkbox size="large">Large checkbox</wa-checkbox>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `checked` | boolean | `false` | No | Whether the checkbox is checked |
| `disabled` | boolean | `false` | No | Disable the checkbox |
| `required` | boolean | `false` | No | Make the checkbox required for form validation |
| `indeterminate` | boolean | `false` | No | Set the checkbox to indeterminate state |
| `name` | string | - | No | Name attribute (for forms) |
| `value` | string | `'on'` | No | Value attribute (for forms) |
| `size` | string | `'medium'` | No | Checkbox size: `small`, `medium`, `large` |

## Examples

### Basic Checkbox

```html
<wa-checkbox>Enable notifications</wa-checkbox>
```

### Checked State

```html
<wa-checkbox checked>Remember me</wa-checkbox>
```

### Indeterminate State

Useful for representing a partially selected state:

```html
<wa-checkbox id="parentCheckbox">Select All Items</wa-checkbox>
<div style="margin-left: 1.5rem;">
  <wa-checkbox class="child-checkbox" value="item1">Item 1</wa-checkbox><br>
  <wa-checkbox class="child-checkbox" value="item2">Item 2</wa-checkbox><br>
  <wa-checkbox class="child-checkbox" value="item3">Item 3</wa-checkbox>
</div>

<script>
  const parent = document.getElementById('parentCheckbox');
  const children = document.querySelectorAll('.child-checkbox');

  // Update parent when children change
  children.forEach(child => {
    child.addEventListener('wa-change', () => {
      const checkedCount = Array.from(children).filter(c => c.checked).length;

      if (checkedCount === 0) {
        parent.checked = false;
        parent.indeterminate = false;
      } else if (checkedCount === children.length) {
        parent.checked = true;
        parent.indeterminate = false;
      } else {
        parent.indeterminate = true;
      }
    });
  });

  // Update children when parent changes
  parent.addEventListener('wa-change', () => {
    children.forEach(child => {
      child.checked = parent.checked;
    });
  });
</script>
```

### Disabled State

```html
<wa-checkbox disabled>Unavailable option</wa-checkbox>
<wa-checkbox checked disabled>Pre-selected and locked</wa-checkbox>
```

### Form Integration

```html
<form id="preferencesForm">
  <div style="display: flex; flex-direction: column; gap: 0.5rem;">
    <wa-checkbox name="newsletter" value="yes">
      Subscribe to newsletter
    </wa-checkbox>

    <wa-checkbox name="notifications" value="yes" checked>
      Enable notifications
    </wa-checkbox>

    <wa-checkbox name="terms" value="accepted" required>
      I agree to the terms and conditions *
    </wa-checkbox>
  </div>

  <br>
  <wa-button type="submit" variant="primary">Save Preferences</wa-button>
</form>

<script>
  const form = document.getElementById('preferencesForm');

  form.addEventListener('submit', (event) => {
    event.preventDefault();

    const formData = new FormData(form);
    console.log('Form data:', Object.fromEntries(formData));

    // Check if required checkbox is checked
    const termsCheckbox = form.querySelector('[name="terms"]');
    if (!termsCheckbox.checkValidity()) {
      alert('Please accept the terms and conditions');
      return;
    }

    alert('Form submitted successfully!');
  });
</script>
```

### Custom Validation

```html
<form id="validationForm">
  <wa-checkbox id="ageConfirm" required>
    I confirm that I am 18 years or older *
  </wa-checkbox>

  <br><br>
  <wa-button type="submit" variant="primary">Continue</wa-button>
  <div id="errorMessage" style="color: red; margin-top: 0.5rem; display: none;">
    You must confirm your age to continue
  </div>
</form>

<script>
  const validationForm = document.getElementById('validationForm');
  const ageConfirm = document.getElementById('ageConfirm');
  const errorMessage = document.getElementById('errorMessage');

  validationForm.addEventListener('submit', (event) => {
    event.preventDefault();

    if (!ageConfirm.checkValidity() || !ageConfirm.checked) {
      errorMessage.style.display = 'block';
      ageConfirm.focus();
      return;
    }

    errorMessage.style.display = 'none';
    alert('Validation passed!');
  });

  ageConfirm.addEventListener('wa-change', () => {
    if (ageConfirm.checked) {
      errorMessage.style.display = 'none';
    }
  });
</script>
```

### Dynamic State Management

```html
<wa-checkbox id="dynamicCheckbox">Dynamic checkbox</wa-checkbox>
<br><br>
<wa-button id="toggleBtn">Toggle Checked</wa-button>
<wa-button id="indeterminateBtn">Set Indeterminate</wa-button>
<wa-button id="disableBtn">Toggle Disabled</wa-button>

<script>
  const checkbox = document.getElementById('dynamicCheckbox');
  const toggleBtn = document.getElementById('toggleBtn');
  const indeterminateBtn = document.getElementById('indeterminateBtn');
  const disableBtn = document.getElementById('disableBtn');

  toggleBtn.addEventListener('click', () => {
    checkbox.checked = !checkbox.checked;
  });

  indeterminateBtn.addEventListener('click', () => {
    checkbox.indeterminate = !checkbox.indeterminate;
  });

  disableBtn.addEventListener('click', () => {
    checkbox.disabled = !checkbox.disabled;
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `click()` | Simulates a click on the checkbox | `void` |
| `focus(options?)` | Sets focus on the checkbox | `void` |
| `blur()` | Removes focus from the checkbox | `void` |
| `checkValidity()` | Checks if the checkbox is valid according to validation rules | `boolean` |

### Method Examples

```javascript
const checkbox = document.querySelector('wa-checkbox');

// Programmatically click the checkbox
checkbox.click();

// Focus the checkbox
checkbox.focus();

// Focus with options
checkbox.focus({ preventScroll: true });

// Remove focus
checkbox.blur();

// Check validity
if (checkbox.checkValidity()) {
  console.log('Checkbox is valid');
} else {
  console.log('Checkbox validation failed');
}
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the checkbox's checked state changes | `{ checked: boolean }` |
| `wa-focus` | Emitted when the checkbox gains focus | - |
| `wa-blur` | Emitted when the checkbox loses focus | - |

### Event Examples

```javascript
const checkbox = document.querySelector('wa-checkbox');

// Listen for checked state changes
checkbox.addEventListener('wa-change', (event) => {
  console.log('Checkbox changed:', event.target.checked);
});

// Listen for focus events
checkbox.addEventListener('wa-focus', () => {
  console.log('Checkbox focused');
});

// Listen for blur events
checkbox.addEventListener('wa-blur', () => {
  console.log('Checkbox blurred');
});
```

### Form Validation Example

```javascript
const form = document.querySelector('form');
const checkbox = form.querySelector('wa-checkbox[required]');

form.addEventListener('submit', (event) => {
  event.preventDefault();

  if (!checkbox.checkValidity()) {
    console.error('Checkbox is required');
    checkbox.focus();
    return;
  }

  console.log('Form is valid');
});

checkbox.addEventListener('wa-change', (event) => {
  if (event.target.checked) {
    console.log('Required checkbox is now checked');
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The checkbox label |

## CSS Parts

Use CSS parts to style internal checkbox elements:

```css
/* Style the base container */
wa-checkbox::part(base) {
  gap: 0.75rem;
}

/* Style the checkbox control */
wa-checkbox::part(control) {
  border-radius: 0.25rem;
  border-width: 2px;
}

/* Style the checked icon */
wa-checkbox::part(checked-icon) {
  color: white;
}

/* Style the label */
wa-checkbox::part(label) {
  font-weight: 500;
}
```

## Customization

### Custom Colors

```css
/* Custom checkbox colors */
wa-checkbox::part(control) {
  border-color: #6366f1;
}

wa-checkbox[checked]::part(control) {
  background-color: #6366f1;
  border-color: #6366f1;
}

wa-checkbox[indeterminate]::part(control) {
  background-color: #6366f1;
  border-color: #6366f1;
}
```

### Custom Sizes

```css
/* Extra large checkbox */
wa-checkbox.xl::part(control) {
  width: 1.5rem;
  height: 1.5rem;
}

wa-checkbox.xl::part(label) {
  font-size: 1.125rem;
}
```

### Custom Styling

```css
/* Rounded checkbox */
wa-checkbox.rounded::part(control) {
  border-radius: 50%;
}

/* Bold label */
wa-checkbox.bold::part(label) {
  font-weight: 700;
}
```

## Best Practices

- ✅ Use clear, concise labels that describe what the checkbox controls
- ✅ Group related checkboxes together logically
- ✅ Use indeterminate state for parent checkboxes in hierarchical selections
- ✅ Mark required checkboxes clearly with `required` attribute and visual indicators
- ✅ Provide immediate feedback when checkbox state changes
- ❌ Don't use checkboxes for mutually exclusive options (use radio buttons instead)
- ❌ Avoid using too many checkboxes in a single group (consider alternative UI patterns)
- ❌ Don't nest interactive elements inside checkbox labels
- ❌ Don't rely solely on color to indicate state

## Accessibility

- Checkboxes automatically include appropriate ARIA roles and states
- The `checked`, `indeterminate`, and `disabled` states are properly communicated to screen readers
- Checkboxes are keyboard accessible:
  - `Tab` - Move focus to/from the checkbox
  - `Space` - Toggle the checked state
- Use descriptive labels for screen readers:

```html
<!-- Good: Clear, descriptive label -->
<wa-checkbox>Enable email notifications</wa-checkbox>

<!-- Good: Using aria-label when no visible label -->
<wa-checkbox aria-label="Accept terms and conditions"></wa-checkbox>
```

- Required checkboxes are announced to screen readers
- Disabled checkboxes are automatically excluded from tab order
- Indeterminate state is announced as "mixed" to screen readers

## Troubleshooting

### Checkbox Not Changing State

**Problem:** Checkbox doesn't toggle when clicked

**Solution:** Check if checkbox is disabled

```javascript
checkbox.disabled = false;
```

### Form Not Validating Required Checkbox

**Problem:** Form submits even when required checkbox is unchecked

**Solution:** Ensure you're checking validity before submission

```javascript
form.addEventListener('submit', (event) => {
  event.preventDefault();

  const checkbox = form.querySelector('wa-checkbox[required]');
  if (!checkbox.checkValidity()) {
    console.error('Required checkbox must be checked');
    return;
  }

  // Submit form
});
```

### Indeterminate State Not Showing

**Problem:** Setting `indeterminate` attribute in HTML doesn't work

**Solution:** The indeterminate state can only be set via JavaScript

```javascript
// ✅ Correct
const checkbox = document.querySelector('wa-checkbox');
checkbox.indeterminate = true;

// ❌ Won't work
// <wa-checkbox indeterminate>Label</wa-checkbox>
```

### Change Event Not Firing

**Problem:** `wa-change` event doesn't fire

**Solution:** Ensure you're using the correct event name and the checkbox isn't disabled

```javascript
// ✅ Correct - WebAwesome event
checkbox.addEventListener('wa-change', (event) => {
  console.log(event.target.checked);
});

// ❌ Standard change event may not work
// checkbox.addEventListener('change', ...);
```

## Related

- [Radio Button](./radio.md)
- [Switch](./switch.md)
- [Form Controls Guide](../guides/form-controls.md)
- [Checkbox Group](./checkbox-group.md)
