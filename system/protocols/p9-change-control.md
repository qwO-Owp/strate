# P9 — Change control

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Only the Mother changes the system: the core, `system/`,
> and the structure of the living documents.
> - Each change is a diff with a reason.
> - Eliott gives an explicit go; a yes/no or readiness question is not a
>   go.
> - Then the write, a new seal, and a `decisions_log` entry.
>
> Eliott applies the core himself. Nothing changes silently.

- **Used by:** the Mère. Every other role only proposes (P3).

## 1. What counts as a change

| Change | Where it happens |
|---|---|
| the core (the Project's instruction field) | Mother → Eliott pastes it |
| `system/`: architecture, roles, protocols, templates, tools | Mother |
| the structure of a living document (its fields, its writer) | Mother |
| the content of a living document | its writer (architecture §8), with OK. Validations, marks and unlocks are recorded only at close. |

## 2. The procedure

1. **Diff and reason.** Show exactly what changes and why, as files when
   the change is large.
2. **Explicit go.** Wait for it. Never announce "je lance" and write in
   the same turn.
3. **Write.**
   - Re-read each document right before writing it.
   - Give every edited sealed doc (architecture, roles, protocols,
     `tools.md`) a **new seal**: a word and a number that appear only in
     its last line. Templates and starters carry none.
4. **Log.** A `decisions_log` entry: what, why, what is next.
5. **Seals to Eliott.** Whenever a sealed doc is written, give Eliott
   its new seal in the chat, and the full list at each release. He keeps
   them outside the Project. **They never go into a file — this log
   included:** in retrieval mode a role could surface a seal from it and
   quote one it never read, which is the exact failure the seal exists to
   catch.

## 3. Versions and releases

- **Numbering:**
  - 0.x: bootstrap;
  - **1.0-rc: in force since 2026-10-02**, the first pasted core;
  - `1.0-rc.N`: fixes released before 1.0 (`1.0-rc.2`, 2026-10-06);
  - 1.0: once the C5 audit's fixes are in; D2 commits it;
  - minor versions (1.1, 1.2): calibrations (wording, a role, a new
    living document);
  - major versions (2.0): a new layer, seam or core rule.
- **A release:**
  1. the `system/` docs are written;
  2. **the core's text is written to `system/core.md` and pasted by
     Eliott into the instruction field, in the same gesture.** The field
     is authoritative; the file is its release copy. Never one without
     the other;
  3. he receives the seal list: the seals that changed, and how many
     sealed docs there are in total, so he can check his own list is
     complete;
  4. `decisions_log` is updated;
  5. the public repo (since D1), in this order:
     1. the Mère builds the bundle from whole reads, the core as its
        public projection (architecture §10), and checks it: every seal
        line is its file's last line; the file list equals the
        `.gitignore` whitelist; a `diff` of the two cores shows one hunk,
        "Who Eliott is";
     2. the Navigateur runs the private-term check (the list lives in
        `living/environment.md` §2) and compares `git status` and
        `git ls-files` with the whitelist, before the commit;
     3. Eliott commits and pushes, then looks at the result on GitHub;
     4. `CHANGELOG.md` gets an entry with nothing private in it.
- **A release that touches no sealed doc costs him no list update.** The
  core carries no seal, so a core-only release is free in that sense —
  worth knowing when deciding whether a step can be split and the
  blocking half shipped first (C3c).
- **Canonical copy:** Project Knowledge holds the live system; the repo
  records releases. This reverses v0.1, where the repo was the canonical
  home; C3 states it in the core.

## 4. Guards

- **The brake:** what real work happened since the last change, and what
  does this one unblock? Once a project is running, maintenance of the
  system does not come before the pipeline in flight.
- **The spine** changes only on Eliott's explicit decision.
- **Prune:** propose removing rules that no longer earn their place.
- **Urgent fix:** if a role misbehaves in a way that risks integrity,
  Eliott stops that conversation. The Mère fixes the doc first, before
  anything else in her queue.
- **Read the document you are about to fix**, not the summary that
  queued the fix. A handoff line can under- or over-state a fault; the
  protocol itself cannot (C3c, the P7 case).

— p9-change-control.md v1.0 · seal: soffit-17 —
