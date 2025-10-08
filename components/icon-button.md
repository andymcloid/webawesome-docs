# Icon Button

Buttons that display only an icon, perfect for toolbars and compact interfaces.

## Overview

The `<wa-icon-button>` component provides a button that contains only an icon, making it ideal for toolbars, action menus, and compact user interfaces where space is limited. Unlike regular buttons with icons, icon buttons are specifically designed and optimized for icon-only use cases.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/icon-button/icon-button.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic icon button -->
<wa-icon-button name="gear" label="Settings"></wa-icon-button>

<!-- Different icons -->
<wa-icon-button name="heart" label="Like"></wa-icon-button>
<wa-icon-button name="trash" label="Delete"></wa-icon-button>
<wa-icon-button name="pencil" label="Edit"></wa-icon-button>
```

## Sizes

Control icon button size:

```html
<!-- Small icon button -->
<wa-icon-button name="gear" label="Settings" size="small"></wa-icon-button>

<!-- Medium icon button (default) -->
<wa-icon-button name="gear" label="Settings" size="medium"></wa-icon-button>

<!-- Large icon button -->
<wa-icon-button name="gear" label="Settings" size="large"></wa-icon-button>
```

## Icon Libraries

Use icons from different libraries:

```html
<!-- Default library -->
<wa-icon-button name="heart" label="Like"></wa-icon-button>

<!-- Bootstrap Icons -->
<wa-icon-button
  name="heart-fill"
  library="bootstrap"
  label="Like">
</wa-icon-button>

<!-- Font Awesome -->
<wa-icon-button
  name="heart"
  library="fa"
  label="Like">
</wa-icon-button>
```

## Disabled State

Disable icon buttons:

```html
<wa-icon-button name="trash" label="Delete" disabled></wa-icon-button>
```

## As Link

Render icon button as a link:

```html
<!-- Simple link -->
<wa-icon-button
  name="link"
  label="External Link"
  href="https://example.com">
</wa-icon-button>

<!-- Open in new tab -->
<wa-icon-button
  name="box-arrow-up-right"
  label="Open in new tab"
  href="https://example.com"
  target="_blank">
</wa-icon-button>

<!-- Download link -->
<wa-icon-button
  name="download"
  label="Download"
  href="/files/document.pdf"
  download>
</wa-icon-button>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `name` | string | - | Yes | Name of the icon to display |
| `library` | string | `'default'` | No | Icon library to use |
| `label` | string | - | Yes | Accessible label for screen readers |
| `disabled` | boolean | `false` | No | Disable the button |
| `href` | string | - | No | When set, renders button as `<a>` link |
| `target` | string | - | No | Link target (requires `href`) |
| `download` | string \| boolean | - | No | Download attribute (requires `href`) |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `click()` | Simulates a click on the button | `void` |
| `focus(options?)` | Sets focus on the button | `void` |
| `blur()` | Removes focus from the button | `void` |

### Method Examples

```javascript
const iconButton = document.querySelector('wa-icon-button');

// Programmatically click
iconButton.click();

// Focus the button
iconButton.focus();

// Remove focus
iconButton.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `click` | Fired when the button is clicked | - |
| `wa-focus` | Emitted when the button gains focus | - |
| `wa-blur` | Emitted when the button loses focus | - |

### Event Examples

```javascript
const iconButton = document.querySelector('wa-icon-button');

// Click event
iconButton.addEventListener('click', () => {
  console.log('Icon button clicked');
});

// Focus event
iconButton.addEventListener('wa-focus', () => {
  console.log('Icon button focused');
});

// Blur event
iconButton.addEventListener('wa-blur', () => {
  console.log('Icon button blurred');
});
```

## Examples

### Toolbar

```html
<div class="toolbar">
  <wa-icon-button name="arrow-left" label="Back"></wa-icon-button>
  <wa-icon-button name="arrow-right" label="Forward"></wa-icon-button>
  <wa-icon-button name="arrow-clockwise" label="Refresh"></wa-icon-button>
  <wa-icon-button name="house" label="Home"></wa-icon-button>
</div>

<style>
  .toolbar {
    display: flex;
    gap: 0.5rem;
    padding: 0.5rem;
    background: #f3f4f6;
    border-radius: 8px;
  }
