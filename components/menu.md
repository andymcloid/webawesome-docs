# Menu

Menus provide a list of options or actions for the user.

## Overview

The `<wa-menu>` component creates a vertical list of selectable options. It's commonly used inside dropdowns, popovers, or as standalone navigation. Menu works together with `<wa-menu-item>` and `<wa-menu-label>` components.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/menu/menu.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple menu -->
<wa-menu>
  <wa-menu-item>Option 1</wa-menu-item>
  <wa-menu-item>Option 2</wa-menu-item>
  <wa-menu-item>Option 3</wa-menu-item>
</wa-menu>

<!-- Menu with labels -->
<wa-menu>
  <wa-menu-label>File Operations</wa-menu-label>
  <wa-menu-item>New File</wa-menu-item>
  <wa-menu-item>Open File</wa-menu-item>
  <wa-menu-item>Save File</wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-label>Edit Operations</wa-menu-label>
  <wa-menu-item>Cut</wa-menu-item>
  <wa-menu-item>Copy</wa-menu-item>
  <wa-menu-item>Paste</wa-menu-item>
</wa-menu>
```

## In Dropdown

The most common use case is inside a dropdown:

```html
<wa-dropdown>
  <wa-button slot="trigger" caret>Actions</wa-button>
  <wa-menu>
    <wa-menu-item>Action 1</wa-menu-item>
    <wa-menu-item>Action 2</wa-menu-item>
    <wa-menu-item>Action 3</wa-menu-item>
  </wa-menu>
</wa-dropdown>
```

## Navigation Menu

Use menus for sidebar or primary navigation:

```html
<wa-menu style="max-width: 250px;">
  <wa-menu-item>
    <wa-icon slot="start" name="home"></wa-icon>
    Dashboard
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="users"></wa-icon>
    Users
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="settings"></wa-icon>
    Settings
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="file-text"></wa-icon>
    Reports
  </wa-menu-item>
</wa-menu>
```

## Menu with Icons

Add icons to improve visual recognition:

```html
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
    <wa-icon slot="start" name="edit"></wa-icon>
    Edit
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="trash"></wa-icon>
    Delete
  </wa-menu-item>
</wa-menu>
```

## Disabled Items

Disable menu items when actions are unavailable:

```html
<wa-menu>
  <wa-menu-item>Active Item</wa-menu-item>
  <wa-menu-item disabled>Disabled Item</wa-menu-item>
  <wa-menu-item>Another Active Item</wa-menu-item>
</wa-menu>
```

## Menu with Values

Assign values to menu items for easier handling:

```html
<wa-menu id="actionMenu">
  <wa-menu-item value="save">
    <wa-icon slot="start" name="save"></wa-icon>
    Save
  </wa-menu-item>
  <wa-menu-item value="export">
    <wa-icon slot="start" name="download"></wa-icon>
    Export
  </wa-menu-item>
  <wa-menu-item value="print">
    <wa-icon slot="start" name="printer"></wa-icon>
    Print
  </wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('actionMenu');

  menu.addEventListener('wa-select', (event) => {
    const value = event.detail.item.value;
    console.log('Selected action:', value);

    switch(value) {
      case 'save':
        // Handle save
        break;
      case 'export':
        // Handle export
        break;
      case 'print':
        // Handle print
        break;
    }
  });
</script>
```

## Context Menu

Create custom context menus:

```html
<div id="targetArea" style="padding: 2rem; border: 2px dashed var(--wa-color-neutral-300); text-align: center;">
  Right-click here
</div>

<wa-dropdown id="contextMenu">
  <wa-menu>
    <wa-menu-item value="cut">
      <wa-icon slot="start" name="scissors"></wa-icon>
      Cut
    </wa-menu-item>
    <wa-menu-item value="copy">
      <wa-icon slot="start" name="copy"></wa-icon>
      Copy
    </wa-menu-item>
    <wa-menu-item value="paste">
      <wa-icon slot="start" name="clipboard"></wa-icon>
      Paste
    </wa-menu-item>
    <wa-divider></wa-divider>
    <wa-menu-item value="delete">
      <wa-icon slot="start" name="trash"></wa-icon>
      Delete
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>

