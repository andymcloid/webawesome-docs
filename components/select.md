# Select

Dropdown selection control for choosing one or multiple options from a list.

## Overview

The `<wa-select>` component provides a fully customizable dropdown selection control with support for single and multiple selection, option groups, custom rendering, and form integration. It offers a consistent, accessible interface for collecting user input from a predefined set of options.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/select/select.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic select -->
<wa-select>
  <wa-option value="option1">Option 1</wa-option>
  <wa-option value="option2">Option 2</wa-option>
  <wa-option value="option3">Option 3</wa-option>
</wa-select>

<!-- Select with label -->
<wa-select label="Choose an option">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
</wa-select>

<!-- Select with placeholder -->
<wa-select placeholder="Select a fruit...">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
</wa-select>

<!-- Select with default value -->
<wa-select value="banana">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
</wa-select>
```

## Multiple Selection

Enable multiple selection with the `multiple` attribute:

```html
<!-- Multiple select -->
<wa-select multiple placeholder="Select fruits...">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
  <wa-option value="grape">Grape</wa-option>
  <wa-option value="mango">Mango</wa-option>
</wa-select>

<!-- Multiple select with default values -->
<wa-select multiple value="apple banana">
  <wa-option value="apple">Apple</wa-option>
  <wa-option value="banana">Banana</wa-option>
  <wa-option value="orange">Orange</wa-option>
  <wa-option value="grape">Grape</wa-option>
</wa-select>
```

## Disabled State

Disable the entire select or individual options:

```html
<!-- Disabled select -->
<wa-select disabled>
  <wa-option value="option1">Option 1</wa-option>
  <wa-option value="option2">Option 2</wa-option>
  <wa-option value="option3">Option 3</wa-option>
</wa-select>

<!-- Select with disabled options -->
<wa-select>
  <wa-option value="available1">Available Option 1</wa-option>
  <wa-option value="unavailable" disabled>Unavailable Option</wa-option>
  <wa-option value="available2">Available Option 2</wa-option>
  <wa-option value="soldout" disabled>Sold Out</wa-option>
</wa-select>
```

## Option Groups

Organize options into groups using `<wa-option-group>`:

```html
<wa-select label="Select a location">
  <wa-option-group label="North America">
    <wa-option value="us">United States</wa-option>
    <wa-option value="ca">Canada</wa-option>
    <wa-option value="mx">Mexico</wa-option>
  </wa-option-group>

  <wa-option-group label="Europe">
    <wa-option value="uk">United Kingdom</wa-option>
    <wa-option value="de">Germany</wa-option>
    <wa-option value="fr">France</wa-option>
  </wa-option-group>

  <wa-option-group label="Asia">
    <wa-option value="jp">Japan</wa-option>
    <wa-option value="cn">China</wa-option>
    <wa-option value="in">India</wa-option>
  </wa-option-group>
</wa-select>
```

## Sizes

Control select size with the `size` attribute:

```html
<wa-select size="small" placeholder="Small select">
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
  <wa-option value="3">Option 3</wa-option>
</wa-select>

<wa-select size="medium" placeholder="Medium select (default)">
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
  <wa-option value="3">Option 3</wa-option>
</wa-select>

<wa-select size="large" placeholder="Large select">
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
  <wa-option value="3">Option 3</wa-option>
</wa-select>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | `''` | No | The selected value(s). For multiple selects, use space-separated values |
| `multiple` | boolean | `false` | No | Enable multiple selection |
| `placeholder` | string | - | No | Placeholder text shown when no option is selected |
| `disabled` | boolean | `false` | No | Disable the select |
| `required` | boolean | `false` | No | Make the select required for form validation |
| `clearable` | boolean | `false` | No | Add a clear button to remove selection |
| `size` | string | `'medium'` | No | Select size: `small`, `medium`, `large` |
| `name` | string | - | No | Name attribute for form submission |
| `label` | string | - | No | Label text displayed above the select |
| `help-text` | string | - | No | Help text displayed below the select |
| `max-options-visible` | number | `3` | No | Maximum number of selected options to display before showing count |
| `placement` | string | `'bottom'` | No | Dropdown placement: `top`, `bottom` |
| `hoist` | boolean | `false` | No | Render dropdown in a portal to prevent clipping |

