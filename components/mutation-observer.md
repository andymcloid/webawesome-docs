# Mutation Observer

A utility component that watches for changes to the DOM and emits events when mutations occur.

## Overview

The `<wa-mutation-observer>` component wraps the native MutationObserver API, making it easy to observe DOM mutations declaratively. It watches for changes to attributes, child elements, and text content within its default slot and emits events when mutations are detected.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/mutation-observer/mutation-observer.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Watch for any changes -->
<wa-mutation-observer>
  <div id="observed">
    Content to observe
  </div>
</wa-mutation-observer>

<script>
  const observer = document.querySelector('wa-mutation-observer');

  observer.addEventListener('wa-mutation', (event) => {
    console.log('Mutations detected:', event.detail.mutations);
  });
</script>
```

## Observation Types

### Attribute Changes

Watch for attribute modifications:

```html
<wa-mutation-observer attr="class style">
  <div id="box" class="initial" style="color: red;">
    Watch my attributes
  </div>
</wa-mutation-observer>

<wa-button id="changeClass">Change Class</wa-button>
<wa-button id="changeStyle">Change Style</wa-button>

<script>
  const observer = document.querySelector('wa-mutation-observer');
  const box = document.getElementById('box');

  observer.addEventListener('wa-mutation', (event) => {
    console.log('Attribute changed:', event.detail.mutations);
  });

  document.getElementById('changeClass').addEventListener('click', () => {
    box.className = 'modified';
  });

  document.getElementById('changeStyle').addEventListener('click', () => {
    box.style.color = 'blue';
  });
</script>
```

### Attribute Old Value

Track previous attribute values:

```html
<wa-mutation-observer attr="data-count" attr-old-value>
  <div id="counter" data-count="0">
    Count: 0
  </div>
</wa-mutation-observer>

<wa-button id="incrementBtn">Increment</wa-button>

<script>
  const observer = document.querySelector('wa-mutation-observer');
  const counter = document.getElementById('counter');

  observer.addEventListener('wa-mutation', (event) => {
    event.detail.mutations.forEach(mutation => {
      console.log('Old value:', mutation.oldValue);
      console.log('New value:', mutation.target.getAttribute('data-count'));
    });
  });

  document.getElementById('incrementBtn').addEventListener('click', () => {
    const current = parseInt(counter.getAttribute('data-count'));
    const next = current + 1;
    counter.setAttribute('data-count', next);
    counter.textContent = `Count: ${next}`;
  });
</script>
```

### Child List Changes

Watch for added or removed child elements:

```html
<wa-mutation-observer child-list>
  <ul id="itemList">
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</wa-mutation-observer>

<wa-button id="addItem">Add Item</wa-button>
<wa-button id="removeItem">Remove Item</wa-button>

<script>
  const observer = document.querySelector('wa-mutation-observer');
  const list = document.getElementById('itemList');
  let itemCount = 2;

  observer.addEventListener('wa-mutation', (event) => {
    event.detail.mutations.forEach(mutation => {
      if (mutation.addedNodes.length) {
        console.log('Added nodes:', mutation.addedNodes);
      }
      if (mutation.removedNodes.length) {
        console.log('Removed nodes:', mutation.removedNodes);
      }
    });
  });

  document.getElementById('addItem').addEventListener('click', () => {
    const li = document.createElement('li');
    li.textContent = `Item ${++itemCount}`;
    list.appendChild(li);
  });

  document.getElementById('removeItem').addEventListener('click', () => {
    const lastItem = list.querySelector('li:last-child');
    if (lastItem) {
      list.removeChild(lastItem);
    }
  });
</script>
```

### Character Data Changes

Watch for text content modifications:

```html
<wa-mutation-observer char-data>
  <p id="textContent">
    Original text content
  </p>
</wa-mutation-observer>

<wa-button id="changeText">Change Text</wa-button>

