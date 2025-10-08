# Input

Text input field for collecting user input with validation support.

## Overview

The `<wa-input>` component provides a text input field with support for various input types, validation, help text, and more. It's fully customizable and integrates seamlessly with HTML forms.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/input/input.js';
```

## Basic Usage

```html
<!-- Basic input -->
<wa-input></wa-input>

<!-- With label -->
<wa-input label="Name"></wa-input>

<!-- With placeholder -->
<wa-input label="Email" placeholder="Enter your email"></wa-input>

<!-- With help text -->
<wa-input label="Username" help-text="Choose a unique username"></wa-input>
```

## Input Types

Support for all standard HTML input types:

```html
<wa-input type="text" label="Text"></wa-input>
<wa-input type="email" label="Email"></wa-input>
<wa-input type="password" label="Password"></wa-input>
<wa-input type="number" label="Age"></wa-input>
<wa-input type="tel" label="Phone"></wa-input>
<wa-input type="url" label="Website"></wa-input>
<wa-input type="search" label="Search"></wa-input>
<wa-input type="date" label="Birth Date"></wa-input>
```

## Sizes

```html
<wa-input size="small" label="Small"></wa-input>
<wa-input size="medium" label="Medium (default)"></wa-input>
<wa-input size="large" label="Large"></wa-input>
```

## States

### Disabled

```html
<wa-input label="Disabled" disabled></wa-input>
```

### Readonly

```html
<wa-input label="Readonly" value="Cannot edit" readonly></wa-input>
```

### Required

```html
<wa-input label="Email" type="email" required></wa-input>
```

### With Value

```html
<wa-input label="Name" value="John Doe"></wa-input>
```

## Icons and Buttons

### Prefix and Suffix

```html
<!-- With prefix icon -->
<wa-input label="Email">
  <wa-icon slot="prefix" name="envelope"></wa-icon>
</wa-input>

<!-- With suffix icon -->
<wa-input label="Search">
  <wa-icon slot="suffix" name="search"></wa-icon>
</wa-input>

<!-- With both -->
<wa-input label="Amount" type="number">
  <span slot="prefix">$</span>
  <span slot="suffix">USD</span>
</wa-input>
```

### Clear Button

```html
<wa-input label="Email" clearable></wa-input>
```

### Password Toggle

```html
<wa-input type="password" label="Password" password-toggle></wa-input>
```

## Validation

### Required Fields

```html
<form>
  <wa-input label="Name" name="name" required></wa-input>
  <wa-button type="submit">Submit</wa-button>
</form>
```

### Pattern Validation

```html
<!-- Email validation -->
<wa-input
  label="Email"
  type="email"
  pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
  required
></wa-input>

<!-- Phone validation -->
<wa-input
  label="Phone"
  type="tel"
  pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
  placeholder="123-456-7890"
></wa-input>
```

### Min/Max Length

```html
<wa-input
  label="Username"
  minlength="3"
  maxlength="20"
  help-text="3-20 characters"
></wa-input>
```

### Custom Validation

```html
<wa-input id="customInput" label="Custom Validation"></wa-input>

