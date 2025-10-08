# Menu Item

Menu items represent individual selectable options within a menu.

## Overview

The `<wa-menu-item>` component is used inside `<wa-menu>` to create selectable options. It supports icons, checkboxes, radio buttons, submenus, and various states.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/menu-item/menu-item.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-menu>
  <wa-menu-item>Simple Item</wa-menu-item>
  <wa-menu-item>Another Item</wa-menu-item>
  <wa-menu-item>Third Item</wa-menu-item>
</wa-menu>
```

## With Values

Assign values to items for easier handling:

```html
<wa-menu id="myMenu">
  <wa-menu-item value="new">New File</wa-menu-item>
  <wa-menu-item value="open">Open File</wa-menu-item>
  <wa-menu-item value="save">Save File</wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('myMenu');

  menu.addEventListener('wa-select', (event) => {
    const value = event.detail.item.value;
    console.log('Selected:', value);
  });
</script>
```

## With Icons

Use slots to add icons before or after the label:

```html
<wa-menu>
  <!-- Icon at start -->
  <wa-menu-item>
    <wa-icon slot="start" name="download"></wa-icon>
    Download
  </wa-menu-item>

  <!-- Icon at end -->
  <wa-menu-item>
    Open in New Tab
    <wa-icon slot="end" name="external-link"></wa-icon>
  </wa-menu-item>

  <!-- Icons on both sides -->
  <wa-menu-item>
    <wa-icon slot="start" name="file"></wa-icon>
    Document
    <wa-badge slot="end" variant="primary" pill>New</wa-badge>
  </wa-menu-item>
</wa-menu>
```

## Disabled State

Disable items that are temporarily unavailable:

```html
<wa-menu>
  <wa-menu-item>Active Item</wa-menu-item>
  <wa-menu-item disabled>Disabled Item</wa-menu-item>
  <wa-menu-item>Another Active Item</wa-menu-item>
</wa-menu>
```

## Checkable Items

Create checkbox-style menu items:

```html
<wa-menu id="viewMenu">
  <wa-menu-item type="checkbox" checked>
    <wa-icon slot="start" name="sidebar"></wa-icon>
    Show Sidebar
  </wa-menu-item>
  <wa-menu-item type="checkbox" checked>
    <wa-icon slot="start" name="terminal"></wa-icon>
    Show Terminal
  </wa-menu-item>
  <wa-menu-item type="checkbox">
    <wa-icon slot="start" name="eye"></wa-icon>
    Show Hidden Files
  </wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('viewMenu');

  menu.addEventListener('wa-select', (event) => {
    const item = event.detail.item;
    console.log(`${item.textContent.trim()}: ${item.checked}`);
  });
</script>
```

## Radio Groups

Create mutually exclusive options with radio items:

```html
<wa-menu id="themeMenu">
  <wa-menu-label>Select Theme</wa-menu-label>
  <wa-menu-item type="checkbox" value="light" checked>
    <wa-icon slot="start" name="sun"></wa-icon>
    Light Theme
  </wa-menu-item>
  <wa-menu-item type="checkbox" value="dark">
    <wa-icon slot="start" name="moon"></wa-icon>
    Dark Theme
  </wa-menu-item>
  <wa-menu-item type="checkbox" value="auto">
    <wa-icon slot="start" name="monitor"></wa-icon>
    Auto Theme
  </wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('themeMenu');

  menu.addEventListener('wa-select', (event) => {
    const selectedItem = event.detail.item;

    // Uncheck all items in the group
    menu.querySelectorAll('wa-menu-item[type="checkbox"]').forEach(item => {
      item.checked = false;
    });

    // Check the selected item
    selectedItem.checked = true;

    console.log('Theme changed to:', selectedItem.value);
  });
