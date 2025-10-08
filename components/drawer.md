# Drawer

Drawers provide a panel that slides in from the edge of the screen to display additional content.

## Overview

The `<wa-drawer>` component creates a slide-out panel that can be positioned on any side of the viewport. It's useful for navigation menus, filters, settings panels, and other contextual content that doesn't need to be visible at all times.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/drawer/drawer.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-button id="openDrawer">Open Drawer</wa-button>

<wa-drawer label="Drawer" id="drawer">
  <p>This is drawer content.</p>
</wa-drawer>

<script>
  const drawer = document.getElementById('drawer');
  const openBtn = document.getElementById('openDrawer');

  openBtn.addEventListener('click', () => drawer.show());
</script>
```

## Placements

Control drawer position with the `placement` attribute:

```html
<!-- Start (left in LTR) -->
<wa-button id="openStart">Open Start</wa-button>
<wa-drawer label="Start Drawer" id="startDrawer" placement="start">
  <p>Drawer from the start side</p>
</wa-drawer>

<!-- End (right in LTR) -->
<wa-button id="openEnd">Open End</wa-button>
<wa-drawer label="End Drawer" id="endDrawer" placement="end">
  <p>Drawer from the end side</p>
</wa-drawer>

<!-- Top -->
<wa-button id="openTop">Open Top</wa-button>
<wa-drawer label="Top Drawer" id="topDrawer" placement="top">
  <p>Drawer from the top</p>
</wa-drawer>

<!-- Bottom -->
<wa-button id="openBottom">Open Bottom</wa-button>
<wa-drawer label="Bottom Drawer" id="bottomDrawer" placement="bottom">
  <p>Drawer from the bottom</p>
</wa-drawer>

<script>
  document.getElementById('openStart').addEventListener('click', () => {
    document.getElementById('startDrawer').show();
  });

  document.getElementById('openEnd').addEventListener('click', () => {
    document.getElementById('endDrawer').show();
  });

  document.getElementById('openTop').addEventListener('click', () => {
    document.getElementById('topDrawer').show();
  });

  document.getElementById('openBottom').addEventListener('click', () => {
    document.getElementById('bottomDrawer').show();
  });
</script>
```

## Contained Drawers

Use the `contained` attribute to keep drawers within a specific container:

```html
<style>
  .drawer-container {
    position: relative;
    border: 2px solid #ccc;
    height: 400px;
    padding: 1rem;
    overflow: hidden;
  }
</style>

<div class="drawer-container">
  <wa-button id="openContained">Open Contained Drawer</wa-button>

  <wa-drawer label="Contained Drawer" id="containedDrawer" contained>
    <p>This drawer is contained within its parent element.</p>
  </wa-drawer>
</div>

<script>
  const containedDrawer = document.getElementById('containedDrawer');
  const openContained = document.getElementById('openContained');

  openContained.addEventListener('click', () => containedDrawer.show());
</script>
```

## No Header

Remove the header by omitting the `label` attribute:

```html
<wa-button id="openNoHeader">Open Drawer</wa-button>

<wa-drawer id="noHeaderDrawer">
  <div style="padding: 1rem;">
    <h2>Custom Header</h2>
    <p>This drawer has no default header.</p>
    <wa-button id="closeCustom">Close</wa-button>
  </div>
</wa-drawer>

<script>
  const noHeaderDrawer = document.getElementById('noHeaderDrawer');
  const openNoHeader = document.getElementById('openNoHeader');
  const closeCustom = document.getElementById('closeCustom');

  openNoHeader.addEventListener('click', () => noHeaderDrawer.show());
  closeCustom.addEventListener('click', () => noHeaderDrawer.hide());
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `open` | boolean | `false` | No | Show or hide the drawer |
| `label` | string | - | No | The drawer label (shown in header) |
| `placement` | string | `'end'` | No | Drawer position: `start`, `end`, `top`, `bottom` |
| `contained` | boolean | `false` | No | Keep drawer within its container instead of viewport |
| `no-header` | boolean | `false` | No | Hide the header (including close button) |

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show()` | Shows the drawer | `Promise<void>` |
| `hide()` | Hides the drawer | `Promise<void>` |

### Method Examples

```javascript
const drawer = document.querySelector('wa-drawer');

// Show the drawer
await drawer.show();

// Hide the drawer
await drawer.hide();

