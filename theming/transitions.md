# Transitions

WebAwesome's comprehensive transition system for smooth, purposeful animations and state changes.

## Overview

WebAwesome's transition system creates lively interactions that emphasize the relationship between user actions and their outcomes. The system uses carefully crafted durations and easing curves to provide responsive feedback while avoiding sluggish or distracting movement.

The system consists of:

1. **Duration scales** - Three timing options (fast, normal, slow)
2. **Easing system** - Standard and custom timing functions
3. **State-based transitions** - Different timings for different interactions
4. **Reduced motion support** - Accessibility-first animation approach

All transition values are designed to feel natural and responsive across all device capabilities.

## Transition Durations

### Duration Properties

Three duration options for different interaction types:

```css
--wa-transition-fast: 75ms      /* Quick micro-interactions */
--wa-transition-normal: 150ms   /* Standard interactions */
--wa-transition-slow: 300ms     /* Deliberate state changes */
```

### Duration Selection Guide

| Duration | Timing | Use Case | Example Interactions |
|----------|--------|----------|---------------------|
| **Fast** (`75ms`) | Quick | Micro-interactions | Hover states, focus rings, button press |
| **Normal** (`150ms`) | Standard | Common state changes | Form controls, icon animations, cards |
| **Slow** (`300ms`) | Deliberate | Significant changes | Modals, panels, checked states, expansions |

## Fast Transitions (75ms)

### Use For

- Hover state changes
- Focus ring appearances
- Button press feedback
- Micro-interactions
- Cursor-following effects

### Examples

```css
/* Button hover state */
.button:hover {
  background-color: var(--wa-color-brand-fill-loud);
  transition: background-color var(--wa-transition-fast) var(--wa-transition-easing);
}

/* Focus ring appearance */
.link:focus {
  outline: var(--wa-focus-ring);
  transition: outline var(--wa-transition-fast) var(--wa-transition-easing);
}

/* Icon color change */
.icon:hover {
  color: var(--wa-color-brand-fill-loud);
  transition: color var(--wa-transition-fast) var(--wa-transition-easing);
}
```

## Normal Transitions (150ms)

### Use For

- Property changes between common states
- Form control interactions
- Icon animations
- Standard component state changes
- Card elevation changes

### Examples

```css
/* Card hover elevation */
.card:hover {
  box-shadow: var(--wa-shadow-m);
  transform: translateY(-2px);
  transition: all var(--wa-transition-normal) var(--wa-transition-easing);
}

/* Input focus state */
.input-field:focus {
  border-color: var(--wa-color-brand-border-loud);
  transition: border-color var(--wa-transition-normal) var(--wa-transition-easing);
}

/* Tab switching */
.tab.active {
  color: var(--wa-color-brand-fill-loud);
  border-bottom-color: var(--wa-color-brand-border-loud);
  transition:
    color var(--wa-transition-normal) var(--wa-transition-easing),
    border-color var(--wa-transition-normal) var(--wa-transition-easing);
}
```

## Slow Transitions (300ms)

### Use For

- Intentional state changes (checked, open, expanded)
- Modal/dialog appearances
- Panel sliding animations
- Complex component transformations
- Page transitions

### Examples

```css
/* Accordion expansion */
.accordion-panel[open] {
  max-height: 500px;
  transition: max-height var(--wa-transition-slow) var(--wa-transition-easing);
}

/* Modal appearance */
.modal.open {
  opacity: 1;
  transform: scale(1);
  transition: all var(--wa-transition-slow) var(--wa-transition-easing);
}

/* Checkbox check animation */
.checkbox:checked::part(control) {
  background: var(--wa-color-brand-fill-loud);
  transition: background var(--wa-transition-slow) var(--wa-transition-easing);
}

/* Drawer slide-in */
.drawer.open {
  transform: translateX(0);
  transition: transform var(--wa-transition-slow) var(--wa-transition-easing);
}
```

## Transition Easing

### Standard Easing Property

```css
--wa-transition-easing: ease    /* Standard easing curve */
```

### Easing Curve Characteristics

The `ease` timing function provides:

- **Fast start** - Immediate visual feedback
- **Gradual deceleration** - Natural feeling movement
- **Smooth completion** - Polished final state

### Custom Easing Options

```css
/* Override easing for specific effects */
:root {
  --wa-transition-easing: ease-in-out;  /* Symmetrical acceleration/deceleration */
}

/* Component-specific easing */
.bounce-effect {
  --wa-transition-easing: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.linear-progress {
  --wa-transition-easing: linear;       /* Constant speed */
}

.snappy-interaction {
  --wa-transition-easing: ease-out;     /* Quick start, slow end */
}

.smooth-start {
  --wa-transition-easing: ease-in;      /* Slow start, quick end */
}
```

### Common Easing Functions

