# Callout

Display important messages, alerts, and notifications with visual emphasis.

## Overview

The `<wa-callout>` component provides a styled container for highlighting important information, warnings, success messages, and other feedback to users. It supports multiple variants, optional close functionality, and icons for enhanced visual communication.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/callout/callout.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default callout -->
<wa-callout>
  This is a basic callout message.
</wa-callout>

<!-- Primary callout -->
<wa-callout variant="primary">
  This is important information you should know.
</wa-callout>

<!-- Success callout -->
<wa-callout variant="success">
  Your changes have been saved successfully!
</wa-callout>

<!-- Warning callout -->
<wa-callout variant="warning">
  Please review your settings before continuing.
</wa-callout>

<!-- Danger callout -->
<wa-callout variant="danger">
  An error occurred while processing your request.
</wa-callout>
```

## Variants

Callouts support multiple semantic variants:

```html
<!-- Primary - General information -->
<wa-callout variant="primary">
  <strong>Pro Tip:</strong> Use keyboard shortcuts to work faster!
</wa-callout>

<!-- Success - Positive feedback -->
<wa-callout variant="success">
  <strong>Success!</strong> Your profile has been updated.
</wa-callout>

<!-- Neutral - Informational (default) -->
<wa-callout variant="neutral">
  <strong>Note:</strong> Maintenance is scheduled for tonight at 2 AM.
</wa-callout>

<!-- Warning - Caution -->
<wa-callout variant="warning">
  <strong>Warning:</strong> This action cannot be undone.
</wa-callout>

<!-- Danger - Error or critical information -->
<wa-callout variant="danger">
  <strong>Error:</strong> Failed to connect to the server.
</wa-callout>
```

## Closable Callouts

Add the `closable` attribute to allow users to dismiss callouts:

```html
<!-- Closable callout -->
<wa-callout closable>
  You can close this message by clicking the X button.
</wa-callout>

<!-- Closable with variant -->
<wa-callout variant="success" closable>
  Your file has been uploaded successfully!
</wa-callout>
```

### Handling Close Events

```html
<wa-callout id="myCallout" variant="warning" closable>
  This is a closable warning message.
</wa-callout>

<script>
  const callout = document.getElementById('myCallout');

  callout.addEventListener('wa-close', () => {
    console.log('Callout was closed');
    // Perform any cleanup or state updates
  });
</script>
```

## With Icons

Add icons to enhance visual communication:

```html
<!-- Information with icon -->
<wa-callout variant="primary">
  <wa-icon slot="icon" name="info-circle"></wa-icon>
  <strong>Did you know?</strong> You can customize your dashboard layout.
</wa-callout>

<!-- Success with icon -->
<wa-callout variant="success">
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  <strong>Complete!</strong> All tasks have been finished.
</wa-callout>

<!-- Warning with icon -->
<wa-callout variant="warning">
  <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
  <strong>Attention:</strong> Your subscription expires in 3 days.
</wa-callout>

<!-- Danger with icon -->
<wa-callout variant="danger">
  <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
  <strong>Error:</strong> Invalid credentials provided.
</wa-callout>

<!-- Neutral with icon -->
<wa-callout variant="neutral">
  <wa-icon slot="icon" name="lightbulb"></wa-icon>
  <strong>Tip:</strong> Save time by using templates.
</wa-callout>
```

## Complex Content

Callouts can contain rich content:

```html
<!-- With title and body -->
<wa-callout variant="primary">
  <div slot="title">Feature Update Available</div>
  <p>
    We've added new collaboration features to help your team work together more effectively.
    Update now to get access to real-time editing and inline comments.
  </p>
  <wa-button variant="primary" size="small">Update Now</wa-button>
</wa-callout>

<!-- With list -->
<wa-callout variant="warning">
  <div slot="title">Before You Continue</div>
  <p>Please ensure you have:</p>
  <ul>
    <li>Backed up your data</li>
    <li>Reviewed the migration guide</li>
    <li>Notified your team members</li>
  </ul>
