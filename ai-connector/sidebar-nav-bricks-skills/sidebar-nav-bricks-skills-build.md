---
icon: sparkles
---

# AI Skills Build Reference

## START HERE

The entry file sent you here because you are on the **build path**. Read this file in full, then
work through the steps in order.

### 0. Read this file first

1. Read every line before your first Bricks write. If a read returns a truncation notice, continue
   with `offset`/`limit` until you reach the last line.
2. State in chat: `"Skill file read: lines 1-[N] of [N], complete."` with the real line count.

### 1. Before you start

**Session type.** Search upward from this file's folder for
`SIDEBAR NAV BRICKS/sidebar-nav-dev-context.md`, checking each ancestor in turn. Found: **developer
session**, read it silently. Not found: **user session**.

**User session only.** Look for `sidebar-nav-bricks-user-context.md` in this file's folder. If it
exists, read it silently. If not, create it with the structure below and tell the user you created it.

```md
# Sidebar Nav Bricks User Context

## Preferences


## Saved Layouts


## Session Notes

```

At the end of a user session, propose additions to it (the entry file's "Ask before you write"
applies). A saved preference in the active context file wins over a default in this file. When you
apply one, tell the user.

**Working directory.** Make a working subdirectory for this task and keep every scratch file in it
(tree snapshots, code fields, scripts). Delete it at the end, except any backup you were told to keep.
Use `node` for scripting and parsing. Never `python` or `jq`.

**Timestamp.** Run `date +%s` before you start work and save the value in your working directory.

### 2. Connect, find the header, check the setup

Follow "Is the site connected" and "Find the header" in the entry file.

