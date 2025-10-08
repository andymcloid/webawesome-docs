# Tab Group

Tab groups organize content into separate views where only one view is visible at a time.

## Overview

The `<wa-tab-group>` component provides a fully customizable tabbed interface with support for multiple placements, activation modes, and responsive layouts. It works together with `<wa-tab>` and `<wa-tab-panel>` components to create organized, accessible tabbed content.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tab-group/tab-group.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="general">General</wa-tab>
  <wa-tab slot="nav" panel="custom">Custom</wa-tab>
  <wa-tab slot="nav" panel="advanced">Advanced</wa-tab>

  <wa-tab-panel name="general">General content goes here</wa-tab-panel>
  <wa-tab-panel name="custom">Custom content goes here</wa-tab-panel>
  <wa-tab-panel name="advanced">Advanced content goes here</wa-tab-panel>
</wa-tab-group>
```

## Placements

Control tab placement with the `placement` attribute:

```html
<!-- Top placement (default) -->
<wa-tab-group placement="top">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>

<!-- Bottom placement -->
<wa-tab-group placement="bottom">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>

<!-- Start placement (vertical - left side) -->
<wa-tab-group placement="start">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>

<!-- End placement (vertical - right side) -->
<wa-tab-group placement="end">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>
```

## Activation Modes

Control when tab panels activate with the `activation` attribute:

```html
<!-- Auto activation (default) - activates on focus -->
<wa-tab-group activation="auto">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>

<!-- Manual activation - requires click or Enter/Space key -->
<wa-tab-group activation="manual">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>
```

## Vertical Tabs

Create vertical tab layouts using `start` or `end` placement:

```html
<wa-tab-group placement="start">
  <wa-tab slot="nav" panel="profile">
    <wa-icon slot="start" name="person"></wa-icon>
    Profile
  </wa-tab>
  <wa-tab slot="nav" panel="settings">
    <wa-icon slot="start" name="gear"></wa-icon>
    Settings
  </wa-tab>
  <wa-tab slot="nav" panel="security">
    <wa-icon slot="start" name="lock"></wa-icon>
    Security
  </wa-tab>

  <wa-tab-panel name="profile">
    <h3>Profile Settings</h3>
    <p>Manage your profile information here.</p>
  </wa-tab-panel>

  <wa-tab-panel name="settings">
    <h3>General Settings</h3>
    <p>Configure your preferences.</p>
  </wa-tab-panel>

  <wa-tab-panel name="security">
    <h3>Security Settings</h3>
    <p>Update your security options.</p>
  </wa-tab-panel>
</wa-tab-group>
```

## Closable Tabs

Enable closable tabs for dynamic content:

```html
<wa-tab-group id="closableTabs">
  <wa-tab slot="nav" panel="tab1" closable>Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2" closable>Tab 2</wa-tab>
  <wa-tab slot="nav" panel="tab3" closable>Tab 3</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
  <wa-tab-panel name="tab3">Content 3</wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('closableTabs');

  tabGroup.addEventListener('wa-tab-hide', (event) => {
    const tab = event.target;
    const panel = tabGroup.querySelector(`wa-tab-panel[name="${tab.panel}"]`);

    // Remove both tab and panel
    if (tab && panel) {
      tab.remove();
      panel.remove();
    }
  });
</script>
```

## Scrollable Tabs

When tabs overflow, they automatically become scrollable:

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="tab1">Dashboard</wa-tab>
  <wa-tab slot="nav" panel="tab2">Analytics</wa-tab>
  <wa-tab slot="nav" panel="tab3">Reports</wa-tab>
  <wa-tab slot="nav" panel="tab4">Settings</wa-tab>
  <wa-tab slot="nav" panel="tab5">Users</wa-tab>
  <wa-tab slot="nav" panel="tab6">Teams</wa-tab>
  <wa-tab slot="nav" panel="tab7">Projects</wa-tab>
  <wa-tab slot="nav" panel="tab8">Calendar</wa-tab>
  <wa-tab slot="nav" panel="tab9">Messages</wa-tab>
  <wa-tab slot="nav" panel="tab10">Notifications</wa-tab>

  <wa-tab-panel name="tab1">Dashboard content</wa-tab-panel>
  <wa-tab-panel name="tab2">Analytics content</wa-tab-panel>
  <wa-tab-panel name="tab3">Reports content</wa-tab-panel>
  <wa-tab-panel name="tab4">Settings content</wa-tab-panel>
  <wa-tab-panel name="tab5">Users content</wa-tab-panel>
  <wa-tab-panel name="tab6">Teams content</wa-tab-panel>
  <wa-tab-panel name="tab7">Projects content</wa-tab-panel>
  <wa-tab-panel name="tab8">Calendar content</wa-tab-panel>
  <wa-tab-panel name="tab9">Messages content</wa-tab-panel>
  <wa-tab-panel name="tab10">Notifications content</wa-tab-panel>
</wa-tab-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `placement` | string | `'top'` | No | Tab placement: `top`, `bottom`, `start`, `end` |
| `activation` | string | `'auto'` | No | Activation mode: `auto`, `manual` |
| `no-scroll-controls` | boolean | `false` | No | Disable scroll controls for overflow tabs |

## Examples

### Tabs with Icons and Badges

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="inbox">
    <wa-icon slot="start" name="inbox"></wa-icon>
    Inbox
    <wa-badge slot="end" variant="primary" pill>12</wa-badge>
  </wa-tab>

  <wa-tab slot="nav" panel="sent">
    <wa-icon slot="start" name="send"></wa-icon>
    Sent
  </wa-tab>

  <wa-tab slot="nav" panel="drafts">
    <wa-icon slot="start" name="file-text"></wa-icon>
    Drafts
    <wa-badge slot="end" variant="neutral" pill>3</wa-badge>
  </wa-tab>

  <wa-tab-panel name="inbox">
    <h3>Inbox Messages</h3>
    <p>You have 12 new messages.</p>
  </wa-tab-panel>

  <wa-tab-panel name="sent">
    <h3>Sent Messages</h3>
    <p>View your sent messages here.</p>
  </wa-tab-panel>

  <wa-tab-panel name="drafts">
    <h3>Draft Messages</h3>
    <p>You have 3 draft messages.</p>
  </wa-tab-panel>
</wa-tab-group>
```

