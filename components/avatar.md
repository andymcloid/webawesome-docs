# Avatar

A component for displaying user avatars with images, initials, or icons.

## Overview

The `<wa-avatar>` component provides a flexible way to display user avatars throughout your application. It supports images, text initials, icons, and fallback states. The component can be customized with different shapes and sizes to match your design requirements.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/avatar/avatar.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Avatar with image -->
<wa-avatar image="https://i.pravatar.cc/150?img=1" label="User avatar"></wa-avatar>

<!-- Avatar with initials -->
<wa-avatar initials="JD" label="John Doe"></wa-avatar>

<!-- Avatar with icon -->
<wa-avatar label="User">
  <wa-icon name="person"></wa-icon>
</wa-avatar>
```

## Shapes

Control avatar shape with the `shape` attribute:

```html
<!-- Circle (default) -->
<wa-avatar image="https://i.pravatar.cc/150?img=2" shape="circle"></wa-avatar>

<!-- Rounded -->
<wa-avatar image="https://i.pravatar.cc/150?img=3" shape="rounded"></wa-avatar>

<!-- Square -->
<wa-avatar image="https://i.pravatar.cc/150?img=4" shape="square"></wa-avatar>
```

## Initials

Display user initials when no image is available:

```html
<!-- Single initial -->
<wa-avatar initials="J" label="Jane"></wa-avatar>

<!-- Two initials -->
<wa-avatar initials="JD" label="John Doe"></wa-avatar>

<!-- Three initials (will display first two) -->
<wa-avatar initials="JDS" label="John David Smith"></wa-avatar>
```

### Generating Initials

```html
<wa-avatar id="userAvatar"></wa-avatar>

<script>
  function getInitials(name) {
    return name
      .split(' ')
      .map(n => n[0])
      .join('')
      .toUpperCase()
      .slice(0, 2);
  }

  const avatar = document.getElementById('userAvatar');
  const userName = 'John Doe';

  avatar.initials = getInitials(userName);
  avatar.label = userName;
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `image` | string | - | No | Image URL for the avatar |
| `label` | string | - | No | Accessible label (required for accessibility) |
| `initials` | string | - | No | Initials to display (when no image) |
| `shape` | string | `'circle'` | No | Avatar shape: `circle`, `rounded`, `square` |
| `loading` | string | `'eager'` | No | Image loading strategy: `eager`, `lazy` |

## Examples

### User Profile

```html
<div style="display: flex; align-items: center; gap: 1rem;">
  <wa-avatar
    image="https://i.pravatar.cc/150?img=5"
    label="Sarah Johnson"
    shape="circle">
  </wa-avatar>
  <div>
    <h3 style="margin: 0;">Sarah Johnson</h3>
    <p style="margin: 0; color: #666;">Product Designer</p>
  </div>
</div>
```

### Avatar Group

```html
<div style="display: flex; margin-left: 1rem;">
  <wa-avatar
    image="https://i.pravatar.cc/150?img=1"
    label="User 1"
    style="margin-left: -1rem;">
  </wa-avatar>
  <wa-avatar
    image="https://i.pravatar.cc/150?img=2"
    label="User 2"
    style="margin-left: -1rem;">
  </wa-avatar>
  <wa-avatar
    image="https://i.pravatar.cc/150?img=3"
    label="User 3"
    style="margin-left: -1rem;">
  </wa-avatar>
  <wa-avatar
    initials="+5"
    label="5 more users"
    style="margin-left: -1rem; background: #e5e7eb; color: #374151;">
  </wa-avatar>
</div>
```

### Avatar with Status Badge

```html
<div style="position: relative; display: inline-block;">
  <wa-avatar
    image="https://i.pravatar.cc/150?img=6"
    label="Online user">
  </wa-avatar>
  <wa-badge
    variant="success"
    pill
    style="
      position: absolute;
      bottom: 0;
      right: 0;
      width: 12px;
      height: 12px;
      padding: 0;
      border: 2px solid white;
    ">
  </wa-badge>
</div>
```

### Different Sizes

