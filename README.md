# fullcalendar-csp-demo

We’ve created a minimal demo page that uses FullCalendar and can be easily hosted on Cloudflare Pages to illustrate the issue.

The purpose of this demo is to add a Content Security Policy (CSP) header with

```
require-trusted-types-for 'script'
```

and have the page work correctly.

At the moment, when we enable this CSP directive, the calendar does not load properly — it seems that the library (or the way it’s initialized) may not be fully compatible with Trusted Types by default.

The demo itself is intentionally very simple:

A single index.html file with no extra frameworks.

It initializes FullCalendar with some static events.

The goal is to isolate the problem and make it easy to reproduce.

We would like to know what changes (if any) are required to make FullCalendar work when require-trusted-types-for 'script' is enforced, or if this is currently unsupported.
