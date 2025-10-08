# Textarea

A multi-line text input control for longer form content.

## Overview

The `<wa-textarea>` component provides a multi-line text input field for collecting longer text content from users. It supports features like placeholder text, validation states, resizing options, and various input restrictions. Perfect for comments, descriptions, messages, and other multi-line content.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/textarea/textarea.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default textarea -->
<wa-textarea label="Comments"></wa-textarea>

<!-- With placeholder -->
<wa-textarea label="Description" placeholder="Enter a description..."></wa-textarea>

<!-- With default value -->
<wa-textarea label="Bio" value="Tell us about yourself"></wa-textarea>

<!-- Disabled textarea -->
<wa-textarea label="Disabled" disabled value="Cannot edit this"></wa-textarea>

<!-- Readonly textarea -->
<wa-textarea label="Readonly" readonly value="Can read but not edit"></wa-textarea>
```

## Rows

Control the visible height with the `rows` attribute:

```html
<!-- Small (3 rows) -->
<wa-textarea label="Short text" rows="3"></wa-textarea>

<!-- Medium (5 rows, default) -->
<wa-textarea label="Medium text" rows="5"></wa-textarea>

<!-- Large (10 rows) -->
<wa-textarea label="Long text" rows="10"></wa-textarea>
```

## Resize Behavior

Control how users can resize the textarea with the `resize` attribute:

```html
<!-- No resizing -->
<wa-textarea label="Fixed size" resize="none"></wa-textarea>

<!-- Vertical resize only (default) -->
<wa-textarea label="Vertical resize" resize="vertical"></wa-textarea>

<!-- Auto-resize to fit content -->
<wa-textarea label="Auto-resize" resize="auto"></wa-textarea>
```

## Validation

```html
<!-- Required field -->
<wa-textarea label="Required field" required></wa-textarea>

<!-- With help text -->
<wa-textarea
  label="Comment"
  help-text="Please provide detailed feedback"
  required>
</wa-textarea>

<!-- With minimum length -->
<wa-textarea
  label="Review"
  minlength="50"
  help-text="Minimum 50 characters">
</wa-textarea>

<!-- With maximum length -->
<wa-textarea
  label="Tweet"
  maxlength="280"
  help-text="Maximum 280 characters">
</wa-textarea>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | `''` | No | The textarea's value |
| `label` | string | - | No | Label text for the textarea |
| `placeholder` | string | - | No | Placeholder text |
| `rows` | number | `4` | No | Number of visible rows |
| `resize` | string | `'vertical'` | No | Resize behavior: `none`, `vertical`, `auto` |
| `disabled` | boolean | `false` | No | Disable the textarea |
| `readonly` | boolean | `false` | No | Make textarea read-only |
| `required` | boolean | `false` | No | Mark as required for validation |
| `minlength` | number | - | No | Minimum character length |
| `maxlength` | number | - | No | Maximum character length |
| `autocomplete` | string | - | No | Browser autocomplete behavior |
| `autocorrect` | string | - | No | Enable/disable autocorrect (iOS) |
| `autocapitalize` | string | - | No | Autocapitalization behavior (mobile) |
| `spellcheck` | boolean | `true` | No | Enable/disable spellcheck |
| `name` | string | - | No | Name attribute for form submission |
| `help-text` | string | - | No | Help text displayed below textarea |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-input` | Emitted when the value changes (on input) | `{ value: string }` |
| `wa-change` | Emitted when the value changes and input loses focus | `{ value: string }` |
| `wa-focus` | Emitted when the textarea gains focus | - |
| `wa-blur` | Emitted when the textarea loses focus | - |

### Event Examples

```javascript
const textarea = document.querySelector('wa-textarea');

// Listen for input (real-time)
textarea.addEventListener('wa-input', (event) => {
  console.log('Current value:', event.detail.value);
});

// Listen for change (on blur)
textarea.addEventListener('wa-change', (event) => {
  console.log('Final value:', event.detail.value);
});

// Listen for focus
textarea.addEventListener('wa-focus', () => {
  console.log('Textarea focused');
});

// Listen for blur
textarea.addEventListener('wa-blur', () => {
  console.log('Textarea blurred');
});
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the textarea | `void` |
| `blur()` | Removes focus from the textarea | `void` |
| `select()` | Selects all text in the textarea | `void` |
| `setSelectionRange(start, end)` | Sets the selection range | `void` |
| `reportValidity()` | Triggers validation and shows validation message | `boolean` |

