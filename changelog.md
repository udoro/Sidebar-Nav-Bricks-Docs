---
icon: clock-rotate-left
---

# Changelog

You'll find every version's template in your Gumroad library.

## 3.0.2 - October 16, 2026

### New

- **Docs and AI Connector.** These docs, with a guide to [using the sidebar with Mega Menu Pro](guides/mega-menu-pro.md), and skills that let an AI agent set up your sidebar.
- **`reinitOnUrlChange` option.** Choose whether the sidebar restarts on page transitions. It's on by default. See [Sidebar Options](sidebar-options.md).
- **`sidebar-ready` class.** `<body>` gets it once the sidebar has loaded. See [Attributes & Classes](attributes-and-classes.md).

### Improved

- **Page transitions.** The sidebar updates right after the new page loads, not two seconds later. Links to a section on the same page no longer restart it.
- **Short screens.** On screens 667px tall or less, panels only show a scrollbar when they need one.
- **New default colors** for the top bar (silver) and the menu button (gray).

### Fixed

- **Logged in?** The top bar and the mobile menu no longer hide behind the WordPress admin bar.
- **CTA button.** Its hover color now shows.

## 3.0.1 - September 27, 2025

### New

- **Partition style dropdown.** The dropdown button is styled apart from the link text.

### Fixed

- The `calcTopPadding` option works again.

## 3.0 - September 6, 2025

### New

- Import the template directly in Bricks. No more copying and pasting JSON.
- Full RTL support.
- Per-page options, for example a sidebar on the home page and off-canvas on the docs pages.
- Collapsible sidebar: works in more layouts, shows tooltips, reopens the active panel or dropdown when it expands, and can overlap the page instead of pushing it.
- Restarts on AJAX or URL changes, for page transitions.

### Improved

- Rebuilt code for better speed and stability.
- Clearer CSS variable names and groups.
- General fixes.

## 2.5.1 - January 14, 2025

- Bug fixes.

## 2.5 - November 12, 2024

- New: collapsible sidebar, with options.
- New: when headroom is on, scrolling to a `#` link leaves room for the sticky header.
- Better styling options for multi-level dropdowns.
- Bug fixes and responsive improvements.

## 2.4 - October 15, 2024

- Fixed: the sidebar no longer flashes unstyled while the page loads.
- New: open the off-canvas or mobile menu above or below the header.

## 2.3 - October 6, 2024

- Better headroom when off-canvas or the top bar is on.
- Added the missing variables for icon styling.
- New variable to style custom SVG icons.
- New option: show the off-canvas or mobile menu over the top bar.
- General refinements.

## 2.2 - September 17, 2024

- Nested multi-level dropdowns.
- When headroom is on, scrolling to a `#` link leaves room for the sticky header.
- General refinements.

## 2.1 - July 6, 2024

- Better keyboard access in off-canvas mode.
- Headroom now works on desktop with a normal header.
- Better mobile layout in off-canvas mode.

## 2.0 - May 20, 2024

- New: off-canvas mode, with an option to push the page content.
- New: fixed menu button, which stays in place when the content is pushed.
- New: the current menu item opens automatically in off-canvas mode too.
- New: open the first dropdown on load.
- New: overlay sidebar, a see-through sidebar over full-width pages.
- New: top bar, for a classic menu bar at the top.
- New: overlay top bar, over the page in off-canvas mode.
- New: RTL support.
- New: headroom, which hides the header as you scroll down and shows it as you scroll up (mobile only).
- Bug fixes and responsive improvements.

From 2.0, off-canvas is built in, so there's no separate off-canvas template.

## 1.3 - March 2, 2024

- Off-canvas template only: the off-canvas now has a menu button and header setup.

## 1.2.2 - September 15, 2023

- Fixed: a JavaScript console error after updating by hand from 1.1 to 1.2.

## 1.2.1 - September 10, 2023

- The top-level dropdown item is now only a dropdown toggle by default.

## 1.2 - September 9, 2023

- New dropdown element.
- New: current menu item. The link to the current page gets its own style.
- New: automatic menu position. On page load, the sidebar slides to the current menu item and opens its dropdown. Not in the off-canvas template. Turn it on or off in the options.
- Better keyboard and screen reader access.
- The options CSS with the template ID now sits next to the styling options.

## 1.1 - September 1, 2023

- New off-canvas template (September 2, 2023). It works with Bricks' Off Canvas element, so you can use the sidebar as an off-canvas menu on desktop.
- Color schemes: black, demo and grayscale.
