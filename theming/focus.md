# Focus

WebAwesome's comprehensive focus system for accessible, consistent keyboard navigation.

## Overview

WebAwesome provides a consistent focus ring system for predictable keyboard navigation across all components. The focus system works in conjunction with `--wa-color-focus` to create uniform, accessible focus states that meet WCAG requirements.

The system consists of:

1. **Focus ring properties** - Style, width, and offset controls
2. **Composite property** - Complete focus ring definition
3. **Focus colors** - Semantic color integration
4. **WCAG compliance** - Accessibility-first approach

All focus indicators are designed to be clearly visible across all color themes while maintaining aesthetic consistency.

## Focus Ring Properties

### Individual Properties

Three core properties define the focus ring appearance:

```css
--wa-focus-ring-style: solid;         /* Focus ring line style */
--wa-focus-ring-width: 0.1875rem;    /* 3px - Focus ring thickness */
--wa-focus-ring-offset: 0.0625rem;   /* 1px - Distance from element */
```

### Property Descriptions

| Property | Default | Purpose |
|----------|---------|---------|
| `--wa-focus-ring-style` | `solid` | Border style (solid, dashed, dotted) |
| `--wa-focus-ring-width` | `0.1875rem` (3px) | Thickness of focus indicator |
| `--wa-focus-ring-offset` | `0.0625rem` (1px) | Gap between element and focus ring |

### Composite Property

Complete focus ring definition combining style, width, and color:

```css
--wa-focus-ring: var(--wa-focus-ring-style) var(--wa-focus-ring-width) var(--wa-color-focus);
```

This composite property is used throughout WebAwesome components for consistent focus indication.

## Implementation

### Standard Focus Application

WebAwesome components automatically apply the focus ring:

```css
/* Automatic application in components */
.component:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}
```

### Manual Focus Application

Apply focus rings to custom focusable elements:

```css
/* Custom interactive element */
.custom-interactive:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* Custom button */
.custom-button:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}
```

### Component Integration

```css
/* Form controls inherit focus ring automatically */
wa-input:focus,
wa-select:focus,
wa-textarea:focus,
wa-checkbox:focus {
  /* Uses --wa-focus-ring automatically */
}

/* Buttons and interactive elements */
wa-button:focus,
wa-link:focus,
wa-icon-button:focus {
  /* Uses --wa-focus-ring automatically */
}
```

## Focus Colors

### Semantic Focus Color

The focus color integrates with WebAwesome's color system:

```css
--wa-color-focus: var(--wa-color-brand-border-loud);  /* Default: brand-themed focus */
```

### Focus Color Options

```css
/* Brand-themed focus (default) */
:root {
  --wa-color-focus: var(--wa-color-brand-border-loud);
}

/* Neutral focus */
:root {
  --wa-color-focus: var(--wa-color-neutral-border-loud);
}

/* High-visibility color options */
:root {
  --wa-color-focus: var(--wa-color-blue-50);   /* Blue focus ring */
}

:root {
  --wa-color-focus: var(--wa-color-orange-50); /* Orange focus ring */
}

/* Success-themed focus */
:root {
  --wa-color-focus: var(--wa-color-success-border-loud);
}
```

## Customization

### Focus Ring Scaling

Adjust focus ring size globally:

```css
/* Thicker focus ring for enhanced visibility */
:root {
  --wa-focus-ring-width: 0.25rem;  /* 4px - Thicker for accessibility */
}

/* Adjust offset proportionally */
:root {
  --wa-focus-ring-offset: 0.125rem;  /* 2px - Larger offset */
}
```

### Custom Focus Styling

Override focus properties for specific components:

```css
/* Dashed focus ring for buttons */
wa-button {
  --wa-focus-ring-style: dashed;
  --wa-focus-ring-width: 0.125rem;  /* 2px instead of 3px */
}

/* Custom focus color for specific context */
.form-group wa-input:focus {
  --wa-color-focus: var(--wa-color-brand-border-normal);
}
```

### Contextual Focus Styles

