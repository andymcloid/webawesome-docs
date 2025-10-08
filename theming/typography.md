# Typography

WebAwesome's comprehensive typography system for consistent, readable, and accessible text styling.

## Overview

WebAwesome's typography system provides consistent text styling through role-based font families, proportional sizing scales, semantic weights, and readable line heights. The system consists of:

1. **Font families** - Role-based fonts for different content types
2. **Font sizes** - Proportional scale system with global scaling support
3. **Font weights** - Semantic weights for clear hierarchy
4. **Line heights** - Optimized spacing for readability
5. **Link styling** - Consistent link decoration

The system prioritizes performance with system fonts while maintaining easy customization for brand-specific typography.

## Font Families

### Format

```css
--wa-font-family-{role}
```

### Available Roles

WebAwesome provides four role-based font families:

```css
--wa-font-family-body      /* Body text, UI elements */
--wa-font-family-heading   /* Headings (inherits body by default) */
--wa-font-family-code      /* Code, technical text */
--wa-font-family-longform  /* Articles, longform content */
```

### Default Values

```css
--wa-font-family-body: ui-sans-serif, system-ui, sans-serif
--wa-font-family-heading: var(--wa-font-family-body)
--wa-font-family-code: ui-monospace, monospace
--wa-font-family-longform: ui-serif, serif
```

### Usage

```css
/* Apply role-based fonts */
body {
  font-family: var(--wa-font-family-body);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--wa-font-family-heading);
}

code, pre, .code-block {
  font-family: var(--wa-font-family-code);
}

article, .longform-content {
  font-family: var(--wa-font-family-longform);
}
```

### Custom Font Integration

Replace system fonts with custom fonts by updating the CSS variables:

```css
/* Import custom font */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap');

/* Apply to role-based properties */
:root {
  --wa-font-family-body: 'Inter', ui-sans-serif, system-ui, sans-serif;
  --wa-font-family-heading: 'Inter', ui-sans-serif, system-ui, sans-serif;
}
```

**Best Practice:** Always include fallback fonts for loading states and font availability.

## Font Sizes

### Format

```css
--wa-font-size-{scale}
```

### Scale System

WebAwesome uses a 1.125 ratio (Major Second) for proportional scaling:

| Property | Calculation | Default Value | Use Case |
|----------|-------------|---------------|----------|
| `--wa-font-size-2xs` | `round(calc(var(--wa-font-size-xs) / 1.125), 1px)` | 11px | Fine print, captions |
| `--wa-font-size-xs` | `round(calc(var(--wa-font-size-s) / 1.125), 1px)` | 12px | Small text, labels |
| `--wa-font-size-s` | `round(calc(var(--wa-font-size-m) / 1.125), 1px)` | 14px | Secondary text |
| `--wa-font-size-m` | `calc(1rem * var(--wa-font-size-scale))` | 16px | Body text (base) |
| `--wa-font-size-l` | `round(calc(var(--wa-font-size-m) * 1.125 * 1.125), 1px)` | 20px | Subheadings |
| `--wa-font-size-xl` | `round(calc(var(--wa-font-size-l) * 1.125 * 1.125), 1px)` | 25px | Small headings |
| `--wa-font-size-2xl` | `round(calc(var(--wa-font-size-xl) * 1.125 * 1.125), 1px)` | 32px | Medium headings |
| `--wa-font-size-3xl` | `round(calc(var(--wa-font-size-2xl) * 1.125 * 1.125), 1px)` | 41px | Large headings |
| `--wa-font-size-4xl` | `round(calc(var(--wa-font-size-3xl) * 1.125 * 1.125), 1px)` | 52px | Display headings |

### Global Scaling

Adjust all font sizes proportionally using the `--wa-font-size-scale` variable:

```css
/* Default scaling (100%) */
--wa-font-size-scale: 1;

/* Increase all font sizes by 12.5% */
:root {
  --wa-font-size-scale: 1.125;
}

/* Decrease all font sizes by 10% */
:root {
  --wa-font-size-scale: 0.9;
}
```

### Relative Size Properties

For context-relative sizing that adapts to parent font size:

```css
--wa-font-size-smaller: round(calc(1em / 1.125), 1px)           /* Smaller than parent */
--wa-font-size-larger: round(calc(1em * 1.125 * 1.125), 1px)   /* Larger than parent */
```

**Usage:**

