# Format Date

Format dates and times with locale support and flexible display options.

## Overview

The `<wa-format-date>` component formats JavaScript Date objects and date strings into human-readable formats with full internationalization support. It provides granular control over date and time components and automatically updates to reflect locale preferences.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/format-date/format-date.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Format current date -->
<wa-format-date></wa-format-date>

<!-- Format specific date (ISO string) -->
<wa-format-date date="2025-03-15T14:30:00"></wa-format-date>

<!-- Format specific date (timestamp) -->
<wa-format-date date="1710513000000"></wa-format-date>

<!-- Format with custom options -->
<wa-format-date
  date="2025-03-15"
  weekday="long"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: Saturday, March 15, 2025 -->
```

## Date Components

Control which date components to display:

```html
<!-- Full date -->
<wa-format-date
  date="2025-03-15"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: March 15, 2025 -->

<!-- Month and year only -->
<wa-format-date
  date="2025-03-15"
  year="numeric"
  month="long">
</wa-format-date>
<!-- Output: March 2025 -->

<!-- Day of week -->
<wa-format-date
  date="2025-03-15"
  weekday="long">
</wa-format-date>
<!-- Output: Saturday -->

<!-- With era -->
<wa-format-date
  date="2025-03-15"
  era="long"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: March 15, 2025 Anno Domini -->
```

## Time Components

Display time information:

```html
<!-- Hours and minutes -->
<wa-format-date
  date="2025-03-15T14:30:00"
  hour="numeric"
  minute="numeric">
</wa-format-date>
<!-- Output: 2:30 PM -->

<!-- With seconds -->
<wa-format-date
  date="2025-03-15T14:30:45"
  hour="numeric"
  minute="numeric"
  second="numeric">
</wa-format-date>
<!-- Output: 2:30:45 PM -->

<!-- 24-hour format -->
<wa-format-date
  date="2025-03-15T14:30:00"
  hour="2-digit"
  minute="2-digit"
  hour-12="false">
</wa-format-date>
<!-- Output: 14:30 -->

<!-- With timezone -->
<wa-format-date
  date="2025-03-15T14:30:00"
  hour="numeric"
  minute="numeric"
  time-zone-name="short">
</wa-format-date>
<!-- Output: 2:30 PM PST -->

<!-- Long timezone name -->
<wa-format-date
  date="2025-03-15T14:30:00"
  hour="numeric"
  minute="numeric"
  time-zone-name="long">
</wa-format-date>
<!-- Output: 2:30 PM Pacific Standard Time -->
```

## Component Styles

Customize the formatting style of each component:

### Weekday Styles

```html
<!-- Short (Mon) -->
<wa-format-date date="2025-03-15" weekday="short"></wa-format-date>

<!-- Long (Monday) -->
<wa-format-date date="2025-03-15" weekday="long"></wa-format-date>

<!-- Narrow (M) -->
<wa-format-date date="2025-03-15" weekday="narrow"></wa-format-date>
```

### Month Styles

```html
<!-- Numeric (3) -->
<wa-format-date date="2025-03-15" month="numeric"></wa-format-date>

<!-- 2-digit (03) -->
<wa-format-date date="2025-03-15" month="2-digit"></wa-format-date>

<!-- Short (Mar) -->
<wa-format-date date="2025-03-15" month="short"></wa-format-date>

<!-- Long (March) -->
<wa-format-date date="2025-03-15" month="long"></wa-format-date>

<!-- Narrow (M) -->
<wa-format-date date="2025-03-15" month="narrow"></wa-format-date>
```

### Year Styles

```html
<!-- Numeric (2025) -->
<wa-format-date date="2025-03-15" year="numeric"></wa-format-date>

<!-- 2-digit (25) -->
<wa-format-date date="2025-03-15" year="2-digit"></wa-format-date>
```

### Day Styles

```html
<!-- Numeric (15) -->
<wa-format-date date="2025-03-15" day="numeric"></wa-format-date>

