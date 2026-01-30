---
layout: page
title: UI Testing
permalink: /tutorials/week5-uitesting
parent: Tutorials
nav_order: 9
---

# Testing User Interfaces on the Web

Testing web applications has always been tricky: web applications run inside of the browser, and browsers are complicated pieces of software. Many pieces of software have been created to provide a test double for the browser and the browser's DOM (Document Object Model). However, the current trend in the mid-2020s is to directly run tests in the browser, and [Playwright](https://playwright.dev/docs/intro) is a popular tool that facilitates running these tests.

This guide isn't intended to replace the [Playwright docs](https://playwright.dev/docs/intro), it's just intended to give an extremely brief introduction to how Playwright can be used in this course. 

## Running Playwright tests

In our course projects, Playwright tests can be run in two ways:

 - `npm run test` runs the tests automatically (this is called "headless mode" for obscure reasons). When tests finish, Playwright generates an HTML report in a `playwright-report` directory.
 - `npm run playwright` runs the tests in an interactive UI mode.

Playwright's UI is extremely useful. You can use it to help you:
- **Write new tests:** Watch mode re-runs tests as you edit
- **Debugging failures:** Step through each action, see the page state at every moment
- **Discovering selectors:** Use the "Pick locator" tool to find the right selector for any element

UI mode is your best friend when a test fails and you don't know why. You can see exactly what the page looked like when an assertion failed.