```css
/* Always relative to parent */
.small-caption {
  font-size: var(--wa-font-size-smaller);
}

.emphasis-text {
  font-size: var(--wa-font-size-larger);
}
```

### Typography Hierarchy

Establish clear visual hierarchy with the font size scale:

```css
h1 { font-size: var(--wa-font-size-4xl); }   /* 52px - Display */
h2 { font-size: var(--wa-font-size-3xl); }   /* 41px - Major heading */
h3 { font-size: var(--wa-font-size-2xl); }   /* 32px - Section heading */
h4 { font-size: var(--wa-font-size-xl); }    /* 25px - Subsection */
h5 { font-size: var(--wa-font-size-l); }     /* 20px - Minor heading */
h6 { font-size: var(--wa-font-size-m); }     /* 16px - Small heading */

body { font-size: var(--wa-font-size-m); }   /* 16px - Body text */
.small { font-size: var(--wa-font-size-s); } /* 14px - Secondary */
.caption { font-size: var(--wa-font-size-xs); } /* 12px - Captions */
```

## Font Weights

### Format

```css
--wa-font-weight-{weight}
--wa-font-weight-{role}
```

### Common Weights

Standard numeric weights:

```css
--wa-font-weight-light: 300       /* Light text */
--wa-font-weight-normal: 400      /* Regular text */
--wa-font-weight-semibold: 500    /* Medium emphasis */
--wa-font-weight-bold: 600        /* Strong emphasis */
```

### Role-Based Weights

Semantic weights for specific content types:

```css
--wa-font-weight-body: var(--wa-font-weight-normal)       /* Body text weight */
--wa-font-weight-heading: var(--wa-font-weight-bold)      /* Heading weight */
--wa-font-weight-action: var(--wa-font-weight-semibold)   /* Interactive text weight */
```

### Usage

```css
/* Apply semantic weights */
body {
  font-weight: var(--wa-font-weight-body);
}

h1, h2, h3, h4, h5, h6 {
  font-weight: var(--wa-font-weight-heading);
}

/* Action weight for interactive elements */
a, button, .interactive-text {
  font-weight: var(--wa-font-weight-action);
}

/* Accessible links without underline */
.link-no-decoration {
  font-weight: var(--wa-font-weight-action); /* Weight signals interactivity */
  text-decoration: none;
}
```

### Customization

Adjust weights globally or per component:

```css
/* Adjust weights globally */
:root {
  --wa-font-weight-body: 300;     /* Lighter body text */
  --wa-font-weight-heading: 700;  /* Bolder headings */
  --wa-font-weight-action: 600;   /* Stronger action emphasis */
}

/* Component-specific weights */
.data-table {
  --wa-font-weight-body: 400;     /* Standard weight for data */
}
```

## Line Heights

### Format

```css
--wa-line-height-{spacing}
```

### Available Spacing

```css
--wa-line-height-condensed: 1.2   /* Tight spacing for headings */
--wa-line-height-normal: 1.6      /* Comfortable reading for body text */
--wa-line-height-expanded: 2      /* Spacious for special emphasis */
```

### Usage

```css
/* Apply appropriate line heights */
h1, h2, h3, h4, h5, h6 {
  line-height: var(--wa-line-height-condensed);
}

body, p, article {
  line-height: var(--wa-line-height-normal); /* Optimal readability */
}

.pull-quote, .important-text {
  line-height: var(--wa-line-height-expanded);
}
```

**Accessibility Note:** `--wa-line-height-normal` (1.6) exceeds WCAG's 1.5 minimum requirement for optimal readability.

## Link Styling

### Format

```css
--wa-link-decoration-{state}
```

### Available Properties

```css
--wa-link-decoration-default: underline color-mix(in oklab, var(--wa-color-text-link) 70%, transparent) dotted;
--wa-link-decoration-hover: underline;
```

### Usage

```css
/* Default link styling */
a {
  color: var(--wa-color-text-link);
  text-decoration: var(--wa-link-decoration-default);
  font-weight: var(--wa-font-weight-action);
}

a:hover {
  text-decoration: var(--wa-link-decoration-hover);
}

/* Custom link decorations */
.subtle-link {
  --wa-link-decoration-default: underline transparent;
  --wa-link-decoration-hover: underline var(--wa-color-text-link);
}
```

## Examples

### Responsive Typography

Scale typography for different viewports:

