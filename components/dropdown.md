# Dropdown

Dropdowns display a menu of actions or options triggered by a button.

## Overview

The `<wa-dropdown>` component provides a customizable dropdown menu system with positioning, keyboard navigation, and accessibility features. It works together with `<wa-menu>` and `<wa-menu-item>` components to create interactive dropdown menus.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/dropdown/dropdown.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic dropdown -->
<wa-dropdown>
  <wa-button slot="trigger" caret>Dropdown</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Dropdown with icons -->
<wa-dropdown>
  <wa-button slot="trigger" caret>Actions</wa-button>
  <wa-menu>
    <wa-menu-item>
      <wa-icon slot="start" name="download"></wa-icon>
      Download
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="share"></wa-icon>
      Share
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="trash"></wa-icon>
      Delete
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Placement

Control the dropdown position with the `placement` attribute:

```html
<!-- Top placement -->
<wa-dropdown placement="top">
  <wa-button slot="trigger" caret>Top</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Right placement -->
<wa-dropdown placement="right">
  <wa-button slot="trigger" caret>Right</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Bottom placement (default) -->
<wa-dropdown placement="bottom">
  <wa-button slot="trigger" caret>Bottom</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Left placement -->
<wa-dropdown placement="left">
  <wa-button slot="trigger" caret>Left</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

### Precise Placement

Use more specific placement values for fine control:

```html
<wa-dropdown placement="top-start">Top Start</wa-dropdown>
<wa-dropdown placement="top-end">Top End</wa-dropdown>
<wa-dropdown placement="right-start">Right Start</wa-dropdown>
<wa-dropdown placement="right-end">Right End</wa-dropdown>
<wa-dropdown placement="bottom-start">Bottom Start</wa-dropdown>
<wa-dropdown placement="bottom-end">Bottom End</wa-dropdown>
<wa-dropdown placement="left-start">Left Start</wa-dropdown>
<wa-dropdown placement="left-end">Left End</wa-dropdown>
```

## Distance & Skidding

Control the dropdown offset from the trigger:

```html
<!-- Distance (gap from trigger) -->
<wa-dropdown distance="20">
  <wa-button slot="trigger" caret>Distance 20px</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Skidding (horizontal offset) -->
<wa-dropdown skidding="20">
  <wa-button slot="trigger" caret>Skidding 20px</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Combined -->
<wa-dropdown distance="15" skidding="10">
  <wa-button slot="trigger" caret>Custom Position</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Hoisting

Use `hoist` to render the dropdown in a higher layer to prevent clipping:

```html
<div style="overflow: hidden; position: relative; height: 150px;">
  <wa-dropdown hoist>
    <wa-button slot="trigger" caret>Hoisted Dropdown</wa-button>
    <wa-menu>
      <wa-menu-item>Option 1</wa-menu-item>
      <wa-menu-item>Option 2</wa-menu-item>
      <wa-menu-item>Option 3</wa-menu-item>
    </wa-menu>
  </wa-dropdown>
</div>
```

## With Dividers

Organize menu items with dividers:

```html
<wa-dropdown>
  <wa-button slot="trigger" caret>File</wa-button>
  <wa-menu>
    <wa-menu-item>New File</wa-menu-item>
    <wa-menu-item>New Window</wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item>Open File</wa-menu-item>
    <wa-menu-item>Open Folder</wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item>Save</wa-menu-item>
    <wa-menu-item>Save As...</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## With Icons

Add icons to menu items for visual clarity:

```html
<wa-dropdown>
  <wa-button slot="trigger" caret>
    <wa-icon slot="start" name="settings"></wa-icon>
    Settings
  </wa-button>
  <wa-menu>
    <wa-menu-item>
      <wa-icon slot="start" name="user"></wa-icon>
      Profile
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="bell"></wa-icon>
      Notifications
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="lock"></wa-icon>
      Privacy
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="shield"></wa-icon>
      Security
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Nested Menus

Create submenus for hierarchical navigation:

```html
<wa-dropdown>
  <wa-button slot="trigger" caret>Menu</wa-button>
  <wa-menu>
    <wa-menu-item>Home</wa-menu-item>
    <wa-menu-item>About</wa-menu-item>
    <wa-menu-item>
      Products
      <wa-menu slot="submenu">
        <wa-menu-item>Electronics</wa-menu-item>
        <wa-menu-item>Clothing</wa-menu-item>
        <wa-menu-item>
          Books
          <wa-menu slot="submenu">
            <wa-menu-item>Fiction</wa-menu-item>
            <wa-menu-item>Non-Fiction</wa-menu-item>
            <wa-menu-item>Technical</wa-menu-item>
          </wa-menu>
        </wa-menu-item>
      </wa-menu>
    </wa-menu-item>
    <wa-menu-item>Contact</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Programmatic Control

Control dropdown state with JavaScript:

```html
<wa-dropdown id="myDropdown">
  <wa-button slot="trigger" caret>Controlled Dropdown</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<div style="margin-top: 1rem;">
  <wa-button id="showBtn">Show</wa-button>
  <wa-button id="hideBtn">Hide</wa-button>
  <wa-button id="toggleBtn">Toggle</wa-button>