</wa-callout>

<!-- With action buttons -->
<wa-callout variant="danger" closable>
  <div slot="title">Subscription Expired</div>
  <p>Your subscription has expired. Renew now to continue using all features.</p>
  <div style="display: flex; gap: 0.5rem; margin-top: 0.5rem;">
    <wa-button variant="danger" size="small">Renew Now</wa-button>
    <wa-button variant="default" size="small" outline>Learn More</wa-button>
  </div>
</wa-callout>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `variant` | string | `'neutral'` | No | Visual style: `primary`, `success`, `neutral`, `warning`, `danger` |
| `closable` | boolean | `false` | No | Show close button and allow dismissal |
| `open` | boolean | `true` | No | Control visibility (useful when programmatically showing/hiding) |

### Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-close` | Emitted when the callout is closed | - |
| `wa-after-hide` | Emitted after the close animation completes | - |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Main content of the callout |
| `icon` | Icon displayed at the start of the callout |
| `title` | Title content (styled appropriately) |

## Examples

### Form Validation Messages

```html
<style>
  .form-container {
    max-width: 500px;
  }
  .form-field {
    margin-bottom: 1rem;
  }
</style>

<div class="form-container">
  <wa-callout variant="danger" style="margin-bottom: 1rem;">
    <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
    <div slot="title">Please correct the following errors:</div>
    <ul style="margin: 0.5rem 0 0 0; padding-left: 1.5rem;">
      <li>Email address is required</li>
      <li>Password must be at least 8 characters</li>
      <li>Terms of service must be accepted</li>
    </ul>
  </wa-callout>

  <div class="form-field">
    <wa-input label="Email" type="email" required></wa-input>
  </div>

  <div class="form-field">
    <wa-input label="Password" type="password" required></wa-input>
  </div>

  <div class="form-field">
    <wa-checkbox>I agree to the terms of service</wa-checkbox>
  </div>

  <wa-button variant="primary">Submit</wa-button>
</div>
```

### Success Notification with Auto-Close

```html
<wa-button id="saveBtn" variant="primary">Save Changes</wa-button>

<wa-callout id="successMessage" variant="success" closable style="margin-top: 1rem; display: none;">
  <wa-icon slot="icon" name="check-circle"></wa-icon>
  <strong>Saved!</strong> Your changes have been saved successfully.
</wa-callout>

<script>
  const saveBtn = document.getElementById('saveBtn');
  const successMessage = document.getElementById('successMessage');

  saveBtn.addEventListener('click', async () => {
    saveBtn.loading = true;

    // Simulate save operation
    await new Promise(resolve => setTimeout(resolve, 1000));

    saveBtn.loading = false;
    successMessage.style.display = 'block';
    successMessage.open = true;

    // Auto-close after 5 seconds
    setTimeout(() => {
      successMessage.open = false;
    }, 5000);
  });

  successMessage.addEventListener('wa-after-hide', () => {
    successMessage.style.display = 'none';
  });
</script>
```

### Documentation Page Callouts

```html
<style>
  .doc-section {
    max-width: 800px;
    margin: 2rem 0;
  }
  .doc-section h2 {
    margin-bottom: 1rem;
  }
  .doc-section p {
    line-height: 1.6;
    margin-bottom: 1rem;
  }
  .callout-spacer {
    margin: 1.5rem 0;
  }
</style>

<div class="doc-section">
  <h2>Installation Guide</h2>

  <p>Follow these steps to install the application on your system.</p>

  <wa-callout variant="warning" class="callout-spacer">
    <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
    <strong>Important:</strong> Make sure you have Node.js version 18 or higher installed before proceeding.
  </wa-callout>

  <p>To install the dependencies, run the following command:</p>

  <pre><code>npm install</code></pre>

  <wa-callout variant="primary" class="callout-spacer">
    <wa-icon slot="icon" name="lightbulb"></wa-icon>
    <strong>Tip:</strong> You can use <code>npm ci</code> for faster, more reliable installs in CI/CD environments.
  </wa-callout>

  <p>Once installation is complete, start the development server:</p>

  <pre><code>npm run dev</code></pre>

  <wa-callout variant="success" class="callout-spacer">
    <wa-icon slot="icon" name="check-circle"></wa-icon>
    <strong>Well done!</strong> Your development environment is now set up and ready to use.
  </wa-callout>
</div>
```