### Method Examples

```javascript
const textarea = document.querySelector('wa-textarea');

// Focus the textarea
textarea.focus();

// Remove focus
textarea.blur();

// Select all text
textarea.select();

// Set selection range
textarea.setSelectionRange(0, 10); // Select first 10 characters

// Check validity
const isValid = textarea.reportValidity();
```

## Examples

### Comment Form

```html
<form id="commentForm" style="max-width: 600px;">
  <wa-textarea
    label="Add a comment"
    name="comment"
    rows="4"
    placeholder="Share your thoughts..."
    required
    minlength="10"
    help-text="Minimum 10 characters">
  </wa-textarea>

  <wa-button type="submit" variant="primary" style="margin-top: 1rem;">
    Post Comment
  </wa-button>
</form>

<script>
  const form = document.getElementById('commentForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(form);
    console.log('Comment:', formData.get('comment'));
  });
</script>
```

### Character Counter

```html
<div style="max-width: 600px;">
  <wa-textarea
    id="tweetInput"
    label="Compose tweet"
    rows="3"
    maxlength="280"
    resize="none">
  </wa-textarea>
  <p style="text-align: right; margin-top: 0.5rem; color: #666;">
    <span id="charCount">0</span> / 280
  </p>
</div>

<script>
  const textarea = document.getElementById('tweetInput');
  const charCount = document.getElementById('charCount');

  textarea.addEventListener('wa-input', (e) => {
    const length = e.detail.value.length;
    charCount.textContent = length;

    // Change color when approaching limit
    if (length > 260) {
      charCount.style.color = '#ef4444';
    } else if (length > 240) {
      charCount.style.color = '#f59e0b';
    } else {
      charCount.style.color = '#666';
    }
  });
</script>
```

### Auto-Resize Textarea

```html
<wa-textarea
  id="autoResizeText"
  label="Description"
  placeholder="Start typing..."
  resize="auto"
  rows="3"
  help-text="This textarea will grow as you type">
</wa-textarea>
```

### Rich Feedback Form

```html
<form id="feedbackForm" style="max-width: 600px;">
  <wa-input
    label="Name"
    name="name"
    required>
  </wa-input>

  <wa-input
    label="Email"
    name="email"
    type="email"
    required>
  </wa-input>

  <wa-select label="Category" name="category" required>
    <wa-option value="bug">Bug Report</wa-option>
    <wa-option value="feature">Feature Request</wa-option>
    <wa-option value="question">Question</wa-option>
    <wa-option value="other">Other</wa-option>
  </wa-select>

  <wa-textarea
    label="Feedback"
    name="feedback"
    rows="6"
    placeholder="Please provide detailed feedback..."
    required
    minlength="20"
    help-text="Minimum 20 characters">
  </wa-textarea>

  <wa-button type="submit" variant="primary" style="margin-top: 1rem;">
    Submit Feedback
  </wa-button>
</form>

<script>
  const form = document.getElementById('feedbackForm');

  form.addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(form);
    const data = Object.fromEntries(formData);
    console.log('Feedback submitted:', data);
  });
</script>
```

### Live Preview

```html
<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; max-width: 900px;">
  <div>
    <wa-textarea
      id="markdownInput"
      label="Markdown Input"
      rows="10"
      placeholder="# Enter markdown here..."
      resize="vertical">
    </wa-textarea>
  </div>

  <div>
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">
      Preview
    </label>
    <div id="preview" style="
      border: 1px solid #e5e7eb;
      border-radius: 4px;
      padding: 1rem;
      min-height: 200px;
      background: #f9fafb;
    "></div>
  </div>
</div>

<script>
  const input = document.getElementById('markdownInput');
  const preview = document.getElementById('preview');

  input.addEventListener('wa-input', (e) => {
    // Simple markdown-like preview (in real app, use a markdown library)
    let html = e.detail.value
      .replace(/^# (.*$)/gim, '<h1>$1</h1>')
      .replace(/^## (.*$)/gim, '<h2>$1</h2>')
      .replace(/^### (.*$)/gim, '<h3>$1</h3>')
      .replace(/\*\*(.*?)\*\*/gim, '<strong>$1</strong>')
      .replace(/\*(.*?)\*/gim, '<em>$1</em>')
      .replace(/\n/gim, '<br>');

    preview.innerHTML = html || '<em style="color: #9ca3af;">Preview will appear here...</em>';
  });
</script>
```

### Save Draft Functionality

