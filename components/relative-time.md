# Relative Time

Display dates and times in a relative, human-readable format.

## Overview

The `<wa-relative-time>` component converts dates and timestamps into relative time expressions like "2 hours ago", "in 3 days", or "just now". It automatically updates the display over time and supports multiple languages and formatting styles, making it perfect for social media feeds, activity logs, and dynamic timestamps.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/relative-time/relative-time.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Show time relative to now -->
<wa-relative-time date="2025-03-15T10:30:00"></wa-relative-time>
<!-- Output: 2 hours ago (if current time is 12:30) -->

<!-- Future date -->
<wa-relative-time date="2025-03-17T14:00:00"></wa-relative-time>
<!-- Output: in 2 days -->

<!-- Recent time -->
<wa-relative-time date="2025-03-15T12:25:00"></wa-relative-time>
<!-- Output: 5 minutes ago (if current time is 12:30) -->

<!-- Very recent -->
<wa-relative-time date="2025-03-15T12:29:50"></wa-relative-time>
<!-- Output: just now -->
```

## Format Styles

Control the verbosity of the relative time output:

```html
<!-- Long format (default) -->
<wa-relative-time date="2025-03-15T10:30:00" format="long"></wa-relative-time>
<!-- Output: 2 hours ago -->

<!-- Short format -->
<wa-relative-time date="2025-03-15T10:30:00" format="short"></wa-relative-time>
<!-- Output: 2 hr. ago -->

<!-- Narrow format -->
<wa-relative-time date="2025-03-15T10:30:00" format="narrow"></wa-relative-time>
<!-- Output: 2h ago -->
```

## Numeric Display

Control whether to always use numeric values:

```html
<!-- Auto (uses "yesterday", "tomorrow", etc. when appropriate) -->
<wa-relative-time date="2025-03-14T12:00:00" numeric="auto"></wa-relative-time>
<!-- Output: yesterday -->

<!-- Always numeric -->
<wa-relative-time date="2025-03-14T12:00:00" numeric="always"></wa-relative-time>
<!-- Output: 1 day ago -->

<!-- Future dates -->
<wa-relative-time date="2025-03-16T12:00:00" numeric="auto"></wa-relative-time>
<!-- Output: tomorrow -->

