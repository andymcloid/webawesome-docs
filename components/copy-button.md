# Copy Button

Copy buttons allow users to quickly copy text content to their clipboard.

## Overview

The `<wa-copy-button>` component provides an easy way to copy text to the clipboard with visual feedback. It automatically shows success or error states and includes customizable labels for different states.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/copy-button/copy-button.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Copy specific value -->
<wa-copy-button value="Text to copy"></wa-copy-button>

<!-- Copy from another element -->
<div id="content">This is the content to copy</div>
<wa-copy-button from="content"></wa-copy-button>

<!-- With custom labels -->
<wa-copy-button
  value="Hello, World!"
  copy-label="Copy to Clipboard"
  success-label="Copied!"
  error-label="Failed to Copy">
</wa-copy-button>
```

## Copy from Value

Use the `value` attribute to specify the text to copy directly:

```html
<!-- Simple text -->
<wa-copy-button value="Hello, World!"></wa-copy-button>

<!-- API key example -->
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <code>pk_live_123456789abcdef</code>
  <wa-copy-button value="pk_live_123456789abcdef"></wa-copy-button>
</div>

<!-- Email address -->
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <span>support@example.com</span>
  <wa-copy-button value="support@example.com"></wa-copy-button>
</div>
```

## Copy from Element

Use the `from` attribute to copy content from another element:

```html
<!-- Copy from paragraph -->
<p id="paragraph">This is a paragraph with some content to copy.</p>
<wa-copy-button from="paragraph"></wa-copy-button>

<!-- Copy from code block -->
<pre id="code">
function greet(name) {
  return `Hello, ${name}!`;
}
</pre>
<wa-copy-button from="code"></wa-copy-button>

<!-- Copy from input -->
<wa-input id="email" value="user@example.com" readonly></wa-input>
<wa-copy-button from="email"></wa-copy-button>
```

## Custom Labels

Customize the button text for different states:

```html
<wa-copy-button
  value="Text to copy"
  copy-label="Copy"
  success-label="Copied!"
  error-label="Error">
</wa-copy-button>

<!-- Icon-only button with tooltips -->
<wa-copy-button
  value="Text to copy"
  copy-label=""
  success-label=""
  error-label="">
</wa-copy-button>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | - | No* | The text to copy to clipboard |
| `from` | string | - | No* | ID of element whose content should be copied |
| `copy-label` | string | `'Copy'` | No | Label shown in default state |
| `success-label` | string | `'Copied'` | No | Label shown after successful copy |
| `error-label` | string | `'Error'` | No | Label shown when copy fails |

*Note: Either `value` or `from` must be provided

## Examples

### Code Snippet with Copy

```html
<div style="position: relative; background: #1f2937; color: #f9fafb; padding: 1rem; border-radius: 0.5rem;">
  <wa-copy-button
    from="codeSnippet"
    style="position: absolute; top: 0.5rem; right: 0.5rem;">
  </wa-copy-button>

  <pre id="codeSnippet" style="margin: 0;"><code>npm install webawesome

import 'webawesome/components/button/button.js';

const button = document.querySelector('wa-button');
button.addEventListener('click', () => {
  console.log('Button clicked!');
});</code></pre>
</div>
```

### API Key Display

```html
<wa-card>
  <div slot="header">
    <h3>API Credentials</h3>
  </div>

  <div style="padding: 1rem;">
    <div style="margin-bottom: 1rem;">
      <label style="display: block; font-weight: 600; margin-bottom: 0.5rem;">
        Public Key
      </label>
      <div style="display: flex; align-items: center; gap: 0.5rem;">
        <code style="flex: 1; padding: 0.5rem; background: #f3f4f6; border-radius: 0.25rem;">
          pk_live_123456789abcdef
        </code>
        <wa-copy-button value="pk_live_123456789abcdef"></wa-copy-button>
      </div>
    </div>

    <div>
      <label style="display: block; font-weight: 600; margin-bottom: 0.5rem;">
        Secret Key
      </label>
      <div style="display: flex; align-items: center; gap: 0.5rem;">
        <code style="flex: 1; padding: 0.5rem; background: #f3f4f6; border-radius: 0.25rem;">
          sk_live_fedcba987654321
        </code>
        <wa-copy-button value="sk_live_fedcba987654321"></wa-copy-button>
      </div>
    </div>
  </div>

  <wa-alert slot="footer" variant="warning" open>
    <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
    Keep your secret key confidential. Do not share it publicly.
  </wa-alert>
</wa-card>
```

### Share Link

```html
<wa-card>
  <div slot="header">
    <h3>Share this Page</h3>
  </div>

  <div style="padding: 1rem;">
    <p style="color: #6b7280; margin-bottom: 1rem;">
      Copy the link below to share this page with others.
    </p>

    <div style="display: flex; gap: 0.5rem;">
      <wa-input
        id="shareLink"
        value="https://example.com/page/123"
        readonly
        style="flex: 1;">
      </wa-input>
      <wa-copy-button from="shareLink" copy-label="Copy Link"></wa-copy-button>
    </div>
  </div>
</wa-card>
```

