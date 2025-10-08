# Colors

WebAwesome's comprehensive color system for consistent, accessible, and semantic color usage.

## Overview

WebAwesome's color system consists of three main categories that work together to create flexible, maintainable themes:

1. **Color scales** - Full spectrum of hues (lowest level tokens)
2. **Foundational colors** - Structural elements (surfaces, text, etc.)
3. **Semantic colors** - Meaningful colors that convey state/intent

## Color Scales

### Format

```css
--wa-color-{hue}-{tint}
```

### Tint Scale

Tints range from 0 (pure black) to 100 (pure white) in increments of 5 and 10:
- Available tints: `05`, `10`, `20`, `30`, `40`, `50`, `60`, `70`, `80`, `90`, `95`

### WCAG Contrast Guidelines

| Tint Difference | Contrast Ratio | WCAG Level | Use Case |
|----------------|----------------|------------|----------|
| 40 | 3:1 | AA | Large text, icons |
| 50 | 4.5:1 | AA / AAA | Normal text / Large text |
| 60 | 7:1 | AAA | All text sizes |

### Available Hues

Each hue has 11 tints (05, 10, 20, 30, 40, 50, 60, 70, 80, 90, 95):

```css
--wa-color-red-{05-95}
--wa-color-orange-{05-95}
--wa-color-yellow-{05-95}
--wa-color-green-{05-95}
--wa-color-cyan-{05-95}
--wa-color-blue-{05-95}
--wa-color-indigo-{05-95}
--wa-color-purple-{05-95}
--wa-color-pink-{05-95}
--wa-color-gray-{05-95}
```

### Example Usage

```css
.example {
  /* Use specific hue and tint */
  background: var(--wa-color-blue-90);
  color: var(--wa-color-blue-30); /* 60 tint difference = AAA contrast */
}
```

## Semantic Scales

Semantic color groups map to specific hues for meaningful color usage.

### Format

```css
--wa-color-{group}-{tint}
```

### Available Groups

```css
--wa-color-brand-{05-95}   /* Your brand color */
--wa-color-neutral-{05-95} /* Grays for UI elements */
--wa-color-success-{05-95} /* Success states */
--wa-color-warning-{05-95} /* Warning states */
--wa-color-danger-{05-95}  /* Error states */
```

### Example Usage

```css
.success-message {
  background: var(--wa-color-success-90);
  color: var(--wa-color-success-20);
  border: 1px solid var(--wa-color-success-40);
}
```

## Foundational Colors

Foundational colors provide structural consistency across your application.

### Surface Colors

Background hierarchy for depth perception:

```css
--wa-color-surface-raised   /* Closest to user (dialogs, dropdowns) */
--wa-color-surface-default  /* Standard surface */
--wa-color-surface-lowered  /* Farthest from user (wells, recessed areas) */
--wa-color-surface-border   /* Surface borders and dividers */
```

**Usage:**

```html
<div style="background: var(--wa-color-surface-default);">
  <div style="background: var(--wa-color-surface-raised);">
    Dialog content appears above the page
  </div>
</div>
```

### Text Colors

```css
--wa-color-text-normal  /* Primary text (4.5:1 contrast min) */
--wa-color-text-quiet   /* Secondary/muted text */
--wa-color-text-link    /* Link text */
```

**Usage:**

```css
p {
  color: var(--wa-color-text-normal);
}

.caption {
  color: var(--wa-color-text-quiet);
}

a {
  color: var(--wa-color-text-link);
}
```

### Overlay Colors

```css
--wa-color-overlay-modal  /* Modal backdrop */
--wa-color-overlay-inline /* Inline overlay */
```

### Shadow Color

```css
--wa-color-shadow  /* Single color for all shadows */
```

### Interaction Colors

```css
--wa-color-focus        /* Focus indicators (3:1 contrast min) */
--wa-color-mix-hover    /* Hover state mixing */
--wa-color-mix-active   /* Active state mixing */
```

## Semantic Colors

The most powerful feature of WebAwesome's color system - semantic colors that convey meaning.

### Format

```css
--wa-color-{group}-{role}-{attention}
```

### Groups

| Group | Purpose | Example Use |
|-------|---------|-------------|
| `brand` | Emphasize brand color | Primary actions, branding |
| `success` | Validity/confirmation | Success messages, checkmarks |
| `neutral` | Ordinary/inactive content | Default states, disabled |
| `warning` | Caution/uncertainty | Warnings, pending states |
| `danger` | Errors/risk | Errors, destructive actions |

### Roles

| Role | Purpose | Example |
|------|---------|---------|
| `fill` | Background colors | Button backgrounds, card fills |
| `border` | Borders, dividers, strokes | Input borders, dividers |
| `on` | Content displayed on fills | Text on colored backgrounds |

### Attention Levels

| Attention | Visual Weight | Use Case |
|-----------|---------------|----------|
| `quiet` | Least attention | Subtle hints, background |
| `normal` | Some attention | Standard emphasis |
| `loud` | Most attention | High emphasis, primary actions |

### Complete Semantic Color Matrix

