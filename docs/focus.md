# Focus

What's been accomplished on this branch so far - read by `scripts/open-pr.py` as the PR description
(it falls back to the branch's commit subjects when this is empty).

Format: one `- ` line per finished piece of work, below the `---`: a short, user-facing one-liner.
Add the line when you actually finish the work (humans and AI agents alike) rather than trying to
reconstruct it right before opening the PR. Fold several small related lines into one when a theme is done.

`scripts/open-pr.py` empties the list (in the PR's last commit) once it is in the PR description, so it never holds over;
`scripts/new-branch.py` also empties it when it creates a new branch.

---

- Did a sweep of error handling an improved a great many places
- We now assume JSON with Comments for settings.schema.json files
- Removed the dependency and load-order fields the launcher read from a mod's mod.json (Required, Optional, Incompatible, LoadBefore, LoadAfter): mod.json belongs to the game; launcher settings go in dw2modlauncher.json
- Mods can declare `dependencies` in dw2modlauncher.json (required or optional, a minimum version, load order the launcher enforces), and hand data to each other over named channels (`provides` / `receives`): the launcher merges every provider's JSON files in load order and gives the receiving DLL the result in a separate InitWithOptions argument
- The details pane lists what a mod provides, receives and depends on, and which enabled mods are on the other end (nothing is shown for a mod that declares none)
- Mods can declare `provides` and `receives` to have the mod loader automatically accumulate and transport data from providers to receivers for a named interface
- The mod list subtitle and the details pane's source line now show just the mod's folder name or "Steam Workshop"