# Form Controls

WebAwesome form controls with built-in validation, form association, and seamless integration with native HTML forms.

## Overview

WebAwesome form controls are form-associated custom elements that integrate seamlessly with native HTML forms. They provide comprehensive support for:

1. **Form submission** - Submit with forms like native controls, participating in FormData
2. **Constraint validation** - Browser's built-in client-side validation with standard HTML attributes
3. **Form association** - Full participation in form lifecycle events (reset, submit, validation)

All form controls (`wa-input`, `wa-select`, `wa-textarea`, etc.) work with native form APIs, support standard validation attributes, and maintain consistent validation states across your application.

## Constraint Validation

WebAwesome form controls support the browser's built-in Constraint Validation API, enabling client-side validation without custom JavaScript.

### Validation Attributes

Standard HTML validation attributes work seamlessly with WebAwesome form controls:

```html
<!-- Required fields -->
<wa-input required></wa-input>

<!-- Pattern validation -->
<wa-input pattern="[A-Za-z]+" title="Letters only"></wa-input>

<!-- Length constraints -->
<wa-input minlength="3" maxlength="50"></wa-input>

<!-- Number constraints -->
<wa-input type="number" min="0" max="100" step="5"></wa-input>

<!-- Email validation -->
<wa-input type="email"></wa-input>

<!-- URL validation -->
<wa-input type="url"></wa-input>
```

### Disabling Validation

Use the `novalidate` attribute to suppress validation on form submission:

```html
<!-- Suppress validation on entire form -->
<form novalidate>
  <wa-input required></wa-input>
  <!-- Will not validate on submit -->
</form>
```

### Validation API

WebAwesome form controls support the standard Constraint Validation API:

```javascript
// Set custom validation message
input.setCustomValidity('This field must contain "webawesome"');

// Clear custom validation
input.setCustomValidity('');

// Check validity
if (input.checkValidity()) {
  // Valid
}

// Get validation message
console.log(input.validationMessage);
```

## Required Fields

Mark form controls as required to prevent form submission when empty.

### Required Attribute

```html
<wa-input label="Name" required></wa-input>
<wa-select label="Country" required>
  <wa-option value="us">United States</wa-option>
</wa-select>
<wa-textarea label="Comment" required></wa-textarea>
```

**Behavior:**
- Automatically adds asterisk (*) after label
- Prevents form submission if empty
- Triggers validation styling when invalid

### Custom Required Indicator

Customize the required field indicator using CSS custom properties:

```css
/* Customize required indicator */
:root {
  --wa-form-control-required-content: '•'; /* Bullet instead of asterisk */
  --wa-form-control-required-content-color: var(--wa-color-danger-border-loud);
}
```

## Input Patterns

Use pattern validation for custom format requirements with regular expressions.

### Pattern Validation

```html
<!-- Letters only -->
<wa-input
  label="Letters Only"
  pattern="[A-Za-z]+"
  title="Only letters are allowed">
</wa-input>

<!-- Phone number format -->
<wa-input
  label="Phone"
  pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
  placeholder="123-456-7890"
  title="Format: 123-456-7890">
</wa-input>

<!-- Alphanumeric with specific length -->
<wa-input
  label="Product Code"
  pattern="[A-Z0-9]{6}"
  title="6 uppercase letters or numbers">
</wa-input>
```

**Best practices:**
- Always provide a `title` attribute with clear format instructions
- Use `placeholder` to show format examples
- Test patterns thoroughly for edge cases

## Input Types

Different input types provide automatic validation based on expected data format.

### Type-based Validation

```html
<!-- Email validation -->
<wa-input type="email" label="Email Address"></wa-input>

<!-- URL validation -->
<wa-input type="url" label="Website URL"></wa-input>

<!-- Number validation -->
<wa-input type="number" label="Age" min="18" max="100"></wa-input>

<!-- Date validation -->
<wa-input type="date" label="Birth Date"></wa-input>

<!-- Password -->
<wa-input type="password" label="Password" minlength="8"></wa-input>
```

Each type enforces specific validation rules:
- `email` - Valid email format
- `url` - Valid URL with protocol
- `number` - Numeric values with optional min/max/step
- `date` - Valid date format
- `password` - No automatic validation, combine with `minlength`

## Custom Error Messages

Implement custom validation logic beyond standard HTML attributes.

### JavaScript Validation

```javascript
const input = document.querySelector('wa-input');

// Custom validation logic
input.addEventListener('wa-input', () => {
  const value = input.value.toLowerCase();

  if (value && !value.includes('webawesome')) {
    input.setCustomValidity('Value must contain "webawesome"');
  } else {
    input.setCustomValidity(''); // Clear custom error
  }
});

// Form submission validation
form.addEventListener('submit', (e) => {
  const isValid = form.checkValidity();
  if (!isValid) {
    e.preventDefault();
    // Handle validation errors
  }
});
```

