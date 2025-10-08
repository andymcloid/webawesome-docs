# Tab

Tabs are individual button controls used within a tab group to switch between different panels.

## Overview

The `<wa-tab>` component represents a single tab button within a `<wa-tab-group>`. It supports icons, badges, closable behavior, and various states. Tabs must be used in conjunction with a tab group and corresponding tab panels.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tab/tab.js';
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

  <wa-tab-panel name="general">General settings</wa-tab-panel>
  <wa-tab-panel name="settings">User settings</wa-tab-panel>
  <wa-tab-panel name="advanced">Advanced options</wa-tab-panel>
</wa-tab-group>
```

## States

### Active Tab

The `active` attribute marks a tab as selected:

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="tab1" active>Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>
  <wa-tab slot="nav" panel="tab3">Tab 3</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
  <wa-tab-panel name="tab3">Content 3</wa-tab-panel>
</wa-tab-group>
```

### Disabled Tab

Disable a tab to prevent user interaction:

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="tab1">Available</wa-tab>
  <wa-tab slot="nav" panel="tab2" disabled>Disabled</wa-tab>
  <wa-tab slot="nav" panel="tab3">Available</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
  <wa-tab-panel name="tab3">Content 3</wa-tab-panel>
</wa-tab-group>
```

### Closable Tab

Add a close button to tabs with the `closable` attribute:

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

  tabGroup.addEventListener('wa-close', (event) => {
    const tab = event.target;
    const panel = tabGroup.querySelector(`wa-tab-panel[name="${tab.panel}"]`);

    if (tab && panel) {
      tab.remove();
      panel.remove();
    }
  });
</script>
```

## Tabs with Icons

Add icons to tabs using the `start` or `end` slots:

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="home">
    <wa-icon slot="start" name="home"></wa-icon>
    Home
  </wa-tab>

  <wa-tab slot="nav" panel="profile">
    <wa-icon slot="start" name="person"></wa-icon>
    Profile
  </wa-tab>

  <wa-tab slot="nav" panel="settings">
    <wa-icon slot="start" name="gear"></wa-icon>
    Settings
  </wa-tab>

  <wa-tab-panel name="home">Home content</wa-tab-panel>
  <wa-tab-panel name="profile">Profile content</wa-tab-panel>
  <wa-tab-panel name="settings">Settings content</wa-tab-panel>
</wa-tab-group>
```

### Icon-Only Tabs

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="list" aria-label="List View">
    <wa-icon name="list"></wa-icon>
  </wa-tab>

  <wa-tab slot="nav" panel="grid" aria-label="Grid View">
    <wa-icon name="grid"></wa-icon>
  </wa-tab>

  <wa-tab slot="nav" panel="table" aria-label="Table View">
    <wa-icon name="table"></wa-icon>
  </wa-tab>

  <wa-tab-panel name="list">List view content</wa-tab-panel>
  <wa-tab-panel name="grid">Grid view content</wa-tab-panel>
  <wa-tab-panel name="table">Table view content</wa-tab-panel>
</wa-tab-group>
```

## Tabs with Badges

Add notification badges to indicate counts or status:

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="inbox">
    <wa-icon slot="start" name="inbox"></wa-icon>
    Inbox
    <wa-badge slot="end" variant="primary" pill>12</wa-badge>
  </wa-tab>

  <wa-tab slot="nav" panel="starred">
    <wa-icon slot="start" name="star"></wa-icon>
    Starred
    <wa-badge slot="end" variant="warning" pill>3</wa-badge>
  </wa-tab>

  <wa-tab slot="nav" panel="sent">
    <wa-icon slot="start" name="send"></wa-icon>
    Sent
  </wa-tab>

  <wa-tab-panel name="inbox">Inbox messages</wa-tab-panel>
  <wa-tab-panel name="starred">Starred messages</wa-tab-panel>
  <wa-tab-panel name="sent">Sent messages</wa-tab-panel>
