# Tab Panel

Tab panels display content associated with a specific tab in a tab group.

## Overview

The `<wa-tab-panel>` component represents a content container that is shown or hidden based on the active tab in a `<wa-tab-group>`. Each panel corresponds to a specific tab and is identified by a unique name.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tab-panel/tab-panel.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="general">General</wa-tab>
  <wa-tab slot="nav" panel="settings">Settings</wa-tab>
  <wa-tab slot="nav" panel="advanced">Advanced</wa-tab>

  <wa-tab-panel name="general">
    <h3>General Settings</h3>
    <p>Configure general application settings here.</p>
  </wa-tab-panel>

  <wa-tab-panel name="settings">
    <h3>User Settings</h3>
    <p>Manage your user preferences and account settings.</p>
  </wa-tab-panel>

  <wa-tab-panel name="advanced">
    <h3>Advanced Options</h3>
    <p>Configure advanced features and options.</p>
  </wa-tab-panel>
</wa-tab-group>
```

## Panel Content

### Simple Text Content

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="about">About</wa-tab>
  <wa-tab slot="nav" panel="contact">Contact</wa-tab>

  <wa-tab-panel name="about">
    <h2>About Us</h2>
    <p>We are a company dedicated to building great products.</p>
  </wa-tab-panel>

  <wa-tab-panel name="contact">
    <h2>Contact Information</h2>
    <p>Email: contact@example.com</p>
    <p>Phone: (555) 123-4567</p>
  </wa-tab-panel>
</wa-tab-group>
```

### Form Content

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="login">Login</wa-tab>
  <wa-tab slot="nav" panel="signup">Sign Up</wa-tab>

  <wa-tab-panel name="login">
    <form>
      <wa-input label="Email" type="email" name="email" required></wa-input>
      <wa-input label="Password" type="password" name="password" required></wa-input>
      <wa-button type="submit" variant="primary">Login</wa-button>
    </form>
  </wa-tab-panel>

  <wa-tab-panel name="signup">
    <form>
      <wa-input label="Name" name="name" required></wa-input>
      <wa-input label="Email" type="email" name="email" required></wa-input>
      <wa-input label="Password" type="password" name="password" required></wa-input>
      <wa-button type="submit" variant="primary">Sign Up</wa-button>
    </form>
  </wa-tab-panel>
</wa-tab-group>
```

### Rich Content

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="overview">Overview</wa-tab>
  <wa-tab slot="nav" panel="details">Details</wa-tab>

  <wa-tab-panel name="overview">
    <wa-card>
      <div slot="header">
        <h3>Product Overview</h3>
      </div>
      <p>This product offers amazing features and benefits.</p>
      <ul>
        <li>Feature 1: High performance</li>
        <li>Feature 2: Easy to use</li>
        <li>Feature 3: Affordable pricing</li>
      </ul>
    </wa-card>
  </wa-tab-panel>

  <wa-tab-panel name="details">
    <wa-card>
      <div slot="header">
        <h3>Technical Details</h3>
      </div>
      <dl>
        <dt>Dimensions</dt>
        <dd>10" x 8" x 2"</dd>

        <dt>Weight</dt>
        <dd>2.5 lbs</dd>

        <dt>Material</dt>
        <dd>Premium aluminum</dd>
      </dl>
    </wa-card>
  </wa-tab-panel>
</wa-tab-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `name` | string | - | Yes | Unique identifier that matches the tab's `panel` attribute |
| `active` | boolean | `false` | No | Whether the panel is currently visible |

## Examples

### Dynamic Panel Content

```html
<wa-tab-group id="dynamicContent">
  <wa-tab slot="nav" panel="data1">Data 1</wa-tab>
  <wa-tab slot="nav" panel="data2">Data 2</wa-tab>
  <wa-tab slot="nav" panel="data3">Data 3</wa-tab>

  <wa-tab-panel name="data1" id="panel1">
    <p>Loading...</p>
  </wa-tab-panel>

  <wa-tab-panel name="data2" id="panel2">
    <p>Loading...</p>
  </wa-tab-panel>

  <wa-tab-panel name="data3" id="panel3">
    <p>Loading...</p>
  </wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('dynamicContent');

  tabGroup.addEventListener('wa-tab-show', async (event) => {
    const panelName = event.detail.name;
    const panel = document.getElementById(`panel${panelName.slice(-1)}`);

    // Load content dynamically
    try {
      const response = await fetch(`/api/data/${panelName}`);
      const data = await response.json();
      panel.innerHTML = `<pre>${JSON.stringify(data, null, 2)}</pre>`;
    } catch (error) {
      panel.innerHTML = `<p>Error loading data: ${error.message}</p>`;
    }
  });