## Examples

### Basic Select with Options

```html
<wa-select label="Select your country" placeholder="Choose a country">
  <wa-option value="us">United States</wa-option>
  <wa-option value="uk">United Kingdom</wa-option>
  <wa-option value="ca">Canada</wa-option>
  <wa-option value="au">Australia</wa-option>
  <wa-option value="de">Germany</wa-option>
</wa-select>
```

### Multiple Selection

```html
<wa-select
  multiple
  label="Select your favorite programming languages"
  placeholder="Choose one or more..."
  max-options-visible="2">
  <wa-option value="javascript">JavaScript</wa-option>
  <wa-option value="python">Python</wa-option>
  <wa-option value="java">Java</wa-option>
  <wa-option value="csharp">C#</wa-option>
  <wa-option value="go">Go</wa-option>
  <wa-option value="rust">Rust</wa-option>
  <wa-option value="typescript">TypeScript</wa-option>
</wa-select>
```

### Disabled Options

```html
<wa-select label="Product availability">
  <wa-option value="product1">Premium Plan - $99/mo</wa-option>
  <wa-option value="product2" disabled>Enterprise Plan - Contact Sales (Coming Soon)</wa-option>
  <wa-option value="product3">Starter Plan - $29/mo</wa-option>
  <wa-option value="product4" disabled>Legacy Plan (No Longer Available)</wa-option>
</wa-select>
```

### Option Groups

```html
<wa-select label="Choose your tech stack" multiple>
  <wa-option-group label="Frontend">
    <wa-option value="react">React</wa-option>
    <wa-option value="vue">Vue</wa-option>
    <wa-option value="angular">Angular</wa-option>
    <wa-option value="svelte">Svelte</wa-option>
  </wa-option-group>

  <wa-option-group label="Backend">
    <wa-option value="node">Node.js</wa-option>
    <wa-option value="django">Django</wa-option>
    <wa-option value="rails">Ruby on Rails</wa-option>
    <wa-option value="laravel">Laravel</wa-option>
  </wa-option-group>

  <wa-option-group label="Database">
    <wa-option value="postgres">PostgreSQL</wa-option>
    <wa-option value="mysql">MySQL</wa-option>
    <wa-option value="mongodb">MongoDB</wa-option>
    <wa-option value="redis">Redis</wa-option>
  </wa-option-group>
</wa-select>
```

### Clearable Select

```html
<wa-select
  clearable
  value="option2"
  label="Clearable select"
  placeholder="Select an option...">
  <wa-option value="option1">Option 1</wa-option>
  <wa-option value="option2">Option 2</wa-option>
  <wa-option value="option3">Option 3</wa-option>
</wa-select>
```

### Custom Rendering

```html
<wa-select label="Choose a team member">
  <wa-option value="user1">
    <wa-avatar slot="start" image="/avatars/user1.jpg"></wa-avatar>
    John Smith - Developer
  </wa-option>
  <wa-option value="user2">
    <wa-avatar slot="start" image="/avatars/user2.jpg"></wa-avatar>
    Jane Doe - Designer
  </wa-option>
  <wa-option value="user3">
    <wa-avatar slot="start" image="/avatars/user3.jpg"></wa-avatar>
    Mike Johnson - Manager
  </wa-option>
</wa-select>

<!-- With icons -->
<wa-select label="Select priority">
  <wa-option value="high">
    <wa-icon slot="start" name="exclamation-triangle" style="color: red;"></wa-icon>
    High Priority
  </wa-option>
  <wa-option value="medium">
    <wa-icon slot="start" name="exclamation-circle" style="color: orange;"></wa-icon>
    Medium Priority
  </wa-option>
  <wa-option value="low">
    <wa-icon slot="start" name="info-circle" style="color: blue;"></wa-icon>
    Low Priority
  </wa-option>
</wa-select>
```

### Form Integration