### System Status Alerts

```html
<style>
  .status-container {
    max-width: 700px;
  }
  .status-header {
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 1rem;
  }
  .callout-stack {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>

<div class="status-container">
  <div class="status-header">System Status</div>

  <div class="callout-stack">
    <wa-callout variant="success">
      <wa-icon slot="icon" name="check-circle"></wa-icon>
      <div slot="title">All Systems Operational</div>
      All services are running normally with no reported issues.
    </wa-callout>

    <wa-callout variant="warning">
      <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
      <div slot="title">Scheduled Maintenance</div>
      Database maintenance scheduled for tonight at 2:00 AM PST (4 hours downtime expected).
    </wa-callout>

    <wa-callout variant="primary">
      <wa-icon slot="icon" name="info-circle"></wa-icon>
      <div slot="title">API Rate Limit Update</div>
      Starting next month, API rate limits will be increased to 10,000 requests per hour for all paid plans.
    </wa-callout>
  </div>
</div>
```

### Cookie Consent Banner

```html
<style>
  .cookie-banner {
    position: fixed;
    bottom: 1rem;
    left: 1rem;
    right: 1rem;
    max-width: 600px;
    z-index: 1000;
  }
  .cookie-actions {
    display: flex;
    gap: 0.5rem;
    margin-top: 0.75rem;
  }
</style>

<wa-callout id="cookieBanner" variant="neutral" class="cookie-banner">
  <div slot="title">We use cookies</div>
  <p style="margin: 0.5rem 0 0 0;">
    We use cookies to enhance your browsing experience, serve personalized content, and analyze our traffic.
    By clicking "Accept All", you consent to our use of cookies.
  </p>
  <div class="cookie-actions">
    <wa-button id="acceptCookies" variant="primary" size="small">Accept All</wa-button>
    <wa-button id="rejectCookies" variant="default" size="small" outline>Reject Non-Essential</wa-button>
    <wa-button id="cookieSettings" variant="default" size="small" outline>Settings</wa-button>
  </div>
</wa-callout>

<script>
  const cookieBanner = document.getElementById('cookieBanner');
  const acceptCookies = document.getElementById('acceptCookies');
  const rejectCookies = document.getElementById('rejectCookies');

  // Check if user has already made a choice
  if (localStorage.getItem('cookieConsent')) {
    cookieBanner.style.display = 'none';
  }

  acceptCookies.addEventListener('click', () => {
    localStorage.setItem('cookieConsent', 'accepted');
    cookieBanner.open = false;
    setTimeout(() => cookieBanner.style.display = 'none', 300);
  });

  rejectCookies.addEventListener('click', () => {
    localStorage.setItem('cookieConsent', 'rejected');
    cookieBanner.open = false;
    setTimeout(() => cookieBanner.style.display = 'none', 300);
  });
</script>
```

### Feature Announcements

```html
<style>
  .announcement-card {
    max-width: 600px;
    margin: 2rem auto;
  }
</style>

<div class="announcement-card">
  <wa-callout variant="primary" closable>
    <wa-icon slot="icon" name="megaphone"></wa-icon>
    <div slot="title">New Feature: Real-Time Collaboration</div>
    <p style="margin: 0.5rem 0;">
      Work together with your team in real-time! See changes as they happen, leave comments, and
      collaborate more effectively than ever before.
    </p>
    <div style="display: flex; gap: 0.5rem; margin-top: 0.75rem;">
      <wa-button variant="primary" size="small">Try It Now</wa-button>
      <wa-button variant="default" size="small" outline>Learn More</wa-button>
    </div>
  </wa-callout>
</div>
```

