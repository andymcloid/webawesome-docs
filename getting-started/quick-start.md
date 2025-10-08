# Quick Start

Get up and running with WebAwesome in minutes. This guide walks you through creating your first WebAwesome application.

## Overview

This quick start guide demonstrates the fastest way to start using WebAwesome components with the CDN autoloader.

## Step 1: Create HTML File

Create a new HTML file with the basic WebAwesome setup:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WebAwesome Quick Start</title>

  <!-- WebAwesome CSS -->
  <link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/webawesome.css" />

  <!-- WebAwesome Autoloader -->
  <script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
</head>
<body>
  <h1>My First WebAwesome App</h1>
</body>
</html>
```

## Step 2: Add Components

Add WebAwesome components to your HTML just like regular HTML elements:

```html
<body>
  <h1>My First WebAwesome App</h1>

  <!-- Button Component -->
  <wa-button variant="primary">Primary Button</wa-button>

  <!-- Input Component -->
  <wa-input label="Email" type="email" placeholder="Enter your email"></wa-input>

  <!-- Card Component -->
  <wa-card>
    <h3 slot="header">Card Title</h3>
    <p>This is a card with some content inside.</p>
    <wa-button slot="footer" variant="primary">Action</wa-button>
  </wa-card>
</body>
```

## Step 3: Add Interactivity

Add JavaScript to handle component events:

```html
<body>
  <wa-button id="myButton" variant="primary">Click me</wa-button>
  <wa-alert id="myAlert" variant="success" closable>
    <wa-icon slot="icon" name="check-circle"></wa-icon>
    <strong>Success!</strong> You clicked the button.
  </wa-alert>

  <script type="module">
    const button = document.getElementById('myButton');
    const alert = document.getElementById('myAlert');

    // Initially hide the alert
    alert.hide();

    // Show alert when button is clicked
    button.addEventListener('click', () => {
      alert.show();
    });
  </script>
</body>
```

## Complete Example

Here's a complete example showcasing multiple components:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WebAwesome Demo</title>

  <link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/webawesome.css" />
  <script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>

  <style>
    body {
      max-width: 600px;
      margin: 2rem auto;
      padding: 1rem;
      font-family: var(--wa-font-family-body);
    }

    .demo-section {
      margin-bottom: 2rem;
    }
  </style>
</head>
<body>
  <h1>WebAwesome Component Demo</h1>

  <!-- Buttons -->
  <div class="demo-section">
    <h2>Buttons</h2>
    <wa-button variant="default">Default</wa-button>
    <wa-button variant="primary">Primary</wa-button>
    <wa-button variant="success">Success</wa-button>
    <wa-button variant="danger">Danger</wa-button>
  </div>

  <!-- Form -->
  <div class="demo-section">
    <h2>Form Controls</h2>
    <wa-input label="Name" placeholder="Enter your name"></wa-input>
    <br><br>
    <wa-select label="Choose an option" placeholder="Select one">
      <wa-option value="1">Option 1</wa-option>
      <wa-option value="2">Option 2</wa-option>
      <wa-option value="3">Option 3</wa-option>
    </wa-select>
    <br><br>
    <wa-checkbox>I agree to the terms</wa-checkbox>
    <br><br>
    <wa-switch>Enable notifications</wa-switch>
  </div>

  <!-- Card -->
  <div class="demo-section">
    <h2>Card</h2>
    <wa-card>
      <img slot="image" src="https://images.unsplash.com/photo-1559209172-0ff8f6d49ff7?w=400" alt="Example">
      <h3 slot="header">Card Header</h3>
      <p>Cards are containers for content with optional headers, footers, and images.</p>
      <div slot="footer">
        <wa-button variant="primary">Learn More</wa-button>
      </div>
    </wa-card>
  </div>

  <!-- Dialog Demo -->
  <div class="demo-section">
    <h2>Dialog</h2>
    <wa-button id="openDialog">Open Dialog</wa-button>

    <wa-dialog id="myDialog" label="Welcome">
      <p>This is a dialog component. It can be used for modals, confirmations, and more.</p>
      <wa-button slot="footer" variant="primary">Close</wa-button>
    </wa-dialog>
  </div>

  <script type="module">
    // Dialog interaction
    const openDialogBtn = document.getElementById('openDialog');
    const dialog = document.getElementById('myDialog');
    const closeBtn = dialog.querySelector('[slot="footer"]');

    openDialogBtn.addEventListener('click', () => dialog.show());
    closeBtn.addEventListener('click', () => dialog.hide());

    // Form validation example
    const nameInput = document.querySelector('wa-input[label="Name"]');
    nameInput.addEventListener('wa-input', (e) => {
      console.log('Name changed to:', e.target.value);
    });
  </script>
</body>
</html>
```