<script>
  const input = document.getElementById('customInput');

  input.addEventListener('wa-input', () => {
    if (input.value === 'invalid') {
      input.setCustomValidity('This value is not allowed');
    } else {
      input.setCustomValidity('');
    }
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `type` | string | `'text'` | No | Input type (text, email, password, number, etc.) |
| `size` | string | `'medium'` | No | Input size: `small`, `medium`, `large` |
| `label` | string | - | No | Label text |
| `placeholder` | string | - | No | Placeholder text |
| `value` | string | - | No | Input value |
| `defaultValue` | string | - | No | Default value |
| `helpText` | string | - | No | Help text displayed below input |
| `clearable` | boolean | `false` | No | Show clear button |
| `disabled` | boolean | `false` | No | Disable the input |
| `readonly` | boolean | `false` | No | Make input readonly |
| `required` | boolean | `false` | No | Make input required |
| `passwordToggle` | boolean | `false` | No | Show password toggle (for type="password") |
| `pattern` | string | - | No | Validation pattern (regex) |
| `minlength` | number | - | No | Minimum length |
| `maxlength` | number | - | No | Maximum length |
| `min` | number/string | - | No | Minimum value (for numbers/dates) |
| `max` | number/string | - | No | Maximum value (for numbers/dates) |
| `step` | number | - | No | Step value (for numbers) |
| `autocomplete` | string | - | No | Autocomplete attribute |
| `autocapitalize` | string | - | No | Auto-capitalize attribute |
| `autocorrect` | string | - | No | Auto-correct attribute |
| `spellcheck` | boolean | - | No | Spellcheck attribute |
| `inputmode` | string | - | No | Input mode attribute |
| `name` | string | - | No | Form field name |

## Examples

### Login Form

```html
<form id="loginForm">
  <wa-input
    label="Email"
    type="email"
    name="email"
    required
    clearable
  >
    <wa-icon slot="prefix" name="envelope"></wa-icon>
  </wa-input>

  <wa-input
    label="Password"
    type="password"
    name="password"
    required
    password-toggle
  >
    <wa-icon slot="prefix" name="lock"></wa-icon>
  </wa-input>

  <wa-button type="submit" variant="primary">Login</wa-button>
</form>
```

### Search with Auto-Submit

```html
<wa-input
  id="search"
  type="search"
  placeholder="Search..."
  clearable
>
  <wa-icon slot="prefix" name="search"></wa-icon>
</wa-input>

<script>
  const search = document.getElementById('search');
  let debounceTimer;

  search.addEventListener('wa-input', (e) => {
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(() => {
      console.log('Searching for:', e.target.value);
      // Perform search
    }, 300);
  });
</script>
```

### Number Input with Validation

```html
<wa-input
  label="Age"
  type="number"
  min="1"
  max="120"
  step="1"
  value="25"
  help-text="Enter your age (1-120)"
></wa-input>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the input | `void` |
| `blur()` | Removes focus from the input | `void` |
| `select()` | Selects all text in the input | `void` |
| `setSelectionRange(start, end, direction?)` | Selects a range of text | `void` |
| `setRangeText(replacement, start?, end?, selectMode?)` | Replaces text in range | `void` |
| `checkValidity()` | Checks if input is valid | `boolean` |
| `reportValidity()` | Shows validation message | `boolean` |
| `setCustomValidity(message)` | Sets custom validation message | `void` |

### Method Examples

```javascript
const input = document.querySelector('wa-input');

// Focus the input
input.focus();

// Select all text
input.select();

// Select partial text
input.setSelectionRange(0, 5);

// Check validity
if (!input.checkValidity()) {
  input.reportValidity();
}

// Set custom validation
input.setCustomValidity('This value is invalid');
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-input` | Fired when input value changes | - |
| `wa-change` | Fired when value changes and input loses focus | - |
| `wa-focus` | Fired when input gains focus | - |
| `wa-blur` | Fired when input loses focus | - |
| `wa-clear` | Fired when clear button is clicked | - |

### Event Examples

```javascript
const input = document.querySelector('wa-input');

// Listen for input changes (real-time)
input.addEventListener('wa-input', (e) => {
  console.log('Current value:', e.target.value);
});

// Listen for committed changes
input.addEventListener('wa-change', (e) => {
  console.log('Final value:', e.target.value);
});

// Clear event
input.addEventListener('wa-clear', () => {
  console.log('Input cleared');
});
```

## Slots

| Slot | Description |
|------|-------------|
| `label` | Label content |
| `prefix` | Content before the input |
| `suffix` | Content after the input |
| `clear-icon` | Custom clear button icon |
| `show-password-icon` | Custom show password icon |
| `hide-password-icon` | Custom hide password icon |
| `help-text` | Custom help text |

## CSS Parts

```css
/* Style the form control wrapper */
wa-input::part(form-control) {
  /* ... */
}

/* Style the label */
wa-input::part(label) {
  font-weight: bold;
}

/* Style the input wrapper */
wa-input::part(input) {
  border-radius: 4px;
}

/* Style the base input element */
wa-input::part(base) {
  background: white;
}

/* Style the help text */
wa-input::part(help-text) {
  color: gray;
}
```

## Best Practices

- ✅ Always provide a label for accessibility
- ✅ Use appropriate input types for better mobile keyboards
- ✅ Provide clear help text for complex inputs
- ✅ Use validation to ensure data quality
- ✅ Show clear error messages
- ❌ Don't use placeholder as a label replacement
- ❌ Avoid overly restrictive validation
- ❌ Don't disable autocomplete without good reason

## Accessibility

- Always provide a `label` for screen readers
- Use `help-text` for additional instructions
- Validation messages are automatically announced
- Disabled inputs are excluded from tab order

## Related

- [Textarea](./textarea.md)
- [Select](./select.md)
- [Form Controls Guide](../guides/form-controls.md)
- [Validation Guide](../guides/validation.md)
