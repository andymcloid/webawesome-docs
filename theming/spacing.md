# Spacing

WebAwesome's comprehensive spacing system for consistent rhythm, meaningful proximity, and accessible layouts.

## Overview

WebAwesome's spacing system creates predictable rhythm and meaningful proximity using rem units that scale proportionally with root font size. The system uses a scale-based approach for consistent spacing across all components.

The spacing system provides:

1. **Spacing Scale** - Predefined spacing values from minimal to maximum
2. **Global Scaling** - Easy system-wide spacing adjustments
3. **Usage Patterns** - Consistent spacing approaches for common scenarios
4. **Contextual Guidelines** - Appropriate spacing for different use cases

## Spacing Scale

### Format

```css
--wa-space-{size}
```

### Properties and Values

| Property | Calculation | Default Value (16px root) | Use Case |
|----------|-------------|---------------------------|----------|
| `--wa-space-3xs` | `calc(var(--wa-space-scale) * 0.125rem)` | 2px | Minimal spacing, borders |
| `--wa-space-2xs` | `calc(var(--wa-space-scale) * 0.25rem)` | 4px | Very tight spacing |
| `--wa-space-xs` | `calc(var(--wa-space-scale) * 0.5rem)` | 8px | Small padding, margins |
| `--wa-space-s` | `calc(var(--wa-space-scale) * 0.75rem)` | 12px | Compact spacing |
| `--wa-space-m` | `calc(var(--wa-space-scale) * 1rem)` | 16px | Standard spacing |
| `--wa-space-l` | `calc(var(--wa-space-scale) * 1.5rem)` | 24px | Comfortable spacing |
| `--wa-space-xl` | `calc(var(--wa-space-scale) * 2rem)` | 32px | Large spacing |
| `--wa-space-2xl` | `calc(var(--wa-space-scale) * 2.5rem)` | 40px | Very large spacing |
| `--wa-space-3xl` | `calc(var(--wa-space-scale) * 3rem)` | 48px | Extra large spacing |
| `--wa-space-4xl` | `calc(var(--wa-space-scale) * 4rem)` | 64px | Maximum spacing |

### Global Space Scaling

Adjust all spacing values proportionally with a single variable:

```css
/* Default scaling */
--wa-space-scale: 1;

/* Increase all spacing by 25% */
:root {
  --wa-space-scale: 1.25;
}

/* Decrease all spacing by 20% */
:root {
  --wa-space-scale: 0.8;
}
```

**Benefits of Scale-based System:**
- Proportional scaling with root font size
- Consistent rhythm across all components
- Easy global spacing adjustments
- Accessibility-friendly (respects user font size preferences)

## Usage Patterns

### Component Spacing

Apply internal spacing within components for consistent padding and structure:

```css
/* Internal component spacing */
.card {
  padding: var(--wa-space-m);
}

.button {
  padding: var(--wa-space-xs) var(--wa-space-s);
}

.form-field {
  margin-bottom: var(--wa-space-l);
}
```

### Layout Spacing

Create consistent spacing between layout elements and structural components:

```css
/* Grid and layout spacing */
.grid {
  gap: var(--wa-space-m);
}

.sidebar {
  margin-right: var(--wa-space-xl);
}

.section {
  margin-bottom: var(--wa-space-3xl);
}
```

### Typography Spacing

Maintain vertical rhythm with consistent text element spacing:

```css
/* Text element spacing */
h1 {
  margin-bottom: var(--wa-space-l);
}

p {
  margin-bottom: var(--wa-space-m);
}

.caption {
  margin-top: var(--wa-space-xs);
}
```

## Guidelines by Context

### Micro Spacing (3xs - xs)

**Use for:**
- Border spacing and offsets
- Icon padding
- Tight list item spacing
- Form control internal padding

```css
/* Examples */
.icon-button {
  padding: var(--wa-space-3xs);
}

.list-item {
  padding: var(--wa-space-2xs) var(--wa-space-xs);
}

.input-field {
  border-width: var(--wa-space-3xs);
}
```

### Small Spacing (s - m)

**Use for:**
- Standard component padding
- Form field spacing
- Button padding
- Card content spacing

