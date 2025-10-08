# Dialog

Modal dialog box for displaying important information or collecting user input.

## Overview

The `<wa-dialog>` component provides a fully accessible modal dialog that overlays the page content. It supports custom headers and footers, various sizes, and can be configured to prevent closing for critical interactions.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/dialog/dialog.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic dialog -->
<wa-dialog label="Dialog Title">
  <p>This is a basic dialog with some content.</p>
</wa-dialog>

<wa-button id="openDialog">Open Dialog</wa-button>

<script>
  const dialog = document.querySelector('wa-dialog');
  const button = document.getElementById('openDialog');

  button.addEventListener('click', () => dialog.show());
</script>
```

## Opening and Closing

Dialogs are hidden by default. Use the `show()` and `hide()` methods or the `open` attribute to control visibility:

```html
<!-- Open by default -->
<wa-dialog label="Open Dialog" open>
  <p>This dialog is open by default.</p>
</wa-dialog>

<!-- Control programmatically -->
<wa-dialog id="myDialog" label="My Dialog">
  <p>Dialog content goes here.</p>
  <wa-button slot="footer" id="closeBtn">Close</wa-button>
</wa-dialog>

<script>
  const dialog = document.getElementById('myDialog');
  const closeBtn = document.getElementById('closeBtn');

  // Show the dialog
  dialog.show();

  // Hide the dialog
  closeBtn.addEventListener('click', () => dialog.hide());
</script>
```

## Dialog with Header and Footer

Use the `header` and `footer` slots to add custom content:

```html
<wa-dialog>
  <div slot="header">
    <h2>Custom Header</h2>
    <p>With additional content</p>
  </div>

  <p>Main dialog content goes here.</p>

  <div slot="footer">
    <wa-button>Cancel</wa-button>
    <wa-button variant="primary">Confirm</wa-button>
  </div>
</wa-dialog>
```

## No Header

Use the `no-header` attribute to hide the header section:

```html
<wa-dialog no-header>
  <p>This dialog has no header section.</p>
  <wa-button slot="footer">Close</wa-button>
</wa-dialog>
```

## Examples

### Basic Dialog

```html
<wa-button id="basicBtn">Show Basic Dialog</wa-button>

<wa-dialog id="basicDialog" label="Welcome">
  <p>Welcome to our application! This is a basic dialog example.</p>
  <wa-button slot="footer" id="basicClose">Got it</wa-button>
</wa-dialog>

<script>
  const basicBtn = document.getElementById('basicBtn');
  const basicDialog = document.getElementById('basicDialog');
  const basicClose = document.getElementById('basicClose');

  basicBtn.addEventListener('click', () => basicDialog.show());
  basicClose.addEventListener('click', () => basicDialog.hide());
</script>
```

### Dialog with Form

```html
<wa-button id="formBtn">Open Form Dialog</wa-button>

<wa-dialog id="formDialog" label="Sign Up">
  <form id="signupForm">
    <wa-input
      name="name"
      label="Full Name"
      required
      style="margin-bottom: 1rem;">
    </wa-input>

    <wa-input
      name="email"
      label="Email"
      type="email"
      required
      style="margin-bottom: 1rem;">
    </wa-input>

    <wa-input
      name="password"
      label="Password"
      type="password"
      required
      style="margin-bottom: 1rem;">
    </wa-input>
  </form>

  <div slot="footer">
    <wa-button id="cancelForm">Cancel</wa-button>
    <wa-button variant="primary" id="submitForm" type="submit">Sign Up</wa-button>
  </div>
</wa-dialog>

<script>
  const formBtn = document.getElementById('formBtn');
  const formDialog = document.getElementById('formDialog');
  const cancelForm = document.getElementById('cancelForm');
  const submitForm = document.getElementById('submitForm');
  const signupForm = document.getElementById('signupForm');

  formBtn.addEventListener('click', () => formDialog.show());
  cancelForm.addEventListener('click', () => formDialog.hide());

  submitForm.addEventListener('click', () => {
    if (signupForm.checkValidity()) {
      const formData = new FormData(signupForm);
      console.log('Form data:', Object.fromEntries(formData));
      formDialog.hide();
    } else {
      signupForm.reportValidity();
    }
  });
</script>
```

### Confirmation Dialog

```html
<wa-button id="deleteBtn" variant="danger">Delete Item</wa-button>

