# Setting up this project on another computer

This is the Flux + Thread website. It's already live at **https://fluxandthread.com** and the
code lives on GitHub at `flylow3d/fluxandthread`. These steps get a new computer (e.g. Sarah's
laptop, Windows) set up to **edit and publish** the site.

> Nothing here affects the live site or the domain — those run on GitHub/Porkbun's servers.
> This is only about being able to make changes from this computer.

## 1. Install the tools (all free)

Open **PowerShell** (Start menu → type "PowerShell") and paste these one at a time:

```powershell
winget install Git.Git
winget install GitHub.cli
winget install Microsoft.VisualStudioCode
```

Then install **Claude Code** by following the instructions at **https://claude.com/claude-code**
— the easiest route is the VS Code extension (open VS Code → Extensions → search "Claude Code" →
Install), then sign in with the Anthropic account.

*(Optional: only if you want to use the AI image-generation helper in `tools/`, also install
Python from https://python.org and recreate a `.env` file with a Gemini API key. Not needed for
normal editing.)*

## 2. Sign in to GitHub (as flylow3d)

Close and reopen PowerShell (so it sees the new tools), then run:

```powershell
gh auth login
```

Answer the prompts: **GitHub.com** → **HTTPS** → **Login with a web browser**. It opens a browser;
sign in with the **flylow3d** account. This also lets `git push` work without asking for a password.

## 3. Download the project

Pick where you want it (Documents is fine) and run:

```powershell
cd $HOME\Documents
git clone https://github.com/flylow3d/fluxandthread.git
```

That creates a `fluxandthread` folder containing everything.

## 4. Open it and start Claude

```powershell
code $HOME\Documents\fluxandthread
```

In VS Code, open Claude (the extension) in that folder. Claude reads `CLAUDE.md` automatically and
will know the full project history — what's built, the domain, what's pending.

## 5. The everyday workflow (publishing a change)

Whenever you change the site, three steps publish it (the live site updates in ~30–60 seconds):

```powershell
git add -A
git commit -m "short note about what changed"
git push
```

Or just ask Claude to do it for you. You can also use VS Code's **Source Control** panel (the
branch icon on the left) to do the same with buttons instead of commands.

**Before starting work each time, pull the latest first** (in case it was edited elsewhere):

```powershell
git pull
```

## Notes

- **Two computers, one project:** if both this laptop and the original computer edit the site,
  always `git pull` before you start and `git push` when you finish, so they stay in sync.
- **Claude's memory** (its private notes) is per-computer and won't transfer — but the important
  project context is all written down in `CLAUDE.md` and `SESSION_LOG.md`, which DO transfer.
- **Pending task:** the email signup form needs a free Web3Forms access key created with Sarah's
  email. See the "email signup" note in `CLAUDE.md`.
