# Rating

Ratings allow users to view or provide feedback using a star-based scale.

## Overview

The `<wa-rating>` component provides an interactive star rating system with support for half-stars, custom precision, read-only mode, and hover states. It's perfect for product reviews, feedback forms, and displaying satisfaction scores.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/rating/rating.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default rating (5 stars, editable) -->
<wa-rating></wa-rating>

<!-- Rating with value -->
<wa-rating value="3"></wa-rating>

<!-- Read-only rating -->
<wa-rating value="4.5" readonly></wa-rating>

<!-- Disabled rating -->
<wa-rating value="3" disabled></wa-rating>
```

## Setting Values

Use the `value` attribute to set the current rating:

```html
<!-- Integer ratings -->
<wa-rating value="1"></wa-rating>
<wa-rating value="2"></wa-rating>
<wa-rating value="3"></wa-rating>
<wa-rating value="4"></wa-rating>
<wa-rating value="5"></wa-rating>

<!-- Decimal ratings (displays half-stars) -->
<wa-rating value="3.5"></wa-rating>
<wa-rating value="4.2"></wa-rating>
```

## Maximum Stars

Control the total number of stars with the `max` attribute:

```html
<!-- 3-star scale -->
<wa-rating max="3"></wa-rating>

<!-- 10-star scale -->
<wa-rating max="10"></wa-rating>

<!-- Custom scale -->
<wa-rating max="7" value="4"></wa-rating>
```

## Precision

Control how precise ratings can be with the `precision` attribute:

```html
<!-- Whole stars only (precision = 1, default) -->
<wa-rating precision="1"></wa-rating>

<!-- Half-star precision (precision = 0.5) -->
<wa-rating precision="0.5"></wa-rating>

<!-- Quarter-star precision (precision = 0.25) -->
<wa-rating precision="0.25"></wa-rating>

<!-- Any decimal value (precision = 0.1) -->
<wa-rating precision="0.1"></wa-rating>
```

## Read-Only Mode

Use the `readonly` attribute to display ratings without allowing changes:

```html
<!-- Display-only rating -->
<wa-rating value="4.5" readonly></wa-rating>

<!-- Product rating display -->
<div style="display: flex; align-items: center; gap: 0.5rem;">
  <wa-rating value="4.3" readonly></wa-rating>
  <span>4.3 out of 5 (127 reviews)</span>
</div>
```

## Disabled State

Disable interaction with the `disabled` attribute:

```html
<wa-rating value="3" disabled></wa-rating>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | number | `0` | No | Current rating value |
| `max` | number | `5` | No | Maximum rating (number of stars) |
| `precision` | number | `1` | No | Increment precision: `1` (whole), `0.5` (half), `0.25` (quarter), etc. |
| `readonly` | boolean | `false` | No | Make rating read-only (display only) |
| `disabled` | boolean | `false` | No | Disable rating interaction |

## Examples

### Product Review

```html
<wa-card>
  <div slot="header">
    <h3>Premium Headphones</h3>
  </div>

  <div style="padding: 1rem;">
    <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 1rem;">
      <wa-rating value="4.5" readonly></wa-rating>
      <span><strong>4.5</strong> (2,341 reviews)</span>
    </div>

    <p>High-quality wireless headphones with exceptional sound quality.</p>

    <wa-button variant="primary" style="margin-top: 1rem;">
      Add to Cart - $299.99
    </wa-button>
  </div>
</wa-card>
```

### Feedback Form