</div>

<script>
  const dropdown = document.getElementById('myDropdown');
  const showBtn = document.getElementById('showBtn');
  const hideBtn = document.getElementById('hideBtn');
  const toggleBtn = document.getElementById('toggleBtn');

  showBtn.addEventListener('click', () => dropdown.show());
  hideBtn.addEventListener('click', () => dropdown.hide());
  toggleBtn.addEventListener('click', () => {
    dropdown.open ? dropdown.hide() : dropdown.show();
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `open` | boolean | `false` | No | Controls the open state of the dropdown |
| `placement` | string | `'bottom-start'` | No | Dropdown position: `top`, `top-start`, `top-end`, `right`, `right-start`, `right-end`, `bottom`, `bottom-start`, `bottom-end`, `left`, `left-start`, `left-end` |
| `distance` | number | `0` | No | Distance in pixels from the trigger |
| `skidding` | number | `0` | No | Offset in pixels along the trigger |
| `hoist` | boolean | `false` | No | Render dropdown in a higher layer to prevent clipping |
| `disabled` | boolean | `false` | No | Disable the dropdown |
| `stay-open-on-select` | boolean | `false` | No | Keep dropdown open after selecting an item |
| `contained` | boolean | `false` | No | Keep dropdown within the bounds of its container |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Opens the dropdown | `Promise<void>` |
| `hide()` | Closes the dropdown | `Promise<void>` |
| `reposition()` | Recalculates dropdown position | `void` |

### Method Examples

```javascript
const dropdown = document.querySelector('wa-dropdown');

// Show the dropdown
await dropdown.show();

// Hide the dropdown
await dropdown.hide();

// Reposition the dropdown (useful after content changes)
dropdown.reposition();

// Toggle with state check
if (dropdown.open) {
  await dropdown.hide();
} else {
  await dropdown.show();
}
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the dropdown opens | - |
| `wa-after-show` | Emitted after the dropdown opens and animations complete | - |
| `wa-hide` | Emitted when the dropdown closes | - |
| `wa-after-hide` | Emitted after the dropdown closes and animations complete | - |
| `wa-select` | Emitted when a menu item is selected | `{ item: HTMLElement }` |

### Event Examples

```javascript
const dropdown = document.querySelector('wa-dropdown');

// Before dropdown shows
dropdown.addEventListener('wa-show', (event) => {
  console.log('Dropdown is opening');
  // You can call event.preventDefault() to cancel
});

// After dropdown shows
dropdown.addEventListener('wa-after-show', () => {
  console.log('Dropdown is now open');
});

// Before dropdown hides
dropdown.addEventListener('wa-hide', (event) => {
  console.log('Dropdown is closing');
  // You can call event.preventDefault() to cancel
});

// After dropdown hides
dropdown.addEventListener('wa-after-hide', () => {
  console.log('Dropdown is now closed');
});

// When an item is selected
dropdown.addEventListener('wa-select', (event) => {
  console.log('Selected item:', event.detail.item);
  console.log('Selected value:', event.detail.item.value);
});
```

## Slots

| Slot | Description |
|------|-------------|
| `trigger` | The element that triggers the dropdown (typically a button) |
| (default) | The dropdown content (typically a wa-menu) |

## Examples

### User Account Menu

```html
<wa-dropdown placement="bottom-end">
  <wa-button slot="trigger" variant="neutral" circle>
    <wa-avatar initials="JD"></wa-avatar>
  </wa-button>
  <wa-menu>
    <wa-menu-item>
      <wa-icon slot="start" name="user"></wa-icon>
      My Profile
    </wa-menu-item>
    <wa-menu-item>
      <wa-icon slot="start" name="settings"></wa-icon>
      Settings
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item>
      <wa-icon slot="start" name="help-circle"></wa-icon>
      Help & Support
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item>
      <wa-icon slot="start" name="log-out"></wa-icon>
      Sign Out
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

### Context Menu

```html
<wa-dropdown id="contextMenu">
  <wa-button slot="trigger" variant="neutral" caret>Right Click</wa-button>
  <wa-menu>
    <wa-menu-item value="cut">
      <wa-icon slot="start" name="scissors"></wa-icon>
      Cut
      <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+X</span>
    </wa-menu-item>
    <wa-menu-item value="copy">
      <wa-icon slot="start" name="copy"></wa-icon>
      Copy
      <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+C</span>
    </wa-menu-item>
    <wa-menu-item value="paste">
      <wa-icon slot="start" name="clipboard"></wa-icon>
      Paste
      <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+V</span>
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item value="delete">
      <wa-icon slot="start" name="trash"></wa-icon>
      Delete
      <span slot="end" style="color: var(--wa-color-neutral-500);">Del</span>
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>

<script>
  const dropdown = document.getElementById('contextMenu');

  dropdown.addEventListener('wa-select', (event) => {
    const action = event.detail.item.value;
    console.log(`Action selected: ${action}`);

    switch(action) {
      case 'cut':
        // Handle cut
        break;
      case 'copy':
        // Handle copy
        break;
      case 'paste':
        // Handle paste
        break;
      case 'delete':
        // Handle delete
        break;
    }
  });
</script>
```

### Filtering Dropdown

```html
<wa-dropdown id="filterDropdown" stay-open-on-select>
  <wa-button slot="trigger" caret>
    <wa-icon slot="start" name="filter"></wa-icon>
    Filters
  </wa-button>
  <wa-menu>
    <wa-menu-item type="checkbox" value="active" checked>
      Show Active
    </wa-menu-item>
    <wa-menu-item type="checkbox" value="pending">
      Show Pending
    </wa-menu-item>
    <wa-menu-item type="checkbox" value="completed">
      Show Completed
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item type="checkbox" value="archived">
      Show Archived
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>

<script>
  const dropdown = document.getElementById('filterDropdown');

  dropdown.addEventListener('wa-select', (event) => {
    const item = event.detail.item;
    console.log(`Filter ${item.value}: ${item.checked ? 'enabled' : 'disabled'}`);
    // Apply filter logic
  });
</script>
```

### Dropdown with Custom Trigger

```html
<wa-dropdown>
  <div slot="trigger" style="cursor: pointer; padding: 0.5rem; border: 1px solid var(--wa-color-neutral-300); border-radius: 4px;">
    Click me for options
  </div>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
    <wa-menu-item>Option 2</wa-menu-item>
    <wa-menu-item>Option 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## CSS Parts

Use CSS parts to style internal dropdown elements:

```css
/* Style the dropdown popup */
wa-dropdown::part(popup) {
  border: 2px solid var(--wa-color-primary-600);
}

/* Style the popup content container */
wa-dropdown::part(panel) {
  background-color: var(--wa-color-neutral-50);
}
```

## Customization

### Custom Styling

```css
/* Custom dropdown appearance */
wa-dropdown::part(popup) {
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
}

wa-dropdown::part(panel) {
  padding: 0.5rem 0;
}
```

### Maximum Height

```css
/* Limit dropdown height with scrolling */
wa-dropdown wa-menu {
  max-height: 300px;
  overflow-y: auto;
}
```

## Best Practices

- Use clear, action-oriented labels for menu items
- Group related items with dividers
- Place frequently used items at the top
- Use icons to improve scannability
- Keep menu depth shallow (2-3 levels max)
- Use keyboard shortcuts indicators for common actions
- Consider using `stay-open-on-select` for multi-select scenarios
- Use appropriate placement to keep menus visible

## Accessibility

- Dropdown automatically manages focus and keyboard navigation
- Use arrow keys to navigate menu items
- Press Enter or Space to select an item
- Press Escape to close the dropdown
- Screen readers announce dropdown state and menu items
- Ensure trigger buttons have descriptive labels

```html
<!-- Good: descriptive trigger -->
<wa-dropdown>
  <wa-button slot="trigger" caret>User Actions</wa-button>
  <wa-menu>
    <wa-menu-item>Edit Profile</wa-menu-item>
    <wa-menu-item>Sign Out</wa-menu-item>
  </wa-menu>
</wa-dropdown>

<!-- Better: with ARIA label for icon-only trigger -->
<wa-dropdown>
  <wa-button slot="trigger" circle aria-label="User account menu">
    <wa-icon name="user"></wa-icon>
  </wa-button>
  <wa-menu>
    <wa-menu-item>Edit Profile</wa-menu-item>
    <wa-menu-item>Sign Out</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Troubleshooting

### Dropdown Getting Clipped

**Problem:** Dropdown is cut off by container overflow

**Solution:** Use the `hoist` attribute

```html
<wa-dropdown hoist>
  <wa-button slot="trigger" caret>Dropdown</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

### Dropdown Not Closing on Select

**Problem:** Dropdown stays open after clicking an item

**Solution:** Remove `stay-open-on-select` attribute or set it to false

```html
<!-- Will close on select -->
<wa-dropdown>
  <wa-button slot="trigger" caret>Dropdown</wa-button>
  <wa-menu>
    <wa-menu-item>Option 1</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

### Dropdown Position Issues

**Problem:** Dropdown appears in wrong position

**Solution:** Use `reposition()` method after content changes

```javascript
const dropdown = document.querySelector('wa-dropdown');
// After updating menu items
dropdown.reposition();
```

## Related

- [Menu](./menu.md)
- [Menu Item](./menu-item.md)
- [Button](./button.md)
- [Divider](./divider.md)
