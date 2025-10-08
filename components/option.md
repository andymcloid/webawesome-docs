# Option

An option element for use within select components.

## Overview

The `<wa-option>` component represents a single selectable option within a `<wa-select>` dropdown. Options can be enabled or disabled and carry values that are submitted with forms.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/option/option.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Options within a select -->
<wa-select label="Choose a color">
  <wa-option value="red">Red</wa-option>
  <wa-option value="green">Green</wa-option>
  <wa-option value="blue">Blue</wa-option>
</wa-select>

<!-- Disabled option -->
<wa-select label="Choose a size">
  <wa-option value="small">Small</wa-option>
  <wa-option value="medium">Medium</wa-option>
  <wa-option value="large" disabled>Large (Out of Stock)</wa-option>
</wa-select>
```

## Option Values

### Simple Text Options

```html
<wa-select label="Select a fruit">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
  <wa-option value="grape">Grape</wa-option>
</wa-select>
```

### Options with Different Display Text

```html
<wa-select label="Select country">
  <wa-option value="us">United States</wa-option>
  <wa-option value="uk">United Kingdom</wa-option>
  <wa-option value="ca">Canada</wa-option>
  <wa-option value="au">Australia</wa-option>
</wa-select>
```

### Numeric Values

```html
<wa-select label="Select quantity">
  <wa-option value="1">1 item</wa-option>
  <wa-option value="5">5 items</wa-option>
  <wa-option value="10">10 items</wa-option>
  <wa-option value="25">25 items</wa-option>
</wa-select>
```

## Disabled Options

```html
<wa-select label="Choose a plan">
  <wa-option value="free">Free Plan</wa-option>
  <wa-option value="starter">Starter Plan - $9/mo</wa-option>
  <wa-option value="pro" disabled>Pro Plan - Coming Soon</wa-option>
  <wa-option value="enterprise" disabled>Enterprise - Contact Sales</wa-option>
</wa-select>
```

## Options with Icons

```html
<wa-select label="Select payment method">
  <wa-option value="credit">
    <wa-icon slot="prefix" name="credit-card"></wa-icon>
    Credit Card
  </wa-option>
  <wa-option value="paypal">
    <wa-icon slot="prefix" name="paypal"></wa-icon>
    PayPal
  </wa-option>
  <wa-option value="bank">
    <wa-icon slot="prefix" name="bank"></wa-icon>
    Bank Transfer
  </wa-option>
</wa-select>
```

## Grouped Options

```html
<wa-select label="Choose location">
  <wa-option value="us-ny">New York, USA</wa-option>
  <wa-option value="us-ca">California, USA</wa-option>
  <wa-option value="uk-london">London, UK</wa-option>
  <wa-option value="uk-manchester">Manchester, UK</wa-option>
  <wa-option value="ca-toronto">Toronto, Canada</wa-option>
  <wa-option value="ca-vancouver">Vancouver, Canada</wa-option>
</wa-select>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | `''` | No | The option's value (submitted with forms) |
| `disabled` | boolean | `false` | No | Disables the option, making it unselectable |

### Properties

```javascript
const option = document.querySelector('wa-option');

// Get the option's value
console.log(option.value); // 'red'

// Set the value
option.value = 'blue';

// Check if disabled
console.log(option.disabled); // false

// Disable the option
option.disabled = true;

// Check if selected (read-only)
console.log(option.selected); // false
```

## Examples

### Dynamic Option Creation

```html
<wa-select id="categorySelect" label="Select category"></wa-select>

<script>
  const categories = [
    { value: 'electronics', label: 'Electronics' },
    { value: 'clothing', label: 'Clothing' },
    { value: 'books', label: 'Books' },
    { value: 'toys', label: 'Toys' }
  ];

  const select = document.getElementById('categorySelect');

  categories.forEach(category => {
    const option = document.createElement('wa-option');
    option.value = category.value;
    option.textContent = category.label;
    select.appendChild(option);
  });
</script>
```

### Loading Options from API

