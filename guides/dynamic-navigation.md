---
icon: database
---

# Dynamic Navigation with Query Loops

You can build the sidebar menu from your pages, so it updates when you add a page. This guide uses Bricks query loops and page categories, not a WordPress menu.

You'll build three kinds of menu item:

* Links to pages that have no child pages.
* Slide buttons for pages that have child pages. Each one opens a panel with its child pages.
* Dropdowns for pages that have child pages. Each one opens a list of its child pages.

{% hint style="info" %}
This guide shows slide buttons and dropdowns. In your menu, use one of them for parent pages, not both. If you use both, every parent page shows twice.
{% endhint %}

Do the steps in order.

***

## 1. Turn on categories for pages

WordPress doesn't let you give pages a category. A free plugin adds it.

1. In WordPress, go to **Plugins > Add New Plugin**.
2. Search for **Pages with category and tag**.
3. Install and activate it.

## 2. Create two categories

Go to **Posts > Categories** and create:

* **menu item**: for every page that should show in the sidebar.
* **has child**: for every page that has child pages.

You can use tags instead of categories. Use the same names.

## 3. Set up your pages

1. Create your top-level pages and their child pages. Set each child page's **Parent** in the page settings.
2. Give every page that should show in the sidebar the **menu item** category.
3. Also give every page that has child pages the **has child** category.

## 4. Open the sidebar template

Open your Sidebar Navigation Builder header template with **Edit with Bricks**. You'll add a query loop to each kind of menu item.

{% hint style="warning" %}
Check your work on a real page of your site, not in the template preview. Dynamic data doesn't always load in the template preview.
{% endhint %}

***

## 5. Links to top-level pages

1. Select the **li - link** element in the Home panel.
2. Turn on **Use query loop** and set:
   * **Post type**: Page
   * **Child of**: `0` (top-level pages only)
   * **Terms to include**: menu item
   * **Terms to exclude**: has child
3. Select the link's text and set it to the dynamic data `{post_title}`.
4. Select the **link** element and set its link to the dynamic data `{post_url}`.

## 6. Slide buttons for parent pages

1. Select the **li - slide button** element in the Home panel.
2. Turn on **Use query loop** and set:
   * **Post type**: Page
   * **Child of**: `0`
   * **Terms to include**: has child
3. Set the button's text to `{post_title}`.

### Save it as a global query

You'll use the same query again, so save it.

1. In the query loop settings, click the **Save** icon.
2. Name it, for example `Sidebar 1st level parent`.
3. Optional: put it in a global query category called `Dynamic Sidebar Nav`, to keep your sidebar queries together.

## 7. Dropdowns for parent pages

1. Select the **li - dropdown** element.
2. Turn on **Use query loop** and pick the global query `Sidebar 1st level parent`.
3. Set the dropdown's text to `{post_title}`.

## 8. Slide panels

1. Select the **Slide panel** element.
2. Turn on **Use query loop** and set:
   * **Post type**: Page
   * **Terms to include**: has child

The loop makes one panel for each parent page.

## 9. Child page links

Do this for the **li - link** inside the slide panel, and for the **li - link** inside the dropdown.

1. Select the **li - link**.
2. Turn on **Use query loop** and set:
   * **Post type**: Page
   * **Child of**: `{post_id}` (the child pages of the parent page around it)
   * **Terms to include**: menu item. Leave it empty to show every child page.
   * **Terms to exclude**: has child
3. Set the link text to `{post_title}` and the link to `{post_url}`.

You can save this as a global query too, for example `Sidebar sublevel child item (childless)`. Use it on any link for a child page with no children of its own.

## 10. Link each slide button to its panel

A slide button opens the panel with the same `data-title`. Use the page title for both.

1. Select the **slide button** element inside the **li - slide button**. In **Style > Attributes**, set `data-title` to `{post_title}`.
2. Select the **Slide panel**. In **Style > Attributes**, set `data-title` to `{post_title}`.

Each parent page needs its own title. Two parent pages with the same title open the same panel.

## 11. Finish

1. Change any other text and images in the menu to dynamic data, for example the **Panel title** to `{post_title}`.
2. Save, and check the menu on a real page of your site.
