# Animated Image

Display animated images (like GIFs) with play and pause controls.

## Overview

The `<wa-animated-image>` component provides a container for animated images with built-in controls to play, pause, and manage animation playback. It's particularly useful for GIFs and other animated image formats where you want to give users control over the animation.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/animated-image/animated-image.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple animated image -->
<wa-animated-image
  src="/images/animated.gif"
  alt="Animated illustration">
</wa-animated-image>

<!-- With autoplay disabled -->
<wa-animated-image
  src="/images/animated.gif"
  alt="Animated illustration"
  play="false">
</wa-animated-image>
```

## Play Control

Control animation playback with the `play` attribute:

```html
<!-- Animation paused by default -->
<wa-animated-image
  src="/images/loading-spinner.gif"
  alt="Loading spinner"
  play="false">
</wa-animated-image>

<!-- Animation playing by default (default behavior) -->
<wa-animated-image
  src="/images/celebration.gif"
  alt="Celebration animation"
  play="true">
</wa-animated-image>
```

## Programmatic Control

Control animation playback programmatically:

```html
<wa-animated-image
  id="myAnimation"
  src="/images/animated.gif"
  alt="Controlled animation">
</wa-animated-image>

<wa-button id="playBtn">Play</wa-button>
<wa-button id="pauseBtn">Pause</wa-button>