```html
<wa-select id="userSelect" label="Assign to user">
  <wa-option value="">Loading users...</wa-option>
</wa-select>

<script>
  const select = document.getElementById('userSelect');

  async function loadUsers() {
    try {
      const response = await fetch('/api/users');
      const users = await response.json();

      // Clear loading option
      select.innerHTML = '';

      // Add placeholder
      const placeholder = document.createElement('wa-option');
      placeholder.value = '';
      placeholder.textContent = 'Select a user...';
      placeholder.disabled = true;
      select.appendChild(placeholder);

      // Add user options
      users.forEach(user => {
        const option = document.createElement('wa-option');
        option.value = user.id;
        option.textContent = `${user.name} (${user.email})`;
        select.appendChild(option);
      });
    } catch (error) {
      console.error('Failed to load users:', error);
    }
  }

  loadUsers();
</script>
```

### Conditional Option Disabling

```html
<wa-select id="sizeSelect" label="Select size">
  <wa-option value="xs">Extra Small</wa-option>
  <wa-option value="s">Small</wa-option>
  <wa-option value="m">Medium</wa-option>
  <wa-option value="l">Large</wa-option>
  <wa-option value="xl">Extra Large</wa-option>
</wa-select>

<script>
  const outOfStock = ['xs', 'xl'];
  const select = document.getElementById('sizeSelect');
  const options = select.querySelectorAll('wa-option');

  options.forEach(option => {
    if (outOfStock.includes(option.value)) {
      option.disabled = true;
      option.textContent += ' - Out of Stock';
    }
  });
</script>
```

### Multi-Select Options

```html
<wa-select label="Select toppings" multiple>
  <wa-option value="cheese">Cheese</wa-option>
  <wa-option value="pepperoni">Pepperoni</wa-option>
  <wa-option value="mushrooms">Mushrooms</wa-option>
  <wa-option value="onions">Onions</wa-option>
  <wa-option value="peppers">Peppers</wa-option>
  <wa-option value="olives">Olives</wa-option>
</wa-select>
```

### Options with Additional Info

```html
<wa-select label="Select plan">
  <wa-option value="basic">
    <div>
      <strong>Basic Plan</strong>
      <div style="font-size: 0.875rem; opacity: 0.7;">
        Up to 5 users
      </div>
    </div>
  </wa-option>
  <wa-option value="pro">
    <div>
      <strong>Pro Plan</strong>
      <div style="font-size: 0.875rem; opacity: 0.7;">
        Up to 25 users
      </div>
    </div>
  </wa-option>
  <wa-option value="enterprise">
    <div>
      <strong>Enterprise Plan</strong>
      <div style="font-size: 0.875rem; opacity: 0.7;">
        Unlimited users
      </div>
    </div>
  </wa-option>
</wa-select>
```

### Form Integration

```html
<form id="orderForm">
  <wa-select name="product" label="Select product" required>
    <wa-option value="">Choose a product...</wa-option>
    <wa-option value="laptop">Laptop - $999</wa-option>
    <wa-option value="phone">Phone - $699</wa-option>
    <wa-option value="tablet">Tablet - $499</wa-option>
  </wa-select>

  <wa-select name="quantity" label="Quantity" required>
    <wa-option value="1">1</wa-option>
    <wa-option value="2">2</wa-option>
    <wa-option value="3">3</wa-option>
    <wa-option value="5">5</wa-option>
  </wa-select>

  <wa-button type="submit" variant="primary">Place Order</wa-button>
</form>

<script>
  document.getElementById('orderForm').addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    console.log({
      product: formData.get('product'),
      quantity: formData.get('quantity')
    });
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the option | `void` |
| `blur()` | Removes focus from the option | `void` |

### Method Examples

```javascript
const option = document.querySelector('wa-option');

// Focus the option
option.focus();

// Remove focus
option.blur();
```

## Events

Options don't emit their own events but participate in select events:

- Selecting an option triggers `wa-change` on the parent `<wa-select>`
- Hovering an option triggers `wa-focus` on the parent `<wa-select>`

### Event Examples

```javascript
const select = document.querySelector('wa-select');

