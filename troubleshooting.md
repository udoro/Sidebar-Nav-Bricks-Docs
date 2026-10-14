---
icon: wrench
---

# Troubleshooting

| Problem | What to do |
| --- | --- |
| The builder canvas is blank | Add your template's ID to the **Sidebar Options CSS/JS** code block. See step 3 in [Installation & Getting Started](getting-started.md). |
| The sidebar doesn't show on the site | Check three things. Code execution is on in **Bricks > Settings > Custom code**. **Execute code** is on for both code blocks in the template. The template has a condition that covers this page. Then clear your site's cache. |
| A slide button doesn't open its panel | The button's `data-title` and the panel's `data-title` must match exactly, including capital letters and spaces. See [Naming panels](building-the-navigation.md#naming-panels). |
| A slide button opens the wrong panel | Two panels have the same `data-title`. Give each panel its own name. |
| The layout breaks between two screen widths | The breakpoint was changed in one place only. Change it in all three. See [Change the breakpoint](sidebar-options.md#change-the-breakpoint). |
| The top bar doesn't hide on scroll | Headroom needs `enableOffCanvas` or `enableTopBar` set to `1`, and doesn't work with `offCanvasPushContent`. See [Headroom and scrolling](sidebar-options.md#headroom-and-scrolling). |
| There's no collapse button | Set `enableCollapsibleSidebar` to `1`. The collapsible sidebar works on desktop only, and not when `enableOffCanvas` is `1`. |
| Icons are cut off when collapsed | The collapsed width doesn't fit your icons. See [Collapsed sidebar](styling.md#collapsed-sidebar). |
| The top bar flashes unstyled while the page loads | Set the `data-topbar-active` attribute to `true`. See [Attributes & Classes](attributes-and-classes.md#sidebar-attributes). |
| Outline icons don't change color | Set the `data-style-svg-stroke` attribute to `true`. |
| The sidebar stops working after a page transition | See [Page transitions](guides/javascript-api.md#page-transitions). |
| Dynamic menu items show placeholder text | Open a real page on your site. Dynamic data can't load in the template preview. |
| Something is wrong with Mega Menu Pro in the sidebar | See [Using with Mega Menu Pro](guides/mega-menu-pro.md). |

## Keyboard and screen readers

The sidebar works with the keyboard: Tab moves through the menu, Enter opens a panel or dropdown, and Escape closes it. If you change the colors, test the menu with the keyboard and a screen reader. Keep the focus outline easy to see. See [Focus outline](styling.md#focus-outline).