### Color Palette

```html
<div class="color-palette">
  <h3>Brand Colors</h3>

  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; margin-top: 1rem;">
    <div style="border: 1px solid #e5e7eb; border-radius: 0.5rem; overflow: hidden;">
      <div style="height: 100px; background: #3b82f6;"></div>
      <div style="padding: 1rem;">
        <div style="display: flex; justify-content: space-between; align-items: center;">
          <span style="font-weight: 600;">Primary Blue</span>
          <wa-copy-button value="#3b82f6" copy-label=""></wa-copy-button>
        </div>
        <code style="color: #6b7280; font-size: 0.875rem;">#3b82f6</code>
      </div>
    </div>

    <div style="border: 1px solid #e5e7eb; border-radius: 0.5rem; overflow: hidden;">
      <div style="height: 100px; background: #10b981;"></div>
      <div style="padding: 1rem;">
        <div style="display: flex; justify-content: space-between; align-items: center;">
          <span style="font-weight: 600;">Success Green</span>
          <wa-copy-button value="#10b981" copy-label=""></wa-copy-button>
        </div>
        <code style="color: #6b7280; font-size: 0.875rem;">#10b981</code>
      </div>
    </div>

    <div style="border: 1px solid #e5e7eb; border-radius: 0.5rem; overflow: hidden;">
      <div style="height: 100px; background: #ef4444;"></div>
      <div style="padding: 1rem;">
        <div style="display: flex; justify-content: space-between; align-items: center;">
          <span style="font-weight: 600;">Error Red</span>
          <wa-copy-button value="#ef4444" copy-label=""></wa-copy-button>
        </div>
        <code style="color: #6b7280; font-size: 0.875rem;">#ef4444</code>
      </div>
    </div>
  </div>
</div>
```

### Command Line Instructions

```html
<div class="terminal-block">
  <h4>Installation</h4>

  <div style="background: #1f2937; color: #f9fafb; padding: 1rem; border-radius: 0.5rem; position: relative; margin-bottom: 1rem;">
    <wa-copy-button
      from="npmInstall"
      copy-label="Copy"
      style="position: absolute; top: 0.5rem; right: 0.5rem;">
    </wa-copy-button>
    <pre id="npmInstall" style="margin: 0;"><code>npm install webawesome</code></pre>
  </div>

  <h4>Import Component</h4>

  <div style="background: #1f2937; color: #f9fafb; padding: 1rem; border-radius: 0.5rem; position: relative;">
    <wa-copy-button
      from="importCode"
      copy-label="Copy"
      style="position: absolute; top: 0.5rem; right: 0.5rem;">
    </wa-copy-button>
    <pre id="importCode" style="margin: 0;"><code>import 'webawesome/components/copy-button/copy-button.js';</code></pre>
  </div>
</div>
```

### Contact Information

```html
<wa-card>
  <div slot="header">
    <h3>Contact Us</h3>
  </div>

  <div style="padding: 1rem;">
    <div style="display: flex; flex-direction: column; gap: 1rem;">
      <div>
        <label style="display: block; font-weight: 600; margin-bottom: 0.5rem;">
          <wa-icon name="envelope"></wa-icon> Email
        </label>
        <div style="display: flex; align-items: center; gap: 0.5rem;">
          <span style="flex: 1;">support@example.com</span>
          <wa-copy-button value="support@example.com" copy-label=""></wa-copy-button>
        </div>
      </div>

      <div>
        <label style="display: block; font-weight: 600; margin-bottom: 0.5rem;">
          <wa-icon name="phone"></wa-icon> Phone
        </label>
        <div style="display: flex; align-items: center; gap: 0.5rem;">
          <span style="flex: 1;">+1 (555) 123-4567</span>
          <wa-copy-button value="+1 (555) 123-4567" copy-label=""></wa-copy-button>
        </div>
      </div>

      <div>
        <label style="display: block; font-weight: 600; margin-bottom: 0.5rem;">
          <wa-icon name="map-pin"></wa-icon> Address
        </label>
        <div style="display: flex; align-items: start; gap: 0.5rem;">
          <span style="flex: 1;">123 Main Street, Suite 100, San Francisco, CA 94102</span>
          <wa-copy-button value="123 Main Street, Suite 100, San Francisco, CA 94102" copy-label=""></wa-copy-button>
        </div>
      </div>
    </div>
  </div>
</wa-card>
```

### Custom Feedback

