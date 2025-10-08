# Shadows

WebAwesome's comprehensive shadow system for elevation, depth, and visual hierarchy.

## Overview

WebAwesome's shadow system creates realistic depth effects through a modular property system that indicates elevation and interactivity. Shadows use the semantic `--wa-color-shadow` and scale-based sizing to maintain consistency across all components.

The system consists of:

1. **Predefined shadow scales** - Three elevation levels (small, medium, large)
2. **Shadow component properties** - Offset, blur, and spread controls
3. **Scaling controls** - Global multipliers for each shadow component
4. **Advanced techniques** - Custom colors, multiple shadows, responsive scaling

All shadow values use rem units to scale proportionally with font size, ensuring accessibility and responsive design.

## Shadow Scales

### Predefined Shadow Sizes

Three elevation levels for different visual depth:

```css
--wa-shadow-s    /* Small shadow - subtle elevation */
--wa-shadow-m    /* Medium shadow - moderate elevation */
--wa-shadow-l    /* Large shadow - high elevation */
```

**Shadow Construction:**
Each shadow combines offset-x, offset-y, blur, and spread properties with `--wa-color-shadow`.

**Scaling System:**
Larger shadows indicate greater distance from the surface below.

### Basic Usage

```css
/* Apply predefined shadows */
.card {
  box-shadow: var(--wa-shadow-m);
}

.popup {
  box-shadow: var(--wa-shadow-l);
}

.button:hover {
  box-shadow: var(--wa-shadow-s);
}
```

### Inset Shadows

Create inner shadows for pressed or recessed effects:

```css
/* Inner shadow for input fields */
.input-field {
  box-shadow: inset var(--wa-shadow-s);
}

/* Pressed button state */
.button:active {
  box-shadow: inset var(--wa-shadow-m);
}
```

## Shadow Component Properties

### Horizontal Offset (X-Axis)

#### Properties

```css
--wa-shadow-offset-x-s: 0rem     /* Small shadow X offset */
--wa-shadow-offset-x-m: 0rem     /* Medium shadow X offset */
--wa-shadow-offset-x-l: 0rem     /* Large shadow X offset */
```

#### Scaling Control

```css
--wa-shadow-offset-x-scale: 0    /* Default: no horizontal offset */
```

**Default Behavior:** All shadows center horizontally (0 offset).

**Calculation:** Each offset-x uses `calc()` with the scale multiplier.

#### Custom Horizontal Offsets

```css
/* Add horizontal shadow offset */
:root {
  --wa-shadow-offset-x-scale: 0.5;  /* Creates rightward shadow */
}

/* Component-specific offset */
.sidebar {
  --wa-shadow-offset-x-s: 0.25rem;  /* Override specific size */
}
```

### Vertical Offset (Y-Axis)

#### Properties and Values

```css
--wa-shadow-offset-y-s: 0.125rem  /* 2px - Small downward offset */
--wa-shadow-offset-y-m: 0.25rem   /* 4px - Medium downward offset */
--wa-shadow-offset-y-l: 0.5rem    /* 8px - Large downward offset */
```

#### Scaling Control

```css
--wa-shadow-offset-y-scale: 1     /* Default: normal downward shadows */
```

**Default Behavior:** Downward shadows simulate natural lighting from above.

#### Custom Vertical Offsets

```css
/* Modify shadow direction */
:root {
  --wa-shadow-offset-y-scale: -1;   /* Upward shadows */
}

/* Increase vertical offset */
:root {
  --wa-shadow-offset-y-scale: 1.5;  /* 1.5x downward offset */
}
```

### Blur Radius

#### Properties and Values

```css
--wa-shadow-blur-s: 0.125rem      /* 2px - Sharp, close shadow */
--wa-shadow-blur-m: 0.25rem       /* 4px - Moderate blur */
--wa-shadow-blur-l: 0.5rem        /* 8px - Soft, distant shadow */
```

#### Scaling Control

```css
--wa-shadow-blur-scale: 1         /* Default: normal blur amounts */
```

**Blur Effect:** Larger blur values create greater perceived distance.

#### Custom Blur Control

```css
/* Sharper shadows */
:root {
  --wa-shadow-blur-scale: 0.5;  /* Half blur radius */
}

/* Softer shadows */
:root {
  --wa-shadow-blur-scale: 2;    /* Double blur radius */
}

/* No blur shadows */
.sharp-shadow {
  --wa-shadow-blur-s: 0;
  --wa-shadow-blur-m: 0;
  --wa-shadow-blur-l: 0;
}
```

### Spread Radius