<script>
  const targetArea = document.getElementById('targetArea');
  const contextMenu = document.getElementById('contextMenu');

  targetArea.addEventListener('contextmenu', (event) => {
    event.preventDefault();
    contextMenu.style.position = 'fixed';
    contextMenu.style.left = event.clientX + 'px';
    contextMenu.style.top = event.clientY + 'px';
    contextMenu.open = true;
  });
</script>
```

## Command Palette

Build a command palette with search:

```html
<div style="max-width: 400px;">
  <wa-input placeholder="Type a command..." id="commandSearch">
    <wa-icon slot="start" name="search"></wa-icon>
  </wa-input>

  <wa-menu id="commandMenu" style="margin-top: 0.5rem;">
    <wa-menu-label>Navigation</wa-menu-label>
    <wa-menu-item data-keywords="home dashboard main">
      <wa-icon slot="start" name="home"></wa-icon>
      Go to Dashboard
    </wa-menu-item>
    <wa-menu-item data-keywords="profile account user">
      <wa-icon slot="start" name="user"></wa-icon>
      Go to Profile
    </wa-menu-item>

    <wa-divider></wa-divider>

    <wa-menu-label>Actions</wa-menu-label>
    <wa-menu-item data-keywords="new create add">
      <wa-icon slot="start" name="plus"></wa-icon>
      Create New Item
    </wa-menu-item>
    <wa-menu-item data-keywords="settings preferences config">
      <wa-icon slot="start" name="settings"></wa-icon>
      Open Settings
    </wa-menu-item>
  </wa-menu>
</div>

<script>
  const searchInput = document.getElementById('commandSearch');
  const menu = document.getElementById('commandMenu');

  searchInput.addEventListener('wa-input', (event) => {
    const searchTerm = event.target.value.toLowerCase();
    const items = menu.querySelectorAll('wa-menu-item');

    items.forEach(item => {
      const text = item.textContent.toLowerCase();
      const keywords = item.dataset.keywords || '';
      const matches = text.includes(searchTerm) || keywords.includes(searchTerm);

      item.style.display = matches ? '' : 'none';
    });
  });
</script>
```

## Grouped Menu

Organize items with labels and dividers:

```html
<wa-menu>
  <wa-menu-label>Recent Files</wa-menu-label>
  <wa-menu-item>document.pdf</wa-menu-item>
  <wa-menu-item>spreadsheet.xlsx</wa-menu-item>
  <wa-menu-item>presentation.pptx</wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-label>Quick Actions</wa-menu-label>
  <wa-menu-item>
    <wa-icon slot="start" name="file-plus"></wa-icon>
    New Document
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder-plus"></wa-icon>
    New Folder
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-label>Settings</wa-menu-label>
  <wa-menu-item>
    <wa-icon slot="start" name="settings"></wa-icon>
    Preferences
  </wa-menu-item>
</wa-menu>
```

## Scrollable Menu

For long menus, add scrolling:

```html
<wa-menu style="max-height: 300px; overflow-y: auto;">
  <wa-menu-item>Item 1</wa-menu-item>
  <wa-menu-item>Item 2</wa-menu-item>
  <wa-menu-item>Item 3</wa-menu-item>
  <wa-menu-item>Item 4</wa-menu-item>
  <wa-menu-item>Item 5</wa-menu-item>
  <wa-menu-item>Item 6</wa-menu-item>
  <wa-menu-item>Item 7</wa-menu-item>
  <wa-menu-item>Item 8</wa-menu-item>
  <wa-menu-item>Item 9</wa-menu-item>
  <wa-menu-item>Item 10</wa-menu-item>
</wa-menu>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| None | - | - | - | Menu component has no specific attributes |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-select` | Emitted when a menu item is selected | `{ item: HTMLElement }` |

### Event Examples

```javascript
const menu = document.querySelector('wa-menu');