```html
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <code id="customCode">const result = calculate(42);</code>
  <wa-copy-button id="customCopy" from="customCode"></wa-copy-button>
</div>

<div id="feedback" style="margin-top: 0.5rem; min-height: 1.5rem;"></div>

<script>
  const copyButton = document.getElementById('customCopy');
  const feedback = document.getElementById('feedback');

  copyButton.addEventListener('wa-copy', (event) => {
    feedback.textContent = `Copied: "${event.detail.value}"`;
    feedback.style.color = '#10b981';

    setTimeout(() => {
      feedback.textContent = '';
    }, 3000);
  });

  copyButton.addEventListener('wa-error', () => {
    feedback.textContent = 'Failed to copy. Please try again.';
    feedback.style.color = '#ef4444';
  });
</script>
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-copy` | Emitted when content is successfully copied | `{ value: string }` |
| `wa-error` | Emitted when copy operation fails | - |

### Event Examples

```javascript
const copyButton = document.querySelector('wa-copy-button');

// Handle successful copy
copyButton.addEventListener('wa-copy', (event) => {
  console.log('Copied to clipboard:', event.detail.value);

  // Show notification
  showNotification('Content copied to clipboard!');

  // Track analytics
  analytics.track('content_copied', {
    value: event.detail.value
  });
});

// Handle copy error
copyButton.addEventListener('wa-error', () => {
  console.error('Failed to copy to clipboard');

  // Show error message
  showErrorNotification('Failed to copy. Please try again.');
});
```

## CSS Parts

Use CSS parts to customize the copy button appearance:

```css
/* Style the base button */
wa-copy-button::part(button) {
  background-color: #3b82f6;
  color: white;
  border: none;
  border-radius: 0.375rem;
  padding: 0.5rem 1rem;
}

wa-copy-button::part(button):hover {
  background-color: #2563eb;
}

/* Style success state */
wa-copy-button[status="success"]::part(button) {
  background-color: #10b981;
}

/* Style error state */
wa-copy-button[status="error"]::part(button) {
  background-color: #ef4444;
}
```

## Customization

### Icon-Only Button

```css
/* Hide label, show only icon */
wa-copy-button.icon-only::part(label) {
  display: none;
}

wa-copy-button.icon-only::part(button) {
  width: 2rem;
  height: 2rem;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### Custom Colors

```css
/* Brand-colored copy button */
wa-copy-button.brand::part(button) {
  background-color: #6366f1;
  color: white;
}

/* Outline style */
wa-copy-button.outline::part(button) {
  background-color: transparent;
  border: 2px solid #6366f1;
  color: #6366f1;
}
```

### Animated Success

```css
@keyframes success-pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

wa-copy-button[status="success"]::part(button) {
  animation: success-pulse 0.3s ease;
}
```

## Best Practices

- ✅ Place copy buttons near the content they copy
- ✅ Provide visual feedback after copying
- ✅ Use appropriate labels that describe what's being copied
- ✅ Consider icon-only buttons for compact layouts
- ✅ Show the actual value being copied when possible
- ❌ Don't use copy buttons for sensitive information without warnings
- ❌ Avoid using copy buttons for very long content (provide download instead)
- ❌ Don't hide copy buttons that users might need to find

## Accessibility

- Copy buttons include appropriate ARIA labels
- Success/error states are announced to screen readers
- Keyboard navigation is fully supported
- Use descriptive labels for screen reader context

```html
<!-- Accessible copy button -->
<wa-copy-button
  value="Code snippet"
  aria-label="Copy code snippet to clipboard">
</wa-copy-button>

<!-- With additional context -->
<label id="codeLabel">Installation Command</label>
<wa-copy-button
  value="npm install webawesome"
  aria-labelledby="codeLabel">
</wa-copy-button>
```

## Troubleshooting

### Copy Not Working

**Problem:** Nothing is copied to clipboard

**Solution:** Ensure either `value` or `from` attribute is set correctly

```html
<!-- ✅ Correct -->
<wa-copy-button value="Text to copy"></wa-copy-button>
<div id="content">Text</div>
<wa-copy-button from="content"></wa-copy-button>

<!-- ❌ Missing both attributes -->
<wa-copy-button></wa-copy-button>
```

### Element Not Found

**Problem:** Copy from element doesn't work

**Solution:** Verify the element ID exists and is spelled correctly

```javascript
// Check if element exists
const element = document.getElementById('myElement');
if (!element) {
  console.error('Element with id="myElement" not found');
}
```

### Clipboard Permission Denied

**Problem:** Browser blocks clipboard access

**Solution:** Clipboard API requires secure context (HTTPS) and user interaction

```javascript
// Check clipboard support
if (!navigator.clipboard) {
  console.warn('Clipboard API not available (requires HTTPS)');
}
```

### Success State Not Resetting

**Problem:** Button stays in success state

**Solution:** The button automatically resets after a timeout. If you need manual control, use JavaScript

```javascript
const copyButton = document.querySelector('wa-copy-button');

// Manually reset after custom timeout
copyButton.addEventListener('wa-copy', () => {
  setTimeout(() => {
    // Reset handled automatically by component
  }, 2000);
});
```

## Related

- [Button](./button.md)
- [Input](./input.md)
- [Tooltip](./tooltip.md)
- [Icon](./icon.md)
- [Clipboard Guide](../guides/clipboard.md)