**No header:** ask the user to import the template and do the installation steps
(https://design-with-cracka.gitbook.io/sidebarnavbricks/getting-started), then start again. Never build
a sidebar from Bricks elements, and never import the template yourself.

**Setup check**, once per session, from the tree you already read:

* Both code blocks have `executeCode: true`. If not, tell the user to turn on **Execute code** on that
  block in the builder. Don't write `executeCode` yourself.
* The options block's `cssCode` contains `postid-<this template's post ID>` twice. If it still holds
  another ID (the template ships with `29799`), the builder canvas stays blank: offer to fix it
  (Operations, "Template ID").
* `bricks/get-template` shows template conditions. If there are none, ask the user where the sidebar
  should show, then set them with `bricks/set-template-conditions`.

### 3. Scope and confirmation gate

Before any write that changes structure or look, ask the user in **one** question batch:

* **(a) Adjust what is there** (keep the menu, change look or behavior), or **(b) rebuild** (remove
  items and build new ones).
* **Behavior words.** "Collapsible" (shrinks to icons on desktop), "off-canvas" (hidden behind a
  menu button on every screen), "top bar" (a bar above the sidebar), "mobile menu" (always there
  below the breakpoint). If the brief uses one of these loosely, ask which it means.
* **Class names.** If you will create a new global class family, propose two or three base names and
  let the user pick or give their own. Never invent and apply one.
* **Unclear phrases.** List every phrase in the brief with more than one technical reading and
  resolve them in the same batch.
* **Screenshots.** If the user gives design screenshots, ask the browser zoom and window width each
  was taken at.
* **Mega Menu Pro.** If the brief puts Mega Menu Pro in the sidebar, ask for layout A or B (section 6).

**Before option (b):** call `bricks/list-revisions` for the header template, note the latest
revision, and tell the user that is the restore point. Do not remove anything until the user
confirms.

To undo, tell the user to restore from the builder's Revisions panel and save. Never call
`bricks/restore-revision`.

### 4. Order of tools

Use the first tier that can do the job. Name the tier in chat before each write.

1. **JS option** in the options block. Reference section 3.
2. **CSS variable** in the options block. Reference section 5.
3. **Attribute** on the root block or Collapse toggle. Reference section 4.
4. **Bricks element settings or global class styles**, for menu items and content you build.
5. **Custom CSS**, only when nothing above covers it. Say in chat which option, variable or attribute
   you checked and why it does not cover the request.

***

## 5. Operations

Every call goes through `mcp-adapter-execute-ability`. Before the first call of each ability in a
session, read its input schema with `mcp-adapter-get-ability-info`, and follow the schema over this
file where they differ. If an ability offers `dryRun`, use it before the first write of each kind and
before any write that adds or removes elements.

### Read the tree

`bricks/get-page-elements` with the header's `postId`. For the structure only, pass
`includeSettings: false`. For one element, pass `elementId` and `maxDepth: 0`. The engine block's
code fields are about 115 KB: save the response to your working directory and parse it with
`node`, instead of reading it into the chat. Re-read before every write that depends on the current
state.

### Write an element

`bricks/update-element` with `postId`, `elementId` and `settings`. It merges: send only the keys you
change. A top-level key sent as `null` or `""` is deleted. To change several elements in one save,
use `bricks/batch-update-elements`.

Every save rewrites the whole tree's `_cssCustom`: a rule on `#brxe-<id>` alone that repeats a native
setting is removed (the setting stays), and other rules are kept but reformatted.

Read the tree after the write. Confirm the changed value equals your expected text exactly, and that
the other keys are unchanged apart from that `_cssCustom` rewrite.

### Change a JS option

1. Take the options block's `javascriptCode` from the tree.
2. Replace the exact text of the one option line with its indent and line break, for example
   `\n    enableOffCanvas: 0,\n` with `\n    enableOffCanvas: 1,\n`. Confirm the old text occurs
   exactly once. Keep comments and spacing.
3. Write the whole `javascriptCode` back with `bricks/update-element`.

Breakpoint options keep their form: `window.matchMedia("(max-width: 991px)")`. `reinitOnUrlChange`
takes `true` or `false`. Never change `mq` alone (see "Change the breakpoint").

### Change a CSS variable

Same as a JS option, in `cssCode`: replace the one `--name: value;` line inside `:root`. Existing
variables only. Give a zero length a unit (`0px`): the collapsed width is a `calc()` over
`--sidebar-panel-inline-padding`, `--sidebar-link-inline-padding` and `--sidebar-link-icon-size`, and
a bare `0` breaks it.

### Per-page options

Add entries to `urlConfigMap` outside its `/* ... */` comment. Key: the page path without domain and
trailing `/`; the home page is `''`. Only the options that change.

### Change an attribute

In the element's `_attributes` array, change the `value` of the row with that `name`. On is `"true"`,
off is `""`. Keep every row and its `id`.

### Template ID

In the options block's `cssCode`, replace each `postid-<old ID>` with `postid-<template post ID>`.
There are two. Confirm both changed.

### Change a link, text or icon

* Link: the block labelled **link** (tag `a`) inside the `li`: its `link` setting.
* Text: the `text-basic` child with `dwc-nav__link__text`: its `text` setting.
* Icon: the `icon` child with `dwc-nav__link__icon`: its `icon` setting.

Copy the value shape from an existing element of the same kind in the tree.

### Add a menu item

1. Pick an existing item of the same kind (reference section 2). Copy its subtree from the tree.
2. Leave out every element `id`: `bricks/add-element` makes new ones. Give every `_attributes` row a
   new 6-character `id`. Keep `_cssGlobalClasses`, `tag`, `customTag` and every other setting.
3. Change the text, link and, for a slide button, `data-title`.
4. Add it with `bricks/add-element` under the target **List &lt;ul&gt;**, at the position the user wants
   (`position`, from 0), as one nested `{name, label, settings, children}` tree.

### Add a slide panel

1. Copy an existing **Slide panel** subtree (step 2 above). Its parent is **Nav**, never another panel.
   Keep `dwc-slide-right` in its classes.
2. Set its `data-title` to a readable, unique name. Visitors see it as "back to <name>".
3. Set its **Panel title** heading `text`, and build its list.
4. Add an **li - slide button** where the user wants it. Set the inner slide button's `data-title`
   to the panel's name, exactly.

A panel's depth comes from the slide button that opens it. Every panel stays a direct child of Nav.

### Add a dropdown inside a dropdown

Copy an **li - dropdown** subtree into another dropdown's **dropdown content > List &lt;ul&gt;**. Level
classes and level variables (`--lvl-2-*`, `--lvl-3-*`) apply on their own.

### Remove a menu element

`bricks/remove-element` removes the element and everything inside it. Before removing more than one,
list them to the user and wait for agreement. Never remove the Home panel, a code block, the Header
inner wrap, the Hamburger Wrapper or the Mobile menu overlay.

### Change the breakpoint

Three edits, all in one go. Use the user's widths; the desktop width is the mobile width + 1.

1. Options block `javascriptCode`: `mq` to `window.matchMedia("(max-width: <mobile>px)")`.
2. Engine block `cssCode`: `@media (min-width: 1025px)` to `@media (min-width: <desktop>px)`.
3. Engine block `cssCode`: `@media (max-width:1024px)` to `@media (max-width:<mobile>px)`.

Confirm each old text occurs exactly once before you replace it. This is the only write to the engine
block. If the engine CSS has `@media (width <= 1024px)` (the admin bar reset), leave it as it is. Send
both blocks in one `bricks/batch-update-elements` call, then compare each field's read-back with your
expected text. If off-canvas is limited to mobile through `offCanvasBreakpoint`, change it to match.

Never raise the breakpoint to get the menu button on desktop: set `enableOffCanvas` to `1`.

### Dynamic navigation

Build the query loops from reference section 9, with the general Bricks skills `bricks-query-loops`
and `bricks-global-queries` for the setting shapes. Ask before installing the category plugin; it's the
user's step if you have no plugin ability. Verify on a real page that uses the header, not the template
preview.

### Your own CSS

* Put it on an element of the sidebar header (`_cssCustom`) or in a global class. In `_cssCustom`
  through the MCP, write full rules with the element's persisted selector `#brxe-<id>`, not `%root%`.
* The engine CSS loads inside the header, after class CSS in the page head, so it wins ties. Start
  every selector with `#brx-header` or `#brxe-<id>`, after a leading `body…` part if any.
* Desktop-only rules start with `body:not(.dwc-mobile)`, mobile-only rules with `body.dwc-mobile`.
  Never use a bare `.dwc-mobile`: Mega Menu Pro puts its own `dwc-mobile` on `<html>`.
* Collapsed-only rules start with `body.dwc-collapse-sidebar`.
* Include the rules below the breakpoint in the same pass.
* After every save, fetch the published page and find one unique string from each rule you saved.
* Keep all your CSS in one local file in your working directory and save each element or class from
  it.

### Import, revisions, files

* Never import the template, and never call `bricks/import-transfer-package` or
  `bricks/restore-revision` on the sidebar header.
* If `bricks/get-template` or the page report `cssLoading: "file"`, call `bricks/regenerate-css-files`
  after style changes.

***

## 6. Mega Menu Pro in the sidebar

Mega Menu Pro **Lite** goes inside the sidebar's **Header inner wrap** as a Section template, through a
Template element. Customer guide: https://design-with-cracka.gitbook.io/sidebarnavbricks/guides/mega-menu-pro

**Layouts** (ask in the gate):

* **A. Mega Menu Pro on desktop, sidebar on mobile:** `enableOffCanvas: 1`, plus the hide rules in
  step 7.
* **B. Both on every screen:** `enableTopBar: 1`, `enableOffCanvas: 0`. No hide rules. Test the
  collapsible sidebar before you leave it on with the top bar.

Two sidebar headers with different conditions can use layouts A and B with the same Mega Menu Pro
template. Each header carries its own options and hide rules.

**Who can write where:**

* The sidebar header: Bricks' element abilities, as in section 5.
* Mega Menu Pro while it is a **Header** template: the MMPro AI Abilities plugin (`mmpro/*`) and the
  Mega Menu Pro Bricks skill (`mmpro-bricks-skills/mega-menu-pro-bricks-skills.md`), if both are in the
  project.
* Mega Menu Pro once it is a **Section** template: only `mmpro/set-template-type`. Other `mmpro/*`
  abilities return `not_header`, and Bricks' element abilities reject Mega Menu Pro's Nav (Nestable)
  tree. To change it, switch it to header, make the change, and switch it back. The Template element
  shows nothing in between.

**Steps, in order:**

1. **Check the version.** Find the Mega Menu Pro template: `bricks/list-templates` (header and section
   types), root `section` label `Header Pro | v<version> Lite`. Without `Lite`, stop and tell the user
   the sidebar needs the Lite template.
2. **Match the breakpoints while Mega Menu Pro is still a Header template.** Default: keep the
   sidebar's 1024px and set Mega Menu Pro's desktop width to 1025px. With `mmpro/get-header`
   available, follow the Mega Menu Pro skill and call `mmpro/set-breakpoint` with `desktopMinWidth`
   `1025`. Without it, give the user the steps from
   https://design-with-cracka.gitbook.io/bricksmegamenupro/menu-options#breakpoint. Make every other
   Mega Menu Pro change the user wants now, for the same reason.
3. **Make it a Section template** with `mmpro/set-template-type`, `type: "section"` (MMPro AI
   Abilities 0.5.0 or later). If the template has conditions, it refuses until you pass
   `acknowledgeConditions: true`. Ask the user first: it stops showing as the site's header. Without
   that ability, it is a user step: in WordPress, **Bricks > Templates**, **Edit** (not Edit with
   Bricks) on the Mega Menu Pro template, **Template Type** from **Header** to **Section**, **Update**.
   Wait for the user, then confirm with `bricks/list-templates`, type `section`.
4. **Add the Template element** with `bricks/add-element`: `postId` the sidebar header, parent the
   Header inner wrap, position just before the Hamburger Wrapper, element
   `{ name: "template", settings: { template: "<Mega Menu Pro post ID>", _width: "auto" } }`. One shared
   Mega Menu Pro template for every sidebar header: never copy its elements into a header.
5. **Options** in the sidebar's options block, for the layout. Both layouts: set `data-topbar-active`
   to `"true"` on the root block.
6. **Spacing.** Add to the Header inner wrap's `_cssCustom`, for both layouts:

   ```css
   #brxe-<header inner wrap ID> > .brxe-template { flex: 1 1 0; min-width: 0; }
   ```

   Remove the bar's block padding where Mega Menu Pro shows, or its dropdowns open inside the bar.
   Layout B: `--sidebar-header-block-padding: 0px` in the options block. Layout A: in the Header
   inner wrap's `_cssCustom`,
   `@media (min-width: 1025px) { #brxe-<header inner wrap ID> { --sidebar-header-block-padding: 0px; } }`,
   so the mobile bar keeps its padding. Position the logo, Template element and Hamburger Wrapper
   with the Header inner wrap's flex settings (`_justifyContent`, `_alignItems`), never with margins.
7. **Layout A rules**, in the Header inner wrap's `_cssCustom` (append to what is there), with the
   real widths and the element's ID:

   ```css
   @media (min-width: 1025px) {
     #brxe-<header inner wrap ID> .dwc-hamburger-wrap { display: none; }
   }
   @media (max-width: 1024px) {
     #brxe-<header inner wrap ID> > .brxe-template { display: none; }
   }
   ```

   They live in this header, so a layout B header with the same Mega Menu Pro template is unaffected.
   Never put them in the Mega Menu Pro template or on the Template element.
8. **One logo.** Where Mega Menu Pro shows, recommend its logo: it sits inside its container. To hide
   the sidebar's Logo there, layout B: `#brxe-<header inner wrap ID> > .brxe-logo { display: none; }`;
   layout A: the same rule inside the `@media (min-width: 1025px)` block. If the user keeps the
   sidebar's Logo next to Mega Menu Pro, add
   `#brxe-<header inner wrap ID> > .brxe-logo { flex-shrink: 0; }`.

**Mega Menu Pro problems inside the sidebar:**

* An extra bar at the top of Mega Menu Pro's mobile menu (layout B): builder step. On Mega Menu Pro's
  **mobile top bar** element, custom CSS `%root%::before { display: none; }`.
* Both menus, or neither, between two widths: the breakpoints differ. Measure where `<html>` gets
  `dwc-mobile` (Mega Menu Pro) and where `<body>` gets it (sidebar).
* Mega Menu Pro missing from the Template element's list: it is still a Header template (step 3).
* Mega Menu Pro's logo is empty: the template file's SVG points to the site it came from. Import it
  with `logoAttachmentId`, or set the logo in the builder.

***

## 7. Rules & gotchas

### Options

* `enableTopBar` needs `enableOffCanvas: 0`. `overlayTopBar` needs `enableOffCanvas: 1`.
  `overlaySidebar` needs `enableOffCanvas: 0`.
* `enableHeadroom` needs `enableOffCanvas` or `enableTopBar`, and stops working with
  `offCanvasPushContent`.
* The collapsible sidebar is desktop only and off whenever `enableOffCanvas` is `1`, at every width,
  even where `offCanvasBreakpoint` doesn't match.
* `offCanvasBreakpoint` defaults to every width. Below `mq` there is always a mobile menu: don't turn on
  off-canvas to get one.
* `updateBackText` writes `back to <data-title>`. For other wording, set it to `0` and change the
  Back to button's text element.
* `urlConfigMap` is read once at page load. `sidebar.reinitialize()` doesn't apply it.

### Panels and data-title

* A slide button opens the panel with the same `data-title`. Exact match, case and spaces included.
* Each panel's `data-title` is unique. With two the same, the button opens the first one.
* Use readable names: they are visible ("back to Services") and spoken ("Services menu").
* Every panel is a direct child of Nav.

### Code blocks

* You edit the options block. The engine block only for the breakpoint (section 5).
* Bricks' Templates > Import turns off Execute code on both blocks. The user turns it back on.
* Don't remove the 4 "AT - Clamp Settings" global variables the import adds.

### Header

* Keep the template setting `headerWidth` at `var(--sidebar-width)`. Change the width with
  `--sidebar-width`.
* `headerPosition` `left` or `right` puts the sidebar on that side.
* Logged-in users have the WordPress admin bar. Offset anything you fix to the top with
  `var(--wp-admin--admin-bar--height, 0px)`.

***

## 8. Verification

A read-back proves configuration. Only the published page proves rendering. Say which you reached.

**A check that finds nothing is a failed check.** A selector that matches nothing returns `0` or
`null`. Prove the element was found before you report on it.

**1. Fetch the published page** with a unique query string (`?nocache=<timestamp>`). The plain URL can
be an old cached copy. The header renders for logged-out visitors on any page its conditions cover.
Grep for what you changed: an option value, a variable, an attribute, a class, a link.

**2. Use your own headless browser** for position, size, computed style and behavior:
`sidebar-test.mjs` in this folder. It needs Node 22+ and Chrome, and launches its own Chrome with a
temporary profile. The import path is relative to your script.

```js
import { open } from '../sidebar-nav-bricks-skills/sidebar-test.mjs';
const b = await open({ url: 'https://example.com/', width: 390, height: 844, mobile: true });
try {
  await b.tap('.dwc-nav-trigger'); await b.settle();
  console.log(await b.fn(() => document.body.className), await b.box('.dwc-sidebar__nav'), b.errors);
  await b.shot('menu.png');
} finally { await b.close(); }
```

* Never attach to the user's own Chrome or ask them to relaunch theirs with a debugging port.
* Elements without their own styles have no `id` on the page: find them by class or text. Only
  elements with element-level styles or `_cssCustom` get `id="brxe-<id>"`.
* **The sidebar's code is running** when `<body>` has `sidebar-ready`. If not, the code blocks did not
  run: stop and tell the user (entry file, invariants).
* **Options:** `sidebar.config.<option>` in the page is the live value.
* **Variables:** `getComputedStyle(document.documentElement).getPropertyValue('--name')`.
* Check desktop and a width below the breakpoint (`body` has `dwc-mobile`). Below it, also run once
  with `adminBar: true`.
* Open the mobile or off-canvas menu with `tap('.dwc-nav-trigger')`, a slide panel with
  `click('.dwc-sidebar__nav__btn[data-title="<name>"]')`, collapse with `click('.dwc-toggle-collapse')`.
  Then `settle()` before measuring. An open panel has neither `dwc-slide-left` nor `dwc-slide-right`,
  and `inert` is false.
* Current-page behavior runs late: wait 2500 ms after load before you check which panel or dropdown
  opened.
* `saveCollapseState` keeps state in `localStorage`. Each `open()` starts with an empty profile.
* When a rule of yours doesn't apply, run `why(selector, property)` before you change anything.
* In test URLs use `nocache` or long keys only. WordPress treats short keys such as `m`, `w`, `p` and
  `s` as its own and serves a different page.

**What you cannot check**, and must hand to the user: the builder view (the blank-canvas fix, builder
labels), drafts, and logged-in-only content.

***

## 9. Agent Skills Update routing (developer sessions)

| Discovery | Where it goes |
| --- | --- |
| New operation or ability pattern | Section 5: Operations |
| Mega Menu Pro combination | Section 6 |
| Mistake to avoid, ability behavior | Section 7: Rules & gotchas |
| Option, attribute, variable or class | Reference file, matching section |
| Verification technique | Section 8: Verification |

One line or a short code block. Confirmed only. State it as a present-tense rule: no dates, no
story, no "an earlier version said".
