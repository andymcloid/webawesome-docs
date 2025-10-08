# Details

An expandable disclosure widget for showing and hiding content.

## Overview

The `<wa-details>` component creates an accessible disclosure widget that allows users to show and hide additional content. It's similar to the native HTML `<details>` element but with enhanced styling and functionality. Perfect for FAQs, settings panels, and progressive disclosure patterns.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/details/details.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple details -->
<wa-details summary="Click to expand">
  This content is hidden by default and revealed when clicked.
</wa-details>

<!-- Open by default -->
<wa-details summary="This is open by default" open>
  This content is visible on page load.
</wa-details>

<!-- Disabled -->
<wa-details summary="This is disabled" disabled>
  This content cannot be toggled.
</wa-details>
```

## Summary

Set the summary text with the `summary` attribute:

```html
<wa-details summary="What is WebAwesome?">
  <p>WebAwesome is a component library built on web components, providing accessible and customizable UI elements.</p>
</wa-details>
```

### Custom Summary Content

Use the `summary` slot for rich content:

```html
<wa-details>
  <div slot="summary" style="display: flex; align-items: center; gap: 0.5rem;">
    <wa-icon name="help-circle"></wa-icon>
    <strong>Need help?</strong>
  </div>
  <p>Contact our support team at support@example.com</p>
</wa-details>
```

## Open State

Control the expanded state:

```html
<!-- Collapsed by default -->
<wa-details summary="Collapsed">
  Hidden content
</wa-details>

<!-- Expanded by default -->
<wa-details summary="Expanded" open>
  Visible content
</wa-details>
```

## Disabled State

Prevent toggling:

```html
<wa-details summary="Disabled Details" disabled>
  This content cannot be toggled.
</wa-details>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `summary` | string | - | No | The summary text (can also use summary slot) |
| `open` | boolean | `false` | No | Whether the details are expanded |
| `disabled` | boolean | `false` | No | Disable toggling |

## Examples

### FAQ Section

```html
<div style="max-width: 800px; margin: 0 auto;">
  <h2>Frequently Asked Questions</h2>

  <wa-details summary="What payment methods do you accept?">
    <p>We accept all major credit cards (Visa, MasterCard, American Express), PayPal, and bank transfers for enterprise customers.</p>
  </wa-details>

  <wa-details summary="How long does shipping take?">
    <p>Standard shipping typically takes 5-7 business days. Express shipping (2-3 business days) is available for an additional fee.</p>
  </wa-details>

  <wa-details summary="What is your return policy?">
    <p>We offer a 30-day money-back guarantee. Items must be returned in their original condition with all packaging and tags intact.</p>
  </wa-details>

  <wa-details summary="Do you offer international shipping?">
    <p>Yes, we ship to over 50 countries worldwide. International shipping times vary by destination but typically range from 10-21 business days.</p>
  </wa-details>

  <wa-details summary="How can I track my order?">
    <p>Once your order ships, you'll receive a tracking number via email. You can use this number on our website or the carrier's website to track your package.</p>
  </wa-details>
</div>

<style>
  wa-details {
    margin-bottom: 1rem;
  }
</style>
```

### Settings Panels

```html
<div style="max-width: 600px;">
  <h2>Account Settings</h2>

  <wa-details summary="Profile Information" open>
    <div style="padding: 1rem;">
      <wa-input label="Full Name" value="John Doe" style="margin-bottom: 1rem;"></wa-input>
      <wa-input label="Email" type="email" value="john@example.com" style="margin-bottom: 1rem;"></wa-input>
      <wa-input label="Phone" type="tel" value="+1 (555) 123-4567" style="margin-bottom: 1rem;"></wa-input>
      <wa-button variant="primary">Save Changes</wa-button>
    </div>
  </wa-details>

  <wa-details summary="Security">
    <div style="padding: 1rem;">
      <wa-input label="Current Password" type="password" style="margin-bottom: 1rem;"></wa-input>
      <wa-input label="New Password" type="password" style="margin-bottom: 1rem;"></wa-input>
      <wa-input label="Confirm Password" type="password" style="margin-bottom: 1rem;"></wa-input>
      <wa-button variant="primary">Update Password</wa-button>
    </div>
  </wa-details>

  <wa-details summary="Notification Preferences">
    <div style="padding: 1rem;">
      <wa-checkbox checked>Email notifications</wa-checkbox>
      <wa-checkbox checked>Push notifications</wa-checkbox>
      <wa-checkbox>SMS notifications</wa-checkbox>
      <wa-checkbox checked>Weekly newsletter</wa-checkbox>
    </div>
  </wa-details>

  <wa-details summary="Privacy Settings">
    <div style="padding: 1rem;">
      <wa-switch checked>Profile visibility</wa-switch>
      <wa-switch checked>Show email publicly</wa-switch>
      <wa-switch>Allow search engines to index profile</wa-switch>
    </div>
  </wa-details>
</wa-details>

<style>
  wa-details {
    margin-bottom: 0.5rem;
  }

  wa-checkbox, wa-switch {
    display: block;
    margin-bottom: 0.75rem;
  }
</style>
```

