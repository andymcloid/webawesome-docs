# Borders

WebAwesome's comprehensive border system for consistent widths, radii, and corner control.

## Overview

WebAwesome's border system provides a flexible, scalable approach to borders and border radii that maintains visual consistency across all components. The system consists of:

1. **Border style** - Line style for all borders
2. **Border widths** - Three sizes with global scaling
3. **Border radii** - Size-based and shape-based options
4. **Scaling controls** - Global multipliers for consistent adjustments

All border values use rem units to scale proportionally with font size, ensuring accessibility and responsive design.

## Border Style

### Custom Property

```css
--wa-border-style: solid;  /* Default border line style */
```

The border style property controls the standard line shape of borders throughout WebAwesome components.

### Example Usage

```css
.custom-border {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-neutral-border-normal);
}
```

## Border Width

### Width Scale

Three size options for different emphasis levels:

```css
--wa-border-width-s: 0.0625rem;  /* 1px - Small borders */
--wa-border-width-m: 0.125rem;   /* 2px - Medium borders */
--wa-border-width-l: 0.1875rem;  /* 3px - Large borders */
```

### Global Scaling

```css
--wa-border-width-scale: 1;  /* Multiplier for all border widths */
```

**Scaling Behavior:**
- Values < 1: Make all borders uniformly thinner
- Values = 1: Default border widths
- Values > 1: Make all borders thicker

### Usage Examples

```css
/* Subtle separator line */
.divider {
  border-bottom: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-border-quiet);
}

/* Standard input outline */
.input-field {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-neutral-border-normal);
}

/* Emphasis border for active states */
.active-button {
  border: var(--wa-border-width-l) var(--wa-border-style) var(--wa-color-brand-border-loud);
}
```

## Border Radius

### Shape-Based Radii

Special radius values for common shapes:

```css
--wa-border-radius-pill: 9999px;  /* Pill/capsule shape */
--wa-border-radius-circle: 50%;   /* Perfect circle */
--wa-border-radius-square: 0px;   /* Sharp corners */
```

### Size-Based Radii

Three size options for different component scales:

```css
--wa-border-radius-s: 0.1875rem;  /* 3px - Small radius */
--wa-border-radius-m: 0.375rem;   /* 6px - Medium radius */
--wa-border-radius-l: 0.75rem;    /* 12px - Large radius */
```

### Global Scaling

```css
--wa-border-radius-scale: 1;  /* Multiplier for all border radii */
```

**Scaling Behavior:**
- Values < 1: Make corners sharper
- Values = 1: Default border radii
- Values > 1: Make corners rounder

### Example Usage

```css
/* Small button with subtle rounding */
.button-small {
  border-radius: var(--wa-border-radius-s);
}

/* Card with medium corners */
.card {
  border-radius: var(--wa-border-radius-m);
}

/* Hero section with large, soft corners */
.hero-panel {
  border-radius: var(--wa-border-radius-l);
}

/* Circular avatar */
.avatar {
  border-radius: var(--wa-border-radius-circle);
  width: 48px;
  height: 48px;
}

/* Pill-shaped badge */
.badge {
  border-radius: var(--wa-border-radius-pill);
  padding: 0.25rem 0.75rem;
}

/* Sharp, technical interface */
.data-table {
  border-radius: var(--wa-border-radius-square);
}
```

## Individual Corner Control

### Controlling Specific Corners

You can apply border radius to specific corners for custom shapes:

```css
/* Top corners rounded, bottom corners square */
.modal-header {
  border-top-left-radius: var(--wa-border-radius-m);
  border-top-right-radius: var(--wa-border-radius-m);
  border-bottom-left-radius: var(--wa-border-radius-square);
  border-bottom-right-radius: var(--wa-border-radius-square);
}

/* Asymmetric rounding */
.speech-bubble {
  border-top-left-radius: var(--wa-border-radius-l);
  border-top-right-radius: var(--wa-border-radius-l);
  border-bottom-right-radius: var(--wa-border-radius-l);
  border-bottom-left-radius: var(--wa-border-radius-s);
}
```

## Selection Guidelines

### Border Width Selection

| Width | Use Case | Example Components |
|-------|----------|-------------------|
| **Small** (`-s`) | Subtle separators, fine outlines | Dividers, input borders, subtle containers |
| **Medium** (`-m`) | Standard component borders | Buttons, cards, form controls |
| **Large** (`-l`) | Emphasis borders, active states | Focus indicators, active selections, highlights |

### Border Radius Selection

| Radius | Use Case | Example Components |
|--------|----------|-------------------|
| **Square** (`0px`) | Technical/data interfaces | Tables, grids, code blocks |
| **Small** (`-s`) | Small components, buttons | Small buttons, chips, tags |
| **Medium** (`-m`) | Standard components | Cards, panels, input fields |
| **Large** (`-l`) | Large containers, hero sections | Hero panels, large cards, modals |
| **Circle** (`50%`) | Avatars, icon buttons | Profile pictures, icon buttons |
| **Pill** (`9999px`) | Toggle switches, badges | Badges, pills, toggle switches |

