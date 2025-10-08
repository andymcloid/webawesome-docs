# Skeleton

Skeletons display placeholder content while data is loading.

## Overview

The `<wa-skeleton>` component provides animated loading placeholders that give users visual feedback during content loading. Skeletons help reduce perceived loading time and improve the user experience by showing the structure of upcoming content.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/skeleton/skeleton.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Default skeleton (rectangular) -->
<wa-skeleton></wa-skeleton>

<!-- Text line skeleton -->
<wa-skeleton style="width: 200px; height: 1rem;"></wa-skeleton>

<!-- Circle skeleton (avatar) -->
<wa-skeleton shape="circle" style="width: 50px; height: 50px;"></wa-skeleton>

<!-- No animation -->
<wa-skeleton effect="none"></wa-skeleton>
```

## Shapes

Skeletons support different shapes for various content types:

```html
<!-- Rectangle (default) -->
<wa-skeleton style="width: 300px; height: 100px;"></wa-skeleton>

<!-- Circle (for avatars, icons) -->
<wa-skeleton shape="circle" style="width: 50px; height: 50px;"></wa-skeleton>
```

## Animation Effects

Control the loading animation with the `effect` attribute:

```html
<!-- Pulse effect (default) -->
<wa-skeleton effect="pulse"></wa-skeleton>

<!-- Sheen effect (shimmer) -->
<wa-skeleton effect="sheen"></wa-skeleton>

<!-- No animation -->
<wa-skeleton effect="none"></wa-skeleton>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `effect` | string | `'pulse'` | No | Animation effect: `pulse`, `sheen`, `none` |
| `shape` | string | `'rectangle'` | No | Skeleton shape: `rectangle`, `circle` |

## Examples

### Text Placeholder

```html
<div style="width: 400px;">
  <wa-skeleton style="width: 100%; height: 1.5rem; margin-bottom: 0.5rem;"></wa-skeleton>
  <wa-skeleton style="width: 90%; height: 1.5rem; margin-bottom: 0.5rem;"></wa-skeleton>
  <wa-skeleton style="width: 95%; height: 1.5rem; margin-bottom: 0.5rem;"></wa-skeleton>
  <wa-skeleton style="width: 80%; height: 1.5rem;"></wa-skeleton>
</div>
```

### Card Loading

```html
<wa-card style="width: 350px;">
  <div style="padding: 1rem;">
    <!-- Header with avatar and text -->
    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;">
      <wa-skeleton shape="circle" style="width: 50px; height: 50px;"></wa-skeleton>
      <div style="flex: 1;">
        <wa-skeleton style="width: 120px; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
        <wa-skeleton style="width: 80px; height: 0.875rem;"></wa-skeleton>
      </div>
    </div>

    <!-- Image -->
    <wa-skeleton style="width: 100%; height: 200px; margin-bottom: 1rem;"></wa-skeleton>

    <!-- Content lines -->
    <wa-skeleton style="width: 100%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
    <wa-skeleton style="width: 95%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
    <wa-skeleton style="width: 85%; height: 1rem;"></wa-skeleton>
  </div>
</wa-card>
```

### Profile Skeleton

```html
<div class="profile-skeleton" style="padding: 2rem;">
  <div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem;">
    <!-- Avatar -->
    <wa-skeleton shape="circle" style="width: 80px; height: 80px;"></wa-skeleton>

    <!-- Info -->
    <div style="flex: 1;">
      <wa-skeleton style="width: 150px; height: 1.5rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 200px; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 120px; height: 1rem;"></wa-skeleton>
    </div>
  </div>

  <!-- Bio -->
  <wa-skeleton style="width: 100%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
  <wa-skeleton style="width: 100%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
  <wa-skeleton style="width: 70%; height: 1rem; margin-bottom: 1.5rem;"></wa-skeleton>

  <!-- Stats -->
  <div style="display: flex; gap: 2rem;">
    <div>
      <wa-skeleton style="width: 60px; height: 1.5rem; margin-bottom: 0.25rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 0.875rem;"></wa-skeleton>
    </div>
    <div>
      <wa-skeleton style="width: 60px; height: 1.5rem; margin-bottom: 0.25rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 0.875rem;"></wa-skeleton>
    </div>
    <div>
      <wa-skeleton style="width: 60px; height: 1.5rem; margin-bottom: 0.25rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 0.875rem;"></wa-skeleton>
    </div>
  </div>
</div>
```

