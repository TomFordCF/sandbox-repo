# Before the Session — What You Need to Set Up

Please work through this checklist before the session. Most steps take only a few minutes each. The whole list should take **30–45 minutes** if you're starting from scratch.

If you get stuck on anything, reach out before the day — it's much easier to troubleshoot in advance than during the session itself.

---

## Checklist

- [ ] 1. Install Git
- [ ] 2. Create a GitHub account
- [ ] 3. Install VS Code
- [ ] 4. Enable GitHub Copilot
- [ ] 5. Install the GitHub Copilot extension in VS Code
- [ ] 6. Install Node.js
- [ ] 7. Verify everything is working

---

## 1. Install Git

Git is the version control tool that underpins the first exercise. It almost certainly needs to be installed separately on your Mac.

**How to check if you already have it:**
Open the Terminal app (search for "Terminal" in Spotlight — Cmd+Space). Type the following and press Enter:

```
git --version
```

If you see something like `git version 2.39.0`, you're done — skip to step 2.

If you see an error, install Git by downloading it from:
**[git-scm.com/download/mac](https://git-scm.com/download/mac)**

Follow the installer. Once it's done, close and reopen Terminal and run `git --version` again to confirm it worked.

---

## 2. Create a GitHub account

GitHub is the platform where the shared repository lives and where you'll open your first pull request.

If you don't already have an account, go to **[github.com](https://github.com)** and sign up with your work or personal email. The free tier is all you need.

If you already have a GitHub account, make sure you know your username and password — you'll need to log in during the session.

> **Note:** If your organisation uses GitHub Enterprise (a company-managed GitHub environment), check with your IT team about whether you should use that account or a personal one for this session.

---

## 3. Install VS Code

VS Code (Visual Studio Code) is the text editor you'll use throughout the session. It's free, widely used, and runs on Mac.

Download it from: **[code.visualstudio.com](https://code.visualstudio.com)**

Click **Download for Mac**, open the downloaded file, and drag VS Code into your Applications folder.

Open it at least once before the session to confirm it launches correctly.

---

## 4. Enable GitHub Copilot

GitHub Copilot is the AI assistant you'll use in Exercises 02 and 03. It's built by GitHub (owned by Microsoft) and works directly inside VS Code.

**Copilot requires a subscription or a free tier account.**

GitHub offers a free tier of Copilot that is sufficient for this session. To check whether you have access or to enable it:

1. Go to **[github.com/settings/copilot](https://github.com/settings/copilot)** and sign in.
2. If Copilot is not yet active on your account, you'll see an option to start a free trial or enable the free tier.
3. Follow the on-screen steps to activate it.

If your organisation has a GitHub Copilot Business or Enterprise licence, you may already have access — check with your IT or engineering team.

> **If you run into trouble with this step, flag it before the session.** Copilot access is required for Exercises 02 and 03, and it can occasionally take a few minutes to propagate after you activate it.

---

## 5. Install the GitHub Copilot extension in VS Code

Once Copilot is enabled on your GitHub account, you need to install the extension inside VS Code.

1. Open VS Code.
2. Click the **Extensions** icon in the left sidebar (it looks like four small squares).
3. Search for **GitHub Copilot**.
4. Click **Install** on the extension published by GitHub.
5. Once installed, you'll be prompted to sign in with your GitHub account. Do this and follow the steps to authorise VS Code.

You should see a small Copilot icon appear in the bottom status bar of VS Code once it's connected.

---

## 6. Install Node.js

Node.js is a tool that runs JavaScript on your computer. You won't write any JavaScript during the session, but it's needed in the background to run MCP servers in Exercise 03.

**How to check if you already have it:**
In Terminal, type:

```
node --version
```

If you see a version number (e.g. `v20.11.0`), you're done — skip to step 7.

If not, download and install the **LTS version** (the one labelled "Recommended For Most Users") from:
**[nodejs.org](https://nodejs.org)**

Open the downloaded `.pkg` file and follow the installer. Once done, run `node --version` again to confirm.

---

## 7. Verify everything is working

Once you've completed the steps above, do a quick check in Terminal:

```
git --version
```
```
node --version
```

Both should print a version number without errors.

Then open VS Code, click the Copilot icon in the left sidebar, and confirm it opens a Chat panel without any error messages. If it asks you to sign in again, do so.

---

## On the day

Please bring:

- Your laptop, charged
- Your GitHub username and password (or have your password manager ready)
- VS Code open and ready

That's it. Everything else will be provided or set up together during the session.

---

*Questions or stuck on a step? Reach out before the session and we'll get it sorted.*