```html
<form id="feedbackForm">
  <h3>How would you rate your experience?</h3>

  <div style="margin: 1.5rem 0;">
    <label style="display: block; margin-bottom: 0.5rem;">
      Overall Satisfaction
    </label>
    <wa-rating id="satisfaction" precision="0.5"></wa-rating>
    <div id="satisfactionValue" style="margin-top: 0.5rem; color: #6b7280;"></div>
  </div>

  <div style="margin: 1.5rem 0;">
    <label style="display: block; margin-bottom: 0.5rem;">
      Product Quality
    </label>
    <wa-rating id="quality" precision="0.5"></wa-rating>
    <div id="qualityValue" style="margin-top: 0.5rem; color: #6b7280;"></div>
  </div>

  <div style="margin: 1.5rem 0;">
    <label style="display: block; margin-bottom: 0.5rem;">
      Customer Service
    </label>
    <wa-rating id="service" precision="0.5"></wa-rating>
    <div id="serviceValue" style="margin-top: 0.5rem; color: #6b7280;"></div>
  </div>

  <wa-button type="submit" variant="primary">Submit Feedback</wa-button>
</form>

<script>
  const form = document.getElementById('feedbackForm');
  const satisfaction = document.getElementById('satisfaction');
  const quality = document.getElementById('quality');
  const service = document.getElementById('service');

  // Update display values
  satisfaction.addEventListener('wa-change', (e) => {
    document.getElementById('satisfactionValue').textContent =
      e.detail.value ? `${e.detail.value} stars` : 'Not rated';
  });

  quality.addEventListener('wa-change', (e) => {
    document.getElementById('qualityValue').textContent =
      e.detail.value ? `${e.detail.value} stars` : 'Not rated';
  });

  service.addEventListener('wa-change', (e) => {
    document.getElementById('serviceValue').textContent =
      e.detail.value ? `${e.detail.value} stars` : 'Not rated';
  });

  // Handle form submission
  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const ratings = {
      satisfaction: satisfaction.value,
      quality: quality.value,
      service: service.value
    };

    console.log('Feedback submitted:', ratings);
    // Submit to your API
  });
</script>
```

### Review List

```html
<div class="reviews">
  <h3>Customer Reviews</h3>

  <div class="review" style="padding: 1rem; border: 1px solid #e5e7eb; border-radius: 0.5rem; margin-bottom: 1rem;">
    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 0.5rem;">
      <div>
        <strong>John Doe</strong>
        <wa-rating value="5" readonly style="margin-top: 0.25rem;"></wa-rating>
      </div>
      <span style="color: #6b7280; font-size: 0.875rem;">2 days ago</span>
    </div>
    <p>Excellent product! Exceeded my expectations in every way.</p>
  </div>

  <div class="review" style="padding: 1rem; border: 1px solid #e5e7eb; border-radius: 0.5rem; margin-bottom: 1rem;">
    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 0.5rem;">
      <div>
        <strong>Jane Smith</strong>
        <wa-rating value="4" readonly style="margin-top: 0.25rem;"></wa-rating>
      </div>
      <span style="color: #6b7280; font-size: 0.875rem;">1 week ago</span>
    </div>
    <p>Very good quality, but shipping took longer than expected.</p>
  </div>

  <div class="review" style="padding: 1rem; border: 1px solid #e5e7eb; border-radius: 0.5rem; margin-bottom: 1rem;">
    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 0.5rem;">
      <div>
        <strong>Bob Johnson</strong>
        <wa-rating value="5" readonly style="margin-top: 0.25rem;"></wa-rating>
      </div>
      <span style="color: #6b7280; font-size: 0.875rem;">2 weeks ago</span>
    </div>
    <p>Perfect! Would definitely recommend to friends.</p>
  </div>
</div>
```

### Interactive Rating with Hover Feedback