## Methods

Control callout visibility programmatically:

```javascript
const callout = document.querySelector('wa-callout');

// Show the callout
callout.open = true;
callout.show();

// Hide the callout
callout.open = false;
callout.hide();

// Toggle visibility
callout.open = !callout.open;
```

## CSS Parts

Customize callout appearance using CSS parts:

```css
/* Style the base container */
wa-callout::part(base) {
  border-radius: 0.5rem;
  padding: 1.5rem;
}

/* Style the close button */
wa-callout::part(close-button) {
  color: inherit;
  opacity: 0.7;
}

wa-callout::part(close-button):hover {
  opacity: 1;
}

/* Style the icon container */
wa-callout::part(icon) {
  font-size: 1.5rem;
}

/* Style the message container */
wa-callout::part(message) {
  line-height: 1.6;
}
```

## Best Practices

- ✅ Use appropriate variants to match message severity (success for positive feedback, danger for errors)
- ✅ Keep messages concise and actionable
- ✅ Include relevant icons to enhance visual scanning
- ✅ Make important callouts closable to improve user experience
- ✅ Use titles to make callouts scannable
- ✅ Group related information together
- ❌ Don't overuse callouts - they lose impact when used too frequently
- ❌ Avoid using danger variant for non-critical information
- ❌ Don't nest callouts inside other callouts
- ❌ Don't use callouts for regular content - they're for emphasis only

## Accessibility

- Callouts automatically include appropriate ARIA roles based on variant
- Use semantic HTML within callouts for proper structure
- Ensure sufficient color contrast for text
- Provide meaningful content that works without color alone

```html
<!-- Good: Clear message with context -->
<wa-callout variant="danger">
  <wa-icon slot="icon" name="exclamation-circle"></wa-icon>
  <strong>Error:</strong> Unable to save your changes. Please try again.
</wa-callout>

<!-- Provide accessible labels for icon-only close buttons -->
<wa-callout closable aria-label="Dismissible notification">
  Your session will expire in 5 minutes.
</wa-callout>
```

## Troubleshooting

### Callout Not Visible

**Problem:** Callout doesn't appear on the page

**Solution:** Check that the `open` attribute is true (default)

```javascript
// Ensure callout is visible
callout.open = true;
```

### Close Button Not Working

**Problem:** Clicking X doesn't close the callout

**Solution:** Verify the `closable` attribute is set

```html
<!-- ✅ Correct -->
<wa-callout closable>Message</wa-callout>

<!-- ❌ Won't have close button -->
<wa-callout>Message</wa-callout>
```

### Icon Not Displaying

**Problem:** Icon slot content doesn't show

**Solution:** Ensure you're using the correct slot name and icon component

```html
<!-- ✅ Correct -->
<wa-callout variant="warning">
  <wa-icon slot="icon" name="exclamation-triangle"></wa-icon>
  Message
</wa-callout>

<!-- ❌ Wrong: missing slot attribute -->
<wa-callout variant="warning">
  <wa-icon name="exclamation-triangle"></wa-icon>
  Message
</wa-callout>
```

### Custom Styling Not Applying

**Problem:** CSS styles don't affect the callout

**Solution:** Use CSS parts to style internal elements

```css
/* ❌ Won't work */
wa-callout {
  background-color: red;
}

/* ✅ Correct: use CSS parts */
wa-callout::part(base) {
  background-color: red;
}
```

## Related

- [Alert](./alert.md)
- [Badge](./badge.md)
- [Toast](./toast.md)
- [Dialog](./dialog.md)
- [Card](./card.md)