### Dynamic Tab Creation

```html
<wa-button id="addTab">Add Tab</wa-button>

<wa-tab-group id="dynamicTabs">
  <wa-tab slot="nav" panel="tab1" closable>Tab 1</wa-tab>
  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('dynamicTabs');
  const addButton = document.getElementById('addTab');
  let tabCount = 1;

  addButton.addEventListener('click', () => {
    tabCount++;
    const tabId = `tab${tabCount}`;

    // Create new tab
    const tab = document.createElement('wa-tab');
    tab.setAttribute('slot', 'nav');
    tab.setAttribute('panel', tabId);
    tab.setAttribute('closable', '');
    tab.textContent = `Tab ${tabCount}`;

    // Create new panel
    const panel = document.createElement('wa-tab-panel');
    panel.setAttribute('name', tabId);
    panel.textContent = `Content ${tabCount}`;

    // Add to tab group
    tabGroup.appendChild(tab);
    tabGroup.appendChild(panel);

    // Activate new tab
    tab.click();
  });

  // Handle tab close
  tabGroup.addEventListener('wa-tab-hide', (event) => {
    const tab = event.target;
    const panel = tabGroup.querySelector(`wa-tab-panel[name="${tab.panel}"]`);

    if (tab && panel) {
      tab.remove();
      panel.remove();
    }
  });
</script>
```

### Tab Group with Form Content

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="account">Account Details</wa-tab>
  <wa-tab slot="nav" panel="preferences">Preferences</wa-tab>
  <wa-tab slot="nav" panel="notifications">Notifications</wa-tab>

  <wa-tab-panel name="account">
    <form>
      <wa-input label="Username" name="username" required></wa-input>
      <wa-input label="Email" name="email" type="email" required></wa-input>
      <wa-button type="submit" variant="primary">Save Changes</wa-button>
    </form>
  </wa-tab-panel>

  <wa-tab-panel name="preferences">
    <form>
      <wa-select label="Theme" name="theme">
        <wa-option value="light">Light</wa-option>
        <wa-option value="dark">Dark</wa-option>
        <wa-option value="auto">Auto</wa-option>
      </wa-select>
      <wa-select label="Language" name="language">
        <wa-option value="en">English</wa-option>
        <wa-option value="es">Spanish</wa-option>
        <wa-option value="fr">French</wa-option>
      </wa-select>
      <wa-button type="submit" variant="primary">Save Changes</wa-button>
    </form>
  </wa-tab-panel>

  <wa-tab-panel name="notifications">
    <form>
      <wa-switch name="email-notifications">Email Notifications</wa-switch>
      <wa-switch name="push-notifications">Push Notifications</wa-switch>
      <wa-switch name="sms-notifications">SMS Notifications</wa-switch>
      <wa-button type="submit" variant="primary">Save Changes</wa-button>
    </form>
  </wa-tab-panel>
</wa-tab-group>
```

### Programmatic Tab Control

```html
<wa-button-group>
  <wa-button id="showTab1">Show Tab 1</wa-button>
  <wa-button id="showTab2">Show Tab 2</wa-button>
  <wa-button id="showTab3">Show Tab 3</wa-button>
</wa-button-group>

<wa-tab-group id="controlledTabs">
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>
  <wa-tab slot="nav" panel="tab3">Tab 3</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
  <wa-tab-panel name="tab3">Content 3</wa-tab-panel>
</wa-tab-group>

<script>
  const tabGroup = document.getElementById('controlledTabs');

  document.getElementById('showTab1').addEventListener('click', () => {
    tabGroup.querySelector('[panel="tab1"]').click();
  });

  document.getElementById('showTab2').addEventListener('click', () => {
    tabGroup.querySelector('[panel="tab2"]').click();
  });

  document.getElementById('showTab3').addEventListener('click', () => {
    tabGroup.querySelector('[panel="tab3"]').click();
  });
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `show(panel)` | Shows the tab panel with the specified name | `void` |

