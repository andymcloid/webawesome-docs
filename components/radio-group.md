# Radio Group

Radio groups organize multiple radio buttons into a single form control with a shared label and validation.

## Overview

The `<wa-radio-group>` component provides a container for `<wa-radio>` elements, ensuring that only one radio button can be selected at a time. It handles validation, labeling, and provides a consistent API for working with radio button selections.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/radio-group/radio-group.js';
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

## Labels

### Basic Label

Use the `label` attribute to provide a descriptive label:

```html
<wa-radio-group label="Select your preferred contact method" name="contact">
  <wa-radio value="email">Email</wa-radio>
  <wa-radio value="phone">Phone</wa-radio>
  <wa-radio value="sms">SMS</wa-radio>
</wa-radio-group>
```

### Required Field

Mark a radio group as required:

```html
<wa-radio-group label="Shipping Method" name="shipping" required>
  <wa-radio value="standard">Standard Shipping</wa-radio>
  <wa-radio value="express">Express Shipping</wa-radio>
  <wa-radio value="overnight">Overnight Shipping</wa-radio>
</wa-radio-group>
```

### Help Text

Provide additional context with help text:

```html
<wa-radio-group
  label="Newsletter Frequency"
  name="newsletter"
  help-text="Choose how often you'd like to receive our newsletter">
  <wa-radio value="daily">Daily</wa-radio>
  <wa-radio value="weekly">Weekly</wa-radio>
  <wa-radio value="monthly">Monthly</wa-radio>
</wa-radio-group>
```

## Default Values

Set a default selection with the `value` attribute:

```html
<wa-radio-group label="Theme Preference" name="theme" value="light">
  <wa-radio value="light">Light</wa-radio>
  <wa-radio value="dark">Dark</wa-radio>
  <wa-radio value="auto">Auto</wa-radio>
</wa-radio-group>
```

## Form Integration

### Basic Form

```html
<form id="preferencesForm">
  <wa-radio-group label="Language" name="language" value="en" required>
    <wa-radio value="en">English</wa-radio>
    <wa-radio value="es">Spanish</wa-radio>
    <wa-radio value="fr">French</wa-radio>
    <wa-radio value="de">German</wa-radio>
  </wa-radio-group>

  <wa-radio-group label="Time Zone" name="timezone" value="pst" required>
    <wa-radio value="est">Eastern (EST)</wa-radio>
    <wa-radio value="cst">Central (CST)</wa-radio>
    <wa-radio value="mst">Mountain (MST)</wa-radio>
    <wa-radio value="pst">Pacific (PST)</wa-radio>
  </wa-radio-group>

  <wa-button type="submit" variant="primary">Save Preferences</wa-button>
</form>

<script>
  const form = document.getElementById('preferencesForm');

  form.addEventListener('submit', (event) => {
    event.preventDefault();

    const formData = new FormData(form);
    const data = Object.fromEntries(formData);

    console.log('Form data:', data);
    // { language: 'en', timezone: 'pst' }
  });
</script>
```

### Form Validation

```html
<form id="surveyForm">
  <wa-radio-group
    label="Overall Satisfaction"
    name="satisfaction"
    id="satisfactionGroup"
    required>
    <wa-radio value="5">Very Satisfied</wa-radio>
    <wa-radio value="4">Satisfied</wa-radio>
    <wa-radio value="3">Neutral</wa-radio>
    <wa-radio value="2">Dissatisfied</wa-radio>
    <wa-radio value="1">Very Dissatisfied</wa-radio>
  </wa-radio-group>

  <wa-button type="submit" variant="primary">Submit Survey</wa-button>
</form>

<script>
  const form = document.getElementById('surveyForm');
  const satisfactionGroup = document.getElementById('satisfactionGroup');

  form.addEventListener('submit', (event) => {
    event.preventDefault();

    // Check if a selection was made
    if (!satisfactionGroup.value) {
      alert('Please rate your satisfaction');
      satisfactionGroup.focus();
      return;
    }

    console.log('Rating:', satisfactionGroup.value);
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `label` | string | - | No | Label text for the radio group |
| `name` | string | - | Yes | Name attribute for form submission |
| `value` | string | - | No | Currently selected value |
| `required` | boolean | `false` | No | Whether a selection is required |
| `disabled` | boolean | `false` | No | Disables all radio buttons in the group |
| `help-text` | string | - | No | Help text displayed below the group |
| `size` | string | `'medium'` | No | Size of radio buttons: `small`, `medium`, `large` |

## Examples

### Payment Method Selection

```html
<form id="checkoutForm">
  <wa-radio-group
    label="Payment Method"
    name="payment"
    value="credit"
    required>
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

  <div id="paymentDetails"></div>

  <wa-button type="submit" variant="primary">Continue to Payment</wa-button>