<wa-dialog id="confirmDialog" label="Confirm Deletion">
  <p>Are you sure you want to delete this item? This action cannot be undone.</p>

  <div slot="footer">
    <wa-button id="cancelDelete">Cancel</wa-button>
    <wa-button variant="danger" id="confirmDelete">Delete</wa-button>
  </div>
</wa-dialog>

<script>
  const deleteBtn = document.getElementById('deleteBtn');
  const confirmDialog = document.getElementById('confirmDialog');
  const cancelDelete = document.getElementById('cancelDelete');
  const confirmDelete = document.getElementById('confirmDelete');

  deleteBtn.addEventListener('click', () => confirmDialog.show());
  cancelDelete.addEventListener('click', () => confirmDialog.hide());

  confirmDelete.addEventListener('click', async () => {
    confirmDelete.loading = true;

    try {
      // Perform delete action
      await performDelete();
      confirmDialog.hide();
    } catch (error) {
      console.error('Delete failed:', error);
    } finally {
      confirmDelete.loading = false;
    }
  });

  async function performDelete() {
    return new Promise(resolve => setTimeout(resolve, 1000));
  }
</script>
```

### Alert Dialog

```html
<wa-button id="alertBtn">Show Alert</wa-button>

<wa-dialog id="alertDialog" label="Important Notice">
  <wa-icon name="exclamation-triangle" style="color: orange; font-size: 3rem; display: block; margin: 1rem auto;"></wa-icon>
  <p style="text-align: center;">Your session will expire in 5 minutes. Please save your work.</p>

  <wa-button slot="footer" variant="primary" id="alertOk" style="width: 100%;">
    Acknowledge
  </wa-button>
</wa-dialog>

<script>
  const alertBtn = document.getElementById('alertBtn');
  const alertDialog = document.getElementById('alertDialog');
  const alertOk = document.getElementById('alertOk');

  alertBtn.addEventListener('click', () => alertDialog.show());
  alertOk.addEventListener('click', () => alertDialog.hide());
</script>
```

### Dialog Sizes

```html
<wa-button id="smallBtn">Small Dialog</wa-button>
<wa-button id="mediumBtn">Medium Dialog</wa-button>
<wa-button id="largeBtn">Large Dialog</wa-button>

<!-- Small dialog -->
<wa-dialog id="smallDialog" label="Small Dialog" style="--width: 400px;">
  <p>This is a small dialog with limited width.</p>
  <wa-button slot="footer" class="closeSmall">Close</wa-button>
</wa-dialog>

<!-- Medium dialog (default) -->
<wa-dialog id="mediumDialog" label="Medium Dialog">
  <p>This is a medium-sized dialog with the default width.</p>
  <wa-button slot="footer" class="closeMedium">Close</wa-button>
</wa-dialog>

<!-- Large dialog -->
<wa-dialog id="largeDialog" label="Large Dialog" style="--width: 800px;">
  <p>This is a large dialog with more space for content.</p>
  <wa-button slot="footer" class="closeLarge">Close</wa-button>
</wa-dialog>

<script>
  document.getElementById('smallBtn').addEventListener('click', () =>
    document.getElementById('smallDialog').show()
  );

  document.getElementById('mediumBtn').addEventListener('click', () =>
    document.getElementById('mediumDialog').show()
  );

  document.getElementById('largeBtn').addEventListener('click', () =>
    document.getElementById('largeDialog').show()
  );

  document.querySelectorAll('.closeSmall, .closeMedium, .closeLarge').forEach(btn => {
    btn.addEventListener('click', (e) => {
      e.target.closest('wa-dialog').hide();
    });
  });
</script>
```

### Preventing Close

Prevent the dialog from being closed by clicking the overlay or pressing Escape:

```html
<wa-button id="criticalBtn">Critical Action</wa-button>

<wa-dialog id="criticalDialog" label="Critical Action Required">
  <p>You must complete this action. The dialog cannot be dismissed without a response.</p>

  <div slot="footer">
    <wa-button variant="danger" id="criticalConfirm">I Understand</wa-button>
  </div>
</wa-dialog>