```html
<form id="userForm">
  <wa-select
    name="country"
    label="Country"
    placeholder="Select your country"
    required>
    <wa-option value="us">United States</wa-option>
    <wa-option value="uk">United Kingdom</wa-option>
    <wa-option value="ca">Canada</wa-option>
  </wa-select>

  <wa-select
    name="interests"
    label="Interests"
    multiple
    help-text="Select all that apply">
    <wa-option value="tech">Technology</wa-option>
    <wa-option value="sports">Sports</wa-option>
    <wa-option value="music">Music</wa-option>
    <wa-option value="art">Art</wa-option>
  </wa-select>

  <wa-button type="submit" variant="primary">Submit</wa-button>
</form>

<script>
  const form = document.getElementById('userForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const formData = new FormData(form);
    const country = formData.get('country');
    const interests = formData.getAll('interests');

    console.log('Country:', country);
    console.log('Interests:', interests);
  });
</script>
```

### Dynamic Options

```html
<wa-select id="dynamicSelect" label="Select a user" placeholder="Loading...">
</wa-select>

<script>
  const select = document.getElementById('dynamicSelect');

  // Fetch and populate options
  async function loadUsers() {
    try {
      const response = await fetch('/api/users');
      const users = await response.json();

      // Clear existing options
      select.innerHTML = '';

      // Add new options
      users.forEach(user => {
        const option = document.createElement('wa-option');
        option.value = user.id;
        option.textContent = user.name;
        select.appendChild(option);
      });

      select.placeholder = 'Select a user...';
    } catch (error) {
      console.error('Failed to load users:', error);
      select.placeholder = 'Error loading users';
    }
  }

  loadUsers();
</script>
```

### Validation

```html
<form id="validationForm">
  <wa-select
    id="categorySelect"
    name="category"
    label="Category"
    required
    help-text="Please select a category">
    <wa-option value="electronics">Electronics</wa-option>
    <wa-option value="clothing">Clothing</wa-option>
    <wa-option value="books">Books</wa-option>
  </wa-select>

  <wa-button type="submit" variant="primary">Validate</wa-button>
</form>

<script>
  const form = document.getElementById('validationForm');
  const select = document.getElementById('categorySelect');

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    if (select.checkValidity()) {
      console.log('Valid!', select.value);
    } else {
      console.log('Invalid - please select an option');
      select.focus();
    }
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus()` | Sets focus on the select | `void` |
| `blur()` | Removes focus from the select | `void` |
| `show()` | Opens the dropdown menu | `void` |
| `hide()` | Closes the dropdown menu | `void` |
| `checkValidity()` | Checks if the select meets validation constraints | `boolean` |
| `reportValidity()` | Checks validity and shows validation message | `boolean` |
| `setCustomValidity(message)` | Sets a custom validation message | `void` |

### Method Examples

```javascript
const select = document.querySelector('wa-select');

// Focus the select
select.focus();

// Remove focus
select.blur();

// Programmatically open dropdown
select.show();

// Close dropdown
select.hide();

// Check if valid
if (select.checkValidity()) {
  console.log('Select is valid');
} else {
  console.log('Select is invalid');
}

// Show validation message
select.reportValidity();

// Set custom validation
select.setCustomValidity('Please choose a different option');
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the selection changes | `{ value: string \| string[] }` |
| `wa-focus` | Emitted when the select gains focus | - |
| `wa-blur` | Emitted when the select loses focus | - |
| `wa-show` | Emitted when the dropdown opens | - |
| `wa-hide` | Emitted when the dropdown closes | - |
| `wa-clear` | Emitted when the clear button is clicked | - |
| `wa-invalid` | Emitted when the select becomes invalid | - |

### Event Examples

```javascript
const select = document.querySelector('wa-select');

// Listen for selection changes
select.addEventListener('wa-change', (event) => {
  console.log('Selected value:', event.detail.value);
});

// Listen for focus
select.addEventListener('wa-focus', () => {
  console.log('Select focused');
});

// Listen for blur
select.addEventListener('wa-blur', () => {
  console.log('Select blurred');
});

// Listen for dropdown open
select.addEventListener('wa-show', () => {
  console.log('Dropdown opened');
});

// Listen for dropdown close
select.addEventListener('wa-hide', () => {
  console.log('Dropdown closed');
});