// Handle menu item selection
menu.addEventListener('wa-select', (event) => {
  const item = event.detail.item;
  console.log('Selected item:', item);
  console.log('Item value:', item.value);
  console.log('Item text:', item.textContent);
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Menu items, labels, and dividers |

## Examples

### Settings Menu

```html
<wa-menu style="max-width: 300px;">
  <wa-menu-label>Appearance</wa-menu-label>
  <wa-menu-item type="checkbox" checked>
    <wa-icon slot="start" name="sun"></wa-icon>
    Light Mode
  </wa-menu-item>
  <wa-menu-item type="checkbox">
    <wa-icon slot="start" name="moon"></wa-icon>
    Dark Mode
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-label>Notifications</wa-menu-label>
  <wa-menu-item type="checkbox" checked>
    <wa-icon slot="start" name="bell"></wa-icon>
    Email Notifications
  </wa-menu-item>
  <wa-menu-item type="checkbox" checked>
    <wa-icon slot="start" name="message-square"></wa-icon>
    Push Notifications
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-label>Privacy</wa-menu-label>
  <wa-menu-item>
    <wa-icon slot="start" name="lock"></wa-icon>
    Change Password
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="shield"></wa-icon>
    Privacy Settings
  </wa-menu-item>
</wa-menu>
```

### File Browser Menu

```html
<wa-menu style="max-width: 300px;">
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    Documents
    <wa-badge slot="end" variant="neutral" pill>24</wa-badge>
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    Images
    <wa-badge slot="end" variant="neutral" pill>156</wa-badge>
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    Videos
    <wa-badge slot="end" variant="neutral" pill>8</wa-badge>
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    Music
    <wa-badge slot="end" variant="neutral" pill>42</wa-badge>
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-item>
    <wa-icon slot="start" name="trash"></wa-icon>
    Trash
    <wa-badge slot="end" variant="warning" pill>3</wa-badge>
  </wa-menu-item>
</wa-menu>
```

## CSS Parts

Use CSS parts to style internal menu elements:

```css
/* Style the menu container */
wa-menu::part(base) {
  background-color: var(--wa-color-neutral-50);
  border-radius: 8px;
  padding: 0.5rem;
}
```

## Customization

### Custom Menu Styling

```css
/* Custom menu appearance */
wa-menu {
  background: linear-gradient(to bottom, #ffffff, #f8f9fa);
  border: 1px solid var(--wa-color-neutral-200);
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 0.5rem;
}

/* Custom menu item spacing */
wa-menu wa-menu-item {
  margin-bottom: 0.25rem;
}

wa-menu wa-menu-item:last-child {
  margin-bottom: 0;
}
```

### Compact Menu

```css
/* Compact menu style */
wa-menu.compact {
  padding: 0.25rem;
}

wa-menu.compact wa-menu-item::part(base) {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
}
```

## Best Practices

- Use clear, descriptive labels for menu items
- Group related items with labels and dividers
- Add icons for better visual scanning
- Keep menu items concise
- Use disabled state for unavailable actions
- Limit menu length (use scrolling for long lists)
- Place most common actions at the top
- Use consistent icon style throughout the menu

## Accessibility

- Menu automatically manages keyboard navigation
- Use Up/Down arrow keys to navigate items
- Press Enter or Space to select an item
- Home key jumps to first item
- End key jumps to last item
- Type to search and highlight matching items
- Screen readers announce menu items and their state
- Disabled items are skipped in keyboard navigation

```html
<!-- Good: menu with descriptive items -->
<wa-menu>
  <wa-menu-item>
    <wa-icon slot="start" name="save"></wa-icon>
    Save Document
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="download"></wa-icon>
    Download as PDF
  </wa-menu-item>
</wa-menu>
```

## Troubleshooting

### Menu Items Not Clickable

**Problem:** Menu items don't respond to clicks

**Solution:** Ensure menu items are not disabled and are properly nested

```html
<!-- Correct structure -->
<wa-menu>
  <wa-menu-item>Clickable Item</wa-menu-item>
</wa-menu>
```

### Menu Selection Not Working

**Problem:** `wa-select` event not firing

**Solution:** Listen on the menu element, not individual items

```javascript
// Correct
menu.addEventListener('wa-select', (event) => {
  console.log('Selected:', event.detail.item);
});

// Incorrect - don't listen on individual items
```

## Related

- [Menu Item](./menu-item.md)
- [Menu Label](./menu-label.md)
- [Dropdown](./dropdown.md)
- [Divider](./divider.md)
