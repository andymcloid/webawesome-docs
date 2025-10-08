# Animation

Apply animations to elements using a simple declarative API.

## Overview

The `<wa-animation>` component provides a powerful way to apply CSS animations and keyframe animations to elements. It wraps the Web Animations API with a simple, declarative interface that makes it easy to create, control, and synchronize animations.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/animation/animation.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple fade in animation -->
<wa-animation name="fadeIn" duration="1000" play>
  <div class="box">I will fade in!</div>
</wa-animation>

<!-- Bounce animation -->
<wa-animation name="bounce" duration="500" iterations="3">
  <wa-button>Click me!</wa-button>
</wa-animation>
```

## Animation Names

Use predefined animation names:

```html
<!-- Fade animations -->
<wa-animation name="fadeIn" play>
  <div>Fade In</div>
</wa-animation>

<wa-animation name="fadeOut" play>
  <div>Fade Out</div>
</wa-animation>

<!-- Slide animations -->
<wa-animation name="slideInLeft" play>
  <div>Slide In From Left</div>
</wa-animation>

<wa-animation name="slideInRight" play>
  <div>Slide In From Right</div>
</wa-animation>

<!-- Scale animations -->
<wa-animation name="scaleUp" play>
  <div>Scale Up</div>
</wa-animation>

<wa-animation name="scaleDown" play>
  <div>Scale Down</div>
</wa-animation>

<!-- Rotation animations -->
<wa-animation name="rotateIn" play>
  <div>Rotate In</div>
</wa-animation>

<!-- Bounce animations -->
<wa-animation name="bounce" play>
  <div>Bounce</div>
</wa-animation>
```

## Timing and Duration

Control animation timing with various attributes:

```html
<!-- Duration in milliseconds -->
<wa-animation name="fadeIn" duration="2000" play>
  <div>Slow fade (2 seconds)</div>
</wa-animation>

<!-- Delay before starting -->
<wa-animation name="slideIn" delay="1000" play>
  <div>Delayed animation (1 second delay)</div>
</wa-animation>

<!-- Multiple iterations -->
<wa-animation name="pulse" iterations="3" play>
  <div>Pulse 3 times</div>
</wa-animation>

<!-- Infinite iterations -->
<wa-animation name="rotate" iterations="infinite" play>
  <div>Rotate forever</div>
</wa-animation>
```

## Direction

Control animation direction:

```html
<!-- Normal direction (default) -->
<wa-animation name="slideIn" direction="normal" play>
  <div>Slide In</div>
</wa-animation>

<!-- Reverse direction -->
<wa-animation name="slideIn" direction="reverse" play>
  <div>Slide In Reversed</div>
</wa-animation>

<!-- Alternate direction -->
<wa-animation name="bounce" direction="alternate" iterations="4" play>
  <div>Bounce back and forth</div>
</wa-animation>

<!-- Alternate reverse -->
<wa-animation name="bounce" direction="alternate-reverse" iterations="4" play>
  <div>Bounce back and forth (starting reversed)</div>
</wa-animation>
```

## Fill Mode

Control how animation styles apply before and after execution:

```html
<!-- No fill (default) - returns to original state -->
<wa-animation name="fadeOut" fill="none">
  <div>Fades out and returns</div>
</wa-animation>

<!-- Forwards - maintains final state -->
<wa-animation name="fadeOut" fill="forwards" play>
  <div>Stays faded out</div>
</wa-animation>

<!-- Backwards - applies initial state during delay -->
<wa-animation name="fadeIn" fill="backwards" delay="1000" play>
  <div>Applies initial fade state during delay</div>
</wa-animation>

<!-- Both - applies both forwards and backwards -->
<wa-animation name="fadeIn" fill="both" delay="500" play>
  <div>Applies styles before, during, and after</div>
</wa-animation>
```

## Easing Functions

Control animation timing with easing functions:

```html
<!-- Linear easing -->
<wa-animation name="slideIn" easing="linear" play>
  <div>Linear motion</div>
</wa-animation>

