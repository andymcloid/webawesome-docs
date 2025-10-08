# Tree

A hierarchical tree structure for displaying nested data and navigation.

## Overview

The `<wa-tree>` component creates an accessible, interactive tree structure for displaying hierarchical data. It supports single and multi-selection modes, lazy loading, and fully customizable tree items. Use with `<wa-tree-item>` elements to build the tree hierarchy.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tree/tree.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple tree structure -->
<wa-tree>
  <wa-tree-item>
    Documents
    <wa-tree-item>Work Files</wa-tree-item>
    <wa-tree-item>Personal</wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    Pictures
    <wa-tree-item>Vacation 2024</wa-tree-item>
    <wa-tree-item>Family</wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>Downloads</wa-tree-item>
</wa-tree>

<!-- Tree with icons -->
<wa-tree>
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Projects
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      project1.js
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      project2.js
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

## Selection Modes

Control how items can be selected:

```html
<!-- Single selection (default) -->
<wa-tree selection="single">
  <wa-tree-item>Item 1</wa-tree-item>
  <wa-tree-item>Item 2</wa-tree-item>
  <wa-tree-item>Item 3</wa-tree-item>
</wa-tree>

<!-- Multiple selection -->
<wa-tree selection="multiple">
  <wa-tree-item>Item 1</wa-tree-item>
  <wa-tree-item>Item 2</wa-tree-item>
  <wa-tree-item>Item 3</wa-tree-item>
</wa-tree>

<!-- Leaf selection only (only leaf nodes can be selected) -->
<wa-tree selection="leaf">
  <wa-tree-item>
    Parent (not selectable)
    <wa-tree-item>Child 1 (selectable)</wa-tree-item>
    <wa-tree-item>Child 2 (selectable)</wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `selection` | string | `'single'` | No | Selection mode: `single`, `multiple`, `leaf`, or `none` |

## Examples

### File Explorer

```html
<wa-tree selection="single" style="max-width: 400px;">
  <wa-tree-item expanded>
    <wa-icon slot="icon" name="folder-open"></wa-icon>
    Documents
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Work
      <wa-tree-item>
        <wa-icon slot="icon" name="file-text"></wa-icon>
        Report.docx
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-text"></wa-icon>
        Presentation.pptx
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-spreadsheet"></wa-icon>
        Budget.xlsx
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Personal
      <wa-tree-item>
        <wa-icon slot="icon" name="file-text"></wa-icon>
        Resume.pdf
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-image"></wa-icon>
        Profile.jpg
      </wa-tree-item>
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Downloads
    <wa-tree-item>
      <wa-icon slot="icon" name="file-zip"></wa-icon>
      archive.zip
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      readme.txt
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Pictures
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Vacation 2024
      <wa-tree-item>
        <wa-icon slot="icon" name="file-image"></wa-icon>
        beach.jpg
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-image"></wa-icon>
        sunset.jpg
      </wa-tree-item>
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

### Organization Chart

```html
<wa-tree selection="single" style="max-width: 500px;">
  <wa-tree-item expanded>
    <wa-avatar slot="icon" label="CEO" initials="JD"></wa-avatar>
    <strong>Jane Doe</strong> - CEO
    <wa-tree-item expanded>
      <wa-avatar slot="icon" label="CTO" initials="MS"></wa-avatar>
      <strong>Mike Smith</strong> - CTO
      <wa-tree-item>
        <wa-avatar slot="icon" label="Lead Developer" initials="SJ"></wa-avatar>
        Sarah Johnson - Lead Developer
        <wa-tree-item>
          <wa-avatar slot="icon" label="Developer" initials="TW"></wa-avatar>
          Tom Wilson - Frontend Developer
        </wa-tree-item>
        <wa-tree-item>
          <wa-avatar slot="icon" label="Developer" initials="EB"></wa-avatar>
          Emily Brown - Backend Developer
        </wa-tree-item>
      </wa-tree-item>
      <wa-tree-item>
        <wa-avatar slot="icon" label="DevOps" initials="DL"></wa-avatar>
        David Lee - DevOps Engineer
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item expanded>
      <wa-avatar slot="icon" label="CFO" initials="LM"></wa-avatar>
      <strong>Lisa Martinez</strong> - CFO
      <wa-tree-item>
        <wa-avatar slot="icon" label="Accountant" initials="RA"></wa-avatar>
        Robert Anderson - Senior Accountant
      </wa-tree-item>
      <wa-tree-item>
        <wa-avatar slot="icon" label="Analyst" initials="JT"></wa-avatar>
        Jennifer Taylor - Financial Analyst
      </wa-tree-item>
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

### Navigation Tree

```html
<wa-tree selection="single" id="navTree" style="max-width: 300px;">
  <wa-tree-item expanded>
    <wa-icon slot="icon" name="home"></wa-icon>
    Dashboard
  </wa-tree-item>
  <wa-tree-item expanded>
    <wa-icon slot="icon" name="users"></wa-icon>
    Users
    <wa-tree-item>
      <wa-icon slot="icon" name="user-plus"></wa-icon>
      Add User
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="list"></wa-icon>
      User List
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="user-check"></wa-icon>
      Permissions
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="shopping-cart"></wa-icon>
    Products
    <wa-tree-item>
      <wa-icon slot="icon" name="package"></wa-icon>
      All Products
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="tag"></wa-icon>
      Categories
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="trending-up"></wa-icon>
      Inventory
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="file-text"></wa-icon>
    Reports
    <wa-tree-item>
      <wa-icon slot="icon" name="bar-chart"></wa-icon>
      Sales Report
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="pie-chart"></wa-icon>
      Analytics
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="settings"></wa-icon>
    Settings
    <wa-tree-item>
      <wa-icon slot="icon" name="user"></wa-icon>
      Profile
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="bell"></wa-icon>
      Notifications
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="shield"></wa-icon>
      Security
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>

