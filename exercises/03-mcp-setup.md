# Exercise 03 — MCP Servers: Connecting AI to Your Tools

**Time:** 30–40 minutes
**You'll need:** VS Code with GitHub Copilot, a stable internet connection

---

## What is MCP?

MCP stands for **Model Context Protocol**. Ignore the acronym — here's what actually matters.

Right now, Copilot can only see what's in front of it: the files you have open in your editor. It doesn't know what's in your Confluence wiki. It doesn't know what your Figma designs look like. It doesn't know what your analytics dashboards say.

**MCP changes that.**

MCP is a standard way for AI tools to connect to external applications — your company tools, internal systems, and data sources — so they can read from them and use that information when answering your questions.

Think of it like this: by default, Copilot is sitting at a desk with only the documents you've put in front of it. MCP gives it a pass to walk over to the relevant filing cabinet, open the right drawer, and pull out what it needs — without you having to copy and paste anything.

### Why does this matter for PMs?

PMs work across many tools at once — Confluence for specs and decisions, Figma for designs, Jira for the backlog, analytics platforms for usage data. The more context Copilot has, the more useful it becomes. With MCP, instead of you bridging the gap between tools manually, the AI can bridge it for you.

Instead of:
- Copy the Confluence page → paste into Copilot → ask your question

You get:
- *"Check the Confluence page and compare it to the PRD"* — and Copilot just does it.

---

## How MCP servers work

Each tool you want Copilot to access has its own **MCP server** — a small, lightweight bridge that knows how to talk to that tool's API. You install the server, add a short block of configuration to VS Code, and from then on you can reference that tool naturally in your Copilot prompts.

The server runs in the background. You never interact with it directly — you just ask Copilot questions that require it, and it calls the server automatically.

---

## Setting up MCP servers in VS Code

### Step 1 — Open your VS Code settings as JSON

Open the Command Palette: **Cmd+Shift+P** (Mac) or **Ctrl+Shift+P** (Windows).

Type `Preferences: Open User Settings (JSON)` and press **Enter**.

A file called `settings.json` will open. This file controls VS Code's behaviour — it's your personal configuration panel.

### Step 2 — Add the MCP server block

MCP servers live inside an `"mcp"` block in your `settings.json`. The full configuration for all four servers covered in this exercise looks like this — paste it into your settings file, then replace each placeholder value with your real credentials (see the sections below for exactly where to get each one):

```json
{
  "mcp": {
    "servers": {

      "confluence": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-confluence"],
        "env": {
          "CONFLUENCE_URL": "https://your-company.atlassian.net/wiki",
          "CONFLUENCE_USERNAME": "your-email@company.com",
          "CONFLUENCE_API_TOKEN": "your-atlassian-api-token"
        }
      },

      "figma": {
        "command": "npx",
        "args": ["-y", "figma-developer-mcp", "--stdio"],
        "env": {
          "FIGMA_API_KEY": "your-figma-personal-access-token"
        }
      },

      "mixpanel": {
        "command": "npx",
        "args": ["-y", "mixpanel-mcp"],
        "env": {
          "MIXPANEL_SERVICE_ACCOUNT_USERNAME": "your-service-account-username",
          "MIXPANEL_SERVICE_ACCOUNT_SECRET": "your-service-account-secret",
          "MIXPANEL_PROJECT_ID": "your-project-id"
        }
      },

      "slack": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-slack"],
        "env": {
          "SLACK_BOT_TOKEN": "xoxb-your-bot-token",
          "SLACK_TEAM_ID": "your-workspace-team-id"
        }
      }

    }
  }
}
```

> **If you already have other settings in your `settings.json`**, don't replace the whole file — add the `"mcp"` block alongside what's already there. If you're unsure, ask for help before saving.

### Step 3 — Where to get each credential

**Confluence (and Jira) — Atlassian API Token**

Atlassian uses a single API token for all its products (Confluence, Jira, etc.).