### Real-time Validation

Validate inputs during user interaction for immediate feedback:

```javascript
// Validate on blur
input.addEventListener('wa-blur', () => {
  if (!input.checkValidity()) {
    // Show error state
    input.setAttribute('data-invalid', '');
  } else {
    input.removeAttribute('data-invalid');
  }
});
```

## Validation States

WebAwesome automatically manages validation state attributes for styling and accessibility.

### State Attributes

These attributes are applied automatically based on validation state:

```html
<!-- Applied automatically based on validation -->
<wa-input required></wa-input>     <!-- Has 'required' attribute -->
<wa-input optional></wa-input>     <!-- Has 'optional' attribute -->
<wa-input invalid></wa-input>      <!-- Has 'invalid' when validation fails -->
<wa-input valid></wa-input>        <!-- Has 'valid' when validation passes -->
<wa-input user-invalid></wa-input> <!-- Has 'user-invalid' after user interaction -->
<wa-input user-valid></wa-input>   <!-- Has 'user-valid' after user interaction -->
```

### Styling Validation States

Use attribute selectors to style controls based on validation state:

```css
/* Style invalid controls */
wa-input[invalid] {
  --border-color: var(--wa-color-danger-border-loud);
}

/* Style valid controls after user interaction */
wa-input[user-valid] {
  --border-color: var(--wa-color-success-border-loud);
}

/* Style required controls */
wa-input[required] {
  --label-color: var(--wa-color-text-normal);
}

/* Style invalid controls that user has interacted with */
wa-input[user-invalid] {
  --border-color: var(--wa-color-danger-border-loud);
  box-shadow: 0 0 0 1px var(--wa-color-danger-border-quiet);
}
```

### Pseudo-class Mapping

WebAwesome attributes map to standard CSS pseudo-classes:

| Attribute | Pseudo-class | Description |
|-----------|-------------|-------------|
| `required` | `:required` | Field is required |
| `optional` | `:optional` | Field is optional |
| `invalid` | `:invalid` | Field is currently invalid |
| `valid` | `:valid` | Field is currently valid |
| `user-invalid` | `:user-invalid` | Invalid after user interaction |
| `user-valid` | `:user-valid` | Valid after user interaction |

## Form Integration

WebAwesome form controls integrate seamlessly with native HTML forms.

### Form Association

Form controls automatically associate with their containing form:

```html
<form id="user-form">
  <wa-input name="username" label="Username" required></wa-input>
  <wa-input name="email" type="email" label="Email" required></wa-input>

  <!-- Controls participate in form submission -->
  <wa-button type="submit">Submit</wa-button>
</form>
```

**Requirements:**
- Each form control needs a `name` attribute to be included in form data
- Controls must be inside a `<form>` element or use the `form` attribute

### Form Data Access

Access form data using standard FormData and validation APIs:

```javascript
// Get form data
const formData = new FormData(form);
console.log(formData.get('username'));

// Validate entire form
const isValid = form.checkValidity();

// Report validity (shows browser validation UI)
form.reportValidity();
```

## Examples

### Complete Registration Form

```html
<form id="registration-form">
  <wa-input
    name="username"
    label="Username"
    required
    minlength="3"
    pattern="[A-Za-z0-9_]+"
    title="Alphanumeric characters and underscores only">
  </wa-input>

  <wa-input
    name="email"
    type="email"
    label="Email Address"
    required>
  </wa-input>

  <wa-input
    name="password"
    type="password"
    label="Password"
    required
    minlength="8">
  </wa-input>

  <wa-select name="country" label="Country" required>
    <wa-option value="">Select a country</wa-option>
    <wa-option value="us">United States</wa-option>
    <wa-option value="uk">United Kingdom</wa-option>
    <wa-option value="ca">Canada</wa-option>
  </wa-select>

  <wa-textarea
    name="bio"
    label="Bio"
    maxlength="500"
    help-text="Tell us about yourself (optional)">
  </wa-textarea>

  <wa-button type="submit">Register</wa-button>
</form>

<script>
  const form = document.getElementById('registration-form');

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    if (!form.checkValidity()) {
      form.reportValidity();
      return;
    }

    const formData = new FormData(form);
    console.log('Form data:', Object.fromEntries(formData));

    // Submit to server
  });
</script>
```

### Contact Form with Custom Validation

