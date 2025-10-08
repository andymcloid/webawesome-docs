# Card

Cards are containers that group related content and actions together.

## Overview

The `<wa-card>` component provides a versatile container for organizing content with optional header, image, body, and footer sections. Cards are perfect for displaying articles, products, user profiles, and other grouped content.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/card/card.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Basic card -->
<wa-card>
  <p>This is a simple card with default content.</p>
</wa-card>

<!-- Card with header -->
<wa-card>
  <div slot="header">Card Header</div>
  <p>Card content goes here.</p>
</wa-card>

<!-- Card with header and footer -->
<wa-card>
  <div slot="header">Card Title</div>
  <p>This card includes both a header and footer section.</p>
  <div slot="footer">
    <wa-button variant="primary">Action</wa-button>
  </div>
</wa-card>
```

## Card with Header

Add a header section using the `header` slot:

```html
<wa-card>
  <div slot="header">
    <h3>Product Name</h3>
    <p>Category: Electronics</p>
  </div>
  <p>Detailed product description and specifications.</p>
</wa-card>

<!-- Header with complex content -->
<wa-card>
  <div slot="header" style="display: flex; align-items: center; gap: 1rem;">
    <wa-avatar label="User Name" image="/avatar.jpg"></wa-avatar>
    <div>
      <strong>John Doe</strong>
      <div style="font-size: 0.875rem; color: var(--wa-color-neutral-600);">
        2 hours ago
      </div>
    </div>
  </div>
  <p>Card content with user information in the header.</p>
</wa-card>
```

## Card with Image

Use the `image` slot to add images to your card:

```html
<!-- Card with image -->
<wa-card>
  <img
    slot="image"
    src="/path/to/image.jpg"
    alt="Card image"
  />
  <div slot="header">Image Card</div>
  <p>This card features an image at the top.</p>
</wa-card>

<!-- Product card with image -->
<wa-card>
  <img
    slot="image"
    src="/product.jpg"
    alt="Product photo"
    style="width: 100%; height: 200px; object-fit: cover;"
  />
  <div slot="header">
    <h3>Wireless Headphones</h3>
  </div>
  <p>Premium noise-canceling headphones with 30-hour battery life.</p>
  <div slot="footer">
    <strong style="font-size: 1.25rem;">$299.99</strong>
  </div>
</wa-card>
```

## Card with Footer

Add action buttons or additional content using the `footer` slot:

```html
<!-- Card with action buttons -->
<wa-card>
  <div slot="header">Confirm Action</div>
  <p>Are you sure you want to proceed with this action?</p>
  <div slot="footer" style="display: flex; gap: 0.5rem; justify-content: flex-end;">
    <wa-button>Cancel</wa-button>
    <wa-button variant="primary">Confirm</wa-button>
  </div>
</wa-card>

<!-- Card with footer metadata -->
<wa-card>
  <div slot="header">Article Title</div>
  <p>Article content and summary text goes here.</p>
  <div slot="footer" style="display: flex; justify-content: space-between; align-items: center;">
    <span>5 min read</span>
    <wa-button variant="primary" outline size="small">Read More</wa-button>
  </div>
</wa-card>
```

## Card with Actions

Create interactive cards with multiple actions:

```html
<!-- Card with icon buttons -->
<wa-card>
  <div slot="header" style="display: flex; justify-content: space-between; align-items: center;">
    <h3>Settings</h3>
    <div style="display: flex; gap: 0.5rem;">
      <wa-button size="small" circle>
        <wa-icon name="pencil"></wa-icon>
      </wa-button>
      <wa-button size="small" circle variant="danger">
        <wa-icon name="trash"></wa-icon>
      </wa-button>
    </div>
  </div>
  <p>Configure your application settings and preferences.</p>
</wa-card>

<!-- Card with dropdown menu -->
<wa-card>
  <div slot="header" style="display: flex; justify-content: space-between; align-items: center;">
    <h3>Project Dashboard</h3>
    <wa-dropdown>
      <wa-button slot="trigger" size="small" circle>
        <wa-icon name="three-dots-vertical"></wa-icon>
      </wa-button>
      <wa-menu>
        <wa-menu-item>Edit</wa-menu-item>
        <wa-menu-item>Share</wa-menu-item>
        <wa-menu-item>Delete</wa-menu-item>
      </wa-menu>
    </wa-dropdown>
  </div>
  <p>View and manage your project details.</p>
