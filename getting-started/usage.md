# Usage Guide

Comprehensive guide to using WebAwesome components effectively. Learn about registration, properties, events, methods, and slots.

## Overview

WebAwesome components are custom elements (web components) that work like regular HTML elements but with enhanced functionality. Each component provides a complete API including properties, events, methods, and slots.

## Component Registration

### Awaiting Individual Components

Before interacting with component properties or methods, ensure registration is complete:

```javascript
// Wait for specific component
await customElements.whenDefined('wa-button');

// Component is ready to use
const button = document.querySelector('wa-button');
button.size = 'large';
```

### Awaiting All WebAwesome Components

For applications using multiple components, use the `allDefined()` utility:

```javascript
import { allDefined } from '/dist/webawesome.js';

// Wait for all WebAwesome components in DOM
await allDefined();

// All wa- prefixed components are ready
document.querySelectorAll('wa-button').forEach(button => {
  button.addEventListener('click', handleClick);
});
```

### Advanced Registration Control

```javascript
import { allDefined } from '/dist/webawesome.js';

// Custom registration waiting with options
await allDefined({
  root: document.getElementById('sidebar'),                    // Search within specific element
  match: tagName => tagName.startsWith('wa-') || tagName === 'my-component', // Custom match function
  additionalElements: ['wa-slider', 'other-slider']           // Wait for specific elements
});
```

**Options:**
- **`root`** - Specify search container (defaults to `document`)
- **`match`** - Function returning `true` for elements to await
- **`additionalElements`** - Array of tag names to wait for regardless of DOM presence

**Important:** `additionalElements` waits for registration only, not loading. Ensure dynamic content injection happens before `allDefined()` call.

## Attributes and Properties

### Setting Attributes

```html
<!-- Size attribute maps to size property -->
<wa-button size="small">Click me</wa-button>

<!-- Type attribute -->
<wa-input type="email"></wa-input>

<!-- Multiple attributes -->
<wa-card appearance="filled" size="large"></wa-card>
```

### Boolean Attributes

```html
<!-- Boolean properties don't need values -->
<wa-button disabled>Cannot click</wa-button>
<wa-input required readonly></wa-input>
<wa-checkbox checked></wa-checkbox>
```

### JavaScript Property Access

```javascript
const button = document.querySelector('wa-button');
button.size = 'large';           // Set property
button.disabled = true;          // Boolean property
console.log(button.variant);     // Get property value
```

### Attribute vs Property Mapping

```javascript
// HTML attributes (kebab-case) map to JavaScript properties (camelCase)
// HTML: custom-attribute="value"
// JS: element.customAttribute = "value"

const input = document.querySelector('wa-input');
input.setAttribute('help-text', 'Enter your email');  // HTML attribute
input.helpText = 'Enter your email';                  // JavaScript property (equivalent)
```

## Events

### Standard Events

```javascript
// Listen for standard DOM events
button.addEventListener('click', () => {
  console.log('Button clicked');
});

input.addEventListener('focus', handleFocus);
input.addEventListener('blur', handleBlur);
```

### Custom WebAwesome Events

```javascript
// Custom events are prefixed with 'wa-'
dialog.addEventListener('wa-after-show', () => {
  console.log('Dialog opened');
});

select.addEventListener('wa-change', (event) => {
  console.log('Selection changed:', event.detail.value);
});

drawer.addEventListener('wa-after-hide', handleDrawerClose);
```

**Event Naming Convention:** All WebAwesome events use `wa-` prefix to prevent collisions with standard events and other libraries.

### Event Details

```javascript
// Many custom events include detail information
input.addEventListener('wa-input', (event) => {
  console.log('Input value:', event.target.value);
  console.log('Event details:', event.detail);
});
```

### Common Events by Component Type

| Component Type | Events | Description |
|---------------|--------|-------------|
| Form controls | `wa-input`, `wa-change`, `wa-blur`, `wa-focus` | Input and state changes |
| Dialogs | `wa-show`, `wa-after-show`, `wa-hide`, `wa-after-hide` | Show/hide lifecycle |
| Drawers | `wa-show`, `wa-after-show`, `wa-hide`, `wa-after-hide` | Drawer lifecycle |
| Dropdowns | `wa-show`, `wa-after-show`, `wa-hide`, `wa-after-hide`, `wa-select` | Menu interactions |
| Tabs | `wa-tab-show`, `wa-tab-hide` | Tab switching |

