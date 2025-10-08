# Carousel

A carousel component for cycling through content like images, cards, or testimonials.

## Overview

The `<wa-carousel>` component creates an interactive slideshow for displaying a collection of content. It supports automatic playback, navigation controls, pagination indicators, and multiple slides per page. Use with `<wa-carousel-item>` elements to define individual slides.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/carousel/carousel.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple image carousel -->
<wa-carousel>
  <wa-carousel-item>
    <img src="image1.jpg" alt="Slide 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="image2.jpg" alt="Slide 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="image3.jpg" alt="Slide 3">
  </wa-carousel-item>
</wa-carousel>

<!-- Carousel with navigation -->
<wa-carousel navigation>
  <wa-carousel-item>
    <img src="product1.jpg" alt="Product 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="product2.jpg" alt="Product 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="product3.jpg" alt="Product 3">
  </wa-carousel-item>
</wa-carousel>
```

## Navigation

Enable navigation arrows with the `navigation` attribute:

```html
<wa-carousel navigation>
  <wa-carousel-item>
    <div style="background: #3498db; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 1</h2>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: #e74c3c; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 2</h2>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: #2ecc71; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 3</h2>
    </div>
  </wa-carousel-item>
</wa-carousel>
```

## Pagination

Show pagination dots with the `pagination` attribute:

```html
<wa-carousel pagination>
  <wa-carousel-item>
    <img src="hero1.jpg" alt="Hero Image 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="hero2.jpg" alt="Hero Image 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="hero3.jpg" alt="Hero Image 3">
  </wa-carousel-item>
</wa-carousel>
```

### Navigation and Pagination Together

```html
<wa-carousel navigation pagination>
  <wa-carousel-item>Content 1</wa-carousel-item>
  <wa-carousel-item>Content 2</wa-carousel-item>
  <wa-carousel-item>Content 3</wa-carousel-item>
</wa-carousel>
```

## Autoplay

Enable automatic slide transitions:

```html
<!-- Autoplay with default interval (3000ms) -->
<wa-carousel autoplay navigation pagination>
  <wa-carousel-item>
    <img src="banner1.jpg" alt="Banner 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="banner2.jpg" alt="Banner 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="banner3.jpg" alt="Banner 3">
  </wa-carousel-item>
</wa-carousel>

<!-- Custom autoplay interval (5 seconds) -->
<wa-carousel autoplay autoplay-interval="5000" navigation pagination>
  <wa-carousel-item>
    <img src="banner1.jpg" alt="Banner 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="banner2.jpg" alt="Banner 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="banner3.jpg" alt="Banner 3">
  </wa-carousel-item>
</wa-carousel>
```

## Loop

Enable continuous looping with the `loop` attribute:

```html
<wa-carousel loop navigation>
  <wa-carousel-item>
    <img src="slide1.jpg" alt="Slide 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="slide2.jpg" alt="Slide 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="slide3.jpg" alt="Slide 3">
  </wa-carousel-item>
</wa-carousel>
```

## Multiple Slides Per Page

Display multiple slides at once:

```html
<wa-carousel slides-per-page="3" navigation pagination>
  <wa-carousel-item>
    <img src="thumb1.jpg" alt="Thumbnail 1">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="thumb2.jpg" alt="Thumbnail 2">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="thumb3.jpg" alt="Thumbnail 3">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="thumb4.jpg" alt="Thumbnail 4">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="thumb5.jpg" alt="Thumbnail 5">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="thumb6.jpg" alt="Thumbnail 6">
  </wa-carousel-item>
</wa-carousel>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `loop` | boolean | `false` | No | Enable continuous looping |
| `navigation` | boolean | `false` | No | Show previous/next navigation buttons |
| `pagination` | boolean | `false` | No | Show pagination dots |
| `autoplay` | boolean | `false` | No | Enable automatic slide transitions |
| `autoplay-interval` | number | `3000` | No | Time between slide transitions in milliseconds |
| `slides-per-page` | number | `1` | No | Number of slides to display at once |

## Examples

### Image Gallery Carousel

```html
<wa-carousel navigation pagination loop style="--aspect-ratio: 16/9;">
  <wa-carousel-item>
    <img
      src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4"
      alt="Mountain landscape"
      style="width: 100%; height: 100%; object-fit: cover;">
  </wa-carousel-item>
  <wa-carousel-item>
    <img
      src="https://images.unsplash.com/photo-1511593358241-7eea1f3c84e5"
      alt="Desert dunes"
      style="width: 100%; height: 100%; object-fit: cover;">
  </wa-carousel-item>
  <wa-carousel-item>
    <img
      src="https://images.unsplash.com/photo-1469474968028-56623f02e42e"
      alt="Forest path"
      style="width: 100%; height: 100%; object-fit: cover;">
  </wa-carousel-item>
</wa-carousel>
```

