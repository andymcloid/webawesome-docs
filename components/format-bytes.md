# Format Bytes

Format byte values into human-readable file sizes.

## Overview

The `<wa-format-bytes>` component formats numeric byte values into human-readable units (KB, MB, GB, etc.) with automatic unit selection and locale-aware formatting. Perfect for displaying file sizes, storage capacity, and data usage.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/format-bytes/format-bytes.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Format bytes (auto-selects unit) -->
<wa-format-bytes value="1024"></wa-format-bytes>
<!-- Output: 1 KB -->

<!-- Format larger values -->
<wa-format-bytes value="1048576"></wa-format-bytes>
<!-- Output: 1 MB -->

<!-- Format with specific unit -->
<wa-format-bytes value="1500000" unit="kilobyte"></wa-format-bytes>
<!-- Output: 1,465 KB -->
```

## Units

The component automatically selects the appropriate unit, or you can specify one explicitly:

```html
<!-- Auto-select unit (default) -->
<wa-format-bytes value="2048000"></wa-format-bytes>
<!-- Output: 2 MB -->

<!-- Force byte display -->
<wa-format-bytes value="1024" unit="byte"></wa-format-bytes>
<!-- Output: 1,024 bytes -->

<!-- Force kilobyte display -->
<wa-format-bytes value="1048576" unit="kilobyte"></wa-format-bytes>
<!-- Output: 1,024 KB -->

<!-- Force megabyte display -->
<wa-format-bytes value="1048576" unit="megabyte"></wa-format-bytes>
<!-- Output: 1 MB -->

<!-- Force gigabyte display -->
<wa-format-bytes value="1073741824" unit="gigabyte"></wa-format-bytes>
<!-- Output: 1 GB -->

<!-- Force terabyte display -->
<wa-format-bytes value="1099511627776" unit="terabyte"></wa-format-bytes>
<!-- Output: 1 TB -->

<!-- Force petabyte display -->
<wa-format-bytes value="1125899906842624" unit="petabyte"></wa-format-bytes>
<!-- Output: 1 PB -->
```

## Display Options

Control the format of the output:

```html
<!-- Default: narrow (1 MB) -->
<wa-format-bytes value="1048576"></wa-format-bytes>

<!-- Short format (1 MB) -->
<wa-format-bytes value="1048576" display="short"></wa-format-bytes>

<!-- Long format (1 megabyte) -->
<wa-format-bytes value="1048576" display="long"></wa-format-bytes>

<!-- Narrow format (1MB - no space) -->
<wa-format-bytes value="1048576" display="narrow"></wa-format-bytes>
```

## Locale Support

Format values according to different locales:

```html
<!-- US English (default) -->
<wa-format-bytes value="1234567" locale="en-US"></wa-format-bytes>
<!-- Output: 1.18 MB -->

<!-- German -->
<wa-format-bytes value="1234567" locale="de-DE"></wa-format-bytes>
<!-- Output: 1,18 MB -->

<!-- French -->
<wa-format-bytes value="1234567" locale="fr-FR"></wa-format-bytes>
<!-- Output: 1,18 Mo -->

<!-- Japanese -->
<wa-format-bytes value="1234567" locale="ja-JP"></wa-format-bytes>
<!-- Output: 1.18 MB -->
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | number | `0` | No | The byte value to format |
| `unit` | string | - | No | Force a specific unit: `byte`, `kilobyte`, `megabyte`, `gigabyte`, `terabyte`, `petabyte` |
| `display` | string | `'narrow'` | No | Display format: `narrow`, `short`, `long` |
| `locale` | string | - | No | Locale code for formatting (e.g., `en-US`, `de-DE`) |

## Examples

### File Upload List

```html
<style>
  .file-list {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  .file-item {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem;
    border: 1px solid #e5e7eb;
    border-radius: 0.25rem;
  }
  .file-name {
    font-weight: 500;
  }
  .file-size {
    color: #6b7280;
  }
</style>

<div class="file-list">
  <div class="file-item">
    <span class="file-name">document.pdf</span>
    <span class="file-size">
      <wa-format-bytes value="2458624"></wa-format-bytes>
    </span>
  </div>
  <div class="file-item">
    <span class="file-name">presentation.pptx</span>
    <span class="file-size">
      <wa-format-bytes value="8945632"></wa-format-bytes>
    </span>
  </div>
  <div class="file-item">
    <span class="file-name">image.jpg</span>
    <span class="file-size">
      <wa-format-bytes value="524288"></wa-format-bytes>
    </span>
  </div>
</div>
```

### Storage Usage Dashboard

```html
<style>
  .storage-card {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1.5rem;
    max-width: 400px;
  }
  .storage-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
  }
  .storage-title {
    font-size: 1.125rem;
    font-weight: 600;
  }
  .storage-used {
    font-size: 0.875rem;
    color: #6b7280;
  }
  .storage-bar {
    width: 100%;
    height: 1rem;
    background-color: #e5e7eb;
    border-radius: 0.5rem;
    overflow: hidden;
    margin-bottom: 0.5rem;
  }
  .storage-fill {
    height: 100%;
    background-color: #3b82f6;
    transition: width 0.3s ease;
  }
  .storage-total {
    font-size: 0.875rem;
    color: #6b7280;
    text-align: right;
  }
</style>

<div class="storage-card">
  <div class="storage-header">
    <span class="storage-title">Cloud Storage</span>
    <span class="storage-used">
      <wa-format-bytes value="32212254720"></wa-format-bytes> used
    </span>
  </div>
  <div class="storage-bar">
    <div class="storage-fill" style="width: 64.4%"></div>
  </div>
  <div class="storage-total">
    <wa-format-bytes value="50000000000"></wa-format-bytes> total
  </div>
</div>
```