<!-- 2-digit (15) -->
<wa-format-date date="2025-03-15" day="2-digit"></wa-format-date>
```

## Locale Support

Format dates according to different locales:

```html
<!-- US English (default) -->
<wa-format-date
  date="2025-03-15"
  locale="en-US"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: March 15, 2025 -->

<!-- British English -->
<wa-format-date
  date="2025-03-15"
  locale="en-GB"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: 15 March 2025 -->

<!-- German -->
<wa-format-date
  date="2025-03-15"
  locale="de-DE"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: 15. März 2025 -->

<!-- Japanese -->
<wa-format-date
  date="2025-03-15"
  locale="ja-JP"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: 2025年3月15日 -->

<!-- French -->
<wa-format-date
  date="2025-03-15"
  locale="fr-FR"
  year="numeric"
  month="long"
  day="numeric">
</wa-format-date>
<!-- Output: 15 mars 2025 -->
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `date` | string \| Date | current date | No | The date to format (ISO string, timestamp, or Date object) |
| `locale` | string | - | No | Locale code for formatting (e.g., `en-US`, `de-DE`) |
| `weekday` | string | - | No | Weekday format: `narrow`, `short`, `long` |
| `era` | string | - | No | Era format: `narrow`, `short`, `long` |
| `year` | string | - | No | Year format: `numeric`, `2-digit` |
| `month` | string | - | No | Month format: `numeric`, `2-digit`, `narrow`, `short`, `long` |
| `day` | string | - | No | Day format: `numeric`, `2-digit` |
| `hour` | string | - | No | Hour format: `numeric`, `2-digit` |
| `minute` | string | - | No | Minute format: `numeric`, `2-digit` |
| `second` | string | - | No | Second format: `numeric`, `2-digit` |
| `time-zone-name` | string | - | No | Timezone name format: `short`, `long` |
| `hour-12` | boolean | - | No | Use 12-hour format (true) or 24-hour format (false) |

## Examples

### Event Schedule

```html
<style>
  .event-card {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1.5rem;
    margin-bottom: 1rem;
    max-width: 500px;
  }
  .event-date {
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 0.5rem;
  }
  .event-title {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }
  .event-time {
    font-size: 0.875rem;
    color: #3b82f6;
  }
</style>

<div class="event-card">
  <div class="event-date">
    <wa-format-date
      date="2025-03-20"
      weekday="long"
      month="long"
      day="numeric">
    </wa-format-date>
  </div>
  <div class="event-title">Product Launch Webinar</div>
  <div class="event-time">
    <wa-icon name="clock"></wa-icon>
    <wa-format-date
      date="2025-03-20T14:00:00"
      hour="numeric"
      minute="numeric"
      time-zone-name="short">
    </wa-format-date>
  </div>
</div>

<div class="event-card">
  <div class="event-date">
    <wa-format-date
      date="2025-03-25"
      weekday="long"
      month="long"
      day="numeric">
    </wa-format-date>
  </div>
  <div class="event-title">Team All-Hands Meeting</div>
  <div class="event-time">
    <wa-icon name="clock"></wa-icon>
    <wa-format-date
      date="2025-03-25T10:00:00"
      hour="numeric"
      minute="numeric"
      time-zone-name="short">
    </wa-format-date>
  </div>
</div>
```

### Article Metadata

```html
<style>
  .article-meta {
    display: flex;
    gap: 1rem;
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 1rem;
  }
  .meta-item {
    display: flex;
    align-items: center;
    gap: 0.25rem;
  }
</style>

<article>
  <h1>Understanding Web Components</h1>
  <div class="article-meta">
    <div class="meta-item">
      <wa-icon name="calendar"></wa-icon>
      Published:
      <wa-format-date
        date="2025-02-15"
        month="short"
        day="numeric"
        year="numeric">
      </wa-format-date>
    </div>
    <div class="meta-item">
      <wa-icon name="clock"></wa-icon>
      Last updated:
      <wa-format-date
        date="2025-03-10T09:30:00"
        month="short"
        day="numeric"
        year="numeric">
      </wa-format-date>
    </div>
  </div>
  <p>Web components are a set of web platform APIs...</p>
</article>
```