### List Loading

```html
<div style="width: 400px;">
  <!-- List item 1 -->
  <div style="display: flex; align-items: center; gap: 1rem; padding: 1rem; border-bottom: 1px solid #e5e7eb;">
    <wa-skeleton shape="circle" style="width: 40px; height: 40px;"></wa-skeleton>
    <div style="flex: 1;">
      <wa-skeleton style="width: 150px; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 100px; height: 0.875rem;"></wa-skeleton>
    </div>
  </div>

  <!-- List item 2 -->
  <div style="display: flex; align-items: center; gap: 1rem; padding: 1rem; border-bottom: 1px solid #e5e7eb;">
    <wa-skeleton shape="circle" style="width: 40px; height: 40px;"></wa-skeleton>
    <div style="flex: 1;">
      <wa-skeleton style="width: 170px; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 120px; height: 0.875rem;"></wa-skeleton>
    </div>
  </div>

  <!-- List item 3 -->
  <div style="display: flex; align-items: center; gap: 1rem; padding: 1rem; border-bottom: 1px solid #e5e7eb;">
    <wa-skeleton shape="circle" style="width: 40px; height: 40px;"></wa-skeleton>
    <div style="flex: 1;">
      <wa-skeleton style="width: 130px; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 90px; height: 0.875rem;"></wa-skeleton>
    </div>
  </div>
</div>
```

### Product Grid Loading

```html
<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; padding: 1rem;">
  <!-- Product 1 -->
  <wa-card>
    <wa-skeleton style="width: 100%; height: 200px; margin-bottom: 1rem;"></wa-skeleton>
    <div style="padding: 1rem;">
      <wa-skeleton style="width: 100%; height: 1.25rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 70%; height: 1rem; margin-bottom: 1rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
    </div>
  </wa-card>

  <!-- Product 2 -->
  <wa-card>
    <wa-skeleton style="width: 100%; height: 200px; margin-bottom: 1rem;"></wa-skeleton>
    <div style="padding: 1rem;">
      <wa-skeleton style="width: 100%; height: 1.25rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 60%; height: 1rem; margin-bottom: 1rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
    </div>
  </wa-card>

  <!-- Product 3 -->
  <wa-card>
    <wa-skeleton style="width: 100%; height: 200px; margin-bottom: 1rem;"></wa-skeleton>
    <div style="padding: 1rem;">
      <wa-skeleton style="width: 100%; height: 1.25rem; margin-bottom: 0.5rem;"></wa-skeleton>
      <wa-skeleton style="width: 80%; height: 1rem; margin-bottom: 1rem;"></wa-skeleton>
      <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
    </div>
  </wa-card>
</div>
```

### Table Loading

```html
<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr style="border-bottom: 2px solid #e5e7eb;">
      <th style="padding: 1rem; text-align: left;">Name</th>
      <th style="padding: 1rem; text-align: left;">Email</th>
      <th style="padding: 1rem; text-align: left;">Status</th>
      <th style="padding: 1rem; text-align: left;">Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom: 1px solid #e5e7eb;">
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 120px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 180px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 100px; height: 1.5rem;"></wa-skeleton>
      </td>
    </tr>
    <tr style="border-bottom: 1px solid #e5e7eb;">
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 140px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 160px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 100px; height: 1.5rem;"></wa-skeleton>
      </td>
    </tr>
    <tr style="border-bottom: 1px solid #e5e7eb;">
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 100px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 170px; height: 1rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 80px; height: 1.5rem;"></wa-skeleton>
      </td>
      <td style="padding: 1rem;">
        <wa-skeleton style="width: 100px; height: 1.5rem;"></wa-skeleton>
      </td>
    </tr>
  </tbody>
</table>
```

