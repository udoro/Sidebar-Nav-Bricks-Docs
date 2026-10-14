---
icon: palette
---

# Styling

You style the sidebar with CSS variables. They're in the **CSS** tab of the **Sidebar Options CSS/JS** code block, inside `:root`.

1. In the builder, select the **Sidebar Options CSS/JS** code block.
2. Open its **CSS** tab.
3. Find the variable and change its value. Keep the `;` at the end of the line.
4. Save, then check the page.

The **Template value** column is the value when you import the template. A value like `var(--sidebar-link-color)` means it copies another variable, so it changes when that one does.

{% hint style="info" %}
Change a variable before you write your own CSS for the same thing. Your change then works in every state: collapsed, off-canvas and mobile.
{% endhint %}

***

## Sidebar

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-width` | `min(90vw, 300px)` | Sidebar width. Also the width of the mobile and off-canvas menu. |
| `--sidebar-header-bg` | `silver` | Background of the **Header inner wrap** (the top of the sidebar, or the top bar). |
| `--sidebar-nav-bg` | `white` | Background behind the menu. |
| `--sidebar-header-block-padding` | `1rem` | Top and bottom padding of the Header inner wrap. |
| `--sidebar-header-inline-padding` | `1.25rem` | Left and right padding of the Header inner wrap. |
| `--sidebar-shadow` | `0px 0px 3px rgba(0, 0, 0, 0.75), 0px 5px 15px rgba(0, 0, 0, 0.3)` | Sidebar shadow. |

## Menu button

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-hamburger-color` | `gray` | Color of the menu (hamburger) button. |
| `--sidebar-hamburger-bg` | `transparent` | Background of the menu button. |

## Links

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-link-color` | `dimgray` | Link text color. |
| `--sidebar-link-bg` | `transparent` | Link background. |
| `--sidebar-link-icon-color` | `dimgray` | Link icon color. |
| `--sidebar-link-txt-size` | `0.875rem` | Link text size. |
| `--sidebar-link-icon-size` | `24px` | Link icon size. |
| `--sidebar-link-inline-padding` | `1rem` | Left and right padding of each link. |
| `--sidebar-link-block-padding` | `0.7rem` | Top and bottom padding of each link. |
| `--sidebar-link-border-radius` | `5px` | Corner rounding of links and the CTA button. |
| `--sidebar-link-underline` | `var(--sidebar-footer-top-border)` | Line under each link. |
| `--sidebar-link-transition` | `500ms` | How long hover color changes take. |
| `--sidebar-link-gap` | `1.125rem` | Space between the icon and the text. |
| `--sidebar-link-hover-color` | `black` | Link text color on hover. |
| `--sidebar-link-hover-bg` | `rgb(0 0 0 / 5%)` | Link background on hover. |
| `--sidebar-link-icon-hover-color` | `black` | Link icon color on hover. |

## Dropdown links

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-dropdown-link-color` | `dimgray` | Text color of links inside a dropdown. |
| `--sidebar-dropdown-link-bg` | `transparent` | Background of links inside a dropdown. |
| `--sidebar-dropdown-link-underline` | `none` | Line under links inside a dropdown. |
| `--sidebar-dropdown-content-bg` | `rgb(0 0 0 / 5%)` | Background of an open dropdown. |
| `--sidebar-dropdown-link-hover-color` | `black` | Dropdown link text color on hover. |
| `--sidebar-dropdown-link-hover-bg` | `rgb(0 0 0 / 8%)` | Dropdown link background on hover. |
| `--sidebar-dropdown-link-indent` | `10px` | How far dropdown links are pushed in. |