```html
<form id="contact-form">
  <wa-input
    name="name"
    label="Full Name"
    required>
  </wa-input>

  <wa-input
    name="email"
    type="email"
    label="Email"
    required>
  </wa-input>

  <wa-input
    name="phone"
    label="Phone Number"
    pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
    placeholder="123-456-7890"
    title="Format: 123-456-7890">
  </wa-input>

  <wa-textarea
    name="message"
    label="Message"
    required
    minlength="10"
    help-text="Please provide at least 10 characters">
  </wa-textarea>

  <wa-button type="submit">Send Message</wa-button>
</form>

<style>
  wa-input[user-invalid],
  wa-textarea[user-invalid] {
    --border-color: var(--wa-color-danger-border-loud);
  }

  wa-input[user-valid],
  wa-textarea[user-valid] {
    --border-color: var(--wa-color-success-border-loud);
  }
</style>

<script>
  const form = document.getElementById('contact-form');
  const inputs = form.querySelectorAll('wa-input, wa-textarea');

  // Real-time validation on blur
  inputs.forEach(input => {
    input.addEventListener('wa-blur', () => {
      input.checkValidity();
    });
  });

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    if (!form.checkValidity()) {
      form.reportValidity();
      return;
    }

    // Submit form
    console.log('Form submitted successfully');
  });
</script>
```

### Advanced Validation with Custom Logic

```html
<form id="advanced-form">
  <wa-input
    id="password"
    name="password"
    type="password"
    label="Password"
    required
    minlength="8">
  </wa-input>

  <wa-input
    id="confirm-password"
    name="confirm_password"
    type="password"
    label="Confirm Password"
    required>
  </wa-input>

  <wa-input
    id="promo-code"
    name="promo_code"
    label="Promo Code"
    help-text="Must contain 'SAVE' or 'DISCOUNT'">
  </wa-input>

  <wa-button type="submit">Submit</wa-button>
</form>

<script>
  const password = document.getElementById('password');
  const confirmPassword = document.getElementById('confirm-password');
  const promoCode = document.getElementById('promo-code');

  // Password match validation
  confirmPassword.addEventListener('wa-input', () => {
    if (password.value !== confirmPassword.value) {
      confirmPassword.setCustomValidity('Passwords do not match');
    } else {
      confirmPassword.setCustomValidity('');
    }
  });

  // Update when password changes
  password.addEventListener('wa-input', () => {
    if (confirmPassword.value) {
      confirmPassword.dispatchEvent(new Event('wa-input'));
    }
  });

  // Custom promo code validation
  promoCode.addEventListener('wa-input', () => {
    const value = promoCode.value.toUpperCase();
    if (value && !value.includes('SAVE') && !value.includes('DISCOUNT')) {
      promoCode.setCustomValidity('Promo code must contain "SAVE" or "DISCOUNT"');
    } else {
      promoCode.setCustomValidity('');
    }
  });
</script>
```

## Best Practices

### Validation Strategy

1. **Use appropriate input types** - Leverage built-in browser validation for common formats (email, url, number)
2. **Combine multiple validation methods** - Use `required`, `pattern`, `min/max`, and custom validation together
3. **Provide clear error messages** - Use `title` attributes for patterns and `setCustomValidity()` for custom messages
4. **Style validation states** - Give immediate visual feedback using validation state attributes

### User Experience

1. **Validate on blur** - Don't overwhelm users by validating on every keystroke
2. **Show success states** - Indicate when fields are valid to build user confidence
3. **Provide helpful error messages** - Include guidance on how to correct errors
4. **Use progressive validation** - Don't show all errors at once; reveal them as users interact
5. **Maintain context** - Keep focus on the invalid field when validation fails

### Accessibility

1. **Associate labels properly** - Always use the `label` attribute or associate labels with IDs
2. **Use validation messages** - Ensure screen readers announce validation errors
3. **Maintain focus management** - Don't trap or lose focus during validation
4. **Provide multiple cues** - Don't rely solely on color; use icons, text, and borders
5. **Test with assistive technology** - Verify validation works with screen readers

### Common Validation Patterns

```css
/* Complete validation styling system */
wa-input[required]:not([value]) {
  /* Style empty required fields */
}

wa-input[user-invalid] {
  --border-color: var(--wa-color-danger-border-loud);
}

wa-input[user-valid] {
  --border-color: var(--wa-color-success-border-loud);
}

wa-input[invalid]:focus {
  outline-color: var(--wa-color-danger-border-loud);
}
```

## Related

- [Input Component](../components/input.md)
- [Select Component](../components/select.md)
- [Textarea Component](../components/textarea.md)
- [Button Component](../components/button.md)
- [Accessibility Guide](./accessibility.md)
