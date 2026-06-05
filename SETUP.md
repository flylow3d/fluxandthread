# Setting up this project on another computer

This guide takes a brand-new computer from **nothing installed** to a working copy of the
**Flux + Thread** website that can edit and publish the live site. It is self-contained — you do
**not** need the project files yet; Step 4 downloads them.

## For Claude (read this first)

If a human handed you this file on a fresh machine, your job is to help them install the tools,
sign in to GitHub, and clone this repo. Important boundaries:

- **You (Claude) can run:** the install commands, `git config`, verification commands
  (`gh auth status`, `gh repo view`, `git remote -v`), and the `git clone`.
- **Only the human can do** (these are interactive — guide them, then wait):
  - Completing the GitHub browser sign-in during `gh auth login` (entering username/password/2FA).
  - Installing the Claude app/extension and signing in to the Anthropic account.
- **Two different logins** are involved — don't confuse them: the **GitHub** account
  (`flylow3d`) is for the code; the **Anthropic/Claude** account is for Claude itself.
- After each step, run the listed **verify** command and confirm it passed before moving on.

## Project facts

- **Live site:** https://fluxandthread.com  (also `www.` → redirects to it)
- **GitHub repo:** `flylow3d/fluxandthread`  →  https://github.com/flylow3d/fluxandthread
- **Clone URL:** `https://github.com/flylow3d/fluxandthread.git`
- **GitHub account to use:** `flylow3d` (the owner of the repo and the domain)
- **What it is:** a static website (plain HTML/CSS) published by GitHub Pages. No build step.
- **Hosting/domain run on servers, not this computer** — setting up here only affects *editing
  and publishing*, never the live site.

---

## Step 0 — Which operating system?

The commands below are written for **Windows** (using `winget`, which is built into Windows 10/11).
If this is a **Mac**, use the macOS column instead (it uses Homebrew — if `brew` is missing,
install it first from https://brew.sh). If unsure, on Windows the Start menu has "PowerShell";
on Mac, Spotlight (⌘+Space) has "Terminal".

---

## Step 1 — Install the tools (all free)

Open a terminal (**PowerShell** on Windows, **Terminal** on Mac) and run these one at a time.

**Windows (PowerShell):**
```powershell
winget install Git.Git
winget install GitHub.cli
winget install Microsoft.VisualStudioCode
```

**Mac (Terminal):**
```bash
brew install git
brew install gh
brew install --cask visual-studio-code
```

Then **close and reopen the terminal** so it picks up the newly installed tools.

**Verify** (should print version numbers, not "not recognized"):
```
git --version
gh --version
```

**Install Claude Code** separately by following https://claude.com/claude-code — the easiest route
is the **VS Code extension**: open VS Code → Extensions (the squares icon) → search "Claude Code" →
Install → sign in with the **Anthropic** account. *(This is the human's step.)*

> Optional, only for the AI image-generation helper in `tools/`: install Python from
> https://python.org and later create a `.env` with a Gemini API key. **Not needed** to edit or
> publish the site — skip unless you specifically want that tool.

---

## Step 2 — Tell git who you are

Git stamps each save with a name and email. Set them once (use the flylow3d identity so commits
are attributed to the same account):

```
git config --global user.name "flylow3d"
git config --global user.email "flylow3d@gmail.com"
```

**Verify:**
```
git config --global user.name
git config --global user.email
```

---

## Step 3 — Sign in to GitHub (as flylow3d)

Run:
```
gh auth login
```
Answer the prompts exactly like this (use the arrow keys + Enter):
1. **What account?** → `GitHub.com`
2. **Preferred protocol?** → `HTTPS`
3. **Authenticate Git with your GitHub credentials?** → `Yes`
4. **How to authenticate?** → `Login with a web browser`
5. It shows a **one-time code** and opens your browser. **(Human:)** copy the code into the
   browser and sign in as **flylow3d** (username + password, and 2-factor if prompted).

This step both signs you in *and* sets up git so `git push` works without re-entering a password.

**Verify** (should say "Logged in to github.com account flylow3d"):
```
gh auth status
```
And confirm access to the repo (should print repo details, no error):
```
gh repo view flylow3d/fluxandthread
```

---

## Step 4 — Download (clone) the project

Pick a location (Documents is fine) and clone:

**Windows:**
```powershell
cd $HOME\Documents
git clone https://github.com/flylow3d/fluxandthread.git
```
**Mac:**
```bash
cd ~/Documents
git clone https://github.com/flylow3d/fluxandthread.git
```

This creates a `fluxandthread` folder with everything in it.

**Verify** the download and the GitHub link:
```
cd fluxandthread
git status            # should say "On branch main ... working tree clean"
git remote -v         # should list origin -> github.com/flylow3d/fluxandthread
```

---

## Step 5 — Open it and start Claude

**Windows:**
```powershell
code $HOME\Documents\fluxandthread
```
**Mac:**
```bash
code ~/Documents/fluxandthread
```

In VS Code, open Claude in that folder. Claude will read `CLAUDE.md` automatically and know the
full project history, what's live, and what's pending.

---

## Step 6 — Confirm publishing works (the round trip)

To be 100% sure pushing works, do a tiny no-op sync (this changes nothing on the site):

```
git pull       # gets any latest changes; should say "Already up to date"
git push       # should say "Everything up-to-date"
```

If both run without an authentication error, the GitHub connection is fully working. The real
publish flow (when you actually change something) is:

```
git add -A
git commit -m "short note about what changed"
git push
```
The live site updates ~30–60 seconds after a push. You can also use VS Code's **Source Control**
panel (branch icon on the left) to do add/commit/push with buttons instead of typing.

> **Before starting work each session,** run `git pull` first — especially if the site is ever
> edited from more than one computer — so you start from the latest version.

---

## Troubleshooting

- **`git: 'commit' ... Please tell me who you are`** → you skipped Step 2. Run the two
  `git config --global` commands.
- **Push asks for a password / says authentication failed** → run `gh auth login` again (Step 3)
  and make sure you chose **HTTPS** and answered **Yes** to "authenticate Git".
- **`winget` not recognized (Windows)** → update "App Installer" from the Microsoft Store, or
  install Git/gh/VS Code from their websites: git-scm.com, cli.github.com, code.visualstudio.com.
- **`code` not recognized** → in VS Code, press `Ctrl/Cmd+Shift+P`, run
  "Shell Command: Install 'code' command in PATH", then reopen the terminal. (Or just open the
  folder from VS Code's File → Open Folder.)
- **`LF will be replaced by CRLF` warnings on Windows** → harmless. It's just git normalizing
  line endings; ignore them.
- **Permission denied pushing / "must be a collaborator"** → you're signed in as the wrong GitHub
  account. Re-run `gh auth login` and sign in as **flylow3d**.

## Good to know

- **Claude's memory** (its private notes) is tied to each computer's folder path and does **not**
  transfer. That's fine — all the durable project context is written in `CLAUDE.md` and
  `SESSION_LOG.md`, which are in the repo and travel with it.
- **Don't hand-copy the project folder** between computers — always `clone` (Step 4) or `git pull`.
  Copying can carry machine-specific junk and miss the GitHub wiring.
- **Pending task:** the email signup form needs a free Web3Forms access key created with Sarah's
  email, pasted into the `access_key` field in `index.html`. See the "email signup" note in
  `CLAUDE.md` for the exact spot.
