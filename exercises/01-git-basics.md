# Exercise 01 — Git Basics: Your First Contribution

**Time:** 20–30 minutes
**You'll need:** VS Code open, a terminal, a GitHub account
**Working file:** `docs/prd-template.md`

---

## What you're doing in this exercise

By the end of this exercise, you will have:

1. Cloned this repository to your own computer
2. Created your own branch (your personal working space)
3. Made a real change to the PRD
4. Committed that change with a meaningful message
5. Pushed your work to GitHub
6. Opened a pull request

These are the core git actions that happen dozens of times a day on any product team. Once you've done them once, they'll feel familiar fast.

---

## A quick mental model before you start

Think of git like this:

- **The repository** is the shared filing cabinet that the whole team uses — it lives on GitHub.
- **Your local copy** is the version downloaded onto your laptop — your personal working space.
- **A branch** is a separate drawer in the filing cabinet where you do your work without affecting anyone else's version.
- **A commit** is saving a snapshot of your work with a note explaining what changed.
- **A push** is sending your commits back up to the shared filing cabinet on GitHub.
- **A pull request** is raising your hand and saying: "I've made some changes — can someone review them before we put them in the main version?"

---

## Step 1 — Open a terminal

In VS Code, open a terminal by going to **Terminal → New Terminal** in the top menu bar.

A terminal panel will appear at the bottom of your screen. This is where you'll type the commands below. Click inside it to make sure it's active, then start typing.

> **What is a terminal?** It's a text-based way to talk to your computer — like a very direct messaging app where the computer always replies instantly. You're only using a handful of commands here, and every single one is written out for you.

---

## Step 2 — Clone the repository

Cloning means downloading a full copy of this repository to your laptop. Type this command, replacing the URL with the one for this repo (you can find it by clicking the green **Code** button on the GitHub page and copying the HTTPS link):

```
git clone https://github.com/TomFordCF/sandbox-repo.git
```

Press **Enter**. After a few seconds, you should see something like:

```
Cloning into 'sandbox-repo'...
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
Receiving objects: 100% (14/14), done.
```

> **What just happened?** Git downloaded a complete copy of the repository — every file and its full history — to a new folder called `sandbox-repo` on your computer.

---

## Step 3 — Navigate into the folder

Now move your terminal into the folder you just downloaded:

```
cd sandbox-repo
```

Press **Enter**.

> **What just happened?** `cd` stands for "change directory" — it's the equivalent of double-clicking a folder to open it. Your terminal is now working inside the `sandbox-repo` folder. To confirm, type `pwd` and press Enter — it will print the full path to where you are.

---

## Step 4 — Check the current state

Before making any changes, check that everything looks clean:

```
git status
```

You should see:

```
On branch main
nothing to commit, working tree clean
```

> **What just happened?** `git status` shows you the current state of your local copy. "Nothing to commit, working tree clean" means your version matches the remote exactly — no changes yet.

---

## Step 5 — Create your own branch

Create a branch to do your work on. Use your own name — replace `your-name` with something like `sarah-chen` or `marcus-w`:

```
git checkout -b your-name/update-prd
```

You should see:

```
Switched to a new branch 'your-name/update-prd'
```

> **What just happened?** You've created a new branch and switched to it in one step. Any changes you make now exist only on this branch — the `main` branch (the shared version) is completely unaffected. The `-b` flag tells git to both create the branch and switch to it at the same time.
>
> Naming branches with `your-name/description` is a common convention on product teams — it makes it obvious who's working on what.

---

## Step 6 — Open the PRD in VS Code

In VS Code's file explorer (the panel on the left side of the screen), click on `docs` to expand the folder, then click on `prd-template.md`.

The file will open in the main editor. Take two minutes to read through it. You'll notice:

- Some sections are complete and polished
- Others have obvious placeholders — things like `[X hours per week]`, `[Add your question here]`, and `[TBD]`
- Some requirements say `[To be defined]` rather than specifying the actual behaviour

These gaps are intentional. They represent the kind of open items that sit in a real PRD waiting to be resolved.

---

## Step 7 — Make a change

Find the **Open Questions** table near the bottom of the PRD. It ends with this row:

```
| 4 | [Add your question here] | | |
```

Replace it with a real question you'd ask about this feature if you were the PM. Here are some examples to get you started — pick one or write your own:

```
| 4 | How do we handle a meeting where the AI summary contains a factual error that was already shared with the client? | Sarah Chen | Open |
```

```
| 4 | Should consultants be able to mark a meeting as confidential to prevent it from syncing to the workspace? | Sarah Chen / Legal | Open |
```

You can also fill in the `[X hours per week]` placeholder in the Problem Statement. Something like `3–5 hours per week` is a reasonable estimate for a consultancy context.

Once you've made your change, save the file with **Cmd+S** (Mac) or **Ctrl+S** (Windows).

---

## Step 8 — See what changed

Run `git status` again:

```
git status
```

This time you'll see:

```
On branch your-name/update-prd
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)

	modified:   docs/prd-template.md
```

To see exactly what changed, line by line, run:

```
git diff docs/prd-template.md
```

Lines starting with `+` are additions. Lines starting with `-` are removals. Press `q` to exit the diff view.

> **What just happened?** Git has noticed that `prd-template.md` has been modified. But the change only exists on your computer — you haven't told git to track it yet.

---

## Step 9 — Stage your change

"Staging" means selecting which changes you want to include in your next commit. Think of it as putting something in an envelope before you seal and send it.

```
git add docs/prd-template.md
```

Run `git status` again to confirm:

```
git status
```

You should see:

```
Changes to be committed:
	modified:   docs/prd-template.md
```

> **What just happened?** Your change has moved from "modified but untracked" to "staged and ready to commit." Git now knows to include this change in your next snapshot.

---

## Step 10 — Commit your change

Now create a commit — a permanent, labelled snapshot of your staged changes. The message after `-m` is the label:

```
git commit -m "docs: add open question about [what you wrote]"
```

For example:

```
git commit -m "docs: add open question about handling AI summary errors shared with clients"
```

You should see something like:

```
[your-name/update-prd 3a2f1c8] docs: add open question about handling AI summary errors shared with clients
 1 file changed, 1 insertion(+), 1 deletion(-)
```

> **What just happened?** You've created a commit — a permanent, named snapshot of your changes. The long string of letters and numbers (like `3a2f1c8`) is git's unique identifier for this specific commit.
>
> **On commit messages:** Good commit messages are short, specific, and written in the present tense. They describe *what* changed, not just "updated file." Many teams use a prefix convention like `docs:`, `fix:`, `feat:` to categorise changes at a glance.

---

## Step 11 — Push your branch to GitHub

Your commit exists on your laptop. Now send it up to GitHub:

```
git push origin your-name/update-prd
```

You should see:

```
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
To https://github.com/TomFordCF/sandbox-repo.git
 * [new branch]      your-name/update-prd -> your-name/update-prd
```

> **What just happened?** You've sent your branch — and all its commits — up to GitHub. `origin` is just git's shorthand for "the remote repository this was cloned from." Other people can now see your branch.

---

## Step 12 — Open a pull request

1. Go to this repository on GitHub in your browser.
2. You should see a yellow banner near the top of the page: **"your-name/update-prd had recent pushes"** with a green **Compare & pull request** button. Click it.
3. Give your pull request a clear, specific title. For example: `Add open question about handling AI summary errors`
4. In the description box, briefly explain what you changed and why. One or two sentences is plenty.
5. Click **Create pull request**.

> **What just happened?** You've opened a pull request — a formal proposal to merge your changes into the main branch, with a built-in space for review and discussion. On real teams, this is where colleagues leave comments, ask questions, and approve changes before anything goes live. Your PR is visible to the whole team.

---

## You did it

You've just completed the full git contribution loop:

**clone → branch → edit → stage → commit → push → pull request**

This is the same workflow engineers, technical writers, data teams, and an increasing number of PMs use every day. The commands get faster with repetition, and once they're in your muscle memory, you'll stop thinking about them at all.

---

## Bonus: things worth exploring

- Type `git log` and press Enter — what do you see?
- Type `git branch` — what branches exist? Which one are you on?
- Go to your pull request on GitHub. Can you leave a comment on your own PR? (You can — it's useful for leaving context for reviewers.)
- What happens if you click **Files changed** on the PR page?

---

**Next:** Head to `exercises/02-copilot-modes.md` to start working with GitHub Copilot.