<script>
  const criticalBtn = document.getElementById('criticalBtn');
  const criticalDialog = document.getElementById('criticalDialog');
  const criticalConfirm = document.getElementById('criticalConfirm');

  criticalBtn.addEventListener('click', () => criticalDialog.show());

  // Prevent closing via request-close event
  criticalDialog.addEventListener('wa-request-close', (event) => {
    // Check if close was triggered by overlay or escape
    if (event.detail.source === 'overlay' || event.detail.source === 'keyboard') {
      event.preventDefault();
    }
  });

  criticalConfirm.addEventListener('click', () => {
    // Perform critical action
    criticalDialog.hide();
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `open` | boolean | `false` | No | Controls whether the dialog is visible |
| `label` | string | - | Yes | The dialog's label (displayed in header) |
| `no-header` | boolean | `false` | No | Hides the header section |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Opens the dialog | `void` |
| `hide()` | Closes the dialog | `void` |

### Method Examples

```javascript
const dialog = document.querySelector('wa-dialog');

// Show the dialog
dialog.show();

// Hide the dialog
dialog.hide();

// Toggle dialog visibility
if (dialog.open) {
  dialog.hide();
} else {
  dialog.show();
}

// Check if dialog is open
console.log('Dialog is open:', dialog.open);
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the dialog is shown (before animation) | - |
| `wa-after-show` | Emitted after the dialog is shown (after animation) | - |
| `wa-hide` | Emitted when the dialog is hidden (before animation) | - |
| `wa-after-hide` | Emitted after the dialog is hidden (after animation) | - |
| `wa-request-close` | Emitted when user attempts to close (via overlay, escape, or close button). Can be prevented with `preventDefault()` | `{ source: 'close-button' \| 'keyboard' \| 'overlay' }` |

### Event Examples

```javascript
const dialog = document.querySelector('wa-dialog');

// Before dialog shows
dialog.addEventListener('wa-show', () => {
  console.log('Dialog is about to show');
});

// After dialog is fully visible
dialog.addEventListener('wa-after-show', () => {
  console.log('Dialog is now visible');
  // Focus first input
  dialog.querySelector('input')?.focus();
});

// Before dialog hides
dialog.addEventListener('wa-hide', () => {
  console.log('Dialog is about to hide');
});

// After dialog is fully hidden
dialog.addEventListener('wa-after-hide', () => {
  console.log('Dialog is now hidden');
  // Clean up or reset form
});

// Handle close requests
dialog.addEventListener('wa-request-close', (event) => {
  console.log('Close requested from:', event.detail.source);

  // Prevent closing if form has unsaved changes
  if (hasUnsavedChanges()) {
    event.preventDefault();

    if (confirm('You have unsaved changes. Close anyway?')) {
      dialog.hide();
    }
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The dialog's main content |
| `header` | Custom header content (overrides default label display) |
| `footer` | Footer content, typically used for action buttons |

### Slot Examples

```html
<!-- Custom header -->
<wa-dialog>
  <div slot="header">
    <h2>Multi-line Header</h2>
    <p style="margin: 0; font-size: 0.875rem; color: gray;">
      Additional context or description
    </p>
  </div>

  <p>Dialog content</p>
</wa-dialog>

<!-- Footer with multiple buttons -->
<wa-dialog label="Actions">
  <p>Choose an action:</p>

  <div slot="footer" style="display: flex; gap: 0.5rem; justify-content: flex-end;">
    <wa-button>Cancel</wa-button>
    <wa-button variant="neutral">Save Draft</wa-button>
    <wa-button variant="primary">Publish</wa-button>
  </div>
</wa-dialog>

<!-- No footer -->
<wa-dialog label="Information">
  <p>This dialog has no footer.</p>
</wa-dialog>
```

## CSS Parts

Use CSS parts to style internal dialog elements:

```css
/* Style the base dialog container */
wa-dialog::part(base) {
  border-radius: 8px;
}

/* Style the overlay backdrop */
wa-dialog::part(overlay) {
  backdrop-filter: blur(4px);
  background-color: rgba(0, 0, 0, 0.5);
}

/* Style the dialog panel */
wa-dialog::part(panel) {
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

/* Style the header */
wa-dialog::part(header) {
  background-color: #f9fafb;
  border-bottom: 1px solid #e5e7eb;
}

/* Style the title */
wa-dialog::part(title) {
  font-size: 1.5rem;
  font-weight: 600;
}

/* Style the close button */
wa-dialog::part(close-button) {
  color: #6b7280;
}

wa-dialog::part(close-button):hover {
  color: #111827;
}

/* Style the body content area */
wa-dialog::part(body) {
  padding: 2rem;
}

/* Style the footer */
wa-dialog::part(footer) {
  background-color: #f9fafb;
  border-top: 1px solid #e5e7eb;
  padding: 1rem;
}
```

## Customization

### Custom Width

Control dialog width with CSS custom properties:

```html
<!-- Small dialog -->
<wa-dialog label="Small" style="--width: 400px;">
  <p>Content</p>
</wa-dialog>

<!-- Large dialog -->
<wa-dialog label="Large" style="--width: 900px;">
  <p>Content</p>
</wa-dialog>

<!-- Full width with max-width -->
<wa-dialog label="Responsive" style="--width: 90vw; --max-width: 1200px;">
  <p>Content</p>
</wa-dialog>
```

### Custom Styling

```css
/* Custom dialog theme */
.custom-dialog::part(panel) {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.custom-dialog::part(header) {
  background-color: transparent;
  border-bottom-color: rgba(255, 255, 255, 0.2);
}

.custom-dialog::part(close-button) {
  color: white;
}

.custom-dialog::part(footer) {
  background-color: transparent;
  border-top-color: rgba(255, 255, 255, 0.2);
}
```

### Scrollable Content

For long content, the dialog body will automatically scroll:

```html
<wa-dialog label="Long Content" style="--height: 600px;">
  <div style="height: 1200px;">
    <p>This content is very long...</p>
    <p>And will scroll automatically...</p>
    <!-- More content -->
  </div>

  <wa-button slot="footer">Close</wa-button>
</wa-dialog>
```

## Best Practices

- ✅ Always provide a clear `label` for accessibility
- ✅ Include a way to close the dialog (footer button or allow escape/overlay clicks)
- ✅ Use appropriate button variants in footer (primary for confirm, danger for destructive)
- ✅ Focus first input field after dialog opens for forms
- ✅ Prevent closing for critical actions that require user response
- ✅ Use `wa-after-show` event to set initial focus
- ✅ Keep dialog content focused and concise
- ❌ Don't nest dialogs within other dialogs
- ❌ Don't use dialogs for non-critical information (use notifications instead)
- ❌ Avoid extremely long content (consider alternative UI patterns)
- ❌ Don't prevent closing without a clear reason

## Accessibility

The dialog component is built with accessibility in mind:

- Automatically traps focus within the dialog when open
- Supports keyboard navigation (Tab, Shift+Tab, Escape)
- Uses proper ARIA attributes (`role="dialog"`, `aria-modal="true"`, `aria-labelledby`)
- Restores focus to trigger element when closed
- Escape key closes the dialog (unless prevented)
- Clicking overlay closes the dialog (unless prevented)
- Screen reader announcements for dialog state changes

### Accessible Label

```html
<!-- Using label attribute -->
<wa-dialog label="User Settings">
  <p>Content</p>
</wa-dialog>

<!-- Using aria-label for dynamic content -->
<wa-dialog id="dynamicDialog">
  <p>Content</p>
</wa-dialog>

<script>
  const dialog = document.getElementById('dynamicDialog');
  dialog.setAttribute('aria-label', 'Notification from ' + userName);
</script>
```

### Focus Management

```javascript
const dialog = document.querySelector('wa-dialog');

// Focus first input when dialog opens
dialog.addEventListener('wa-after-show', () => {
  const firstInput = dialog.querySelector('input, textarea, select');
  if (firstInput) {
    firstInput.focus();
  }
});
```

## Troubleshooting

### Dialog Not Showing

**Problem:** Dialog doesn't appear when calling `show()`

**Solution:** Ensure the dialog element is in the DOM and not hidden by CSS

```javascript
const dialog = document.querySelector('wa-dialog');

// Check if element exists
if (dialog) {
  dialog.show();
} else {
  console.error('Dialog element not found');
}
```

### Dialog Closes Unexpectedly

**Problem:** Dialog closes when you don't want it to

**Solution:** Prevent the `wa-request-close` event

```javascript
dialog.addEventListener('wa-request-close', (event) => {
  // Prevent all close attempts
  event.preventDefault();

  // Or conditionally prevent
  if (shouldPreventClose()) {
    event.preventDefault();
  }
});
```

### Content Not Visible

**Problem:** Dialog content is cut off or not visible

**Solution:** Adjust dialog height or ensure content fits

```html
<!-- Set max height -->
<wa-dialog label="Title" style="--max-height: 80vh;">
  <div style="overflow-y: auto;">
    <!-- Long content -->
  </div>
</wa-dialog>
```

### Z-Index Issues

**Problem:** Other elements appear on top of dialog

**Solution:** Dialogs use a high z-index by default, but you can adjust if needed

```css
wa-dialog::part(base) {
  z-index: 10000;
}
```

## Related

- [Alert](./alert.md)
- [Drawer](./drawer.md)
- [Button](./button.md)
- [Modal Patterns Guide](../guides/modal-patterns.md)
