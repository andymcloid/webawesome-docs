# Customizing

Comprehensive guide to customizing WebAwesome components using themes, CSS properties, parts, and states.

## Overview

WebAwesome provides multiple levels of customization to suit different needs:

1. **Themes** - High-level global styling with design tokens
2. **Component Custom Properties** - Component-specific styling without `--wa-` prefix
3. **CSS Parts** - Low-level component internal targeting with `::part()`
4. **Custom States** - State-based styling with `:state()` selector

## Themes

### Theme Application

Add a theme stylesheet to your page `<head>`:

```html
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/default.css" />
<!-- Optional: additional theme -->
<link rel="stylesheet" href="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/styles/themes/awesome.css" />
```

### Theme Customization

Override design tokens using CSS custom properties prefixed with `--wa-`:

```css
:root,
.wa-light,
.wa-dark .wa-invert {
  /* Brand colors */
  --wa-color-brand-fill-quiet: var(--wa-color-purple-95);
  --wa-color-brand-fill-normal: var(--wa-color-purple-90);
  --wa-color-brand-fill-loud: var(--wa-color-purple-50);

  /* Border colors */
  --wa-color-brand-border-quiet: var(--wa-color-purple-90);
  --wa-color-brand-border-normal: var(--wa-color-purple-80);
  --wa-color-brand-border-loud: var(--wa-color-purple-60);

  /* On colors (for text/content) */
  --wa-color-brand-on-quiet: var(--wa-color-purple-40);
  --wa-color-brand-on-normal: var(--wa-color-purple-30);
  --wa-color-brand-on-loud: white;
}
```

### Theme Scope Targeting

| Selector | Purpose |
|----------|---------|
| `:root` | Global fallback for all themes |
| `.wa-light` | Light mode specific styling |
| `.wa-dark` | Dark mode specific styling |
| `.wa-dark .wa-invert` | Inverted elements in dark mode |

### Example: Custom Brand Theme

```css
:root {
  /* Change brand to green */
  --wa-color-brand-05: var(--wa-color-green-05);
  --wa-color-brand-10: var(--wa-color-green-10);
  --wa-color-brand-20: var(--wa-color-green-20);
  --wa-color-brand-30: var(--wa-color-green-30);
  --wa-color-brand-40: var(--wa-color-green-40);
  --wa-color-brand-50: var(--wa-color-green-50);
  --wa-color-brand-60: var(--wa-color-green-60);
  --wa-color-brand-70: var(--wa-color-green-70);
  --wa-color-brand-80: var(--wa-color-green-80);
  --wa-color-brand-90: var(--wa-color-green-90);
  --wa-color-brand-95: var(--wa-color-green-95);

  /* Adjust typography */
  --wa-font-family-body: 'Inter', system-ui, sans-serif;
  --wa-font-size-scale: 1.05;

  /* Adjust spacing */
  --wa-space-scale: 1.1;
}
```

## Component Custom Properties

### Scoped Properties

Components expose custom properties **without** the `--wa-` prefix (component-scoped):

```css
/* CSS targeting */
wa-avatar {
  --size: 6rem;
}

/* Class-specific targeting */
wa-avatar.large {
  --size: 8rem;
}

/* Button customization */
wa-button {
  --border-radius: 0;
  --padding-horizontal: 2rem;
}
```

### Inline Properties

Apply custom properties directly in HTML:

```html
<wa-avatar style="--size: 6rem;"></wa-avatar>
<wa-button style="--border-radius: 20px;">Rounded</wa-button>
<wa-card style="--padding: var(--wa-space-xl);">Large padding</wa-card>
```

### Common Component Properties

| Property | Description | Example Components |
|----------|-------------|-------------------|
| `--size` | Component size | avatar, icon, spinner |
| `--background-color` | Background color | card, button, input |
| `--border-color` | Border color | input, card, button |
| `--border-width` | Border width | input, card |
| `--border-radius` | Corner radius | button, card, input |
| `--color` | Text/content color | button, badge, tag |
| `--padding` | Internal spacing | card, button |

### Example: Custom Button Styles

