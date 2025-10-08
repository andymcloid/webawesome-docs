# Progress Bar

A progress bar component to visually indicate the completion status of a task or operation.

## Overview

The `<wa-progress-bar>` component provides a visual indicator of progress for tasks such as file uploads, form completion, or multi-step processes. It supports both determinate (with a specific value) and indeterminate (unknown duration) states, and can display optional labels.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/progress-bar/progress-bar.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Determinate progress bar at 50% -->
<wa-progress-bar value="50"></wa-progress-bar>

<!-- Indeterminate progress bar (loading) -->
<wa-progress-bar indeterminate></wa-progress-bar>

<!-- Progress bar with label -->
<wa-progress-bar value="75" label="75% Complete"></wa-progress-bar>
```

## Determinate Progress

Use the `value` attribute to show specific progress (0-100):

```html
<!-- 0% progress -->
<wa-progress-bar value="0"></wa-progress-bar>

<!-- 25% progress -->
<wa-progress-bar value="25"></wa-progress-bar>

<!-- 50% progress -->
<wa-progress-bar value="50"></wa-progress-bar>

<!-- 75% progress -->
<wa-progress-bar value="75"></wa-progress-bar>

<!-- 100% progress (complete) -->
<wa-progress-bar value="100"></wa-progress-bar>
```

### Dynamic Progress

```html
<wa-progress-bar id="uploadProgress" value="0"></wa-progress-bar>
<p>Upload progress: <span id="progressText">0%</span></p>

<script>
  const progressBar = document.getElementById('uploadProgress');
  const progressText = document.getElementById('progressText');

  // Simulate upload progress
  let progress = 0;
  const interval = setInterval(() => {
    progress += 10;
    progressBar.value = progress;
    progressText.textContent = `${progress}%`;

    if (progress >= 100) {
      clearInterval(interval);
    }
  }, 500);
</script>
```

## Indeterminate Progress

Use the `indeterminate` attribute when the duration is unknown:

```html
<wa-progress-bar indeterminate></wa-progress-bar>

<!-- With label -->
<wa-progress-bar indeterminate label="Loading..."></wa-progress-bar>
```

### Toggle Between States

```html
<wa-progress-bar id="dynamicProgress"></wa-progress-bar>
<wa-button id="toggleBtn">Start Loading</wa-button>

<script>
  const progressBar = document.getElementById('dynamicProgress');
  const toggleBtn = document.getElementById('toggleBtn');
  let isLoading = false;

  toggleBtn.addEventListener('click', () => {
    isLoading = !isLoading;
    progressBar.indeterminate = isLoading;
    toggleBtn.textContent = isLoading ? 'Stop Loading' : 'Start Loading';
  });
</script>
```

## Labels

Add descriptive text with the `label` attribute:

```html
<!-- Simple percentage label -->
<wa-progress-bar value="60" label="60%"></wa-progress-bar>

<!-- Descriptive label -->
<wa-progress-bar value="80" label="Processing your request..."></wa-progress-bar>

<!-- Step indicator -->
<wa-progress-bar value="33" label="Step 1 of 3"></wa-progress-bar>
```

### Dynamic Label

```html
<wa-progress-bar id="downloadProgress" value="0"></wa-progress-bar>

<script>
  const progressBar = document.getElementById('downloadProgress');
  let downloaded = 0;
  const total = 100;

  const interval = setInterval(() => {
    downloaded += 5;
    const percentage = (downloaded / total) * 100;
    progressBar.value = percentage;
    progressBar.label = `${downloaded} MB / ${total} MB`;

    if (downloaded >= total) {
      clearInterval(interval);
      progressBar.label = 'Download complete!';
    }
  }, 200);
</script>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | number | `0` | No | Progress value (0-100) |
| `indeterminate` | boolean | `false` | No | Show indeterminate loading state |
| `label` | string | - | No | Descriptive label for the progress bar |

## Examples

### File Upload Progress

```html
<div style="max-width: 500px;">
  <h3>Upload File</h3>
  <input type="file" id="fileInput" />
  <wa-progress-bar id="fileProgress" value="0" style="margin-top: 1rem;"></wa-progress-bar>
  <p id="statusText">Select a file to upload</p>
</div>

<script>
  const fileInput = document.getElementById('fileInput');
  const progressBar = document.getElementById('fileProgress');
  const statusText = document.getElementById('statusText');

  fileInput.addEventListener('change', async (e) => {
    const file = e.target.files[0];
    if (!file) return;

    statusText.textContent = `Uploading ${file.name}...`;

    // Simulate upload with progress
    for (let i = 0; i <= 100; i += 10) {
      await new Promise(resolve => setTimeout(resolve, 200));
      progressBar.value = i;
      progressBar.label = `${i}%`;
    }

    statusText.textContent = 'Upload complete!';
    progressBar.label = 'Complete';
  });
</script>
```

### Multi-Step Form

```html
<div style="max-width: 600px;">
  <wa-progress-bar id="formProgress" value="33"></wa-progress-bar>
  <p style="margin-top: 0.5rem; color: #666;">Step 1 of 3: Personal Information</p>

  <form id="multiStepForm">
    <div id="step1">
      <wa-input label="Name" required></wa-input>
      <wa-input label="Email" type="email" required></wa-input>
      <wa-button type="button" id="nextBtn1">Next</wa-button>
    </div>
  </form>
</div>

<script>
  const progressBar = document.getElementById('formProgress');
  const nextBtn1 = document.getElementById('nextBtn1');

  nextBtn1.addEventListener('click', () => {
    // Move to step 2
    progressBar.value = 66;
    // Update form content and continue...
  });
</script>
```