### Product Showcase

```html
<wa-carousel navigation pagination slides-per-page="3" style="max-width: 1200px;">
  <wa-carousel-item>
    <wa-card>
      <img slot="image" src="product1.jpg" alt="Product 1">
      <h3>Wireless Headphones</h3>
      <p>$199.99</p>
      <wa-button slot="footer" variant="primary">Add to Cart</wa-button>
    </wa-card>
  </wa-carousel-item>
  <wa-carousel-item>
    <wa-card>
      <img slot="image" src="product2.jpg" alt="Product 2">
      <h3>Smart Watch</h3>
      <p>$299.99</p>
      <wa-button slot="footer" variant="primary">Add to Cart</wa-button>
    </wa-card>
  </wa-carousel-item>
  <wa-carousel-item>
    <wa-card>
      <img slot="image" src="product3.jpg" alt="Product 3">
      <h3>Laptop Stand</h3>
      <p>$49.99</p>
      <wa-button slot="footer" variant="primary">Add to Cart</wa-button>
    </wa-card>
  </wa-carousel-item>
  <wa-carousel-item>
    <wa-card>
      <img slot="image" src="product4.jpg" alt="Product 4">
      <h3>USB-C Hub</h3>
      <p>$79.99</p>
      <wa-button slot="footer" variant="primary">Add to Cart</wa-button>
    </wa-card>
  </wa-carousel-item>
</wa-carousel>
```

### Testimonial Carousel

```html
<wa-carousel
  autoplay
  autoplay-interval="6000"
  pagination
  loop
  style="max-width: 800px; margin: 0 auto;">
  <wa-carousel-item>
    <wa-card>
      <div style="text-align: center; padding: 2rem;">
        <wa-avatar
          image="https://i.pravatar.cc/150?img=1"
          label="Sarah Johnson"
          style="--size: 80px; margin-bottom: 1rem;">
        </wa-avatar>
        <p style="font-size: 1.125rem; font-style: italic; margin-bottom: 1rem;">
          "This product has completely transformed how we work. Highly recommended!"
        </p>
        <strong>Sarah Johnson</strong>
        <div style="color: #666;">CEO, TechCorp</div>
      </div>
    </wa-card>
  </wa-carousel-item>
  <wa-carousel-item>
    <wa-card>
      <div style="text-align: center; padding: 2rem;">
        <wa-avatar
          image="https://i.pravatar.cc/150?img=2"
          label="Michael Chen"
          style="--size: 80px; margin-bottom: 1rem;">
        </wa-avatar>
        <p style="font-size: 1.125rem; font-style: italic; margin-bottom: 1rem;">
          "Outstanding quality and excellent customer support. Five stars!"
        </p>
        <strong>Michael Chen</strong>
        <div style="color: #666;">Designer, Creative Studio</div>
      </div>
    </wa-card>
  </wa-carousel-item>
  <wa-carousel-item>
    <wa-card>
      <div style="text-align: center; padding: 2rem;">
        <wa-avatar
          image="https://i.pravatar.cc/150?img=3"
          label="Emily Rodriguez"
          style="--size: 80px; margin-bottom: 1rem;">
        </wa-avatar>
        <p style="font-size: 1.125rem; font-style: italic; margin-bottom: 1rem;">
          "Best investment we've made this year. Exceeded all expectations!"
        </p>
        <strong>Emily Rodriguez</strong>
        <div style="color: #666;">Marketing Director, StartupCo</div>
      </div>
    </wa-card>
  </wa-carousel-item>
</wa-carousel>
```

### Hero Banner with Autoplay