## Common Patterns

### Setting Component Properties

```javascript
// Get component reference
const button = document.querySelector('wa-button');

// Set properties
button.size = 'large';
button.variant = 'primary';
button.disabled = true;
```

### Listening to Events

```javascript
// Standard events
button.addEventListener('click', () => {
  console.log('Button clicked');
});

// Custom WebAwesome events (wa- prefix)
input.addEventListener('wa-input', (e) => {
  console.log('Value:', e.target.value);
});

dialog.addEventListener('wa-after-show', () => {
  console.log('Dialog opened');
});
```

### Using Slots

```html
<!-- Named slots -->
<wa-button>
  <wa-icon slot="start" name="gear"></wa-icon>
  Settings
  <wa-icon slot="end" name="chevron-right"></wa-icon>
</wa-button>

<!-- Default slot -->
<wa-card>
  This content goes in the default slot
</wa-card>
```

## Framework Integration

### React

```jsx
import { useRef } from 'react';

function MyComponent() {
  const buttonRef = useRef();

  const handleClick = () => {
    console.log('Button clicked');
  };

  return (
    <wa-button ref={buttonRef} onClick={handleClick}>
      Click me
    </wa-button>
  );
}
```

### Vue

```vue
<template>
  <wa-button @click="handleClick" variant="primary">
    Click me
  </wa-button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      console.log('Button clicked');
    }
  }
}
</script>
```

### Angular

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <wa-button (click)="handleClick()" variant="primary">
      Click me
    </wa-button>
  `
})
export class AppComponent {
  handleClick() {
    console.log('Button clicked');
  }
}
```

## Next Steps

Now that you've created your first WebAwesome app, explore these topics:

- **[Usage Guide](./usage.md)** - Deep dive into component APIs, events, and methods
- **[Component Reference](../components/)** - Browse all available components
- **[Theming](../theming/)** - Customize colors, spacing, and typography
- **[Form Controls](../guides/form-controls.md)** - Learn about form validation and submission

## Best Practices

1. ✅ **Always use closing tags** - Custom elements require closing tags (`<wa-button></wa-button>`)
2. ✅ **Wait for component registration** - Use `customElements.whenDefined()` before manipulating components
3. ✅ **Use semantic HTML** - Combine WebAwesome components with standard HTML elements
4. ✅ **Leverage slots** - Use named slots for flexible component composition
5. ❌ **Don't use self-closing tags** - `<wa-button />` won't work

## Troubleshooting

### Components Not Appearing

Ensure the autoloader script is loaded before components are used:

```html
<!-- Load autoloader first -->
<script type="module" src=".../webawesome.loader.js"></script>

<!-- Then use components -->
<wa-button>Click me</wa-button>
```

### Styles Not Applied

Verify the WebAwesome CSS is loaded:

```html
<link rel="stylesheet" href=".../webawesome.css" />
```

### Events Not Firing

WebAwesome custom events use the `wa-` prefix:

```javascript
// ❌ Wrong
input.addEventListener('input', handler);

// ✅ Correct
input.addEventListener('wa-input', handler);
```

## Related

- [Introduction](./introduction.md)
- [Installation](./installation.md)
- [Usage Guide](./usage.md)
- [Component Reference](../components/)