#### Properties and Values

```css
--wa-shadow-spread-s: -0.0625rem  /* -1px - Slight inward spread */
--wa-shadow-spread-m: -0.125rem   /* -2px - Moderate inward spread */
--wa-shadow-spread-l: -0.25rem    /* -4px - Strong inward spread */
```

#### Scaling Control

```css
--wa-shadow-spread-scale: -0.5    /* Default: negative spread for realism */
```

**Negative Spread:** Creates more realistic shadows by shrinking shadow size.

**Positive Spread:** Expands shadow beyond element bounds.

#### Custom Spread Control

```css
/* No spread */
:root {
  --wa-shadow-spread-scale: 0;
}

/* Positive spread (expanded shadows) */
:root {
  --wa-shadow-spread-scale: 0.5;
}

/* Custom spread per size */
.expanded-shadow {
  --wa-shadow-spread-s: 0.125rem;  /* Positive spread */
  --wa-shadow-spread-m: 0.25rem;
  --wa-shadow-spread-l: 0.5rem;
}
```

## Elevation Hierarchy

### Standard Elevation Levels

Create clear visual layers using consistent shadow sizes:

```css
/* Surface level - no shadow */
.surface-level {
  box-shadow: none;
}

/* Raised level - slightly elevated */
.raised-level {
  box-shadow: var(--wa-shadow-s);
}

/* Floating level - moderately elevated */
.floating-level {
  box-shadow: var(--wa-shadow-m);
}

/* Overlay level - highly elevated */
.overlay-level {
  box-shadow: var(--wa-shadow-l);
}
```

### Elevation Usage Guidelines

| Shadow | Elevation | Use Case | Example Components |
|--------|-----------|----------|-------------------|
| None | Ground level | Base surfaces | Page backgrounds, app shells |
| **Small** (`-s`) | Subtle elevation | Buttons, form controls | Buttons, inputs, small cards |
| **Medium** (`-m`) | Moderate elevation | Cards, panels | Cards, panels, dropdowns |
| **Large** (`-l`) | High elevation | Overlays, modals | Modals, dialogs, tooltips |

## Examples

### Interactive Elements

```css
/* Interactive element shadow progression */
.interactive-element {
  box-shadow: var(--wa-shadow-s);
  transition: box-shadow 0.2s ease;
}

.interactive-element:hover {
  box-shadow: var(--wa-shadow-m);
}

.interactive-element:active {
  box-shadow: inset var(--wa-shadow-s);
}
```

### Component Shadows

```css
/* Button with subtle elevation */
.button {
  box-shadow: var(--wa-shadow-s);
}

/* Card with moderate elevation */
.card {
  box-shadow: var(--wa-shadow-m);
}

/* Modal with high elevation */
.modal {
  box-shadow: var(--wa-shadow-l);
}

/* Toolbar at surface level */
.toolbar {
  box-shadow: var(--wa-shadow-s);
}
```

### Input Fields

```css
/* Standard input with inset shadow */
.input {
  box-shadow: inset var(--wa-shadow-s);
}

/* Focused input with outer shadow */
.input:focus {
  box-shadow: var(--wa-shadow-s);
}
```

## Advanced Shadow Customization

### Custom Shadow Colors

```css
/* Use theme shadow color (default) */
.element {
  box-shadow: var(--wa-shadow-m);
  /* Automatically uses --wa-color-shadow */
}

/* Custom shadow color */
.colored-shadow {
  box-shadow:
    var(--wa-shadow-offset-x-m)
    var(--wa-shadow-offset-y-m)
    var(--wa-shadow-blur-m)
    var(--wa-shadow-spread-m)
    rgba(255, 0, 0, 0.2);  /* Red shadow */
}

/* Brand-colored shadow */
.brand-shadow {
  box-shadow:
    0
    0.25rem
    0.5rem
    0
    var(--wa-color-brand-30);
}
```

### Multiple Shadows

Combine multiple shadow effects for complex depth:

```css
/* Layered shadow for enhanced depth */
.complex-shadow {
  box-shadow:
    var(--wa-shadow-s),                     /* Close subtle shadow */
    0 0.5rem 1rem rgba(0, 0, 0, 0.1);     /* Additional distant shadow */
}

/* Inner and outer shadow combination */
.elevated-card {
  box-shadow:
    inset var(--wa-shadow-s),              /* Inner depth */
    var(--wa-shadow-l);                    /* Outer elevation */
}

/* Three-layer shadow for maximum depth */
.dramatic-elevation {
  box-shadow:
    0 0.125rem 0.25rem rgba(0, 0, 0, 0.05),  /* Close, subtle */
    0 0.5rem 1rem rgba(0, 0, 0, 0.1),        /* Mid-range */
    0 1rem 2rem rgba(0, 0, 0, 0.15);         /* Distant, soft */
}
```