</wa-tab-group>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `panel` | string | - | Yes | The name of the tab panel to control |
| `active` | boolean | `false` | No | Whether the tab is active |
| `closable` | boolean | `false` | No | Whether the tab can be closed |
| `disabled` | boolean | `false` | No | Whether the tab is disabled |

## Examples

### Tabs with Multiple Elements

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="tasks">
    <wa-icon slot="start" name="check-square"></wa-icon>
    Tasks
    <wa-badge slot="end" variant="danger" pill>5</wa-badge>
  </wa-tab>

  <wa-tab slot="nav" panel="messages">
    <wa-icon slot="start" name="message-circle"></wa-icon>
    Messages
    <wa-badge slot="end" variant="primary" pill>24</wa-badge>
  </wa-tab>

  <wa-tab slot="nav" panel="notifications">
    <wa-icon slot="start" name="bell"></wa-icon>
    Notifications
    <wa-badge slot="end" variant="warning" pill>8</wa-badge>
  </wa-tab>

  <wa-tab-panel name="tasks">Your tasks</wa-tab-panel>
  <wa-tab-panel name="messages">Your messages</wa-tab-panel>
  <wa-tab-panel name="notifications">Your notifications</wa-tab-panel>
</wa-tab-group>
```

### Programmatically Activating Tabs

```html
<wa-button id="activateTab2">Activate Tab 2</wa-button>

<wa-tab-group id="programmaticTabs">
  <wa-tab slot="nav" panel="tab1" id="tab1">Tab 1</wa-tab>
  <wa-tab slot="nav" panel="tab2" id="tab2">Tab 2</wa-tab>
  <wa-tab slot="nav" panel="tab3" id="tab3">Tab 3</wa-tab>

  <wa-tab-panel name="tab1">Content 1</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
  <wa-tab-panel name="tab3">Content 3</wa-tab-panel>
</wa-tab-group>

<script>
  const button = document.getElementById('activateTab2');
  const tab2 = document.getElementById('tab2');

  button.addEventListener('click', () => {
    tab2.click();
  });
</script>
```

### Dynamic Tab State

```html
<wa-button id="toggleDisabled">Toggle Disabled</wa-button>
<wa-button id="toggleClosable">Toggle Closable</wa-button>

<wa-tab-group>
  <wa-tab slot="nav" panel="tab1" id="dynamicTab">Dynamic Tab</wa-tab>
  <wa-tab slot="nav" panel="tab2">Tab 2</wa-tab>

  <wa-tab-panel name="tab1">Dynamic content</wa-tab-panel>
  <wa-tab-panel name="tab2">Content 2</wa-tab-panel>
</wa-tab-group>

<script>
  const tab = document.getElementById('dynamicTab');

  document.getElementById('toggleDisabled').addEventListener('click', () => {
    tab.disabled = !tab.disabled;
  });

  document.getElementById('toggleClosable').addEventListener('click', () => {
    tab.closable = !tab.closable;
  });
</script>
```

### Custom Tab Content

```html
<wa-tab-group>
  <wa-tab slot="nav" panel="user">
    <wa-avatar slot="start" image="/user.jpg" label="User"></wa-avatar>
    <div>
      <div style="font-weight: bold;">John Doe</div>
      <div style="font-size: 0.75rem; opacity: 0.7;">Admin</div>
    </div>
  </wa-tab>

  <wa-tab slot="nav" panel="team">
    <wa-avatar slot="start" initials="TM" label="Team"></wa-avatar>
    <div>
      <div style="font-weight: bold;">Team Settings</div>
      <div style="font-size: 0.75rem; opacity: 0.7;">5 members</div>
    </div>
  </wa-tab>

  <wa-tab-panel name="user">User profile settings</wa-tab-panel>
  <wa-tab-panel name="team">Team management</wa-tab-panel>
</wa-tab-group>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `focus(options?)` | Sets focus on the tab | `void` |
| `blur()` | Removes focus from the tab | `void` |

### Method Examples

```javascript
const tab = document.querySelector('wa-tab');

// Focus the tab
tab.focus();

// Focus without scrolling
tab.focus({ preventScroll: true });

// Remove focus
tab.blur();
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-close` | Emitted when the close button is clicked | - |