### Dynamic Date Display

```html
<div style="display: flex; flex-direction: column; gap: 1rem; max-width: 400px;">
  <wa-input
    type="date"
    id="dateInput"
    label="Select a date"
    value="2025-03-15">
  </wa-input>

  <wa-card>
    <div slot="header">Formatted Dates</div>

    <div style="display: flex; flex-direction: column; gap: 0.5rem;">
      <div>
        <strong>Full:</strong>
        <wa-format-date
          id="fullDate"
          date="2025-03-15"
          weekday="long"
          year="numeric"
          month="long"
          day="numeric">
        </wa-format-date>
      </div>

      <div>
        <strong>Short:</strong>
        <wa-format-date
          id="shortDate"
          date="2025-03-15"
          year="numeric"
          month="2-digit"
          day="2-digit">
        </wa-format-date>
      </div>

      <div>
        <strong>Month/Year:</strong>
        <wa-format-date
          id="monthYear"
          date="2025-03-15"
          year="numeric"
          month="long">
        </wa-format-date>
      </div>
    </div>
  </wa-card>
</div>

<script>
  const dateInput = document.getElementById('dateInput');
  const fullDate = document.getElementById('fullDate');
  const shortDate = document.getElementById('shortDate');
  const monthYear = document.getElementById('monthYear');

  dateInput.addEventListener('wa-change', (event) => {
    const selectedDate = event.target.value;
    fullDate.date = selectedDate;
    shortDate.date = selectedDate;
    monthYear.date = selectedDate;
  });
</script>
```

### Timestamp List

```html
<style>
  .timestamp-list {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .timestamp-item {
    display: flex;
    justify-content: space-between;
    padding: 0.75rem;
    border: 1px solid #e5e7eb;
    border-radius: 0.25rem;
  }
  .timestamp-label {
    font-weight: 500;
  }
  .timestamp-value {
    color: #6b7280;
    font-size: 0.875rem;
  }
</style>

<div class="timestamp-list">
  <div class="timestamp-item">
    <span class="timestamp-label">Created</span>
    <span class="timestamp-value">
      <wa-format-date
        date="2025-03-01T08:00:00"
        month="short"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </span>
  </div>

  <div class="timestamp-item">
    <span class="timestamp-label">Modified</span>
    <span class="timestamp-value">
      <wa-format-date
        date="2025-03-10T14:30:00"
        month="short"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </span>
  </div>

  <div class="timestamp-item">
    <span class="timestamp-label">Last Accessed</span>
    <span class="timestamp-value">
      <wa-format-date
        date="2025-03-15T16:45:00"
        month="short"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </span>
  </div>
</div>
```

### International Date Display

```html
<style>
  .locale-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
  }
  .locale-card {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1rem;
  }
  .locale-name {
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: #1f2937;
  }
  .locale-date {
    color: #6b7280;
  }
</style>

<div class="locale-grid">
  <div class="locale-card">
    <div class="locale-name">United States</div>
    <div class="locale-date">
      <wa-format-date
        date="2025-03-15T14:30:00"
        locale="en-US"
        weekday="long"
        year="numeric"
        month="long"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </div>
  </div>

  <div class="locale-card">
    <div class="locale-name">United Kingdom</div>
    <div class="locale-date">
      <wa-format-date
        date="2025-03-15T14:30:00"
        locale="en-GB"
        weekday="long"
        year="numeric"
        month="long"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </div>
  </div>

  <div class="locale-card">
    <div class="locale-name">Germany</div>
    <div class="locale-date">
      <wa-format-date
        date="2025-03-15T14:30:00"
        locale="de-DE"
        weekday="long"
        year="numeric"
        month="long"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </div>
  </div>

  <div class="locale-card">
    <div class="locale-name">Japan</div>
    <div class="locale-date">
      <wa-format-date
        date="2025-03-15T14:30:00"
        locale="ja-JP"
        weekday="long"
        year="numeric"
        month="long"
        day="numeric"
        hour="numeric"
        minute="numeric">
      </wa-format-date>
    </div>
  </div>
</div>
```