</form>

<script>
  const paymentGroup = document.querySelector('[name="payment"]');
  const paymentDetails = document.getElementById('paymentDetails');

  paymentGroup.addEventListener('wa-change', (event) => {
    const method = event.detail.value;

    switch (method) {
      case 'credit':
        paymentDetails.innerHTML = `
          <wa-input label="Card Number" name="card-number" required></wa-input>
          <wa-input label="Expiry Date" name="expiry" required></wa-input>
          <wa-input label="CVV" name="cvv" type="password" required></wa-input>
        `;
        break;
      case 'paypal':
        paymentDetails.innerHTML = `
          <wa-input label="PayPal Email" name="paypal-email" type="email" required></wa-input>
        `;
        break;
      case 'bank':
        paymentDetails.innerHTML = `
          <wa-input label="Account Number" name="account" required></wa-input>
          <wa-input label="Routing Number" name="routing" required></wa-input>
        `;
        break;
    }
  });

  // Trigger initial load
  paymentGroup.dispatchEvent(new CustomEvent('wa-change', {
    detail: { value: paymentGroup.value }
  }));
</script>
```

### Subscription Plans

```html
<form id="subscriptionForm">
  <wa-radio-group
    label="Choose Your Plan"
    name="plan"
    value="pro"
    help-text="You can upgrade or downgrade at any time">
    <wa-radio value="free">
      <div style="display: flex; justify-content: space-between; width: 100%;">
        <div>
          <strong>Free</strong>
          <div style="font-size: 0.875rem; opacity: 0.7;">
            Basic features • Up to 5 projects
          </div>
        </div>
        <div style="font-weight: bold;">$0/mo</div>
      </div>
    </wa-radio>

    <wa-radio value="pro">
      <div style="display: flex; justify-content: space-between; width: 100%;">
        <div>
          <strong>Pro</strong>
          <div style="font-size: 0.875rem; opacity: 0.7;">
            Advanced features • Unlimited projects
          </div>
        </div>
        <div style="font-weight: bold;">$9.99/mo</div>
      </div>
    </wa-radio>

    <wa-radio value="enterprise">
      <div style="display: flex; justify-content: space-between; width: 100%;">
        <div>
          <strong>Enterprise</strong>
          <div style="font-size: 0.875rem; opacity: 0.7;">
            Full features • Priority support • SSO
          </div>
        </div>
        <div style="font-weight: bold;">Custom</div>
      </div>
    </wa-radio>
  </wa-radio-group>

  <wa-button type="submit" variant="primary">Continue</wa-button>
</form>
```

### Dynamic Options

```html
<wa-radio-group
  id="locationGroup"
  label="Select Location"
  name="location"
  help-text="Choose your preferred store location">
  <wa-spinner></wa-spinner>
</wa-radio-group>

<script>
  const locationGroup = document.getElementById('locationGroup');

  async function loadLocations() {
    try {
      const response = await fetch('/api/locations');
      const locations = await response.json();

      // Clear loading spinner
      locationGroup.innerHTML = '';

      // Add radio for each location
      locations.forEach(location => {
        const radio = document.createElement('wa-radio');
        radio.value = location.id;
        radio.innerHTML = `
          <strong>${location.name}</strong>
          <div style="font-size: 0.875rem; opacity: 0.7;">
            ${location.address} • ${location.distance} miles away
          </div>
        `;
        locationGroup.appendChild(radio);
      });

      // Select first location by default
      if (locations.length > 0) {
        locationGroup.value = locations[0].id;
      }
    } catch (error) {
      locationGroup.innerHTML = '<p>Error loading locations</p>';
    }
  }

  loadLocations();
