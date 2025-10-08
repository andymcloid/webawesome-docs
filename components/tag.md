# Tag

Tags are small, compact elements used for labeling, categorizing, or organizing content.

## Overview

The `<wa-tag>` component provides a versatile label element with multiple variants, sizes, and interactive capabilities. Tags are perfect for displaying categories, filters, status indicators, or any compact piece of information.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/tag/tag.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default tag -->
<wa-tag>Tag</wa-tag>

<!-- Primary tag -->
<wa-tag variant="primary">Primary</wa-tag>

<!-- Removable tag -->
<wa-tag removable>Removable</wa-tag>

<!-- Pill-shaped tag -->
<wa-tag pill>Pill Tag</wa-tag>
```

## Variants

Tags support multiple visual variants to convey different meanings:

```html
<wa-tag variant="default">Default</wa-tag>
<wa-tag variant="primary">Primary</wa-tag>
<wa-tag variant="success">Success</wa-tag>
<wa-tag variant="neutral">Neutral</wa-tag>
<wa-tag variant="warning">Warning</wa-tag>
<wa-tag variant="danger">Danger</wa-tag>
```

## Sizes

Control tag size with the `size` attribute:

```html
<wa-tag size="small">Small</wa-tag>
<wa-tag size="medium">Medium (default)</wa-tag>
<wa-tag size="large">Large</wa-tag>
```

## Pill Shape

Make tags rounded with the `pill` attribute:

```html
<wa-tag pill>Pill Tag</wa-tag>
<wa-tag variant="primary" pill>Primary Pill</wa-tag>
<wa-tag variant="success" pill>Success Pill</wa-tag>
```

## Removable Tags

Add the `removable` attribute to allow users to dismiss tags:

```html
<wa-tag removable>Removable Tag</wa-tag>
<wa-tag variant="primary" removable>Remove Me</wa-tag>

<script>
  const tags = document.querySelectorAll('wa-tag[removable]');

  tags.forEach(tag => {
    tag.addEventListener('wa-remove', () => {
      tag.remove();
      console.log('Tag removed');
    });
  });
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `variant` | string | `'default'` | No | Tag variant: `default`, `primary`, `success`, `neutral`, `warning`, `danger` |
| `size` | string | `'medium'` | No | Tag size: `small`, `medium`, `large` |
| `pill` | boolean | `false` | No | Render tag with rounded ends |
| `removable` | boolean | `false` | No | Show remove button to allow dismissal |

## Examples

### Category Tags

```html
<div style="display: flex; gap: 0.5rem; flex-wrap: wrap;">
  <wa-tag variant="primary">JavaScript</wa-tag>
  <wa-tag variant="primary">TypeScript</wa-tag>
  <wa-tag variant="primary">Web Components</wa-tag>
  <wa-tag variant="primary">CSS</wa-tag>
  <wa-tag variant="primary">HTML</wa-tag>
</div>
```

### Status Indicators

```html
<div style="display: flex; gap: 0.5rem; align-items: center;">
  <wa-tag variant="success" pill>
    <wa-icon slot="start" name="check-circle"></wa-icon>
    Active
  </wa-tag>

  <wa-tag variant="warning" pill>
    <wa-icon slot="start" name="exclamation-circle"></wa-icon>
    Pending
  </wa-tag>

  <wa-tag variant="danger" pill>
    <wa-icon slot="start" name="x-circle"></wa-icon>
    Inactive
  </wa-tag>

  <wa-tag variant="neutral" pill>
    <wa-icon slot="start" name="clock"></wa-icon>
    Draft
  </wa-tag>
</div>
```

### Removable Filter Tags

```html
<div id="filterContainer" style="display: flex; gap: 0.5rem; flex-wrap: wrap;">
  <wa-tag removable pill data-filter="javascript">JavaScript</wa-tag>
  <wa-tag removable pill data-filter="python">Python</wa-tag>
  <wa-tag removable pill data-filter="react">React</wa-tag>
  <wa-tag removable pill data-filter="vue">Vue</wa-tag>
</div>

<script>
  const container = document.getElementById('filterContainer');
  const filters = new Set(['javascript', 'python', 'react', 'vue']);

  container.addEventListener('wa-remove', (event) => {
    const tag = event.target;
    const filter = tag.dataset.filter;

    filters.delete(filter);
    tag.remove();

    console.log('Active filters:', Array.from(filters));
    // Update your filtered content here
  });
</script>
```