<script>
  const navTree = document.getElementById('navTree');

  navTree.addEventListener('wa-select', (event) => {
    const item = event.detail.item;
    console.log('Navigate to:', item.textContent.trim());
    // Handle navigation logic here
  });
</script>
```

### Multiple Selection with Checkboxes

```html
<wa-tree selection="multiple" id="multiTree" style="max-width: 400px;">
  <wa-tree-item>
    Features
    <wa-tree-item>User Authentication</wa-tree-item>
    <wa-tree-item>Database Integration</wa-tree-item>
    <wa-tree-item>API Endpoints</wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    Testing
    <wa-tree-item>Unit Tests</wa-tree-item>
    <wa-tree-item>Integration Tests</wa-tree-item>
    <wa-tree-item>E2E Tests</wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    Documentation
    <wa-tree-item>User Guide</wa-tree-item>
    <wa-tree-item>API Reference</wa-tree-item>
    <wa-tree-item>Changelog</wa-tree-item>
  </wa-tree-item>
</wa-tree>

<div style="margin-top: 1rem;">
  <wa-button id="getSelected">Get Selected Items</wa-button>
  <wa-button id="clearSelection">Clear Selection</wa-button>
</div>

<script>
  const multiTree = document.getElementById('multiTree');
  const getSelectedBtn = document.getElementById('getSelected');
  const clearSelectionBtn = document.getElementById('clearSelection');

  getSelectedBtn.addEventListener('click', () => {
    const selectedItems = multiTree.querySelectorAll('wa-tree-item[selected]');
    const selectedText = Array.from(selectedItems).map(item => item.textContent.trim());
    console.log('Selected items:', selectedText);
    alert(`Selected: ${selectedText.join(', ')}`);
  });

  clearSelectionBtn.addEventListener('click', () => {
    const selectedItems = multiTree.querySelectorAll('wa-tree-item[selected]');
    selectedItems.forEach(item => item.selected = false);
  });
</script>
```

### Lazy Loading Tree

```html
<wa-tree selection="single" id="lazyTree" style="max-width: 400px;">
  <wa-tree-item lazy>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Lazy Loaded Folder
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Regular Folder
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      file1.txt
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>

<script>
  const lazyTree = document.getElementById('lazyTree');

  lazyTree.addEventListener('wa-lazy-load', async (event) => {
    const item = event.detail.item;

    // Show loading state
    item.loading = true;

    try {
      // Simulate API call
      const children = await fetchChildren(item);

      // Add loaded children
      children.forEach(child => {
        const childItem = document.createElement('wa-tree-item');
        const icon = document.createElement('wa-icon');
        icon.slot = 'icon';
        icon.name = child.type === 'folder' ? 'folder' : 'file';
        childItem.appendChild(icon);
        childItem.textContent = child.name;
        if (child.type === 'folder') {
          childItem.lazy = true;
        }
        item.appendChild(childItem);
      });

    } catch (error) {
      console.error('Failed to load children:', error);
    } finally {
      item.loading = false;
    }
  });

  async function fetchChildren(item) {
    // Simulate API delay
    await new Promise(resolve => setTimeout(resolve, 1000));

    // Return mock data
    return [
      { name: 'Loaded File 1.txt', type: 'file' },
      { name: 'Loaded File 2.txt', type: 'file' },
      { name: 'Loaded Subfolder', type: 'folder' }
    ];
  }
</script>
```

### Dynamic Tree Population

```html
<wa-tree id="dynamicTree" selection="single" style="max-width: 400px;"></wa-tree>

<script>
  const treeData = {
    name: 'Root',
    children: [
      {
        name: 'Fruits',
        children: [
          { name: 'Apple' },
          { name: 'Banana' },
          { name: 'Orange' }
        ]
      },
      {
        name: 'Vegetables',
        children: [
          { name: 'Carrot' },
          { name: 'Broccoli' },
          { name: 'Spinach' }
        ]
      },
      {
        name: 'Grains',
        children: [
          { name: 'Rice' },
          { name: 'Wheat' },
          { name: 'Oats' }
        ]
      }
    ]
  };

  function createTreeItem(data) {
    const item = document.createElement('wa-tree-item');

    // Add icon
    const icon = document.createElement('wa-icon');
    icon.slot = 'icon';
    icon.name = data.children ? 'folder' : 'file';
    item.appendChild(icon);

    // Add text
    const text = document.createTextNode(data.name);
    item.appendChild(text);

    // Add children recursively
    if (data.children) {
      data.children.forEach(child => {
        item.appendChild(createTreeItem(child));
      });
    }

    return item;
  }

  const dynamicTree = document.getElementById('dynamicTree');
  treeData.children.forEach(child => {
    dynamicTree.appendChild(createTreeItem(child));
  });
