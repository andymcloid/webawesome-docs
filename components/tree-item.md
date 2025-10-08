# Tree Item

Individual items within a tree structure, supporting nesting and lazy loading.

## Overview

The `<wa-tree-item>` component represents a single node within a `<wa-tree>`. It supports expand/collapse behavior, selection states, custom icons, lazy loading, and arbitrary nesting depth. Tree items can contain other tree items to create hierarchical structures.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tree-item/tree-item.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-tree>
  <!-- Simple tree item -->
  <wa-tree-item>Simple Item</wa-tree-item>

  <!-- Tree item with children -->
  <wa-tree-item>
    Parent Item
    <wa-tree-item>Child Item 1</wa-tree-item>
    <wa-tree-item>Child Item 2</wa-tree-item>
  </wa-tree-item>

  <!-- Tree item with icon -->
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Folder
  </wa-tree-item>
</wa-tree>
```

## Expanded State

Control whether an item is expanded by default:

```html
<wa-tree>
  <!-- Collapsed by default -->
  <wa-tree-item>
    Collapsed Parent
    <wa-tree-item>Hidden Child</wa-tree-item>
  </wa-tree-item>

  <!-- Expanded by default -->
  <wa-tree-item expanded>
    Expanded Parent
    <wa-tree-item>Visible Child</wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

## Selected State

Mark items as selected:

```html
<wa-tree>
  <wa-tree-item>Unselected Item</wa-tree-item>
  <wa-tree-item selected>Selected Item</wa-tree-item>
  <wa-tree-item>Another Item</wa-tree-item>
</wa-tree>
```

## Disabled State

Disable interaction with tree items:

```html
<wa-tree>
  <wa-tree-item>Active Item</wa-tree-item>
  <wa-tree-item disabled>Disabled Item</wa-tree-item>
  <wa-tree-item>
    Parent Item
    <wa-tree-item disabled>Disabled Child</wa-tree-item>
    <wa-tree-item>Active Child</wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

## Lazy Loading

Enable lazy loading for dynamic content:

```html
<wa-tree id="lazyTree">
  <wa-tree-item lazy>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Load on Expand
  </wa-tree-item>
</wa-tree>