<!-- Ease-in -->
<wa-animation name="slideIn" easing="ease-in" play>
  <div>Slow start</div>
</wa-animation>

<!-- Ease-out -->
<wa-animation name="slideIn" easing="ease-out" play>
  <div>Slow end</div>
</wa-animation>

<!-- Ease-in-out -->
<wa-animation name="slideIn" easing="ease-in-out" play>
  <div>Slow start and end</div>
</wa-animation>

<!-- Custom cubic-bezier -->
<wa-animation name="slideIn" easing="cubic-bezier(0.68, -0.55, 0.265, 1.55)" play>
  <div>Custom easing</div>
</wa-animation>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `name` | string | - | Yes | Animation name (e.g., fadeIn, slideInLeft, bounce) |
| `play` | boolean | `false` | No | Whether to play the animation automatically |
| `delay` | number | `0` | No | Delay before animation starts (in milliseconds) |
| `duration` | number | `1000` | No | Duration of the animation (in milliseconds) |
| `iterations` | number \| string | `1` | No | Number of times to repeat (`infinite` for endless) |
| `direction` | string | `'normal'` | No | Animation direction: `normal`, `reverse`, `alternate`, `alternate-reverse` |
| `fill` | string | `'auto'` | No | Fill mode: `none`, `forwards`, `backwards`, `both`, `auto` |
| `easing` | string | `'linear'` | No | Timing function: `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`, or custom cubic-bezier |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `play()` | Starts or resumes the animation | `void` |
| `pause()` | Pauses the animation | `void` |
| `cancel()` | Cancels the animation and resets to initial state | `void` |
| `finish()` | Immediately completes the animation | `void` |

### Method Examples

```javascript
const animation = document.querySelector('wa-animation');

// Start the animation
animation.play();

// Pause the animation
animation.pause();

// Cancel and reset
animation.cancel();

// Jump to the end
animation.finish();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-start` | Emitted when the animation starts | - |
| `wa-finish` | Emitted when the animation completes | - |
| `wa-cancel` | Emitted when the animation is cancelled | - |

### Event Examples

```javascript
const animation = document.querySelector('wa-animation');

// Listen for animation start
animation.addEventListener('wa-start', () => {
  console.log('Animation started');
});

// Listen for animation finish
animation.addEventListener('wa-finish', () => {
  console.log('Animation completed');
});

// Listen for animation cancel
animation.addEventListener('wa-cancel', () => {
  console.log('Animation cancelled');
});
```

## Examples

### Click to Animate

```html
<wa-animation id="clickAnimation" name="bounce" duration="500">
  <wa-button id="animateBtn" variant="primary">Click to Animate</wa-button>
</wa-animation>

<script>
  const animation = document.getElementById('clickAnimation');
  const button = document.getElementById('animateBtn');

  button.addEventListener('click', () => {
    animation.play();
  });
</script>
```

### Sequential Animations

```html
<wa-animation id="anim1" name="fadeIn" duration="500" fill="forwards">
  <div class="box">First</div>
</wa-animation>

<wa-animation id="anim2" name="fadeIn" duration="500" fill="forwards">
  <div class="box">Second</div>
</wa-animation>

<wa-animation id="anim3" name="fadeIn" duration="500" fill="forwards">
  <div class="box">Third</div>
</wa-animation>

<script>
  const anim1 = document.getElementById('anim1');
  const anim2 = document.getElementById('anim2');
  const anim3 = document.getElementById('anim3');

  anim1.play();

  anim1.addEventListener('wa-finish', () => {
    anim2.play();
  });

  anim2.addEventListener('wa-finish', () => {
    anim3.play();
  });
</script>
```

### Hover Animation

```html
<wa-animation id="hoverAnimation" name="scaleUp" duration="200">
  <wa-card id="hoverCard">
    <h3>Hover over me!</h3>
    <p>I'll grow when you hover.</p>
  </wa-card>
</wa-animation>

<script>
  const hoverAnimation = document.getElementById('hoverAnimation');
  const hoverCard = document.getElementById('hoverCard');

  hoverCard.addEventListener('mouseenter', () => {
    hoverAnimation.play();
  });

  hoverCard.addEventListener('mouseleave', () => {
    hoverAnimation.cancel();
  });
</script>
```

