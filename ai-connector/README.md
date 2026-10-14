---
icon: sparkles
---

# AI Connector

The AI Connector lets an AI agent work on your Sidebar Navigation Builder header in Bricks. You describe what you want in plain English, and the agent changes your sidebar for you.

***

## What you need

* **Bricks 2.4 or later**, with the Sidebar Navigation Builder header template imported and set up. See [Installation](../getting-started.md).
* An **AI agent that can use MCP tools**, such as [Claude Code](https://docs.claude.com/en/docs/claude-code/overview), [Codex](https://openai.com/codex/) or [Cursor](https://www.cursor.com).

A chat window with no tools won't work.

***

## Set it up

Do both steps, in order.

### Step 1: Set up the Bricks MCP server

Follow this video: [How to Set Up the Bricks MCP Server (Bricks 2.4+)](https://youtu.be/JVsinkC7psM).

Come back here once your agent is connected to your site.

### Step 2: Add the skills files

The skills files teach your agent how the sidebar works in Bricks.

1. Make a folder on your computer for this work, for example `Sidebar Nav`. Open it in your agent and start a session there.
2. Paste this into the chat and send it:

```
Use curl to download these four files into a folder called sidebar-nav-bricks-skills in this project. Then read sidebar-nav-bricks-skills/sidebar-nav-bricks-skills.md and follow it.
https://raw.githubusercontent.com/udoro/Sidebar-Nav-Bricks-Docs/main/ai-connector/sidebar-nav-bricks-skills/sidebar-nav-bricks-skills.md
https://raw.githubusercontent.com/udoro/Sidebar-Nav-Bricks-Docs/main/ai-connector/sidebar-nav-bricks-skills/sidebar-nav-bricks-skills-build.md
https://raw.githubusercontent.com/udoro/Sidebar-Nav-Bricks-Docs/main/ai-connector/sidebar-nav-bricks-skills/sidebar-nav-bricks-skills-reference.md
https://raw.githubusercontent.com/udoro/Sidebar-Nav-Bricks-Docs/main/ai-connector/sidebar-nav-bricks-skills/sidebar-test.mjs
```

To update the skills later, paste the same message again.

**Prefer a manual download?** [Download this repository](https://github.com/udoro/Sidebar-Nav-Bricks-Docs/archive/refs/heads/main.zip), copy the `ai-connector/sidebar-nav-bricks-skills` folder into your project folder, and tell your agent to read `sidebar-nav-bricks-skills/sidebar-nav-bricks-skills.md`.

### Using Mega Menu Pro in the sidebar?

Also set up [Mega Menu Pro's AI Connector](https://design-with-cracka.gitbook.io/bricksmegamenupro/ai-connector) in the same project folder. The agent then makes Mega Menu Pro's own changes, such as its breakpoint, before Mega Menu Pro goes into the sidebar. Once Mega Menu Pro is a Section template, the agent can't change it any more: it tells you the steps to do in the builder instead.

***

## What you can ask for

**Change the look**

> *"Make the sidebar dark navy with white links, and orange on hover."*

> *"Make the icons smaller and the links closer together."*

**Change behavior**

> *"Let me collapse the sidebar to icons, and expand it on hover."*

> *"Hide the sidebar behind a menu button and push the page aside when it opens."*

**Add to the menu**

> *"Add a Services panel with links to Design, Build and Support."*

> *"Put a dropdown with our three locations under About."*

**Use it with Mega Menu Pro**

> *"Put my Mega Menu Pro Lite header in the sidebar's top bar, and show the sidebar on mobile only."*

**For the best results**

* Attach a screenshot of a sidebar you like.
* Say what should happen on mobile.
* Say if it should collapse, slide in, or stay open.

The agent asks before it changes the structure of your sidebar, and tells you how to undo it.

***

## Your context file

The agent keeps a file called `sidebar-nav-bricks-user-context.md` next to the skills files. It notes your preferences and what you've built, so the next session starts faster. The agent creates it on your first session and asks before it adds anything. Updating the skills files keeps it.

***

## Tips

* **Start each session by telling your agent to read `sidebar-nav-bricks-skills/sidebar-nav-bricks-skills.md`.** Agents don't remember earlier sessions.
* **Check the result on your site.** The agent checks your published pages, but it can't see inside your Bricks builder.
* **Undo the agent's last change:** in the builder, open the header template's **Revisions** panel, click the revision just below **Current version**, click **Apply**, then save.

***

## Troubleshooting

| Problem | What to do |
| --- | --- |
| The agent says it can't reach your site | Check your connection with the video in step 1, then start a new session. |
| The server shows as connected, but the agent has no Bricks tools | See [Connected, but no Bricks tools](#connected-but-no-bricks-tools) below. |
| The agent says an ability is turned off | Go to **Bricks > AI** and turn that ability on. |
| The agent says the sidebar's code isn't running | Go to **Bricks > Settings > Custom code** and check **Code execution** is on. Then check **Execute code** is on for both code blocks in the template. |
| The agent can't find your sidebar | Import the Sidebar Navigation Builder template first. See [Installation](../getting-started.md). |
| The agent gives you builder steps instead of making a change | Some changes can't be made through the Bricks MCP server. Do the steps in the builder, then tell the agent you're done. |
| Changes show in the builder but not on your site | Clear your site's cache. |

### Connected, but no Bricks tools

If your agent's MCP settings mention `mcp-wordpress-remote`, connect over HTTP instead. Do all three steps, in order.

**1. Make your sign-in token.** Copy this command:

```bash
node -e "console.log(Buffer.from('your-username:your-application-password').toString('base64'))"
```

Before you run it in a terminal, replace both placeholders. Keep the colon between them.

* `your-username`: your WordPress username. It's the `WP_API_USERNAME` value in your current MCP settings.
* `your-application-password`: your application password, spaces included. It looks like `abcd efgh ijkl mnop qrst uvwx`. It's the `WP_API_PASSWORD` value in your current MCP settings.

Copy the line it prints. That's your token. Keep it private, like the password.

**2. Swap the server.** First remove the old server:

* In Claude Code, run `claude mcp list` to see the old server's name. Then run `claude mcp remove` followed by that name, for example `claude mcp remove my-old-site`.
* In other agents, delete the old server's entry from their MCP settings.

Then add the new server. In Claude Code, open a terminal in your project folder and run:

```bash
claude mcp add --transport http my-bricks-site https://your-site.com/wp-json/mcp/mcp-adapter-default-server --header "Authorization: Basic YOUR_TOKEN"
```

For other agents, add this to their MCP settings:

```json
{
  "mcpServers": {
    "my-bricks-site": {
      "type": "http",
      "url": "https://your-site.com/wp-json/mcp/mcp-adapter-default-server",
      "headers": { "Authorization": "Basic YOUR_TOKEN" }
    }
  }
}
```

Put in your own site address and token. `my-bricks-site` is only a name for the server, so you can use any name you like, such as your site's name.

**3. Start a new agent session.** Agents only load MCP servers when a session starts.