## Methods

### Calling Component Methods

```javascript
// Focus an input
const input = document.querySelector('wa-input');
input.focus();

// Show a dialog
const dialog = document.querySelector('wa-dialog');
dialog.show();

// Validate a form
const form = document.querySelector('form');
const isValid = form.checkValidity();

// Reset form controls
form.reset();
```

### Method Examples by Component Type

```javascript
// Form controls
input.focus();                    // Set focus
input.blur();                     // Remove focus
input.select();                   // Select text content
input.setSelectionRange(0, 5);    // Select text range

// Dialogs and overlays
dialog.show();                    // Open dialog
dialog.hide();                    // Close dialog
popup.reposition();               // Recalculate position

// Complex components
carousel.goToSlide(2);            // Navigate to slide
imageComparer.setPosition(50);    // Set comparison position
```

### Common Methods

| Method | Components | Description |
|--------|-----------|-------------|
| `focus()` | Form controls | Sets focus to the element |
| `blur()` | Form controls | Removes focus from the element |
| `show()` | Dialog, Drawer, Dropdown | Shows the element |
| `hide()` | Dialog, Drawer, Dropdown | Hides the element |
| `checkValidity()` | Form controls | Checks if form control is valid |
| `reportValidity()` | Form controls | Shows validation message |

## Slots

### Default Slot

The default slot accepts content without a `slot` attribute:

```html
<!-- Button label goes in default slot -->
<wa-button>Click me</wa-button>

<!-- Card content in default slot -->
<wa-card>
  <p>This content goes in the default slot</p>
</wa-card>
```

### Named Slots

Use the `slot` attribute to target specific slots:

```html
<!-- Button with icon in start slot -->
<wa-button>
  <wa-icon slot="start" name="gear" variant="solid"></wa-icon>
  Settings
</wa-button>

<!-- Card with header and footer slots -->
<wa-card>
  <h3 slot="header">Card Title</h3>
  <p>Main content in default slot</p>
  <div slot="footer">
    <wa-button>Action</wa-button>
  </div>
</wa-card>
```

### Slot Positioning

```html
<!-- Slot order in HTML doesn't matter -->
<wa-dialog>
  <wa-button slot="footer">Close</wa-button>  <!-- Appears in footer -->
  <h2 slot="header">Dialog Title</h2>         <!-- Appears in header -->
  <p>This content appears in the body</p>     <!-- Default slot -->
</wa-dialog>
```

**Important:** Browsers automatically move slotted content to correct positions regardless of HTML order.

### Common Slots by Component

| Component | Available Slots | Description |
|-----------|----------------|-------------|
| Button | `start`, `end` | Icon or content before/after label |
| Card | `header`, `image`, `footer` | Header, image, and footer areas |
| Dialog | `header`, `footer` | Dialog header and footer |
| Alert | `icon` | Custom icon |
| Menu Item | `start`, `end` | Content before/after label |

## Component Updates and Rendering

### Understanding Lit Rendering

WebAwesome components use Lit, which batches updates for performance:

```javascript
// ❌ This won't work as expected
const checkbox = document.querySelector('wa-checkbox');
checkbox.checked = true;
console.log(checkbox.hasAttribute('checked')); // false - update not complete
```

### Waiting for Updates

```javascript
// ✅ Wait for component update
const checkbox = document.querySelector('wa-checkbox');
checkbox.checked = true;

await checkbox.updateComplete;
console.log(checkbox.hasAttribute('checked')); // true - update complete
```

### Multiple Component Updates

```javascript
// Update multiple components and wait for all
const components = document.querySelectorAll('wa-checkbox');
components.forEach(cb => cb.checked = true);

// Wait for next animation frame (all updates batched)
requestAnimationFrame(() => {
  // All components updated
  console.log('All checkboxes updated');
});
```

## Best Practices

### Always Use Closing Tags

```html
<!-- ❌ Don't use self-closing tags -->
<wa-input />
<wa-button />

<!-- ✅ Always include closing tags -->
<wa-input></wa-input>
<wa-button></wa-button>
```