<script>
  const tree = document.getElementById('lazyTree');

  tree.addEventListener('wa-lazy-load', async (event) => {
    const item = event.detail.item;
    item.loading = true;

    // Fetch data from API
    const data = await fetchChildData();

    // Add children
    data.forEach(child => {
      const childItem = document.createElement('wa-tree-item');
      childItem.textContent = child.name;
      item.appendChild(childItem);
    });

    item.loading = false;
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `expanded` | boolean | `false` | No | Whether the tree item is expanded |
| `selected` | boolean | `false` | No | Whether the tree item is selected |
| `disabled` | boolean | `false` | No | Disable the tree item |
| `lazy` | boolean | `false` | No | Enable lazy loading of children |
| `loading` | boolean | `false` | No | Show loading state (used with lazy loading) |

## Examples

### Nested File Structure

```html
<wa-tree selection="single">
  <wa-tree-item expanded>
    <wa-icon slot="icon" name="folder-open"></wa-icon>
    src
    <wa-tree-item expanded>
      <wa-icon slot="icon" name="folder-open"></wa-icon>
      components
      <wa-tree-item>
        <wa-icon slot="icon" name="file"></wa-icon>
        Button.js
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file"></wa-icon>
        Input.js
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file"></wa-icon>
        Select.js
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      utils
      <wa-tree-item>
        <wa-icon slot="icon" name="file"></wa-icon>
        helpers.js
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file"></wa-icon>
        constants.js
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      index.js
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    public
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      index.html
    </wa-tree-item>
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="file"></wa-icon>
    package.json
  </wa-tree-item>
  <wa-tree-item>
    <wa-icon slot="icon" name="file"></wa-icon>
    README.md
  </wa-tree-item>
</wa-tree>
```

### Custom Expand/Collapse Icons

```html
<wa-tree selection="single">
  <wa-tree-item>
    <wa-icon slot="expand-icon" name="plus-circle"></wa-icon>
    <wa-icon slot="collapse-icon" name="minus-circle"></wa-icon>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Custom Icons
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      Child Item
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

### Interactive File Manager

```html
<wa-tree id="fileManager" selection="single" style="max-width: 500px;">
  <wa-tree-item expanded>
    <wa-icon slot="icon" name="hard-drive"></wa-icon>
    My Computer
    <wa-tree-item expanded>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Documents
      <wa-tree-item>
        <wa-icon slot="icon" name="file-text"></wa-icon>
        resume.pdf
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-text"></wa-icon>
        cover-letter.docx
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Downloads
      <wa-tree-item>
        <wa-icon slot="icon" name="file-zip"></wa-icon>
        archive.zip
      </wa-tree-item>
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="folder"></wa-icon>
      Pictures
      <wa-tree-item>
        <wa-icon slot="icon" name="file-image"></wa-icon>
        vacation.jpg
      </wa-tree-item>
      <wa-tree-item>
        <wa-icon slot="icon" name="file-image"></wa-icon>
        family.png
      </wa-tree-item>
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>

<div style="margin-top: 1rem; padding: 1rem; background: #f5f5f5; border-radius: 4px;">
  <strong>Selected:</strong> <span id="selectedFile">None</span>
</div>

<script>
  const fileManager = document.getElementById('fileManager');
  const selectedFile = document.getElementById('selectedFile');

  fileManager.addEventListener('wa-select', (event) => {
    const item = event.detail.item;
    selectedFile.textContent = item.textContent.trim();
  });
</script>
```

### Lazy Loading Large Dataset

```html
<wa-tree id="lazyTree" selection="single" style="max-width: 400px;">
  <wa-tree-item lazy>
    <wa-icon slot="icon" name="database"></wa-icon>
    Users (Click to load)
  </wa-tree-item>
  <wa-tree-item lazy>
    <wa-icon slot="icon" name="database"></wa-icon>
    Products (Click to load)
  </wa-tree-item>
  <wa-tree-item lazy>
    <wa-icon slot="icon" name="database"></wa-icon>
    Orders (Click to load)
  </wa-tree-item>
</wa-tree>

<script>
  const lazyTree = document.getElementById('lazyTree');

  lazyTree.addEventListener('wa-lazy-load', async (event) => {
    const item = event.detail.item;
    const category = item.textContent.trim().split('(')[0].trim();

    // Show loading state
    item.loading = true;

    try {
      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1000));

      // Generate mock data
      const items = generateMockData(category);

      // Add children
      items.forEach(child => {
        const childItem = document.createElement('wa-tree-item');

        const icon = document.createElement('wa-icon');
        icon.slot = 'icon';
        icon.name = child.icon;
        childItem.appendChild(icon);

        const text = document.createTextNode(child.name);
        childItem.appendChild(text);

        // Make some items also lazy loadable
        if (child.hasChildren) {
          childItem.lazy = true;
        }

        item.appendChild(childItem);
      });

    } catch (error) {
      console.error('Failed to load data:', error);
    } finally {
      item.loading = false;
    }
  });

  function generateMockData(category) {
    const data = {
      'Users': [
        { name: 'Admin Users', icon: 'users', hasChildren: true },
        { name: 'Regular Users', icon: 'users', hasChildren: true },
        { name: 'Guest Users', icon: 'user', hasChildren: false }
      ],
      'Products': [
        { name: 'Electronics', icon: 'cpu', hasChildren: true },
        { name: 'Clothing', icon: 'shopping-bag', hasChildren: true },
        { name: 'Books', icon: 'book', hasChildren: true }
      ],
      'Orders': [
        { name: 'Pending', icon: 'clock', hasChildren: true },
        { name: 'Completed', icon: 'check-circle', hasChildren: true },
        { name: 'Cancelled', icon: 'x-circle', hasChildren: true }
      ]
    };

    return data[category] || [];
  }
</script>
```

### Tree with Context Menu

```html
<wa-tree id="contextTree" selection="single" style="max-width: 400px;">
  <wa-tree-item>
    <wa-icon slot="icon" name="folder"></wa-icon>
    Documents
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      Report.docx
    </wa-tree-item>
    <wa-tree-item>
      <wa-icon slot="icon" name="file"></wa-icon>
      Presentation.pptx
    </wa-tree-item>
  </wa-tree-item>
</wa-tree>