### Product Details

```html
<wa-card style="max-width: 600px;">
  <img
    slot="image"
    src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e"
    alt="Wireless headphones"
    style="width: 100%; height: 300px; object-fit: cover;">

  <h2>Premium Wireless Headphones</h2>
  <div style="font-size: 1.5rem; color: #2ecc71; margin-bottom: 1rem;">$199.99</div>

  <wa-details summary="Product Description" open>
    <p>Experience premium sound quality with our flagship wireless headphones. Featuring active noise cancellation, 30-hour battery life, and premium comfort padding.</p>
  </wa-details>

  <wa-details summary="Technical Specifications">
    <ul>
      <li><strong>Driver Size:</strong> 40mm</li>
      <li><strong>Frequency Response:</strong> 20Hz - 20kHz</li>
      <li><strong>Bluetooth:</strong> 5.0</li>
      <li><strong>Battery Life:</strong> 30 hours</li>
      <li><strong>Weight:</strong> 250g</li>
      <li><strong>Charging:</strong> USB-C fast charging</li>
    </ul>
  </wa-details>

  <wa-details summary="What's in the Box">
    <ul>
      <li>Wireless Headphones</li>
      <li>USB-C Charging Cable</li>
      <li>3.5mm Audio Cable</li>
      <li>Carrying Case</li>
      <li>User Manual</li>
    </ul>
  </wa-details>

  <wa-details summary="Shipping & Returns">
    <p><strong>Shipping:</strong> Free standard shipping on orders over $50. Express shipping available.</p>
    <p><strong>Returns:</strong> 30-day money-back guarantee. Products must be in original condition.</p>
  </wa-details>

  <wa-button slot="footer" variant="primary" style="width: 100%;">Add to Cart</wa-button>
</wa-card>

<style>
  wa-details {
    margin-bottom: 0.5rem;
  }
</style>
```

### Nested Details

```html
<wa-details summary="Chapter 1: Getting Started" open>
  <p>This chapter covers the basics of getting started with our platform.</p>

  <wa-details summary="1.1 Installation">
    <p>Learn how to install the software on your system.</p>
    <pre><code>npm install @example/package</code></pre>
  </wa-details>

  <wa-details summary="1.2 Configuration">
    <p>Configure your environment with these settings.</p>
    <pre><code>{
  "apiKey": "your-api-key",
  "environment": "production"
}</code></pre>
  </wa-details>

  <wa-details summary="1.3 First Steps">
    <p>Take your first steps with a simple example.</p>
    <pre><code>import { App } from '@example/package';

const app = new App();
app.start();</code></pre>
  </wa-details>
</wa-details>

<wa-details summary="Chapter 2: Advanced Topics">
  <p>Dive deeper into advanced features and capabilities.</p>

  <wa-details summary="2.1 Performance Optimization">
    <p>Learn how to optimize your application for maximum performance.</p>
  </wa-details>

  <wa-details summary="2.2 Security Best Practices">
    <p>Implement security best practices to protect your application.</p>
  </wa-details>
</wa-details>
```

### Collapsible Content Sections

