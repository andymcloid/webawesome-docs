# QR Code

Generate QR codes for URLs, text, and other data.

## Overview

The `<wa-qr-code>` component generates QR (Quick Response) codes that can be scanned by smartphones and other devices. It's perfect for sharing URLs, contact information, Wi-Fi credentials, and any other data that needs to be easily transferred to mobile devices.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/qr-code/qr-code.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Simple URL QR code -->
<wa-qr-code value="https://example.com"></wa-qr-code>

<!-- Text QR code -->
<wa-qr-code value="Hello, World!"></wa-qr-code>

<!-- Email address -->
<wa-qr-code value="mailto:contact@example.com"></wa-qr-code>
```

## Size

Control the QR code size:

```html
<!-- Small QR code -->
<wa-qr-code value="https://example.com" size="128"></wa-qr-code>

<!-- Medium QR code (default) -->
<wa-qr-code value="https://example.com" size="256"></wa-qr-code>

<!-- Large QR code -->
<wa-qr-code value="https://example.com" size="512"></wa-qr-code>
```

## Colors

Customize the QR code colors:

```html
<!-- Custom fill color -->
<wa-qr-code
  value="https://example.com"
  fill="#6366f1">
</wa-qr-code>

<!-- Custom background color -->
<wa-qr-code
  value="https://example.com"
  background="#f3f4f6">
</wa-qr-code>

<!-- Both custom colors -->
<wa-qr-code
  value="https://example.com"
  fill="#1e293b"
  background="#f1f5f9">
</wa-qr-code>
```

## Border Radius

Add rounded corners to QR code modules:

```html
<!-- No radius (default) -->
<wa-qr-code value="https://example.com" radius="0"></wa-qr-code>

<!-- Small radius -->
<wa-qr-code value="https://example.com" radius="0.25"></wa-qr-code>

<!-- Medium radius -->
<wa-qr-code value="https://example.com" radius="0.5"></wa-qr-code>

<!-- Full radius (circular modules) -->
<wa-qr-code value="https://example.com" radius="1"></wa-qr-code>
```

## Error Correction

Set the error correction level:

```html
<!-- Low error correction (7%) -->
<wa-qr-code
  value="https://example.com"
  error-correction="L">
</wa-qr-code>

<!-- Medium error correction (15%) - default -->
<wa-qr-code
  value="https://example.com"
  error-correction="M">
</wa-qr-code>

<!-- Quartile error correction (25%) -->
<wa-qr-code
  value="https://example.com"
  error-correction="Q">
</wa-qr-code>

<!-- High error correction (30%) -->
<wa-qr-code
  value="https://example.com"
  error-correction="H">
</wa-qr-code>
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | string | - | Yes | The data to encode in the QR code |
| `size` | number | `256` | No | Size of the QR code in pixels |
| `fill` | string | `'#000000'` | No | Color of the QR code modules (foreground) |
| `background` | string | `'#ffffff'` | No | Background color of the QR code |
| `radius` | number | `0` | No | Border radius of modules (0-1) |
| `error-correction` | string | `'M'` | No | Error correction level: `L` (7%), `M` (15%), `Q` (25%), `H` (30%) |

## Examples

### Website URL

```html
<div class="qr-container">
  <h3>Visit Our Website</h3>
  <wa-qr-code
    value="https://www.example.com"
    size="200"
    radius="0.5">
  </wa-qr-code>
  <p>Scan to visit example.com</p>
</div>

<style>
  .qr-container {
    text-align: center;
    padding: 2rem;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
  }
</style>
```

### Contact Information (vCard)

```html
<wa-qr-code
  id="contactQR"
  size="256"
  fill="#1e293b"
  background="#f8fafc"
  error-correction="H">
</wa-qr-code>

<script>
  const vcard = `BEGIN:VCARD
VERSION:3.0
FN:John Doe
TEL:+1234567890
EMAIL:john@example.com
URL:https://johndoe.com
END:VCARD`;

  document.getElementById('contactQR').value = vcard;
</script>
```