</style>
```

### Action Menu

```html
<wa-card>
  <div slot="header" class="card-header">
    <h3>Article Title</h3>
    <div class="actions">
      <wa-icon-button name="pencil" label="Edit"></wa-icon-button>
      <wa-icon-button name="share" label="Share"></wa-icon-button>
      <wa-icon-button name="trash" label="Delete"></wa-icon-button>
    </div>
  </div>

  <p>Article content goes here...</p>
</wa-card>

<style>
  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .actions {
    display: flex;
    gap: 0.25rem;
  }
</style>
```

### Like Button with State

```html
<wa-icon-button
  id="likeBtn"
  name="heart"
  label="Like">
</wa-icon-button>
<span id="likeCount">0</span>

<script>
  const likeBtn = document.getElementById('likeBtn');
  const likeCount = document.getElementById('likeCount');
  let liked = false;
  let count = 0;

  likeBtn.addEventListener('click', () => {
    liked = !liked;
    likeBtn.name = liked ? 'heart-fill' : 'heart';
    count += liked ? 1 : -1;
    likeCount.textContent = count;
  });
</script>
```

### Media Player Controls

```html
<div class="media-player">
  <audio id="audio" src="/audio/sample.mp3"></audio>

  <div class="player-controls">
    <wa-icon-button
      id="prevBtn"
      name="skip-backward"
      label="Previous">
    </wa-icon-button>

    <wa-icon-button
      id="playBtn"
      name="play-fill"
      label="Play"
      size="large">
    </wa-icon-button>

    <wa-icon-button
      id="nextBtn"
      name="skip-forward"
      label="Next">
    </wa-icon-button>

    <wa-icon-button
      id="volumeBtn"
      name="volume-up"
      label="Mute">
    </wa-icon-button>
  </div>
</div>

<script>
  const audio = document.getElementById('audio');
  const playBtn = document.getElementById('playBtn');
  const volumeBtn = document.getElementById('volumeBtn');

  let isPlaying = false;
  let isMuted = false;

  playBtn.addEventListener('click', () => {
    if (isPlaying) {
      audio.pause();
      playBtn.name = 'play-fill';
      playBtn.label = 'Play';
    } else {
      audio.play();
      playBtn.name = 'pause-fill';
      playBtn.label = 'Pause';
    }
    isPlaying = !isPlaying;
  });

  volumeBtn.addEventListener('click', () => {
    audio.muted = !isMuted;
    volumeBtn.name = isMuted ? 'volume-up' : 'volume-mute';
    volumeBtn.label = isMuted ? 'Unmute' : 'Mute';
    isMuted = !isMuted;
  });
</script>

<style>
  .player-controls {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
    background: #f3f4f6;
    border-radius: 12px;
  }
</style>
```

### Navigation Buttons

```html
<div class="nav-buttons">
  <wa-icon-button
    name="chevron-left"
    label="Previous page"
    href="/page/1">
  </wa-icon-button>

  <span>Page 2 of 10</span>

  <wa-icon-button
    name="chevron-right"
    label="Next page"
    href="/page/3">
  </wa-icon-button>
</div>

<style>
  .nav-buttons {
    display: flex;
    align-items: center;
    gap: 1rem;
    justify-content: center;
    padding: 1rem;
  }
</style>
```

### Social Share Buttons

```html
<div class="share-buttons">
  <p>Share this article:</p>

  <div class="buttons">
    <wa-icon-button
      name="twitter"
      label="Share on Twitter"
      href="https://twitter.com/intent/tweet?url=..."
      target="_blank">
    </wa-icon-button>

    <wa-icon-button
      name="facebook"
      label="Share on Facebook"
      href="https://www.facebook.com/sharer/sharer.php?u=..."
      target="_blank">
    </wa-icon-button>

    <wa-icon-button
      name="linkedin"
      label="Share on LinkedIn"
      href="https://www.linkedin.com/sharing/share-offsite/?url=..."
      target="_blank">
    </wa-icon-button>

    <wa-icon-button
      name="envelope"
      label="Share via Email"
      href="mailto:?subject=...&body=...">
    </wa-icon-button>
  </div>
</div>

<style>
  .share-buttons {
    text-align: center;
    padding: 2rem;
  }

  .buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
    margin-top: 1rem;
  }
