# Changelog

Versions follow Strate's own numbering (P9): 0.x bootstrap, 1.0-rc the
first live core, 1.0 after the external audit's fixes, minor versions for
calibrations, major versions for a new layer, seam or core rule.

## [1.0-rc.2] — 2026-10-06

Fixes released before 1.0.
- The published core keeps personal details private: its "Who Eliott is"
  section is reduced to a first name, the only difference from the live
  core, checked by diff at each release.
- The core states the Piscine rule without quoting campus sanctions:
  candidates are never recruited or admitted to a space the student runs.
- Two new core rules: questions for the student go in the reply, numbered
  and self-contained; a role departs from a protocol only when following
  it would defeat its purpose, and says so.
- Navigator: settings read back before being recorded as done; a first
  publication goes private, is checked, then made public; passphrases are
  never written to a file; handoffs for sessions that span days.
- Architecture and change control describe the public repository as it
  is: the whitelist `.gitignore`, the core's public projection, the
  checks before each commit.
- Course production: a twin may be a terminal lab; the integrity rule
  covers every graded file, not only functions; a render check before a
  page is recorded; size guidance per composition turn.
- Diagnostic: targeted blocks, aimed first at what the record declares
  solid.
- Builder: rules for an open community server: no Piscine candidates, no
  Piscine or exam material, no agent acting on the server.
- Toolbox: man pages in the workspace; testing allocation failures under
  ASan.

## [1.0-rc] — 2026-10-02

First release in service.
- The core (`system/core.md`): identity, spine, integrity, router, handshake.
- The architecture (`system/architecture.md`).
- Seven roles: Mère, Éclaireur, Professeur, Tuteur, Examinateur, Navigateur, Bâtisseur.
- Nine protocols, P1–P9.
- Templates: recon, atlas, course, eval, brief, starters.
- The toolbox (`system/tools.md`).