<wa-relative-time date="2025-03-16T12:00:00" numeric="always"></wa-relative-time>
<!-- Output: in 1 day -->
```

## Auto-Sync

Enable automatic updates to keep the relative time current:

```html
<!-- Static (doesn't update) -->
<wa-relative-time date="2025-03-15T12:25:00"></wa-relative-time>

<!-- Auto-sync (updates automatically) -->
<wa-relative-time date="2025-03-15T12:25:00" sync></wa-relative-time>
```

The component intelligently adjusts the update frequency:
- Seconds: Updates every second
- Minutes: Updates every minute
- Hours: Updates every hour
- Days and beyond: Updates every hour

## Locale Support

Format relative times in different languages:

```html
<!-- English (default) -->
<wa-relative-time
  date="2025-03-15T10:30:00"
  locale="en-US">
</wa-relative-time>
<!-- Output: 2 hours ago -->

<!-- Spanish -->
<wa-relative-time
  date="2025-03-15T10:30:00"
  locale="es-ES">
</wa-relative-time>
<!-- Output: hace 2 horas -->

<!-- French -->
<wa-relative-time
  date="2025-03-15T10:30:00"
  locale="fr-FR">
</wa-relative-time>
<!-- Output: il y a 2 heures -->

<!-- German -->
<wa-relative-time
  date="2025-03-15T10:30:00"
  locale="de-DE">
</wa-relative-time>
<!-- Output: vor 2 Stunden -->

<!-- Japanese -->
<wa-relative-time
  date="2025-03-15T10:30:00"
  locale="ja-JP">
</wa-relative-time>
<!-- Output: 2 時間前 -->
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `date` | string \| Date | current date | No | The date to format (ISO string, timestamp, or Date object) |
| `locale` | string | - | No | Locale code for formatting (e.g., `en-US`, `es-ES`) |
| `format` | string | `'long'` | No | Display format: `long`, `short`, `narrow` |
| `numeric` | string | `'auto'` | No | Numeric display: `auto` (uses "yesterday"), `always` (uses "1 day ago") |
| `sync` | boolean | `false` | No | Automatically update the display over time |

## Examples

### Social Media Feed

```html
<style>
  .feed {
    max-width: 600px;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .post {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1rem;
  }
  .post-header {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 0.75rem;
  }
  .post-avatar {
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 50%;
    background-color: #3b82f6;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: 600;
  }
  .post-meta {
    flex: 1;
  }
  .post-author {
    font-weight: 600;
    margin-bottom: 0.125rem;
  }
  .post-time {
    font-size: 0.875rem;
    color: #6b7280;
  }
  .post-content {
    color: #1f2937;
    line-height: 1.5;
  }
</style>

<div class="feed">
  <div class="post">
    <div class="post-header">
      <div class="post-avatar">JD</div>
      <div class="post-meta">
        <div class="post-author">Jane Doe</div>
        <div class="post-time">
          <wa-relative-time date="2025-03-15T11:45:00" sync></wa-relative-time>
        </div>
      </div>
    </div>
    <div class="post-content">
      Just deployed the new feature to production! Check it out and let me know what you think.
    </div>
  </div>

  <div class="post">
    <div class="post-header">
      <div class="post-avatar">BS</div>
      <div class="post-meta">
        <div class="post-author">Bob Smith</div>
        <div class="post-time">
          <wa-relative-time date="2025-03-15T09:20:00" sync></wa-relative-time>
        </div>
      </div>
    </div>
    <div class="post-content">
      Great team meeting this morning! Excited about the roadmap for Q2.
    </div>
  </div>

  <div class="post">
    <div class="post-header">
      <div class="post-avatar">AJ</div>
      <div class="post-meta">
        <div class="post-author">Alice Johnson</div>
        <div class="post-time">
          <wa-relative-time date="2025-03-14T16:30:00" sync></wa-relative-time>
        </div>
      </div>
    </div>
    <div class="post-content">
      Finished the design review. Thanks everyone for the valuable feedback!
    </div>
  </div>
</div>
```

### Activity Log

```html
<style>
  .activity-log {
    max-width: 500px;
    display: flex;
    flex-direction: column;
  }
  .activity-item {
    display: flex;
    gap: 1rem;
    padding: 1rem 0;
    border-bottom: 1px solid #e5e7eb;
  }
  .activity-item:last-child {
    border-bottom: none;
  }
  .activity-icon {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }
  .activity-icon.success {
    background-color: #d1fae5;
    color: #10b981;
  }
  .activity-icon.warning {
    background-color: #fef3c7;
    color: #f59e0b;
  }
  .activity-icon.info {
    background-color: #dbeafe;
    color: #3b82f6;
  }
  .activity-details {
    flex: 1;
  }
  .activity-message {
    margin-bottom: 0.25rem;
    color: #1f2937;
  }
  .activity-time {
    font-size: 0.875rem;
    color: #6b7280;
  }
</style>

<div class="activity-log">
  <div class="activity-item">
    <div class="activity-icon success">
      <wa-icon name="check-circle-fill"></wa-icon>
    </div>
    <div class="activity-details">
      <div class="activity-message">Deployment completed successfully</div>
      <div class="activity-time">
        <wa-relative-time date="2025-03-15T12:15:00" sync></wa-relative-time>
      </div>
    </div>
  </div>

  <div class="activity-item">
    <div class="activity-icon info">
      <wa-icon name="upload"></wa-icon>
    </div>
    <div class="activity-details">
      <div class="activity-message">Sarah uploaded 3 new files</div>
      <div class="activity-time">
        <wa-relative-time date="2025-03-15T11:30:00" sync></wa-relative-time>
      </div>
    </div>
  </div>

  <div class="activity-item">
    <div class="activity-icon warning">
      <wa-icon name="exclamation-triangle-fill"></wa-icon>
    </div>
    <div class="activity-details">
      <div class="activity-message">High memory usage detected</div>
      <div class="activity-time">
        <wa-relative-time date="2025-03-15T10:45:00" sync></wa-relative-time>
      </div>
    </div>
  </div>

  <div class="activity-item">
    <div class="activity-icon success">
      <wa-icon name="check-circle-fill"></wa-icon>
    </div>
    <div class="activity-details">
      <div class="activity-message">Database backup completed</div>
      <div class="activity-time">
        <wa-relative-time date="2025-03-15T08:00:00" sync></wa-relative-time>
      </div>
    </div>
  </div>

  <div class="activity-item">
    <div class="activity-icon info">
      <wa-icon name="person-plus-fill"></wa-icon>
    </div>
    <div class="activity-details">
      <div class="activity-message">John joined the team</div>
      <div class="activity-time">
        <wa-relative-time date="2025-03-14T16:20:00" sync></wa-relative-time>
      </div>
    </div>
  </div>
</div>
```

### Comment System

```html
<style>
  .comments {
    max-width: 700px;
  }
  .comment {
    display: flex;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }
  .comment-avatar {
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 50%;
    background-color: #6b7280;
    flex-shrink: 0;
  }
  .comment-content {
    flex: 1;
    background-color: #f3f4f6;
    border-radius: 0.5rem;
    padding: 0.75rem;
  }
  .comment-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.5rem;
  }
  .comment-author {
    font-weight: 600;
    color: #1f2937;
  }
  .comment-time {
    font-size: 0.75rem;
    color: #6b7280;
  }
  .comment-text {
    color: #374151;
    line-height: 1.5;
  }
  .comment-actions {
    margin-top: 0.5rem;
    display: flex;
    gap: 1rem;
  }
  .comment-action {
    font-size: 0.875rem;
    color: #6b7280;
    cursor: pointer;
  }
  .comment-action:hover {
    color: #3b82f6;
  }
</style>

<div class="comments">
  <div class="comment">
    <div class="comment-avatar"></div>
    <div class="comment-content">
      <div class="comment-header">
        <span class="comment-author">Emily Chen</span>
        <span class="comment-time">
          <wa-relative-time date="2025-03-15T12:20:00" format="narrow" sync>
          </wa-relative-time>
        </span>
      </div>
      <div class="comment-text">
        This is a great article! I especially appreciated the section on performance optimization. Would love to see a follow-up on accessibility best practices.
      </div>
      <div class="comment-actions">
        <span class="comment-action">Reply</span>
        <span class="comment-action">Like</span>
      </div>
    </div>
  </div>

  <div class="comment">
    <div class="comment-avatar"></div>
    <div class="comment-content">
      <div class="comment-header">
        <span class="comment-author">Michael Rodriguez</span>
        <span class="comment-time">
          <wa-relative-time date="2025-03-15T11:45:00" format="narrow" sync>
          </wa-relative-time>
        </span>
      </div>
      <div class="comment-text">
        Thanks for sharing! Quick question: does this approach work with server-side rendering?
      </div>
      <div class="comment-actions">
        <span class="comment-action">Reply</span>
        <span class="comment-action">Like</span>
      </div>
    </div>
  </div>

  <div class="comment">
    <div class="comment-avatar"></div>
    <div class="comment-content">
      <div class="comment-header">
        <span class="comment-author">Sarah Wilson</span>
        <span class="comment-time">
          <wa-relative-time date="2025-03-15T09:30:00" format="narrow" sync>
          </wa-relative-time>
        </span>
      </div>
      <div class="comment-text">
        Excellent write-up! I've been looking for something like this. Bookmarked for future reference.
      </div>
      <div class="comment-actions">
        <span class="comment-action">Reply</span>
        <span class="comment-action">Like</span>
      </div>
    </div>
  </div>
</div>
```

### File Version History

```html
<style>
  .version-history {
    max-width: 600px;
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
  }
  .version-header {
    padding: 1rem;
    background-color: #f9fafb;
    border-bottom: 1px solid #e5e7eb;
    font-weight: 600;
  }
  .version-list {
    display: flex;
    flex-direction: column;
  }
  .version-item {
    padding: 1rem;
    border-bottom: 1px solid #e5e7eb;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .version-item:last-child {
    border-bottom: none;
  }
  .version-item:hover {
    background-color: #f9fafb;
  }
  .version-info {
    flex: 1;
  }
  .version-name {
    font-weight: 500;
    margin-bottom: 0.25rem;
  }
  .version-meta {
    font-size: 0.875rem;
    color: #6b7280;
  }
  .version-badge {
    padding: 0.25rem 0.5rem;
    background-color: #3b82f6;
    color: white;
    border-radius: 0.25rem;
    font-size: 0.75rem;
    font-weight: 600;
  }
</style>

<div class="version-history">
  <div class="version-header">Version History</div>
  <div class="version-list">
    <div class="version-item">
      <div class="version-info">
        <div class="version-name">v3.2.1 - Current Version</div>
        <div class="version-meta">
          Updated by Sarah •
          <wa-relative-time date="2025-03-15T12:00:00" sync></wa-relative-time>
        </div>
      </div>
      <div class="version-badge">CURRENT</div>
    </div>

    <div class="version-item">
      <div class="version-info">
        <div class="version-name">v3.2.0</div>
        <div class="version-meta">
          Updated by Michael •
          <wa-relative-time date="2025-03-14T15:30:00" sync></wa-relative-time>
        </div>
      </div>
    </div>

    <div class="version-item">
      <div class="version-info">
        <div class="version-name">v3.1.5</div>
        <div class="version-meta">
          Updated by Emily •
          <wa-relative-time date="2025-03-13T10:15:00" sync></wa-relative-time>
        </div>
      </div>
    </div>

    <div class="version-item">
      <div class="version-info">
        <div class="version-name">v3.1.4</div>
        <div class="version-meta">
          Updated by Sarah •
          <wa-relative-time date="2025-03-10T14:20:00" sync></wa-relative-time>
        </div>
      </div>
    </div>

    <div class="version-item">
      <div class="version-info">
        <div class="version-name">v3.1.3</div>
        <div class="version-meta">
          Updated by David •
          <wa-relative-time date="2025-03-08T09:00:00" sync></wa-relative-time>
        </div>
      </div>
    </div>
  </div>
</div>
```

### Notification Panel

```html
<style>
  .notification-panel {
    max-width: 400px;
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    background-color: white;
  }
  .notification-header {
    padding: 1rem;
    border-bottom: 1px solid #e5e7eb;
    font-weight: 600;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .notification-list {
    max-height: 400px;
    overflow-y: auto;
  }
  .notification {
    padding: 1rem;
    border-bottom: 1px solid #e5e7eb;
    cursor: pointer;
  }
  .notification:hover {
    background-color: #f9fafb;
  }
  .notification.unread {
    background-color: #eff6ff;
  }
  .notification.unread:hover {
    background-color: #dbeafe;
  }
  .notification-title {
    font-weight: 500;
    margin-bottom: 0.25rem;
    color: #1f2937;
  }
  .notification-message {
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 0.25rem;
  }
  .notification-time {
    font-size: 0.75rem;
    color: #9ca3af;
  }
  .unread-badge {
    background-color: #3b82f6;
    color: white;
    padding: 0.125rem 0.5rem;
    border-radius: 1rem;
    font-size: 0.75rem;
    font-weight: 600;
  }
</style>

<div class="notification-panel">
  <div class="notification-header">
    <span>Notifications</span>
    <span class="unread-badge">3</span>
  </div>
  <div class="notification-list">
    <div class="notification unread">
      <div class="notification-title">New comment on your post</div>
      <div class="notification-message">
        Alice commented: "Great work on this feature!"
      </div>
      <div class="notification-time">
        <wa-relative-time date="2025-03-15T12:25:00" sync></wa-relative-time>
      </div>
    </div>

    <div class="notification unread">
      <div class="notification-title">Deployment completed</div>
      <div class="notification-message">
        Your changes have been deployed to production
      </div>
      <div class="notification-time">
        <wa-relative-time date="2025-03-15T11:50:00" sync></wa-relative-time>
      </div>
    </div>

    <div class="notification unread">
      <div class="notification-title">Meeting reminder</div>
      <div class="notification-message">
        Team standup starts in 15 minutes
      </div>
      <div class="notification-time">
        <wa-relative-time date="2025-03-15T11:15:00" sync></wa-relative-time>
      </div>
    </div>

    <div class="notification">
      <div class="notification-title">Sarah mentioned you</div>
      <div class="notification-message">
        Sarah mentioned you in a comment
      </div>
      <div class="notification-time">
        <wa-relative-time date="2025-03-15T09:45:00" sync></wa-relative-time>
      </div>
    </div>

    <div class="notification">
      <div class="notification-title">Build failed</div>
      <div class="notification-message">
        CI pipeline failed on branch feature/new-ui
      </div>
      <div class="notification-time">
        <wa-relative-time date="2025-03-14T17:30:00" sync></wa-relative-time>
      </div>
    </div>
  </div>
</div>
```

## Methods

The component updates automatically when properties change:

```javascript
const relativeTime = document.querySelector('wa-relative-time');

// Update date
relativeTime.date = new Date();
relativeTime.date = '2025-03-15T10:30:00';
relativeTime.date = Date.now();

// Change format
relativeTime.format = 'short';

// Change numeric display
relativeTime.numeric = 'always';

// Enable/disable sync
relativeTime.sync = true;

// Change locale
relativeTime.locale = 'es-ES';
```

## Best Practices

- ✅ Use `sync` attribute for timestamps that need to stay current
- ✅ Choose appropriate format for your context (narrow for compact UIs, long for clarity)
- ✅ Use `numeric="auto"` for more natural language ("yesterday" vs "1 day ago")
- ✅ Combine with absolute timestamps on hover for precision
- ✅ Consider using short/narrow formats in mobile views to save space
- ❌ Don't use sync for historical dates that won't change relative position
- ❌ Avoid mixing different format styles in the same view
- ❌ Don't forget to handle future dates appropriately

## Accessibility

- The component outputs plain text that is naturally accessible to screen readers
- Consider providing absolute time as a fallback:

```html
<time datetime="2025-03-15T10:30:00">
  <wa-relative-time date="2025-03-15T10:30:00" sync></wa-relative-time>
</time>
```

- Add tooltips with absolute timestamps for additional context:

```html
<wa-tooltip>
  <wa-relative-time date="2025-03-15T10:30:00" sync></wa-relative-time>
  <div slot="content">
    March 15, 2025 at 10:30 AM
  </div>
</wa-tooltip>
```

## Troubleshooting

### Time Not Updating

**Problem:** Time displays but doesn't update automatically

**Solution:** Ensure you've added the `sync` attribute

```html
<!-- ❌ Won't update -->
<wa-relative-time date="2025-03-15T10:30:00"></wa-relative-time>

<!-- ✅ Updates automatically -->
<wa-relative-time date="2025-03-15T10:30:00" sync></wa-relative-time>
```

### Shows "Invalid Date"

**Problem:** Component displays "Invalid Date" or blank output

**Solution:** Ensure the date is in a valid format

```html
<!-- ✅ Correct: ISO string -->
<wa-relative-time date="2025-03-15T10:30:00"></wa-relative-time>

<!-- ✅ Correct: timestamp -->
<wa-relative-time date="1710497400000"></wa-relative-time>

<!-- ❌ Wrong: invalid format -->
<wa-relative-time date="15/03/2025"></wa-relative-time>
```

```javascript
// When setting dynamically
relativeTime.date = new Date().toISOString(); // Convert to ISO string
```

### Wrong Language Display

**Problem:** Relative time doesn't display in expected language

**Solution:** Set the locale attribute explicitly

```html
<!-- ✅ Correct: explicit locale -->
<wa-relative-time date="2025-03-15T10:30:00" locale="es-ES"></wa-relative-time>

<!-- May use browser default locale -->
<wa-relative-time date="2025-03-15T10:30:00"></wa-relative-time>
```

## Related

- [Format Date](./format-date.md)
- [Format Number](./format-number.md)
- [Badge](./badge.md)
- [Card](./card.md)