These five only work when the `data-partition-dropdown` attribute is `true`. See [Attributes & Classes](attributes-and-classes.md#sidebar-attributes).

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-dropdown-button-bg` | `white` | Background of the chevron button. |
| `--sidebar-dropdown-button-hover-bg` | `black` | Chevron button background on hover. |
| `--sidebar-dropdown-button-active-bg` | `black` | Chevron button background while the dropdown is open. |
| `--sidebar-dropdown-chevron-hover-color` | `white` | Chevron color on hover. |
| `--sidebar-dropdown-chevron-active-color` | `white` | Chevron color while the dropdown is open. |

## Lists and chevrons

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-list-items-block-padding` | `1.25rem` | Space above and below each list. |
| `--sidebar-list-gap` | `0` | Space between list items. |
| `--sidebar-chevron-size` | `1rem` | Chevron icon size. |
| `--sidebar-chevron-color` | `var(--sidebar-link-icon-color)` | Chevron icon color. |

## CTA button

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-cta-color` | `white` | CTA button text color. |
| `--sidebar-cta-bg` | `dimgray` | CTA button background. |
| `--sidebar-cta-hover-bg` | `black` | CTA button background on hover. |

## Social links

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-social-link-color` | `dimgray` | Social link text color. |
| `--sidebar-social-link-bg` | `initial` | Social link background. |
| `--sidebar-social-icon-color` | `dimgray` | Social icon color. |
| `--sidebar-social-icon-size` | `1.5rem` | Social icon size. |
| `--sidebar-social-link-hover-color` | `black` | Social link text color on hover. |
| `--sidebar-social-link-hover-bg` | `rgb(0 0 0 / 5%)` | Social link background on hover. |
| `--sidebar-social-icon-hover-color` | `var(--sidebar-social-link-hover-color)` | Social icon color on hover. |

## Panels

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-panel-title-size` | `1.125rem` | Panel title size. |
| `--sidebar-panel-title-color` | `black` | Panel title color. |
| `--sidebar-panel-title-bg` | `initial` | Panel title background. |
| `--sidebar-panel-label-color` | `orangered` | Color of the labels you see in the builder only, such as the panel each slide button opens. |
| `--sidebar-panel-backtext-font-size` | `0.6rem` | Size of the "back to" text. |
| `--sidebar-panel-backtext-color` | `var(--sidebar-link-color)` | Color of the "back to" text. |
| `--sidebar-panel-block-padding` | `clamp(0.5rem, -1.375rem + 5vh, 2rem)` | Top and bottom padding of each panel. |
| `--sidebar-panel-inline-padding` | `0.5rem` | Left and right padding of each panel. |
| `--sidebar-panel-shadow` | `-5px -5px 20px rgb(0 0 0/3%)` | Shadow of each panel. |

## Panel footer

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-footer-top-border` | `1px solid rgb(0 0 0 / 10%)` | Line above the Panel footer. Links copy it for their underline. |
| `--sidebar-footer-block-padding` | `1.25rem` | Top and bottom padding of the Panel footer. |
| `--sidebar-footer-inline-padding` | `var(--sidebar-panel-inline-padding)` | Left and right padding of the Panel footer. |

## Current page link

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-current-link-bg` | `rgba(0, 0, 0, 0.05)` | Background of the link to the page you're on. |
| `--sidebar-current-link-underline` | `solid 3px gray` | Line under the link to the page you're on. |

## Collapsed sidebar

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-collapse-icon-bg` | `initial` | Background of the **Collapse toggle** button. |
| `--sidebar-collapse-icon-size` | `35px` | Size of the Collapse toggle button. |
| `--sidebar-collapse-icon-color` | `#B1B1B1` | Color of the Collapse toggle icon. |
| `--sidebar-collapse-width` | `80px` | Collapsed width, when the **collapseAutoWidth** option is `0`. |
| `--sidebar-collapse-ttf` | `cubic-bezier(0.4, 0, 0.2, 1)` | Easing of the collapse animation. |

With **collapseAutoWidth** on (the template value), the collapsed width is worked out from `--sidebar-panel-inline-padding`, `--sidebar-link-inline-padding` and `--sidebar-link-icon-size`. If your icons show bigger or smaller than `--sidebar-link-icon-size`, the collapsed sidebar can cut them off or leave extra space. Fix it with `--icon-size-multiplier`, just below `:root` in the `.dwc-auto-width` rule: set it to your icon's real width divided by `--sidebar-link-icon-size`. Check the real width with your browser's inspector.

### Tooltips

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-tooltip-font-size` | `10px` | Tooltip text size. |
| `--sidebar-tooltip-font-color` | `white` | Tooltip text color. |
| `--sidebar-tooltip-bg` | `black` | Tooltip background. |
| `--sidebar-tooltip-radius` | `0.5em` | Tooltip corner rounding. |
| `--sidebar-tooltip-inline-padding` | `1em` | Left and right padding of tooltips. |
| `--sidebar-tooltip-block-padding` | `0.5em` | Top and bottom padding of tooltips. |

## Overlay and backdrop

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-backdrop-overlay-bg` | `black` | Color of the layer behind the open mobile or off-canvas menu. |
| `--sidebar-backdrop-overlay-opacity` | `0.5` | How see-through that layer is. `0` is invisible, `1` is solid. |
| `--overlay-sidebar-blur` | `blur(0px)` | Blurs the page behind the sidebar when the **overlaySidebar** option is on. For example `blur(8px)`. |

## Motion

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-transition` | `400ms` | How long the slide and collapse animations take. |
| `--sidebar-ttf` | `var(--material-design-ttf)` | Easing of the slide animations. You can also use `var(--default-ttf)`. |
| `--material-design-ttf` | `cubic-bezier(0.2, 0.0, 0, 1.0)` | One easing you can pick for `--sidebar-ttf`. |
| `--default-ttf` | `cubic-bezier(1, 0, 0.2, 1)` | Another easing you can pick for `--sidebar-ttf`. |
| `--sidebar-opacity-transition` | `500ms 200ms` | How long text takes to fade, and the wait before it starts. |

## Spacing

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-padding-m` | `1.25rem` | Padding around the menu (hamburger) button. |
| `--sidebar-padding-s` | `0.75rem` | Padding of the Home button, and above and below the panel title. |
| `--sidebar-padding-xs` | `0.5rem` | Padding left and right of the panel title. |
| `--sidebar-content-gap` | `0` | Space between the items in the Header inner wrap and in each Panel header. |

## Focus outline

The outline shows when a visitor moves through the menu with the keyboard.

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--sidebar-focus-outline-color` | `black` | Outline color. |
| `--sidebar-focus-outline-width` | `2px` | Outline thickness. |
| `--sidebar-focus-outline-offset` | `4px` | Space between the outline and the item. |

## Dropdown levels

A dropdown inside a dropdown is level 2, and one inside that is level 3. By default, every level copies the dropdown variables above. Change a level's variable to style that level on its own.

| Variable | Template value | What it sets |
| --- | --- | --- |
| `--lvl-2-indent`, `--lvl-3-indent` | `var(--sidebar-dropdown-link-indent)` | Indent of each level. |
| `--lvl-1-toggle-bg-active`, `--lvl-2-toggle-bg-active`, `--lvl-3-toggle-bg-active` | `var(--sidebar-link-hover-bg)` | Background of an open dropdown's toggle. |
| `--lvl-1-content-bg`, `--lvl-2-content-bg`, `--lvl-3-content-bg` | `var(--sidebar-dropdown-content-bg)` | Background of an open dropdown. |
| `--lvl-2-toggle-color-active`, `--lvl-3-toggle-color-active` | `var(--sidebar-link-color)` | Text color of an open dropdown's toggle. |
| `--lvl-1-icon-color`, `--lvl-2-icon-color`, `--lvl-3-icon-color` | `var(--sidebar-chevron-color)` | Chevron color. |
| `--lvl-2-icon-hover-color`, `--lvl-3-icon-hover-color` | `var(--sidebar-link-icon-hover-color)` | Chevron color on hover. |
| `--lvl-1-icon-size` | `var(--sidebar-link-icon-size)` | Icon size at level 1. |
| `--lvl-2-icon-size`, `--lvl-3-icon-size` | `calc(var(--sidebar-link-icon-size) * 0.75)` | Icon size at levels 2 and 3. |

***

## Before you finish

* **Check every state you use:** collapsed, off-canvas, and the mobile menu below the breakpoint.
* **Keep text readable.** Text and its background need enough contrast, in the normal and hover colors.
* **Keep the focus outline.** Keyboard users need it to see where they are.
* **Leave room to tap.** On mobile, links need enough padding to tap with a finger.
