# Exercise 02 — Working with GitHub Copilot

**Time:** 30–40 minutes
**You'll need:** VS Code with the GitHub Copilot extension installed and signed in
**Working files:** `docs/prd-template.md`, `docs/decisions-log.md`

---

## Before you start

GitHub Copilot is an AI assistant built directly into VS Code. It can read your files, answer questions, make edits, and — in its most capable mode — work through multi-step tasks on your behalf.

In this exercise, you'll work through three modes in order, from conversational to autonomous. Each one is more hands-off than the last.

One thing worth knowing before you dive in: as you type in any file, Copilot may offer suggestions inline — a greyed-out completion appearing directly in your text. If you see one you like, press **Tab** to accept it and move on. If not, just keep typing and it will disappear.

---

## The three modes at a glance

| Mode | What it does | Best for |
|---|---|---|
| **Chat** | Conversational Q&A in a sidebar panel | Exploring ideas, asking questions, generating first drafts |
| **Edits** | Makes direct, reviewable changes to specific files | Targeted rewrites, filling placeholders, standardising format |
| **Agent** | Works autonomously across multiple files toward a goal | Multi-step tasks, cross-document analysis, brief-driven work |

Think of it as a progression. Chat is like talking to a colleague. Edits is like asking them to redline a document. Agent is like handing them a brief and asking them to come back when it's done.

---

## Mode 1 — Chat

### What it does

Chat opens a sidebar where you can have a back-and-forth conversation with Copilot. You describe what you want, it responds in the panel. It does not make changes to your files unless you explicitly copy the output and paste it in yourself — you're always in control.

### When a PM would use it

- "Help me think through the risks of this approach"
- "Suggest user stories for this persona"
- "Explain the difference between opt-in and opt-out consent in a product context"
- "Read this section and tell me what's unclear or missing"

### How to open it

Click the **Copilot icon** in the left sidebar (it looks like a small sparkle or star shape), then select **Chat**. Alternatively, press **Ctrl+Shift+I** on Windows or **Cmd+Shift+I** on Mac.

---

### Exercise 2a — Use Chat to find gaps in the Risks section

Open `docs/prd-template.md` and scroll to the **Risks** table. Right now it has two rows and a placeholder.

Open Copilot Chat and try this prompt:

> *"I'm a PM at a technology consultancy working on an internal AI meeting transcription feature. I have a PRD with a Risks table that currently lists two risks: low consultant adoption due to discomfort with recording, and AI summaries being inaccurate enough to damage client trust. Suggest two additional risks I might be missing that are specific to a consultancy context — things like contractual, competitive, or operational risks. Write them in the same format as the existing rows: Risk, Likelihood, Impact, Mitigation."*

When Copilot responds:

1. Read the suggestions critically. Are they plausible for a consultancy like Luminary? Would they apply here?
2. Pick the most useful one, copy it, and add it to the Risks table in the PRD.
3. Edit the mitigation column to make it feel grounded in Luminary's context — even if that means writing `[To be defined]` for now.

> **What to notice:** The AI gave you a starting point, but *you* made the judgement call about what was realistic and relevant. That's the right dynamic — Copilot reduces the blank-page problem, you apply the context it doesn't have.

---

### Exercise 2b — Use Chat to generate a missing user story

In the PRD, under **User Stories**, there's a placeholder for the Project Lead persona:

```
- [Add user story here]
```

Open Copilot Chat and try:

> *"I'm writing a PRD for an AI meeting transcription feature. After meetings end, the system generates a structured summary — decisions, action items, key discussion points — and syncs it to a project workspace. I need one more user story for a Project Lead persona who oversees multiple client workstreams but doesn't attend every meeting. What would they care about most? Write it as a single user story in the format 'As a Project Lead, I want to... so that...' "*

Use the response to fill in the placeholder in `docs/prd-template.md`.

---

## Mode 2 — Edits

### What it does

Edits mode lets you instruct Copilot to make changes directly to one or more open files. You describe what you want, Copilot proposes the edits, and you see a diff — additions and removals highlighted — before you accept anything. Think of it like tracked changes in Word, but the AI is the one doing the redlining.

### When a PM would use it

- "Tighten this section — it's too long"
- "Rewrite this requirement in plain English, it reads like internal engineering shorthand"
- "Fill in this placeholder based on the context elsewhere in the document"
- "Standardise the formatting across this whole table"

### How to open it

