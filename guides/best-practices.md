---
meta:
  title: Best Practices
  description: Comprehensive guide to building robust, accessible, and performant applications with Web Awesome components.
---

# Best Practices

A comprehensive guide to building robust, accessible, and performant applications with Web Awesome components.

## Overview

Following best practices when working with Web Awesome components ensures your applications are maintainable, accessible, and performant. This guide covers essential patterns and anti-patterns across component usage, performance optimization, accessibility, styling, forms, events, security, code organization, and testing.

These recommendations are based on real-world usage patterns and are designed to help you avoid common pitfalls while maximizing the benefits of Web Awesome's component library.

## Component Usage

### Always Use Closing Tags

Web components require proper closing tags, even when they have no content. Self-closing tags are not valid in HTML for custom elements.

**Do:**

```html
<wa-button></wa-button>
<wa-icon name="check"></wa-icon>
<wa-spinner></wa-spinner>
```

**Don't:**

```html
<wa-button />
<wa-icon name="check" />
<wa-spinner />
```

### Wait for Component Registration

Before accessing component properties or methods, ensure the component is defined and ready.

**Do:**

```javascript
// Wait for component to be defined
await customElements.whenDefined('wa-button');
const button = document.querySelector('wa-button');
button.variant = 'primary';

// Or use the ready promise
const dialog = document.querySelector('wa-dialog');
await dialog.updateComplete;
dialog.show();
```

**Don't:**

```javascript
// Component may not be registered yet
const button = document.querySelector('wa-button');
button.variant = 'primary'; // May fail silently
```

### Use Semantic HTML

Leverage the semantic meaning of components to improve accessibility and maintainability.

**Do:**

```html
<wa-button type="submit">Submit Form</wa-button>
<wa-button type="button">Cancel</wa-button>
<wa-icon-button name="close" label="Close dialog"></wa-icon-button>
```

**Don't:**

```html
<wa-button onclick="submitForm()">Submit Form</wa-button>
<div class="button" onclick="cancel()">Cancel</div>
<wa-icon name="close" onclick="closeDialog()"></wa-icon>
```

### Provide Required Properties

Always provide required attributes and properties for proper component functionality.

**Do:**

```html
<wa-icon name="star"></wa-icon>
<wa-icon-button name="settings" label="Open settings"></wa-icon-button>
<wa-avatar label="User profile picture"></wa-avatar>
```

**Don't:**

```html
<wa-icon></wa-icon>
<wa-icon-button name="settings"></wa-icon-button>
<wa-avatar></wa-avatar>
```

## Performance

### Batch Property Changes

When updating multiple properties, batch changes to minimize re-renders.

**Do:**

```javascript
const element = document.querySelector('wa-input');

// Batch updates
requestAnimationFrame(() => {
  element.value = 'New value';
  element.label = 'New label';
  element.helpText = 'New help text';
});
```

**Don't:**

```javascript
const element = document.querySelector('wa-input');

// Each change triggers a re-render
element.value = 'New value';
element.label = 'New label';
element.helpText = 'New help text';
```

### Use Event Delegation

For dynamic lists or tables, use event delegation instead of attaching listeners to each item.

**Do:**

```javascript
// Attach one listener to the container
const list = document.querySelector('.item-list');
list.addEventListener('wa-select', (event) => {
  if (event.target.matches('wa-menu-item')) {
    handleItemSelect(event.target);
  }
});
```

**Don't:**

```javascript
// Attach listeners to every item
const items = document.querySelectorAll('wa-menu-item');
items.forEach(item => {
  item.addEventListener('wa-select', handleItemSelect);
});
```

### Lazy Load Components

For large applications, lazy load components that aren't immediately needed.

**Do:**

```javascript
// Load dialog only when needed
async function openSettings() {
  if (!customElements.get('wa-dialog')) {
    await import('@web-awesome/components/wa-dialog');
  }

  const dialog = document.querySelector('wa-dialog');
  await dialog.show();
}
```

**Don't:**

```javascript
// Import everything upfront
import '@web-awesome/components/dist/all';

function openSettings() {
  document.querySelector('wa-dialog').show();
}
```