```css
/* Large rounded primary button */
wa-button.custom-primary {
  --border-radius: 50px;
  --padding-horizontal: 2rem;
  --font-weight: 600;
}

/* Minimal outlined button */
wa-button.minimal {
  --background-color: transparent;
  --border-color: var(--wa-color-neutral-border-quiet);
  --color: var(--wa-color-text-normal);
}
```

## Custom States

### State-based Styling

Use the `:state()` selector to style component based on their internal state:

```css
/* Checked checkbox */
wa-checkbox:state(checked) {
  outline: dotted 2px var(--wa-color-success-border-loud);
}

/* Disabled button */
wa-button:state(disabled) {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Invalid input */
wa-input:state(invalid) {
  --border-color: var(--wa-color-danger-border-loud);
}

/* Focused element */
wa-select:state(focused) {
  box-shadow: 0 0 0 3px var(--wa-color-brand-fill-quiet);
}
```

### Combining States with Parts

Target specific parts of a component in a particular state:

```css
/* Checked checkbox control background */
wa-checkbox:state(checked)::part(control) {
  background: var(--wa-color-success-fill-loud);
  border-color: var(--wa-color-success-border-loud);
}

/* Disabled button base */
wa-button:state(disabled)::part(base) {
  background: var(--wa-color-neutral-fill-quiet);
  color: var(--wa-color-text-quiet);
}
```

## CSS Parts

### Part Targeting

Use the `::part()` selector to target component internals:

```css
/* Button base element */
wa-button::part(base) {
  border-radius: 0;
  text-transform: uppercase;
}

/* Card header */
wa-card::part(header) {
  background: var(--wa-color-brand-fill-quiet);
  border-bottom: 2px solid var(--wa-color-brand-border-normal);
}

/* Input field */
wa-input::part(input) {
  font-family: monospace;
  letter-spacing: 1px;
}

/* Dialog panel */
wa-dialog::part(panel) {
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
}
```

### Part Advantages

1. **Explicit selectors** - `::part(icon)` is clearer than `.button > div > span + .icon`
2. **API stability** - Parts are guaranteed interfaces; internals can change
3. **Intentional design** - Forces consideration of customization points
4. **Better performance** - More efficient than deep descendant selectors

### Common Parts

| Part | Description | Common Components |
|------|-------------|-------------------|
| `base` | Root element of component | button, input, card, dialog |
| `control` | Interactive control element | checkbox, switch, radio |
| `input` | Input field element | input, textarea, select |
| `label` | Label text element | input, checkbox, switch |
| `prefix` | Leading content | input, button |
| `suffix` | Trailing content | input, button |
| `icon` | Icon elements | button, menu-item, alert |
| `content` | Main content area | card, dialog |
| `header` | Header section | card, dialog, drawer |
| `body` | Body section | card, dialog |
| `footer` | Footer section | card, dialog, drawer |

### Example: Custom Card Styling

```css
/* Card with gradient header */
wa-card::part(header) {
  background: linear-gradient(135deg,
    var(--wa-color-brand-50),
    var(--wa-color-purple-50));
  color: white;
  padding: var(--wa-space-l);
}

/* Card body spacing */
wa-card::part(body) {
  padding: var(--wa-space-xl);
  line-height: var(--wa-line-height-expanded);
}

/* Card footer buttons */
wa-card::part(footer) {
  background: var(--wa-color-surface-lowered);
  padding: var(--wa-space-m);
  display: flex;
  justify-content: flex-end;
  gap: var(--wa-space-s);
}
```

## Native Element Compatibility

### Styling Native Counterparts

Apply the same customizations to both WebAwesome components and native elements:

```css
/* Style both component and native checkboxes */
wa-checkbox,
input[type="checkbox"] {
  --size: 1.5rem;
  --border-width: 2px;
}

/* Checked state for both */
wa-checkbox:state(checked)::part(control),
input[type="checkbox"]:checked {
  background: var(--wa-color-success-fill-loud);
}

/* Buttons */
wa-button,
button {
  border-radius: var(--wa-border-radius-m);
  padding: var(--wa-space-s) var(--wa-space-m);
}
```

## Style Utilities

