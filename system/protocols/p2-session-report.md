# P2 — Session report

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Every conversation ends with a report in a fixed format.
> It is written where the next reader will look for it, one file per
> report, never into a shared file, and always with Eliott's OK. With no
> write tool, print the full file with its path. Never claim a write that
> no tool result confirms.

- **Used by:** every role.

## 1. The format

```
## Report — <role> · <object> · <YYYY-MM-DD>
- Done:
- Learned:
- Weak spots:
- AI use: <what AI was used for in this session; "none" if none>
- Decisions:
- Next step:
- → Mère: <proposals, numbered; "none" if none>
- KB residue: <assertion-shaped ideas, with their anchor; "none" if none>
```

- Every line is present; write "none" rather than dropping a line.
- Keep it short. The next reader has a phone screen too.
- **KB residue** follows the candidate shape of
  `system/templates/course.md` §9: a title that is a complete assertion,
  a few lines in Eliott's words, its anchors.

## 2. Where it goes

| Session | The report goes to | Read by |
|---|---|---|
| Tuteur, one atlas step | `projects/<p>/handoff-<step>.md` (the handoff, P5) | the next step; the close |
| Examinateur, on a project | `projects/<p>/eval-<n>.md` | the close; the Tuteur on a failure |
| Éclaireur, open | inside `projects/<p>/recon.md` | every project role |
| Éclaireur, close | the proposed state updates | Eliott |
| Professeur | its "KB residue" goes to the course's "KB candidates" section | the KB, later |
| Professeur, a course spanning conversations | `courses/<concept>-handoff.md` (P5), deleted once the course is approved | the next Professeur session |
| Examinateur, diagnostic | the proposed `living/baseline.md` (P7) | every role |
| Examinateur, review | the Review block at the end of the source (P6) | the Professeur |
| Éclaireur, research for a project | `projects/<p>/research-<topic>.md` | the role that asked |
| Bâtisseur | `builds/<object>/handoff-<n>.md` | the next session |
| Navigateur | machine changes go to `living/environment.md`; frictions to `living/friction_log.md` | the Navigateur |
| **any role with a proposal** | a new file `inbox/<YYYY-MM-DD>-<role>-<object>.md` | the Mère |
| Mère | its `decisions_log` entry; its handoff goes to `living/mother_handoff.md` | the next Mother |

`<role>` is the role's slug (`tuteur`, `eclaireur`, `professeur`…). A
tagged session with **no role doc** uses its tag instead: `[audit]`
writes `inbox/<YYYY-MM-DD>-audit-<object>.md`.

`<p>` is the project slug of P1 §1 (the intranet name, lowercased,
underscores), the same in every conversation.

Anything else stays in the chat: a `[learn]` answer, research not tied
to a project, or a session with nothing to hand over. If another role
will need it, it goes into that role's next handoff.

## 3. Writing it

1. Show the report in the chat, then ask for the OK to write it.
2. Re-read the target file right before writing, if it exists.
3. Write, and confirm with the tool result.
4. **No write tool:** print the full file and its exact path, and let
   Eliott paste it. Proposals for the Mère can be pasted straight into
   the Mother conversation.

**Inbox files:**
- one per session;
- they hold only the proposals, each with what, why and the evidence;
- the Mère deletes them once triaged (P3).

## 4. Deletion

| File | Deleted |
|---|---|
| inbox files | after the Mère's triage |
| handoffs and evals | at the project's close, after the KB residue has moved to `living/kb_candidates.md` |
| build handoffs | when the build ends, after its lessons are recorded |

— p2-session-report.md v1.0 · seal: plinth-29 —
