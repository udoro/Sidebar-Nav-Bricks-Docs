---
icon: sparkles
---

# AI Skills Reference Tables

Sidebar Navigation Builder for Bricks, version 3.0.2. Grep the section you need. Never read this file in full.

Customer docs: https://design-with-cracka.gitbook.io/sidebarnavbricks

## 1. Fingerprint

* Root element: `block`, label `Sidebar Nav 3.0.2`, global classes `dwc-sidebar` and `dwc-offcanvas-header`.
* Options code block: `code` element whose `javascriptCode` contains `const DWCSidebarConfig`. Template label `Sidebar Options CSS/JS`. First child of the root.
* Engine code block: `code` element whose `javascriptCode` contains `class DWCSidebarNavigation`. Template label `Sidebar CSS and JS`. Last child of the root. Its last line logs `<Sidebar Nav Builder v3.0.2>`.
* Template settings: `headerPosition` `left` (or `right`), `headerWidth` `var(--sidebar-width)`.
* The import adds 4 global variables in the category "AT - Clamp Settings": `min-viewport`, `max-viewport`, `base-font`, `clamp-unit`. Never remove them.

For another version, compare the live option names and attributes with sections 3 and 4. The live code wins.

## 2. Element map

Labels are the template's. Users can rename them: match by global class first.

| Label | Element | Tag | Global classes | Attributes | Notes |
| --- | --- | --- | --- | --- | --- |
| Sidebar Nav 3.0.2 | block | div | `dwc-sidebar`, `dwc-offcanvas-header` | section 4 | Root. |
| Sidebar Options CSS/JS | code | | | | The one code block you edit. |
| Header inner wrap | block | div | `dwc-header-inner-wrap` | | Top of the sidebar; the top bar with `enableTopBar` or `enableOffCanvas`. Children: Logo, Hamburger Wrapper, Collapse toggle. Mega Menu Pro's Template element goes here. |
| (Logo) | logo | | `dwc-sidebar__logo` | | |
| Hamburger Wrapper | div | | `dwc-hamburger-wrap` | | |
| Hamburger Trigger | div | custom `button` | `dwc-nav-trigger` | `aria-expanded`, `aria-label` | Opens the mobile and off-canvas menu. |
| Collapse toggle | div | custom `button` | `dwc-toggle-collapse` | `data-static` | Child: icon. |
| Nav | div | `nav` | `dwc-sidebar__nav` | | Every panel is a direct child. |
| Home panel | block | | `dwc-sidebar__nav__panel`, `dwc-sidebar__nav__panel--home` | `data-title` `Home` | Children: Inner wrap, Panel footer. |
| Slide panel | block | | `dwc-sidebar__nav__panel`, `dwc-slide-right` | `data-title` | Children: Panel header, Inner wrap. Keep `dwc-slide-right` on every non-home panel. |
| Inner wrap | block | | `dwc-nav__panel__inner` | | |
| Panel header | block | | `dwc-nav__panel__header` | | Children: Home button, Back to button. |
| Home button | block | custom `button` | `dwc-nav__home-btn` | `title` | Children: icon, text with `screen-reader-text`. |
| Back to button | block | custom `button` | `dwc-sidebar__nav__btn`, `dwc-nav__back-btn` | | Child text: `dwc-nav__back__text`. |
| Panel title | block | | `dwc-nav__panel__title-wrap` | | Child heading: `dwc-nav__panel__title`. |
| List &lt;ul&gt; | block | `ul` | `dwc-sidebar__nav__ul` | | |
| li - link | block | `li` | `dwc-sidebar__nav__li` | | Child `link` (block, tag `a`, `dwc-sidebar__nav__link`) > icon `dwc-nav__link__icon` + text-basic (span) `dwc-nav__link__text`. |
| li - slide button | block | `li` | `dwc-sidebar__nav__li` | | Child `slide button` (block, custom `button`, `dwc-sidebar__nav__btn`, attribute `data-title`) > icon, text-basic `dwc-nav__link__text`, chevron icon `dwc-nav__link__icon--chevron-right` + `dwc-nav__link__icon`. |
| li - dropdown | block | `li` | `dwc-sidebar__nav__li`, `dwc-sidebar__dropdown` | | Children: `dropdown toggle` (`dwc-sidebar__dropdown-toggle`) > icon, text, `button` (custom tag) > chevron; `dropdown content` (`dwc-sidebar__dropdown-content`) > List &lt;ul&gt; > li items. |
| Panel footer | block | | `dwc-sidebar__nav__panel-footer` | | Social icons (`dwc-social-wrapper`), CTA button (`dwc-cta`, `dwc-hide`, `dwc-fade`). |
| Mobile menu overlay | block | | `dwc-mobile-menu-overlay` | `tabindex` `0` | |
| Sidebar CSS and JS | code | | | | Engine. Never edit, except the breakpoint (section 7). |

