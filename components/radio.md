# Radio

Radio buttons allow users to select a single option from a set of mutually exclusive choices.

## Overview

The `<wa-radio>` component provides a fully accessible radio button that must be used within a `<wa-radio-group>`. Radio buttons are ideal for presenting users with 2-5 mutually exclusive options where only one selection is allowed.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/radio/radio.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-radio-group label="Choose a size" name="size" value="medium">
  <wa-radio value="small">Small</wa-radio>
  <wa-radio value="medium">Medium</wa-radio>
  <wa-radio value="large">Large</wa-radio>
</wa-radio-group>
```

## States

### Checked Radio

Use the `checked` attribute to pre-select a radio button:

```html
<wa-radio-group label="Shipping Method" name="shipping">
  <wa-radio value="standard">Standard Shipping</wa-radio>
  <wa-radio value="express" checked>Express Shipping</wa-radio>
  <wa-radio value="overnight">Overnight Shipping</wa-radio>
</wa-radio-group>
```

### Disabled Radio

Disable individual radio buttons with the `disabled` attribute:

```html
<wa-radio-group label="Select Option" name="option">
  <wa-radio value="option1">Available Option</wa-radio>
  <wa-radio value="option2" disabled>Unavailable Option</wa-radio>
  <wa-radio value="option3">Another Available Option</wa-radio>
</wa-radio-group>
```

### Disabled Group

Disable all radio buttons in a group:

```html
<wa-radio-group label="Select Option" name="option" disabled>
  <wa-radio value="option1">Option 1</wa-radio>
  <wa-radio value="option2">Option 2</wa-radio>
  <wa-radio value="option3">Option 3</wa-radio>
</wa-radio-group>
```

## Radio with Descriptions

Add descriptive text to help users make informed choices:

```html
<wa-radio-group label="Choose a plan" name="plan">
  <wa-radio value="free">
    <strong>Free</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Basic features for personal use
    </div>
  </wa-radio>

  <wa-radio value="pro">
    <strong>Pro - $9.99/month</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Advanced features for professionals
    </div>
  </wa-radio>

  <wa-radio value="enterprise">
    <strong>Enterprise - Custom pricing</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Full features with dedicated support
    </div>
  </wa-radio>
</wa-radio-group>
```

## Radio with Icons

Enhance radio buttons with icons for better visual recognition:

```html
<wa-radio-group label="Choose a theme" name="theme">
  <wa-radio value="light">
    <wa-icon name="sun" style="margin-right: 0.5rem;"></wa-icon>
    Light Theme
  </wa-radio>

  <wa-radio value="dark">
    <wa-icon name="moon" style="margin-right: 0.5rem;"></wa-icon>
    Dark Theme
  </wa-radio>

  <wa-radio value="auto">
    <wa-icon name="monitor" style="margin-right: 0.5rem;"></wa-icon>
    Auto (System)
  </wa-radio>
</wa-radio-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | - | Yes | The radio button's value |
| `checked` | boolean | `false` | No | Whether the radio is checked |
| `disabled` | boolean | `false` | No | Whether the radio is disabled |
| `name` | string | - | No | Name attribute (inherited from group) |

## Examples

### Payment Method Selection

```html
<wa-radio-group label="Payment Method" name="payment" required>
  <wa-radio value="credit">
    <wa-icon name="credit-card" style="margin-right: 0.5rem;"></wa-icon>
    Credit Card
  </wa-radio>

  <wa-radio value="paypal">
    <wa-icon name="paypal" style="margin-right: 0.5rem;"></wa-icon>
    PayPal
  </wa-radio>

  <wa-radio value="bank">
    <wa-icon name="bank" style="margin-right: 0.5rem;"></wa-icon>
    Bank Transfer
  </wa-radio>
</wa-radio-group>
```

### Notification Preferences

```html
<wa-radio-group label="Email Frequency" name="email-frequency" value="daily">
  <wa-radio value="realtime">
    <strong>Real-time</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Get notified immediately as events occur
    </div>
  </wa-radio>

  <wa-radio value="daily">
    <strong>Daily Digest</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Receive a summary once per day
    </div>
  </wa-radio>

  <wa-radio value="weekly">
    <strong>Weekly Summary</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Get a weekly roundup of activity
    </div>
  </wa-radio>

  <wa-radio value="never">
    <strong>Never</strong>
    <div style="font-size: 0.875rem; opacity: 0.7;">
      Don't send me email notifications
    </div>
  </wa-radio>
</wa-radio-group>
```

