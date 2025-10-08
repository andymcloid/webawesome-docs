# Spinner

A loading spinner indicator to show that content is being loaded or processed.

## Overview

The `<wa-spinner>` component provides a visual loading indicator that can be used to show users that an operation is in progress. It supports multiple sizes and can be easily customized to match your application's design.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/spinner/spinner.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default spinner -->
<wa-spinner></wa-spinner>

<!-- With custom size -->
<wa-spinner size="large"></wa-spinner>

<!-- Inline with text -->
<p>
  Loading content <wa-spinner></wa-spinner>
</p>
```

## Sizes

Control spinner size with the `size` attribute:

```html
<wa-spinner size="small"></wa-spinner>
<wa-spinner size="medium"></wa-spinner>
<wa-spinner size="large"></wa-spinner>
```

### Custom Size

You can also set a custom size using CSS:

```html
<wa-spinner style="font-size: 3rem;"></wa-spinner>
```

The spinner scales relative to its font-size, making it easy to adjust to any size.

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `size` | string | `'medium'` | No | Spinner size: `small`, `medium`, `large` |

## Examples

### Loading State in Button

```html
<wa-button id="loadButton" variant="primary">
  <wa-spinner slot="start" id="spinner" style="display: none;"></wa-spinner>
  <span id="buttonText">Load Data</span>
</wa-button>

<script>
  const button = document.getElementById('loadButton');
  const spinner = document.getElementById('spinner');
  const buttonText = document.getElementById('buttonText');

  button.addEventListener('click', async () => {
    spinner.style.display = 'inline-block';
    buttonText.textContent = 'Loading...';
    button.disabled = true;

    try {
      await fetch('/api/data');
      buttonText.textContent = 'Load Data';
    } catch (error) {
      console.error('Error:', error);
    } finally {
      spinner.style.display = 'none';
      button.disabled = false;
    }
  });
</script>
```

### Loading Overlay

```html
<div style="position: relative; min-height: 200px;">
  <div id="content">
    <h3>Content Area</h3>
    <p>This content will be covered by the loading overlay.</p>
  </div>

  <div id="loadingOverlay" style="
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.8);
    align-items: center;
    justify-content: center;
  ">
    <wa-spinner size="large"></wa-spinner>
  </div>
</div>

<script>
  const overlay = document.getElementById('loadingOverlay');

  function showLoading() {
    overlay.style.display = 'flex';
  }

  function hideLoading() {
    overlay.style.display = 'none';
  }
</script>
```

### Centered Page Loading

```html
<div style="
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 400px;
">
  <wa-spinner size="large"></wa-spinner>
</div>
```

### Loading with Message

```html
<div style="text-align: center;">
  <wa-spinner size="large"></wa-spinner>
  <p style="margin-top: 1rem; color: #666;">Loading your data...</p>
</div>
```

## CSS Parts

Use CSS parts to style internal spinner elements:

```css
/* Style the spinner base */
wa-spinner::part(base) {
  color: #3b82f6;
}

/* Change spinner color on hover */
wa-spinner:hover::part(base) {
  color: #2563eb;
}
```

## Customization

### Custom Colors

```css
/* Blue spinner */
wa-spinner.blue::part(base) {
  color: #3b82f6;
}

/* Red spinner */
wa-spinner.red::part(base) {
  color: #ef4444;
}

/* Green spinner */
wa-spinner.green::part(base) {
  color: #10b981;
}
```

### Custom Animation Speed

```css
/* Faster spinner */
wa-spinner.fast::part(base) {
  animation-duration: 0.5s;
}

/* Slower spinner */
wa-spinner.slow::part(base) {
  animation-duration: 2s;
}
```

## Best Practices

- Use spinners to indicate loading or processing states
- Place spinners near the content being loaded when possible
- Use appropriate sizes for the context (small for inline, large for page loading)
- Combine spinners with descriptive text for better user experience
- Remove spinners when loading is complete
- Don't use multiple large spinners on the same screen
- Consider using skeleton screens for initial page loads instead of spinners

## Accessibility

- Spinners automatically include `role="progressbar"` for screen readers
- Use `aria-label` to provide context for screen reader users:

```html
<wa-spinner aria-label="Loading user data"></wa-spinner>
```

- For loading overlays, consider adding `aria-live="polite"` to announce loading states:

```html
<div aria-live="polite" aria-busy="true">
  <wa-spinner aria-label="Loading content"></wa-spinner>
  <span class="sr-only">Loading, please wait...</span>
</div>
```

## Troubleshooting

### Spinner Not Visible

**Problem:** Spinner doesn't appear on the page

**Solution:** Check if the spinner has a visible color and adequate size

```css
/* Ensure spinner is visible */
wa-spinner {
  color: currentColor;
  font-size: 2rem;
}
```

### Spinner Not Animating

**Problem:** Spinner appears but doesn't rotate

**Solution:** Check for CSS that might be disabling animations

```css
/* Ensure animations are enabled */
wa-spinner::part(base) {
  animation: inherit;
}
```

## Related

- [Progress Bar](./progress-bar.md)
- [Button](./button.md)
- [Loading States Guide](../guides/loading-states.md)