// Listen for clear
select.addEventListener('wa-clear', () => {
  console.log('Selection cleared');
});

// Listen for validation errors
select.addEventListener('wa-invalid', () => {
  console.log('Select is invalid');
});
```

### Reactive Form Handling

```html
<wa-select id="countrySelect" label="Country">
  <wa-option value="us">United States</wa-option>
  <wa-option value="uk">United Kingdom</wa-option>
  <wa-option value="ca">Canada</wa-option>
</wa-select>

<wa-select id="stateSelect" label="State" placeholder="First select a country" disabled>
</wa-select>

<script>
  const countrySelect = document.getElementById('countrySelect');
  const stateSelect = document.getElementById('stateSelect');

  const statesByCountry = {
    us: ['California', 'Texas', 'New York', 'Florida'],
    uk: ['England', 'Scotland', 'Wales', 'Northern Ireland'],
    ca: ['Ontario', 'Quebec', 'British Columbia', 'Alberta']
  };

  countrySelect.addEventListener('wa-change', (event) => {
    const country = event.detail.value;

    // Clear and populate state options
    stateSelect.innerHTML = '';
    stateSelect.value = '';

    if (country && statesByCountry[country]) {
      statesByCountry[country].forEach(state => {
        const option = document.createElement('wa-option');
        option.value = state.toLowerCase().replace(/\s+/g, '-');
        option.textContent = state;
        stateSelect.appendChild(option);
      });

      stateSelect.disabled = false;
      stateSelect.placeholder = 'Select a state...';
    } else {
      stateSelect.disabled = true;
      stateSelect.placeholder = 'First select a country';
    }
  });
</script>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The select's options (wa-option elements) |
| `label` | The select's label (alternative to label attribute) |
| `help-text` | Help text displayed below the select |
| `clear-icon` | Custom icon for the clear button |
| `expand-icon` | Custom icon for the dropdown expand indicator |

### Slot Examples

```html
<!-- Custom label slot -->
<wa-select>
  <span slot="label">
    Choose Option
    <wa-badge variant="primary">Required</wa-badge>
  </span>
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
</wa-select>

<!-- Custom help text -->
<wa-select label="Email preference">
  <wa-option value="daily">Daily digest</wa-option>
  <wa-option value="weekly">Weekly summary</wa-option>
  <wa-option value="never">Never</wa-option>

  <span slot="help-text">
    You can change this anytime in settings
  </span>
</wa-select>
```

## CSS Parts

Use CSS parts to style internal select elements:

```css
/* Style the form control wrapper */
wa-select::part(form-control) {
  /* Custom styles */
}

/* Style the label */
wa-select::part(label) {
  font-weight: bold;
  color: #333;
}

/* Style the combobox (main select display) */
wa-select::part(combobox) {
  border: 2px solid #ddd;
  border-radius: 8px;
}

/* Style when focused */
wa-select::part(combobox):focus {
  border-color: #4f46e5;
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

/* Style the display area */
wa-select::part(display-input) {
  font-size: 16px;
}

/* Style the listbox (dropdown) */
wa-select::part(listbox) {
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Style the clear button */
wa-select::part(clear-button) {
  color: #999;
}

/* Style the expand icon */
wa-select::part(expand-icon) {
  color: #666;
}

/* Style help text */
wa-select::part(help-text) {
  font-size: 14px;
  color: #666;
}
```

### Custom Theming

```css
/* Dark theme select */
wa-select.dark::part(combobox) {
  background-color: #1f2937;
  border-color: #374151;
  color: #f9fafb;
}

wa-select.dark::part(listbox) {
  background-color: #1f2937;
  border-color: #374151;
}

/* Rounded select */
wa-select.rounded::part(combobox) {
  border-radius: 24px;
}

/* Minimal select */
wa-select.minimal::part(combobox) {
  border: none;
  border-bottom: 2px solid #ddd;
  border-radius: 0;
}
```

## Best Practices