</script>
```

### Conditional Fields

```html
<form id="accountForm">
  <wa-radio-group
    label="Account Type"
    name="account-type"
    id="accountType"
    value="personal"
    required>
    <wa-radio value="personal">Personal Account</wa-radio>
    <wa-radio value="business">Business Account</wa-radio>
  </wa-radio-group>

  <div id="personalFields">
    <wa-input label="Full Name" name="full-name" required></wa-input>
    <wa-input label="Date of Birth" name="dob" type="date" required></wa-input>
  </div>

  <div id="businessFields" style="display: none;">
    <wa-input label="Company Name" name="company" required></wa-input>
    <wa-input label="Tax ID" name="tax-id" required></wa-input>
    <wa-input label="Business Address" name="business-address" required></wa-input>
  </div>

  <wa-button type="submit" variant="primary">Create Account</wa-button>
</form>

<script>
  const accountType = document.getElementById('accountType');
  const personalFields = document.getElementById('personalFields');
  const businessFields = document.getElementById('businessFields');

  accountType.addEventListener('wa-change', (event) => {
    if (event.detail.value === 'personal') {
      personalFields.style.display = 'block';
      businessFields.style.display = 'none';
      // Enable/disable required fields as needed
      businessFields.querySelectorAll('[required]').forEach(field => {
        field.required = false;
      });
      personalFields.querySelectorAll('wa-input').forEach(field => {
        field.required = true;
      });
    } else {
      personalFields.style.display = 'none';
      businessFields.style.display = 'block';
      personalFields.querySelectorAll('[required]').forEach(field => {
        field.required = false;
      });
      businessFields.querySelectorAll('wa-input').forEach(field => {
        field.required = true;
      });
    }
  });
</script>
```

### Radio Group with Reset

```html
<form id="filterForm">
  <wa-radio-group
    label="Filter by Status"
    name="status"
    id="statusFilter">
    <wa-radio value="all">All Items</wa-radio>
    <wa-radio value="active">Active</wa-radio>
    <wa-radio value="inactive">Inactive</wa-radio>
    <wa-radio value="pending">Pending</wa-radio>
  </wa-radio-group>

  <wa-button-group>
    <wa-button id="resetFilter">Reset Filter</wa-button>
    <wa-button type="submit" variant="primary">Apply Filter</wa-button>
  </wa-button-group>
</form>