```html
<div style="display: flex; align-items: center; gap: 1rem;">
  <!-- Small -->
  <wa-avatar
    image="https://i.pravatar.cc/150?img=7"
    label="Small avatar"
    style="--size: 2rem; font-size: 0.75rem;">
  </wa-avatar>

  <!-- Medium (default) -->
  <wa-avatar
    image="https://i.pravatar.cc/150?img=8"
    label="Medium avatar"
    style="--size: 3rem; font-size: 1rem;">
  </wa-avatar>

  <!-- Large -->
  <wa-avatar
    image="https://i.pravatar.cc/150?img=9"
    label="Large avatar"
    style="--size: 4rem; font-size: 1.25rem;">
  </wa-avatar>

  <!-- Extra Large -->
  <wa-avatar
    image="https://i.pravatar.cc/150?img=10"
    label="Extra large avatar"
    style="--size: 6rem; font-size: 1.5rem;">
  </wa-avatar>
</div>
```

### Fallback Pattern

```html
<wa-avatar id="userAvatar" label="User avatar"></wa-avatar>

<script>
  const avatar = document.getElementById('userAvatar');
  const user = {
    name: 'John Doe',
    avatar: 'https://invalid-url.com/avatar.jpg' // Broken URL
  };

  // Try to load image, fallback to initials
  avatar.image = user.avatar;
  avatar.initials = user.name
    .split(' ')
    .map(n => n[0])
    .join('')
    .toUpperCase();
  avatar.label = user.name;

  // Listen for image load errors
  avatar.addEventListener('error', () => {
    console.log('Image failed to load, showing initials');
  });
</script>
```

### Team Members List

```html
<div style="max-width: 400px;">
  <h3>Team Members</h3>

  <div style="display: flex; flex-direction: column; gap: 1rem;">
    <div style="display: flex; align-items: center; gap: 1rem;">
      <wa-avatar
        image="https://i.pravatar.cc/150?img=11"
        label="Alice Cooper">
      </wa-avatar>
      <div style="flex: 1;">
        <div style="font-weight: 500;">Alice Cooper</div>
        <div style="font-size: 0.875rem; color: #666;">Team Lead</div>
      </div>
      <wa-badge variant="success">Active</wa-badge>
    </div>

    <div style="display: flex; align-items: center; gap: 1rem;">
      <wa-avatar
        image="https://i.pravatar.cc/150?img=12"
        label="Bob Smith">
      </wa-avatar>
      <div style="flex: 1;">
        <div style="font-weight: 500;">Bob Smith</div>
        <div style="font-size: 0.875rem; color: #666;">Developer</div>
      </div>
      <wa-badge variant="warning">Away</wa-badge>
    </div>

    <div style="display: flex; align-items: center; gap: 1rem;">
      <wa-avatar
        initials="CD"
        label="Carol Davis">
      </wa-avatar>
      <div style="flex: 1;">
        <div style="font-weight: 500;">Carol Davis</div>
        <div style="font-size: 0.875rem; color: #666;">Designer</div>
      </div>
      <wa-badge variant="neutral">Offline</wa-badge>
    </div>
  </div>
</div>
```

### Interactive Avatar Upload

```html
<div style="text-align: center;">
  <wa-avatar
    id="profileAvatar"
    initials="JD"
    label="Profile picture"
    shape="circle"
    style="--size: 8rem; cursor: pointer; margin-bottom: 1rem;">
  </wa-avatar>

  <input
    type="file"
    id="avatarUpload"
    accept="image/*"
    style="display: none;">

  <br>
  <wa-button id="uploadBtn">
    <wa-icon slot="start" name="camera"></wa-icon>
    Upload Photo
  </wa-button>
</div>

<script>
  const avatar = document.getElementById('profileAvatar');
  const uploadInput = document.getElementById('avatarUpload');
  const uploadBtn = document.getElementById('uploadBtn');

  uploadBtn.addEventListener('click', () => {
    uploadInput.click();
  });

  avatar.addEventListener('click', () => {
    uploadInput.click();
  });

  uploadInput.addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => {
        avatar.image = event.target.result;
      };
      reader.readAsDataURL(file);
    }
  });
</script>
```

### Avatar with Dropdown Menu