</wa-card>
```

## Card Layouts

### Grid Layout

Create card grids for displaying multiple items:

```html
<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 1rem;">
  <wa-card>
    <div slot="header">Card 1</div>
    <p>First card content</p>
  </wa-card>

  <wa-card>
    <div slot="header">Card 2</div>
    <p>Second card content</p>
  </wa-card>

  <wa-card>
    <div slot="header">Card 3</div>
    <p>Third card content</p>
  </wa-card>
</div>
```

### Horizontal Layout

```html
<wa-card style="display: flex; flex-direction: row;">
  <img
    slot="image"
    src="/thumbnail.jpg"
    alt="Thumbnail"
    style="width: 150px; height: 150px; object-fit: cover;"
  />
  <div style="flex: 1; padding: 1rem;">
    <h3>Horizontal Card</h3>
    <p>Content displayed alongside the image.</p>
  </div>
</wa-card>
```

### Stacked Layout

```html
<div style="display: flex; flex-direction: column; gap: 1rem; max-width: 600px;">
  <wa-card>
    <div slot="header">First Item</div>
    <p>First item description</p>
  </wa-card>

  <wa-card>
    <div slot="header">Second Item</div>
    <p>Second item description</p>
  </wa-card>

  <wa-card>
    <div slot="header">Third Item</div>
    <p>Third item description</p>
  </wa-card>
</div>
```

## Configuration

### Props / Attributes

The card component primarily uses slots and does not have specific attributes. All customization is done through slots and CSS styling.

## Examples

### User Profile Card

```html
<wa-card style="max-width: 400px;">
  <img
    slot="image"
    src="/cover.jpg"
    alt="Profile cover"
    style="width: 100%; height: 150px; object-fit: cover;"
  />
  <div style="text-align: center; margin-top: -40px;">
    <wa-avatar
      label="Jane Smith"
      image="/avatar.jpg"
      style="--size: 80px; border: 4px solid white;"
    ></wa-avatar>
    <h2 style="margin: 0.5rem 0;">Jane Smith</h2>
    <p style="color: var(--wa-color-neutral-600);">Product Designer</p>
  </div>
  <div slot="footer" style="display: flex; gap: 0.5rem;">
    <wa-button variant="primary" style="flex: 1;">Follow</wa-button>
    <wa-button style="flex: 1;">Message</wa-button>
  </div>
</wa-card>
```

### Product Card

```html
<wa-card style="max-width: 350px;">
  <img
    slot="image"
    src="/product.jpg"
    alt="Product"
    style="width: 100%; height: 250px; object-fit: cover;"
  />
  <div slot="header">
    <h3 style="margin: 0;">Wireless Keyboard</h3>
    <div style="display: flex; align-items: center; gap: 0.5rem; margin-top: 0.25rem;">
      <wa-rating value="4.5" readonly></wa-rating>
      <span style="font-size: 0.875rem; color: var(--wa-color-neutral-600);">(128 reviews)</span>
    </div>
  </div>
  <p>Mechanical switches with customizable RGB lighting. Compatible with all devices.</p>
  <div slot="footer" style="display: flex; justify-content: space-between; align-items: center;">
    <strong style="font-size: 1.5rem; color: var(--wa-color-primary-600);">$89.99</strong>
    <wa-button variant="primary">
      <wa-icon slot="start" name="cart"></wa-icon>
      Add to Cart
    </wa-button>
  </div>