### Tag Group with Icons

```html
<div style="display: flex; gap: 0.5rem; flex-wrap: wrap;">
  <wa-tag variant="primary">
    <wa-icon slot="start" name="star"></wa-icon>
    Featured
  </wa-tag>

  <wa-tag variant="success">
    <wa-icon slot="start" name="badge-check"></wa-icon>
    Verified
  </wa-tag>

  <wa-tag variant="warning">
    <wa-icon slot="start" name="flame"></wa-icon>
    Trending
  </wa-tag>

  <wa-tag variant="danger">
    <wa-icon slot="start" name="bolt"></wa-icon>
    Limited
  </wa-tag>
</div>
```

### Product Tags

```html
<wa-card>
  <div slot="header">
    <div style="display: flex; justify-content: space-between; align-items: center;">
      <h3>Premium Headphones</h3>
      <div style="display: flex; gap: 0.5rem;">
        <wa-tag variant="success" size="small" pill>In Stock</wa-tag>
        <wa-tag variant="danger" size="small" pill>Sale</wa-tag>
      </div>
    </div>
  </div>

  <img src="/headphones.jpg" alt="Headphones">

  <div style="padding: 1rem;">
    <p>High-quality wireless headphones with noise cancellation.</p>

    <div style="display: flex; gap: 0.5rem; margin-top: 1rem; flex-wrap: wrap;">
      <wa-tag size="small">Wireless</wa-tag>
      <wa-tag size="small">Bluetooth</wa-tag>
      <wa-tag size="small">Noise Cancelling</wa-tag>
      <wa-tag size="small">20h Battery</wa-tag>
    </div>
  </div>
</wa-card>
```

### User Skills

```html
<div class="user-profile">
  <h3>Skills</h3>
  <div id="skills" style="display: flex; gap: 0.5rem; flex-wrap: wrap;">
    <wa-tag variant="primary" pill removable>JavaScript</wa-tag>
    <wa-tag variant="primary" pill removable>Python</wa-tag>
    <wa-tag variant="primary" pill removable>React</wa-tag>
    <wa-tag variant="primary" pill removable>Node.js</wa-tag>
    <wa-tag variant="primary" pill removable>Docker</wa-tag>
  </div>

  <wa-button id="addSkill" style="margin-top: 1rem;">
    <wa-icon slot="start" name="plus"></wa-icon>
    Add Skill
  </wa-button>
</div>

<script>
  const skillsContainer = document.getElementById('skills');
  const addSkillButton = document.getElementById('addSkill');

  // Handle remove
  skillsContainer.addEventListener('wa-remove', (event) => {
    const tag = event.target;
    tag.style.opacity = '0';
    tag.style.transform = 'scale(0.8)';
    tag.style.transition = 'all 0.2s ease';

    setTimeout(() => {
      tag.remove();
    }, 200);
  });

  // Handle add (simplified)
  addSkillButton.addEventListener('click', () => {
    const skill = prompt('Enter skill name:');
    if (skill) {
      const tag = document.createElement('wa-tag');
      tag.setAttribute('variant', 'primary');
      tag.setAttribute('pill', '');
      tag.setAttribute('removable', '');
      tag.textContent = skill;
      skillsContainer.appendChild(tag);
    }
  });
</script>
```

### Email Recipients

```html
<div class="email-composer">
  <label>To:</label>
  <div id="recipients" style="display: flex; gap: 0.5rem; flex-wrap: wrap; padding: 0.5rem; border: 1px solid #e5e7eb; border-radius: 0.25rem;">
    <wa-tag removable>john@example.com</wa-tag>
    <wa-tag removable>jane@example.com</wa-tag>
    <wa-tag removable>bob@example.com</wa-tag>
  </div>
</div>

<script>
  const recipients = document.getElementById('recipients');

  recipients.addEventListener('wa-remove', (event) => {
    const email = event.target.textContent.trim();
    console.log('Removed recipient:', email);
    event.target.remove();
  });
</script>
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-remove` | Emitted when the remove button is clicked | - |

### Event Examples

```javascript
const tag = document.querySelector('wa-tag[removable]');

// Listen for remove event
tag.addEventListener('wa-remove', (event) => {
  console.log('Remove button clicked');

  // You can prevent the default behavior
  // and handle removal manually if needed
  event.preventDefault();

  // Custom removal logic
  if (confirm('Are you sure you want to remove this tag?')) {
    tag.remove();
  }
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Tag content/label |
| `start` | Content before the label (typically icons) |
| `end` | Content after the label (typically icons) |

### Slot Examples

```html
<!-- Icon before text -->
<wa-tag variant="primary">
  <wa-icon slot="start" name="star"></wa-icon>
  Featured
