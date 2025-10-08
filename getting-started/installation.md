# Installation

Add WebAwesome to your project using CDN or npm. This guide covers all installation methods and configuration options.

## Overview

WebAwesome v3.0.0-beta.6 offers multiple installation methods to suit different project needs.

## Quick Start (CDN Autoloader)

The fastest way to get started. Add these two lines to your HTML `<head>`:

```html
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/webawesome.css" />
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

### What This Includes

- **WebAwesome styles** - Default theme, native element styles, utility classes
- **Autoloader** - Lightweight script that lazy-loads components as needed

### Benefits

- ✅ Zero configuration required
- ✅ Automatic component loading (even dynamically added elements)
- ✅ Complete WebAwesome feature set
- ✅ Perfect for prototyping and simple projects

### Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My WebAwesome App</title>

  <!-- WebAwesome -->
  <link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/webawesome.css" />
  <script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
</head>
<body>
  <wa-button variant="primary">Click me</wa-button>
  <wa-input label="Email" type="email"></wa-input>
</body>
</html>
```

## Cherry Picking Components (CDN)

Load only specific components to minimize bundle size. Best for production applications.

### Basic Setup

```html
<!-- Required: Default theme -->
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/default.css" />

<!-- Load specific components -->
<script type="module">
  import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/button/button.js';
  import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/input/input.js';

  // Components are ready to use!
</script>
```

### Component Import Pattern

```javascript
// Standard pattern
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/[component-name]/[component-name].js';

// Examples
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/avatar/avatar.js';
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/card/card.js';
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/drawer/drawer.js';
```

### Requirements

1. **Default theme** - Always required for component styling
2. **Additional themes** - Include after default theme if needed
3. **Dependencies** - Automatically loaded for each component

### Advantages

- ✅ Smaller initial bundle size
- ✅ Explicit component loading
- ✅ Better performance for simple applications

### Disadvantages

- ❌ Manual import management per page
- ❌ More complex dependency tracking

## Font Awesome Integration

WebAwesome supports Font Awesome premium icon packs via kit codes.

### Option 1: Data Attribute

```html
<script src="bundle.js" data-fa-kit-code="abc123"></script>
```

### Option 2: JavaScript Method

```javascript
import { setKitCode } from 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js';
setKitCode('YOUR_KIT_CODE_HERE');
```

**Note:** Kit codes unlock premium Font Awesome icon collections for enhanced design options.

## Themes

### Theme Selection

```html
<!-- Default theme (always required) -->
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/default.css" />

<!-- Additional themes (optional, load after default) -->
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/awesome.css" />
```

### Theme Layering

- **Base:** Default theme provides foundational styling
- **Enhancement:** Additional themes override/extend defaults
- **Order:** Load default theme first, then additional themes

## Component Dependencies

### Automatic Dependency Resolution

- Cherry-picked components automatically import their dependencies
- No manual dependency management required
- Check component documentation for dependency lists

### Dependency Chain Example

```javascript
// Importing wa-dialog automatically includes:
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/dialog/dialog.js';
// - wa-icon-button (for close button)
// - wa-popup (for positioning)
// - Related chunks and utilities
```

## File Structure

### CDN Organization

```
webawesome@3.0.0-beta.6/
├── dist/
│   ├── styles/
│   │   ├── webawesome.css           # Complete styles bundle
│   │   └── themes/
│   │       ├── default.css          # Required base theme
│   │       └── awesome.css          # Optional enhanced theme
│   ├── webawesome.loader.js         # Autoloader script
│   ├── components/
│   │   └── [component-name]/
│   │       └── [component-name].js  # Individual components
│   └── chunks/
│       └── chunk.[hash].js          # Generated dependency chunks
```

**Important:** Never import `chunk.[hash].js` files directly - they are auto-generated and version-dependent.

## Installation Method Selection

### Use Autoloader When

- ✅ Prototyping or developing quickly
- ✅ Using many (10+) different components
- ✅ Prioritizing convenience over bundle size
- ✅ Adding components dynamically at runtime

### Use Cherry Picking When

- ✅ Optimizing for production
- ✅ Using few (< 10) components
- ✅ Need precise control over bundle size
- ✅ Components are known at build time

## Best Practices

1. **Always include default theme** when cherry picking
2. **Use autoloader for development** - switch to cherry picking for production optimization
3. **Configure Font Awesome kit codes** early if premium icons are needed
4. **Test component dependencies** when cherry picking complex components
5. **Monitor bundle size** in production builds

## Common Setup Patterns

### Development Setup (Full Autoloader)

```html
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/webawesome.css" />
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

### Production Setup (Cherry Picked)

```html
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/default.css" />
<script type="module">
  // Import only needed components
  import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/button/button.js';
  import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/input/input.js';
</script>
```

## Beta Considerations

- WebAwesome v3.0.0-beta.6 is in active development
- APIs may change between beta versions
- Test thoroughly before production deployment
- Monitor release notes for breaking changes

## Troubleshooting

### Components Not Rendering

**Problem:** Components appear as undefined elements

**Solution:** Ensure the autoloader script has loaded or components are imported correctly

```javascript
// Wait for component registration
await customElements.whenDefined('wa-button');
```

### Styles Not Applied

**Problem:** Components render without styling

**Solution:** Verify the default theme CSS is loaded before component scripts

```html
<!-- CSS must load first -->
<link rel="stylesheet" href=".../themes/default.css" />
<!-- Then component scripts -->
<script type="module" src="..."></script>
```

## Next Steps

Now that WebAwesome is installed, continue to the [Quick Start Guide](./quick-start.md) to build your first components.

## Related

- [Introduction](./introduction.md)
- [Quick Start](./quick-start.md)
- [Usage Guide](./usage.md)