<wa-menu id="contextMenu" style="display: none;">
  <wa-menu-item>
    <wa-icon slot="icon" name="edit"></wa-icon>
    Rename
  </wa-menu-item>
  <wa-menu-item>
    <wa-icon slot="icon" name="copy"></wa-icon>
    Duplicate
  </wa-menu-item>
  <wa-divider></wa-divider>
  <wa-menu-item>
    <wa-icon slot="icon" name="trash"></wa-icon>
    Delete
  </wa-menu-item>
</wa-menu>

<script>
  const contextTree = document.getElementById('contextTree');
  const contextMenu = document.getElementById('contextMenu');
  let contextTarget = null;

  contextTree.addEventListener('contextmenu', (event) => {
    event.preventDefault();

    // Find the tree item
    const item = event.target.closest('wa-tree-item');
    if (item) {
      contextTarget = item;
      contextMenu.style.display = 'block';
      contextMenu.style.position = 'fixed';
      contextMenu.style.left = event.clientX + 'px';
      contextMenu.style.top = event.clientY + 'px';
    }
  });

  document.addEventListener('click', () => {
    contextMenu.style.display = 'none';
  });

  contextMenu.addEventListener('wa-select', (event) => {
    const action = event.detail.item.textContent.trim();
    console.log(`Action: ${action} on item:`, contextTarget?.textContent.trim());
    contextMenu.style.display = 'none';
  });
</script>
```

### Indeterminate State for Parent Items

```html
<wa-tree selection="multiple" id="checkboxTree" style="max-width: 400px;">
  <wa-tree-item>
    All Items
    <wa-tree-item>Feature A</wa-tree-item>
    <wa-tree-item>Feature B</wa-tree-item>
    <wa-tree-item>Feature C</wa-tree-item>
  </wa-tree-item>
</wa-tree>

<script>
  const checkboxTree = document.getElementById('checkboxTree');

  checkboxTree.addEventListener('wa-selection-change', () => {
    updateParentStates();
  });

  function updateParentStates() {
    const parents = checkboxTree.querySelectorAll('wa-tree-item');

    parents.forEach(parent => {
      const children = Array.from(parent.querySelectorAll(':scope > wa-tree-item'));

      if (children.length > 0) {
        const selectedCount = children.filter(c => c.selected).length;

        if (selectedCount === 0) {
          parent.selected = false;
          parent.indeterminate = false;
        } else if (selectedCount === children.length) {
          parent.selected = true;
          parent.indeterminate = false;
        } else {
          parent.selected = false;
          parent.indeterminate = true;
        }
      }
    });
  }
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `expand()` | Expand the tree item | `void` |
| `collapse()` | Collapse the tree item | `void` |

### Method Examples

```javascript
const treeItem = document.querySelector('wa-tree-item');

// Expand an item
treeItem.expand();

// Collapse an item
treeItem.collapse();

// Toggle expanded state
if (treeItem.expanded) {
  treeItem.collapse();
} else {
  treeItem.expand();
}

// Expand all items in a tree
const allItems = document.querySelectorAll('wa-tree-item');
allItems.forEach(item => item.expand());

// Collapse all items
allItems.forEach(item => item.collapse());
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-expand` | Emitted when the item is expanded | - |
| `wa-collapse` | Emitted when the item is collapsed | - |
| `wa-lazy-load` | Emitted when a lazy item needs to load children | `{ item: HTMLElement }` |

### Event Examples

```javascript
const treeItem = document.querySelector('wa-tree-item');

// Listen for expand
treeItem.addEventListener('wa-expand', () => {
  console.log('Item expanded');
});

// Listen for collapse
treeItem.addEventListener('wa-collapse', () => {
  console.log('Item collapsed');
});

// Lazy loading
treeItem.addEventListener('wa-lazy-load', async (event) => {
  const item = event.detail.item;
  item.loading = true;

  const children = await fetchChildren(item);
  children.forEach(child => item.appendChild(child));

  item.loading = false;
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The tree item's label and nested children |
| `icon` | An icon to display before the label |
| `expand-icon` | Custom icon for the expand button |
| `collapse-icon` | Custom icon for the collapse button |

### Slot Examples

```html
<!-- Custom icons -->
<wa-tree-item>
  <wa-icon slot="icon" name="folder"></wa-icon>
  <wa-icon slot="expand-icon" name="chevron-right"></wa-icon>
  <wa-icon slot="collapse-icon" name="chevron-down"></wa-icon>
  Folder with custom icons
  <wa-tree-item>Child</wa-tree-item>