</wa-tag>

<!-- Icon after text -->
<wa-tag variant="success">
  Verified
  <wa-icon slot="end" name="badge-check"></wa-icon>
</wa-tag>

<!-- Icons on both sides -->
<wa-tag variant="warning">
  <wa-icon slot="start" name="exclamation-circle"></wa-icon>
  Warning
  <wa-icon slot="end" name="arrow-right"></wa-icon>
</wa-tag>
```

## CSS Parts

Use CSS parts to customize tag appearance:

```css
/* Style the base tag container */
wa-tag::part(base) {
  border-radius: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Style the tag content */
wa-tag::part(content) {
  font-weight: 600;
}

/* Style the remove button */
wa-tag::part(remove-button) {
  color: currentColor;
  opacity: 0.7;
}

wa-tag::part(remove-button):hover {
  opacity: 1;
}
```

## Customization

### Custom Colors

```css
/* Custom info variant */
wa-tag[variant="info"]::part(base) {
  background-color: #dbeafe;
  color: #1e40af;
  border: 1px solid #93c5fd;
}

/* Custom dark variant */
wa-tag.dark::part(base) {
  background-color: #1f2937;
  color: #f9fafb;
}
```

### Custom Sizing

```css
/* Extra small tags */
wa-tag.xs::part(base) {
  font-size: 0.625rem;
  padding: 0.125rem 0.375rem;
}

/* Extra large tags */
wa-tag.xl::part(base) {
  font-size: 1rem;
  padding: 0.5rem 1rem;
}
```

### Outlined Tags

```css
wa-tag.outline::part(base) {
  background-color: transparent;
  border: 2px solid currentColor;
}
```

## Best Practices

- ✅ Use consistent variants for similar types of information
- ✅ Combine tags with icons for better visual communication
- ✅ Use removable tags for interactive filters or selections
- ✅ Keep tag labels concise (1-3 words)
- ✅ Use pill shape for more modern, rounded appearance
- ❌ Don't use too many different variants on the same screen
- ❌ Avoid lengthy text in tags; use tooltips for additional info
- ❌ Don't make non-removable tags look interactive

## Accessibility

- Tags use appropriate semantic markup
- Removable tags include accessible remove buttons with aria-labels
- Icons should have appropriate aria-labels when used alone
- Use sufficient color contrast for tag variants
- Consider providing tooltips for abbreviated tag text

```html
<!-- Accessible removable tag -->
<wa-tag removable aria-label="JavaScript skill tag">
  JavaScript
</wa-tag>

<!-- Icon-only tag with label -->
<wa-tag aria-label="Verified">
  <wa-icon name="badge-check"></wa-icon>
</wa-tag>
```

## Troubleshooting

### Remove Button Not Working

**Problem:** Clicking the remove button doesn't trigger wa-remove event

**Solution:** Ensure you've added the `removable` attribute and are listening for the correct event

```javascript
// ✅ Correct
tag.addEventListener('wa-remove', (e) => {
  tag.remove();
});

// ❌ Wrong event name
tag.addEventListener('remove', (e) => {
  tag.remove();
});
```

### Tags Not Wrapping

**Problem:** Tags overflow instead of wrapping to next line

**Solution:** Ensure the container has `flex-wrap: wrap`

```html
<!-- ✅ Correct -->
<div style="display: flex; flex-wrap: wrap; gap: 0.5rem;">
  <wa-tag>Tag 1</wa-tag>
  <wa-tag>Tag 2</wa-tag>
  <wa-tag>Tag 3</wa-tag>
</div>
```

### Icon Alignment Issues

**Problem:** Icons don't align properly with text

**Solution:** Use the `start` or `end` slots for icons

```html
<!-- ✅ Correct -->
<wa-tag>
  <wa-icon slot="start" name="star"></wa-icon>
  Featured
</wa-tag>

<!-- ❌ May have alignment issues -->
<wa-tag>
  <wa-icon name="star"></wa-icon> Featured
</wa-tag>
```

## Related

- [Badge](./badge.md)
- [Chip](./chip.md)
- [Button](./button.md)
- [Icon](./icon.md)
- [Form Controls Guide](../guides/form-controls.md)
