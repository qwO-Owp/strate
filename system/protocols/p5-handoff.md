# P5 — Handoff

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** A handoff lets a fresh conversation continue exactly
> where the last one stopped. Write it at the end of every Tuteur step,
> every build session, and whenever a conversation grows long or starts
> losing track. It carries the P2 report fields too. Name it so the next
> conversation can find it without searching.

- **Used by:** the Tuteur (every step), the Bâtisseur (every session), the
  Mère (when her conversation degrades), any role whose conversation grows
  long.

## 1. When

- At the end of every atlas step (Tuteur) or build session (Bâtisseur).
- When the conversation grows long, or shows the signs of it:
  - it forgets earlier decisions;
  - it repeats questions;
  - it contradicts its role doc;
  - it misses the seal on a re-check.

  Better one handoff too early than one too late.

## 2. Names and places

| Handoff | File |
|---|---|
| a Tuteur step | `projects/<p>/handoff-<step>.md`, for example `handoff-P1.2.md` |
| a build session | `builds/<object>/handoff-<n>.md` (n = 1, 2, 3…) |
| a course spanning conversations | `courses/<concept>-handoff.md`, deleted once the course is approved |
| the Mother | `living/mother_handoff.md` (the Mère is its only writer; one Mother at a time) |
| another long conversation | next to its object: `projects/<p>/handoff-<role>-<n>.md` or `builds/<object>/handoff-<n>.md` |

Handoffs never go into `inbox/`: it holds only proposals for the Mère.

## 3. The format

```
## Handoff — <role> · <object> <step> · <YYYY-MM-DD>
- Done: <what this conversation did>
- State: <where things stand, in 3–5 lines>
- Decisions: <what was decided, and why, in one line each>
- Open points: <what is unresolved>
- Files touched: <paths, and what changed in each>
- Next step: <the exact first action of the next conversation>
- Learned:               (P2)
- Weak spots:            (P2)
- AI use:                (P2)
- → Mère:                (P2; the proposals also go to inbox/)
- KB residue:            (P2)
```

- "Next step" is precise enough to start without asking, for example
  "P1.3: ft_memmove; Eliott has the N1 contract; start from his first
  attempt".
- Write with Eliott's OK. With no write tool, print the file and its path
  (P2).

## 4. Starting from a handoff

The next conversation uses the tag, reads the handoff, and quotes it in
the handshake ("Lu : … handoff P1.2"). Then it starts from "Next step".

— p5-handoff.md v1.0 · seal: tansy-06 —