### Responsive Shadow Scaling

```css
/* Scale shadows for different viewports */
@media (max-width: 768px) {
  :root {
    --wa-shadow-blur-scale: 0.75;      /* Smaller shadows on mobile */
    --wa-shadow-offset-y-scale: 0.75;
  }
}

@media (min-width: 1200px) {
  :root {
    --wa-shadow-blur-scale: 1.25;      /* Larger shadows on desktop */
    --wa-shadow-offset-y-scale: 1.25;
  }
}
```

## Best Practices

1. **Use predefined shadows** for consistency and performance
2. **Maintain elevation hierarchy** - ground < raised < floating < overlay
3. **Avoid complex multiple shadows** on frequently animated elements
4. **Use shadows purposefully** to indicate interactivity or elevation
5. **Ensure shadows don't interfere** with content readability
6. **Test shadow performance** on lower-end devices
7. **Combine with transitions** for smooth elevation changes

### Do's and Don'ts

```css
/* ✅ Good - consistent system usage */
.button {
  box-shadow: var(--wa-shadow-s);
  transition: box-shadow var(--wa-transition-normal) ease;
}

.button:hover {
  box-shadow: var(--wa-shadow-m);
}

/* ❌ Avoid - hardcoded shadow values */
.button-bad {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* ✅ Good - semantic elevation */
.modal {
  box-shadow: var(--wa-shadow-l);  /* Highest elevation */
}

/* ❌ Avoid - inappropriate elevation */
.text-label {
  box-shadow: var(--wa-shadow-l);  /* Too much for a label */
}
```

## Performance Optimization

### GPU Acceleration

```css
/* Optimize for animated shadows */
.animated-shadow {
  will-change: box-shadow;
  box-shadow: var(--wa-shadow-s);
  transition: box-shadow 0.2s ease;
}

.animated-shadow.completed {
  will-change: auto;  /* Remove after animation */
}
```

### Efficient Animation

```css
/* Prefer transform over shadow animation when possible */
.hover-lift {
  box-shadow: var(--wa-shadow-s);
  transform: translateY(0);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.hover-lift:hover {
  transform: translateY(-2px);
  box-shadow: var(--wa-shadow-m);
}
```

## Accessibility Considerations

### Contrast and Readability

Ensure shadows maintain sufficient contrast without overwhelming content:

```css
/* ✅ Good - subtle shadow doesn't interfere */
.card {
  background: var(--wa-color-surface-default);
  box-shadow: var(--wa-shadow-m);
}

/* ❌ Avoid - shadow too dark, reduces contrast */
.card-bad {
  background: white;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.8);
}
```

### Reduced Motion

Consider user motion preferences when animating shadows:

```css
/* Respect reduced motion preferences */
@media (prefers-reduced-motion: reduce) {
  .interactive-element {
    transition: none;
  }

  .interactive-element:hover {
    box-shadow: var(--wa-shadow-m);
    /* Shadow still changes, but without transition */
  }
}
```

### High Contrast Mode

```css
/* Ensure shadows remain effective in high contrast */
@media (prefers-contrast: high) {
  :root {
    --wa-shadow-blur-scale: 0.5;      /* Sharper shadows */
    --wa-shadow-spread-scale: 0;      /* More defined edges */
  }
}
```

## Troubleshooting

### Shadows Too Subtle

**Solution:** Increase blur scale or use a darker shadow color:

```css
:root {
  --wa-shadow-blur-scale: 1.5;
}
```

### Shadows Too Harsh

**Solution:** Decrease blur scale or use a lighter shadow color:

```css
:root {
  --wa-shadow-blur-scale: 0.7;
}
```

### Shadows Pointing Wrong Direction

**Solution:** Adjust the Y-axis offset scale:

```css
:root {
  --wa-shadow-offset-y-scale: -1;  /* Flip shadow direction */
}
```

### Performance Issues

**Solution:** Reduce shadow complexity and use `will-change` sparingly:

```css
/* Simplify shadows on mobile */
@media (max-width: 768px) {
  .complex-shadow {
    box-shadow: var(--wa-shadow-m);  /* Single shadow instead of multiple */
  }
}
```

## Related

- [Colors](./colors.md)
- [Borders](./borders.md)
- [Transitions](./transitions.md)
- [Customization Guide](../guides/customizing.md)