### Wi-Fi Credentials

```html
<wa-card>
  <div slot="header">
    <h3>Guest Wi-Fi Access</h3>
  </div>

  <div style="text-align: center;">
    <wa-qr-code
      id="wifiQR"
      size="200"
      radius="0.5"
      error-correction="H">
    </wa-qr-code>

    <div style="margin-top: 1rem;">
      <strong>Network:</strong> GuestNetwork<br>
      <strong>Password:</strong> Welcome123
    </div>
  </div>
</wa-card>

<script>
  // Wi-Fi QR code format: WIFI:T:WPA;S:SSID;P:PASSWORD;;
  document.getElementById('wifiQR').value =
    'WIFI:T:WPA;S:GuestNetwork;P:Welcome123;;';
</script>
```

### Event Ticket

```html
<wa-card class="ticket">
  <div slot="header">
    <h3>Concert Ticket</h3>
  </div>

  <div class="ticket-content">
    <div class="ticket-info">
      <p><strong>Event:</strong> Summer Music Festival</p>
      <p><strong>Date:</strong> July 15, 2024</p>
      <p><strong>Seat:</strong> A-23</p>
      <p><strong>Ticket ID:</strong> #TKT-2024-001</p>
    </div>

    <wa-qr-code
      value="https://tickets.example.com/verify?id=TKT-2024-001"
      size="150"
      radius="0.25"
      error-correction="H">
    </wa-qr-code>
  </div>
</wa-card>

<style>
  .ticket {
    max-width: 400px;
  }

  .ticket-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
  }

  .ticket-info {
    flex: 1;
  }
</style>
```

### Branded QR Code

```html
<div class="branded-qr">
  <wa-qr-code
    value="https://www.example.com"
    size="300"
    fill="#6366f1"
    background="#f8fafc"
    radius="0.75"
    error-correction="H">
  </wa-qr-code>

  <div class="logo-overlay">
    <img src="/logo.png" alt="Company Logo">
  </div>
</div>

<style>
  .branded-qr {
    position: relative;
    display: inline-block;
  }

  .logo-overlay {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 8px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .logo-overlay img {
    width: 60px;
    height: 60px;
    display: block;
  }
</style>
```

### Download QR Code

```html
<div class="qr-download-container">
  <wa-qr-code
    id="downloadQR"
    value="https://example.com"
    size="256">
  </wa-qr-code>

  <wa-button id="downloadBtn" style="margin-top: 1rem;">
    <wa-icon slot="start" name="download"></wa-icon>
    Download QR Code
  </wa-button>
</div>

<script>
  const downloadBtn = document.getElementById('downloadBtn');
  const qrCode = document.getElementById('downloadQR');

  downloadBtn.addEventListener('click', async () => {
    // Get the QR code as a data URL
    const canvas = qrCode.shadowRoot.querySelector('canvas');
    const dataUrl = canvas.toDataURL('image/png');

    // Create download link
    const link = document.createElement('a');
    link.download = 'qr-code.png';
    link.href = dataUrl;
    link.click();
  });
</script>
```

### Dynamic QR Code

```html
<div class="dynamic-qr">
  <wa-input
    id="urlInput"
    label="Enter URL"
    placeholder="https://example.com"
    value="https://example.com">
  </wa-input>

  <wa-qr-code
    id="dynamicQR"
    value="https://example.com"
    size="256"
    radius="0.5"
    style="margin-top: 1rem;">
  </wa-qr-code>
</div>

<script>
  const urlInput = document.getElementById('urlInput');
  const dynamicQR = document.getElementById('dynamicQR');

  urlInput.addEventListener('wa-input', () => {
    dynamicQR.value = urlInput.value || 'https://example.com';
  });
</script>
```

### Color Picker QR Code