</script>
```

### Lazy Loading Panel Content

```html
<wa-tab-group id="lazyTabs">
  <wa-tab slot="nav" panel="images">Images</wa-tab>
  <wa-tab slot="nav" panel="videos">Videos</wa-tab>
  <wa-tab slot="nav" panel="documents">Documents</wa-tab>

  <wa-tab-panel name="images">
    <!-- Content loaded when tab is activated -->
  </wa-tab-panel>

  <wa-tab-panel name="videos">
    <!-- Content loaded when tab is activated -->
  </wa-tab-panel>

  <wa-tab-panel name="documents">
    <!-- Content loaded when tab is activated -->
  </wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('lazyTabs');
  const loadedPanels = new Set();

  tabGroup.addEventListener('wa-tab-show', (event) => {
    const panelName = event.detail.name;

    // Only load content once
    if (loadedPanels.has(panelName)) return;

    const panel = tabGroup.querySelector(`wa-tab-panel[name="${panelName}"]`);

    // Load content based on panel type
    switch (panelName) {
      case 'images':
        panel.innerHTML = '<div class="image-grid"><!-- Images here --></div>';
        break;
      case 'videos':
        panel.innerHTML = '<div class="video-grid"><!-- Videos here --></div>';
        break;
      case 'documents':
        panel.innerHTML = '<div class="document-list"><!-- Documents here --></div>';
        break;
    }

    loadedPanels.add(panelName);
  });
</script>
```

### Panel with Loading State

```html
<wa-tab-group id="loadingTabs">
  <wa-tab slot="nav" panel="dashboard">Dashboard</wa-tab>
  <wa-tab slot="nav" panel="analytics">Analytics</wa-tab>

  <wa-tab-panel name="dashboard">
    <div id="dashboardContent">
      <wa-spinner></wa-spinner>
      <p>Loading dashboard...</p>
    </div>
  </wa-tab-panel>

  <wa-tab-panel name="analytics">
    <div id="analyticsContent">
      <wa-spinner></wa-spinner>
      <p>Loading analytics...</p>
    </div>
  </wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('loadingTabs');

  tabGroup.addEventListener('wa-tab-show', async (event) => {
    const panelName = event.detail.name;
    const contentDiv = document.getElementById(`${panelName}Content`);

    try {
      const response = await fetch(`/api/${panelName}`);
      const data = await response.json();

      contentDiv.innerHTML = `
        <h3>${panelName.charAt(0).toUpperCase() + panelName.slice(1)}</h3>
        <div>${renderData(data)}</div>
      `;
    } catch (error) {
      contentDiv.innerHTML = `
        <wa-alert variant="danger">
          <wa-icon slot="icon" name="alert-circle"></wa-icon>
          Failed to load ${panelName} data
        </wa-alert>
      `;
    }
  });

  function renderData(data) {
    // Render data based on structure
    return `<pre>${JSON.stringify(data, null, 2)}</pre>`;
  }
</script>
```

### Multi-Column Panel Layout

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="products">Products</wa-tab>
  <wa-tab slot="nav" panel="services">Services</wa-tab>

  <wa-tab-panel name="products">
    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem;">
      <wa-card>
        <h4>Product A</h4>
        <p>Description of product A</p>
        <wa-button variant="primary">Learn More</wa-button>
      </wa-card>

      <wa-card>
        <h4>Product B</h4>
        <p>Description of product B</p>
        <wa-button variant="primary">Learn More</wa-button>
      </wa-card>

      <wa-card>
        <h4>Product C</h4>
        <p>Description of product C</p>
        <wa-button variant="primary">Learn More</wa-button>
      </wa-card>
    </div>
  </wa-tab-panel>

  <wa-tab-panel name="services">
    <div style="display: flex; flex-direction: column; gap: 1rem;">
      <wa-card>
        <h4>Service 1</h4>
        <p>Professional consulting services</p>
      </wa-card>

      <wa-card>
        <h4>Service 2</h4>
        <p>Technical support and maintenance</p>
      </wa-card>
    </div>
  </wa-tab-panel>
</wa-tab-group>
```