// Check if drawer is open
if (drawer.open) {
  console.log('Drawer is open');
}
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-show` | Emitted when the drawer starts to open | - |
| `wa-after-show` | Emitted after the drawer has finished opening and animations are complete | - |
| `wa-hide` | Emitted when the drawer starts to close | - |
| `wa-after-hide` | Emitted after the drawer has finished closing and animations are complete | - |
| `wa-request-close` | Emitted when the user attempts to close the drawer (clicking overlay, close button, or ESC key). Can be cancelled to prevent closing. | `{ source: 'close-button' | 'keyboard' | 'overlay' }` |

### Event Examples

```javascript
const drawer = document.querySelector('wa-drawer');

drawer.addEventListener('wa-show', () => {
  console.log('Drawer is opening');
});

drawer.addEventListener('wa-after-show', () => {
  console.log('Drawer is now open');
});

drawer.addEventListener('wa-hide', () => {
  console.log('Drawer is closing');
});

drawer.addEventListener('wa-after-hide', () => {
  console.log('Drawer is now closed');
});

// Prevent closing under certain conditions
drawer.addEventListener('wa-request-close', (event) => {
  const hasUnsavedChanges = true; // Your condition

  if (hasUnsavedChanges) {
    event.preventDefault();

    if (confirm('You have unsaved changes. Are you sure you want to close?')) {
      drawer.hide();
    }
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The drawer's main content |
| `label` | The drawer's label (alternative to label attribute) |
| `header-actions` | Optional actions to add to the header |
| `footer` | The drawer's footer |

## Examples

### Navigation Drawer

```html
<wa-button id="openNav">
  <wa-icon slot="start" name="bars"></wa-icon>
  Menu
</wa-button>

<wa-drawer label="Navigation" id="navDrawer" placement="start">
  <nav style="padding: 1rem;">
    <div style="display: flex; flex-direction: column; gap: 0.5rem;">
      <wa-button variant="text" style="justify-content: flex-start;">
        <wa-icon slot="start" name="house"></wa-icon>
        Home
      </wa-button>
      <wa-button variant="text" style="justify-content: flex-start;">
        <wa-icon slot="start" name="user"></wa-icon>
        Profile
      </wa-button>
      <wa-button variant="text" style="justify-content: flex-start;">
        <wa-icon slot="start" name="gear"></wa-icon>
        Settings
      </wa-button>
      <wa-button variant="text" style="justify-content: flex-start;">
        <wa-icon slot="start" name="circle-info"></wa-icon>
        About
      </wa-button>
    </div>
  </nav>
</wa-drawer>

<script>
  const navDrawer = document.getElementById('navDrawer');
  const openNav = document.getElementById('openNav');

  openNav.addEventListener('click', () => navDrawer.show());

  // Close drawer when navigation items are clicked
  navDrawer.querySelectorAll('wa-button').forEach(button => {
    button.addEventListener('click', () => navDrawer.hide());
  });
</script>
```

### Filter Drawer

```html
<wa-button id="openFilters">
  <wa-icon slot="start" name="filter"></wa-icon>
  Filters
</wa-button>

<wa-drawer label="Filters" id="filterDrawer" placement="end">
  <div style="padding: 1rem; display: flex; flex-direction: column; gap: 1rem;">
    <div>
      <label>Category</label>
      <wa-select>
        <wa-option value="all">All Categories</wa-option>
        <wa-option value="electronics">Electronics</wa-option>
        <wa-option value="clothing">Clothing</wa-option>
        <wa-option value="books">Books</wa-option>
      </wa-select>
    </div>

    <div>
      <label>Price Range</label>
      <wa-range min="0" max="1000" step="10"></wa-range>
    </div>

    <div>
      <label>Brand</label>
      <wa-checkbox>Brand A</wa-checkbox>
      <wa-checkbox>Brand B</wa-checkbox>
      <wa-checkbox>Brand C</wa-checkbox>
    </div>
  </div>

  <div slot="footer" style="display: flex; gap: 0.5rem; padding: 1rem;">
    <wa-button variant="primary" style="flex: 1;" id="applyFilters">Apply</wa-button>
    <wa-button style="flex: 1;" id="resetFilters">Reset</wa-button>
  </div>
</wa-drawer>

<script>
  const filterDrawer = document.getElementById('filterDrawer');
  const openFilters = document.getElementById('openFilters');
  const applyFilters = document.getElementById('applyFilters');
  const resetFilters = document.getElementById('resetFilters');

  openFilters.addEventListener('click', () => filterDrawer.show());

  applyFilters.addEventListener('click', () => {
    // Apply filters logic
    filterDrawer.hide();
  });

  resetFilters.addEventListener('click', () => {
    // Reset filters logic
  });
</script>
```

### Settings Drawer

```html
<wa-button id="openSettings">
  <wa-icon name="gear"></wa-icon>
</wa-button>

<wa-drawer label="Settings" id="settingsDrawer">
  <div style="padding: 1rem; display: flex; flex-direction: column; gap: 1.5rem;">
    <div>
      <h3>Account</h3>
      <wa-switch>Email notifications</wa-switch>
      <wa-switch>Push notifications</wa-switch>
      <wa-switch>SMS alerts</wa-switch>
    </div>

    <wa-divider></wa-divider>

    <div>
      <h3>Appearance</h3>
      <label>Theme</label>
      <wa-radio-group>
        <wa-radio value="light">Light</wa-radio>
        <wa-radio value="dark">Dark</wa-radio>
        <wa-radio value="auto">Auto</wa-radio>
      </wa-radio-group>
    </div>

    <wa-divider></wa-divider>

    <div>
      <h3>Privacy</h3>
      <wa-switch>Profile visibility</wa-switch>
      <wa-switch>Show activity status</wa-switch>
    </div>
  </div>

  <div slot="footer" style="padding: 1rem;">
    <wa-button variant="primary" style="width: 100%;" id="saveSettings">
      Save Changes
    </wa-button>
  </div>
</wa-drawer>

<script>
  const settingsDrawer = document.getElementById('settingsDrawer');
  const openSettings = document.getElementById('openSettings');
  const saveSettings = document.getElementById('saveSettings');

  openSettings.addEventListener('click', () => settingsDrawer.show());

  saveSettings.addEventListener('click', () => {
    // Save settings logic
    settingsDrawer.hide();
  });
</script>
```

### Scrollable Content

```html
<wa-button id="openScrollable">Open Scrollable Drawer</wa-button>

<wa-drawer label="Long Content" id="scrollableDrawer">
  <div style="padding: 1rem;">
    <p>This drawer has a lot of content that will scroll.</p>

    <h3>Section 1</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>

    <h3>Section 2</h3>
    <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>

    <h3>Section 3</h3>
    <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.</p>

    <h3>Section 4</h3>
    <p>Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

    <!-- More sections... -->
  </div>

  <div slot="footer" style="padding: 1rem; border-top: 1px solid #e0e0e0;">
    <wa-button variant="primary" style="width: 100%;">Action</wa-button>
  </div>
</wa-drawer>

<script>
  const scrollableDrawer = document.getElementById('scrollableDrawer');
  const openScrollable = document.getElementById('openScrollable');

  openScrollable.addEventListener('click', () => scrollableDrawer.show());
</script>
```

### Custom Header

```html
<wa-button id="openCustomHeader">Open Custom Header</wa-button>

<wa-drawer id="customHeaderDrawer">
  <div slot="label" style="display: flex; align-items: center; gap: 0.5rem;">
    <wa-icon name="star" style="color: gold;"></wa-icon>
    <span>Premium Features</span>
  </div>

  <div slot="header-actions">
    <wa-icon-button name="ellipsis-vertical"></wa-icon-button>
  </div>

  <div style="padding: 1rem;">
    <p>Custom header with icon and actions.</p>
  </div>
</wa-drawer>

<script>
  const customHeaderDrawer = document.getElementById('customHeaderDrawer');
  const openCustomHeader = document.getElementById('openCustomHeader');

  openCustomHeader.addEventListener('click', () => customHeaderDrawer.show());
</script>
```

### Confirmation Dialog

```html
<wa-button id="openConfirmation">Delete Item</wa-button>

<wa-drawer label="Confirm Deletion" id="confirmDrawer" placement="bottom">
  <div style="padding: 1rem;">
    <p>Are you sure you want to delete this item? This action cannot be undone.</p>
  </div>

  <div slot="footer" style="display: flex; gap: 0.5rem; padding: 1rem;">
    <wa-button style="flex: 1;" id="cancelDelete">Cancel</wa-button>
    <wa-button variant="danger" style="flex: 1;" id="confirmDelete">Delete</wa-button>
  </div>
</wa-drawer>

<script>
  const confirmDrawer = document.getElementById('confirmDrawer');
  const openConfirmation = document.getElementById('openConfirmation');
  const cancelDelete = document.getElementById('cancelDelete');
  const confirmDelete = document.getElementById('confirmDelete');

  openConfirmation.addEventListener('click', () => confirmDrawer.show());
  cancelDelete.addEventListener('click', () => confirmDrawer.hide());

  confirmDelete.addEventListener('click', () => {
    // Perform delete action
    console.log('Item deleted');
    confirmDrawer.hide();
  });
</script>
```

## CSS Parts

Use CSS parts to style internal drawer elements:

```css
/* Style the drawer panel */
wa-drawer::part(panel) {
  background-color: #f5f5f5;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
}

/* Style the overlay */
wa-drawer::part(overlay) {
  background-color: rgba(0, 0, 0, 0.6);
}

/* Style the header */
wa-drawer::part(header) {
  background-color: #0066cc;
  color: white;
  padding: 1.5rem;
}

/* Style the body */
wa-drawer::part(body) {
  padding: 0;
}

/* Style the footer */
wa-drawer::part(footer) {
  background-color: #f5f5f5;
  border-top: 1px solid #e0e0e0;
}

/* Style the close button */
wa-drawer::part(close-button) {
  color: white;
}
```

## Customization

### Custom Width/Height

```css
/* Custom drawer width for start/end placements */
wa-drawer[placement="start"]::part(panel),
wa-drawer[placement="end"]::part(panel) {
  width: 400px;
}

/* Custom drawer height for top/bottom placements */
wa-drawer[placement="top"]::part(panel),
wa-drawer[placement="bottom"]::part(panel) {
  height: 300px;
}

/* Responsive drawer width */
@media (max-width: 768px) {
  wa-drawer::part(panel) {
    width: 100%;
  }
}
```

### Custom Animation

```css
/* Custom slide animation */
wa-drawer::part(panel) {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
```

## Best Practices

- ✅ Use drawers for contextual content that doesn't need constant visibility
- ✅ Provide clear close mechanisms (close button, overlay click, ESC key)
- ✅ Keep drawer content focused and organized
- ✅ Use appropriate placement based on content type (navigation from start, filters from end)
- ✅ Include a footer for primary actions when needed
- ❌ Don't nest drawers inside other drawers
- ❌ Avoid opening multiple drawers simultaneously
- ❌ Don't use drawers for critical workflows that require constant reference
- ❌ Avoid making drawers too wide (300-500px recommended)

## Accessibility

- Drawers automatically include appropriate ARIA attributes
- Focus is trapped within the drawer when open
- ESC key closes the drawer by default
- Screen readers announce drawer opening/closing
- Close button includes proper ARIA label

```html
<!-- Accessible drawer -->
<wa-drawer label="Accessible Drawer" id="accessibleDrawer">
  <p>This drawer is fully accessible.</p>

  <wa-button>Focusable Element 1</wa-button>
  <wa-button>Focusable Element 2</wa-button>
  <wa-input label="Input Field"></wa-input>
</wa-drawer>
```

- Ensure logical focus order within drawer content
- Provide meaningful labels for all interactive elements
- Consider keyboard navigation for all actions

## Troubleshooting

### Drawer Not Opening

**Problem:** Drawer doesn't appear when show() is called

**Solution:** Ensure drawer element is in the DOM and check console for errors

```javascript
const drawer = document.querySelector('wa-drawer');

if (drawer) {
  await drawer.show();
} else {
  console.error('Drawer element not found');
}
```

### Content Overflow

**Problem:** Content doesn't scroll properly

**Solution:** Ensure body content has proper styling

```css
wa-drawer::part(body) {
  overflow-y: auto;
  max-height: calc(100vh - 120px); /* Adjust based on header/footer */
}
```

### Drawer Width Issues

**Problem:** Drawer is too wide or narrow

**Solution:** Set custom width using CSS parts

```css
wa-drawer::part(panel) {
  width: 350px;
}

@media (max-width: 768px) {
  wa-drawer::part(panel) {
    width: 90vw;
  }
}
```

### Overlay Not Blocking Interaction

**Problem:** Can interact with page content when drawer is open

**Solution:** Ensure overlay is properly configured (this is default behavior)

```javascript
// Verify drawer is not contained
const drawer = document.querySelector('wa-drawer');
console.log('Contained:', drawer.contained); // Should be false for full overlay
```

## Related

- [Dialog](./dialog.md)
- [Dropdown](./dropdown.md)
- [Navigation Patterns Guide](../guides/navigation-patterns.md)
- [Modal Guide](../guides/modals.md)