</script>
```

## Methods

The tree component itself doesn't have methods, but you can interact with tree items. See [Tree Item](./tree-item.md) for item-specific methods.

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-select` | Emitted when a tree item is selected | `{ item: HTMLElement }` |
| `wa-selection-change` | Emitted when the selection changes | `{ selection: HTMLElement[] }` |

### Event Examples

```javascript
const tree = document.querySelector('wa-tree');

// Listen for item selection
tree.addEventListener('wa-select', (event) => {
  console.log('Selected item:', event.detail.item);
  console.log('Item text:', event.detail.item.textContent.trim());
});

// Listen for selection changes (useful for multiple selection)
tree.addEventListener('wa-selection-change', (event) => {
  console.log('Current selection:', event.detail.selection);
  console.log('Number of selected items:', event.detail.selection.length);
});

// Handle navigation
tree.addEventListener('wa-select', (event) => {
  const item = event.detail.item;
  const itemText = item.textContent.trim();

  // Navigate based on selection
  if (itemText === 'Dashboard') {
    window.location.href = '/dashboard';
  } else if (itemText === 'Settings') {
    window.location.href = '/settings';
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Tree items (`wa-tree-item` elements) |

## CSS Parts

Use CSS parts to style internal tree elements:

```css
/* Style the tree container */
wa-tree::part(base) {
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  padding: 0.5rem;
}
```

## Customization

### Custom Tree Styling

```css
/* Custom tree appearance */
wa-tree {
  background-color: #f9f9f9;
  padding: 1rem;
  border-radius: 8px;
}

/* Style tree items */
wa-tree-item {
  --indent-size: 1.5rem;
  font-size: 0.95rem;
}

/* Custom selection color */
wa-tree-item[selected]::part(item) {
  background-color: #e3f2fd;
  color: #1976d2;
  font-weight: 500;
}

/* Hover effect */
wa-tree-item::part(item):hover {
  background-color: #f5f5f5;
}
```

### Compact Tree

```css
/* Compact spacing */
wa-tree-item {
  --indent-size: 1rem;
  --spacing: 0.25rem;
}

wa-tree-item::part(item) {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
}
```

## Best Practices

- ✅ Use meaningful, descriptive labels for tree items
- ✅ Include icons to enhance visual hierarchy
- ✅ Implement lazy loading for large trees
- ✅ Provide keyboard navigation support
- ✅ Use appropriate selection mode for your use case
- ✅ Keep tree depth reasonable (max 4-5 levels)
- ❌ Don't create overly deep nested structures
- ❌ Avoid using trees for simple flat lists
- ❌ Don't forget to handle loading states for lazy trees
- ❌ Avoid putting too much content in tree item labels

## Accessibility

- Tree automatically includes appropriate ARIA roles and attributes
- Full keyboard navigation support (arrow keys, Enter, Space)
- Screen reader announcements for expand/collapse and selection
- Focus management for keyboard users
- Proper nesting and hierarchy communicated to assistive technologies

```html
<!-- Accessible tree with labels -->
<wa-tree selection="single" aria-label="File system navigation">
  <wa-tree-item aria-label="Documents folder">
    Documents
    <wa-tree-item aria-label="Work documents">Work</wa-tree-item>
    <wa-tree-item aria-label="Personal documents">Personal</wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

### Keyboard Navigation

- Arrow Up/Down: Navigate between items
- Arrow Right: Expand item
- Arrow Left: Collapse item or move to parent
- Enter/Space: Select item
- Home: Move to first item
- End: Move to last item

## Troubleshooting

### Tree Items Not Showing

**Problem:** Tree structure doesn't display

**Solution:** Ensure proper nesting of `wa-tree-item` elements

```html
<!-- ❌ Incorrect -->
<wa-tree>
  <div>Item</div>
</wa-tree>

<!-- ✅ Correct -->
<wa-tree>
  <wa-tree-item>Item</wa-tree-item>
</wa-tree>
```

### Selection Not Working

**Problem:** Cannot select tree items

**Solution:** Verify selection mode is set correctly

```javascript
// Enable selection
tree.selection = 'single'; // or 'multiple', 'leaf'
```

### Icons Not Aligned

**Problem:** Icons appear misaligned with text

**Solution:** Use the `icon` slot properly

```html
<!-- ✅ Correct usage -->
<wa-tree-item>
  <wa-icon slot="icon" name="folder"></wa-icon>
  Folder Name
</wa-tree-item>
```

## Related

- [Tree Item](./tree-item.md)
- [Icon](./icon.md)
- [Menu](./menu.md)
- [Dropdown](./dropdown.md)
