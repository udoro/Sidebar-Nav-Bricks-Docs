---
icon: sparkles
---

# AI Skills Reference

Entry point for configuring Sidebar Navigation Builder for **Bricks** through the Bricks MCP
abilities, alone or with Mega Menu Pro Lite inside it.

**This file is short on purpose. Read all of it, then read only what it sends you to.**

| File | What it is | When to read it |
| --- | --- | --- |
| `sidebar-nav-bricks-skills-build.md` | Workflow, ability calls, Mega Menu Pro combination, rules and gotchas, verification | In full, on the build path only |
| `sidebar-nav-bricks-skills-reference.md` | Element map, JS options, attributes, CSS variables, classes | Never in full. Grep one section |
| `sidebar-test.mjs` | Headless Chrome helper: open the page, act, measure, screenshot | Import it when the build file's Verification needs a browser. Don't read it unless it fails |

***

## Is the site connected

Only a few high-level Bricks abilities are direct tools. Every ability this skill uses goes through
the dispatcher tool `mcp-adapter-execute-ability`, with `ability_name` (for example
`"bricks/get-page-elements"`) and `parameters`. `mcp-adapter-get-ability-info` returns an ability's
input schema. If your client defers MCP tools, load the dispatcher by name first. A missing direct tool
does not mean a missing ability.

* **No `mcp-adapter-execute-ability` tool:** stop. Tell the user: "I can't reach your Bricks site.
  Follow the AI Connector setup, then start a new session." Do not try REST calls, PHP or a browser
  instead.
* **An ability is disabled:** call `bricks/list-ability-status`, name the disabled ability to the
  user, and stop that operation. Do not route around it.

If your client also has the general Bricks skills (`bricks:*`), load the matching one for generic
Bricks work such as query loops, conditions or template settings. This file covers what is specific
to Sidebar Navigation Builder.

***

## Which path are you on

**Correction path:** you are changing something that already exists: a JS option, a CSS variable, an
attribute, a menu item's text, link or icon.

**Build path:** you are creating structure: new menu items, panels or dropdowns, query loops, Mega
Menu Pro in the sidebar, or a rebuild.

If you cannot tell, you are on the build path. If a correction turns out to need new structure, stop
and switch at that point.

***

## Correction path

Read these three things and nothing else:

1. **The invariants below.**
2. **Section 7 (Rules & gotchas) in `sidebar-nav-bricks-skills-build.md`**, grepped for the feature
   you are touching, and the Operations entry for the write you will make (section 5).
3. **One row** of the reference file, for the option, attribute or variable you are changing.

Then find the header (below), change the one value, verify, stop.

**Do not** read the build file end to end, read the engine code block, re-read the whole tree after
every write, or inventory anything you are not touching.

### Invariants that apply on every path

* **You edit one code block: Sidebar Options CSS/JS** (the `code` element whose `javascriptCode`
  contains `const DWCSidebarConfig`). Options are in its `javascriptCode`, variables in its `cssCode`.
  The engine block (`class DWCSidebarNavigation`) holds product code: never change it, except the
  documented breakpoint change. To change behaviour beyond options and variables, add your own CSS.
* **Change one value with a targeted replace.** Replace the exact text of that one line, confirm it
  occurs once, and write the whole field back. Never rewrite or reformat the rest of the field.
* **Send complete settings.** On `bricks/update-element`, send the element's full current settings
  with your change applied, unless the ability's schema says it merges.
* **Options are `1` or `0`**, except `reinitOnUrlChange` (`true`/`false`) and the breakpoints
  (`window.matchMedia("(max-width: Npx)")`).
* **Attributes: on is `"true"`, off is `""`.** Keep the attribute row and its `id`.
* **Element IDs and global class IDs are site-local.** Resolve them from the live tree every
  session. Never use an ID from any document, including this one.
* **A slide button opens the panel with the same `data-title`.** Exact match, unique per panel,
  readable: visitors see "back to <data-title>".
* **A success response proves the value persisted, not that it rendered.** Check the published
  page before you call a change done, and say which level you reached.