### Virtualize Long Lists

For lists with many items, use virtualization to render only visible items.

**Do:**

```javascript
// Use virtual scrolling for large datasets
const virtualList = document.querySelector('wa-virtual-list');
virtualList.items = largeDataset; // Only visible items are rendered
```

**Don't:**

```html
<!-- Rendering thousands of items -->
<wa-menu>
  <wa-menu-item>Item 1</wa-menu-item>
  <wa-menu-item>Item 2</wa-menu-item>
  <!-- ... 10,000 more items ... -->
</wa-menu>
```

## Accessibility

### Always Provide Labels

Labels are essential for screen readers and assistive technologies.

**Do:**

```html
<wa-input label="Email address" type="email" required></wa-input>
<wa-icon-button name="close" label="Close dialog"></wa-icon-button>
<wa-switch>Enable notifications</wa-switch>
```

**Don't:**

```html
<wa-input type="email" placeholder="Email"></wa-input>
<wa-icon-button name="close"></wa-icon-button>
<wa-switch></wa-switch>
```

### Use ARIA Attributes Appropriately

Enhance accessibility with proper ARIA attributes when native semantics aren't sufficient.

**Do:**

```html
<wa-button aria-expanded="false" aria-controls="menu-panel">
  Menu
</wa-button>

<wa-alert role="alert" aria-live="polite">
  Your changes have been saved.
</wa-alert>
```

**Don't:**

```html
<wa-button>Menu</wa-button>
<wa-alert>Your changes have been saved.</wa-alert>
```

### Support Keyboard Navigation

Ensure all interactive elements are keyboard accessible.

**Do:**

```javascript
// Allow keyboard interaction
dropdown.addEventListener('keydown', (event) => {
  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault();
    dropdown.show();
  }

  if (event.key === 'Escape') {
    dropdown.hide();
  }
});
```

**Don't:**

```javascript
// Mouse-only interaction
dropdown.addEventListener('click', () => {
  dropdown.show();
});
```

### Manage Focus Properly

Handle focus management for modals, dropdowns, and dynamic content.

**Do:**

```javascript
const dialog = document.querySelector('wa-dialog');

// Save focus before opening
const previousFocus = document.activeElement;

await dialog.show();

// Return focus when closing
dialog.addEventListener('wa-hide', () => {
  previousFocus.focus();
}, { once: true });
```

**Don't:**

```javascript
const dialog = document.querySelector('wa-dialog');
await dialog.show();
// Focus is lost, user doesn't know where they are
```

### Provide Alternative Text

Always provide alternative text for images and icons that convey meaning.

**Do:**

```html
<wa-icon name="success" label="Success"></wa-icon>
<wa-avatar image="/user.jpg" label="John Doe's profile picture"></wa-avatar>
```

**Don't:**

```html
<wa-icon name="success"></wa-icon>
<wa-avatar image="/user.jpg"></wa-avatar>
```

## Styling

### Use Design Tokens

Leverage design tokens for consistent theming and easy customization.

**Do:**

```css
.custom-component {
  color: var(--wa-color-primary-600);
  padding: var(--wa-spacing-medium);
  border-radius: var(--wa-border-radius-medium);
  font-size: var(--wa-font-size-medium);
}
```

**Don't:**

```css
.custom-component {
  color: #0066cc;
  padding: 16px;
  border-radius: 4px;
  font-size: 14px;
}
```

### Leverage CSS Parts

Use CSS parts to style internal component elements without breaking encapsulation.

**Do:**

```css
/* Style specific parts of the component */
wa-button::part(base) {
  border-width: 2px;
}

wa-input::part(input) {
  font-family: monospace;
}

wa-card::part(header) {
  background: var(--wa-color-primary-50);
}
```

**Don't:**

```css
/* Trying to pierce shadow DOM (doesn't work) */
wa-button .button {
  border-width: 2px;
}

wa-input input {
  font-family: monospace;
}
```

### Scope Customizations

Keep custom styles scoped to avoid unintended side effects.

**Do:**

```css
/* Scoped to specific context */
.settings-panel wa-button::part(base) {
  min-width: 120px;
}

.toolbar wa-icon-button {
  --wa-icon-button-size: 2rem;
}
```