```html
<div style="max-width: 800px;">
  <h1>Documentation</h1>

  <wa-details summary="Introduction" open>
    <div style="padding: 1rem;">
      <p>Welcome to our comprehensive documentation. This guide will help you get started and master all features of our platform.</p>
    </div>
  </wa-details>

  <wa-details summary="Quick Start Guide">
    <div style="padding: 1rem;">
      <h3>Getting Started in 3 Steps</h3>
      <ol>
        <li>Create an account</li>
        <li>Complete your profile</li>
        <li>Start your first project</li>
      </ol>
    </div>
  </wa-details>

  <wa-details summary="API Reference">
    <div style="padding: 1rem;">
      <h3>Available Endpoints</h3>
      <ul>
        <li><code>GET /api/users</code> - Retrieve user list</li>
        <li><code>POST /api/users</code> - Create new user</li>
        <li><code>PUT /api/users/:id</code> - Update user</li>
        <li><code>DELETE /api/users/:id</code> - Delete user</li>
      </ul>
    </div>
  </wa-details>

  <wa-details summary="Troubleshooting">
    <div style="padding: 1rem;">
      <h3>Common Issues</h3>
      <p><strong>Q: Login not working?</strong></p>
      <p>A: Clear your browser cache and cookies, then try again.</p>

      <p><strong>Q: Upload failed?</strong></p>
      <p>A: Check that your file is under 10MB and in a supported format.</p>
    </div>
  </wa-details>
</div>

<style>
  wa-details {
    margin-bottom: 0.5rem;
  }
</style>
```

### Programmatic Control

```html
<div style="max-width: 600px;">
  <div style="margin-bottom: 1rem; display: flex; gap: 0.5rem;">
    <wa-button id="openAll">Open All</wa-button>
    <wa-button id="closeAll">Close All</wa-button>
    <wa-button id="toggle1">Toggle First</wa-button>
  </div>

  <wa-details id="detail1" summary="Section 1">
    <p>Content for section 1</p>
  </wa-details>

  <wa-details id="detail2" summary="Section 2">
    <p>Content for section 2</p>
  </wa-details>

  <wa-details id="detail3" summary="Section 3">
    <p>Content for section 3</p>
  </wa-details>
</div>

<script>
  const openAllBtn = document.getElementById('openAll');
  const closeAllBtn = document.getElementById('closeAll');
  const toggle1Btn = document.getElementById('toggle1');
  const detail1 = document.getElementById('detail1');

  openAllBtn.addEventListener('click', () => {
    document.querySelectorAll('wa-details').forEach(detail => {
      detail.open = true;
    });
  });

  closeAllBtn.addEventListener('click', () => {
    document.querySelectorAll('wa-details').forEach(detail => {
      detail.open = false;
    });
  });

  toggle1Btn.addEventListener('click', () => {
    detail1.open = !detail1.open;
  });
</script>

<style>
  wa-details {
    margin-bottom: 0.5rem;
  }
</style>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Expand the details | `void` |
| `hide()` | Collapse the details | `void` |

### Method Examples

```javascript
const details = document.querySelector('wa-details');

// Show details
details.show();

// Hide details
details.hide();

// Toggle based on condition
if (someCondition) {
  details.show();
} else {
  details.hide();
}

// Show with delay
setTimeout(() => {
  details.show();
}, 1000);
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the details open (before animation) | - |
| `wa-after-show` | Emitted after the details open (after animation) | - |
| `wa-hide` | Emitted when the details close (before animation) | - |
| `wa-after-hide` | Emitted after the details close (after animation) | - |

### Event Examples

```javascript
const details = document.querySelector('wa-details');

// Listen for show event
details.addEventListener('wa-show', () => {
  console.log('Details starting to open');
});

// Listen for after-show event
details.addEventListener('wa-after-show', () => {
  console.log('Details fully opened');
  // Good place to load content or trigger animations
});

// Listen for hide event
details.addEventListener('wa-hide', () => {
  console.log('Details starting to close');
});

// Listen for after-hide event
details.addEventListener('wa-after-hide', () => {
  console.log('Details fully closed');
});

// Track analytics
details.addEventListener('wa-show', () => {
  gtag('event', 'details_opened', {
    summary: details.summary
  });
});

// Prevent closing under certain conditions
details.addEventListener('wa-hide', (event) => {
  if (formHasUnsavedChanges()) {
    event.preventDefault();
    alert('Please save your changes first');
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The details content |
| `summary` | The summary/header content |
| `icon` | Custom expand/collapse icon |

### Slot Examples

```html
<!-- Custom summary with icon -->
<wa-details>
  <div slot="summary" style="display: flex; align-items: center; gap: 0.5rem;">
    <wa-icon name="info-circle"></wa-icon>
    <strong>Important Information</strong>
    <wa-badge variant="warning">New</wa-badge>
  </div>
  <p>This is important information you should know about.</p>
</wa-details>

