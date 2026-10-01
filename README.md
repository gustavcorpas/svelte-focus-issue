# SvelteKit iframe focus reproduction

Minimal reproduction of a focus issue when a SvelteKit application is embedded in an `<iframe>`.

## Reproduction

1. Start the SvelteKit project.
2. Open the `/` route in the browser.
3. Click **Load iframe**.
4. Press <kbd>Tab</kbd> to move focus to the next focusable element.

### Expected

The **Focusable** button on the host page receives focus.

### Actual

When server-side rendering is disabled (`ssr = false`), focus moves into the iframe and the focusable button inside the iframe receives focus instead.

The issue does not reproduce with server-side rendering enabled.

## Relevant configuration

The iframe page uses:

```js
// +page.js
export const ssr = false;
```

This is required to reproduce the issue in the minimal example.

## Project structure

```text
.
├── src/
│   └── routes/
│       ├── +page.svelte        # Host page
│       └── iframe/
│           └── +page.svelte    # Embedded page
└── ...
```

The host page dynamically creates and removes the iframe:

```js
function loadIframe() {
	const iframe = document.createElement('iframe');
	iframe.id = 'iframe';
	iframe.title = 'Embedded page';
	iframe.src = './iframe';

	frameContainer.appendChild(iframe);
}
```

## Purpose

This repository is intended as a minimal reproduction for investigating SvelteKit's focus management during client-side navigation and its interaction with embedded browsing contexts.
