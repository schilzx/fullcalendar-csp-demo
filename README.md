# fullcalendar-csp-demo

https://fullcalendar-csp-demo.pages.dev/

We’ve created a minimal demo page that uses FullCalendar and can be easily hosted on Cloudflare Pages to illustrate the
issue.

The purpose of this demo is to add a Content Security Policy (CSP) header with

```
require-trusted-types-for 'script'
```

and have the page work correctly.

At the moment, when we enable this CSP directive, the calendar does not load properly — it seems that the library (or
the way it’s initialized) may not be fully compatible with Trusted Types by default.

The demo itself is intentionally very simple:

A single index.html file with no extra frameworks.

It initializes FullCalendar with some static events.

The goal is to isolate the problem and make it easy to reproduce.

We would like to know what changes (if any) are required to make FullCalendar work when require-trusted-types-for '
script' is enforced, or if this is currently unsupported.

❌ Error Description

When enabling the following CSP directive:

```
Content-Security-Policy: require-trusted-types-for 'script'
```

the browser throws this error during page load:

```
index.global.min.js:6 This document requires 'TrustedHTML' assignment.
index.global.min.js:6 Uncaught TypeError: Failed to set the 'innerHTML' property on 'Element': This document requires 'TrustedHTML' assignment.
```

This happens because the FullCalendar library uses innerHTML internally to render UI components.
With require-trusted-types-for 'script' enabled, the browser blocks all assignments to innerHTML unless the value is a
TrustedHTML object created through a Trusted Types policy.

As a result, FullCalendar fails to render, and the page crashes before the calendar is displayed.