**Don't:**

```css
/* Global changes affect all instances */
wa-button::part(base) {
  min-width: 120px;
}

wa-icon-button {
  --wa-icon-button-size: 2rem;
}
```

### Use CSS Custom Properties

Customize components using their exposed CSS custom properties.

**Do:**

```html
<style>
  wa-button.large {
    --wa-button-font-size: 1.25rem;
    --wa-button-height: 3rem;
  }
</style>

<wa-button class="large">Large Button</wa-button>
```

**Don't:**

```html
<style>
  wa-button.large::part(base) {
    font-size: 1.25rem !important;
    height: 3rem !important;
  }
</style>

<wa-button class="large">Large Button</wa-button>
```

## Forms

### Implement Validation Strategy

Use built-in validation with custom validation for complex requirements.

**Do:**

```html
<form id="signup-form">
  <wa-input
    name="email"
    type="email"
    label="Email"
    required
  ></wa-input>

  <wa-input
    name="password"
    type="password"
    label="Password"
    minlength="8"
    required
  ></wa-input>

  <wa-button type="submit">Sign Up</wa-button>
</form>

<script>
  const form = document.getElementById('signup-form');

  form.addEventListener('submit', async (event) => {
    event.preventDefault();

    // Check native validation
    if (!form.reportValidity()) {
      return;
    }

    // Custom validation
    const password = form.querySelector('[name="password"]');
    if (!/[A-Z]/.test(password.value)) {
      password.setCustomValidity('Password must contain an uppercase letter');
      password.reportValidity();
      return;
    }

    // Submit form
    await submitForm(new FormData(form));
  });
</script>
```

**Don't:**

```javascript
// No validation
form.addEventListener('submit', (event) => {
  event.preventDefault();
  submitForm(new FormData(form));
});
```

### Handle Errors Gracefully

Provide clear, actionable error messages.

**Do:**

```javascript
try {
  await submitForm(formData);
  showSuccessMessage('Your account has been created!');
} catch (error) {
  if (error.code === 'EMAIL_EXISTS') {
    emailInput.setCustomValidity('This email is already registered');
    emailInput.reportValidity();
  } else {
    showErrorAlert('Unable to create account. Please try again.');
  }
}
```

**Don't:**

```javascript
try {
  await submitForm(formData);
} catch (error) {
  alert('Error');
}
```

### Enhance User Experience

Provide feedback during submission and disable submit button to prevent double submissions.

**Do:**

```javascript
const submitButton = form.querySelector('wa-button[type="submit"]');

form.addEventListener('submit', async (event) => {
  event.preventDefault();

  // Disable button and show loading state
  submitButton.loading = true;
  submitButton.disabled = true;

  try {
    await submitForm(new FormData(form));
    showSuccessMessage('Form submitted successfully!');
  } catch (error) {
    handleError(error);
  } finally {
    submitButton.loading = false;
    submitButton.disabled = false;
  }
});
```

**Don't:**

```javascript
form.addEventListener('submit', async (event) => {
  event.preventDefault();
  await submitForm(new FormData(form));
  // No feedback, button can be clicked multiple times
});
```

### Use Appropriate Input Types

Choose the right input type for better user experience and validation.

**Do:**

```html
<wa-input type="email" label="Email"></wa-input>
<wa-input type="tel" label="Phone"></wa-input>
<wa-input type="url" label="Website"></wa-input>
<wa-input type="number" label="Age" min="18" max="120"></wa-input>
<wa-input type="date" label="Birth Date"></wa-input>
```

**Don't:**

```html
<wa-input type="text" label="Email"></wa-input>
<wa-input type="text" label="Phone"></wa-input>
<wa-input type="text" label="Website"></wa-input>
<wa-input type="text" label="Age"></wa-input>
<wa-input type="text" label="Birth Date"></wa-input>
```

## Events

### Use Web Awesome Event Names

Web Awesome components emit events with the `wa-` prefix. Always use these standard event names.

**Do:**