## 3. JS options

`DWCSidebarConfig` in the options block's `javascriptCode`. `1` on, `0` off.

| Option | Template | Needs / limits | Effect |
| --- | --- | --- | --- |
| `mq` | `window.matchMedia("(max-width: 1024px)")` | Change with the two engine media queries (section 7) | Mobile breakpoint. |
| `offCanvasBreakpoint` | `window.matchMedia("(max-width:10024px)")` | | Off-canvas applies at this width and below: every screen by default. |
| `updateBackText` | `1` | | Back to button text becomes `back to <data-title of the target panel>`. The words "back to" are fixed in the engine. |
| `autoCurrentPosition` | `1` | Skipped while collapsed | Slides to the panel holding the current page's link, 1000 ms after start. A current link in a dropdown opens its dropdown 2000 ms after start, whatever this option is. |
| `enableTopBar` | `0` | `enableOffCanvas: 0` | Header inner wrap becomes a full-width bar above the sidebar. |
| `enableOffCanvas` | `0` | | Sidebar hidden off screen, opened by the Hamburger Trigger. Disables the collapsible sidebar at every width. |
| `offCanvasPushContent` | `0` | `enableOffCanvas: 1` | Pushes the page instead of covering it. Disables headroom. Wraps header, main and footer in `dwc-site-wrapper`. |
| `fixedNavTrigger` | `1` | Push content, desktop only | Keeps the trigger in place. |
| `mobileMenuAboveHeader` | `1` | | Mobile and off-canvas menu covers the top bar. |
| `openFirstDropDown` | `0` | | Opens the first dropdown 600 ms after start. |
| `autoCloseDropdown` | `1` | | Closes a dropdown when keyboard focus leaves it. |
| `overlaySidebar` | `0` | `enableOffCanvas: 0` | Sidebar over the content. Blur: `--overlay-sidebar-blur`. |
| `overlayTopBar` | `0` | `enableOffCanvas: 1` | Top bar over the content. |
| `enableHeadroom` | `1` | `enableOffCanvas` or `enableTopBar` is `1`; not with `offCanvasPushContent` | Hides the bar on scroll down after 200px, shows it on scroll up. |
| `enableRTL` | `0` | | Sets `dir="rtl"` on `<html>`: the whole page. |
| `calcTopPadding` | `1` | Off-canvas, or top bar plus headroom | Adds the bar's height as top padding to the first child of `<main>` and to every panel. |
| `offsetHashLinkScroll` | `1` | | Same-page anchor links scroll to the target minus the Header inner wrap's height. |
| `enableCollapsibleSidebar` | `0` | Desktop only; off whenever `enableOffCanvas` is `1` | Collapse toggle shrinks the sidebar to icons. |
| `collapseOnPageLoad` | `0` | Collapsible | Starts collapsed. |
| `restoreActivePanelOnExpand` | `1` | Collapsible | Reopens the panel and dropdowns that were open before collapsing. |
| `saveCollapseState` | `1` | Collapsible | Stores `sidebarCollapsed` (`"true"`/`"false"`) in `localStorage`. |
| `hoverToExpandSidebar` | `0` | Collapsible | Expands on mouse enter, collapses on mouse leave. |
| `collapseAutoWidth` | `1` | Collapsible | Collapsed width from padding and icon variables (section 5). `0`: `--sidebar-collapse-width`. |
| `enableTooltips` | `1` | Collapsed state | Copies each link's, button's and dropdown toggle's text to `data-tooltip`. |
| `reinitOnUrlChange` | `true` | `true`/`false`, not `1`/`0` | Restarts the sidebar when the URL changes without a reload (Navigation API, else `pushState`/`replaceState`/`popstate`). |

`debugTooltips` is commented out in the template: developer only.

### Per-page options

`urlConfigMap`, below `DWCSidebarConfig` in the same field. Its template entries sit inside `/* ... */` and do nothing.

```js
const urlConfigMap = {
  '/docs': { enableOffCanvas: 1, enableCollapsibleSidebar: 0 }
};
```