See [Playwright UI Mode docs](https://playwright.dev/docs/test-ui-mode) for a full walkthrough.

## Example

Here's an example of using Playwright to log in to the home page. 

```ts
// From login.e2e.spec.ts - testing successful login
test('should allow an existing user to log in', async ({ page }) => {
  // Assemble
  await page.goto('/login');
  await page.getByLabel('Username').fill("user3");
  await page.getByLabel('Password', { exact: true }).fill("pwd3333");

  // Act
  await page.getByRole('button', { name: 'Log In' }).click();

  // Assess
  await page.waitForURL('/');
  await expect(page.getByText('signed in as Frau Drei')).toBeVisible();
});
```

This short code demonstrates several types of Playwright actions: 

 - Navigating to different pages and waiting for URLs to change
 - Locating elements on a page (like the field for entering username, or the button for logging in)
 - Interacting with elements on a page
 - Testing assertions about an element on a page

## Locating Elements on a Page

A lot of the challenge of browser UI testing in general is locating elements on a web page. Ideally, tests should interact with web pages the way a human user does. ***XXX TODO: Say something about ARIA roles, accessibility, and how relying on ARIA roles actually makes this easier. "The UI is intentionally accessible so tests can be robust" doesn't communicate anything helpful. Playwright seems like it's based on a philosophy that writing good tests should push you towards making websites that are more accessible e.g. to people using screen readers or interacting with webpages without a mouse.***

- Inputs use labels, so tests use `getByLabel`.
- Buttons are targeted by role and name, so tests use `getByRole("button", { name: "..." })`.
- Lists use ARIA roles like `role="listitem"` so tests can filter and click reliably.

If a test is hard to write, prefer adding or improving ARIA labels/roles in the component instead of using fragile selectors. XXX TODO: fragile selectors is probably new jargon for students

### Discovering Selectors

**Option 1: Playwright UI mode (recommended)**

Run `npm run playwright`, then use the "Pick locator" tool (target icon) to click on any element. Playwright suggests the best selector automatically.

**Option 2: Browser DevTools**

1. Right-click an element → Inspect
2. Look for `aria-label`, `role`, `placeholder`, or visible text
3. Map what you find to the appropriate `getBy*` method:

| What you see in HTML | Playwright method |
|---------------------|-------------------|
| `aria-label="Username"` | `getByLabel('Username')` |
| `placeholder="Send a message to chat"` | `getByPlaceholder('Send a message to chat')` |
| `role="button"` with text "Log In" | `getByRole('button', { name: 'Log In' })` |
| `role="listitem"` | `getByRole('listitem')` |
| Visible text "signed in as..." | `getByText('signed in as...')` |

XXX TODO: one of the reasons we need an introduction to ARIA with links to more information is to get across the idea that things like `<button>` inherently have the aria role button even if that's not explicitly assigned.

### Filtering and Chaining

When multiple elements match, narrow down with `.filter()`:

```ts
// From testutils.ts - find the specific list item containing a username, then click its link
await page2.getByRole('listitem').filter({ hasText: username1 }).getByRole('link').click();
```

See [Playwright Locators docs](https://playwright.dev/docs/locators) for more filtering options.

## Interacting With Elements on a Page

***XXX TODO: put the thing about `{ exact: true }` in here somewhere. I removed the "**Use `{ exact: true }` for Password field.** Otherwise it matches "Show Password" checkbox. " advice from the gamenite-specific advice because we're going for something more general: lots of interactions only work when .***

One of the things that Playwright does quite well is handle interactions with page elements. If an action can't be taken right away, Playwright will generally wait until the action becomes available. A few cases need explicit waits, and this is one of the trickier parts of Playwright—it works so well most of the time that the exceptions can be surprising.

Clicking and filling elements will automatically wait for the element to be visible and actionable:

```ts
await page.getByLabel('Username').fill('user3');
await page.getByRole('button', { name: 'Log In' }).click();
```

Sometimes, you need explicit waits.

**After navigation or redirects:** Actions like clicking a login button trigger a redirect, but the action itself completes immediately. Use `waitForURL` to explicitly wait for the navigation to finish before continuing.

```ts
// From login.e2e.spec.ts
await page.getByRole('button', { name: 'Log In' }).click();  // Click completes, redirect starts
await page.waitForURL('/');  // Explicitly wait for redirect to complete
await expect(page.getByText('signed in as Frau Drei')).toBeVisible();
```

**After WebSocket updates:** When another user's action updates your UI (common in multiplayer games), wait on the resulting UI change:

```ts
// Pattern for multiplayer games - after player 1 acts, verify player 2's UI updates
await page1.getByRole('button', { name: 'Take three' }).click();
await expect(page2.getByRole('button', { name: 'Take one' })).toBeEnabled();  // Wait for WebSocket update
```

**When data loads asynchronously:** If a component renders after fetching data, wait on the element you need:

```ts
// From testutils.ts - wait for the chat input to confirm game page loaded
await page1.getByPlaceholder('Send a message to chat').click();
```

The rule of tumb is: when auto-wait isn't enough, use `await expect(...)` assertions, because these consistently retry until the condition is met or timeout. 

## Assertions

XXX TODO some kind of introduction

Here are some useful assertions. XXX TODO link to more

```ts
await expect(element).toBeVisible();
await expect(element).toBeEnabled();
await expect(element).toHaveText('expected');
await expect(element).toBeDisabled();
await expect(element).not.toBeVisible();
```

## Debugging Failed Tests

Test failures happen. Here's how to diagnose them efficiently.

### 1. Read the Error Message

Playwright's error messages are detailed. Look for:
- **Which assertion failed:** e.g., `expect(locator).toBeVisible()`
- **What it was waiting for:** e.g., `Locator: getByRole('button', { name: 'Start Game' })`
- **Timeout:** If it says "Timeout 30000ms exceeded," the element never appeared

```
Error: expect(locator).toBeVisible()

Locator: getByRole('button', { name: 'Start Game' })
Expected: visible
Received: <element not found>
Call log:
  - waiting for getByRole('button', { name: 'Start Game' })
```

### 2. Check the HTML Report

After `npm run test` fails, Playwright generates a report:

```
client/playwright-report/index.html
```

Open it in a browser. The report shows:
- ✅ / ❌ status for each test
- **Error details** with the full call log
- **Source location** of the failing line

> Note: Screenshots and traces are not captured by default. The current config only generates the basic HTML report. If you need these, you'd enable them in `playwright.config.mjs`.

### 3. Reproduce in UI Mode

Run the failing test in UI mode for interactive debugging:

```bash
npm run playwright
```

In UI mode you can:
- **Watch the test run** in a real browser
- **Pause on any step** and inspect the page
- **See the DOM state** at each action
- **Use "Pick locator"** to verify your selectors match what you expect

### 4. Common Failure Patterns

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| "Element not found" | Selector doesn't match | Use UI mode's "Pick locator" to find the right selector |
| "Element not visible" | Element exists but hidden/covered | Check if something is overlaying it, or wait for animation |
| Timeout after navigation | Missing `waitForURL` | Add `await page.waitForURL('/expected-path')` |
| Flaky (passes sometimes) | Race condition with async data | Add `await expect(...)` on the element before interacting |
| Works locally, fails in CI | Server not ready | Check `webServer` config in `playwright.config.mjs` |

### 5. Isolate the Problem

Run just the failing test:

```bash
# In UI mode - click on the specific test
npm run playwright

# Or from command line
npx playwright test -g "test name here"
```

UI mode is the best debugging tool—you can pause on any step, inspect the page, and see exactly what Playwright sees. Prefer this over adding debug code to your tests.

### 6. Check if It's a UI Bug

Sometimes the test is correct but the UI has a bug. Before spending hours on the test:
1. Run the app manually (`npm run dev` in both `client/` and `server/`)
2. Try the exact flow your test is doing
3. If the UI doesn't work manually, fix the UI first

## References

| Documentation | What It Covers |
|------|----------------|
| [Test intro](https://playwright.dev/docs/test-intro) | Basic test structure, running tests |
| [UI Mode](https://playwright.dev/docs/test-ui-mode) | Interactive debugging, watch mode |
| [Locators](https://playwright.dev/docs/locators) | All `getBy*` methods, filtering, chaining |
| [getByRole reference](https://playwright.dev/docs/api/class-page#page-get-by-role) | Role names, options like `{ name, exact }` |
| [Actionability](https://playwright.dev/docs/actionability) | How auto-wait works, what Playwright checks |
| [Assertions](https://playwright.dev/docs/test-assertions) | All `expect()` matchers: `toBeVisible`, `toHaveText`, etc. |

## GameNite-Specific Tips

XXX TODO: maybe transfer something about `createAndLoadGame` and other `testutils.ts` helper functions here. 

- **Always `waitForURL` after login/navigation.** The redirect happens async.
- **Create random usernames in tests.** Avoids collisions: `'user' + Math.floor(Math.random() * 1_000_000)` helps avoid “User already exists” when the test creates accounts.
- **Test display names, not usernames.** The UI shows "Frau Drei", not "user3".
- **WebSocket updates need explicit waits.** After one player acts, wait for the other player's UI to update.
- **The server resets on restart (in dev mode).** If your test data seems stale, restart the dev server. (Note: This only applies to the default in-memory setup. With MongoDB configured, data persists across restarts.)
