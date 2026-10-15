---
icon: object-group
---

# Using with Mega Menu Pro

You can put Mega Menu Pro inside the sidebar's top bar. The sidebar stays your header, and Mega Menu Pro goes into it as a Section template. You keep one copy of Mega Menu Pro, and every sidebar header that uses it shows the same menu.

{% hint style="warning" %}
**Use the Lite version of Mega Menu Pro**, for example **Mega Menu Pro Header Template v1.4.7 Lite**. The Full version has its own sidebar feature, which gets in the way of this one.
{% endhint %}

***

## Pick a layout

| Layout | What visitors see | Sidebar options |
| --- | --- | --- |
| **A. Mega Menu Pro on desktop, sidebar on mobile** | On desktop, a top bar with Mega Menu Pro. On mobile, the sidebar opens from a menu button. | `enableOffCanvas: 1` |
| **B. Both on every screen** | A top bar with Mega Menu Pro, and the sidebar below it. | `enableTopBar: 1`, `enableOffCanvas: 0` |

Don't use off-canvas for layout B. Off-canvas hides the sidebar until someone opens it.

With layout B, test the collapsible sidebar before you use it. It may not work well with the top bar.

You can use both layouts on one site. Make two Sidebar Navigation Builder headers with different template conditions, and put the same Mega Menu Pro template in both.

Do the steps below in order.

***

## 1. Make Mega Menu Pro a Section template

Mega Menu Pro is a Header template. To place it inside the sidebar, it must be a Section template.

1. In WordPress, go to **Bricks > Templates**.
2. Hover over the Mega Menu Pro template and click **Edit**, not **Edit with Bricks**.
3. Find the **Template Type** setting and change it from **Header** to **Section**.
4. Click **Update**.

Mega Menu Pro now only shows where you place it.

Using the AI Connector? Your agent can do this step for you (MMPro AI Abilities 0.5.0 or later).

## 2. Put Mega Menu Pro in the sidebar

1. Open your Sidebar Navigation Builder header with **Edit with Bricks**. If it was already open, reload the builder.
2. Add a **Template** element inside the **Header inner wrap**, just before the **Hamburger Wrapper**. It must be inside the Header inner wrap.
3. In the Template element, pick the Mega Menu Pro template.
4. Save.

For a second sidebar header, add a Template element the same way. Don't import Mega Menu Pro again. With one shared template, you edit Mega Menu Pro in one place and every header updates.

## 3. Set the sidebar options

In the **JS** tab of the **Sidebar Options CSS/JS** code block:

* **Layout A:** set `enableOffCanvas` to `1`.
* **Layout B:** set `enableTopBar` to `1`, and leave `enableOffCanvas` at `0`.

Both layouts use the top bar, so also set the `data-topbar-active` attribute to `true`. It stops the top bar flashing unstyled while the page loads. See [Attributes & Classes](../attributes-and-classes.md#sidebar-attributes).

## 4. Use one breakpoint for both

Both products switch to a mobile menu at their own breakpoint. Mega Menu Pro's mobile menu starts below 1201px, and the sidebar's below 1025px. Give them the same breakpoint. Otherwise they switch at different widths and the header looks wrong in between.

The easiest way is to keep the sidebar's breakpoint and change Mega Menu Pro's: set its desktop width to `1025px` and its mobile width to `1024px`. Follow [Mega Menu Pro's breakpoint steps](https://design-with-cracka.gitbook.io/bricksmegamenupro/menu-options#breakpoint).

To use another width, change it in both products. For the sidebar, see [Change the breakpoint](../sidebar-options.md#change-the-breakpoint).

## 5. Add the header CSS

1. In the sidebar header, select the **Header inner wrap**.
2. In **Style > Custom CSS**, add the CSS for your layout.

   **Layout A:**

   ```css
   @media (min-width: 1025px) {
     %root% {
       --sidebar-header-block-padding: 0px;
     }
     %root% .dwc-hamburger-wrap {
       display: none;
     }
     %root% > .brxe-logo {
       display: none;
     }
   }

   @media (max-width: 1024px) {
     %root% > .brxe-template {
       display: none;
     }
   }

   %root% > .brxe-template {
     flex: 1 1 0;
     min-width: 0;
   }
   ```

   On desktop you'll see Mega Menu Pro with its own logo. On mobile you'll see the sidebar's logo and menu button.

   **Layout B:**

   ```css
   %root% > .brxe-logo {
     display: none;
   }

   %root% > .brxe-template {
     flex: 1 1 0;
     min-width: 0;
   }
   ```

   Then, in the **CSS** tab of **Sidebar Options CSS/JS**, set `--sidebar-header-block-padding` to `0px`.

3. Save.

If you changed the breakpoint, use your own widths in layout A: the desktop width in the first rule, the mobile width in the second.

Keep the Template element's **Render without wrapper** setting off. This CSS needs it off.

The CSS is on this sidebar header, not in the shared Mega Menu Pro template. So a layout B header that uses the same Mega Menu Pro template still shows its menu on mobile. Don't put it on the Template element either: with **Render without wrapper** on, the Template element's own styles don't reach the page.

## 6. Tidy the spacing

* **The header looks too tall?** Check your logo image. Empty space inside the image file makes the header taller.
* **Position the logo, menu and button** with the Header inner wrap's flex settings, such as **Justify content** and **Align items**. Don't use margins inside the Mega Menu Pro template: it's shared, so a margin there moves the menu in every header.

***

## Change one header or all of them

The Mega Menu Pro template is shared:

* **To change every header,** edit the Mega Menu Pro template.
* **To change one header only,** make the change in that sidebar header, for example on its Header inner wrap, not inside Mega Menu Pro.

## Check it

Open a page on desktop and on a phone, or a narrow browser window, and check:

* The logo shows at every width.
* Layout A: only one menu button shows at each width.
* Mega Menu Pro's dropdowns open right below the header bar.
* Nothing jumps or overlaps as you resize the window past the breakpoint.

## Troubleshooting

| Problem | What to do |
| --- | --- |
| An extra bar shows at the top of Mega Menu Pro's mobile menu | In the Mega Menu Pro template, select the **mobile top bar** element. In **Style > Custom CSS**, add `%root%::before { display: none; }`. |
| The logo and buttons are pushed out of place | Check the CSS from step 5 is on the **Header inner wrap**, and **Render without wrapper** is off. |
| Both menus show at some widths, or neither | The breakpoints don't match. See step 4. |
| Mega Menu Pro doesn't show in the Template element's list | It's still a Header template. See step 1, then reload the builder. |
| Mega Menu Pro's logo is empty | In the Mega Menu Pro template, pick your logo again in the **SVG** element inside **Logowrap (link)**. |
| Dropdowns open inside the header bar | Set `--sidebar-header-block-padding` to `0px` (step 5). |