### Page Loading Indicator

```html
<div style="position: fixed; top: 0; left: 0; right: 0; z-index: 9999;">
  <wa-progress-bar id="pageProgress" indeterminate style="height: 3px;"></wa-progress-bar>
</div>

<script>
  const pageProgress = document.getElementById('pageProgress');

  // Show on page navigation
  window.addEventListener('beforeunload', () => {
    pageProgress.style.display = 'block';
  });

  // Hide on page load
  window.addEventListener('load', () => {
    pageProgress.style.display = 'none';
  });
</script>
```

### Task Completion Tracker

```html
<div style="max-width: 500px;">
  <h3>Daily Tasks</h3>
  <wa-progress-bar id="taskProgress" value="0"></wa-progress-bar>
  <p id="taskLabel">0 of 5 tasks complete</p>

  <ul style="list-style: none; padding: 0;">
    <li>
      <wa-checkbox class="task-checkbox">Morning exercise</wa-checkbox>
    </li>
    <li>
      <wa-checkbox class="task-checkbox">Read for 30 minutes</wa-checkbox>
    </li>
    <li>
      <wa-checkbox class="task-checkbox">Meditation</wa-checkbox>
    </li>
    <li>
      <wa-checkbox class="task-checkbox">Work on project</wa-checkbox>
    </li>
    <li>
      <wa-checkbox class="task-checkbox">Evening walk</wa-checkbox>
    </li>
  </ul>
</div>

<script>
  const taskProgress = document.getElementById('taskProgress');
  const taskLabel = document.getElementById('taskLabel');
  const checkboxes = document.querySelectorAll('.task-checkbox');
  const totalTasks = checkboxes.length;

  function updateProgress() {
    const completedTasks = Array.from(checkboxes).filter(cb => cb.checked).length;
    const percentage = (completedTasks / totalTasks) * 100;

    taskProgress.value = percentage;
    taskLabel.textContent = `${completedTasks} of ${totalTasks} tasks complete`;
  }

  checkboxes.forEach(checkbox => {
    checkbox.addEventListener('wa-change', updateProgress);
  });
</script>
```

## CSS Parts

Use CSS parts to style internal progress bar elements:

```css
/* Style the progress bar base container */
wa-progress-bar::part(base) {
  height: 8px;
  border-radius: 4px;
}

/* Style the progress indicator */
wa-progress-bar::part(indicator) {
  background: linear-gradient(90deg, #3b82f6, #8b5cf6);
}

/* Style the label */
wa-progress-bar::part(label) {
  font-weight: bold;
  color: #374151;
}
```

## Customization

### Custom Colors

```css
/* Success progress (green) */
wa-progress-bar.success::part(indicator) {
  background-color: #10b981;
}

/* Warning progress (yellow) */
wa-progress-bar.warning::part(indicator) {
  background-color: #f59e0b;
}

/* Danger progress (red) */
wa-progress-bar.danger::part(indicator) {
  background-color: #ef4444;
}
```

### Custom Height

```css
/* Thin progress bar */
wa-progress-bar.thin::part(base) {
  height: 2px;
}

/* Thick progress bar */
wa-progress-bar.thick::part(base) {
  height: 16px;
}
```

### Gradient Progress

```css
wa-progress-bar.gradient::part(indicator) {
  background: linear-gradient(90deg, #3b82f6, #8b5cf6, #ec4899);
}
```

## Best Practices

- Use determinate progress bars when you know the completion percentage
- Use indeterminate progress bars for operations with unknown duration
- Provide meaningful labels to give context to users
- Keep progress bars visible during operations
- Update progress smoothly, not in large jumps
- Show completion state before removing the progress bar
- Use appropriate colors to indicate status (success, warning, error)
- Place progress bars near the content being loaded when possible

## Accessibility

- Progress bars automatically include `role="progressbar"` and appropriate ARIA attributes
- The `value` is automatically announced to screen readers
- Use the `label` attribute to provide context:

```html
<wa-progress-bar value="60" label="Uploading file: 60% complete"></wa-progress-bar>
```

- For critical operations, combine with `aria-live` announcements:

```html
<div aria-live="polite" aria-atomic="true">
  <wa-progress-bar value="100" label="Upload complete"></wa-progress-bar>
</div>
```

## Troubleshooting

### Progress Not Updating

**Problem:** Progress bar value doesn't change

**Solution:** Ensure you're setting the `value` property correctly

```javascript
// Correct
progressBar.value = 50;

// Also works
progressBar.setAttribute('value', '50');
```

### Value Out of Range

**Problem:** Progress bar displays incorrectly

**Solution:** Ensure value is between 0 and 100

```javascript
// Clamp value to valid range
function setProgress(value) {
  progressBar.value = Math.max(0, Math.min(100, value));
}
```

### Indeterminate Not Showing

**Problem:** Indeterminate state doesn't animate

**Solution:** Remove the `value` attribute when setting indeterminate

```javascript
progressBar.removeAttribute('value');
progressBar.indeterminate = true;
```

## Related

- [Spinner](./spinner.md)
- [Loading States Guide](../guides/loading-states.md)
- [Form Controls Guide](../guides/form-controls.md)