### Event Examples

```javascript
const tab = document.querySelector('wa-tab');

// Listen for close event
tab.addEventListener('wa-close', (event) => {
  console.log('Tab close requested');

  // Prevent default behavior if needed
  event.preventDefault();
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The tab label |
| `start` | Content before the label (typically icons) |
| `end` | Content after the label (typically badges) |

## CSS Parts

Use CSS parts to style internal tab elements:

```css
/* Style the base tab */
wa-tab::part(base) {
  padding: 1rem 1.5rem;
  background-color: transparent;
  border: none;
  border-bottom: 2px solid transparent;
  transition: all 0.2s;
}

/* Style hover state */
wa-tab::part(base):hover {
  background-color: rgba(0, 0, 0, 0.05);
}

/* Style active tab */
wa-tab[active]::part(base) {
  border-bottom-color: #6366f1;
  color: #6366f1;
}

/* Style the close button */
wa-tab::part(close-button) {
  color: #999;
  margin-left: 0.5rem;
}

wa-tab::part(close-button):hover {
  color: #666;
}
```

## Customization

### Custom Tab Appearance

```css
/* Pill-style tabs */
wa-tab::part(base) {
  border-radius: 2rem;
  border: 1px solid #e0e0e0;
  margin: 0 0.25rem;
}

wa-tab[active]::part(base) {
  background-color: #6366f1;
  color: white;
  border-color: #6366f1;
}
```

### Custom Active Indicator

```css
/* Underline active tab */
wa-tab::part(base) {
  position: relative;
  border-bottom: none;
}

wa-tab[active]::part(base)::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 3px;
  background-color: #6366f1;
}
```

### Compact Tabs

```css
wa-tab::part(base) {
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
}
```

## Best Practices

- Use clear, concise tab labels
- Provide `aria-label` for icon-only tabs
- Link each tab to its panel using the `panel` attribute
- Use badges to show notification counts
- Use icons to enhance recognition and scannability
- Don't overuse closable tabs - reserve for dynamic content
- Ensure disabled tabs communicate why they're unavailable
- Keep tab labels consistent in length and style

## Accessibility

- Tabs have appropriate ARIA roles and attributes
- Active state communicated via `aria-selected`
- Disabled tabs are properly announced to screen readers
- Keyboard navigation with Arrow keys
- Icon-only tabs must have `aria-label`
- Close buttons have accessible labels
- Focus management follows WAI-ARIA tab pattern

### Accessible Icon-Only Tabs

```html
<wa-tab slot="nav" panel="settings" aria-label="Settings">
  <wa-icon name="gear"></wa-icon>
</wa-tab>
```

## Troubleshooting

### Tab Not Linking to Panel

**Problem:** Clicking tab doesn't show panel

**Solution:** Ensure `panel` attribute matches panel `name`

```html
<!-- Correct -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="settings">Content</wa-tab-panel>

<!-- Incorrect - mismatch -->
<wa-tab slot="nav" panel="settings">Settings</wa-tab>
<wa-tab-panel name="config">Content</wa-tab-panel>
```

### Tab Not Showing in Group

**Problem:** Tab doesn't appear in tab group

**Solution:** Ensure tab has `slot="nav"` attribute

```html
<!-- Correct -->
<wa-tab slot="nav" panel="tab1">Tab 1</wa-tab>

<!-- Incorrect - missing slot -->
<wa-tab panel="tab1">Tab 1</wa-tab>
```

### Close Button Not Working

**Problem:** Close button doesn't trigger event

**Solution:** Listen for `wa-close` event on tab or parent element

```javascript
// Listen on individual tab
tab.addEventListener('wa-close', handleClose);

// Or listen on tab group (event bubbles)
tabGroup.addEventListener('wa-close', handleClose);
```

## Related

- [Tab Group](./tab-group.md)
- [Tab Panel](./tab-panel.md)
- [Badge](./badge.md)
- [Icon](./icon.md)