Different focus styles for different contexts:

```css
/* Toolbar focus style */
.toolbar wa-button:focus {
  --wa-focus-ring-style: dotted;
  --wa-focus-ring-offset: 0.125rem;
}

/* Card focus style */
.card:focus {
  --wa-focus-ring-width: 0.125rem;
  --wa-focus-ring-offset: 0.25rem;
}
```

## Advanced Techniques

### Focus-Within Styling

Style containers when child elements are focused:

```css
/* Card highlights when any child is focused */
.card:focus-within {
  box-shadow: 0 0 0 var(--wa-focus-ring-width) var(--wa-color-focus);
  border-color: var(--wa-color-focus);
}

/* Form group highlights on input focus */
.form-group:focus-within {
  background: var(--wa-color-brand-fill-quiet);
}
```

### Focus-Visible vs Focus

Use `:focus-visible` for keyboard-only focus indicators:

```css
/* Show focus ring only for keyboard navigation */
.button:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* Hide focus ring for mouse clicks */
.button:focus:not(:focus-visible) {
  outline: none;
}
```

### Custom Focus Effects

```css
/* Glow effect on focus */
.input:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
  box-shadow: 0 0 0 4px rgba(var(--wa-color-focus-rgb), 0.2);
}

/* Animated focus ring */
.button:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
  transition: outline-offset var(--wa-transition-fast) ease;
}

.button:focus:active {
  outline-offset: 0;
}
```

## Responsive Focus Adjustments

### Mobile Optimization

Larger focus rings for touch accessibility:

```css
@media (max-width: 768px) {
  :root {
    --wa-focus-ring-width: 0.25rem;    /* 4px - Thicker on mobile */
    --wa-focus-ring-offset: 0.125rem;  /* 2px - Larger offset */
  }
}
```

### Large Screen Adjustments

```css
@media (min-width: 1200px) {
  :root {
    --wa-focus-ring-width: 0.1875rem;  /* 3px - Standard on desktop */
    --wa-focus-ring-offset: 0.125rem;  /* 2px - Larger offset for comfort */
  }
}
```

## WCAG Compliance

### Contrast Requirements

Focus indicators must meet WCAG contrast requirements:

- **Minimum 3:1 contrast ratio** between focus color and adjacent colors
- **Visible indication** for all interactive elements
- **Consistent appearance** across all focusable components

### Ensuring Sufficient Contrast

```css
/* ✅ Good - high contrast focus color */
:root {
  --wa-color-focus: var(--wa-color-blue-50);  /* High contrast on most backgrounds */
}

/* ❌ Avoid - low contrast on light backgrounds */
:root {
  --wa-color-focus: var(--wa-color-gray-90);  /* May not have 3:1 contrast */
}
```

### Testing Focus Visibility

Test focus indicators against all background colors:

```css
/* Ensure focus is visible on dark backgrounds */
.dark-background .button:focus {
  --wa-color-focus: var(--wa-color-blue-70);  /* Lighter color for dark backgrounds */
}

/* Ensure focus is visible on light backgrounds */
.light-background .button:focus {
  --wa-color-focus: var(--wa-color-blue-30);  /* Darker color for light backgrounds */
}
```

## Examples

### Form Controls

```css
/* Standard input focus */
.input:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
  border-color: var(--wa-color-focus);
}

/* Checkbox focus */
.checkbox:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* Select focus */
.select:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}
```

### Buttons

```css
/* Primary button focus */
.button-primary:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* Icon button focus */
.button-icon:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: 0.125rem;  /* Larger offset for circular buttons */
}

/* Link button focus */
.button-link:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: 0.25rem;  /* Extra space for inline context */
}
```

### Cards and Panels

```css
/* Focusable card */
.card[tabindex]:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* Accordion header focus */
.accordion-header:focus {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}
```

## Best Practices