### Nested Tab Groups

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="settings">Settings</wa-tab>
  <wa-tab slot="nav" panel="advanced">Advanced</wa-tab>

  <wa-tab-panel name="settings">
    <h3>Settings</h3>

    <wa-tab-group>
      <wa-tab slot="nav" panel="general">General</wa-tab>
      <wa-tab slot="nav" panel="privacy">Privacy</wa-tab>
      <wa-tab slot="nav" panel="notifications">Notifications</wa-tab>

      <wa-tab-panel name="general">
        <p>General settings options</p>
      </wa-tab-panel>

      <wa-tab-panel name="privacy">
        <p>Privacy settings options</p>
      </wa-tab-panel>

      <wa-tab-panel name="notifications">
        <p>Notification preferences</p>
      </wa-tab-panel>
    </wa-tab-group>
  </wa-tab-panel>

  <wa-tab-panel name="advanced">
    <h3>Advanced Settings</h3>
    <p>Advanced configuration options</p>
  </wa-tab-panel>
</wa-tab-group>
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The panel content |

## CSS Parts

Use CSS parts to style internal panel elements:

```css
/* Style the base panel */
wa-tab-panel::part(base) {
  padding: 1.5rem;
  background-color: #fafafa;
  border: 1px solid #e0e0e0;
  border-radius: 0 0 4px 4px;
}
```

## Customization

### Custom Panel Padding

```css
/* Add more padding to panels */
wa-tab-panel::part(base) {
  padding: 2rem;
}

/* Responsive padding */
@media (max-width: 768px) {
  wa-tab-panel::part(base) {
    padding: 1rem;
  }
}
```

### Custom Panel Background

```css
/* Light background for panels */
wa-tab-panel::part(base) {
  background-color: #f8f9fa;
}

/* Dark mode panels */
@media (prefers-color-scheme: dark) {
  wa-tab-panel::part(base) {
    background-color: #1a1a1a;
    color: #ffffff;
  }
}
```

### Panel with Border

```css
wa-tab-panel::part(base) {
  border: 2px solid #e0e0e0;
  border-top: none;
  border-radius: 0 0 8px 8px;
}
```

## Best Practices

- Use unique `name` attributes for each panel
- Ensure panel `name` matches corresponding tab's `panel` attribute
- Keep panel content organized and scannable
- Consider lazy loading for heavy content
- Use consistent padding and spacing across panels
- Provide loading states for dynamic content
- Handle errors gracefully in dynamic panels
- Keep panel content focused on the tab's topic

## Accessibility

- Panels have `role="tabpanel"` automatically applied
- Hidden panels are excluded from tab order
- Active panel has appropriate ARIA attributes
- Panel content is announced when tab is activated
- Ensure panel content maintains logical heading hierarchy
- Use semantic HTML within panels for better screen reader support

### Accessible Panel Headings

```html
<wa-tab-panel name="account">
  <h2>Account Settings</h2>
  <h3>Profile Information</h3>
  <p>Update your profile details</p>

  <h3>Password</h3>
  <p>Change your password</p>
</wa-tab-panel>
```

## Troubleshooting

### Panel Not Showing

**Problem:** Panel content doesn't display when tab is clicked

**Solution:** Ensure panel `name` matches tab's `panel` attribute exactly

```html
<!-- Correct -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="settings">Content</wa-tab-panel>

<!-- Incorrect - name mismatch -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="setting">Content</wa-tab-panel>
```

### Panel Content Cut Off

**Problem:** Panel content is clipped or not fully visible

**Solution:** Check container height and overflow settings

```css
/* Ensure panel can expand */
wa-tab-panel::part(base) {
  min-height: 200px;
  overflow: auto;
}
```

### Multiple Panels Active

**Problem:** Multiple panels showing at once

**Solution:** Ensure each panel has a unique `name` attribute

```html
<!-- Correct - unique names -->
<wa-tab-panel name="tab1">Content 1</wa-tab-panel>
<wa-tab-panel name="tab2">Content 2</wa-tab-panel>

<!-- Incorrect - duplicate names -->
<wa-tab-panel name="tab1">Content 1</wa-tab-panel>
<wa-tab-panel name="tab1">Content 2</wa-tab-panel>
```

## Related

- [Tab Group](./tab-group.md)
- [Tab](./tab.md)
- [Card](./card.md)
- [Spinner](./spinner.md)