### Method Examples

```javascript
const tabGroup = document.querySelector('wa-tab-group');

// Show specific panel
tabGroup.show('advanced');
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-tab-show` | Emitted when a tab is shown | `{ name: string }` |
| `wa-tab-hide` | Emitted when a tab is hidden | `{ name: string }` |

### Event Examples

```javascript
const tabGroup = document.querySelector('wa-tab-group');

// Listen for tab show
tabGroup.addEventListener('wa-tab-show', (event) => {
  console.log('Tab shown:', event.detail.name);
});

// Listen for tab hide
tabGroup.addEventListener('wa-tab-hide', (event) => {
  console.log('Tab hidden:', event.detail.name);
});
```

## Slots

| Slot | Description |
|------|-------------|
| `nav` | Tab buttons (wa-tab elements) |
| (default) | Tab panels (wa-tab-panel elements) |

## CSS Parts

Use CSS parts to style internal tab group elements:

```css
/* Style the base container */
wa-tab-group::part(base) {
  border: 1px solid #ccc;
}

/* Style the nav container */
wa-tab-group::part(nav) {
  background-color: #f5f5f5;
}

/* Style the tabs container */
wa-tab-group::part(tabs) {
  gap: 0.5rem;
}

/* Style the active tab indicator */
wa-tab-group::part(active-tab-indicator) {
  background-color: #6366f1;
  height: 3px;
}

/* Style the body container */
wa-tab-group::part(body) {
  padding: 1.5rem;
}

/* Style scroll buttons */
wa-tab-group::part(scroll-button) {
  color: #666;
}

wa-tab-group::part(scroll-button--start) {
  /* Styles for left/top scroll button */
}

wa-tab-group::part(scroll-button--end) {
  /* Styles for right/bottom scroll button */
}
```

## Customization

### Custom Tab Styles

```css
/* Customize tab appearance */
wa-tab::part(base) {
  background-color: transparent;
  border: 1px solid transparent;
  border-bottom: 2px solid transparent;
  transition: all 0.2s;
}

wa-tab::part(base):hover {
  background-color: rgba(0, 0, 0, 0.05);
}

wa-tab[active]::part(base) {
  border-bottom-color: #6366f1;
  color: #6366f1;
}
```

### Custom Panel Padding

```css
wa-tab-group::part(body) {
  padding: 2rem;
  background-color: #fafafa;
}
```

### Compact Vertical Tabs

```css
wa-tab-group[placement="start"] {
  --track-width: 200px;
}

wa-tab-group[placement="start"]::part(nav) {
  width: 200px;
}
```

## Best Practices

- Use clear, concise tab labels that describe the content
- Limit the number of tabs to 5-7 for better usability
- Use icons to enhance tab recognition
- Consider vertical tabs for narrow layouts or many tabs
- Use `activation="manual"` for tabs with heavy content loading
- Ensure tab panels have sufficient content to justify separate tabs
- Don't use tabs for sequential steps (use a stepper instead)
- Keep related content together in the same tab

## Accessibility

- Tab groups follow WAI-ARIA tab pattern
- Keyboard navigation with Arrow keys, Home, and End
- Tab key moves between tab list and panel content
- Active tab has `aria-selected="true"`
- Tab panels have appropriate `role="tabpanel"`
- Use `activation="manual"` for better accessibility with screen readers
- Ensure tab labels are descriptive for screen reader users
- Disabled tabs are excluded from keyboard navigation

## Troubleshooting

### Tabs Not Switching

**Problem:** Clicking tabs doesn't change panels

**Solution:** Ensure tab `panel` attribute matches panel `name` attribute

```html
<!-- Correct -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="settings">Content</wa-tab-panel>

<!-- Incorrect - names don't match -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="config">Content</wa-tab-panel>
```

### Panel Content Not Visible

**Problem:** Panel content is hidden or not displaying

**Solution:** Ensure panels are direct children of tab group and have unique names

```html
<!-- Correct -->
<wa-tab-group>
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <wa-tab-panel name="tab1">Content</wa-tab-panel>
</wa-tab-group>

<!-- Incorrect - panel wrapped in div -->
<wa-tab-group>
  <wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>
  <div>
    <wa-tab-panel name="tab1">Content</wa-tab-panel>
  </div>
</wa-tab-group>
```

### Scroll Buttons Not Appearing

**Problem:** Overflow tabs don't show scroll controls

**Solution:** Ensure container has defined width and `no-scroll-controls` is not set

```html
<!-- Tabs will scroll when they overflow -->
<wa-tab-group style="width: 400px;">
  <!-- Many tabs here -->
</wa-tab-group>
```

## Related

- [Tab](./tab.md)
- [Tab Panel](./tab-panel.md)
- [Card](./card.md)
- [Drawer](./drawer.md)