</wa-tree-item>

<!-- Rich content in label -->
<wa-tree-item>
  <wa-avatar slot="icon" initials="JD"></wa-avatar>
  <div>
    <strong>John Doe</strong>
    <div style="font-size: 0.875rem; color: #666;">john@example.com</div>
  </div>
</wa-tree-item>
```

## CSS Parts

Use CSS parts to style internal tree item elements:

```css
/* Style the item container */
wa-tree-item::part(item) {
  padding: 0.5rem;
  border-radius: 4px;
}

/* Style selected state */
wa-tree-item[selected]::part(item) {
  background-color: #e3f2fd;
  color: #1976d2;
}

/* Style hover state */
wa-tree-item::part(item):hover {
  background-color: #f5f5f5;
}

/* Style the expand button */
wa-tree-item::part(expand-button) {
  color: #666;
}

/* Style the label */
wa-tree-item::part(label) {
  font-weight: normal;
}

/* Style indentation */
wa-tree-item::part(indentation) {
  width: 1.5rem;
}

/* Style children container */
wa-tree-item::part(children) {
  margin-left: 1rem;
}
```

## Customization

### Custom Item Styling

```css
/* Highlight important items */
wa-tree-item.important::part(item) {
  background-color: #fff3cd;
  border-left: 3px solid #ffc107;
}

/* Custom disabled state */
wa-tree-item[disabled]::part(item) {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Custom loading state */
wa-tree-item[loading]::part(expand-button) {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```

### CSS Custom Properties

```css
/* Adjust indentation */
wa-tree-item {
  --indent-size: 2rem;
  --indent-guide-width: 1px;
  --indent-guide-color: #e0e0e0;
  --spacing: 0.5rem;
}
```

## Best Practices

- ✅ Use icons to indicate item type (folder, file, etc.)
- ✅ Provide feedback for loading states
- ✅ Keep item labels concise and descriptive
- ✅ Use lazy loading for trees with many items
- ✅ Provide expand/collapse all functionality for deep trees
- ✅ Implement proper error handling for lazy loading
- ❌ Don't create excessively deep nesting (max 5-7 levels)
- ❌ Avoid long labels that wrap multiple lines
- ❌ Don't forget to handle loading failures
- ❌ Avoid mixing selectable and non-selectable items inconsistently

## Accessibility

- Tree items include appropriate ARIA roles and attributes
- Keyboard navigation fully supported
- Expand/collapse state announced to screen readers
- Selection state communicated to assistive technologies
- Disabled items properly excluded from navigation

```html
<!-- Accessible tree items -->
<wa-tree>
  <wa-tree-item aria-label="Documents folder, contains 3 items">
    <wa-icon slot="icon" name="folder"></wa-icon>
    Documents
    <wa-tree-item>File 1</wa-tree-item>
    <wa-tree-item>File 2</wa-tree-item>
    <wa-tree-item>File 3</wa-tree-item>
  </wa-tree-item>
</wa-tree>
```

## Troubleshooting

### Children Not Showing

**Problem:** Nested items don't appear when expanded

**Solution:** Ensure items are properly nested and expanded attribute is set

```html
<!-- ✅ Correct nesting -->
<wa-tree-item expanded>
  Parent
  <wa-tree-item>Child</wa-tree-item>
</wa-tree-item>
```

### Lazy Loading Not Triggering

**Problem:** `wa-lazy-load` event doesn't fire

**Solution:** Ensure `lazy` attribute is set and listen on the tree

```javascript
// Listen on the tree, not the item
tree.addEventListener('wa-lazy-load', (event) => {
  // Handle lazy loading
});
```

### Icons Misaligned

**Problem:** Icons don't align properly with text

**Solution:** Use the proper slot for icons

```html
<!-- ✅ Correct -->
<wa-tree-item>
  <wa-icon slot="icon" name="folder"></wa-icon>
  Folder
</wa-tree-item>

<!-- ❌ Incorrect -->
<wa-tree-item>
  <wa-icon name="folder"></wa-icon>
  Folder
</wa-tree-item>
```

## Related

- [Tree](./tree.md)
- [Icon](./icon.md)
- [Avatar](./avatar.md)
- [Menu](./menu.md)