<!-- Custom expand/collapse icon -->
<wa-details>
  <wa-icon slot="icon" name="plus-circle"></wa-icon>
  <span slot="summary">Custom Icon</span>
  <p>Content with custom expand icon</p>
</wa-details>
```

## CSS Parts

Use CSS parts to style internal details elements:

```css
/* Style the base container */
wa-details::part(base) {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
}

/* Style the header/summary */
wa-details::part(header) {
  background-color: #f5f5f5;
  padding: 1rem;
  font-weight: 500;
}

/* Style the summary text */
wa-details::part(summary) {
  font-size: 1rem;
}

/* Style the expand/collapse icon */
wa-details::part(summary-icon) {
  color: #666;
  transition: transform 0.3s;
}

/* Rotate icon when open */
wa-details[open]::part(summary-icon) {
  transform: rotate(90deg);
}

/* Style the content area */
wa-details::part(content) {
  padding: 1rem;
}
```

## Customization

### Custom Styling

```css
/* Card-like appearance */
wa-details {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  overflow: hidden;
}

wa-details::part(header) {
  background: linear-gradient(to right, #667eea, #764ba2);
  color: white;
  padding: 1rem;
}

wa-details::part(header):hover {
  background: linear-gradient(to right, #5568d3, #6a3f8f);
}

wa-details::part(content) {
  padding: 1.5rem;
  background-color: #fafafa;
}

/* Animated border */
wa-details[open] {
  border-color: #667eea;
  box-shadow: 0 2px 8px rgba(102, 126, 234, 0.2);
}

/* Custom icon rotation */
wa-details::part(summary-icon) {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

wa-details[open]::part(summary-icon) {
  transform: rotate(180deg);
}
```

### Accordion Style

```css
/* Remove spacing between details for accordion look */
wa-details {
  border: 1px solid #ddd;
  border-bottom: none;
  margin: 0;
}

wa-details:first-of-type {
  border-radius: 8px 8px 0 0;
}

wa-details:last-of-type {
  border-radius: 0 0 8px 8px;
  border-bottom: 1px solid #ddd;
}

wa-details::part(header) {
  border-bottom: 1px solid transparent;
}

wa-details[open]::part(header) {
  border-bottom-color: #ddd;
}
```

## Best Practices

- ✅ Use clear, descriptive summary text
- ✅ Group related content in details sections
- ✅ Keep content sections focused and concise
- ✅ Use for progressive disclosure of complex information
- ✅ Consider initial open state for important content
- ✅ Provide visual feedback for interactive states
- ❌ Don't nest details too deeply (max 2-3 levels)
- ❌ Avoid putting critical content only in collapsed sections
- ❌ Don't use for navigation (use menu/tree instead)
- ❌ Avoid very long content sections

## Accessibility

- Details automatically includes appropriate ARIA attributes
- Keyboard accessible (Enter/Space to toggle)
- Screen readers announce expand/collapse state
- Focus management for keyboard navigation
- Respects `prefers-reduced-motion` for animations

```html
<!-- Accessible details with proper labeling -->
<wa-details
  summary="Accessibility Features"
  aria-label="Information about accessibility features">
  <p>Our platform includes comprehensive accessibility support including keyboard navigation, screen reader compatibility, and high contrast modes.</p>
</wa-details>
```

### Keyboard Navigation

- Enter/Space: Toggle open/closed
- Tab: Move focus to next focusable element
- Shift + Tab: Move focus to previous focusable element

## Troubleshooting

### Content Not Animating

**Problem:** Details content appears/disappears without animation

**Solution:** Ensure CSS transitions are not disabled

```css
/* Enable smooth animations */
wa-details::part(content) {
  transition: all 0.3s ease;
}
```

### Icon Not Rotating

**Problem:** Expand/collapse icon doesn't rotate

**Solution:** Add rotation styles to the icon part

```css
wa-details::part(summary-icon) {
  transition: transform 0.3s;
}

wa-details[open]::part(summary-icon) {
  transform: rotate(90deg);
}
```

### Events Not Firing

**Problem:** Show/hide events not being triggered

**Solution:** Ensure you're listening for the correct event names

```javascript
// ✅ Correct event names
details.addEventListener('wa-show', handler);
details.addEventListener('wa-after-show', handler);

// ❌ These won't work
details.addEventListener('show', handler);
details.addEventListener('open', handler);
```

## Related

- [Accordion](./accordion.md)
- [Card](./card.md)
- [Dialog](./dialog.md)
- [Drawer](./drawer.md)