### Attribute and Class Equivalence

Target both attribute variations and utility classes:

```css
/* Support both appearance attribute and class */
wa-callout[appearance="outlined"],
wa-callout.wa-outlined {
  border-left: 4px solid var(--wa-color-brand-border-loud);
}

/* Support variant attribute and class */
wa-button[variant="primary"],
wa-button.primary {
  background: var(--wa-color-brand-fill-loud);
  color: var(--wa-color-brand-on-loud);
}
```

## Examples

### Example 1: Dark Mode Theme

```css
/* Dark mode theme customization */
.wa-dark {
  --wa-color-surface-default: var(--wa-color-gray-10);
  --wa-color-surface-raised: var(--wa-color-gray-20);
  --wa-color-surface-lowered: var(--wa-color-gray-05);

  --wa-color-text-normal: var(--wa-color-gray-95);
  --wa-color-text-quiet: var(--wa-color-gray-70);

  --wa-color-surface-border: var(--wa-color-gray-30);
}
```

### Example 2: Custom Dashboard Components

```css
/* Dashboard card */
.dashboard-card::part(base) {
  border-radius: var(--wa-border-radius-l);
  box-shadow: var(--wa-shadow-m);
  transition: transform var(--wa-transition-normal);
}

.dashboard-card:hover::part(base) {
  transform: translateY(-2px);
  box-shadow: var(--wa-shadow-l);
}

/* Dashboard stat card */
.stat-card::part(header) {
  font-size: var(--wa-font-size-2xl);
  font-weight: var(--wa-font-weight-bold);
  color: var(--wa-color-brand-fill-loud);
}
```

### Example 3: Form Component Styling

```css
/* Consistent form styling */
wa-input,
wa-select,
wa-textarea {
  --border-radius: var(--wa-border-radius-m);
}

wa-input:state(focused)::part(input),
wa-select:state(focused)::part(input),
wa-textarea:state(focused)::part(input) {
  box-shadow: 0 0 0 3px var(--wa-color-brand-fill-quiet);
}

/* Form validation states */
wa-input:state(invalid)::part(base) {
  border-color: var(--wa-color-danger-border-loud);
  background: var(--wa-color-danger-fill-quiet);
}

wa-input:state(valid)::part(base) {
  border-color: var(--wa-color-success-border-normal);
}
```

## Best Practices

### Customization Strategy Priority

1. **Theme tokens** - Use for global, consistent changes across the application
2. **Component properties** - Use for component-specific adjustments
3. **CSS parts** - Use for detailed internal styling of specific components
4. **Custom states** - Use for conditional/interactive styling

### Maintainability

1. ✅ **Use theme tokens** instead of hard-coded values
2. ✅ **Use semantic color names** for better theme adaptability
3. ✅ **Leverage CSS parts** instead of fragile internal selectors
4. ✅ **Document customizations** for easier maintenance
5. ❌ **Don't hardcode colors** - use design tokens
6. ❌ **Don't deeply nest selectors** - use parts instead
7. ❌ **Don't override internal classes** - they may change

### Organization

```css
/* Good: Organized by component and concern */
/* ====== Buttons ====== */
wa-button {
  --border-radius: var(--wa-border-radius-m);
}

wa-button::part(base) {
  text-transform: none;
}

/* ====== Forms ====== */
wa-input,
wa-select {
  --border-color: var(--wa-color-neutral-border-normal);
}
```

### Testing

- ✅ Test customizations in both light and dark modes
- ✅ Verify accessibility (color contrast, focus indicators)
- ✅ Test across different browsers
- ✅ Check responsive behavior

## Accessibility

When customizing components:

- ✅ Maintain sufficient color contrast (WCAG AA minimum)
- ✅ Preserve focus indicators (3:1 contrast minimum)
- ✅ Don't remove outlines without providing alternatives
- ✅ Test with screen readers
- ✅ Ensure touch targets are 44x44px minimum

## Related

- [Colors](../theming/colors.md)
- [Typography](../theming/typography.md)
- [Spacing](../theming/spacing.md)
- [Best Practices](./best-practices.md)
- [Component Reference](../components/)