```javascript
input.addEventListener('wa-input', (event) => {
  console.log('Input value changed:', event.target.value);
});

dialog.addEventListener('wa-show', () => {
  console.log('Dialog opened');
});

dialog.addEventListener('wa-hide', () => {
  console.log('Dialog closed');
});
```

**Don't:**

```javascript
input.addEventListener('input', (event) => {
  // This won't fire for wa-input components
  console.log('Input changed');
});

dialog.addEventListener('open', () => {
  // This won't fire
  console.log('Dialog opened');
});
```

### Handle Events Properly

Always check event properties and handle errors appropriately.

**Do:**

```javascript
button.addEventListener('wa-click', (event) => {
  if (event.defaultPrevented) {
    return;
  }

  try {
    handleButtonClick(event);
  } catch (error) {
    console.error('Error handling click:', error);
    showErrorAlert('An error occurred. Please try again.');
  }
});
```

**Don't:**

```javascript
button.addEventListener('wa-click', (event) => {
  handleButtonClick(event);
  // No error handling
});
```

### Prevent Default When Necessary

Use `preventDefault()` to stop default behavior when implementing custom functionality.

**Do:**

```javascript
form.addEventListener('submit', (event) => {
  event.preventDefault();
  handleCustomSubmit(new FormData(event.target));
});

link.addEventListener('wa-click', (event) => {
  event.preventDefault();
  handleNavigationInApp(link.href);
});
```

**Don't:**

```javascript
form.addEventListener('submit', (event) => {
  handleCustomSubmit(new FormData(event.target));
  // Form submits normally, page reloads
});
```

### Clean Up Event Listeners

Remove event listeners when components are destroyed to prevent memory leaks.

**Do:**

```javascript
class MyComponent {
  constructor() {
    this.handleResize = this.handleResize.bind(this);
  }

  connectedCallback() {
    window.addEventListener('resize', this.handleResize);
  }

  disconnectedCallback() {
    window.removeEventListener('resize', this.handleResize);
  }

  handleResize() {
    // Handle resize
  }
}
```

**Don't:**

```javascript
class MyComponent {
  connectedCallback() {
    window.addEventListener('resize', () => {
      // Anonymous function can't be removed
      this.handleResize();
    });
  }

  // No cleanup
}
```

## Security

### Validate Input

Always validate and sanitize user input before processing or displaying it.

**Do:**

```javascript
function handleUserInput(input) {
  // Validate input
  if (!input || typeof input !== 'string') {
    throw new Error('Invalid input');
  }

  // Sanitize for length
  if (input.length > 1000) {
    throw new Error('Input too long');
  }

  // Sanitize for allowed characters
  const sanitized = input.replace(/[<>]/g, '');

  return sanitized;
}
```

**Don't:**

```javascript
function handleUserInput(input) {
  // No validation
  return input;
}
```

### Prevent XSS Attacks

Never use `innerHTML` with user-provided content. Use `textContent` or sanitization libraries.

**Do:**

```javascript
// Safe: Uses textContent
const message = document.querySelector('.message');
message.textContent = userInput;

// Safe: Uses a sanitization library
import DOMPurify from 'dompurify';
message.innerHTML = DOMPurify.sanitize(userInput);
```

**Don't:**

```javascript
// Dangerous: XSS vulnerability
const message = document.querySelector('.message');
message.innerHTML = userInput;
```

### Sanitize URLs

Validate and sanitize URLs before using them in links or redirects.

**Do:**

```javascript
function isSafeUrl(url) {
  try {
    const parsed = new URL(url, window.location.origin);
    return ['http:', 'https:'].includes(parsed.protocol);
  } catch {
    return false;
  }
}

const link = document.querySelector('wa-button');
if (isSafeUrl(userProvidedUrl)) {
  link.href = userProvidedUrl;
} else {
  console.error('Invalid URL');
}
```

**Don't:**

```javascript
// Dangerous: javascript: URLs can execute code
const link = document.querySelector('wa-button');
link.href = userProvidedUrl;
```

### Use Content Security Policy

Implement a Content Security Policy to prevent XSS and other injection attacks.