```html
<div style="max-width: 600px;">
  <wa-textarea
    id="draftTextarea"
    label="Article content"
    rows="8"
    placeholder="Start writing your article..."
    help-text="Your draft is automatically saved">
  </wa-textarea>

  <p style="margin-top: 0.5rem; color: #666; font-size: 0.875rem;">
    <span id="saveStatus">No changes</span>
  </p>
</div>

<script>
  const textarea = document.getElementById('draftTextarea');
  const saveStatus = document.getElementById('saveStatus');
  let saveTimeout;

  // Load saved draft
  const savedDraft = localStorage.getItem('articleDraft');
  if (savedDraft) {
    textarea.value = savedDraft;
    saveStatus.textContent = 'Draft loaded';
  }

  // Auto-save on input
  textarea.addEventListener('wa-input', (e) => {
    saveStatus.textContent = 'Saving...';

    // Debounce save
    clearTimeout(saveTimeout);
    saveTimeout = setTimeout(() => {
      localStorage.setItem('articleDraft', e.detail.value);
      saveStatus.textContent = 'Draft saved';

      setTimeout(() => {
        saveStatus.textContent = 'All changes saved';
      }, 1000);
    }, 1000);
  });
</script>
```

## Slots

| Slot | Description |
|------|-------------|
| `label` | Label text (alternative to label attribute) |
| `help-text` | Help text displayed below textarea |

## CSS Parts

Use CSS parts to style internal textarea elements:

```css
/* Style the form control wrapper */
wa-textarea::part(form-control) {
  margin-bottom: 1rem;
}

/* Style the label */
wa-textarea::part(label) {
  font-weight: bold;
  color: #374151;
}

/* Style the textarea input */
wa-textarea::part(textarea) {
  font-family: 'Monaco', monospace;
  border: 2px solid #e5e7eb;
}

/* Style the help text */
wa-textarea::part(help-text) {
  color: #6b7280;
  font-size: 0.875rem;
}
```

## Customization

### Custom Styling

```css
/* Custom border and focus state */
wa-textarea::part(textarea) {
  border: 2px solid #e5e7eb;
  border-radius: 8px;
}

wa-textarea::part(textarea):focus {
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

/* Custom font */
wa-textarea.monospace::part(textarea) {
  font-family: 'Courier New', monospace;
  font-size: 0.875rem;
}
```

### Error State Styling

```css
/* Error state */
wa-textarea.error::part(textarea) {
  border-color: #ef4444;
}

wa-textarea.error::part(help-text) {
  color: #ef4444;
}
```

## Best Practices

- Use clear, descriptive labels for all textareas
- Provide appropriate placeholder text as examples
- Set reasonable default row heights based on expected content
- Use `minlength` and `maxlength` for content validation
- Show character counters for length-limited inputs
- Enable auto-resize for dynamic content when appropriate
- Disable resize when fixed dimensions are required
- Provide helpful validation messages
- Use help text to explain requirements or provide examples
- Save drafts automatically for longer content
- Consider accessibility - ensure labels are always present

## Accessibility

- Textareas automatically include appropriate ARIA attributes
- Always provide a label (via attribute or slot)
- Use `help-text` for additional instructions
- Error messages are announced to screen readers
- Required textareas are marked with `aria-required`
- Invalid textareas are marked with `aria-invalid`

```html
<!-- Good accessibility -->
<wa-textarea
  label="Description"
  help-text="Please provide a detailed description"
  required
  aria-describedby="description-help">
</wa-textarea>
```

## Troubleshooting

### Value Not Updating

**Problem:** Textarea value doesn't update when changed

**Solution:** Use the `wa-input` event to track changes

```javascript
textarea.addEventListener('wa-input', (e) => {
  console.log('New value:', e.detail.value);
});
```

### Auto-Resize Not Working

**Problem:** Textarea with `resize="auto"` doesn't grow

**Solution:** Ensure there are no conflicting CSS styles

```css
/* Remove any height constraints */
wa-textarea[resize="auto"]::part(textarea) {
  max-height: none !important;
}
```

### Validation Not Showing

**Problem:** Validation errors don't appear

**Solution:** Call `reportValidity()` to trigger validation

```javascript
const textarea = document.querySelector('wa-textarea');
textarea.reportValidity();
```

## Related

- [Input](./input.md)
- [Form](./form.md)
- [Form Controls Guide](../guides/form-controls.md)
- [Validation Guide](../guides/validation.md)
