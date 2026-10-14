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

## 2. Put Mega Menu Pro in the sidebar

1. Open your Sidebar Navigation Builder header with **Edit with Bricks**. If it was already open, reload the builder.
2. Add a **Template** element inside the **Header inner wrap**, just before the **Hamburger Wrapper**. It must be inside the Header inner wrap.
3. In the Template element, pick the Mega Menu Pro template.
4. Set the Template element's width to `auto`. Otherwise it takes up the full width and pushes the logo and buttons out of place.
5. Save.

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

## 5. Show each menu at the right width

**Layout A only.** Hide the sidebar's menu button on desktop, and Mega Menu Pro's menu on mobile.

1. In the sidebar header, select the **Header inner wrap**.
2. In **Style > Custom CSS**, add:

   ```css
   @media (min-width: 1025px) {
     %root% .dwc-hamburger-wrap {
       display: none;
     }
   }

   @media (max-width: 1024px) {
     %root% .dwc-menu-wrap {
       display: none;
     }
   }
   ```

3. Save.

If you changed the breakpoint, use your own widths: the desktop width in the first rule, the mobile width in the second.

* `.dwc-hamburger-wrap` is the sidebar's **Hamburger Wrapper**.
* `.dwc-menu-wrap` is Mega Menu Pro's **Menu wrap**. The logo is in **Logowrap (link)**, next to it, so the logo stays visible.

The CSS is on this sidebar header, not in the shared Mega Menu Pro template. So a layout B header that uses the same Mega Menu Pro template still shows its menu on mobile. Don't put it on the Template element either: with **Render without wrapper** on, the Template element's own styles don't reach the page.

## 6. Tidy the spacing

* **The header looks too tall.** In the **CSS** tab of **Sidebar Options CSS/JS**, set `--sidebar-header-block-padding` to `0px`. It's the top and bottom padding of the Header inner wrap.
* **Still too tall?** Check your logo image. Empty space inside the image file makes the header taller.
* **Two logos.** Keep one: the sidebar's **Logo** or Mega Menu Pro's **Logowrap (link)**. Remove or hide the other. Using the same one in every header makes later changes easier.
* **Position the logo, menu and button** with the Header inner wrap's flex settings, such as **Justify content** and **Align items**. Don't use margins inside the Mega Menu Pro template: it's shared, so a margin there moves the menu in every header.

## 7. Optional: render without wrapper

On the Template element, you can turn on **Render without wrapper** for cleaner HTML. The Template element's own settings, such as its width, then stop working. Check the header on desktop and mobile after you change it.

***

## Change one header or all of them

The Mega Menu Pro template is shared:

* **To change every header,** edit the Mega Menu Pro template.
* **To change one header only,** make the change in that sidebar header, for example on its Header inner wrap, not inside Mega Menu Pro.

## Check it

Open a page on desktop and on a phone, or a narrow browser window, and check:

* The logo shows at every width.
* Only one menu button shows at each width.
* Nothing jumps or overlaps as you resize the window past the breakpoint.

## Troubleshooting

| Problem | What to do |
| --- | --- |
| An extra bar shows at the top of Mega Menu Pro's mobile menu | In the Mega Menu Pro template, select the **mobile top bar** element. In **Style > Custom CSS**, add `%root%::before { display: none; }`. |
| The logo and buttons are pushed out of place | Set the Template element's width to `auto` (step 2). |
| Both menus show at some widths, or neither | The breakpoints don't match. See step 4. |
| Mega Menu Pro doesn't show in the Template element's list | It's still a Header template. See step 1, then reload the builder. |