## Examples

### Button Variants

```css
/* Default button */
.button-default {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-neutral-border-normal);
  border-radius: var(--wa-border-radius-s);
}

/* Pill button */
.button-pill {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-brand-border-loud);
  border-radius: var(--wa-border-radius-pill);
  padding: 0.5rem 1.5rem;
}

/* Icon button */
.button-icon {
  border: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-border-quiet);
  border-radius: var(--wa-border-radius-circle);
  width: 40px;
  height: 40px;
}
```

### Card Designs

```css
/* Standard card */
.card {
  border: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-border-quiet);
  border-radius: var(--wa-border-radius-m);
}

/* Highlighted card */
.card-highlighted {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-brand-border-normal);
  border-radius: var(--wa-border-radius-l);
}

/* Sharp data card */
.card-data {
  border: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-border-normal);
  border-radius: var(--wa-border-radius-square);
}
```

### Input Fields

```css
/* Standard input */
.input {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-neutral-border-normal);
  border-radius: var(--wa-border-radius-s);
}

/* Focused input */
.input:focus {
  border: var(--wa-border-width-l) var(--wa-border-style) var(--wa-color-brand-border-loud);
  border-radius: var(--wa-border-radius-s);
}

/* Error state */
.input-error {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-danger-border-loud);
  border-radius: var(--wa-border-radius-s);
}
```

## Scaling and Customization

### Global Theme Adjustments

```css
/* Softer, rounder theme */
:root {
  --wa-border-radius-scale: 1.5;  /* 50% rounder corners */
}

/* Sharper, thinner theme */
:root {
  --wa-border-width-scale: 0.75;   /* 25% thinner borders */
  --wa-border-radius-scale: 0.5;   /* 50% sharper corners */
}

/* Bolder theme */
:root {
  --wa-border-width-scale: 1.5;    /* 50% thicker borders */
}
```

### Component-Specific Overrides

```css
/* Override radius for specific component */
.custom-card {
  --wa-border-radius-m: 1rem;  /* Custom medium radius */
}

/* Override width for specific context */
.sidebar {
  --wa-border-width-s: 0.125rem;  /* Thicker thin borders in sidebar */
}
```

### Responsive Scaling

```css
/* Adjust borders for mobile */
@media (max-width: 768px) {
  :root {
    --wa-border-radius-scale: 0.75;  /* Slightly sharper on mobile */
  }
}

/* Adjust borders for large screens */
@media (min-width: 1200px) {
  :root {
    --wa-border-radius-scale: 1.25;  /* Rounder on desktop */
  }
}
```

## Best Practices

1. **Use scaling properties** for consistent theme adjustments across all components
2. **Maintain proportional relationships** by using the scale multipliers
3. **Test scaling values** in both large and small font size contexts
4. **Choose semantic border widths** based on emphasis level needed
5. **Match border radius** to component size (small radius for small components)
6. **Use shape-based radii** (pill, circle, square) for their specific use cases
7. **Combine with semantic colors** for consistent, meaningful borders

## Accessibility Considerations

### High Contrast Borders

```css
/* Ensure borders are visible in high contrast mode */
@media (prefers-contrast: high) {
  :root {
    --wa-border-width-scale: 1.5;  /* Thicker borders for visibility */
  }
}
```

### Focus Indicators

```css
/* Use large border width for focus states */
.focusable:focus {
  outline: var(--wa-border-width-l) var(--wa-border-style) var(--wa-color-focus);
  outline-offset: 2px;
}
```

### Readable Boundaries

Ensure border colors maintain adequate contrast with both the background and foreground:

```css
/* ✅ Good - sufficient contrast */
.container {
  background: var(--wa-color-surface-default);
  border: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-border-normal);
}

/* ❌ Avoid - insufficient contrast */
.container-bad {
  background: var(--wa-color-neutral-90);
  border: var(--wa-border-width-s) var(--wa-border-style) var(--wa-color-neutral-95);
}
```

## Troubleshooting

### Borders Look Too Thick/Thin

**Solution:** Adjust the global scale multiplier rather than individual properties:

```css
:root {
  --wa-border-width-scale: 0.8;  /* Make all borders 20% thinner */
}
```

### Corners Too Sharp/Round

**Solution:** Use the radius scale multiplier for global adjustments:

```css
:root {
  --wa-border-radius-scale: 1.3;  /* Make all corners 30% rounder */
}
```

### Inconsistent Border Appearance

**Solution:** Ensure you're using the system properties consistently:

```css
/* ✅ Consistent */
.element {
  border: var(--wa-border-width-m) var(--wa-border-style) var(--wa-color-neutral-border-normal);
}

/* ❌ Inconsistent */
.element {
  border: 2px solid gray;
}
```

## Related

- [Colors](./colors.md)
- [Shadows](./shadows.md)
- [Focus](./focus.md)
- [Customization Guide](../guides/customizing.md)