</script>
```

## With Submenu

Create nested menus with the submenu slot:

```html
<wa-menu>
  <wa-menu-item>Home</wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="folder"></wa-icon>
    Products
    <wa-menu slot="submenu">
      <wa-menu-item>Electronics</wa-menu-item>
      <wa-menu-item>Clothing</wa-menu-item>
      <wa-menu-item>Books</wa-menu-item>
    </wa-menu>
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="start" name="settings"></wa-icon>
    Settings
    <wa-menu slot="submenu">
      <wa-menu-item>General</wa-menu-item>
      <wa-menu-item>Privacy</wa-menu-item>
      <wa-menu-item>Security</wa-menu-item>
    </wa-menu>
  </wa-menu-item>
</wa-menu>
```

## With Keyboard Shortcuts

Display keyboard shortcuts as visual hints:

```html
<wa-menu>
  <wa-menu-item value="save">
    <wa-icon slot="start" name="save"></wa-icon>
    Save
    <span slot="end" style="color: var(--wa-color-neutral-500); font-size: 0.875rem;">Ctrl+S</span>
  </wa-menu-item>
  <wa-menu-item value="copy">
    <wa-icon slot="start" name="copy"></wa-icon>
    Copy
    <span slot="end" style="color: var(--wa-color-neutral-500); font-size: 0.875rem;">Ctrl+C</span>
  </wa-menu-item>
  <wa-menu-item value="paste">
    <wa-icon slot="start" name="clipboard"></wa-icon>
    Paste
    <span slot="end" style="color: var(--wa-color-neutral-500); font-size: 0.875rem;">Ctrl+V</span>
  </wa-menu-item>