1. **Always provide focus indicators** for all interactive elements
2. **Use `:focus-visible`** when appropriate to avoid focus rings on mouse clicks
3. **Maintain consistent focus appearance** across all components
4. **Test focus visibility** on all background colors
5. **Ensure 3:1 minimum contrast** for focus indicators
6. **Respect user preferences** for reduced motion when animating focus
7. **Don't remove focus indicators** without providing alternatives

### Do's and Don'ts

```css
/* ✅ Good - clear, visible focus indicator */
.button:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
}

/* ❌ Avoid - removing focus without alternative */
.button:focus {
  outline: none;  /* Don't do this! */
}

/* ✅ Good - custom focus with sufficient contrast */
.button:focus-visible {
  outline: 3px solid var(--wa-color-brand-50);
  outline-offset: 2px;
}

/* ❌ Avoid - insufficient contrast */
.button:focus {
  outline: 1px solid rgba(0, 0, 0, 0.1);
}
```

## Common Patterns

### High Visibility Focus

```css
:root {
  --wa-focus-ring-width: 0.25rem;
  --wa-color-focus: var(--wa-color-orange-50);
}
```

### Subtle Focus

```css
:root {
  --wa-focus-ring-width: 0.125rem;
  --wa-color-focus: var(--wa-color-neutral-border-loud);
}
```

### Brand-Coordinated Focus

```css
:root {
  --wa-color-focus: var(--wa-color-brand-border-loud);
  --wa-focus-ring-width: 0.1875rem;
}
```

### Animated Focus

```css
.interactive:focus-visible {
  outline: var(--wa-focus-ring);
  outline-offset: var(--wa-focus-ring-offset);
  animation: focus-pulse 2s infinite;
}

@keyframes focus-pulse {
  0%, 100% { outline-offset: var(--wa-focus-ring-offset); }
  50% { outline-offset: calc(var(--wa-focus-ring-offset) + 2px); }
}

/* Disable animation for reduced motion */
@media (prefers-reduced-motion: reduce) {
  .interactive:focus-visible {
    animation: none;
  }
}
```

## Accessibility Considerations

### High Contrast Mode

```css
/* Enhance focus in high contrast mode */
@media (prefers-contrast: high) {
  :root {
    --wa-focus-ring-width: 0.25rem;  /* Thicker for high contrast */
  }
}
```

### Reduced Motion

```css
/* Respect reduced motion for focus animations */
@media (prefers-reduced-motion: reduce) {
  .button:focus {
    transition: none;
  }
}
```

### Keyboard Navigation

Ensure focus order is logical:

```html
<!-- ✅ Good - logical tab order -->
<nav>
  <a href="#home">Home</a>
  <a href="#about">About</a>
  <a href="#contact">Contact</a>
</nav>

<!-- ❌ Avoid - manipulated tab order without reason -->
<nav>
  <a href="#home" tabindex="3">Home</a>
  <a href="#about" tabindex="1">About</a>
  <a href="#contact" tabindex="2">Contact</a>
</nav>
```

## Troubleshooting

### Focus Ring Not Visible

**Solution:** Increase contrast or thickness:

```css
:root {
  --wa-focus-ring-width: 0.25rem;
  --wa-color-focus: var(--wa-color-blue-50);
}
```

### Focus Ring Too Prominent

**Solution:** Reduce width or use subtler color:

```css
:root {
  --wa-focus-ring-width: 0.125rem;
  --wa-color-focus: var(--wa-color-neutral-border-loud);
}
```

### Focus Ring Doesn't Match Theme

**Solution:** Update focus color to match theme:

```css
:root {
  --wa-color-focus: var(--wa-color-brand-border-loud);
}
```

### Focus Ring Clipped by Container

**Solution:** Ensure container doesn't clip outline:

```css
.container {
  overflow: visible;  /* Don't clip focus rings */
  padding: 0.5rem;    /* Add padding for focus ring space */
}
```

## Related

- [Colors](./colors.md)
- [Borders](./borders.md)
- [Transitions](./transitions.md)
- [Accessibility Guide](../guides/accessibility.md)
- [Keyboard Navigation Guide](../guides/keyboard-navigation.md)