* Key: `location.pathname` without the trailing `/`. Home page: `''`. Exact match only.
* The value is merged over `DWCSidebarConfig` once, at page load.

### Runtime names

`sidebar` (the instance), `DWCSidebarConfig`, `urlConfigMap` and the class `DWCSidebarNavigation` are top-level `const`/`class` declarations in classic scripts. They are global names but not `window` properties.

* `sidebar.reinitialize(options)`: `config = { ...DWCSidebarConfig, ...options }`, then cleanup, re-cache elements, init. Does not apply `urlConfigMap`.
* `sidebar.cleanup()`: removes body classes and listeners.
* `new DWCSidebarNavigation(options)` and `DWCSidebarNavigation.createInstance(options)`: clean up every running instance first. One sidebar per page.
* `sidebar.config`: the live options. Read it in the browser to verify an option.

## 4. Attributes

On the root block (`Sidebar Nav 3.0.2`). On: `"true"`. Off: empty value, attribute kept.

| Attribute | Template | On means |
| --- | --- | --- |
| `data-topbar-active` | empty | Header inner wrap fixed at the top and hidden until the script runs: no flash of unstyled top bar. Use with `enableTopBar` or `enableOffCanvas`. |
| `data-push-footer` | `true` | Nav scrolls; Panel footer sits after the menu. Off: panels fill the sidebar height and the Panel footer stays at the bottom. |
| `data-overlap-collapsible` | empty | Collapsible sidebar covers content instead of resizing it. |
| `data-style-svg-stroke` | empty | SVG link icons get `stroke` from the icon color variables. |
| `data-partition-dropdown` | empty | Dropdown toggle split: text, plus the chevron `button` in its own box with a divider. Colors: `--sidebar-dropdown-button-*`, `--sidebar-dropdown-chevron-*`. |

On Collapse toggle:

| Attribute | Template | On means |
| --- | --- | --- |
| `data-static` | empty | Toggle stays in the layout flow instead of `position: absolute`. |

On panels and slide buttons: `data-title`. See build file, section 7.

## 5. CSS variables

In `:root` of the options block's `cssCode`. One declaration per line.