### Dynamic Radio Options

```html
<wa-radio-group id="dynamicRadios" label="Select a product" name="product">
  <wa-spinner></wa-spinner>
</wa-radio-group>

<script>
  const radioGroup = document.getElementById('dynamicRadios');

  // Fetch and populate radio options
  async function loadProducts() {
    try {
      const response = await fetch('/api/products');
      const products = await response.json();

      // Clear loading spinner
      radioGroup.innerHTML = '';

      // Add radio buttons for each product
      products.forEach(product => {
        const radio = document.createElement('wa-radio');
        radio.value = product.id;
        radio.textContent = `${product.name} - $${product.price}`;
        radioGroup.appendChild(radio);
      });
    } catch (error) {
      radioGroup.innerHTML = '<p>Error loading products</p>';
    }
  }

  loadProducts();
</script>
```

### Conditional Form Fields

```html
<form id="orderForm">
  <wa-radio-group label="Delivery Method" name="delivery" id="deliveryMethod">
    <wa-radio value="pickup">Pick Up</wa-radio>
    <wa-radio value="delivery">Home Delivery</wa-radio>
  </wa-radio-group>

  <div id="deliveryFields" style="display: none; margin-top: 1rem;">
    <wa-input label="Delivery Address" name="address" required></wa-input>
    <wa-input label="City" name="city" required></wa-input>
    <wa-input label="ZIP Code" name="zip" required></wa-input>
  </div>

  <wa-button type="submit" variant="primary">Submit Order</wa-button>
</form>

<script>
  const deliveryMethod = document.getElementById('deliveryMethod');
  const deliveryFields = document.getElementById('deliveryFields');

  deliveryMethod.addEventListener('wa-change', (event) => {
    if (event.detail.value === 'delivery') {
      deliveryFields.style.display = 'block';
    } else {
      deliveryFields.style.display = 'none';
    }
  });
</script>
```

### Programmatic Selection

```html
<wa-button-group>
  <wa-button id="selectSmall">Select Small</wa-button>
  <wa-button id="selectMedium">Select Medium</wa-button>
  <wa-button id="selectLarge">Select Large</wa-button>
</wa-button-group>

<wa-radio-group id="sizeGroup" label="Size" name="size">
  <wa-radio value="small" id="smallRadio">Small</wa-radio>
  <wa-radio value="medium" id="mediumRadio">Medium</wa-radio>
  <wa-radio value="large" id="largeRadio">Large</wa-radio>
</wa-radio-group>

<script>
  document.getElementById('selectSmall').addEventListener('click', () => {
    document.getElementById('smallRadio').checked = true;
  });

  document.getElementById('selectMedium').addEventListener('click', () => {
    document.getElementById('mediumRadio').checked = true;
  });

  document.getElementById('selectLarge').addEventListener('click', () => {
    document.getElementById('largeRadio').checked = true;
  });
</script>
```

### Radio with Validation

```html
<form id="surveyForm">
  <wa-radio-group label="How satisfied are you?" name="satisfaction" id="satisfaction" required>
    <wa-radio value="very-satisfied">Very Satisfied</wa-radio>
    <wa-radio value="satisfied">Satisfied</wa-radio>
    <wa-radio value="neutral">Neutral</wa-radio>
    <wa-radio value="dissatisfied">Dissatisfied</wa-radio>
    <wa-radio value="very-dissatisfied">Very Dissatisfied</wa-radio>
  </wa-radio-group>

  <wa-button type="submit" variant="primary">Submit Survey</wa-button>
</form>

<script>
  const form = document.getElementById('surveyForm');
  const satisfaction = document.getElementById('satisfaction');

  form.addEventListener('submit', (event) => {
    event.preventDefault();

    if (!satisfaction.value) {
      alert('Please select your satisfaction level');
      return;
    }

    console.log('Submitted:', satisfaction.value);
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the radio button | `void` |
| `blur()` | Removes focus from the radio button | `void` |

### Method Examples

```javascript
const radio = document.querySelector('wa-radio');

// Focus the radio button
radio.focus();

// Focus without scrolling
radio.focus({ preventScroll: true });

// Remove focus
radio.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-blur` | Emitted when the radio loses focus | - |
| `wa-focus` | Emitted when the radio gains focus | - |

**Note:** For change events, listen on the parent `wa-radio-group` instead.

### Event Examples

```javascript
const radio = document.querySelector('wa-radio');

// Listen for focus
radio.addEventListener('wa-focus', () => {
  console.log('Radio focused');
});