**Do:**

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline';">
```

**Don't:**

```html
<!-- No CSP, vulnerable to XSS -->
```

## Code Organization

### Follow Naming Conventions

Use consistent, descriptive names for components, functions, and variables.

**Do:**

```javascript
// Clear, descriptive names
const submitButton = document.querySelector('#submit-button');
const userEmailInput = document.querySelector('#user-email');

function validateEmailFormat(email) {
  // Validation logic
}

async function fetchUserProfile(userId) {
  // API call
}
```

**Don't:**

```javascript
// Unclear, abbreviated names
const btn = document.querySelector('#submit-button');
const inp = document.querySelector('#user-email');

function valEmail(e) {
  // Validation logic
}

async function getUser(id) {
  // API call
}
```

### Organize File Structure

Keep related files together and separate concerns logically.

**Do:**

```
src/
├── components/
│   ├── user-profile/
│   │   ├── user-profile.js
│   │   ├── user-profile.css
│   │   └── user-profile.test.js
│   └── settings-panel/
│       ├── settings-panel.js
│       ├── settings-panel.css
│       └── settings-panel.test.js
├── utils/
│   ├── validation.js
│   └── api.js
└── styles/
    └── theme.css
```

**Don't:**

```
src/
├── user-profile.js
├── settings-panel.js
├── user-profile.css
├── settings-panel.css
├── validation.js
├── api.js
└── theme.css
```

### Document Your Code

Write clear comments and documentation for complex logic and public APIs.

**Do:**

```javascript
/**
 * Validates an email address format.
 * @param {string} email - The email address to validate
 * @returns {boolean} True if valid, false otherwise
 */
function validateEmail(email) {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}

/**
 * User profile component that displays user information
 * and allows editing.
 *
 * @fires user-updated - Fired when user information is saved
 * @property {Object} user - The user object to display
 * @property {boolean} editable - Whether the profile can be edited
 */
class UserProfile extends HTMLElement {
  // Implementation
}
```

**Don't:**

```javascript
// No documentation
function validateEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

class UserProfile extends HTMLElement {
  // No documentation
}
```

### Use Constants for Magic Values

Define constants for repeated values and configuration.

**Do:**

```javascript
const API_ENDPOINT = 'https://api.example.com/v1';
const MAX_RETRY_ATTEMPTS = 3;
const TIMEOUT_DURATION = 5000;

async function fetchData(endpoint) {
  const url = `${API_ENDPOINT}${endpoint}`;
  const response = await fetch(url, {
    timeout: TIMEOUT_DURATION
  });
  return response.json();
}
```

**Don't:**

```javascript
async function fetchData(endpoint) {
  const url = `https://api.example.com/v1${endpoint}`;
  const response = await fetch(url, {
    timeout: 5000
  });
  return response.json();
}
```

## Testing

### Write Unit Tests

Test individual components and functions in isolation.

**Do:**

```javascript
import { expect, fixture, html } from '@open-wc/testing';
import '@web-awesome/components/wa-button';

describe('wa-button', () => {
  it('renders with correct text', async () => {
    const el = await fixture(html`
      <wa-button>Click me</wa-button>
    `);

    expect(el.textContent).to.equal('Click me');
  });

  it('emits wa-click event when clicked', async () => {
    const el = await fixture(html`
      <wa-button>Click me</wa-button>
    `);

    let clicked = false;
    el.addEventListener('wa-click', () => {
      clicked = true;
    });

    el.click();
    expect(clicked).to.be.true;
  });

  it('can be disabled', async () => {
    const el = await fixture(html`
      <wa-button disabled>Click me</wa-button>
    `);

    expect(el.disabled).to.be.true;
  });
});
```

**Don't:**

```javascript
// No tests
```

### Test Integration Scenarios

Test how components work together in realistic scenarios.

**Do:**

```javascript
describe('User form integration', () => {
  it('validates and submits form data', async () => {
    const form = await fixture(html`
      <form>
        <wa-input name="email" type="email" required></wa-input>
        <wa-input name="password" type="password" required></wa-input>
        <wa-button type="submit">Submit</wa-button>
      </form>
    `);

    const email = form.querySelector('[name="email"]');
    const password = form.querySelector('[name="password"]');
    const button = form.querySelector('wa-button');

    // Test invalid state
    email.value = 'invalid';
    password.value = 'short';
    expect(form.reportValidity()).to.be.false;

    // Test valid state
    email.value = 'user@example.com';
    password.value = 'validpassword123';
    expect(form.reportValidity()).to.be.true;

    // Test submission
    let submitted = false;
    form.addEventListener('submit', (e) => {
      e.preventDefault();
      submitted = true;
    });

    button.click();
    expect(submitted).to.be.true;
  });
});
```

**Don't:**

```javascript
// Only testing isolated components, no integration
```

### Test Accessibility

Ensure components meet accessibility standards.

**Do:**

```javascript
import { expect, fixture, html } from '@open-wc/testing';
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