| Easing | Curve | Best For |
|--------|-------|----------|
| `ease` | Fast start, slow end | General purpose (default) |
| `ease-in-out` | Symmetrical | Smooth, natural movements |
| `ease-out` | Quick start, gradual end | Entering elements |
| `ease-in` | Gradual start, quick end | Exiting elements |
| `linear` | Constant speed | Progress indicators, loading |

## Comprehensive Transition Patterns

### Complete Transition Declaration

```css
/* Recommended transition pattern */
.interactive-element {
  transition:
    background-color var(--wa-transition-normal) var(--wa-transition-easing),
    border-color var(--wa-transition-normal) var(--wa-transition-easing),
    box-shadow var(--wa-transition-normal) var(--wa-transition-easing),
    transform var(--wa-transition-normal) var(--wa-transition-easing);
}
```

### Multi-Property Transitions

Different durations for different properties:

```css
/* Fast color change, normal transform, slow height */
.complex-component {
  transition:
    opacity var(--wa-transition-fast) var(--wa-transition-easing),
    transform var(--wa-transition-normal) var(--wa-transition-easing),
    height var(--wa-transition-slow) var(--wa-transition-easing);
}
```

### State-Specific Transitions

Different transitions for enter vs. exit states:

```css
/* Slow fade-in */
.fade-in {
  opacity: 0;
  transition: opacity var(--wa-transition-slow) var(--wa-transition-easing);
}

/* Fast fade-out */
.fade-in.hidden {
  opacity: 0;
  transition: opacity var(--wa-transition-fast) var(--wa-transition-easing);
}
```

## Component Integration Examples

### Button Transitions

```css
wa-button {
  transition:
    background-color var(--wa-transition-fast) var(--wa-transition-easing),
    border-color var(--wa-transition-fast) var(--wa-transition-easing),
    box-shadow var(--wa-transition-fast) var(--wa-transition-easing);
}

wa-button:hover {
  /* Fast response to hover */
  background-color: var(--wa-color-brand-fill-loud);
}

wa-button:active {
  /* Even faster response to press */
  transition-duration: var(--wa-transition-fast);
  transform: scale(0.98);
}
```

### Form Control Transitions

```css
/* Input field transitions */
wa-input {
  transition:
    border-color var(--wa-transition-normal) var(--wa-transition-easing),
    box-shadow var(--wa-transition-normal) var(--wa-transition-easing);
}

/* Checkbox transitions */
wa-checkbox:checked {
  transition:
    background-color var(--wa-transition-slow) var(--wa-transition-easing);
}

/* Select dropdown */
wa-select[open] {
  transition:
    max-height var(--wa-transition-slow) var(--wa-transition-easing);
}
```

### Card/Panel Transitions

```css
/* Card hover effect */
wa-card {
  transition:
    box-shadow var(--wa-transition-normal) var(--wa-transition-easing),
    transform var(--wa-transition-normal) var(--wa-transition-easing);
}

wa-card:hover {
  box-shadow: var(--wa-shadow-m);
  transform: translateY(-2px);
}

/* Accordion expansion */
wa-details[open] summary::part(icon) {
  transform: rotate(90deg);
  transition: transform var(--wa-transition-slow) var(--wa-transition-easing);
}
```

## Accessibility: Reduced Motion

### Respecting User Preferences

```css
/* Honor reduced motion preferences */
@media (prefers-reduced-motion: reduce) {
  :root {
    --wa-transition-fast: 0ms;
    --wa-transition-normal: 0ms;
    --wa-transition-slow: 0ms;
  }
}
```

### Alternative: Reduce but Don't Eliminate

```css
/* Reduce transitions but maintain some feedback */
@media (prefers-reduced-motion: reduce) {
  :root {
    --wa-transition-fast: 0ms;
    --wa-transition-normal: 50ms;
    --wa-transition-slow: 100ms;
  }
}
```

### Component-Level Reduced Motion

```css
/* Disable specific animations */
@media (prefers-reduced-motion: reduce) {
  .animated-card {
    transform: none !important;
    transition: opacity var(--wa-transition-fast) ease;
  }
}
```

### Focus-Visible Transitions

```css
/* Immediate focus indication, smooth removal */
.focusable:focus-visible {
  outline: var(--wa-focus-ring);
  transition: none;  /* Immediate focus appearance */
}

.focusable:not(:focus-visible) {
  transition: outline var(--wa-transition-fast) var(--wa-transition-easing);
}
```

## Performance Optimization

### GPU-Accelerated Properties

Prefer `transform` and `opacity` for smooth animations:

```css
/* ✅ Good - GPU accelerated */
.smooth-animation {
  transform: translateY(0);
  opacity: 1;
  transition:
    transform var(--wa-transition-normal) var(--wa-transition-easing),
    opacity var(--wa-transition-normal) var(--wa-transition-easing);
}

/* ❌ Avoid - causes layout recalculation */
.laggy-animation {
  height: 100px;
  top: 0;
  transition:
    height var(--wa-transition-normal) var(--wa-transition-easing),
    top var(--wa-transition-normal) var(--wa-transition-easing);
}
```

