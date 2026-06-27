# Repo Standardization Prompt

A reusable prompt for bringing one GitHub repository up to a consistent
"house template" — synced with local, secured, and documented. Do **one repo
per session**: open Claude Code in (or pointed at) that repo's folder, paste the
prompt below, and fill in the two blanks at the top.

The prompt runs in phases and pauses for your approval before making any change.

---

## The prompt (copy everything in the block)

```text
Standardize ONE of my GitHub repositories to my house template. I do one repo
per session, so treat this as a self-contained task for a single repo. Follow my
global rule: ask for explicit approval before changing any file or any GitHub
setting — show me the plan first and wait for my "go ahead."

REPO FOR THIS SESSION:
- GitHub repo (owner/name): __________________
- Local clone path (or "not cloned locally"): __________________

PHASE 1 — ASSESS (read-only, make NO changes):
1. Confirm gh is authenticated (gh auth status).
2. Report the repo's current state: visibility, description (present/empty),
   default branch name, Issues enabled?, README.md present (real vs. stub)?,
   .gitignore present?, LICENSE present?, and security settings (secret
   scanning, push protection, Dependabot alerts, default-branch protection).
3. If a local path was given: run git status and git fetch, then tell me whether
   local and GitHub are in sync / ahead / behind / diverged, and list any
   uncommitted changes.
4. Summarize the gaps versus my template (below) and give me a short plan.
   STOP and wait for my approval before Phase 2.

PHASE 2 — SYNC (after I approve):
5. If there are uncommitted local changes, show them and ask before committing
   (propose a commit message). Never commit silently.
6. Push so GitHub matches local. NEVER force-push. If the branches have
   diverged, explain why and ask me how to proceed.

PHASE 3 — STANDARDIZE (after I approve; one logical change at a time):
7. Visibility: if the repo is not already PUBLIC, make it public now
   (gh repo edit --visibility public). Public repos unlock secret scanning,
   push protection, Dependabot, and branch protection on the free plan.
8. Description: if missing, propose a one-line description and set it.
9. README.md: if missing, draft one from the ACTUAL code (purpose, install,
   usage) and add it. If it exists, confirm it isn't a stub.
10. .gitignore: if missing or wrong for the language, propose one.
11. LICENSE: do NOT add a LICENSE file. Skip this step entirely.
12. Security settings (match my PDF-to-Markdown-Converter repo):
    - Enable secret scanning + push protection
    - Enable Dependabot vulnerability alerts
    - Protect the default branch: block force-pushes and deletion
13. Enable Issues; disable Wiki; disable Projects (always — no exceptions).

PHASE 4 — REPORT:
14. Give me a checklist: what you changed, what was already fine, and anything
    that needs MY action or a decision.
15. Also FLAG (don't auto-fix) any of: secrets that look already-committed in
    history, default branch not named "main", repo looks stale/abandoned
    (suggest archiving), or a wrong/confusing repo name.

MY HOUSE TEMPLATE (the target state for every repo):
- GitHub is in sync with my local clone
- Has a Description
- Has a real README.md (not a stub)
- Has a language-appropriate .gitignore
- No LICENSE file
- Secret scanning + push protection ON
- Dependabot alerts ON
- Default branch protected (no force-push, no deletion)
- Issues ON; Wiki OFF; Projects OFF
- All repos are PUBLIC

One-time, account-wide (NOT per repo) — remind me if not done: enable 2FA on my
GitHub account.
```

---

## Notes

- **One repo per session.** The prompt is deliberately scoped to a single repo
  so you can spread the work across days.
- **It pauses for approval** after the read-only assessment (Phase 1) and before
  any change — nothing is modified without your sign-off.
- **All repos are public.** This is a house rule, not a per-repo decision. Making
  repos public also unlocks secret scanning, push protection, Dependabot alerts,
  and branch protection on the free GitHub plan.
- **Reference repo:** the security baseline mirrors
  `vtak007/PDF-to-Markdown-Converter`, the first repo set up this way.