describe('Accessibility', () => {
  it('button has no accessibility violations', async () => {
    const el = await fixture(html`
      <wa-button>Click me</wa-button>
    `);

    const results = await axe(el);
    expect(results).toHaveNoViolations();
  });

  it('icon button has accessible label', async () => {
    const el = await fixture(html`
      <wa-icon-button name="close" label="Close"></wa-icon-button>
    `);

    expect(el.getAttribute('label')).to.equal('Close');

    const results = await axe(el);
    expect(results).toHaveNoViolations();
  });

  it('supports keyboard navigation', async () => {
    const el = await fixture(html`
      <wa-button>Click me</wa-button>
    `);

    let clicked = false;
    el.addEventListener('wa-click', () => {
      clicked = true;
    });

    // Simulate Enter key
    el.dispatchEvent(new KeyboardEvent('keydown', { key: 'Enter' }));
    expect(clicked).to.be.true;
  });
});
```

**Don't:**

```javascript
// No accessibility testing
```

### Test Error Scenarios

Test how components handle errors and edge cases.

**Do:**

```javascript
describe('Error handling', () => {
  it('handles API errors gracefully', async () => {
    const component = await fixture(html`
      <user-profile user-id="123"></user-profile>
    `);

    // Mock API failure
    global.fetch = () => Promise.reject(new Error('Network error'));

    await component.loadUserData();

    // Component should display error message
    const errorMessage = component.shadowRoot.querySelector('.error-message');
    expect(errorMessage).to.exist;
    expect(errorMessage.textContent).to.include('Unable to load user data');
  });

  it('validates required fields', async () => {
    const input = await fixture(html`
      <wa-input required></wa-input>
    `);

    // Empty value should be invalid
    expect(input.checkValidity()).to.be.false;

    // With value should be valid
    input.value = 'test';
    expect(input.checkValidity()).to.be.true;
  });
});
```

**Don't:**

```javascript
// Only testing happy path
```

## Examples

### Good Pattern: Form with Validation

```html
<form id="contact-form">
  <wa-input
    name="name"
    label="Full Name"
    required
    minlength="2"
  ></wa-input>

  <wa-input
    name="email"
    type="email"
    label="Email Address"
    required
  ></wa-input>

  <wa-textarea
    name="message"
    label="Message"
    required
    minlength="10"
    rows="5"
  ></wa-textarea>

  <wa-button type="submit" variant="primary">
    Send Message
  </wa-button>
</form>

<script>
  const form = document.getElementById('contact-form');
  const submitButton = form.querySelector('wa-button[type="submit"]');

  form.addEventListener('submit', async (event) => {
    event.preventDefault();

    // Validate form
    if (!form.reportValidity()) {
      return;
    }

    // Show loading state
    submitButton.loading = true;
    submitButton.disabled = true;

    try {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(Object.fromEntries(new FormData(form)))
      });

      if (!response.ok) {
        throw new Error('Failed to submit form');
      }

      // Show success message
      const alert = document.createElement('wa-alert');
      alert.variant = 'success';
      alert.textContent = 'Message sent successfully!';
      form.prepend(alert);

      // Reset form
      form.reset();
    } catch (error) {
      // Show error message
      const alert = document.createElement('wa-alert');
      alert.variant = 'danger';
      alert.textContent = 'Failed to send message. Please try again.';
      form.prepend(alert);
    } finally {
      submitButton.loading = false;
      submitButton.disabled = false;
    }
  });