- Use clear, descriptive labels for select controls
- Provide meaningful placeholder text when appropriate
- Use option groups to organize large lists of options
- Consider multiple select for scenarios where users commonly need to choose multiple items
- Use disabled options to show unavailable choices rather than hiding them
- Provide help text for complex selections
- Use clearable selects when the selection is optional
- For very large lists, consider implementing search functionality
- Validate selections on submission for required fields
- Use appropriate sizes to match your design system
- Don't use select controls for navigation (use links or menus instead)
- Order options logically (alphabetically, by frequency, or by relevance)

### Do's and Don'ts

- Do use selects for 4+ options (use radio buttons for fewer)
- Do show the most common options first
- Do use clear, concise option labels
- Do provide default selections when appropriate
- Do use clearable for optional selections
- Don't use select for binary choices (use checkbox or toggle)
- Don't hide important options in deeply nested groups
- Don't use overly long option labels
- Don't forget to handle validation errors gracefully
- Don't use disabled selects without explaining why

## Accessibility

The `wa-select` component follows WAI-ARIA best practices for accessibility:

- Automatically includes appropriate ARIA roles and attributes
- Supports keyboard navigation:
  - `Tab` - Focus the select
  - `Space/Enter` - Open dropdown
  - `Arrow Up/Down` - Navigate options
  - `Home/End` - Jump to first/last option
  - `Escape` - Close dropdown
  - `Type to search` - Filter options by typing
- Properly announces selection state to screen readers
- Associates labels with form controls
- Announces validation errors
- Disabled options are properly marked and not focusable

### Accessible Examples

```html
<!-- Properly labeled select -->
<wa-select
  label="Country of residence"
  required
  help-text="Select the country where you currently live">
  <wa-option value="us">United States</wa-option>
  <wa-option value="uk">United Kingdom</wa-option>
  <wa-option value="ca">Canada</wa-option>
</wa-select>

<!-- Select with aria-describedby -->
<wa-select
  label="Notification frequency"
  aria-describedby="frequency-help">
  <wa-option value="immediately">Immediately</wa-option>
  <wa-option value="daily">Daily</wa-option>
  <wa-option value="weekly">Weekly</wa-option>
</wa-select>
<div id="frequency-help" style="font-size: 0.875rem; color: #666;">
  Choose how often you want to receive notifications
</div>

<!-- Required field with clear indication -->
<wa-select
  label="Department"
  required
  aria-required="true">
  <wa-option value="sales">Sales</wa-option>
  <wa-option value="marketing">Marketing</wa-option>
  <wa-option value="engineering">Engineering</wa-option>
</wa-select>
```

## Troubleshooting

### Select Not Showing Options

**Problem:** Dropdown appears empty

**Solution:** Ensure you're using `<wa-option>` elements and they have values

```html
<!-- Correct -->
<wa-select>
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
</wa-select>

<!-- Incorrect - missing wa-option -->
<wa-select>
  <div>Option 1</div>
  <div>Option 2</div>
</wa-select>
```

### Value Not Updating

**Problem:** Programmatically setting value doesn't work

**Solution:** Ensure the value matches an existing option value exactly

```javascript
// Correct
select.value = 'option1';

// Incorrect - value doesn't match any option
select.value = 'Option 1'; // Should be 'option1'
```

### Multiple Select Values

**Problem:** Multiple select not recognizing selected values

**Solution:** Use space-separated values or array

```javascript
// Space-separated string
select.value = 'option1 option2 option3';

// Or set via property as array
select.value = ['option1', 'option2', 'option3'];
```

### Dropdown Clipped by Container

**Problem:** Dropdown is cut off by parent container

**Solution:** Use the `hoist` attribute to render dropdown in a portal

```html
<wa-select hoist>
  <wa-option value="1">Option 1</wa-option>
  <wa-option value="2">Option 2</wa-option>
</wa-select>
```

### Custom Validation Not Working

**Problem:** Custom validation message not displaying

**Solution:** Call `setCustomValidity()` and then `reportValidity()`

```javascript
select.setCustomValidity('This option is not allowed');
select.reportValidity(); // This shows the message
```

## Related

- [Option](./option.md)
- [Option Group](./option-group.md)
- [Input](./input.md)
- [Checkbox](./checkbox.md)
- [Radio](./radio.md)
- [Form Controls Guide](../guides/form-controls.md)
