<!--
URL: https://playwright.dev/docs/emulation
Fetch date: 2026-08-18
Source type: official docs
Research cluster: visual-funnel-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Emulation | Playwright
URL: https://playwright.dev/docs/emulation

Emulation | Playwright

## Introduction

With Playwright you can test your app on any browser as well as emulate a real device such as a mobile phone or tablet. Simply configure the devices you would like to emulate and Playwright will simulate the browser behavior such as `"userAgent"`, `"screenSize"`, `"viewport"` and if it `"hasTouch"` enabled. You can also emulate the `"geolocation"`, `"locale"` and `"timezone"` for all tests or for a specific test as well as set the `"permissions"` to show notifications or change the `"colorScheme"`.

## Devices

Playwright comes with a registry of device parameters using playwright.devices for selected desktop, tablet and mobile devices. It can be used to simulate browser behavior for a specific device such as user agent, screen size, viewport and if it has touch enabled. All tests will run with the specified device parameters.

```js
import { defineConfig, devices } from '@playwright/test'; // import devices
export default defineConfig({
  projects: [
    {
      name: 'chromium',
      use: {
        ...devices['Desktop Chrome'],
      },
    },
    {
      name: 'Mobile Safari',
      use: {
        ...devices['iPhone 13'],
      },
    },
  ],
});
```

Note: Pre-configured devices assume a specific platform. For example, "Desktop Chrome" will provide a Windows-specific user agent string.

If you would like to use the user agent specific to the platform that is running the tests, we recommend unsetting the user agent property.

```js
const context = await browser.newContext({
  ...devices['Desktop Chrome'],
  userAgent: undefined,
});
```

## Viewport

The viewport is included in the device but you can override it for some tests with page.setViewportSize().

```js
import { defineConfig, devices } from '@playwright/test';
export default defineConfig({
  projects: [
    {
      name: 'chromium',
      use: {
        ...devices['Desktop Chrome'],
        // It is important to define the `viewport` property after destructuring `devices`,
        // since devices also define the `viewport` for that device.
        viewport: { width: 1280, height: 720 },
      },
    },
  ]
});
```

Test file:

```js
import { test, expect } from '@playwright/test';
test.use({
  viewport: { width: 1600, height: 1200 },
});
test('my test', async ({ page }) => {
  // ...
});
```

The same works inside a test file, including scoped to a `test.describe` block:

```js
import { test, expect } from '@playwright/test';
test.describe('specific viewport block', () => {
  test.use({ viewport: { width: 1600, height: 1200 } });
  test('my test', async ({ page }) => {
    // ...
  });
});
```

## isMobile

Whether the meta viewport tag is taken into account and touch events are enabled.

```js
import { defineConfig, devices } from '@playwright/test';
export default defineConfig({
  projects: [
    {
      name: 'chromium',
      use: {
        ...devices['Desktop Chrome'],
        // It is important to define the `isMobile` property after destructuring `devices`,
        // since devices also define the `isMobile` for that device.
        isMobile: false,
      },
    },
  ]
});
```

## Locale and Timezone

Emulate the browser Locale and Timezone which can be set globally for all tests in the config and then overridden for particular tests.

```js
import { defineConfig } from '@playwright/test';
export default defineConfig({
  use: {
    // Emulates the browser locale.
    locale: 'en-GB',
    // Emulates the browser timezone.
    timezoneId: 'Europe/Paris',
  },
});
```

Note that this only affects the browser timezone and locale, not the test runner timezone. To set the test runner timezone, you can use the TZ environment variable.

## Permissions

Allow app to show system notifications. Permissions can be granted for a specific domain and revoked with `browserContext.clearPermissions()`.

## Geolocation

Grant `"geolocation"` permissions and set geolocation to a specific area. The location can be changed later within a test, but note you can only change geolocation for all pages in the context (not per-page).

## Color Scheme and Media

Emulate the users `"colorScheme"`. Supported values are 'light' and 'dark'. You can also emulate the media type with page.emulateMedia().

## User Agent

The User Agent is included in the device and therefore you will rarely need to change it, however if you do need to test a different user agent you can override it with the `userAgent` property.

## Offline

Emulate the network being offline (content cut off in the archived fetch beyond this heading).