* **If the sidebar's code stops running** (`<body>` has no `sidebar-ready`), check that Code execution
  is on (Bricks > Settings > Custom code) and Execute code is on for both code blocks. Stop and tell
  the user; do not retry the write.
* **A refused write:** name the error code to the user, give them the builder steps for that change,
  and carry on with the rest. Never route around a refusal with PHP, REST or another ability.

### Find the header

1. `bricks/list-templates` with type `header`.
2. Read each candidate's tree with `bricks/get-page-elements` and save it to a file. The Sidebar
   Navigation Builder header has a root `block` with two `code` children: one whose `javascriptCode`
   contains `const DWCSidebarConfig` (options), one with `class DWCSidebarNavigation` (engine).
   Elements list global classes by ID: map IDs to names with `bricks/list-global-classes`
   (`perPage: 100`) when you need them.
3. More than one: ask the user which, by template title. None: see the build file, section 2.

Record the post ID and the IDs of the root block, the options block, the Header inner wrap, Nav and
the Home panel.

The root label carries the version: `Sidebar Nav 3.0.2`. The reference describes 3.0.2. For any other
version, compare the live option names and attributes with the reference. Where they differ, the live
code is authoritative and the reference is not.

### When the page disagrees with the builder

**Always fetch a published page with a unique query string** (`?nocache=<timestamp>`). Hosts and CDNs
serve old copies of the plain URL, and an old copy can be missing the whole header. A response header
reporting a cache hit (`x-hcdn-cache-status`, `cf-cache-status`, `x-cache`, `x-litespeed-cache`)
means the copy may predate your change: fetch again with a new query string.

Cheapest cause first, stop at the first hit: **did the write land on the template you checked**
(the ability response names the post ID), **was the copy cached** (above), **does this template
apply to this page** (template conditions). Three checks is the budget. If none explains it, report
the discrepancy and stop. Never sweep other pages or audit the site.

***

## Build path

Read `sidebar-nav-bricks-skills-build.md` in full, then follow its workflow from "START HERE".
Everything above still applies.

***

## Agent Skills Update

Where you record a finding depends on the session. Decide before writing anything. A session is a
**developer** session when `SIDEBAR NAV BRICKS/sidebar-nav-dev-context.md` is found by searching
upward from this file's folder, and a **user** session otherwise.

| Session | Record findings in | Never edit |
| --- | --- | --- |
| **Developer** | these skills files, routed by the table in the build file | `sidebar-nav-bricks-user-context.md` |
| **User** | `sidebar-nav-bricks-user-context.md`, in this folder | these skills files |

**If you cannot tell, treat it as a user session.** On a user install these files are overwritten by
the next update.

**Ask before you write, in either session.** Show the exact text, name the file and section, and
wait for agreement. If the answer is no, drop it rather than recording it somewhere else.

***

## Before you say you are done

End every task with a short report. Five lines, not a paragraph.

**Time.** Always give it. Run `date +%s` when you start and again at the end. If the task spans
several messages, save the start value in a file, so a context summary can't lose it.

**Calls.** How many Bricks ability calls you made.

**What changed.** Elements, attributes, variables and options you touched, by name. Name templates
and elements by their title, not only their ID. If you replaced or deleted anything, say so first.

**Custom code.** Name every place that now holds CSS or JS that the template doesn't ship: each
element, global class, code block or stylesheet, and what it styles. Say where the mobile rules are.
Write `Custom code: none` when you added none, and `No custom JS` when it is all CSS.

**What you verified, and how.** Say which level you reached: persisted (read-back) or rendered
(published page). Name anything you could not check as unverified.

**Do not report tokens or cost.** You cannot measure them.

```
3m 40s, 5 Bricks calls.
Changed: Sidebar Options CSS/JS enableCollapsibleSidebar 0 -> 1, hoverToExpandSidebar 0 -> 1; --sidebar-link-color dimgray -> #1a1a2e.
Custom code: none.
Verified: rendered. Published page at 1440px: sidebar.config.enableCollapsibleSidebar is 1, collapsed width 67px, tooltips on 9 items.
Unverified: builder view.
```
