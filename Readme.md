# Github Housekeeping

Reusable prompts and checklists for maintaining GitHub repositories to a consistent standard.

---

## Files

| File | Purpose |
|---|---|
| `repo-standardization-prompt.md` | Paste-and-run prompt for bringing any repo up to the house template — one repo per session |

## House template (target state for every repo)

- Public visibility
- Description present
- Real README (not a stub)
- Language-appropriate `.gitignore`
- No LICENSE file
- Secret scanning + push protection ON
- Dependabot alerts ON
- Default branch protected (no force-push, no deletion)
- Issues ON; Wiki OFF; Projects OFF

## Usage

Open Claude Code in (or pointed at) the target repo's folder, copy the full contents of `repo-standardization-prompt.md`, fill in the two blanks at the top, and paste. The prompt runs in phases and pauses for approval before making any change.