### Will-Change Optimization

```css
/* Optimize for upcoming transitions */
.will-animate {
  will-change: transform, opacity;
  transition: transform var(--wa-transition-normal) ease;
}

.will-animate:hover {
  transform: scale(1.05);
}

.will-animate.completed {
  will-change: auto;  /* Remove after animation */
}
```

### Performance Best Practices

1. **Limit properties** - Only transition properties that change
2. **Use GPU-accelerated properties** - `transform`, `opacity`, `filter`
3. **Avoid expensive properties** - `height`, `width`, `top`, `left`, `margin`
4. **Use `will-change` sparingly** - Only for animations you know will happen
5. **Remove `will-change` after** - Clean up after animations complete

## Examples and Common Patterns

### Interactive Element Pattern

```css
.interactive {
  transition: all var(--wa-transition-normal) var(--wa-transition-easing);
}

.interactive:hover {
  transform: translateY(-2px);
  box-shadow: var(--wa-shadow-m);
}

.interactive:active {
  transform: translateY(0);
  box-shadow: var(--wa-shadow-s);
}
```

### Hover Lift Pattern

```css
.hover-lift {
  transform: translateY(0);
  box-shadow: var(--wa-shadow-s);
  transition:
    transform var(--wa-transition-normal) var(--wa-transition-easing),
    box-shadow var(--wa-transition-normal) var(--wa-transition-easing);
}

.hover-lift:hover {
  transform: translateY(-2px);
  box-shadow: var(--wa-shadow-m);
}
```

### State Toggle Pattern

```css
.toggle {
  background: var(--wa-color-neutral-fill-quiet);
  transition: all var(--wa-transition-slow) var(--wa-transition-easing);
}

.toggle.active {
  background: var(--wa-color-brand-fill-loud);
}
```

### Micro-Interaction Pattern

```css
.button {
  transform: scale(1);
  transition: transform var(--wa-transition-fast) var(--wa-transition-easing);
}

.button:active {
  transform: scale(0.98);
}
```

## Best Practices

1. **Use system properties** - Leverage WebAwesome's predefined durations
2. **Match interaction intent** - Quick feedback for minor changes, slower for important changes
3. **Always respect `prefers-reduced-motion`** - Essential for accessibility
4. **Optimize performance** - Prefer `transform` and `opacity` for animations
5. **Test on various devices** - Ensure smooth performance across capabilities
6. **Be consistent** - Use the same transition for the same type of interaction
7. **Don't overuse slow transitions** - They can make interfaces feel sluggish

### Do's and Don'ts

```css
/* ✅ Good - appropriate duration for interaction */
.button:hover {
  background: var(--wa-color-brand-fill-loud);
  transition: background var(--wa-transition-fast) ease;
}

/* ❌ Avoid - too slow for hover */
.button:hover {
  background: var(--wa-color-brand-fill-loud);
  transition: background 1s ease;
}

/* ✅ Good - GPU-accelerated properties */
.card:hover {
  transform: translateY(-2px);
  transition: transform var(--wa-transition-normal) ease;
}

/* ❌ Avoid - causes layout thrashing */
.card:hover {
  margin-top: -2px;
  transition: margin-top var(--wa-transition-normal) ease;
}
```

## Debugging Transitions

### Slow Down All Transitions

```css
/* Debug mode - slow down transitions */
.debug-transitions * {
  transition-duration: 2s !important;
}
```

### Visualize Transition Timing

```css
/* Show current transition values */
.debug-transitions::after {
  content: 'Fast: ' var(--wa-transition-fast) ' Normal: ' var(--wa-transition-normal) ' Slow: ' var(--wa-transition-slow);
  position: fixed;
  top: 0;
  left: 0;
  background: yellow;
  padding: 0.5rem;
  z-index: 9999;
}
```

## Troubleshooting

### Transitions Feel Too Slow

**Solution:** Reduce duration or use faster transition speed:

```css
:root {
  --wa-transition-normal: 100ms;
  --wa-transition-slow: 200ms;
}
```

### Transitions Feel Too Fast

**Solution:** Increase duration or use slower transition speed:

```css
:root {
  --wa-transition-normal: 200ms;
  --wa-transition-slow: 400ms;
}
```

### Janky/Choppy Animations

**Solution:** Use GPU-accelerated properties and `will-change`:

```css
.smooth-element {
  will-change: transform;
  transform: translateZ(0);  /* Force GPU acceleration */
  transition: transform var(--wa-transition-normal) ease;
}
```

### Transitions Not Working

**Solution:** Check that you're transitioning animatable properties and have both initial and final states defined.

## Related

- [Shadows](./shadows.md)
- [Focus](./focus.md)
- [Colors](./colors.md)
- [Accessibility Guide](../guides/accessibility.md)