```html
<wa-dropdown>
  <wa-avatar
    slot="trigger"
    image="https://i.pravatar.cc/150?img=13"
    label="User menu"
    style="cursor: pointer;">
  </wa-avatar>

  <wa-menu>
    <wa-menu-item>
      <wa-icon slot="start" name="person"></wa-icon>
      Profile
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="gear"></wa-icon>
      Settings
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item>
      <wa-icon slot="start" name="box-arrow-right"></wa-icon>
      Logout
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Icon or content to display when no image is provided |
| `icon` | Icon slot (alternative to default slot) |

## CSS Parts

Use CSS parts to style internal avatar elements:

```css
/* Style the avatar base */
wa-avatar::part(base) {
  border: 2px solid #e5e7eb;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

/* Style the avatar image */
wa-avatar::part(image) {
  object-fit: cover;
}

/* Style the initials */
wa-avatar::part(initials) {
  font-weight: bold;
  text-transform: uppercase;
}
```

## Customization

### Custom Colors for Initials

```css
/* Blue avatar */
wa-avatar.blue::part(base) {
  background-color: #3b82f6;
  color: white;
}

/* Green avatar */
wa-avatar.green::part(base) {
  background-color: #10b981;
  color: white;
}

/* Purple avatar */
wa-avatar.purple::part(base) {
  background-color: #8b5cf6;
  color: white;
}
```

### Generate Color from Name

```javascript
function stringToColor(str) {
  let hash = 0;
  for (let i = 0; i < str.length; i++) {
    hash = str.charCodeAt(i) + ((hash << 5) - hash);
  }

  const hue = hash % 360;
  return `hsl(${hue}, 70%, 50%)`;
}

// Apply to avatar
const avatar = document.querySelector('wa-avatar');
const userName = 'John Doe';
avatar.style.backgroundColor = stringToColor(userName);
avatar.style.color = 'white';
```

### Custom Border and Shadow

```css
/* Elevated avatar */
wa-avatar.elevated::part(base) {
  border: 3px solid white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Outlined avatar */
wa-avatar.outlined::part(base) {
  border: 2px solid currentColor;
}
```

## Best Practices

- Always provide a descriptive `label` for accessibility
- Use images when available, initials as fallback
- Keep initials to 1-2 characters for best appearance
- Use consistent shapes throughout your application
- Consider lazy loading for avatar images in lists
- Provide appropriate contrast for initials on backgrounds
- Use appropriate sizes for different contexts
- Group avatars when showing multiple users
- Add status indicators when showing online/offline states
- Handle image loading errors gracefully with fallbacks

## Accessibility

- Always provide a `label` attribute for screen readers
- The component automatically includes appropriate ARIA attributes
- Ensure sufficient contrast between initials and background
- For interactive avatars (buttons/links), add appropriate roles:

```html
<!-- Avatar as button -->
<wa-avatar
  role="button"
  tabindex="0"
  image="https://i.pravatar.cc/150?img=14"
  label="Open user menu"
  style="cursor: pointer;">
</wa-avatar>
```

- For decorative avatars, use `aria-hidden`:

```html
<wa-avatar image="url" aria-hidden="true"></wa-avatar>
```

## Troubleshooting

### Image Not Displaying

**Problem:** Avatar image doesn't appear

**Solution:** Check the image URL and CORS policy

```javascript
// Verify image loads
const img = new Image();
img.onload = () => console.log('Image loaded successfully');
img.onerror = () => console.error('Image failed to load');
img.src = 'your-image-url';
```

### Initials Not Showing

**Problem:** Initials don't appear when no image is set

**Solution:** Ensure `initials` attribute is set and avatar has no image

```html
<!-- Won't show initials (image takes precedence) -->
<wa-avatar image="url" initials="JD"></wa-avatar>

<!-- Will show initials -->
<wa-avatar initials="JD"></wa-avatar>
```

### Avatar Size Issues

**Problem:** Avatar appears too small or large

**Solution:** Use CSS custom property `--size` to control dimensions

```css
wa-avatar {
  --size: 3rem; /* Adjust as needed */
}
```

## Related

- [Badge](./badge.md)
- [Icon](./icon.md)
- [Card](./card.md)
- [Dropdown](./dropdown.md)