// Listen for selection changes
select.addEventListener('wa-change', (event) => {
  const selectedOption = select.querySelector('wa-option[value="' + select.value + '"]');
  console.log('Selected:', selectedOption.textContent);
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The option's label/display text |
| `prefix` | Content to display before the label (typically icons) |
| `suffix` | Content to display after the label |

### Slot Examples

```html
<!-- With prefix icon -->
<wa-option value="home">
  <wa-icon slot="prefix" name="house"></wa-icon>
  Home
</wa-option>

<!-- With suffix badge -->
<wa-option value="premium">
  Premium
  <wa-badge slot="suffix" variant="primary">New</wa-badge>
</wa-option>

<!-- With both -->
<wa-option value="featured">
  <wa-icon slot="prefix" name="star"></wa-icon>
  Featured Item
  <wa-badge slot="suffix" variant="warning">Hot</wa-badge>
</wa-option>
```

## CSS Parts

Use CSS parts to style internal option elements:

```css
/* Style the base option */
wa-option::part(base) {
  padding: 0.75rem;
}

/* Style when option is checked */
wa-option::part(checked-icon) {
  color: #16a34a;
}

/* Style the label */
wa-option::part(label) {
  font-weight: 500;
}

/* Style the prefix container */
wa-option::part(prefix) {
  margin-right: 0.75rem;
}

/* Style the suffix container */
wa-option::part(suffix) {
  margin-left: 0.75rem;
}
```

## Customization

### Custom Option Colors

```css
/* Highlighted option */
wa-option.highlighted::part(base) {
  background-color: #fef3c7;
  border-left: 3px solid #f59e0b;
}

/* Danger option */
wa-option.danger::part(base) {
  color: #dc2626;
}

wa-option.danger::part(base):hover {
  background-color: #fee2e2;
}
```

### Custom Disabled Style

```css
/* Custom disabled appearance */
wa-option[disabled]::part(base) {
  opacity: 0.4;
  text-decoration: line-through;
}
```

### Custom Spacing

```css
/* Compact options */
wa-option.compact::part(base) {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
}

/* Spacious options */
wa-option.spacious::part(base) {
  padding: 1rem 1.5rem;
}
```

## Best Practices

- ✅ Always provide a value attribute for each option
- ✅ Use clear, descriptive option labels
- ✅ Consider adding a placeholder option for required selects
- ✅ Disable options that are temporarily unavailable rather than removing them
- ✅ Use icons to enhance visual clarity when appropriate
- ❌ Don't use overly long option text
- ❌ Avoid duplicate values within the same select
- ❌ Don't forget to handle the case where no option is selected

## Accessibility

- Options are automatically associated with their parent select
- Disabled options are excluded from keyboard navigation
- Screen readers announce option text and state
- Arrow keys navigate through enabled options

```html
<!-- Accessible options with clear labels -->
<wa-select label="Select your country" required>
  <wa-option value="">Please select a country</wa-option>
  <wa-option value="us">United States of America</wa-option>
  <wa-option value="uk">United Kingdom</wa-option>
  <wa-option value="ca">Canada</wa-option>
</wa-select>
```

## Troubleshooting

### Option Not Selectable

**Problem:** Clicking an option doesn't select it

**Solution:** Check if the option is disabled or if the parent select is disabled

```javascript
const option = document.querySelector('wa-option[value="test"]');
const select = option.closest('wa-select');

console.log('Option disabled:', option.disabled);
console.log('Select disabled:', select.disabled);
```

### Value Not Submitting in Form

**Problem:** Option value isn't included in form submission

**Solution:** Ensure the parent `<wa-select>` has a `name` attribute

```html
<!-- ✅ Correct - select has name attribute -->
<wa-select name="color" label="Color">
  <wa-option value="red">Red</wa-option>
</wa-select>

<!-- ❌ Wrong - missing name attribute -->
<wa-select label="Color">
  <wa-option value="red">Red</wa-option>
</wa-select>
```

### Option Display Issues

**Problem:** Option content not displaying correctly

**Solution:** Ensure content is properly placed in slots

```html
<!-- ✅ Correct - icon in prefix slot -->
<wa-option value="home">
  <wa-icon slot="prefix" name="house"></wa-icon>
  Home
</wa-option>

<!-- ❌ Wrong - icon not in slot -->
<wa-option value="home">
  <wa-icon name="house"></wa-icon>
  Home
</wa-option>
```

## Related

- [Select](./select.md)
- [Icon](./icon.md)
- [Badge](./badge.md)
- [Form Controls Guide](../guides/form-controls.md)
