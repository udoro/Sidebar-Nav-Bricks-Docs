---
icon: tags
---

# Attributes & Classes

## Sidebar attributes

These attributes are on the **Sidebar Nav 3.0.2** block, the top element of the template. To change one, see [Change an attribute](README.md#change-an-attribute).

Set the value to `true` to turn an attribute on. Clear the value to turn it off.

| Attribute | Template value | What `true` does |
| --- | --- | --- |
| `data-topbar-active` | empty | Stops the top bar from flashing unstyled while the page loads. Set it to `true` when `enableTopBar` or `enableOffCanvas` is on. |
| `data-push-footer` | `true` | The **Panel footer** (social icons and button) sits below the menu, and the sidebar scrolls when the menu is long. Clear it to keep the Panel footer at the bottom of the sidebar. |
| `data-overlap-collapsible` | empty | The collapsible sidebar covers the page content instead of pushing it aside. |
| `data-style-svg-stroke` | empty | Colors the lines (stroke) of SVG icons with the icon color, not only the fill. Turn it on if your outline icons don't change color. |
| `data-partition-dropdown` | empty | Splits each dropdown item in two: the text on the left, and the chevron as its own button with a divider. The colors come from the [partitioned dropdown variables](styling.md#dropdown-links). |

## Collapse toggle attribute

This attribute is on the **Collapse toggle** element.

| Attribute | Template value | What `true` does |
| --- | --- | --- |
| `data-static` | empty | The button stays where it sits in the **Header inner wrap**, instead of floating at the edge of the sidebar. |

***

## Helper classes

Add these classes to any element inside the sidebar.

| Class | What it does |
| --- | --- |
| `dwc-hide` | Hides the element while the sidebar is collapsed. The template's **CTA button** uses it. |

***

## Classes on the page

The sidebar adds classes to `<body>`, so your own CSS can change things in each state.

| Class on `<body>` | When it's there |
| --- | --- |
| `dwc-mobile` | Below the breakpoint. |
| `dwc-slide-nav-open` | The mobile or off-canvas menu is open. |
| `dwc-collapse-enabled` | The collapsible sidebar is on. |
| `dwc-collapse-sidebar` | The sidebar is collapsed. |
| `dwc-offcanvas` | Off-canvas mode is active. |
| `dwc-push-content` | Off-canvas push content is active. |
| `dwc-topbar-enabled` | The top bar is on. |
| `dwc-headroom` | Headroom is on. `scroll-down` and `scroll-up` show which way the visitor last scrolled. |
| `sidebar-ready` | The sidebar's code has run. |

The link to the current page gets the `dwc-current-menu-item` class.

### Example: a different logo when collapsed

A wide logo doesn't fit the collapsed sidebar. You can show a small logo in its place.

1. Put both logos in one block with the class `logo-wrap`. Give the wide logo the class `default-logo`, and the small one `alt-logo`.
2. Add this CSS to your site, for example in **Bricks > Settings > Custom code > Custom CSS**:

```css
.logo-wrap {
  position: relative;
}

.logo-wrap img {
  position: absolute;
}

.default-logo {
  opacity: 1;
}

.alt-logo {
  opacity: 0;
}

.dwc-collapse-sidebar .default-logo {
  opacity: 0;
}

.dwc-collapse-sidebar .alt-logo {
  opacity: 1;
}
```

Both logos sit in the same spot, and only one shows at a time. Give `.logo-wrap` a height that fits your logo, because both images are taken out of the layout.