**Reason:** Custom elements cannot be self-closing, similar to `<script>` and `<textarea>` elements.

### API Differences from Native Elements

```html
<!-- Native button defaults to type="submit" -->
<button type="button">Native</button>

<!-- WebAwesome button defaults to type="button" -->
<wa-button>WebAwesome</wa-button>
```

**Important:** Don't assume WebAwesome components have identical APIs to native elements. Always consult component documentation.

### Wait for Component Registration

```javascript
// ✅ Good - wait for registration
await customElements.whenDefined('wa-dialog');
const dialog = document.querySelector('wa-dialog');
dialog.show();

// ❌ Bad - may fail if component not registered
document.querySelector('wa-dialog').show();
```

### Use Semantic HTML

```html
<!-- ✅ Combine WebAwesome with semantic HTML -->
<nav>
  <wa-button>Home</wa-button>
  <wa-button>About</wa-button>
</nav>

<main>
  <wa-card>
    <article>
      <h2>Article Title</h2>
      <p>Content...</p>
    </article>
  </wa-card>
</main>
```

## Performance Considerations

### Batch Property Changes

```javascript
// ❌ Multiple updates trigger multiple renders
button.size = 'large';
button.variant = 'primary';
button.disabled = true;

// ✅ Better - updates are batched automatically by Lit
// But you can optimize further by setting all at once
Object.assign(button, {
  size: 'large',
  variant: 'primary',
  disabled: true
});
```

### Use Event Delegation

```javascript
// ❌ Attach listeners to each button
document.querySelectorAll('wa-button').forEach(btn => {
  btn.addEventListener('click', handleClick);
});

// ✅ Use event delegation
document.addEventListener('click', (e) => {
  if (e.target.tagName === 'WA-BUTTON') {
    handleClick(e);
  }
});
```

### Lazy Load Components

```javascript
// Load components only when needed
async function showDialog() {
  await import('https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/dialog/dialog.js');
  await customElements.whenDefined('wa-dialog');

  const dialog = document.querySelector('wa-dialog');
  dialog.show();
}
```

## Error Prevention

1. **Always use closing tags** for custom elements
2. **Don't assume native element APIs** apply directly
3. **Wait for updates** before checking reflected attributes
4. **Check component documentation** for specific APIs
5. **Handle registration timing** properly in dynamic applications

## Framework Integration

### React

```jsx
import { useRef, useEffect } from 'react';

function MyComponent() {
  const inputRef = useRef();

  useEffect(() => {
    const input = inputRef.current;
    const handleInput = (e) => console.log(e.target.value);
    input.addEventListener('wa-input', handleInput);
    return () => input.removeEventListener('wa-input', handleInput);
  }, []);

  return <wa-input ref={inputRef} label="Name" />;
}
```

### Vue

```vue
<template>
  <wa-input
    ref="input"
    label="Name"
    @wa-input="handleInput"
  />
</template>

<script>
export default {
  methods: {
    handleInput(e) {
      console.log(e.target.value);
    }
  }
}
</script>
```

### Angular

```typescript
import { Component, ViewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-root',
  template: '<wa-input #input label="Name"></wa-input>'
})
export class AppComponent {
  @ViewChild('input') input: ElementRef;

  ngAfterViewInit() {
    this.input.nativeElement.addEventListener('wa-input', (e) => {
      console.log(e.target.value);
    });
  }
}
```

## Troubleshooting

### Components Not Updating

**Problem:** Property changes don't reflect immediately

**Solution:** Wait for `updateComplete` promise

```javascript
button.variant = 'primary';
await button.updateComplete;
// Now the update is complete
```

### Events Not Firing

**Problem:** Standard events don't fire for custom behaviors

**Solution:** Use WebAwesome events with `wa-` prefix

```javascript
// ❌ Wrong
input.addEventListener('input', handler);

// ✅ Correct
input.addEventListener('wa-input', handler);
```

### Styles Not Applied

**Problem:** Components render without styles

**Solution:** Ensure theme CSS is loaded before component scripts

## Related

- [Quick Start](./quick-start.md)
- [Form Controls](../guides/form-controls.md)
- [Component Reference](../components/)
- [Customization](../guides/customizing.md)