```css
/* Mobile devices */
@media (max-width: 768px) {
  :root {
    --wa-font-size-scale: 0.9;           /* Smaller on mobile */
    --wa-line-height-normal: 1.5;        /* Tighter line height */
  }
}

/* Large desktop */
@media (min-width: 1200px) {
  :root {
    --wa-font-size-scale: 1.1;           /* Larger on desktop */
  }
}
```

### Component Typography

Apply typography to WebAwesome components:

```css
/* Card typography */
wa-card {
  font-family: var(--wa-font-family-body);
  font-size: var(--wa-font-size-m);
  line-height: var(--wa-line-height-normal);
}

wa-card::part(header) {
  font-size: var(--wa-font-size-l);
  font-weight: var(--wa-font-weight-heading);
  line-height: var(--wa-line-height-condensed);
}

/* Button typography */
wa-button {
  font-family: var(--wa-font-family-body);
  font-weight: var(--wa-font-weight-action);
  font-size: var(--wa-font-size-m);
}
```

### Utility Classes

Create utility classes for common typography patterns:

```css
/* Font size utilities */
.text-xs { font-size: var(--wa-font-size-xs); }
.text-sm { font-size: var(--wa-font-size-s); }
.text-base { font-size: var(--wa-font-size-m); }
.text-lg { font-size: var(--wa-font-size-l); }
.text-xl { font-size: var(--wa-font-size-xl); }

/* Font weight utilities */
.font-light { font-weight: var(--wa-font-weight-light); }
.font-normal { font-weight: var(--wa-font-weight-normal); }
.font-semibold { font-weight: var(--wa-font-weight-semibold); }
.font-bold { font-weight: var(--wa-font-weight-bold); }

/* Line height utilities */
.leading-tight { line-height: var(--wa-line-height-condensed); }
.leading-normal { line-height: var(--wa-line-height-normal); }
.leading-loose { line-height: var(--wa-line-height-expanded); }
```

### Common Typography Patterns

```css
/* Article/blog post typography */
.article {
  font-family: var(--wa-font-family-longform);
  font-size: var(--wa-font-size-m);
  line-height: var(--wa-line-height-normal);
}

.article h1 {
  font-size: var(--wa-font-size-3xl);
  font-weight: var(--wa-font-weight-heading);
  line-height: var(--wa-line-height-condensed);
}

/* UI component typography */
.ui-text {
  font-family: var(--wa-font-family-body);
  font-size: var(--wa-font-size-s);
  font-weight: var(--wa-font-weight-normal);
}

/* Interactive element typography */
.interactive {
  font-weight: var(--wa-font-weight-action);
  color: var(--wa-color-text-link);
}
```

## Best Practices

1. **Use role-based properties** - Prefer semantic font families and weights over specific values
2. **Maintain scale consistency** - Stay within the defined font size scale for proportional harmony
3. **Leverage system fonts** - Use system fonts for optimal performance when possible
4. **Test across devices** - Verify readability on various screen sizes and resolutions
5. **Establish clear hierarchy** - Use font sizes and weights to create visual hierarchy
6. **Optimize custom fonts** - Use font-display: swap and subset fonts to improve loading
7. **Respect user preferences** - Use rem units to honor user's font size settings
8. **Avoid too many weights** - Limit custom font weights to improve performance

## Accessibility

### Requirements

- **Minimum font size** - Ensure 16px+ for body text
- **Line height minimum** - Use 1.5+ for body text (WebAwesome default: 1.6)
- **Color contrast** - Test text color against backgrounds (4.5:1 minimum for normal text)
- **Relative units** - Use rem/em units to respect user font preferences
- **Font loading** - Provide fallback fonts during custom font loading

### Implementation Guidelines

1. **Line height spacing** - `--wa-line-height-normal` (1.6) exceeds WCAG's 1.5 minimum
2. **Interactive elements** - Use `--wa-font-weight-action` to signal interactivity without relying solely on color
3. **Links without underline** - Increase font weight to maintain accessibility when removing underlines
4. **Readable base size** - Default 16px body text ensures readability for all users
5. **User preferences** - rem-based sizing respects user's browser font settings

### Testing Checklist

- Test with browser zoom at 200%
- Verify text remains readable at different font sizes
- Check contrast ratios for all text/background combinations
- Test with different system font settings
- Ensure custom fonts have proper fallbacks

## Related

- [Colors](./colors.md)
- [Customization Guide](../guides/customizing.md)
- [Accessibility](../guides/accessibility.md)