### Dynamic File Size Display

```html
<wa-input type="file" id="fileInput" label="Choose a file"></wa-input>
<div id="fileInfo" style="margin-top: 1rem; display: none;">
  <p>
    File size: <wa-format-bytes id="fileSize"></wa-format-bytes>
  </p>
</div>

<script>
  const fileInput = document.getElementById('fileInput');
  const fileInfo = document.getElementById('fileInfo');
  const fileSize = document.getElementById('fileSize');

  fileInput.addEventListener('wa-change', (event) => {
    const file = event.target.files[0];

    if (file) {
      fileSize.value = file.size;
      fileInfo.style.display = 'block';
    } else {
      fileInfo.style.display = 'none';
    }
  });
</script>
```

### Data Usage Breakdown

```html
<style>
  .usage-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 500px;
  }
  .usage-item {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  .usage-icon {
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #f3f4f6;
  }
  .usage-details {
    flex: 1;
  }
  .usage-label {
    font-weight: 500;
    margin-bottom: 0.25rem;
  }
  .usage-count {
    font-size: 0.875rem;
    color: #6b7280;
  }
  .usage-size {
    font-weight: 600;
    color: #1f2937;
  }
</style>

<div class="usage-list">
  <div class="usage-item">
    <div class="usage-icon">
      <wa-icon name="file-earmark-text"></wa-icon>
    </div>
    <div class="usage-details">
      <div class="usage-label">Documents</div>
      <div class="usage-count">24 files</div>
    </div>
    <div class="usage-size">
      <wa-format-bytes value="12582912"></wa-format-bytes>
    </div>
  </div>

  <div class="usage-item">
    <div class="usage-icon">
      <wa-icon name="image"></wa-icon>
    </div>
    <div class="usage-details">
      <div class="usage-label">Images</div>
      <div class="usage-count">156 files</div>
    </div>
    <div class="usage-size">
      <wa-format-bytes value="268435456"></wa-format-bytes>
    </div>
  </div>

  <div class="usage-item">
    <div class="usage-icon">
      <wa-icon name="camera-video"></wa-icon>
    </div>
    <div class="usage-details">
      <div class="usage-label">Videos</div>
      <div class="usage-count">8 files</div>
    </div>
    <div class="usage-size">
      <wa-format-bytes value="1073741824"></wa-format-bytes>
    </div>
  </div>

  <div class="usage-item">
    <div class="usage-icon">
      <wa-icon name="folder"></wa-icon>
    </div>
    <div class="usage-details">
      <div class="usage-label">Other</div>
      <div class="usage-count">42 files</div>
    </div>
    <div class="usage-size">
      <wa-format-bytes value="52428800"></wa-format-bytes>
    </div>
  </div>
</div>
```

## Methods

The component updates automatically when properties change:

```javascript
const formatter = document.querySelector('wa-format-bytes');

// Update value
formatter.value = 1048576;

// Change unit
formatter.unit = 'kilobyte';

// Change display format
formatter.display = 'long';

// Change locale
formatter.locale = 'de-DE';
```

## Best Practices

- ✅ Let the component auto-select units for varying file sizes
- ✅ Use consistent display format within the same UI section
- ✅ Consider using `long` format for clarity in educational contexts
- ✅ Use locale-specific formatting for international audiences
- ✅ Show both used and total storage for capacity indicators
- ❌ Don't mix binary (1024) and decimal (1000) conventions in the same UI
- ❌ Avoid forcing inappropriate units (e.g., showing bytes as gigabytes)
- ❌ Don't forget to handle zero or negative values appropriately

## Accessibility

- The component outputs plain text that is naturally accessible to screen readers
- Consider adding context for screen reader users:

```html
<span aria-label="File size">
  <wa-format-bytes value="1048576"></wa-format-bytes>
</span>
```

- For storage indicators, provide text alternatives:

```html
<div role="status" aria-label="Storage usage: 32 gigabytes used of 50 gigabytes total">
  <wa-format-bytes value="32212254720"></wa-format-bytes> of
  <wa-format-bytes value="50000000000"></wa-format-bytes> used
</div>
```

## Troubleshooting

### Incorrect Unit Display

**Problem:** Component shows unexpected unit (e.g., bytes instead of KB)

**Solution:** Check that the value is a number, not a string

```html
<!-- ❌ Wrong: string value -->
<wa-format-bytes value="1024"></wa-format-bytes>

<!-- ✅ Correct: numeric value -->
<wa-format-bytes value="1024"></wa-format-bytes>
```

```javascript
// When setting dynamically
formatter.value = parseInt(fileSize); // Ensure numeric type
```

### Display Format Not Working

**Problem:** Display attribute doesn't change the output format

**Solution:** Verify the display value is one of: `narrow`, `short`, or `long`

```html
<!-- ✅ Correct -->
<wa-format-bytes value="1048576" display="long"></wa-format-bytes>

<!-- ❌ Wrong -->
<wa-format-bytes value="1048576" display="verbose"></wa-format-bytes>
```

### Locale Not Applied

**Problem:** Formatting doesn't respect the specified locale

**Solution:** Ensure the locale code is valid and supported

```html
<!-- ✅ Correct -->
<wa-format-bytes value="1234567" locale="de-DE"></wa-format-bytes>

<!-- ❌ Wrong: invalid locale -->
<wa-format-bytes value="1234567" locale="german"></wa-format-bytes>
```

## Related

- [Format Number](./format-number.md)
- [Format Date](./format-date.md)
- [Progress Bar](./progress-bar.md)
- [Card](./card.md)