1. Go to: **[id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens)**
2. Click **Create API token**, give it a name (e.g. "VS Code MCP"), and copy the token.
3. Paste it as the value for `CONFLUENCE_API_TOKEN`.
4. Set `CONFLUENCE_URL` to your company's Atlassian domain — e.g. `https://luminarygroup.atlassian.net/wiki`.
5. Set `CONFLUENCE_USERNAME` to the email address you use to log into Atlassian.

**Figma — Personal Access Token**

1. In Figma, click your **profile icon** (top left) → **Settings**.
2. Scroll to the **Security** section and click **Generate new token**.
3. Give it a name (e.g. "VS Code MCP") and copy the token.
4. Paste it as the value for `FIGMA_API_KEY`.

**Mixpanel — Service Account**

1. In Mixpanel, go to **Settings → Organization Settings → Service Accounts**.
2. Click **Add Service Account**, give it a name, and note the username and secret it generates.
3. Find your Project ID under **Settings → Project Settings**.
4. Paste all three values into the corresponding fields in `settings.json`.

**Slack — Bot Token**

Slack requires you to create a small internal app to generate a bot token. It sounds more involved than it is.

1. Go to **[api.slack.com/apps](https://api.slack.com/apps)** and click **Create New App → From scratch**.
2. Give it a name (e.g. "Copilot MCP") and select your workspace.
3. In the left menu, go to **OAuth & Permissions**. Under **Scopes → Bot Token Scopes**, add the following: `channels:history`, `channels:read`, `groups:read`, `im:read`, `mpim:read`, `users:read`.
4. Scroll up and click **Install to Workspace**, then **Allow**.
5. Copy the **Bot User OAuth Token** (it starts with `xoxb-`) and paste it as `SLACK_BOT_TOKEN`.
6. To find your Team ID: in Slack, click your workspace name → **Settings & administration → Workspace settings**. The Team ID appears in the browser URL — it's the string starting with `T` (e.g. `T01AB2CD3EF`). Paste it as `SLACK_TEAM_ID`.

### Step 4 — Restart and verify

Save `settings.json`. Open the Command Palette and search for **MCP: List Servers** — you should see your servers listed. If any show an error, double-check the credential values for that server.

To test, open Copilot Chat and try: *"Using the Confluence MCP, list the spaces you can see."* If the connection is working, Copilot will return a list of Confluence spaces.

---

## What it looks like in practice

The three scenarios below show how you'd use connected MCP servers as a PM. These are **illustrated examples** — they show a realistic prompt and the kind of response you'd get back, so you can see what's possible before trying it with your own tools.

---

### Example 1 — Figma: checking designs against requirements

**The scenario:** The latest mockups for the AI Meeting Intelligence notification flow have just been shared. You want to check whether what the designer has built matches what the PRD specifies — without switching between tabs and cross-referencing manually.

**You type in Copilot Chat:**

> *"Using the Figma MCP, open the 'AI Meeting Intelligence — Notification Flow' frame in the Meridian design file. Compare what you see with the notification requirements in docs/prd-template.md section 5.4. Flag any places where the design and the written requirements don't align."*

**Example response from Copilot:**

> I've reviewed the Notification Flow frame in Figma and compared it with section 5.4 of the PRD. Here's what I found:
>
> **Aligned:**
> - The design correctly shows a Slack notification sent to the meeting host when a summary is ready. This matches the requirement in 5.4.
> - The host review screen matches the edit-before-sharing requirement in section 5.2.
>
> **Gaps and mismatches:**
> 1. **Email notification not in PRD:** The design includes an optional email notification to all meeting attendees when a summary is published. This behaviour isn't mentioned anywhere in the PRD — it's unclear whether this is an intentional addition or a design decision that hasn't been documented.
> 2. **Opt-out toggle missing from design:** The PRD's decisions log (Decision 5) specifies an opt-out model, but there's no visible suppress or opt-out control in the current notification flow mockups.
> 3. **Notification timing not reflected:** The PRD states summaries should be available within 15 minutes of meeting end, but the design doesn't surface this SLA to the user anywhere — for example, as a "your summary will be ready shortly" holding state.
>
> Would you like me to draft suggested requirement updates for items 1 and 3, or flag these as comments for the designer?

**Why this matters:** Design and requirements drift apart constantly in fast-moving teams. Catching it usually means one person carefully cross-referencing two tabs. With Figma connected, you get that audit in a single prompt — and you can run it again any time designs update.

---

### Example 2 — Confluence: auditing documentation consistency

**The scenario:** Your team maintains a technical architecture page in Confluence that includes data policies and integration decisions. You want to check whether your decisions log is consistent with what's formally documented — or whether the two have drifted apart since the last update.

**You type in Copilot Chat:**

> *"Using the Confluence MCP, find the Meridian technical architecture page in the 'Platform Engineering' space. Then read docs/decisions-log.md. Are there any decisions in the log that appear to conflict with what's documented in Confluence? Focus especially on data retention and platform integrations."*

**Example response from Copilot:**

> I've retrieved the Meridian Technical Architecture page from Confluence (last updated 14 November 2025) and compared it with the decisions log. I found two conflicts:
>
> **1. Data retention — direct contradiction**
> - Confluence states: *"All meeting recordings and transcripts are retained for a minimum of 30 days in line with the standard project artefact retention policy."*
> - Decisions log (Decision 4, 10 Dec 2025): audio is retained for **7 days** only, following Legal review.
>
> The decisions log entry is more recent and was signed off by Legal. The Confluence architecture page appears not to have been updated to reflect this decision. **Recommended action:** Update the Confluence page to reflect the 7-day audio retention window agreed in Decision 4.
>
> **2. Meeting platform scope — partial conflict**
> - Confluence states: *"The transcription integration supports Microsoft Teams and Zoom via the unified transcription adapter."*
> - Decisions log (Decision 3, 3 Dec 2025): Zoom was de-scoped from v1.
>
> The Confluence architecture page still references Zoom as an active integration target. **Recommended action:** Update Confluence to note that Zoom support is planned for v2, not v1, and remove the Zoom adapter from the current architecture diagram.
>
> Would you like me to draft the updated text for both sections?

**Why this matters:** Decisions get made in one place and documented in another, and the two rarely stay in sync. With Confluence connected, Copilot becomes a live consistency checker across your documentation — something that would take a careful human an hour to do, done in seconds.

---

### Example 3 — Mixpanel: turning data into a narrative

**The scenario:** You're preparing for a quarterly product review and want to make a data-backed case for the AI Meeting Intelligence feature. You need to understand where Meridian engagement is weakest among senior consultants — and turn that into a compelling problem statement.

**You type in Copilot Chat:**

> *"Using the Mixpanel MCP, look at the 'Meridian — Feature Engagement' dashboard for the last 90 days. Which features have the lowest engagement among Manager-level and above users? Based on that data, draft a short problem statement paragraph — 3–4 sentences — for an internal executive briefing arguing for the AI Meeting Intelligence feature."*

**Example response from Copilot:**

> Based on Mixpanel data for the 90-day period ending 4 March 2026:
>
> **Lowest engagement features (Manager+ users):**
> - Meeting notes (manual entry): 12% of eligible users active in the past 30 days
> - Post-meeting action item tracker: 9% of eligible users active in the past 30 days
> - Project handover log: 17% of eligible users active in the past 30 days
>
> The three lowest-engagement features are all post-meeting documentation tools — a clear signal that the current manual approach isn't working.
>
> **Drafted problem statement:**
>
> *"Meridian's post-meeting documentation features — meeting notes, action item tracking, and project handover logs — are used by fewer than one in five eligible senior consultants, despite being central to the platform's value proposition. Engagement data for the past 90 days shows that Manager-level and above users are consistently not recording meeting outcomes in Meridian, creating gaps in project knowledge and increasing handover risk. The barrier is not awareness; it is the friction of manual documentation against the pace of consulting work. AI Meeting Intelligence removes that friction entirely — turning meeting capture from a task that gets skipped into one that happens automatically."*
>
> Want me to adjust the tone or length, or pull in a specific data point to support the argument further?

**Why this matters:** PMs spend significant time extracting metrics from one tool and translating them into narratives in another. With Mixpanel connected, you move from raw engagement data to a first-draft argument in one step — and you can iterate on the framing without going back to the dashboard every time.

---

### Example 4 — Slack: surfacing decisions buried in conversation

**The scenario:** A key decision about the notification model was discussed in a Slack thread two weeks ago, but it never made it into the decisions log. You need to find it, confirm what was actually agreed, and get it documented before the next planning session.

**You type in Copilot Chat:**

> *"Using the Slack MCP, search the #meridian-product channel for conversations about notification preferences or opt-in/opt-out from the last 30 days. Summarise what was discussed and whether a clear decision was reached. Then compare that to what's currently written in docs/decisions-log.md Decision 5 and tell me if there's anything missing or contradictory."*

**Example response from Copilot:**

> I searched the #meridian-product channel for the last 30 days and found a relevant thread from 19 January 2026. Here's a summary:
>
> **What was discussed:**
> Sarah Chen raised the notification model question and proposed opt-out as the default. Marcus Webb agreed but flagged that the suppression option needs to be surfaced clearly in the meeting UI — not buried in settings. Priya Nair confirmed she'd add the suppress toggle to the host controls screen. Three people reacted with ✅.
>
> **Comparison with decisions-log.md Decision 5:**
> The core opt-out decision is accurately captured. However, Decision 5 doesn't mention the specific design requirement flagged by Marcus — that the suppress option must be visible in the meeting UI, not only in settings. This nuance is in the Slack thread but not in the formal log.
>
> **Suggested addition to Decision 5:**
> *"The opt-out suppress control must be accessible directly from the meeting host UI — not only from account settings — to ensure consultants can act on it in the moment. This was agreed by Marcus Webb and confirmed by Priya Nair on 19 January 2026."*
>
> Would you like me to add this to the decisions log now?

**Why this matters:** Slack is where real decisions often actually happen — in threads, in reactions, in quick back-and-forths that never make it into formal documentation. With Slack connected, Copilot can surface those conversations and reconcile them with your written records, closing the gap between what was agreed and what got written down.

---

## Reflection

Before you close this exercise, take a few minutes to sit with these questions. You don't need to write anything down.

**1. Which of your tools would be most valuable to connect?**
Think about where you spend time manually copying context between tools. Confluence? Notion? A design tool? Your analytics platform? A project management tool?

**2. What questions do you currently struggle to answer quickly?**
Are there things you'd ask an AI if only it could see your data? What would change in your day-to-day if it could?

**3. How would your planning process change if Copilot had access to all your tools at once?**
Would you write PRDs differently? Run reviews differently? Onboard new team members differently? Handle post-mortems differently?

MCP is still relatively new, and the ecosystem of available servers is growing quickly. Many tools you already use — Confluence, Jira, Figma, Slack, Notion, GitHub, and various analytics platforms — already have MCP servers available.

---

## Where to find more MCP servers

- **Official documentation and registry:** [modelcontextprotocol.io](https://modelcontextprotocol.io)
- **Full list of available servers:** [github.com/modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers)

Both are worth bookmarking. Search for your tool by name — if a server exists, it will be listed here along with its configuration instructions.

---

## You've completed all three exercises

Well done. You've:

- Made your first git contribution — clone, branch, commit, push, pull request
- Used Copilot in three modes — Chat, Edits, and Agent — to improve real product documents
- Understood what MCP servers are, seen how to configure them, and seen what connected AI looks like in practice

If you have time before the session wraps up, go back to any exercise and explore further. The best way to get comfortable with these tools is to use them on something you actually care about — bring in your own PRD, your own decisions, your own open questions, and see what happens.

---

*Session guide: `README.md` — start there if you need to reorient.*
