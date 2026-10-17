---
icon: desktop-arrow-down
---

# Installation & Getting Started

## Before you start

You need:

* **Bricks Builder** on a WordPress site.
* **An administrator account.** The sidebar runs from code blocks, and only roles with code execution can turn them on.

***

## Installation

Do all four steps, in order.

### 1. Import the header template

1. Download the JSON file from your Gumroad library.
2. In WordPress, go to **Bricks > Templates** and click **Import**.
3. Select the JSON file. Tick **Import images**, then click **Import**.

### 2. Turn on code execution

The sidebar runs from two code blocks inside the template: **Sidebar Options CSS/JS** and **Sidebar CSS and JS**. Bricks only runs them when code execution is on.

1. Go to **Bricks > Settings > Custom code**.
2. Turn on **Code execution** for administrators.
3. Open the new template with **Edit with Bricks**.
4. Select **Sidebar Options CSS/JS** in the Structure panel and turn on **Execute code**. Do the same for **Sidebar CSS and JS**. Importing a template turns this off, so check both.
5. If Bricks asks you to sign the code, sign it. You can sign every code block at once with **Regenerate code signatures** on the **Bricks > Settings > Custom code** page.

### 3. Add the template's ID

At first, the builder canvas is blank. That's normal. The sidebar shows once the code knows your template's ID.

1. Find the ID. Go to **Bricks > Templates** and look at the **Shortcode** column. For example, `[bricks_template id="29142"]` means the ID is `29142`.
2. In the builder, select the **Sidebar Options CSS/JS** code block and open its **CSS** tab.
3. Scroll to the bottom and find the comment `/* INSIDE BRICKS */`.
4. Below it, `postid-29799` appears twice. In both places, replace `29799` with your template's ID. Keep `postid-` in front, for example `postid-29142`.
5. Save. The sidebar now shows in the builder.

### 4. Show the sidebar on your pages

1. In the builder, open **Settings > Template Settings > Conditions**.
2. Add a condition. Pick **Entire website** to show the sidebar everywhere, or pick the pages and posts it should show on.
3. Save.

Open one of those pages to check the sidebar shows.

***

## Put the sidebar on the right

The template sits on the left of the page. To move it to the right:

1. In the builder, open **Settings > Template Settings**.
2. In the header settings, set the **Position** setting to **Right**.
3. Leave the header width at `var(--sidebar-width)`. To change the width, change the `--sidebar-width` variable instead. See [Styling](styling.md#sidebar).
4. Save.

***

## What's inside the template

```
Sidebar Nav 3.0.3               (block: the sidebar attributes)
├── Sidebar Options CSS/JS      (code block: your JS options and CSS variables)
├── Header inner wrap           (top of the sidebar, or the top bar)
│   ├── Logo
│   ├── Hamburger Wrapper
│   │   └── Hamburger Trigger   (opens the mobile and off-canvas menu)
│   └── Collapse toggle         (collapses the sidebar)
├── Nav                         (holds every panel)
│   ├── Home panel              (the first panel, always there)
│   │   ├── Inner wrap
│   │   │   └── List <ul>
│   │   │       ├── li - link            (a plain link)
│   │   │       ├── li - slide button    (opens a slide panel)
│   │   │       └── li - dropdown        (opens a list in place)
│   │   └── Panel footer        (social icons and a button)
│   └── Slide panel             (opened by a slide button)
│       ├── Panel header        (Home button and Back to button)
│       └── Inner wrap
│           ├── Panel title
│           └── List <ul>
├── Mobile menu overlay         (the dark layer behind the open menu)
└── Sidebar CSS and JS          (code block: don't edit)
```

* You build your menu inside **Nav**. See [Building the Navigation](building-the-navigation.md).
* You only edit the **Sidebar Options CSS/JS** code block. See [Sidebar Options](sidebar-options.md) and [Styling](styling.md).
* The **Sidebar Nav 3.0.3** block holds a few attributes. See [Attributes & Classes](attributes-and-classes.md).