<script>
  const form = document.getElementById('filterForm');
  const statusFilter = document.getElementById('statusFilter');
  const resetButton = document.getElementById('resetFilter');

  form.addEventListener('submit', (event) => {
    event.preventDefault();
    console.log('Filter applied:', statusFilter.value);
  });

  resetButton.addEventListener('click', () => {
    statusFilter.value = '';
    console.log('Filter reset');
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `reportValidity()` | Checks validity and shows validation message | `boolean` |
| `setCustomValidity(message)` | Sets a custom validation message | `void` |

### Method Examples

```javascript
const radioGroup = document.querySelector('wa-radio-group');

// Check if valid and show validation message
const isValid = radioGroup.reportValidity();

// Set custom validation message
radioGroup.setCustomValidity('Please select an option from the list');

// Clear custom validation
radioGroup.setCustomValidity('');
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the selected radio changes | `{ value: string }` |
| `wa-input` | Emitted when a radio is selected | `{ value: string }` |
| `wa-invalid` | Emitted when the form control fails validation | - |

### Event Examples

```javascript
const radioGroup = document.querySelector('wa-radio-group');

// Listen for value changes
radioGroup.addEventListener('wa-change', (event) => {
  console.log('Selected value:', event.detail.value);
});

// Listen for input events
radioGroup.addEventListener('wa-input', (event) => {
  console.log('Input received:', event.detail.value);
});

// Listen for validation failures
radioGroup.addEventListener('wa-invalid', () => {
  console.log('Validation failed');
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Radio buttons (wa-radio elements) |
| `label` | Custom label content |
| `help-text` | Custom help text content |

## CSS Parts

Use CSS parts to style internal radio group elements:

```css
/* Style the base form control */
wa-radio-group::part(form-control) {
  margin-bottom: 1rem;
}

/* Style the label */
wa-radio-group::part(label) {
  font-weight: bold;
  margin-bottom: 0.5rem;
}

/* Style the button group container */
wa-radio-group::part(button-group) {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

/* Style the help text */
wa-radio-group::part(help-text) {
  font-size: 0.875rem;
  color: #666;
  margin-top: 0.5rem;
}
```

## Customization

### Horizontal Layout

```css
/* Display radios in a row */
wa-radio-group::part(button-group) {
  flex-direction: row;
  gap: 1rem;
}
```

### Card-Style Radio Group

```css
wa-radio-group {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 1rem;
  background-color: #fafafa;
}

wa-radio-group::part(label) {
  color: #333;
  font-size: 1.125rem;
}
```

### Compact Radio Group

```css
wa-radio-group::part(button-group) {
  gap: 0.25rem;
}

wa-radio-group::part(label) {
  font-size: 0.875rem;
  margin-bottom: 0.25rem;
}
```

## Best Practices

- Provide a clear, descriptive label for the group
- Use 2-5 radio options (consider select for more)
- Pre-select a sensible default when appropriate
- Use required attribute for mandatory selections
- Provide help text for complex choices
- Order options logically (alphabetically, by frequency, etc.)
- Use consistent wording across similar radio groups
- Consider using icons to enhance recognition
- Validate selections on form submission

## Accessibility

- Radio groups have proper ARIA roles and attributes
- Group label provides context for all options
- Keyboard navigation with Arrow keys between radios
- Tab key moves between form fields
- Required state announced to screen readers
- Validation errors communicated accessibly
- Help text associated with the group
- Focus management follows best practices

### Required Radio Groups

Always provide clear indication when a selection is required:

```html
<wa-radio-group
  label="Required Selection"
  name="selection"
  required
  help-text="* This field is required">
  <wa-radio value="option1">Option 1</wa-radio>
  <wa-radio value="option2">Option 2</wa-radio>
</wa-radio-group>
```

## Troubleshooting

### Value Not Updating

**Problem:** Radio group value doesn't update when radio is clicked

**Solution:** Ensure all radios have unique `value` attributes

```html
<!-- Correct -->
<wa-radio-group name="option">
  <wa-radio value="a">Option A</wa-radio>
  <wa-radio value="b">Option B</wa-radio>
</wa-radio-group>

<!-- Incorrect - duplicate values -->
<wa-radio-group name="option">
  <wa-radio value="same">Option A</wa-radio>
  <wa-radio value="same">Option B</wa-radio>
</wa-radio-group>
```

### Form Submission Issues

**Problem:** Radio group value not included in form data

**Solution:** Ensure radio group has a `name` attribute

```html
<!-- Correct -->
<wa-radio-group name="selection">
  <wa-radio value="a">Option A</wa-radio>
</wa-radio-group>

<!-- Incorrect - missing name -->
<wa-radio-group>
  <wa-radio value="a">Option A</wa-radio>
</wa-radio-group>
```

### Validation Not Working

**Problem:** Required validation not triggering

**Solution:** Ensure `required` attribute is set on the group, not individual radios

```html
<!-- Correct -->
<wa-radio-group name="option" required>
  <wa-radio value="a">Option A</wa-radio>
  <wa-radio value="b">Option B</wa-radio>
</wa-radio-group>

<!-- Incorrect - required on radio instead of group -->
<wa-radio-group name="option">
  <wa-radio value="a" required>Option A</wa-radio>
  <wa-radio value="b" required>Option B</wa-radio>
</wa-radio-group>
```

## Related

- [Radio](./radio.md)
- [Checkbox](./checkbox.md)
- [Switch](./switch.md)
- [Select](./select.md)
- [Form Controls Guide](../guides/form-controls.md)