| Group | Variables (template value) |
| --- | --- |
| Sidebar | `--sidebar-width` (`min(90vw, 300px)`, also the mobile and off-canvas menu width), `--sidebar-header-bg` (`silver`, Header inner wrap), `--sidebar-nav-bg` (`white`), `--sidebar-header-block-padding` (`1rem`, Header inner wrap top/bottom only), `--sidebar-header-inline-padding` (`1.25rem`), `--sidebar-shadow` |
| Menu button | `--sidebar-hamburger-color` (`gray`), `--sidebar-hamburger-bg` (`transparent`) |
| Links | `--sidebar-link-color` (`dimgray`), `--sidebar-link-bg`, `--sidebar-link-icon-color` (`dimgray`), `--sidebar-link-txt-size` (`0.875rem`), `--sidebar-link-icon-size` (`24px`), `--sidebar-link-inline-padding` (`1rem`), `--sidebar-link-block-padding` (`0.7rem`), `--sidebar-link-border-radius` (`5px`, also the CTA), `--sidebar-link-underline` (`var(--sidebar-footer-top-border)`), `--sidebar-link-transition` (`500ms`), `--sidebar-link-gap` (`1.125rem`, icon to text), `--sidebar-link-hover-color` (`black`), `--sidebar-link-hover-bg` (`rgb(0 0 0 / 5%)`), `--sidebar-link-icon-hover-color` (`black`) |
| Dropdown links | `--sidebar-dropdown-link-color`, `--sidebar-dropdown-link-bg`, `--sidebar-dropdown-link-underline` (`none`), `--sidebar-dropdown-content-bg` (`rgb(0 0 0 / 5%)`), `--sidebar-dropdown-link-hover-color`, `--sidebar-dropdown-link-hover-bg`, `--sidebar-dropdown-link-indent` (`10px`) |
| Partitioned dropdown | `--sidebar-dropdown-button-bg` (`white`), `--sidebar-dropdown-button-hover-bg` (`black`), `--sidebar-dropdown-button-active-bg` (`black`), `--sidebar-dropdown-chevron-hover-color` (`white`), `--sidebar-dropdown-chevron-active-color` (`white`) |
| Lists, chevrons | `--sidebar-list-items-block-padding` (`1.25rem`), `--sidebar-list-gap` (`0`), `--sidebar-chevron-size` (`1rem`), `--sidebar-chevron-color` |
| CTA | `--sidebar-cta-color` (`white`), `--sidebar-cta-bg` (`dimgray`), `--sidebar-cta-hover-bg` (`black`) |
| Social | `--sidebar-social-link-color`, `--sidebar-social-link-bg`, `--sidebar-social-icon-color`, `--sidebar-social-icon-size` (`1.5rem`), `--sidebar-social-link-hover-color`, `--sidebar-social-link-hover-bg`, `--sidebar-social-icon-hover-color` |
| Panels | `--sidebar-panel-title-size` (`1.125rem`), `--sidebar-panel-title-color` (`black`), `--sidebar-panel-title-bg`, `--sidebar-panel-label-color` (`orangered`, builder-only labels), `--sidebar-panel-backtext-font-size` (`0.6rem`), `--sidebar-panel-backtext-color`, `--sidebar-panel-block-padding` (`clamp(0.5rem, -1.375rem + 5vh, 2rem)`), `--sidebar-panel-inline-padding` (`0.5rem`), `--sidebar-panel-shadow` |
| Panel footer | `--sidebar-footer-top-border` (`1px solid rgb(0 0 0 / 10%)`), `--sidebar-footer-block-padding` (`1.25rem`), `--sidebar-footer-inline-padding` |
| Current link | `--sidebar-current-link-bg` (`rgba(0, 0, 0, 0.05)`), `--sidebar-current-link-underline` (`solid 3px gray`) |
| Collapsed | `--sidebar-collapse-icon-bg`, `--sidebar-collapse-icon-size` (`35px`), `--sidebar-collapse-icon-color` (`#B1B1B1`), `--sidebar-collapse-width` (`80px`, only with `collapseAutoWidth: 0`), `--sidebar-collapse-ttf` |
| Tooltips | `--sidebar-tooltip-font-size` (`10px`), `--sidebar-tooltip-font-color` (`white`), `--sidebar-tooltip-bg` (`black`), `--sidebar-tooltip-radius`, `--sidebar-tooltip-inline-padding`, `--sidebar-tooltip-block-padding` |
| Backdrop, overlay | `--sidebar-backdrop-overlay-bg` (`black`), `--sidebar-backdrop-overlay-opacity` (`0.5`), `--overlay-sidebar-blur` (`blur(0px)`, with `overlaySidebar`) |
| Motion | `--sidebar-transition` (`400ms`), `--sidebar-ttf` (`var(--material-design-ttf)`), `--material-design-ttf`, `--default-ttf` (only as a value for `--sidebar-ttf`), `--sidebar-opacity-transition` (`500ms 200ms`) |
| Spacing | `--sidebar-padding-m` (`1.25rem`, Hamburger Trigger padding), `--sidebar-padding-s` (`0.75rem`, Home button, panel title top/bottom), `--sidebar-padding-xs` (`0.5rem`, panel title sides), `--sidebar-content-gap` (`0`, gap in Header inner wrap and Panel header) |
| Focus | `--sidebar-focus-outline-color` (`black`), `--sidebar-focus-outline-width` (`2px`), `--sidebar-focus-outline-offset` (`4px`) |
| Dropdown levels | `--lvl-2-indent`, `--lvl-3-indent`; `--lvl-1/2/3-toggle-bg-active`; `--lvl-1/2/3-content-bg`; `--lvl-2/3-toggle-color-active`; `--lvl-1/2/3-icon-color`; `--lvl-2/3-icon-hover-color`; `--lvl-1/2/3-icon-size` (level 1 `var(--sidebar-link-icon-size)`, levels 2 and 3 `calc(var(--sidebar-link-icon-size) * 0.75)`) |

Read by nothing in 3.0.2, so changing them does nothing: `--sidebar-cta-hover-color`, `--skip-link-color`, `--skip-link-background`, `--lvl-1-toggle-color-active`, `--lvl-1-icon-hover-color`. The CTA's hover text color is set on the `dwc-cta` class (`#ffffff`).

Collapsed auto width, in the `.dwc-auto-width` rule below `:root`:
`--sidebar-collapse-width: calc((var(--sidebar-panel-inline-padding) * 2) + (var(--sidebar-link-inline-padding) * 2) + (var(--sidebar-link-icon-size) * var(--icon-size-multiplier)))`, with `--icon-size-multiplier: 0.8`. Set the multiplier to the rendered icon width divided by `--sidebar-link-icon-size`. Measured at template values: 67px.