In the Copilot panel, look for **Edits** — often shown as a pencil icon or accessible via a dropdown at the top of the Chat panel. You can also press **Ctrl+Shift+E** / **Cmd+Shift+E** depending on your configuration.

Once open, you can specify which files Copilot should be allowed to edit.

---

### Exercise 2c — Fill in a placeholder requirement

In `docs/prd-template.md`, section 5.4 (Notifications) contains this unresolved placeholder:

```
- [Define notification preferences — opt-in vs opt-out? Confirm with Priya re: UX implications]
```

Open Copilot Edits, add `docs/prd-template.md` as the working file, and try:

> *"In prd-template.md, replace the notification preferences placeholder in section 5.4 with a clear, specific functional requirement. The product is an internal enterprise tool for a professional services firm — consultants need to know about meeting summaries, but shouldn't feel surveilled. Base your recommendation on what makes sense for this context. Match the tone and bullet format of the surrounding requirements."*

Before you accept Copilot's proposed change, check it against **Decision 5** in `docs/decisions-log.md`. Does the proposed requirement align with the opt-out decision that was already made? If not, edit it until it does.

> **What to notice:** This is a very common PM situation — AI generates something plausible, but you need to reconcile it with decisions that already exist elsewhere. The AI doesn't know what's in your decisions log unless you tell it.

---

### Exercise 2d — Sharpen the Problem Statement

The Problem Statement in the PRD is a bit vague. It doesn't quite sell the problem yet — it describes it, but doesn't make you feel it.

Open Copilot Edits and try:

> *"In prd-template.md, rewrite the Problem Statement section to be more specific and compelling. Keep it to 3–4 tight sentences. Replace the [X hours per week] placeholder with a realistic-sounding estimate (use 3–5 hours). The audience is internal stakeholders at a consultancy — smart people who are time-poor and need to quickly understand why this matters. Keep the professional, internal-document tone."*

Review what Copilot proposes. Accept the changes that feel right, and manually edit anything that feels off or generic.

---

## Mode 3 — Agent

### What it does

Agent mode is the most autonomous of the three. You give Copilot a higher-level goal — a brief, not a request — and it figures out the steps: reading files, planning changes, making edits across multiple documents. It works like a capable colleague you've handed a task to, rather than a tool you're operating.

Agent mode will always tell you what it's planning to do before it acts. Read that plan. You can course-correct before anything is changed.

### When a PM would use it

- "Review all my documentation and flag inconsistencies"
- "Update the changelog to reflect what changed in the PRD"
- "Draft a summary of the decisions log in plain English for a stakeholder update"
- "Read the PRD and the decisions log and identify what's still unresolved"

### How to open it

In the Copilot panel, look for **Agent** mode — usually accessible via a dropdown at the top of the Chat panel, or via the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`, then search for "Copilot Agent").

---

### Exercise 2e — Ask Agent to find inconsistencies between the PRD and decisions log

This is the most powerful exercise in the session. You're going to ask Copilot to read two documents simultaneously and identify contradictions between them.

Open Copilot Agent and try this prompt:

> *"Please read docs/prd-template.md and docs/decisions-log.md in full. Compare the two documents carefully and list any inconsistencies you find — places where the PRD and the decisions log contradict each other, or where the PRD hasn't been updated to reflect a decision that was made. Don't make any edits yet. Just list what you find and explain each inconsistency clearly."*

Copilot will read both files and return a list. There are **at least three intentional inconsistencies** between these two documents. See if Copilot catches all of them.

Once you have the list:

1. Go through each inconsistency. Do you agree it's a real contradiction?
2. Decide which document is "correct" — the decision or the PRD requirement?
3. Use Edits mode to fix the PRD to align with the decisions log, one inconsistency at a time.

> **Why this matters for PMs:** Documentation sprawl is one of the most persistent problems in product work. PRDs, decisions logs, changelogs, and Confluence pages all drift apart over time. Asking AI to audit consistency across your documents is one of the highest-leverage things you can do with Copilot — and it takes seconds rather than the hour it would take to do manually.

---

## Wrapping up

You've now used all three Copilot modes:

- **Chat** for exploration, ideation, and generating first drafts
- **Edits** for targeted, reviewable changes to specific files
- **Agent** for multi-file analysis and brief-driven autonomous work

The pattern that works: Copilot handles the first draft, the analysis, and the tedious parts. You make the judgement calls, check the context it doesn't have, and make the output actually good.

---

**Next:** Head to `exercises/03-mcp-setup.md` to learn how to connect Copilot to your real tools with MCP servers.
