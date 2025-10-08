# Button Group

Button groups organize related buttons together with seamless visual styling.

## Overview

The `<wa-button-group>` component provides a container for grouping related buttons together. It automatically handles the styling to make buttons appear connected, creating a cohesive visual unit perfect for toolbars, toggle groups, and segmented controls.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/button-group/button-group.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple button group -->
<wa-button-group>
  <wa-button>Left</wa-button>
  <wa-button>Center</wa-button>
  <wa-button>Right</wa-button>
</wa-button-group>

<!-- With label -->
<wa-button-group label="Text Alignment">
  <wa-button>Left</wa-button>
  <wa-button>Center</wa-button>
  <wa-button>Right</wa-button>
</wa-button-group>
```

## Icon Button Groups

Create compact toolbar buttons with icons:

```html
<!-- Icon-only buttons -->
<wa-button-group label="Text Formatting">
  <wa-button>
    <wa-icon name="bold"></wa-icon>
  </wa-button>
  <wa-button>
    <wa-icon name="italic"></wa-icon>
  </wa-button>
  <wa-button>
    <wa-icon name="underline"></wa-icon>
  </wa-button>
  <wa-button>
    <wa-icon name="strikethrough"></wa-icon>
  </wa-button>
</wa-button-group>

<!-- With accessible labels -->
<wa-button-group label="Clipboard">
  <wa-button aria-label="Cut">
    <wa-icon name="scissors"></wa-icon>
  </wa-button>
  <wa-button aria-label="Copy">
    <wa-icon name="copy"></wa-icon>
  </wa-button>
  <wa-button aria-label="Paste">
    <wa-icon name="clipboard"></wa-icon>
  </wa-button>
</wa-button-group>
```

## Variants and Sizes

Button groups work with all button variants and sizes:

```html
<!-- Primary button group -->
<wa-button-group>
  <wa-button variant="primary">Save</wa-button>
  <wa-button variant="primary">Save & Close</wa-button>
  <wa-button variant="primary">Save & New</wa-button>
</wa-button-group>

<!-- Outline button group -->
<wa-button-group>
  <wa-button variant="primary" outline>Day</wa-button>
  <wa-button variant="primary" outline>Week</wa-button>
  <wa-button variant="primary" outline>Month</wa-button>
  <wa-button variant="primary" outline>Year</wa-button>
</wa-button-group>

<!-- Small size -->
<wa-button-group>
  <wa-button size="small">Undo</wa-button>
  <wa-button size="small">Redo</wa-button>
</wa-button-group>

<!-- Large size -->
<wa-button-group>
  <wa-button size="large">Previous</wa-button>
  <wa-button size="large">Next</wa-button>