## 6. Classes

On `<body>`:

| Class | When |
| --- | --- |
| `show-nav`, `sidebar-ready` | The script has run. |
| `dwc-mobile` | `mq` matches. |
| `dwc-slide-nav-open`, `dwc-no-scroll` | Mobile or off-canvas menu open. |
| `dwc-offcanvas` | `enableOffCanvas` and `offCanvasBreakpoint` matches. |
| `dwc-push-content`, `dwc-nav-trigger-is-fixed` | Push content; fixed trigger. |
| `dwc-topbar-enabled` | `enableTopBar` without off-canvas. |
| `dwc-overlay-sidebar`, `dwc-overlay-topbar` | Overlay options. |
| `dwc-mobile-menu-over` | `mobileMenuAboveHeader`. |
| `dwc-collapse-enabled`, `dwc-auto-width` | Collapsible on; auto width. |
| `dwc-collapse-sidebar`, `dwc-is-collapsed` | Collapsed. |
| `dwc-headroom`, `scroll-down`, `scroll-up` | Headroom; last scroll direction. |
| `hasHeaderHeight` | Header height measured. |

On elements: `dwc-current-menu-item` on the current page's link; `dwc-slide-left` on a panel moved out to the left, `dwc-slide-right` on a closed panel (open panel: neither); `level-1`, `level-2`... on dropdown toggles; panels get `inert` while closed and `aria-label` `<data-title> menu`.

Helper class: `dwc-hide` (opacity 0 while collapsed). `dwc-fade` and `dwc-show` have no effect in 3.0.2: don't use them.

## 7. Code block fields

Options block (`Sidebar Options CSS/JS`), settings `javascriptCode`, `cssCode`, `executeCode: true`, `noRoot`, `_cssCustom` (`#brxe-<id>{ display: none }`, keep it):

* `javascriptCode`: `DWCSidebarConfig`, then `urlConfigMap`.
* `cssCode`: `:root { ... }` variables, the `.dwc-auto-width` rule, then after `/* INSIDE BRICKS */` two selectors containing `.postid-29799`: the template's own post ID goes there (`postid-<template ID>`). Until it matches, the builder canvas is blank. The frontend doesn't depend on it.

Engine block (`Sidebar CSS and JS`), `cssCode` holds the only breakpoint widths outside `mq`:

* `@media (min-width: 1025px)`: one occurrence. Desktop width.
* `@media (max-width:1024px)`: one occurrence, no space after the colon. Mobile width.

No code field in either block contains a backslash.

## 8. Mega Menu Pro Lite inside the sidebar

| Thing | Value |
| --- | --- |
| Version check | Mega Menu Pro root `section` label `Header Pro \| v<version> Lite`. Without `Lite`: Full, not supported in the sidebar. |
| Breakpoint | Desktop from `1201px`, mobile `1200px` and below, unless changed. |
| Mobile class | Mega Menu Pro puts `dwc-mobile` on `<html>`; the sidebar puts it on `<body>`. |
| Menu wrap | `div`, label `Menu wrap`, class `dwc-menu-wrap`. Holds Nav (Nestable) and its mobile toggle. |
| Logo | `div`, label `Logowrap (link)`, class `dwc-nest-menu__logo`, next to Menu wrap. |
| Mobile top bar | `block`, label `mobile top bar`, class `dwc-nest-menu-top`. |
| Template element | `name: "template"`, `settings.template`: the Mega Menu Pro template's post ID as a string. |
| MMPro AI Abilities | `mmpro/*` abilities read and write Header templates only. A Section template returns `not_header`. |

## 9. Dynamic navigation query settings

Pages need the categories `menu item` and `has child` (the "Pages with category and tag" plugin gives pages categories). Use the general Bricks skill `bricks-query-loops` for the exact query object.

| Element | Query |
| --- | --- |
| li - link (Home panel) | Pages, parent `0`, include term `menu item`, exclude term `has child`. Text `{post_title}`, link `{post_url}`. |
| li - slide button | Pages, parent `0`, include term `has child`. Text `{post_title}`. Slide button `data-title` `{post_title}`. |
| li - dropdown | Same query as li - slide button. Use one of the two for parent pages, never both. |
| Slide panel | Pages, include term `has child`. `data-title` `{post_title}`. |
| li - link inside a slide panel or dropdown | Pages, parent `{post_id}`, include term `menu item` (optional), exclude term `has child`. |

Parent page titles must be unique: `data-title` links button and panel by title.