<script>
  const observer = document.querySelector('wa-mutation-observer');
  const paragraph = document.getElementById('textContent');

  observer.addEventListener('wa-mutation', (event) => {
    console.log('Text changed:', event.detail.mutations);
  });

  document.getElementById('changeText').addEventListener('click', () => {
    paragraph.textContent = 'Updated text content at ' + new Date().toLocaleTimeString();
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `attr` | string | `''` | No | Space-separated list of attribute names to observe (empty string = all attributes) |
| `attr-old-value` | boolean | `false` | No | Record previous attribute values |
| `char-data` | boolean | `false` | No | Observe text content changes |
| `char-data-old-value` | boolean | `false` | No | Record previous text content |
| `child-list` | boolean | `false` | No | Observe child element additions/removals |
| `disabled` | boolean | `false` | No | Disables observation when true |

### Properties

```javascript
const observer = document.querySelector('wa-mutation-observer');

// Enable/disable observation
observer.disabled = true;
observer.disabled = false;

// Configure what to observe
observer.attr = 'class id'; // Observe specific attributes
observer.childList = true; // Watch for child changes
observer.charData = true; // Watch for text changes

// Track old values
observer.attrOldValue = true;
observer.charDataOldValue = true;
```

## Examples

### Form Field Validation Tracker

```html
<wa-mutation-observer attr="class" id="validationObserver">
  <form id="myForm">
    <wa-input
      id="email"
      label="Email"
      type="email"
      required
    ></wa-input>

    <wa-input
      id="password"
      label="Password"
      type="password"
      required
    ></wa-input>
  </form>
</wa-mutation-observer>

<script>
  const observer = document.getElementById('validationObserver');

  observer.addEventListener('wa-mutation', (event) => {
    event.detail.mutations.forEach(mutation => {
      const element = mutation.target;
      if (element.tagName.toLowerCase().startsWith('wa-')) {
        console.log(`${element.id} validation state changed`);
      }
    });
  });
</script>
```

### Dynamic Content Monitor

```html
<wa-mutation-observer child-list id="contentObserver">
  <div id="dynamicContent">
    <p>Initial content</p>
  </div>
</wa-mutation-observer>

<wa-button id="loadMore">Load More Content</wa-button>

<div id="stats">
  <p>Total items: <span id="itemCount">1</span></p>
</div>

<script>
  const observer = document.getElementById('contentObserver');
  const content = document.getElementById('dynamicContent');
  const itemCount = document.getElementById('itemCount');

  observer.addEventListener('wa-mutation', (event) => {
    const paragraphs = content.querySelectorAll('p');
    itemCount.textContent = paragraphs.length;
  });

  document.getElementById('loadMore').addEventListener('click', () => {
    const p = document.createElement('p');
    p.textContent = `Content item ${content.children.length + 1}`;
    content.appendChild(p);
  });
</script>
```

### Theme Change Detector

```html
<wa-mutation-observer attr="data-theme" attr-old-value id="themeObserver">
  <div id="app" data-theme="light">
    <h1>My Application</h1>
    <p>Watch the theme changes</p>
  </div>
</wa-mutation-observer>

<wa-button-group>
  <wa-button id="lightTheme">Light Theme</wa-button>
  <wa-button id="darkTheme">Dark Theme</wa-button>
  <wa-button id="autoTheme">Auto Theme</wa-button>
</wa-button-group>

<script>
  const observer = document.getElementById('themeObserver');
  const app = document.getElementById('app');

  observer.addEventListener('wa-mutation', (event) => {
    event.detail.mutations.forEach(mutation => {
      console.log('Theme changed from', mutation.oldValue, 'to', app.getAttribute('data-theme'));

      // Apply theme-specific styles
      const theme = app.getAttribute('data-theme');
      if (theme === 'dark') {
        app.style.background = '#1e293b';
        app.style.color = '#f1f5f9';
      } else {
        app.style.background = '#ffffff';
        app.style.color = '#1e293b';
      }
    });
  });

  document.getElementById('lightTheme').addEventListener('click', () => {
    app.setAttribute('data-theme', 'light');
  });

  document.getElementById('darkTheme').addEventListener('click', () => {
    app.setAttribute('data-theme', 'dark');
  });

  document.getElementById('autoTheme').addEventListener('click', () => {
    app.setAttribute('data-theme', 'auto');
  });
</script>
```

### Live Analytics Dashboard

```html
<wa-mutation-observer child-list char-data id="analyticsObserver">
  <div id="dashboard">
    <div class="metric">
      <span class="label">Users:</span>
      <span class="value" id="userCount">0</span>
    </div>
    <div class="metric">
      <span class="label">Revenue:</span>
      <span class="value" id="revenue">$0</span>
    </div>
  </div>
</wa-mutation-observer>

<wa-button id="updateMetrics">Update Metrics</wa-button>

<script>
  const observer = document.getElementById('analyticsObserver');
  const userCount = document.getElementById('userCount');
  const revenue = document.getElementById('revenue');

  observer.addEventListener('wa-mutation', (event) => {
    console.log('Dashboard metrics updated');

    // Track changes for analytics
    event.detail.mutations.forEach(mutation => {
      if (mutation.type === 'characterData' || mutation.type === 'childList') {
        console.log('Metric changed:', mutation.target.textContent);
      }
    });
  });

  document.getElementById('updateMetrics').addEventListener('click', () => {
    userCount.textContent = Math.floor(Math.random() * 1000);
    revenue.textContent = '$' + (Math.random() * 10000).toFixed(2);
  });
</script>
```

### Component State Sync

```html
<wa-mutation-observer attr="aria-expanded" id="accordionObserver">
  <wa-details id="details1" summary="Section 1">
    Content for section 1
  </wa-details>
  <wa-details id="details2" summary="Section 2">
    Content for section 2
  </wa-details>
  <wa-details id="details3" summary="Section 3">
    Content for section 3
  </wa-details>
</wa-mutation-observer>

<div id="status">
  <p>Open sections: <span id="openCount">0</span></p>
</div>

<script>
  const observer = document.getElementById('accordionObserver');
  const openCount = document.getElementById('openCount');

  function updateCount() {
    const expanded = observer.querySelectorAll('[aria-expanded="true"]');
    openCount.textContent = expanded.length;
  }

  observer.addEventListener('wa-mutation', (event) => {
    updateCount();
  });

  // Initial count
  updateCount();
</script>
```

### Auto-Save Indicator

```html
<wa-mutation-observer char-data id="editorObserver">
  <wa-textarea
    id="editor"
    label="Document Editor"
    rows="10"
    placeholder="Start typing..."
  ></wa-textarea>
</wa-mutation-observer>

<div id="saveStatus" style="margin-top: 1rem;">
  <wa-badge id="statusBadge" variant="neutral">Saved</wa-badge>
  <span id="lastSaved" style="margin-left: 0.5rem; font-size: 0.875rem; color: #64748b;">
    Just now
  </span>
</div>

<script>
  const observer = document.getElementById('editorObserver');
  const statusBadge = document.getElementById('statusBadge');
  const lastSaved = document.getElementById('lastSaved');
  let saveTimeout;

  observer.addEventListener('wa-mutation', (event) => {
    // Show "Unsaved changes" status
    statusBadge.variant = 'warning';
    statusBadge.textContent = 'Unsaved';

    // Clear existing timeout
    clearTimeout(saveTimeout);

    // Auto-save after 2 seconds of no changes
    saveTimeout = setTimeout(() => {
      // Simulate save
      console.log('Auto-saving content...');

      statusBadge.variant = 'success';
      statusBadge.textContent = 'Saved';
      lastSaved.textContent = new Date().toLocaleTimeString();
    }, 2000);
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| N/A | This component has no public methods | - |

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-mutation` | Fired when mutations are observed | `{ mutations: MutationRecord[] }` |

### Event Detail Structure

The `wa-mutation` event detail contains an array of `MutationRecord` objects with the following properties:

- `type`: Type of mutation (`'attributes'`, `'characterData'`, or `'childList'`)
- `target`: The node affected by the mutation
- `addedNodes`: NodeList of added nodes
- `removedNodes`: NodeList of removed nodes
- `previousSibling`: Previous sibling of added/removed nodes
- `nextSibling`: Next sibling of added/removed nodes
- `attributeName`: Name of changed attribute
- `attributeNamespace`: Namespace of changed attribute
- `oldValue`: Previous value (if tracking enabled)

### Event Examples

```javascript
const observer = document.querySelector('wa-mutation-observer');

// Listen for all mutations
observer.addEventListener('wa-mutation', (event) => {
  console.log('Mutations:', event.detail.mutations);
});

// Handle specific mutation types
observer.addEventListener('wa-mutation', (event) => {
  event.detail.mutations.forEach(mutation => {
    switch (mutation.type) {
      case 'attributes':
        console.log('Attribute changed:', mutation.attributeName);
        break;
      case 'childList':
        console.log('Children changed');
        break;
      case 'characterData':
        console.log('Text content changed');
        break;
    }
  });
});

// Track old values
observer.addEventListener('wa-mutation', (event) => {
  event.detail.mutations.forEach(mutation => {
    if (mutation.oldValue !== null) {
      console.log('Changed from:', mutation.oldValue);
      console.log('Changed to:', mutation.target.textContent);
    }
  });
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Elements to observe for mutations |

### Slot Examples

```html
<!-- Single element -->
<wa-mutation-observer>
  <div>Observed content</div>
</wa-mutation-observer>

<!-- Multiple elements -->
<wa-mutation-observer child-list>
  <div>Element 1</div>
  <div>Element 2</div>
  <div>Element 3</div>
</wa-mutation-observer>

<!-- Complex structure -->
<wa-mutation-observer attr child-list>
  <div id="container">
    <header>
      <h1>Title</h1>
    </header>
    <main>
      <p>Content</p>
    </main>
    <footer>
      <p>Footer</p>
    </footer>
  </div>
</wa-mutation-observer>
```

## CSS Parts

This component has no exposed CSS parts as it doesn't render visual content.

## Best Practices

- ✅ Be specific about what to observe (use `attr` to limit to specific attributes)
- ✅ Disable observation when not needed to improve performance
- ✅ Use `attr-old-value` only when you need previous values
- ✅ Debounce actions triggered by frequent mutations
- ✅ Clean up event listeners when done
- ❌ Don't observe more than necessary (impacts performance)
- ❌ Avoid creating infinite mutation loops
- ❌ Don't use for high-frequency changes without throttling

## Accessibility

The `<wa-mutation-observer>` component is a utility component and doesn't directly impact accessibility. However, when using it to track UI changes:

- Ensure important state changes are announced to screen readers
- Use ARIA live regions for dynamic content updates
- Don't rely solely on visual changes for important information

```html
<!-- Announce changes to screen readers -->
<wa-mutation-observer child-list>
  <div id="notifications" role="status" aria-live="polite" aria-atomic="true">
    <!-- Dynamic notifications -->
  </div>
</wa-mutation-observer>
```

## Troubleshooting

### Mutations Not Detected

**Problem:** The `wa-mutation` event is not firing

**Solution:** Ensure you've configured the correct observation type(s)

```html
<!-- ❌ No observation types specified -->
<wa-mutation-observer>
  <div id="content">Content</div>
</wa-mutation-observer>

<!-- ✅ Specify what to observe -->
<wa-mutation-observer attr child-list char-data>
  <div id="content">Content</div>
</wa-mutation-observer>
```

### Too Many Events

**Problem:** The `wa-mutation` event fires too frequently

**Solution:** Be more specific about what to observe or throttle your event handler

```javascript
// Throttle mutations
let throttleTimeout;
observer.addEventListener('wa-mutation', (event) => {
  if (throttleTimeout) return;

  throttleTimeout = setTimeout(() => {
    // Handle mutations
    console.log('Mutations:', event.detail.mutations);
    throttleTimeout = null;
  }, 100);
});
```

### Old Values Not Available

**Problem:** `mutation.oldValue` is null

**Solution:** Enable old value tracking with `attr-old-value` or `char-data-old-value`

```html
<!-- ❌ Old values not tracked -->
<wa-mutation-observer attr="class">
  <div>Content</div>
</wa-mutation-observer>

<!-- ✅ Track old values -->
<wa-mutation-observer attr="class" attr-old-value>
  <div>Content</div>
</wa-mutation-observer>
```

### Observer Not Working After Re-enable

**Problem:** Observer doesn't work after setting `disabled` back to false

**Solution:** Ensure the observer has content in its default slot

```javascript
const observer = document.querySelector('wa-mutation-observer');

// Disable
observer.disabled = true;

// Re-enable
observer.disabled = false;

// If issues persist, check if content still exists
console.log('Observed content:', observer.children.length);
```

## Related

- [Resize Observer](./resize-observer.md)
- [Intersection Observer](./intersection-observer.md)
- [Visually Hidden](./visually-hidden.md)