```html
<wa-carousel
  autoplay
  autoplay-interval="5000"
  navigation
  pagination
  loop
  style="--aspect-ratio: 21/9;">
  <wa-carousel-item>
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                height: 400px;
                display: flex;
                align-items: center;
                justify-content: center;
                color: white;
                text-align: center;
                padding: 2rem;">
      <div>
        <h1 style="font-size: 3rem; margin-bottom: 1rem;">Welcome to Our Platform</h1>
        <p style="font-size: 1.5rem; margin-bottom: 2rem;">Build amazing experiences</p>
        <wa-button variant="primary" size="large">Get Started</wa-button>
      </div>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
                height: 400px;
                display: flex;
                align-items: center;
                justify-content: center;
                color: white;
                text-align: center;
                padding: 2rem;">
      <div>
        <h1 style="font-size: 3rem; margin-bottom: 1rem;">Powerful Features</h1>
        <p style="font-size: 1.5rem; margin-bottom: 2rem;">Everything you need to succeed</p>
        <wa-button variant="primary" size="large">Learn More</wa-button>
      </div>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
                height: 400px;
                display: flex;
                align-items: center;
                justify-content: center;
                color: white;
                text-align: center;
                padding: 2rem;">
      <div>
        <h1 style="font-size: 3rem; margin-bottom: 1rem;">Join Thousands of Users</h1>
        <p style="font-size: 1.5rem; margin-bottom: 2rem;">Start your journey today</p>
        <wa-button variant="primary" size="large">Sign Up Free</wa-button>
      </div>
    </div>
  </wa-carousel-item>
</wa-carousel>
```

### Programmatic Control

```html
<wa-carousel id="myCarousel" navigation pagination>
  <wa-carousel-item>
    <div style="background: #3498db; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 1</h2>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: #e74c3c; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 2</h2>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: #2ecc71; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 3</h2>
    </div>
  </wa-carousel-item>
  <wa-carousel-item>
    <div style="background: #f39c12; height: 300px; display: flex; align-items: center; justify-content: center; color: white;">
      <h2>Slide 4</h2>
    </div>
  </wa-carousel-item>
</wa-carousel>

<div style="margin-top: 1rem; display: flex; gap: 1rem;">
  <wa-button id="prevBtn">Previous</wa-button>
  <wa-button id="nextBtn">Next</wa-button>
  <wa-button id="firstBtn">First</wa-button>
  <wa-button id="lastBtn">Last</wa-button>
</div>

<script>
  const carousel = document.getElementById('myCarousel');
  const prevBtn = document.getElementById('prevBtn');
  const nextBtn = document.getElementById('nextBtn');
  const firstBtn = document.getElementById('firstBtn');
  const lastBtn = document.getElementById('lastBtn');

  prevBtn.addEventListener('click', () => carousel.previous());
  nextBtn.addEventListener('click', () => carousel.next());
  firstBtn.addEventListener('click', () => carousel.goToSlide(0));
  lastBtn.addEventListener('click', () => carousel.goToSlide(3));
</script>
```

## Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `goToSlide(index)` | Navigate to a specific slide by index (0-based) | `void` |
| `next()` | Navigate to the next slide | `void` |
| `previous()` | Navigate to the previous slide | `void` |

### Method Examples

```javascript
const carousel = document.querySelector('wa-carousel');

// Navigate to specific slide
carousel.goToSlide(2); // Go to third slide

// Navigate to next slide
carousel.next();

// Navigate to previous slide
carousel.previous();

// Create custom thumbnail navigation
const thumbnails = document.querySelectorAll('.thumbnail');
thumbnails.forEach((thumb, index) => {
  thumb.addEventListener('click', () => {
    carousel.goToSlide(index);
  });
});

// Auto-advance with custom logic
let currentSlide = 0;
setInterval(() => {
  currentSlide = (currentSlide + 1) % 5; // Assuming 5 slides
  carousel.goToSlide(currentSlide);
}, 4000);
```

## Events

| Event | Description | Event Detail |
|-------|-------------|--------------|
| `wa-slide-change` | Emitted when the active slide changes | `{ index: number, slide: HTMLElement }` |

### Event Examples

```javascript
const carousel = document.querySelector('wa-carousel');

// Listen for slide changes
carousel.addEventListener('wa-slide-change', (event) => {
  console.log('Changed to slide:', event.detail.index);
  console.log('Slide element:', event.detail.slide);
});

// Update custom indicator
const indicator = document.getElementById('slideIndicator');
carousel.addEventListener('wa-slide-change', (event) => {
  indicator.textContent = `Slide ${event.detail.index + 1} of ${carousel.children.length}`;
});

// Track analytics
carousel.addEventListener('wa-slide-change', (event) => {
  // Send to analytics
  gtag('event', 'carousel_view', {
    slide_index: event.detail.index,
    slide_content: event.detail.slide.textContent
  });
});

// Sync with another carousel
const mainCarousel = document.getElementById('mainCarousel');
const thumbCarousel = document.getElementById('thumbCarousel');

mainCarousel.addEventListener('wa-slide-change', (event) => {
  thumbCarousel.goToSlide(event.detail.index);
});
```

## Slots