</wa-button-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `label` | string | - | No | Accessible label for the button group (required for accessibility if purpose isn't obvious) |

## Examples

### Text Editor Toolbar

```html
<div class="editor-toolbar">
  <!-- Text formatting -->
  <wa-button-group label="Text Style">
    <wa-button id="boldBtn" aria-label="Bold">
      <wa-icon name="bold"></wa-icon>
    </wa-button>
    <wa-button id="italicBtn" aria-label="Italic">
      <wa-icon name="italic"></wa-icon>
    </wa-button>
    <wa-button id="underlineBtn" aria-label="Underline">
      <wa-icon name="underline"></wa-icon>
    </wa-button>
  </wa-button-group>

  <!-- Alignment -->
  <wa-button-group label="Text Alignment">
    <wa-button id="alignLeft" aria-label="Align Left">
      <wa-icon name="text-left"></wa-icon>
    </wa-button>
    <wa-button id="alignCenter" aria-label="Align Center">
      <wa-icon name="text-center"></wa-icon>
    </wa-button>
    <wa-button id="alignRight" aria-label="Align Right">
      <wa-icon name="text-right"></wa-icon>
    </wa-button>
    <wa-button id="alignJustify" aria-label="Justify">
      <wa-icon name="text-justify"></wa-icon>
    </wa-button>
  </wa-button-group>

  <!-- Lists -->
  <wa-button-group label="Lists">
    <wa-button id="bulletList" aria-label="Bullet List">
      <wa-icon name="list-ul"></wa-icon>
    </wa-button>
    <wa-button id="numberList" aria-label="Numbered List">
      <wa-icon name="list-ol"></wa-icon>
    </wa-button>
  </wa-button-group>
</div>

<script>
  // Toggle button states
  document.querySelectorAll('.editor-toolbar wa-button').forEach(button => {
    button.addEventListener('click', () => {
      button.toggleAttribute('active');
    });
  });
</script>

<style>
  .editor-toolbar {
    display: flex;
    gap: 1rem;
    padding: 0.5rem;
    background: #f3f4f6;
    border-radius: 0.5rem;
  }

  wa-button[active]::part(base) {
    background-color: #3b82f6;
    color: white;
  }
</style>
```

### View Switcher

```html
<wa-button-group label="View Mode">
  <wa-button id="gridView" aria-label="Grid View">
    <wa-icon name="grid"></wa-icon>
  </wa-button>
  <wa-button id="listView" aria-label="List View">
    <wa-icon name="list"></wa-icon>
  </wa-button>
  <wa-button id="tableView" aria-label="Table View">
    <wa-icon name="table"></wa-icon>
  </wa-button>
</wa-button-group>

<div id="content">
  <!-- Content will change based on view -->
</div>

<script>
  const buttons = [
    document.getElementById('gridView'),
    document.getElementById('listView'),
    document.getElementById('tableView')
  ];

  const content = document.getElementById('content');

  buttons.forEach((button, index) => {
    button.addEventListener('click', () => {
      // Remove active from all buttons
      buttons.forEach(btn => btn.removeAttribute('active'));

      // Set active on clicked button
      button.setAttribute('active', '');

      // Update view
      const views = ['grid', 'list', 'table'];
      content.setAttribute('data-view', views[index]);
      console.log(`Switched to ${views[index]} view`);
    });
  });

  // Set initial view
  buttons[0].setAttribute('active', '');
</script>
```

### Zoom Controls

```html
<wa-button-group label="Zoom">
  <wa-button id="zoomOut" aria-label="Zoom Out">
    <wa-icon name="zoom-out"></wa-icon>
  </wa-button>
  <wa-button id="zoomReset">100%</wa-button>
  <wa-button id="zoomIn" aria-label="Zoom In">
    <wa-icon name="zoom-in"></wa-icon>
  </wa-button>
</wa-button-group>

<script>
  let zoom = 100;
  const zoomOut = document.getElementById('zoomOut');
  const zoomIn = document.getElementById('zoomIn');
  const zoomReset = document.getElementById('zoomReset');

  zoomOut.addEventListener('click', () => {
    zoom = Math.max(25, zoom - 25);
    zoomReset.textContent = `${zoom}%`;
    applyZoom(zoom);
  });

  zoomIn.addEventListener('click', () => {
    zoom = Math.min(200, zoom + 25);
    zoomReset.textContent = `${zoom}%`;
    applyZoom(zoom);
  });

  zoomReset.addEventListener('click', () => {
    zoom = 100;
    zoomReset.textContent = '100%';
    applyZoom(zoom);
  });

  function applyZoom(level) {
    document.body.style.zoom = `${level}%`;
  }
</script>
```

### Pagination Controls

```html
<wa-button-group label="Pagination">
  <wa-button id="firstPage" aria-label="First Page">
    <wa-icon name="chevron-double-left"></wa-icon>
  </wa-button>
  <wa-button id="prevPage" aria-label="Previous Page">
    <wa-icon name="chevron-left"></wa-icon>
  </wa-button>
  <wa-button id="pageInfo" disabled>Page 1 of 10</wa-button>
  <wa-button id="nextPage" aria-label="Next Page">
    <wa-icon name="chevron-right"></wa-icon>
  </wa-button>
  <wa-button id="lastPage" aria-label="Last Page">
    <wa-icon name="chevron-double-right"></wa-icon>
  </wa-button>
</wa-button-group>

<script>
  let currentPage = 1;
  const totalPages = 10;
  const pageInfo = document.getElementById('pageInfo');

  document.getElementById('firstPage').addEventListener('click', () => {
    currentPage = 1;
    updatePagination();
  });

  document.getElementById('prevPage').addEventListener('click', () => {
    currentPage = Math.max(1, currentPage - 1);
    updatePagination();
  });

  document.getElementById('nextPage').addEventListener('click', () => {
    currentPage = Math.min(totalPages, currentPage + 1);
    updatePagination();
  });

  document.getElementById('lastPage').addEventListener('click', () => {
    currentPage = totalPages;
    updatePagination();
  });

  function updatePagination() {
    pageInfo.textContent = `Page ${currentPage} of ${totalPages}`;

    // Enable/disable buttons based on current page
    document.getElementById('firstPage').disabled = currentPage === 1;
    document.getElementById('prevPage').disabled = currentPage === 1;
    document.getElementById('nextPage').disabled = currentPage === totalPages;
    document.getElementById('lastPage').disabled = currentPage === totalPages;
  }

  updatePagination();
</script>
```

### Media Controls

```html
<wa-button-group label="Media Controls">
  <wa-button id="skipBack" aria-label="Skip Back">
    <wa-icon name="skip-back"></wa-icon>
  </wa-button>
  <wa-button id="playPause" aria-label="Play">
    <wa-icon name="play"></wa-icon>
  </wa-button>
  <wa-button id="skipForward" aria-label="Skip Forward">
    <wa-icon name="skip-forward"></wa-icon>
  </wa-button>
  <wa-button id="volume" aria-label="Volume">
    <wa-icon name="volume-high"></wa-icon>
  </wa-button>
</wa-button-group>

<script>
  let isPlaying = false;
  const playPauseBtn = document.getElementById('playPause');
  const playIcon = playPauseBtn.querySelector('wa-icon');

  playPauseBtn.addEventListener('click', () => {
    isPlaying = !isPlaying;
    playIcon.name = isPlaying ? 'pause' : 'play';
    playPauseBtn.setAttribute('aria-label', isPlaying ? 'Pause' : 'Play');

    if (isPlaying) {
      console.log('Playing media');
    } else {
      console.log('Paused media');
    }
  });

  document.getElementById('skipBack').addEventListener('click', () => {
    console.log('Skip back 10 seconds');
  });

  document.getElementById('skipForward').addEventListener('click', () => {
    console.log('Skip forward 10 seconds');
  });

  document.getElementById('volume').addEventListener('click', () => {
    console.log('Toggle volume');
  });
</script>
```

### Segmented Control / Toggle Group

```html
<wa-button-group label="Time Period">
  <wa-button id="day" variant="primary" outline>Day</wa-button>
  <wa-button id="week" variant="primary" outline>Week</wa-button>
  <wa-button id="month" variant="primary" outline>Month</wa-button>
  <wa-button id="year" variant="primary" outline>Year</wa-button>
</wa-button-group>

<div id="chart">
  <!-- Chart or content based on selection -->
</div>

<script>
  const timeButtons = ['day', 'week', 'month', 'year'].map(id =>
    document.getElementById(id)
  );

  timeButtons.forEach(button => {
    button.addEventListener('click', () => {
      // Remove outline from all, add solid to clicked
      timeButtons.forEach(btn => {
        btn.outline = true;
        btn.removeAttribute('data-selected');
      });

      button.outline = false;
      button.setAttribute('data-selected', '');

      console.log(`Loading ${button.id} view`);
      loadChartData(button.id);
    });
  });

  // Set initial selection
  timeButtons[0].outline = false;
  timeButtons[0].setAttribute('data-selected', '');

  function loadChartData(period) {
    // Load data for selected period
    console.log(`Loading data for period: ${period}`);
  }
</script>
```

### Split Button Group

```html
<wa-button-group>
  <wa-button variant="primary" id="primaryAction">Save</wa-button>
  <wa-dropdown>
    <wa-button slot="trigger" variant="primary" caret></wa-button>
    <wa-menu>
      <wa-menu-item id="saveClose">Save & Close</wa-menu-item>
      <wa-menu-item id="saveNew">Save & New</wa-menu-item>
      <wa-menu-item id="saveCopy">Save as Copy</wa-menu-item>
    </wa-menu>
  </wa-dropdown>
</wa-button-group>

<script>
  document.getElementById('primaryAction').addEventListener('click', () => {
    console.log('Saving...');
  });

  document.getElementById('saveClose').addEventListener('click', () => {
    console.log('Save & Close');
  });

  document.getElementById('saveNew').addEventListener('click', () => {
    console.log('Save & New');
  });

  document.getElementById('saveCopy').addEventListener('click', () => {
    console.log('Save as Copy');
  });
</script>
```

### Filter Button Group

```html
<wa-button-group label="Filter Status">
  <wa-button id="allFilter">All</wa-button>
  <wa-button id="activeFilter">Active</wa-button>
  <wa-button id="completedFilter">Completed</wa-button>
  <wa-button id="archivedFilter">Archived</wa-button>
</wa-button-group>

<div id="itemsList">
  <!-- Filtered items -->
</div>

<script>
  const filters = ['allFilter', 'activeFilter', 'completedFilter', 'archivedFilter'];

  filters.forEach(filterId => {
    const button = document.getElementById(filterId);

    button.addEventListener('click', () => {
      // Remove active state from all
      filters.forEach(id => {
        document.getElementById(id).removeAttribute('active');
      });

      // Add active state to clicked
      button.setAttribute('active', '');

      // Apply filter
      const filterType = filterId.replace('Filter', '');
      applyFilter(filterType);
    });
  });

  // Set initial filter
  document.getElementById('allFilter').setAttribute('active', '');

  function applyFilter(type) {
    console.log(`Filtering by: ${type}`);
    // Apply filtering logic
  }
</script>

<style>
  wa-button[active]::part(base) {
    background-color: #3b82f6;
    color: white;
    border-color: #3b82f6;
  }
</style>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | One or more `<wa-button>` components |

## CSS Parts

Use CSS parts to style internal button group elements:

```css
/* Style the base container */
wa-button-group::part(base) {
  gap: 0;
  border-radius: 0.5rem;
  overflow: hidden;
}

/* Style the label */
wa-button-group::part(label) {
  font-weight: 600;
  margin-bottom: 0.5rem;
}
```

## Customization

### Vertical Button Group

```html
<wa-button-group class="vertical">
  <wa-button>Top</wa-button>
  <wa-button>Middle</wa-button>
  <wa-button>Bottom</wa-button>
</wa-button-group>

<style>
  wa-button-group.vertical::part(base) {
    flex-direction: column;
  }
</style>
```

### Separated Buttons

```html
<wa-button-group class="separated">
  <wa-button>First</wa-button>
  <wa-button>Second</wa-button>
  <wa-button>Third</wa-button>
</wa-button-group>

<style>
  wa-button-group.separated::part(base) {
    gap: 0.5rem;
  }
</style>
```

### Custom Button Styling

```css
/* Remove rounded corners for middle buttons */
wa-button-group wa-button:not(:first-child):not(:last-child)::part(base) {
  border-radius: 0;
}

/* Round only first button */
wa-button-group wa-button:first-child::part(base) {
  border-radius: 0.5rem 0 0 0.5rem;
}

/* Round only last button */
wa-button-group wa-button:last-child::part(base) {
  border-radius: 0 0.5rem 0.5rem 0;
}

/* Remove double borders */
wa-button-group wa-button:not(:last-child)::part(base) {
  border-right-width: 0;
}
```

## Best Practices

- Group buttons that perform related actions
- Use consistent button variants and sizes within a group
- Provide accessible labels for icon-only button groups
- Use `aria-label` on individual icon buttons for screen reader support
- Implement visual feedback for active/selected states in toggle groups
- Keep button groups to 3-5 buttons for optimal usability
- Use button groups for mutually exclusive options (like view switchers)
- Avoid mixing too many different button types in one group
- Ensure adequate touch targets for mobile devices (minimum 44x44px)

## Accessibility

- Button groups automatically include appropriate ARIA roles
- Use the `label` attribute to describe the group's purpose
- Provide `aria-label` on icon-only buttons within the group
- For toggle groups, use `aria-pressed` to indicate button state:

```html
<wa-button-group label="Text Alignment">
  <wa-button aria-label="Align Left" aria-pressed="true">
    <wa-icon name="text-left"></wa-icon>
  </wa-button>
  <wa-button aria-label="Align Center" aria-pressed="false">
    <wa-icon name="text-center"></wa-icon>
  </wa-button>
  <wa-button aria-label="Align Right" aria-pressed="false">
    <wa-icon name="text-right"></wa-icon>
  </wa-button>
</wa-button-group>
```

- Keyboard navigation works naturally (Tab moves between buttons)
- Ensure sufficient color contrast for button states
- Use `role="group"` or `role="toolbar"` when appropriate

## Troubleshooting

### Buttons Not Visually Connected

**Problem:** Buttons appear separated instead of connected

**Solution:** Ensure buttons are direct children of the button group

```html
<!-- Correct -->
<wa-button-group>
  <wa-button>One</wa-button>
  <wa-button>Two</wa-button>
</wa-button-group>

<!-- Incorrect - wrapped in div -->
<wa-button-group>
  <div>
    <wa-button>One</wa-button>
    <wa-button>Two</wa-button>
  </div>
</wa-button-group>
```

### Inconsistent Button Sizes

**Problem:** Buttons have different sizes in the group

**Solution:** Ensure all buttons use the same size attribute

```html
<!-- Correct - consistent size -->
<wa-button-group>
  <wa-button size="small">One</wa-button>
  <wa-button size="small">Two</wa-button>
</wa-button-group>

<!-- Incorrect - mixed sizes -->
<wa-button-group>
  <wa-button size="small">One</wa-button>
  <wa-button size="large">Two</wa-button>
</wa-button-group>
```

### Toggle State Not Working

**Problem:** Active/selected state doesn't show

**Solution:** Implement custom styling for active state

```css
wa-button[active]::part(base) {
  background-color: #3b82f6;
  color: white;
}
```

## Related

- [Button](./button.md)
- [Icon Button](./icon-button.md)
- [Icon](./icon.md)
- [Dropdown](./dropdown.md)
- [Toolbar Guide](../guides/toolbar.md)