### Loading Animation

```html
<wa-animation
  name="pulse"
  iterations="infinite"
  duration="1000"
  play>
  <div class="loading-indicator">
    <wa-icon name="arrow-clockwise"></wa-icon>
    Loading...
  </div>
</wa-animation>

<style>
  .loading-indicator {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 1.2rem;
    color: #6366f1;
  }
</style>
```

### Success Notification

```html
<wa-animation id="successAnimation" name="slideInRight" fill="forwards">
  <wa-alert id="successAlert" variant="success" closable>
    <wa-icon slot="icon" name="check-circle"></wa-icon>
    Your changes have been saved successfully!
  </wa-alert>
</wa-animation>

<wa-button id="saveBtn" variant="primary">Save Changes</wa-button>

<script>
  const successAnimation = document.getElementById('successAnimation');
  const successAlert = document.getElementById('successAlert');
  const saveBtn = document.getElementById('saveBtn');

  saveBtn.addEventListener('click', async () => {
    // Simulate save operation
    await new Promise(resolve => setTimeout(resolve, 1000));

    // Show success animation
    successAlert.open = true;
    successAnimation.play();

    // Auto-hide after 3 seconds
    setTimeout(() => {
      successAlert.open = false;
    }, 3000);
  });
</script>
```

### Attention Seeker

```html
<wa-animation
  id="attentionAnimation"
  name="shake"
  duration="500"
  iterations="2">
  <wa-badge variant="danger">5 new messages</wa-badge>
</wa-animation>

<script>
  const attentionAnimation = document.getElementById('attentionAnimation');

  // Shake every 5 seconds to grab attention
  setInterval(() => {
    attentionAnimation.play();
  }, 5000);
</script>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The element(s) to animate |

## Best Practices

- ✅ Use animations to enhance user experience, not distract
- ✅ Keep animations short (typically 200-500ms for UI feedback)
- ✅ Use `fill="forwards"` when you want to maintain the final state
- ✅ Provide a way to disable animations for accessibility
- ✅ Use appropriate easing functions for natural motion
- ✅ Test animations on lower-powered devices
- ❌ Don't overuse animations - they should serve a purpose
- ❌ Avoid animations that could trigger seizures (rapid flashing)
- ❌ Don't animate during critical user tasks
- ❌ Avoid blocking user interaction with long animations

## Accessibility

- Respect user motion preferences:

```javascript
const animation = document.querySelector('wa-animation');

// Check if user prefers reduced motion
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  animation.duration = 0; // Skip animation
} else {
  animation.play();
}
```

- Avoid animations with rapid flashing or strobing effects
- Don't convey important information through animation alone
- Provide alternative ways to access information
- Use animations to supplement, not replace, static content

## Troubleshooting

### Animation Not Playing

**Problem:** Animation doesn't start

**Solution:** Ensure `play` attribute is set or call `play()` method

```html
<!-- ✅ Correct -->
<wa-animation name="fadeIn" play>
  <div>Content</div>
</wa-animation>

<!-- ❌ Missing play attribute -->
<wa-animation name="fadeIn">
  <div>Content</div>
</wa-animation>
```

### Animation Resets After Completion

**Problem:** Element returns to original state after animation

**Solution:** Use `fill="forwards"` to maintain the final state

```html
<wa-animation name="fadeOut" fill="forwards" play>
  <div>Stays faded out</div>
</wa-animation>
```

### Animation Too Fast/Slow

**Problem:** Animation speed is not right

**Solution:** Adjust the `duration` property

```javascript
const animation = document.querySelector('wa-animation');
animation.duration = 1500; // 1.5 seconds
animation.play();
```

## Related

- [Animated Image](./animated-image.md)
- [Progress Bar](./progress-bar.md)
- [Spinner](./spinner.md)
- [Transitions Guide](../guides/transitions.md)