</wa-menu>
```

## With Loading State

Show loading state for async actions:

```html
<wa-menu id="loadingMenu">
  <wa-menu-item id="loadItem" value="load">
    <wa-icon slot="start" name="download"></wa-icon>
    Load Data
  </wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('loadingMenu');
  const loadItem = document.getElementById('loadItem');

  menu.addEventListener('wa-select', async (event) => {
    if (event.detail.item.value === 'load') {
      // Show loading state
      const icon = loadItem.querySelector('wa-icon');
      icon.name = 'loader';
      loadItem.disabled = true;

      try {
        await fetch('/api/data');
        // Handle success
      } finally {
        // Reset state
        icon.name = 'download';
        loadItem.disabled = false;
      }
    }
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | - | No | Value associated with the menu item |
| `disabled` | boolean | `false` | No | Disable the menu item |
| `checked` | boolean | `false` | No | Checked state (for checkbox type) |
| `type` | string | - | No | Menu item type: `checkbox` for checkable items |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| (Bubbles to menu) | Selection events bubble to the parent menu | - |

### Event Examples

```javascript
// Listen on the parent menu
const menu = document.querySelector('wa-menu');

menu.addEventListener('wa-select', (event) => {
  const item = event.detail.item;
  console.log('Selected item:', item);
  console.log('Value:', item.value);
  console.log('Checked:', item.checked);
  console.log('Disabled:', item.disabled);
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The menu item label |
| `start` | Content before the label (typically icons) |
| `end` | Content after the label (typically badges or shortcuts) |
| `submenu` | A nested menu for hierarchical navigation |

## Examples

### File Operations Menu

```html
<wa-menu>
  <wa-menu-item value="new">
    <wa-icon slot="start" name="file-plus"></wa-icon>
    New File
    <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+N</span>
  </wa-menu-item>
  <wa-menu-item value="open">
    <wa-icon slot="start" name="folder-open"></wa-icon>
    Open File
    <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+O</span>
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-item value="save">
    <wa-icon slot="start" name="save"></wa-icon>
    Save
    <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+S</span>
  </wa-menu-item>
  <wa-menu-item value="save-as">
    <wa-icon slot="start" name="save"></wa-icon>
    Save As...
    <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+Shift+S</span>
  </wa-menu-item>

  <wa-divider></wa-divider>

  <wa-menu-item value="close" disabled>
    <wa-icon slot="start" name="x"></wa-icon>
    Close
    <span slot="end" style="color: var(--wa-color-neutral-500);">Ctrl+W</span>
  </wa-menu-item>
</wa-menu>
```

### User Status Menu

```html
<wa-menu id="statusMenu">
  <wa-menu-item type="checkbox" value="online" checked>
    <div slot="start" style="width: 8px; height: 8px; border-radius: 50%; background: var(--wa-color-success-600);"></div>
    Online
  </wa-menu-item>
  <wa-menu-item type="checkbox" value="away">
    <div slot="start" style="width: 8px; height: 8px; border-radius: 50%; background: var(--wa-color-warning-600);"></div>
    Away
  </wa-menu-item>
  <wa-menu-item type="checkbox" value="busy">
    <div slot="start" style="width: 8px; height: 8px; border-radius: 50%; background: var(--wa-color-danger-600);"></div>
    Busy
  </wa-menu-item>
  <wa-menu-item type="checkbox" value="offline">
    <div slot="start" style="width: 8px; height: 8px; border-radius: 50%; background: var(--wa-color-neutral-400);"></div>
    Offline
  </wa-menu-item>
</wa-menu>

<script>
  const menu = document.getElementById('statusMenu');

  menu.addEventListener('wa-select', (event) => {
    const selectedItem = event.detail.item;

    // Radio button behavior
    menu.querySelectorAll('wa-menu-item').forEach(item => {
      item.checked = false;
    });
    selectedItem.checked = true;

    console.log('Status changed to:', selectedItem.value);
  });
</script>
```

### Multi-Select Menu

```html
<wa-dropdown stay-open-on-select>
  <wa-button slot="trigger" caret>
    <wa-icon slot="start" name="filter"></wa-icon>
    Filter Options
  </wa-button>
  <wa-menu id="filterMenu">
    <wa-menu-item type="checkbox" value="active" checked>
      Show Active
    </wa-menu-item>
    <wa-menu-item type="checkbox" value="pending" checked>
      Show Pending
    </wa-menu-item>
    <wa-menu-item type="checkbox" value="completed">
      Show Completed
    </wa-menu-item>
    <wa-menu-item type="checkbox" value="archived">
      Show Archived
    </wa-menu-item>
  </wa-menu>
</wa-dropdown>

<script>
  const menu = document.getElementById('filterMenu');

  menu.addEventListener('wa-select', (event) => {
    const item = event.detail.item;
    console.log(`Filter ${item.value}: ${item.checked ? 'enabled' : 'disabled'}`);

    // Apply filters
    updateFilters();
  });

  function updateFilters() {
    const activeFilters = Array.from(menu.querySelectorAll('wa-menu-item[checked]'))
      .map(item => item.value);
    console.log('Active filters:', activeFilters);
  }
</script>
```

### Nested Menu Example

```html
<wa-menu>
  <wa-menu-item>
    <wa-icon slot="start" name="file"></wa-icon>
    New
    <wa-menu slot="submenu">
      <wa-menu-item value="new-file">
        <wa-icon slot="start" name="file-text"></wa-icon>
        Text File
      </wa-menu-item>
      <wa-menu-item value="new-folder">
        <wa-icon slot="start" name="folder"></wa-icon>
        Folder
      </wa-menu-item>
      <wa-menu-item>
        <wa-icon slot="start" name="code"></wa-icon>
        From Template
        <wa-menu slot="submenu">
          <wa-menu-item value="template-react">React App</wa-menu-item>
          <wa-menu-item value="template-vue">Vue App</wa-menu-item>
          <wa-menu-item value="template-angular">Angular App</wa-menu-item>
        </wa-menu>
      </wa-menu-item>
    </wa-menu>
  </wa-menu-item>

  <wa-menu-item>
    <wa-icon slot="start" name="folder-open"></wa-icon>
    Open
  </wa-menu-item>
</wa-menu>
```

## CSS Parts

Use CSS parts to style internal menu item elements:

```css
/* Style the menu item base */
wa-menu-item::part(base) {
  border-radius: 4px;
  padding: 0.5rem 1rem;
}

/* Style hovered items */
wa-menu-item::part(base):hover {
  background-color: var(--wa-color-primary-50);
}

/* Style the label */
wa-menu-item::part(label) {
  font-weight: 500;
}

/* Style the start slot container */
wa-menu-item::part(start) {
  margin-right: 0.75rem;
}

/* Style the end slot container */
wa-menu-item::part(end) {
  margin-left: auto;
  padding-left: 1rem;
}

/* Style checked items */
wa-menu-item[checked]::part(base) {
  background-color: var(--wa-color-primary-50);
  color: var(--wa-color-primary-700);
}

/* Style disabled items */
wa-menu-item[disabled]::part(base) {
  opacity: 0.5;
  cursor: not-allowed;
}
```

## Customization

### Custom Menu Item Colors

```css
/* Danger item style */
wa-menu-item.danger::part(base) {
  color: var(--wa-color-danger-600);
}

wa-menu-item.danger::part(base):hover {
  background-color: var(--wa-color-danger-50);
}

/* Success item style */
wa-menu-item.success::part(base) {
  color: var(--wa-color-success-600);
}

wa-menu-item.success::part(base):hover {
  background-color: var(--wa-color-success-50);
}
```

### Compact Menu Items

```css
/* Compact item style */
wa-menu-item.compact::part(base) {
  padding: 0.25rem 0.75rem;
  font-size: 0.875rem;
}
```

## Best Practices

- Use clear, action-oriented labels
- Add icons for better visual recognition
- Group related items with dividers
- Show keyboard shortcuts for common actions
- Use disabled state appropriately
- Provide feedback for async actions
- Keep submenu depth shallow (2-3 levels max)
- Use values for programmatic handling
- Use checkboxes for multi-select scenarios
- Implement radio behavior when only one option should be selected

## Accessibility

- Menu items automatically handle keyboard navigation
- Press Enter or Space to select an item
- Screen readers announce item state (checked, disabled)
- Disabled items are skipped in keyboard navigation
- Checkable items announce their checked state
- Ensure sufficient color contrast for text
- Use descriptive labels

```html
<!-- Good: descriptive label -->
<wa-menu-item>
  <wa-icon slot="start" name="download"></wa-icon>
  Download Report
</wa-menu-item>

<!-- Good: with keyboard shortcut -->
<wa-menu-item>
  <wa-icon slot="start" name="save"></wa-icon>
  Save Document
  <span slot="end" aria-label="Keyboard shortcut Control S">Ctrl+S</span>
</wa-menu-item>
```

## Troubleshooting

### Menu Item Not Clickable

**Problem:** Menu item doesn't respond to clicks

**Solution:** Check if item is disabled

```javascript
const item = document.querySelector('wa-menu-item');
item.disabled = false;
```

### Checkbox State Not Updating

**Problem:** Checked state doesn't change on click

**Solution:** Ensure you're updating the checked property

```javascript
menu.addEventListener('wa-select', (event) => {
  const item = event.detail.item;
  if (item.type === 'checkbox') {
    item.checked = !item.checked; // Toggle state
  }
});
```

### Submenu Not Showing

**Problem:** Submenu doesn't appear on hover

**Solution:** Ensure submenu is using the correct slot

```html
<!-- Correct -->
<wa-menu-item>
  Products
  <wa-menu slot="submenu">
    <wa-menu-item>Item 1</wa-menu-item>
  </wa-menu>
</wa-menu-item>
```

## Related

- [Menu](./menu.md)
- [Menu Label](./menu-label.md)
- [Dropdown](./dropdown.md)
- [Divider](./divider.md)
- [Icon](./icon.md)