</script>
```

### Bad Pattern: Form with No Validation

```html
<form id="contact-form">
  <input name="name" placeholder="Name">
  <input name="email" placeholder="Email">
  <textarea name="message" placeholder="Message"></textarea>
  <button type="submit">Send</button>
</form>

<script>
  document.getElementById('contact-form').addEventListener('submit', (e) => {
    e.preventDefault();
    fetch('/api/contact', {
      method: 'POST',
      body: new FormData(e.target)
    });
  });
</script>
```

### Good Pattern: Accessible Dialog

```html
<wa-button id="open-settings">Open Settings</wa-button>

<wa-dialog id="settings-dialog" label="Settings">
  <form>
    <wa-switch name="notifications">
      Enable notifications
    </wa-switch>

    <wa-switch name="dark-mode">
      Dark mode
    </wa-switch>

    <div slot="footer">
      <wa-button variant="default" type="button" id="cancel">
        Cancel
      </wa-button>
      <wa-button variant="primary" type="submit">
        Save
      </wa-button>
    </div>
  </form>
</wa-dialog>

<script>
  const openButton = document.getElementById('open-settings');
  const dialog = document.getElementById('settings-dialog');
  const cancelButton = document.getElementById('cancel');
  const form = dialog.querySelector('form');

  openButton.addEventListener('click', async () => {
    await dialog.show();
  });

  cancelButton.addEventListener('click', () => {
    dialog.hide();
  });

  form.addEventListener('submit', (event) => {
    event.preventDefault();

    // Save settings
    const settings = Object.fromEntries(new FormData(form));
    saveSettings(settings);

    dialog.hide();
  });

  // Handle escape key
  dialog.addEventListener('wa-hide', (event) => {
    if (event.detail.source === 'keyboard') {
      openButton.focus();
    }
  });
</script>
```

### Bad Pattern: Inaccessible Dialog

```html
<button onclick="showDialog()">Settings</button>

<div id="dialog" style="display: none;">
  <div>
    <input type="checkbox" id="notif"> Notifications
    <input type="checkbox" id="dark"> Dark mode
  </div>
  <button onclick="saveSettings()">Save</button>
</div>

<script>
  function showDialog() {
    document.getElementById('dialog').style.display = 'block';
  }

  function saveSettings() {
    document.getElementById('dialog').style.display = 'none';
  }
</script>
```

### Good Pattern: Responsive Data Table

```html
<wa-table>
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
        <th>Role</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>John Doe</td>
        <td>john@example.com</td>
        <td>Admin</td>
        <td>
          <wa-icon-button
            name="edit"
            label="Edit user"
            data-user-id="1"
          ></wa-icon-button>
          <wa-icon-button
            name="trash"
            label="Delete user"
            data-user-id="1"
          ></wa-icon-button>
        </td>
      </tr>
    </tbody>
  </table>
</wa-table>

<script>
  const table = document.querySelector('wa-table');

  // Use event delegation
  table.addEventListener('wa-click', (event) => {
    const button = event.target;
    if (!button.matches('wa-icon-button')) return;

    const userId = button.dataset.userId;
    const action = button.name;

    if (action === 'edit') {
      editUser(userId);
    } else if (action === 'trash') {
      confirmDeleteUser(userId);
    }
  });
</script>
```

### Bad Pattern: Non-Accessible Table

```html
<table>
  <tr>
    <td>Name</td>
    <td>Email</td>
    <td>Role</td>
    <td>Actions</td>
  </tr>
  <tr>
    <td>John Doe</td>
    <td>john@example.com</td>
    <td>Admin</td>
    <td>
      <button onclick="editUser(1)">Edit</button>
      <button onclick="deleteUser(1)">Delete</button>
    </td>
  </tr>
</table>
```

## Related Links

- [Getting Started](/getting-started/installation)
- [Component Guidelines](/guides/component-guidelines)
- [Accessibility Guide](/guides/accessibility)
- [Theming Guide](/guides/theming)
- [Form Validation](/guides/form-validation)
- [Performance Optimization](/guides/performance)
- [Security Best Practices](/guides/security)
- [Testing Components](/guides/testing)