```html
<div class="color-qr">
  <div class="controls">
    <wa-color-picker
      id="fillPicker"
      label="QR Code Color"
      value="#000000">
    </wa-color-picker>

    <wa-color-picker
      id="bgPicker"
      label="Background Color"
      value="#ffffff">
    </wa-color-picker>
  </div>

  <wa-qr-code
    id="colorQR"
    value="https://example.com"
    size="256"
    fill="#000000"
    background="#ffffff">
  </wa-qr-code>
</div>

<script>
  const fillPicker = document.getElementById('fillPicker');
  const bgPicker = document.getElementById('bgPicker');
  const colorQR = document.getElementById('colorQR');

  fillPicker.addEventListener('wa-change', () => {
    colorQR.fill = fillPicker.value;
  });

  bgPicker.addEventListener('wa-change', () => {
    colorQR.background = bgPicker.value;
  });
</script>

<style>
  .color-qr {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  .controls {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>
```

## CSS Parts

Use CSS parts to style internal elements:

```css
/* Style the container */
wa-qr-code::part(container) {
  border: 4px solid #e5e7eb;
  border-radius: 12px;
  padding: 1rem;
}
```

## Customization

### With Border and Shadow

```css
wa-qr-code {
  border: 2px solid #e5e7eb;
  border-radius: 16px;
  padding: 1rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background: white;
}
```

### Responsive Sizing

```html
<wa-qr-code
  value="https://example.com"
  style="width: 100%; max-width: 300px; height: auto;">
</wa-qr-code>
```

## Best Practices

- ✅ Use high error correction for branded QR codes with logos
- ✅ Test QR codes with multiple devices before deploying
- ✅ Ensure sufficient contrast between fill and background colors
- ✅ Keep the data short for faster scanning
- ✅ Provide context about what the QR code links to
- ✅ Use appropriate size (minimum 2cm x 2cm for print)
- ❌ Don't use low contrast color combinations
- ❌ Avoid making QR codes too small to scan
- ❌ Don't encode sensitive information without encryption
- ❌ Avoid using very light fills on white backgrounds

## Accessibility

- Provide text alternatives for QR code content
- Include descriptive labels near QR codes:

```html
<div role="img" aria-label="QR code linking to example.com">
  <wa-qr-code value="https://example.com"></wa-qr-code>
  <p>Scan to visit example.com</p>
</div>
```

- Ensure sufficient color contrast (minimum 4.5:1 ratio)
- Provide alternative ways to access the information
- Don't rely solely on QR codes for critical information

## Troubleshooting

### QR Code Not Scanning

**Problem:** QR code doesn't scan reliably

**Solution:** Increase the error correction level and ensure sufficient size

```html
<!-- ✅ Better for scanning -->
<wa-qr-code
  value="https://example.com"
  size="300"
  error-correction="H">
</wa-qr-code>

<!-- ❌ Too small and low error correction -->
<wa-qr-code
  value="https://example.com"
  size="64"
  error-correction="L">
</wa-qr-code>
```

### Low Contrast Issues

**Problem:** QR code is hard to see or scan

**Solution:** Use colors with sufficient contrast

```html
<!-- ✅ Good contrast -->
<wa-qr-code
  value="https://example.com"
  fill="#000000"
  background="#ffffff">
</wa-qr-code>

<!-- ❌ Poor contrast -->
<wa-qr-code
  value="https://example.com"
  fill="#cccccc"
  background="#ffffff">
</wa-qr-code>
```

### Too Much Data

**Problem:** QR code becomes too dense with lots of data

**Solution:** Use a URL shortener or higher error correction

```javascript
// Use a URL shortener for long URLs
const longUrl = 'https://example.com/very/long/path/to/page?param=value';
const shortUrl = await shortenUrl(longUrl); // Use your URL shortening service

document.querySelector('wa-qr-code').value = shortUrl;
```

## Related

- [Barcode](./barcode.md)
- [Image](./image.md)
- [Icon](./icon.md)
- [Card](./card.md)