```css
/* Examples */
.form-group {
  margin-bottom: var(--wa-space-s);
}

.card-content {
  padding: var(--wa-space-m);
}

.button-primary {
  padding: var(--wa-space-s) var(--wa-space-m);
}
```

### Medium Spacing (l - xl)

**Use for:**
- Section spacing
- Component margins
- Layout gaps
- Comfortable reading spacing

```css
/* Examples */
.component-margin {
  margin: var(--wa-space-l) 0;
}

.grid-gap {
  gap: var(--wa-space-l);
}

.comfortable-padding {
  padding: var(--wa-space-xl);
}
```

### Large Spacing (2xl - 4xl)

**Use for:**
- Page sections
- Major layout divisions
- Hero sections
- Maximum visual separation

```css
/* Examples */
.page-section {
  padding: var(--wa-space-3xl) 0;
}

.hero-spacing {
  margin-bottom: var(--wa-space-4xl);
}

.major-separator {
  margin: var(--wa-space-2xl) 0;
}
```

## Advanced Techniques

### Responsive Spacing

Scale spacing automatically for different viewport sizes:

```css
/* Scale spacing for different viewports */
@media (max-width: 768px) {
  :root {
    --wa-space-scale: 0.875; /* 12.5% smaller on mobile */
  }
}

@media (min-width: 1200px) {
  :root {
    --wa-space-scale: 1.125; /* 12.5% larger on desktop */
  }
}
```

### Component-Specific Scaling

Override the spacing scale for specific contexts or components:

```css
/* Override spacing scale for specific contexts */
.compact-mode {
  --wa-space-scale: 0.75;
}

.spacious-mode {
  --wa-space-scale: 1.5;
}

/* Dense data tables */
.data-table {
  --wa-space-scale: 0.6;
}
```

### Directional Spacing

Apply spacing to specific directions for precise control:

```css
/* Apply spacing to specific directions */
.push-right {
  margin-right: var(--wa-space-l);
}

.vertical-rhythm h2 {
  margin-top: var(--wa-space-xl);
  margin-bottom: var(--wa-space-m);
}

.horizontal-spacing {
  padding-left: var(--wa-space-m);
  padding-right: var(--wa-space-m);
}
```

### Negative Spacing

Use negative spacing for overlapping effects and tight grouping:

```css
/* Pull elements closer together */
.tight-group > * + * {
  margin-top: calc(var(--wa-space-s) * -0.5);
}

.overlap-effect {
  margin-top: calc(var(--wa-space-l) * -1);
}
```

## Examples

### Form Spacing Pattern

```css
/* Form field spacing */
.form-field {
  margin-bottom: var(--wa-space-s);
}

.form-section {
  margin-bottom: var(--wa-space-xl);
}

.form-submit {
  margin-top: var(--wa-space-l);
}
```

### Card Spacing Pattern

```css
/* Card component spacing */
.card {
  padding: var(--wa-space-l);
  margin-bottom: var(--wa-space-m);
}

.card-header {
  margin-bottom: var(--wa-space-m);
}

.card-footer {
  margin-top: var(--wa-space-m);
}
```

### Typography Spacing Pattern

```css
/* Consistent typography spacing */
h1 {
  margin-bottom: var(--wa-space-l);
}

h2 {
  margin-bottom: var(--wa-space-m);
}

p {
  margin-bottom: var(--wa-space-s);
}

ul, ol {
  margin-bottom: var(--wa-space-m);
}

li + li {
  margin-top: var(--wa-space-xs);
}
```

### Page Layout Pattern

```html
<div style="padding: var(--wa-space-3xl) var(--wa-space-m);">
  <header style="margin-bottom: var(--wa-space-2xl);">
    <h1>Page Title</h1>
  </header>

  <main style="margin-bottom: var(--wa-space-3xl);">
    <section style="margin-bottom: var(--wa-space-xl);">
      <h2 style="margin-bottom: var(--wa-space-m);">Section Title</h2>
      <p style="margin-bottom: var(--wa-space-s);">Content paragraph</p>
    </section>
  </main>

  <footer style="padding-top: var(--wa-space-xl);">
    Footer content
  </footer>
</div>
```