```html
<div style="text-align: center; padding: 2rem;">
  <h3>Rate this article</h3>
  <p id="ratingLabel" style="color: #6b7280; margin: 1rem 0;">Click to rate</p>
  <wa-rating id="articleRating" style="font-size: 2rem;"></wa-rating>
  <p id="ratingMessage" style="margin-top: 1rem; min-height: 1.5rem; font-weight: 500;"></p>
</div>

<script>
  const rating = document.getElementById('articleRating');
  const label = document.getElementById('ratingLabel');
  const message = document.getElementById('ratingMessage');

  const messages = {
    1: 'Poor',
    2: 'Fair',
    3: 'Good',
    4: 'Very Good',
    5: 'Excellent'
  };

  // Show message on hover
  rating.addEventListener('wa-hover', (e) => {
    const value = e.detail.value;
    if (value > 0) {
      label.textContent = messages[value];
    } else {
      label.textContent = rating.value ?
        `You rated: ${messages[rating.value]}` :
        'Click to rate';
    }
  });

  // Save rating on change
  rating.addEventListener('wa-change', (e) => {
    const value = e.detail.value;
    message.textContent = `Thank you for rating this article ${value} star${value !== 1 ? 's' : ''}!`;
    message.style.color = '#10b981';

    // Submit rating to your API
    console.log('Rating submitted:', value);
  });
</script>
```

### Rating Statistics

```html
<div class="rating-stats" style="max-width: 500px;">
  <h3>Customer Ratings</h3>

  <div style="display: flex; align-items: center; gap: 1rem; margin: 1.5rem 0;">
    <div style="font-size: 3rem; font-weight: bold;">4.3</div>
    <div style="flex: 1;">
      <wa-rating value="4.3" readonly></wa-rating>
      <div style="color: #6b7280; margin-top: 0.25rem;">Based on 1,234 reviews</div>
    </div>
  </div>

  <div style="display: flex; flex-direction: column; gap: 0.5rem;">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <span style="width: 60px;">5 stars</span>
      <div style="flex: 1; background: #e5e7eb; height: 8px; border-radius: 4px;">
        <div style="background: #fbbf24; height: 100%; width: 70%; border-radius: 4px;"></div>
      </div>
      <span style="width: 40px; text-align: right; color: #6b7280;">864</span>
    </div>

    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <span style="width: 60px;">4 stars</span>
      <div style="flex: 1; background: #e5e7eb; height: 8px; border-radius: 4px;">
        <div style="background: #fbbf24; height: 100%; width: 20%; border-radius: 4px;"></div>
      </div>
      <span style="width: 40px; text-align: right; color: #6b7280;">247</span>
    </div>

    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <span style="width: 60px;">3 stars</span>
      <div style="flex: 1; background: #e5e7eb; height: 8px; border-radius: 4px;">
        <div style="background: #fbbf24; height: 100%; width: 7%; border-radius: 4px;"></div>
      </div>
      <span style="width: 40px; text-align: right; color: #6b7280;">86</span>
    </div>

    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <span style="width: 60px;">2 stars</span>
      <div style="flex: 1; background: #e5e7eb; height: 8px; border-radius: 4px;">
        <div style="background: #fbbf24; height: 100%; width: 2%; border-radius: 4px;"></div>
      </div>
      <span style="width: 40px; text-align: right; color: #6b7280;">25</span>
    </div>

    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <span style="width: 60px;">1 star</span>
      <div style="flex: 1; background: #e5e7eb; height: 8px; border-radius: 4px;">
        <div style="background: #fbbf24; height: 100%; width: 1%; border-radius: 4px;"></div>
      </div>
      <span style="width: 40px; text-align: right; color: #6b7280;">12</span>
    </div>
  </div>
</div>
```

### Clear Rating Option

```html
<div style="display: flex; align-items: center; gap: 1rem;">
  <wa-rating id="clearableRating" value="3"></wa-rating>
  <wa-button id="clearButton" size="small">Clear</wa-button>
</div>

<script>
  const rating = document.getElementById('clearableRating');
  const clearButton = document.getElementById('clearButton');

  clearButton.addEventListener('click', () => {
    rating.value = 0;
  });

  rating.addEventListener('wa-change', (e) => {
    console.log('New rating:', e.detail.value);
  });
</script>
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-change` | Emitted when the rating value changes | `{ value: number }` |
| `wa-hover` | Emitted when hovering over a star | `{ value: number }` |