```css
/* Fill Colors */
--wa-color-brand-fill-quiet
--wa-color-brand-fill-normal
--wa-color-brand-fill-loud
--wa-color-success-fill-quiet
--wa-color-success-fill-normal
--wa-color-success-fill-loud
--wa-color-neutral-fill-quiet
--wa-color-neutral-fill-normal
--wa-color-neutral-fill-loud
--wa-color-warning-fill-quiet
--wa-color-warning-fill-normal
--wa-color-warning-fill-loud
--wa-color-danger-fill-quiet
--wa-color-danger-fill-normal
--wa-color-danger-fill-loud

/* Border Colors */
--wa-color-brand-border-quiet
--wa-color-brand-border-normal
--wa-color-brand-border-loud
/* ... (same pattern for success, neutral, warning, danger) */

/* On Colors (for text/content on fills) */
--wa-color-brand-on-quiet
--wa-color-brand-on-normal
--wa-color-brand-on-loud
/* ... (same pattern for success, neutral, warning, danger) */
```

## Examples

### Button Variants

```html
<!-- Primary button -->
<wa-button style="
  background: var(--wa-color-brand-fill-loud);
  color: var(--wa-color-brand-on-loud);
  border-color: var(--wa-color-brand-border-loud);
">
  Primary Action
</wa-button>

<!-- Success button -->
<wa-button style="
  background: var(--wa-color-success-fill-normal);
  color: var(--wa-color-success-on-normal);
">
  Success
</wa-button>

<!-- Danger button -->
<wa-button style="
  background: var(--wa-color-danger-fill-loud);
  color: var(--wa-color-danger-on-loud);
">
  Delete
</wa-button>
```

### Alert Messages

```css
.alert-success {
  background: var(--wa-color-success-fill-quiet);
  color: var(--wa-color-success-on-quiet);
  border: 1px solid var(--wa-color-success-border-normal);
}

.alert-warning {
  background: var(--wa-color-warning-fill-quiet);
  color: var(--wa-color-warning-on-quiet);
  border: 1px solid var(--wa-color-warning-border-normal);
}

.alert-danger {
  background: var(--wa-color-danger-fill-quiet);
  color: var(--wa-color-danger-on-quiet);
  border: 1px solid var(--wa-color-danger-border-normal);
}
```

### Surface Hierarchy

```html
<div style="background: var(--wa-color-surface-lowered); padding: 2rem;">
  <div style="background: var(--wa-color-surface-default); padding: 2rem;">
    <div style="background: var(--wa-color-surface-raised); padding: 2rem;">
      This appears to float above the page
    </div>
  </div>
</div>
```

## Color Pairing Rules

### Always Pair Fill + On Colors

```css
/* ✅ Correct - matching group and attention */
.button-primary {
  background: var(--wa-color-brand-fill-loud);
  color: var(--wa-color-brand-on-loud);
}

/* ❌ Wrong - mismatched attention levels */
.button-wrong {
  background: var(--wa-color-brand-fill-loud);
  color: var(--wa-color-brand-on-quiet); /* Don't mix attention levels */
}
```

### Use Matching Attention Levels

Quiet with quiet, normal with normal, loud with loud.

### Maintain Semantic Consistency

Don't mix semantic groups inappropriately (e.g., danger fill with success on color).

## Hierarchy Usage

### Surface Elevation

```
raised > default > lowered
```

### Attention Levels

```
loud > normal > quiet
```

### Semantic Priority

```
danger > warning > success > brand > neutral
```

## Accessibility Requirements

- ✅ **Minimum 3:1 contrast** for focus indicators
- ✅ **Minimum 4.5:1 contrast** for normal text
- ✅ **Use tint differences of 40+** for accessible contrast
- ✅ **Test all color combinations** for WCAG compliance

## Best Practices

1. ✅ **Use semantic colors** over direct color scale references
2. ✅ **Pair colors within the same semantic group**
3. ✅ **Use `color-mix()` properties** for consistent hover/active states
4. ✅ **Avoid hardcoded color values** in components
5. ❌ **Don't mix attention levels** in the same component
6. ❌ **Don't use color as the only indicator** - combine with icons/text

## Customization

### Changing Brand Color

```css
:root {
  /* Map brand to a different hue */
  --wa-color-brand-05: var(--wa-color-purple-05);
  --wa-color-brand-10: var(--wa-color-purple-10);
  --wa-color-brand-20: var(--wa-color-purple-20);
  /* ... continue for all tints */
}
```

### Creating Custom Semantic Groups

```css
:root {
  /* Define custom info color group */
  --wa-color-info-fill-quiet: var(--wa-color-cyan-90);
  --wa-color-info-fill-normal: var(--wa-color-cyan-70);
  --wa-color-info-fill-loud: var(--wa-color-cyan-50);
  --wa-color-info-on-quiet: var(--wa-color-cyan-20);
  --wa-color-info-on-normal: var(--wa-color-cyan-10);
  --wa-color-info-on-loud: white;
}
```

## Troubleshooting

### Colors Look Washed Out

**Solution:** Increase contrast by using tints with larger differences (50+ tint difference).

### Text is Hard to Read

**Solution:** Ensure you're using proper fill + on color pairs and check WCAG contrast ratios.

### Dark Mode Issues

**Solution:** Invert tint values (use 10 instead of 90, 90 instead of 10) for dark themes.

## Related

- [Typography](./typography.md)
- [Customization Guide](../guides/customizing.md)
- [Accessibility](../guides/accessibility.md)