// Listen for blur
radio.addEventListener('wa-blur', () => {
  console.log('Radio blurred');
});

// Listen for changes on the group
const radioGroup = document.querySelector('wa-radio-group');
radioGroup.addEventListener('wa-change', (event) => {
  console.log('Selected value:', event.detail.value);
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The radio button label |

## CSS Parts

Use CSS parts to style internal radio elements:

```css
/* Style the base container */
wa-radio::part(base) {
  padding: 0.5rem;
  border-radius: 4px;
  transition: background-color 0.2s;
}

wa-radio::part(base):hover {
  background-color: rgba(0, 0, 0, 0.05);
}

/* Style the control (the circle) */
wa-radio::part(control) {
  width: 20px;
  height: 20px;
  border: 2px solid #999;
}

wa-radio[checked]::part(control) {
  border-color: #6366f1;
  background-color: #6366f1;
}

/* Style the control when checked */
wa-radio::part(control--checked) {
  background-color: #6366f1;
  border-color: #6366f1;
}

/* Style the label */
wa-radio::part(label) {
  margin-left: 0.5rem;
  user-select: none;
}
```

## Customization

### Custom Radio Size

```css
/* Large radio buttons */
wa-radio::part(control) {
  width: 24px;
  height: 24px;
}

wa-radio::part(label) {
  font-size: 1.125rem;
}
```

### Custom Colors

```css
/* Custom checked color */
wa-radio[checked]::part(control) {
  background-color: #10b981;
  border-color: #10b981;
}

/* Custom focus ring */
wa-radio:focus-within::part(control) {
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.2);
}
```

### Card-Style Radio Buttons

```css
wa-radio::part(base) {
  border: 2px solid #e0e0e0;
  padding: 1rem;
  border-radius: 8px;
  background-color: white;
  margin-bottom: 0.5rem;
}

wa-radio[checked]::part(base) {
  border-color: #6366f1;
  background-color: #f0f1ff;
}
```

## Best Practices

- Use 2-5 options in a radio group (use select for more options)
- Provide clear, distinct labels for each option
- Use radio groups for mutually exclusive choices
- Always include a group label that describes the choice
- Pre-select a sensible default option when appropriate
- Use descriptive text for complex options
- Disable unavailable options rather than hiding them
- Consider using icons to enhance recognition
- Use consistent ordering (e.g., ascending size, price)

## Accessibility

- Radio buttons have proper ARIA roles and attributes
- Keyboard navigation with arrow keys within group
- Space key toggles selection
- Tab key moves between form fields
- Labels are properly associated with controls
- Disabled state announced to screen readers
- Group label provides context for all options
- Focus management follows best practices

### Required Radio Groups

Always provide clear indication when a selection is required:

```html
<wa-radio-group label="Select an option" name="option" required>
  <wa-radio value="option1">Option 1</wa-radio>
  <wa-radio value="option2">Option 2</wa-radio>
</wa-radio-group>
```

## Troubleshooting

### Multiple Radios Selected

**Problem:** Multiple radio buttons are checked in a group

**Solution:** Ensure all radios are within a `wa-radio-group` and have unique values

```html
<!-- Correct -->
<wa-radio-group name="option">
  <wa-radio value="a">Option A</wa-radio>
  <wa-radio value="b">Option B</wa-radio>
</wa-radio-group>

<!-- Incorrect - radios outside group -->
<wa-radio value="a" name="option">Option A</wa-radio>
<wa-radio value="b" name="option">Option B</wa-radio>
```

### Radio Not Checking

**Problem:** Clicking radio doesn't check it

**Solution:** Ensure radio has a `value` attribute and is not disabled

```html
<!-- Correct -->
<wa-radio value="option1">Option 1</wa-radio>

<!-- Incorrect - missing value -->
<wa-radio>Option 1</wa-radio>
```

### Radio Value Not Submitted

**Problem:** Radio value not included in form submission

**Solution:** Ensure radio group has a `name` attribute

```html
<!-- Correct -->
<wa-radio-group name="option">
  <wa-radio value="a">Option A</wa-radio>
</wa-radio-group>

<!-- Incorrect - missing name -->
<wa-radio-group>
  <wa-radio value="a">Option A</wa-radio>
</wa-radio-group>
```

## Related

- [Radio Group](./radio-group.md)
- [Checkbox](./checkbox.md)
- [Switch](./switch.md)
- [Select](./select.md)
- [Form Controls Guide](../guides/form-controls.md)