### Event Examples

```javascript
const rating = document.querySelector('wa-rating');

// Handle rating changes
rating.addEventListener('wa-change', (event) => {
  console.log('Rating changed to:', event.detail.value);

  // Send to API
  fetch('/api/ratings', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ rating: event.detail.value })
  });
});

// Handle hover for preview
rating.addEventListener('wa-hover', (event) => {
  const value = event.detail.value;

  if (value > 0) {
    console.log('Hovering over star:', value);
    // Show preview text
  } else {
    console.log('Not hovering');
    // Hide preview text
  }
});
```

## CSS Parts

Use CSS parts to customize the rating appearance:

```css
/* Style the base container */
wa-rating::part(base) {
  gap: 0.25rem;
}

/* Style individual stars */
wa-rating::part(symbol) {
  color: #fbbf24;
  transition: all 0.2s ease;
}

wa-rating::part(symbol):hover {
  transform: scale(1.2);
}

/* Style inactive stars */
wa-rating::part(symbol--inactive) {
  color: #d1d5db;
}
```

## Customization

### Custom Star Color

```css
/* Gold stars */
wa-rating.gold::part(symbol) {
  color: #f59e0b;
}

/* Red hearts */
wa-rating.hearts::part(symbol) {
  color: #ef4444;
}
```

### Custom Size

```css
/* Large rating */
wa-rating.large {
  font-size: 2rem;
}

/* Small rating */
wa-rating.small {
  font-size: 0.875rem;
}
```

### Custom Symbol

```css
/* Use hearts instead of stars */
wa-rating.hearts::part(symbol)::before {
  content: '♥';
}
```

## Best Practices

- ✅ Use read-only mode when displaying existing ratings
- ✅ Provide visual feedback on hover for interactive ratings
- ✅ Show the numeric value alongside the visual stars
- ✅ Use appropriate precision for your use case (0.5 for most cases)
- ✅ Include the number of reviews for context
- ❌ Don't use too many stars (5-10 max is recommended)
- ❌ Avoid using ratings for yes/no or binary choices
- ❌ Don't hide the rating value from screen readers

## Accessibility

- Ratings include appropriate ARIA labels and roles
- Keyboard navigation is supported (arrow keys to change rating)
- Screen readers announce the current rating value
- Readonly ratings are properly marked for assistive technologies

```html
<!-- Accessible rating with label -->
<label id="productRating">Product Rating</label>
<wa-rating aria-labelledby="productRating" value="4"></wa-rating>

<!-- Accessible readonly rating -->
<wa-rating value="4.5" readonly aria-label="Average rating: 4.5 out of 5 stars"></wa-rating>
```

## Troubleshooting

### Rating Not Changing

**Problem:** Clicking stars doesn't update the rating

**Solution:** Ensure the rating is not readonly or disabled

```javascript
// Check and fix
const rating = document.querySelector('wa-rating');
rating.readonly = false;
rating.disabled = false;
```

### Decimal Values Not Showing

**Problem:** Setting value="4.5" shows 4 or 5 stars only

**Solution:** Set appropriate precision attribute

```html
<!-- ✅ Correct -->
<wa-rating value="4.5" precision="0.5"></wa-rating>

<!-- ❌ Won't show half-stars -->
<wa-rating value="4.5"></wa-rating>
```

### Events Not Firing

**Problem:** wa-change event doesn't fire

**Solution:** Ensure you're listening for the correct custom event

```javascript
// ✅ Correct
rating.addEventListener('wa-change', (e) => {
  console.log(e.detail.value);
});

// ❌ Wrong event name
rating.addEventListener('change', (e) => {
  console.log(e.detail.value);
});
```

## Related

- [Icon](./icon.md)
- [Form Controls](../guides/form-controls.md)
- [Input](./input.md)
- [Feedback Components](../guides/feedback-components.md)