</wa-card>
```

### Article Card

```html
<wa-card>
  <img
    slot="image"
    src="/article.jpg"
    alt="Article cover"
    style="width: 100%; height: 200px; object-fit: cover;"
  />
  <div slot="header">
    <span style="color: var(--wa-color-primary-600); font-size: 0.875rem; font-weight: 600;">
      TECHNOLOGY
    </span>
    <h2 style="margin: 0.5rem 0;">Getting Started with Web Components</h2>
    <div style="display: flex; align-items: center; gap: 1rem; font-size: 0.875rem; color: var(--wa-color-neutral-600);">
      <span>By John Doe</span>
      <span>•</span>
      <span>March 15, 2025</span>
      <span>•</span>
      <span>5 min read</span>
    </div>
  </div>
  <p>
    Learn how to build reusable, encapsulated components using modern web standards.
    This comprehensive guide covers everything from basic concepts to advanced patterns.
  </p>
  <div slot="footer">
    <wa-button variant="primary" outline>Read More</wa-button>
  </div>
</wa-card>
```

### Notification Card

```html
<wa-card style="max-width: 400px;">
  <div slot="header" style="display: flex; align-items: center; gap: 1rem;">
    <wa-icon name="bell" style="color: var(--wa-color-warning-600); font-size: 1.5rem;"></wa-icon>
    <div style="flex: 1;">
      <strong>New Notification</strong>
      <div style="font-size: 0.875rem; color: var(--wa-color-neutral-600);">
        2 minutes ago
      </div>
    </div>
    <wa-button size="small" circle>
      <wa-icon name="x"></wa-icon>
    </wa-button>
  </div>
  <p>You have a new message from Sarah. Click to view details.</p>
  <div slot="footer">
    <wa-button variant="primary" size="small">View Message</wa-button>
  </div>
</wa-card>
```

### Statistics Card

```html
<wa-card>
  <div slot="header">
    <div style="display: flex; justify-content: space-between; align-items: center;">
      <h3 style="margin: 0;">Total Revenue</h3>
      <wa-icon name="currency-dollar" style="color: var(--wa-color-success-600);"></wa-icon>
    </div>
  </div>
  <div style="font-size: 2rem; font-weight: bold; color: var(--wa-color-neutral-900);">
    $45,231.89
  </div>
  <div style="display: flex; align-items: center; gap: 0.5rem; margin-top: 0.5rem;">
    <wa-icon name="arrow-up" style="color: var(--wa-color-success-600);"></wa-icon>
    <span style="color: var(--wa-color-success-600); font-weight: 600;">+20.1%</span>
    <span style="color: var(--wa-color-neutral-600); font-size: 0.875rem;">from last month</span>
  </div>
</wa-card>
```

## Methods

The card component does not expose any public methods.

## Events

The card component does not emit any custom events. Standard DOM events like `click` can be used on the card element.

```javascript
const card = document.querySelector('wa-card');