### Dynamic Loading with Real Data

```html
<div id="userProfile">
  <!-- Skeleton shown initially -->
  <div id="skeleton" style="display: block;">
    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;">
      <wa-skeleton shape="circle" style="width: 60px; height: 60px;"></wa-skeleton>
      <div style="flex: 1;">
        <wa-skeleton style="width: 150px; height: 1.25rem; margin-bottom: 0.5rem;"></wa-skeleton>
        <wa-skeleton style="width: 200px; height: 1rem;"></wa-skeleton>
      </div>
    </div>
    <wa-skeleton style="width: 100%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
    <wa-skeleton style="width: 95%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
    <wa-skeleton style="width: 80%; height: 1rem;"></wa-skeleton>
  </div>

  <!-- Real content hidden initially -->
  <div id="content" style="display: none;">
    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;">
      <img id="avatar" src="" alt="Avatar" style="width: 60px; height: 60px; border-radius: 50%;">
      <div>
        <h3 id="name" style="margin: 0 0 0.25rem 0;"></h3>
        <p id="email" style="margin: 0; color: #6b7280;"></p>
      </div>
    </div>
    <p id="bio"></p>
  </div>
</div>

<script>
  // Simulate loading user data
  async function loadUserProfile() {
    const skeleton = document.getElementById('skeleton');
    const content = document.getElementById('content');

    try {
      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 2000));

      const userData = {
        name: 'Jane Doe',
        email: 'jane@example.com',
        avatar: '/path/to/avatar.jpg',
        bio: 'Software engineer passionate about web development and user experience design.'
      };

      // Update content
      document.getElementById('name').textContent = userData.name;
      document.getElementById('email').textContent = userData.email;
      document.getElementById('avatar').src = userData.avatar;
      document.getElementById('bio').textContent = userData.bio;

      // Swap skeleton with content
      skeleton.style.display = 'none';
      content.style.display = 'block';

    } catch (error) {
      console.error('Failed to load profile:', error);
    }
  }

  // Load on page load
  loadUserProfile();
</script>
```

### Progressive Loading

```html
<div id="articleList"></div>

<script>
  const articleList = document.getElementById('articleList');

  // Show skeletons
  function showSkeletons(count) {
    for (let i = 0; i < count; i++) {
      const skeleton = document.createElement('div');
      skeleton.className = 'article-skeleton';
      skeleton.style.cssText = 'padding: 1rem; border-bottom: 1px solid #e5e7eb;';
      skeleton.innerHTML = `
        <wa-skeleton style="width: 100%; height: 1.5rem; margin-bottom: 0.5rem;"></wa-skeleton>
        <wa-skeleton style="width: 90%; height: 1rem; margin-bottom: 0.5rem;"></wa-skeleton>
        <wa-skeleton style="width: 80%; height: 1rem;"></wa-skeleton>
      `;
      articleList.appendChild(skeleton);
    }
  }

  // Load articles
  async function loadArticles() {
    showSkeletons(5);

    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));

    // Remove skeletons
    document.querySelectorAll('.article-skeleton').forEach(el => el.remove());

    // Add real articles
    const articles = [
      { title: 'Getting Started with Web Components', excerpt: 'Learn the basics...' },
      { title: 'Advanced CSS Techniques', excerpt: 'Explore modern CSS...' },
      { title: 'JavaScript Best Practices', excerpt: 'Write cleaner code...' }
    ];

    articles.forEach(article => {
      const div = document.createElement('div');
      div.style.cssText = 'padding: 1rem; border-bottom: 1px solid #e5e7eb;';
      div.innerHTML = `
        <h3 style="margin: 0 0 0.5rem 0;">${article.title}</h3>
        <p style="margin: 0; color: #6b7280;">${article.excerpt}</p>
      `;
      articleList.appendChild(div);
    });
  }

  loadArticles();
</script>
```

## CSS Parts

Use CSS parts to customize skeleton appearance:

```css
/* Style the base skeleton */
wa-skeleton::part(base) {
  background-color: #f3f4f6;
  border-radius: 0.375rem;
}

/* Customize pulse animation */
wa-skeleton[effect="pulse"]::part(base) {
  animation-duration: 2s;
}

/* Customize sheen effect */
wa-skeleton[effect="sheen"]::part(indicator) {
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.8),
    transparent
  );
}
```

## Customization

### Custom Colors

```css
/* Dark theme skeleton */
wa-skeleton.dark::part(base) {
  background-color: #374151;
}

/* Custom color scheme */
wa-skeleton.custom::part(base) {
  background-color: #e0e7ff;
}

wa-skeleton.custom[effect="sheen"]::part(indicator) {
  background: linear-gradient(
    90deg,
    transparent,
    rgba(99, 102, 241, 0.3),
    transparent
  );
}
```

### Custom Animation Speed

```css
/* Slow animation */
wa-skeleton.slow[effect="pulse"]::part(base) {
  animation-duration: 3s;
}

/* Fast animation */
wa-skeleton.fast[effect="pulse"]::part(base) {
  animation-duration: 1s;
}
```

### Rounded Corners

```css
/* Fully rounded */
wa-skeleton.rounded::part(base) {
  border-radius: 9999px;
}

/* Slightly rounded */
wa-skeleton.rounded-sm::part(base) {
  border-radius: 0.25rem;
}
```

## Best Practices

- ✅ Match skeleton layout to actual content structure
- ✅ Use appropriate shapes (circle for avatars, rectangle for text)
- ✅ Keep skeleton durations reasonable (1-3 seconds typical)
- ✅ Show skeletons immediately when loading starts
- ✅ Use consistent animation effects across your application
- ❌ Don't show skeletons for very fast-loading content (< 200ms)
- ❌ Avoid overly complex skeleton structures
- ❌ Don't use skeletons as permanent placeholders

## Accessibility

- Skeletons include `aria-busy="true"` and `aria-live="polite"`
- Use `aria-label` to describe what's loading
- Announce content completion to screen readers
- Ensure sufficient contrast for skeleton elements

```html
<!-- Accessible skeleton -->
<div aria-busy="true" aria-label="Loading user profile">
  <wa-skeleton shape="circle" style="width: 50px; height: 50px;"></wa-skeleton>
  <wa-skeleton style="width: 200px; height: 1rem;"></wa-skeleton>
</div>

<!-- After loading -->
<div aria-busy="false">
  <!-- Real content here -->
</div>
```

## Troubleshooting

### Skeleton Not Visible

**Problem:** Skeleton doesn't appear on the page

**Solution:** Ensure the skeleton has explicit width and height

```html
<!-- ✅ Correct -->
<wa-skeleton style="width: 200px; height: 1rem;"></wa-skeleton>

<!-- ❌ May not be visible -->
<wa-skeleton></wa-skeleton>
```

### Animation Not Working

**Problem:** Pulse or sheen effect doesn't animate

**Solution:** Check the `effect` attribute is set correctly

```html
<!-- ✅ Correct -->
<wa-skeleton effect="pulse"></wa-skeleton>
<wa-skeleton effect="sheen"></wa-skeleton>

<!-- ❌ Wrong value -->
<wa-skeleton effect="fade"></wa-skeleton>
```

### Layout Shift on Load

**Problem:** Content jumps when skeleton is replaced

**Solution:** Ensure skeleton dimensions match the actual content

```css
/* Reserve space exactly matching content */
.skeleton-container {
  min-height: 200px; /* Match expected content height */
}
```

### Circle Not Round

**Problem:** Circle skeleton appears oval-shaped

**Solution:** Ensure width and height are equal

```html
<!-- ✅ Correct -->
<wa-skeleton shape="circle" style="width: 50px; height: 50px;"></wa-skeleton>

<!-- ❌ Will be oval -->
<wa-skeleton shape="circle" style="width: 50px; height: 30px;"></wa-skeleton>
```

## Related

- [Spinner](./spinner.md)
- [Progress Bar](./progress-bar.md)
- [Card](./card.md)
- [Loading States Guide](../guides/loading-states.md)
