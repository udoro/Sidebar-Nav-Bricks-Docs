---
icon: code
---

# JavaScript API & Page Transitions

You don't need this page to use the sidebar. It's for when your own JavaScript has to restart the sidebar or change its options while the page is open.

***

## What the template gives you

The template starts the sidebar on every page. Three names are ready for your code:

| Name | What it is |
| --- | --- |
| `sidebar` | The running sidebar. |
| `DWCSidebarConfig` | Your options from the **Sidebar Options CSS/JS** code block. |
| `urlConfigMap` | Your per-page options from the same code block. |

Write them as they are: `sidebar`, not `window.sidebar`. They don't exist on `window`, so `window.sidebar`, `window.DWCSidebarConfig` and `window.urlConfigMap` give you `undefined`.

### Where to put your code

Your code must run after the sidebar has started. Put it in one of these places:

* **A Code element placed below Sidebar CSS and JS** in the sidebar template, with **Execute code** on.
* **Bricks > Settings > Custom code > Body (footer) scripts.**

Don't put it in **Sidebar Options CSS/JS**. That code block runs before the sidebar starts.

***

## Restart the sidebar

```js
sidebar.reinitialize();
```

Use it after your code adds or replaces menu items, for example after loading content with AJAX. The sidebar finds its elements again and starts over.

It starts with `DWCSidebarConfig` only. On a page listed in `urlConfigMap`, use the last example under [Restart with other options](#restart-with-other-options), so the page keeps its own options.

### Restart with other options

```js
sidebar.reinitialize({ enableCollapsibleSidebar: 0, enableOffCanvas: 1 });
```

* The options you pass are added to `DWCSidebarConfig`. Every other option keeps its value from `DWCSidebarConfig`.
* Each call starts again from `DWCSidebarConfig`, so options from an earlier call are gone. Pass every change you want, every time.
* Per-page options from `urlConfigMap` are not added for you. To keep them, add them yourself:

```js
const path = window.location.pathname.replace(/\/$/, '');
sidebar.reinitialize({ ...DWCSidebarConfig, ...(urlConfigMap[path] || {}), enableOffCanvas: 1 });
```

## Stop the sidebar

```js
sidebar.cleanup();
```

This removes the sidebar's classes and event listeners. To start it again, call `sidebar.reinitialize()`.

## One sidebar at a time

Only one sidebar runs on a page. `new DWCSidebarNavigation(options)` and `DWCSidebarNavigation.createInstance(options)` stop the running sidebar before they start a new one. To change a running sidebar, use `sidebar.reinitialize()` instead.

***

## Page transitions

Some plugins load the next page without a full reload, for example AJAX page transitions. The sidebar handles this itself: with the **reinitOnUrlChange** option on (the template value), it restarts every time the page address changes. See [Sidebar Options](../sidebar-options.md#page-transitions).

If the sidebar still stops working after a transition, restart it from your plugin's "after the page changes" setting. Add this code:

```js
(function () {
  if (typeof sidebar === 'undefined') return;
  const path = window.location.pathname.replace(/\/$/, '');
  sidebar.reinitialize({ ...DWCSidebarConfig, ...(urlConfigMap[path] || {}) });
})();
```

It keeps your per-page options from `urlConfigMap`.

### Bricksforge page transitions

In **Bricksforge > Features > Page Transitions > Compatibility (page:view)**, add the code above.
