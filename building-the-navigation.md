---
icon: list-tree
---

# Building the Navigation

You build the menu inside the **Nav** element. Every panel sits directly inside **Nav**, and every menu item is an `li` inside a panel's **List &lt;ul&gt;**.

***

## Menu items

The template has three kinds of menu item. To add one, duplicate an item of the same kind and change it.

| Item | What it does |
| --- | --- |
| **li - link** | A plain link to a page. |
| **li - slide button** | Opens a slide panel. The Home panel slides away and the new panel slides in. |
| **li - dropdown** | Opens a list of links below it, in place. |

### Change a link

1. Select the **link** element inside the **li - link**.
2. In the **Content** tab, set its link.
3. Select the text element inside it and change the text.
4. To change the icon, select **link icon** and pick another icon.

The sidebar marks the link to the page you're on, so visitors can see where they are. It matches the link's address with the page's address.

***

## Slide panels

A slide button opens the panel that has the same `data-title` attribute.

### Add a slide panel

1. Duplicate the **Slide panel** element. Keep the copy directly inside **Nav**.
2. Select the copy, open **Style > Attributes** and set `data-title` to a new name, for example `Services`.
3. In the copy, change the **Panel title** heading, then build its list.
4. Duplicate an **li - slide button** where the new button should go, and change its text.
5. Select the **slide button** element inside it, open **Style > Attributes** and set `data-title` to the same name: `Services`.

Now the button opens the new panel. In the builder, each panel shows a blue tab with its name, and each slide button shows the name of the panel it opens. Use them to check the names match. Visitors don't see these labels.

### Naming panels

* **Each panel needs its own `data-title`.** If two panels share a name, the button always opens the first one.
* **The button and the panel must match exactly**, including capital letters and spaces.
* **Use a name people can read**, such as `Services`, not `slide2`. Visitors see it: the Back to button reads "back to Services" when it goes back to that panel. Screen readers also hear it, as "Services menu".
* The **Home panel** is called `Home`. You can rename it, for example to `Main menu`. Back buttons then read "back to Main menu".

### Go deeper

To add another level, put an **li - slide button** inside a slide panel's list, and point it at another slide panel. Keep that panel directly inside **Nav** too, next to the others. A panel's level comes from the button that opens it, not from where the panel sits in the Structure panel.

### Back and Home buttons

Each slide panel has a **Panel header** with two buttons:

* **Back to button** goes back one panel. With the **updateBackText** option on, it reads "back to" and the name of that panel. See [Sidebar Options](sidebar-options.md#navigation).
* **Home button** goes straight back to the Home panel.

***

## Dropdowns

### Nest a dropdown

1. Duplicate an **li - dropdown**.
2. Drag the copy into another dropdown's list: **li - dropdown > dropdown content > List &lt;ul&gt;**.

Each level can have its own indent, background and icon size. See [Styling](styling.md#dropdown-levels).

To make the dropdown text a link and the chevron a separate button, see the `data-partition-dropdown` attribute in [Attributes & Classes](attributes-and-classes.md#sidebar-attributes).

***

## Anything else in a panel

Panels are normal Bricks blocks, so you can put any element in them: an image, a gallery, tabs, a query loop or a Template element. The template's slide panel has an image inside its link, for example.

To build the menu from your pages with query loops instead of by hand, see [Dynamic Navigation with Query Loops](guides/dynamic-navigation.md).

## Panel footer

The Home panel's **Panel footer** holds the **Social icons** and the **CTA button**. Change them like any other Bricks element. The CTA button has the `dwc-hide` class, so it hides when the sidebar is collapsed. See [Attributes & Classes](attributes-and-classes.md#helper-classes).