## Methods

The component updates automatically when properties change:

```javascript
const formatter = document.querySelector('wa-format-date');

// Update date
formatter.date = new Date('2025-03-15');
formatter.date = '2025-03-15T14:30:00';
formatter.date = '1710513000000';

// Change locale
formatter.locale = 'de-DE';

// Update formatting options
formatter.weekday = 'long';
formatter.month = 'long';
formatter.year = 'numeric';
formatter.day = 'numeric';
```

## Best Practices

- ✅ Use consistent date formats throughout your application
- ✅ Respect user locale preferences when available
- ✅ Include timezone information for time-sensitive data
- ✅ Use appropriate detail level (full date for important events, short for lists)
- ✅ Combine with `wa-relative-time` for recent timestamps
- ❌ Don't mix different date formats in the same context
- ❌ Avoid ambiguous formats like MM/DD/YYYY without locale context
- ❌ Don't forget to handle invalid date values

## Accessibility

- The component outputs plain text that is naturally accessible to screen readers
- Consider adding semantic HTML context:

```html
<time datetime="2025-03-15T14:30:00">
  <wa-format-date
    date="2025-03-15T14:30:00"
    month="long"
    day="numeric"
    year="numeric">
  </wa-format-date>
</time>
```

- For important dates, provide additional context:

```html
<span aria-label="Event start time: March 15, 2025 at 2:30 PM">
  <wa-format-date
    date="2025-03-15T14:30:00"
    month="short"
    day="numeric"
    hour="numeric"
    minute="numeric">
  </wa-format-date>
</span>
```

## Troubleshooting

### Invalid Date Display

**Problem:** Component shows "Invalid Date" or blank output

**Solution:** Ensure the date value is in a valid format

```html
<!-- ✅ Correct: ISO string -->
<wa-format-date date="2025-03-15"></wa-format-date>

<!-- ✅ Correct: ISO with time -->
<wa-format-date date="2025-03-15T14:30:00"></wa-format-date>

<!-- ✅ Correct: timestamp -->
<wa-format-date date="1710513000000"></wa-format-date>

<!-- ❌ Wrong: invalid format -->
<wa-format-date date="15/03/2025"></wa-format-date>
```

```javascript
// When setting dynamically
formatter.date = new Date('2025-03-15').toISOString(); // Convert to ISO string
```

### Time Not Showing

**Problem:** Time components don't appear in output

**Solution:** Ensure you've set the hour, minute, and/or second attributes

```html
<!-- ✅ Correct: includes time attributes -->
<wa-format-date
  date="2025-03-15T14:30:00"
  hour="numeric"
  minute="numeric">
</wa-format-date>

<!-- ❌ Wrong: no time attributes -->
<wa-format-date date="2025-03-15T14:30:00"></wa-format-date>
```

### Locale Not Applied

**Problem:** Date doesn't format according to specified locale

**Solution:** Verify the locale code is valid

```html
<!-- ✅ Correct -->
<wa-format-date date="2025-03-15" locale="de-DE"></wa-format-date>

<!-- ❌ Wrong: invalid locale -->
<wa-format-date date="2025-03-15" locale="german"></wa-format-date>
```

## Related

- [Relative Time](./relative-time.md)
- [Format Number](./format-number.md)
- [Format Bytes](./format-bytes.md)
- [Input](./input.md)