## Best Practices

### Spacing Selection Strategy

1. **Start with standard spacing** (`--wa-space-m`) and adjust as needed
2. **Use relative spacing** - choose sizes relative to each other on the scale
3. **Maintain consistent rhythm** - prefer staying within the defined scale
4. **Consider content hierarchy** - larger spacing for more important separations

### Use CSS Custom Properties

Always use spacing variables instead of hardcoded values:

```css
/* ✅ Correct */
.component {
  padding: var(--wa-space-m);
}

/* ❌ Wrong */
.component {
  padding: 16px;
}
```

### Leverage the Cascade

Set spacing at higher levels when possible for efficiency:

```css
/* Set once for all children */
.form-container > * {
  margin-bottom: var(--wa-space-m);
}
```

### Use Gap for Flexbox/Grid

Prefer `gap` property over margins for flexbox and grid layouts:

```css
/* ✅ Preferred for flex/grid */
.grid {
  display: grid;
  gap: var(--wa-space-m);
}

/* ❌ Less efficient */
.grid > * {
  margin: var(--wa-space-m);
}
```

### Consider Margin Collapsing

Be aware of vertical margin collapsing behavior:

```css
/* Margins may collapse vertically */
.section {
  margin-bottom: var(--wa-space-xl);
}

.section + .section {
  margin-top: var(--wa-space-xl); /* May collapse with previous margin */
}
```

### Maintain Consistent Patterns

Use the same spacing patterns across similar components:

```css
/* Consistent button spacing */
.button-small {
  padding: var(--wa-space-2xs) var(--wa-space-xs);
}

.button-medium {
  padding: var(--wa-space-xs) var(--wa-space-s);
}

.button-large {
  padding: var(--wa-space-s) var(--wa-space-m);
}
```

## Accessibility

### Respects User Font Size

Spacing automatically scales with the root font size, respecting user preferences:

```css
/* Scales proportionally when users increase font size */
:root {
  font-size: 18px; /* User preference */
  /* All spacing values scale automatically */
}
```

### Adequate Touch Targets

Ensure interactive elements have sufficient spacing for touch interaction:

```css
/* Minimum touch target size */
.interactive-element {
  padding: var(--wa-space-l); /* At least 24px for comfortable tapping */
  min-height: 44px; /* Recommended minimum for touch targets */
}
```

### Maintains Reading Flow

Consistent vertical rhythm improves readability and cognitive flow:

```css
/* Consistent vertical spacing */
.content h2 {
  margin-top: var(--wa-space-xl);
  margin-bottom: var(--wa-space-m);
}

.content p {
  margin-bottom: var(--wa-space-s);
  line-height: 1.6;
}
```

### Reduces Cognitive Load

Appropriate spacing reduces visual clutter and improves comprehension:

```css
/* Clear visual grouping */
.form-section {
  margin-bottom: var(--wa-space-2xl); /* Separates major sections */
}

.form-field {
  margin-bottom: var(--wa-space-s); /* Groups related fields */
}
```

## Debugging and Maintenance

### Visualize Spacing During Development

Add visual indicators to understand spacing in your layouts:

```css
/* Visualize spacing during development */
.debug-spacing * {
  outline: 1px solid rgba(255, 0, 0, 0.2);
  background: rgba(255, 0, 0, 0.05);
}

/* Show spacing scale values */
.debug-spacing::after {
  content: 'Scale: ' var(--wa-space-scale);
  position: fixed;
  top: 0;
  right: 0;
  background: yellow;
  padding: var(--wa-space-xs);
}
```

### Test with Different Font Sizes

Verify spacing works across different user font size preferences:

```css
/* Test larger font sizes */
:root {
  font-size: 20px; /* Test at 125% */
}

/* Test smaller font sizes */
:root {
  font-size: 14px; /* Test at 87.5% */
}
```

## Related

- [Colors](./colors.md)
- [Typography](./typography.md)
- [Customization Guide](../guides/customizing.md)
- [Accessibility](../guides/accessibility.md)