</style>
```

### Image Gallery Controls

```html
<div class="gallery">
  <img id="galleryImage" src="/images/photo1.jpg" alt="Gallery image">

  <div class="gallery-controls">
    <wa-icon-button
      id="zoomOut"
      name="zoom-out"
      label="Zoom out">
    </wa-icon-button>

    <wa-icon-button
      id="zoomIn"
      name="zoom-in"
      label="Zoom in">
    </wa-icon-button>

    <wa-icon-button
      id="rotate"
      name="arrow-clockwise"
      label="Rotate">
    </wa-icon-button>

    <wa-icon-button
      id="download"
      name="download"
      label="Download"
      href="/images/photo1.jpg"
      download>
    </wa-icon-button>

    <wa-icon-button
      id="fullscreen"
      name="fullscreen"
      label="Fullscreen">
    </wa-icon-button>
  </div>
</div>

<style>
  .gallery {
    max-width: 800px;
    margin: 0 auto;
  }

  .gallery img {
    width: 100%;
    height: auto;
    border-radius: 8px;
  }

  .gallery-controls {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    margin-top: 1rem;
    padding: 0.5rem;
    background: #f3f4f6;
    border-radius: 8px;
  }
</style>
```

### Notification Badge

```html
<div class="notification-button">
  <wa-icon-button name="bell" label="Notifications"></wa-icon-button>
  <wa-badge variant="danger" pill>5</wa-badge>
</div>

<style>
  .notification-button {
    position: relative;
    display: inline-block;
  }

  .notification-button wa-badge {
    position: absolute;
    top: -4px;
    right: -4px;
  }
</style>
```

## CSS Parts

Use CSS parts to style internal elements:

```css
/* Style the button base */
wa-icon-button::part(base) {
  border-radius: 8px;
  background-color: #f3f4f6;
}

wa-icon-button::part(base):hover {
  background-color: #e5e7eb;
}
```

## Customization

### Custom Colors

```css
/* Primary action */
wa-icon-button.primary::part(base) {
  color: #6366f1;
}

/* Danger action */
wa-icon-button.danger::part(base) {
  color: #ef4444;
}

wa-icon-button.danger::part(base):hover {
  background-color: #fee2e2;
}
```

### Custom Sizing

```css
/* Extra large */
wa-icon-button.xl {
  font-size: 2rem;
}

/* Extra small */
wa-icon-button.xs {
  font-size: 0.875rem;
}
```

## Best Practices

- ✅ Always provide a descriptive `label` attribute for accessibility
- ✅ Use consistent icon styles throughout your interface
- ✅ Group related icon buttons together
- ✅ Provide tooltips to clarify button actions
- ✅ Use appropriate icon sizes for touch targets (minimum 44x44px)
- ✅ Use familiar icons for common actions
- ❌ Don't rely on icons alone without proper labels
- ❌ Avoid using obscure icons that users won't recognize
- ❌ Don't make icon buttons too small to interact with
- ❌ Avoid too many icon buttons in a row without grouping

## Accessibility

- Always include the `label` attribute for screen readers:

```html
<!-- ✅ Good - has label -->
<wa-icon-button name="trash" label="Delete item"></wa-icon-button>

<!-- ❌ Bad - no label -->
<wa-icon-button name="trash"></wa-icon-button>
```

- Ensure sufficient color contrast for icons
- Make sure touch targets are at least 44x44 pixels
- Provide tooltips to clarify icon meanings:

```html
<wa-tooltip content="Delete this item">
  <wa-icon-button name="trash" label="Delete"></wa-icon-button>
</wa-tooltip>
```

- Icon buttons are keyboard accessible by default
- Use ARIA attributes when needed for additional context

## Troubleshooting

### Icon Not Displaying

**Problem:** Icon doesn't appear in the button

**Solution:** Verify the icon name and library are correct

```html
<!-- ✅ Correct icon name -->
<wa-icon-button name="gear" label="Settings"></wa-icon-button>

<!-- ❌ Wrong icon name -->
<wa-icon-button name="settings" label="Settings"></wa-icon-button>
```

### Button Too Small to Click

**Problem:** Icon button is difficult to interact with

**Solution:** Increase the size or add padding

```css
wa-icon-button {
  font-size: 1.5rem;
  padding: 0.5rem;
}
```

### Missing Label Warning

**Problem:** Console shows accessibility warning

**Solution:** Always include the `label` attribute

```html
<wa-icon-button name="heart" label="Like this post"></wa-icon-button>
```

## Related

- [Button](./button.md)
- [Icon](./icon.md)
- [Button Group](./button-group.md)
- [Tooltip](./tooltip.md)