<script>
  const animation = document.getElementById('myAnimation');
  const playBtn = document.getElementById('playBtn');
  const pauseBtn = document.getElementById('pauseBtn');

  playBtn.addEventListener('click', () => {
    animation.play();
  });

  pauseBtn.addEventListener('click', () => {
    animation.pause();
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `src` | string | - | Yes | The path to the animated image |
| `alt` | string | - | Yes | Alternative text for the image |
| `play` | boolean | `true` | No | Whether the animation should play automatically |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `play()` | Starts or resumes the animation | `void` |
| `pause()` | Pauses the animation | `void` |

### Method Examples

```javascript
const animatedImage = document.querySelector('wa-animated-image');

// Start playing the animation
animatedImage.play();

// Pause the animation
animatedImage.pause();

// Toggle play/pause
if (animatedImage.play) {
  animatedImage.pause();
} else {
  animatedImage.play();
}
```

## Examples

### Toggle Play/Pause Button

```html
<wa-animated-image
  id="toggleAnimation"
  src="/images/animated.gif"
  alt="Toggleable animation"
  play="false">
</wa-animated-image>

<wa-button id="toggleBtn">Play</wa-button>

<script>
  const animation = document.getElementById('toggleAnimation');
  const toggleBtn = document.getElementById('toggleBtn');
  let isPlaying = false;

  toggleBtn.addEventListener('click', () => {
    if (isPlaying) {
      animation.pause();
      toggleBtn.textContent = 'Play';
    } else {
      animation.play();
      toggleBtn.textContent = 'Pause';
    }
    isPlaying = !isPlaying;
  });
</script>
```

### Hover to Play

```html
<wa-animated-image
  id="hoverAnimation"
  src="/images/animated.gif"
  alt="Hover to play"
  play="false">
</wa-animated-image>

<script>
  const animation = document.getElementById('hoverAnimation');

  animation.addEventListener('mouseenter', () => {
    animation.play();
  });

  animation.addEventListener('mouseleave', () => {
    animation.pause();
  });
</script>
```

### Loading Indicator

```html
<wa-animated-image
  id="loadingIndicator"
  src="/images/loading.gif"
  alt="Loading"
  play="false"
  style="width: 48px; height: 48px;">
</wa-animated-image>

<wa-button id="loadDataBtn" variant="primary">Load Data</wa-button>

<script>
  const loadingIndicator = document.getElementById('loadingIndicator');
  const loadDataBtn = document.getElementById('loadDataBtn');

  loadDataBtn.addEventListener('click', async () => {
    loadingIndicator.play();
    loadDataBtn.disabled = true;

    try {
      await fetch('/api/data');
      // Process data
    } catch (error) {
      console.error('Error loading data:', error);
    } finally {
      loadingIndicator.pause();
      loadDataBtn.disabled = false;
    }
  });
</script>
```

### Image Gallery with Animations

```html
<div class="animation-gallery">
  <wa-animated-image
    src="/images/cat1.gif"
    alt="Cat animation 1"
    play="false"
    class="gallery-item">
  </wa-animated-image>

  <wa-animated-image
    src="/images/cat2.gif"
    alt="Cat animation 2"
    play="false"
    class="gallery-item">
  </wa-animated-image>

  <wa-animated-image
    src="/images/cat3.gif"
    alt="Cat animation 3"
    play="false"
    class="gallery-item">
  </wa-animated-image>
</div>

<style>
  .animation-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1rem;
  }

  .gallery-item {
    cursor: pointer;
    border-radius: 8px;
    overflow: hidden;
  }
</style>

<script>
  const galleryItems = document.querySelectorAll('.gallery-item');

  galleryItems.forEach(item => {
    item.addEventListener('click', () => {
      // Pause all animations
      galleryItems.forEach(anim => anim.pause());
      // Play clicked animation
      item.play();
    });
  });
</script>
```

## CSS Parts

Use CSS parts to style internal elements:

```css
/* Style the image container */
wa-animated-image::part(container) {
  border: 2px solid #ccc;
  border-radius: 8px;
}

/* Style the control bar */
wa-animated-image::part(control-bar) {
  background-color: rgba(0, 0, 0, 0.7);
}
```

## Customization

### Custom Sizing

```html
<!-- Fixed size -->
<wa-animated-image
  src="/images/animated.gif"
  alt="Fixed size animation"
  style="width: 300px; height: 300px;">
</wa-animated-image>

<!-- Responsive size -->
<wa-animated-image
  src="/images/animated.gif"
  alt="Responsive animation"
  style="width: 100%; max-width: 500px;">
</wa-animated-image>
```

### Custom Styling

```css
/* Rounded corners */
wa-animated-image {
  border-radius: 12px;
  overflow: hidden;
}

/* Shadow effect */
wa-animated-image {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Border */
wa-animated-image {
  border: 3px solid #e5e7eb;
}
```

## Best Practices

- ✅ Always provide meaningful `alt` text for accessibility
- ✅ Set `play="false"` for animations that might be distracting
- ✅ Use appropriate file sizes to ensure fast loading
- ✅ Consider autoplay preferences for users who may find animations distracting
- ✅ Provide visible controls for important animations
- ❌ Don't autoplay animations that could cause seizures (rapid flashing)
- ❌ Avoid using large animated GIFs that slow down page load
- ❌ Don't use animations as the only way to convey important information

## Accessibility

- Always include descriptive `alt` text for screen readers
- Consider users with vestibular disorders who may be sensitive to motion
- Respect user preferences for reduced motion:

```javascript
const animation = document.querySelector('wa-animated-image');

// Check if user prefers reduced motion
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  animation.pause();
}
```

- Ensure animations don't contain rapidly flashing content that could trigger seizures
- Provide alternative ways to access information if conveyed through animation

## Troubleshooting

### Animation Not Loading

**Problem:** The animated image doesn't display

**Solution:** Verify the `src` path is correct and the file is accessible

```html
<!-- ✅ Correct -->
<wa-animated-image src="/images/animation.gif" alt="Animation"></wa-animated-image>

<!-- ❌ Wrong path -->
<wa-animated-image src="animation.gif" alt="Animation"></wa-animated-image>
```

### Animation Not Pausing

**Problem:** Calling `pause()` doesn't stop the animation

**Solution:** Ensure you're calling the method on the correct element and the image has loaded

```javascript
const animation = document.querySelector('wa-animated-image');

// Wait for the image to load
animation.addEventListener('load', () => {
  animation.pause();
});
```

### Performance Issues

**Problem:** Page becomes slow with multiple animations

**Solution:** Limit the number of simultaneously playing animations

```javascript
// Only play one animation at a time
const animations = document.querySelectorAll('wa-animated-image');

animations.forEach(animation => {
  animation.pause();
});

// Play only the selected one
selectedAnimation.play();
```

## Related

- [Image](./image.md)
- [Image Comparer](./image-comparer.md)
- [Icon](./icon.md)
- [Avatar](./avatar.md)