| Slot | Description |
|------|-------------|
| (default) | Carousel items (`wa-carousel-item` elements) |
| `navigation` | Custom navigation controls |
| `pagination` | Custom pagination indicators |

### Custom Navigation Example

```html
<wa-carousel>
  <wa-carousel-item>Slide 1</wa-carousel-item>
  <wa-carousel-item>Slide 2</wa-carousel-item>
  <wa-carousel-item>Slide 3</wa-carousel-item>

  <div slot="navigation" style="display: flex; gap: 0.5rem;">
    <wa-button circle size="small">
      <wa-icon name="chevron-left"></wa-icon>
    </wa-button>
    <wa-button circle size="small">
      <wa-icon name="chevron-right"></wa-icon>
    </wa-button>
  </div>
</wa-carousel>
```

## CSS Parts

Use CSS parts to style internal carousel elements:

```css
/* Style the carousel container */
wa-carousel::part(base) {
  border-radius: 8px;
  overflow: hidden;
}

/* Style the scroll container */
wa-carousel::part(scroll-container) {
  scroll-behavior: smooth;
}

/* Style navigation buttons */
wa-carousel::part(navigation-button) {
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
}

wa-carousel::part(navigation-button):hover {
  background-color: rgba(0, 0, 0, 0.7);
}

/* Style pagination dots */
wa-carousel::part(pagination) {
  padding: 1rem;
}

wa-carousel::part(pagination-item) {
  background-color: rgba(255, 255, 255, 0.5);
}

wa-carousel::part(pagination-item--active) {
  background-color: white;
}
```

## Customization

### Custom Navigation Styling

```css
/* Custom arrow buttons */
wa-carousel::part(navigation-button) {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: 2px solid white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

/* Custom pagination */
wa-carousel::part(pagination-item) {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background-color: #ccc;
  transition: all 0.3s;
}

wa-carousel::part(pagination-item--active) {
  width: 30px;
  border-radius: 6px;
  background-color: #3498db;
}
```

### Custom Slide Transitions

```css
/* Fade transition effect */
wa-carousel {
  --transition-duration: 500ms;
  --transition-timing-function: ease-in-out;
}

/* Custom aspect ratio */
wa-carousel {
  --aspect-ratio: 16/9;
}
```

## Best Practices

- ✅ Use `alt` attributes on images for accessibility
- ✅ Provide pause/play controls for autoplay carousels
- ✅ Keep slide count reasonable (5-10 slides maximum)
- ✅ Optimize images for web to ensure fast loading
- ✅ Use consistent aspect ratios across slides
- ✅ Test touch/swipe gestures on mobile devices
- ❌ Don't autoplay too quickly (minimum 3-5 seconds per slide)
- ❌ Avoid putting critical content only in carousels
- ❌ Don't use too many slides per page on mobile
- ❌ Avoid animating carousels on page load without user intent

## Accessibility

- Carousel automatically includes appropriate ARIA roles and labels
- Navigation buttons have proper ARIA labels
- Keyboard navigation supported (arrow keys, tab)
- Respects `prefers-reduced-motion` for users who prefer less motion
- Autoplay pauses on hover and focus

```html
<!-- Accessible carousel with labels -->
<wa-carousel
  navigation
  pagination
  aria-label="Product showcase carousel"
  aria-roledescription="carousel">
  <wa-carousel-item>
    <img src="product1.jpg" alt="Wireless headphones in black">
  </wa-carousel-item>
  <wa-carousel-item>
    <img src="product2.jpg" alt="Smart watch with silver band">
  </wa-carousel-item>
</wa-carousel>
```

## Troubleshooting

### Slides Not Visible

**Problem:** Carousel items don't display or have no height

**Solution:** Ensure carousel items have content with defined dimensions

```css
/* Give slides minimum height */
wa-carousel-item {
  min-height: 300px;
}

/* Or ensure images have dimensions */
wa-carousel-item img {
  width: 100%;
  height: auto;
}
```

### Autoplay Not Working

**Problem:** Carousel doesn't auto-advance

**Solution:** Ensure `autoplay` attribute is set and check interval

```html
<!-- ✅ Correct -->
<wa-carousel autoplay autoplay-interval="3000">
  <!-- slides -->
</wa-carousel>
```

### Navigation Not Appearing

**Problem:** Navigation buttons don't show

**Solution:** Verify `navigation` attribute is set

```javascript
// Enable navigation programmatically
carousel.navigation = true;
```

## Related

- [Carousel Item](./carousel-item.md)
- [Image](./image.md)
- [Card](./card.md)
- [Animation](./animation.md)