card.addEventListener('click', () => {
  console.log('Card clicked');
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | The main content area of the card |
| `header` | Optional header section at the top of the card |
| `image` | Optional image section, typically displayed above the header |
| `footer` | Optional footer section at the bottom of the card |

## CSS Parts

Use CSS parts to style internal card elements:

```css
/* Style the base card container */
wa-card::part(base) {
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Style the header section */
wa-card::part(header) {
  background-color: var(--wa-color-neutral-50);
  border-bottom: 2px solid var(--wa-color-neutral-200);
  padding: 1.5rem;
}

/* Style the body/content section */
wa-card::part(body) {
  padding: 2rem;
  font-size: 1rem;
  line-height: 1.6;
}

/* Style the image section */
wa-card::part(image) {
  overflow: hidden;
}

/* Style the footer section */
wa-card::part(footer) {
  background-color: var(--wa-color-neutral-50);
  border-top: 1px solid var(--wa-color-neutral-200);
  padding: 1rem 1.5rem;
}
```

## Customization

### Custom Styling

```css
/* Elevated card with shadow */
wa-card.elevated::part(base) {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
              0 4px 6px -2px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s, box-shadow 0.2s;
}

wa-card.elevated::part(base):hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
              0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

/* Bordered card */
wa-card.bordered::part(base) {
  border: 2px solid var(--wa-color-primary-600);
  box-shadow: none;
}

/* Compact card */
wa-card.compact::part(header),
wa-card.compact::part(body),
wa-card.compact::part(footer) {
  padding: 0.75rem;
}

/* Card with colored header */
wa-card.primary-header::part(header) {
  background-color: var(--wa-color-primary-600);
  color: white;
}
```

### Dark Card

```html
<wa-card class="dark">
  <div slot="header">Dark Card</div>
  <p>This card uses a dark theme.</p>
</wa-card>

<style>
  wa-card.dark::part(base) {
    background-color: var(--wa-color-neutral-900);
    color: var(--wa-color-neutral-100);
  }

  wa-card.dark::part(header) {
    background-color: var(--wa-color-neutral-800);
    border-bottom-color: var(--wa-color-neutral-700);
  }
</style>
```

### Gradient Card

```html
<wa-card class="gradient">
  <div slot="header">Featured Content</div>
  <p>This card features a gradient background.</p>
</wa-card>

<style>
  wa-card.gradient::part(base) {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
  }

  wa-card.gradient::part(header) {
    background: rgba(255, 255, 255, 0.1);
    border-bottom-color: rgba(255, 255, 255, 0.2);
  }
</style>
```

### Clickable Card

```html
<wa-card class="clickable" onclick="handleCardClick()">
  <div slot="header">Click Me</div>
  <p>This entire card is clickable.</p>
</wa-card>

<style>
  wa-card.clickable::part(base) {
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
  }

  wa-card.clickable::part(base):hover {
    transform: scale(1.02);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
  }

  wa-card.clickable::part(base):active {
    transform: scale(0.98);
  }
</style>
```

## Best Practices

- Use cards to group related content and actions
- Keep card content concise and focused
- Use consistent card layouts across your application
- Provide clear visual hierarchy with headers and footers
- Use images sparingly and ensure they are optimized
- Make cards responsive to different screen sizes
- Use appropriate spacing and padding for readability
- Avoid nesting cards within cards
- Use cards for content that users can scan quickly
- Include clear calls-to-action in card footers when needed

## Accessibility

- Ensure card content has sufficient color contrast
- Use semantic HTML within card slots (headings, paragraphs, etc.)
- Provide alt text for images in the image slot
- For clickable cards, ensure proper keyboard navigation:

```html
<wa-card tabindex="0" role="button" aria-label="View product details" onkeydown="handleKeyDown(event)">
  <div slot="header">Product Name</div>
  <p>Product description</p>
</wa-card>

<script>
  function handleKeyDown(event) {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      // Handle card interaction
    }
  }
</script>
```

- Use ARIA labels for icon-only actions in cards
- Ensure interactive elements within cards are keyboard accessible
- Use proper heading hierarchy in card headers

## Troubleshooting

### Card Not Displaying Correctly

**Problem:** Card appears broken or unstyled

**Solution:** Ensure the card component is properly imported and the autoloader is configured

```html
<!-- Verify component import -->
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

### Slots Not Rendering

**Problem:** Header, image, or footer slots are not appearing

**Solution:** Check that the `slot` attribute is correctly set

```html
<!-- Correct slot usage -->
<wa-card>
  <div slot="header">Header content</div>
  <p>Body content</p>
  <div slot="footer">Footer content</div>
</wa-card>

<!-- Incorrect - missing slot attribute -->
<wa-card>
  <div>This won't appear in the header</div>
</wa-card>
```

### Image Not Fitting Properly

**Problem:** Images appear stretched or cropped incorrectly

**Solution:** Use CSS object-fit and explicit dimensions

```html
<wa-card>
  <img
    slot="image"
    src="/image.jpg"
    alt="Card image"
    style="width: 100%; height: 200px; object-fit: cover;"
  />
  <p>Content</p>
</wa-card>
```

### Card Layout Issues

**Problem:** Card content overflows or doesn't align properly

**Solution:** Use flexbox or grid for complex layouts within card slots

```html
<wa-card>
  <div slot="footer" style="display: flex; justify-content: space-between; align-items: center;">
    <span>Left content</span>
    <wa-button>Right action</wa-button>
  </div>
</wa-card>
```

## Related

- [Avatar](./avatar.md)
- [Button](./button.md)
- [Icon](./icon.md)
- [Rating](./rating.md)
- [Dropdown](./dropdown.md)
