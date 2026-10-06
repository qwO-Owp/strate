# P1 — Project cycle

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Every graded project runs the same cycle:
>
> 0. recon;
> 0b. diagnostic, when due;
> 1. courses;
> 2. atlas and its review;
> 3. tutoring, one step per conversation;
> 4. checklist and defense simulation;
> 5. turn-in;
> 6. close.
>
> Four gates are never skipped. Roles run in separate conversations, and
> steps that do not depend on each other run in parallel.

- **Used by:** every role that touches a graded project.

## 1. The cycle

| Step | Role and tag | Output | Needs |
|---|---|---|---|
| 0 | Éclaireur `[recon:<p>]` | `projects/<p>/recon.md` (rules card inside); proposed "Now" update of `cursus_progress` | the subject |
| 0b | Examinateur `[eval:baseline]` | proposed `living/baseline.md` (P7) | first project, or baseline stale |
| 1 | Professeur `[prof:<concept>]` | `courses/<concept>.md` + page (P6) | recon's course list, re-filtered after 0b |
| 2 | Professeur `[prof:<p>-atlas]` | `projects/<p>/atlas.md`, `atlas-<part>.md` (P6) | recon |
| 2r | Examinateur `[eval:courses]` | status `approved`, or a Review block | a draft in review |
| 3 | Tuteur `[graded:<p>] <step>` | `projects/<p>/handoff-<step>.md` (P5) | an **approved** atlas part |
| 4 | Examinateur `[eval:<p>]` | `projects/<p>/eval-<n>.md` | all steps done, README written |
| 5 | Navigateur `[nav] turn-in <p>` | project declared finished | checklist passed on the commit that is the Vogsphere head |
| 6 | Éclaireur `[recon:<p>] close` | state updates (see §4) | the intranet result |

Eliott registers on the intranet whenever he wants before step 3.
Registering creates the Vogsphere repo he clones and works in.

**The project slug `<p>`** is the project's name **as the intranet writes
it**, lowercased, with spaces and hyphens as underscores:

| Intranet | Slug |
|---|---|
| Libft | `libft` |
| push_swap | `push_swap` |
| get_next_line | `get_next_line` |
| Born2beroot | `born2beroot` |

Every role uses the same slug, in its tag and for `projects/<p>/`, so two
conversations never create two directories and a later gather step never
comes back empty. **Not** the subject PDF's filename: `GetNextLine.pdf`
would give `getnextline`, which is not the project's name. Decided
2026-10-02.

## 2. The gates

1. **No step 3 without an approved atlas part.** A draft atlas never
   drives tutoring.
2. **No turn-in without the checklist passed on the exact commit**, run in
   a fresh clone from Vogsphere, with its hash recorded.
3. **No unlock without Eliott's statement that the project is validated.**
4. **No close without the project's handoffs and evals.**

## 3. How the steps work

**Step 3, tutoring.**
- One conversation per atlas step (`P<part>.<n>`). Each starts from the
  previous handoff.
- Eliott's code lives on his machines. The Tuteur sees only what he pastes
  or attaches, and never assumes it sees the repo.
- The Tuteur may compile and run Eliott's own pasted code, with his own
  `main` and inputs, to show him what happens. The fix stays his. At
  stage 1, the Tuteur writes no test harness for him.
- The last step gathers the AI-use lines (the recon, the handoffs, the
  evals and the Review blocks of the project's atlas files) and asks
  about any `[learn]` use. Eliott then writes the README, its AI-use
  section included, before step 4.

**Step 4, verification.** The checklist, then one defense simulation or
more. Failures go back to step 3.

**Step 5, the 42 turn-in,** as Eliott practises it (a subject can say
otherwise). He pushes as he works, so the checked commit is already on
Vogsphere.
1. Nothing is left unpushed, and there has been no push since the check.
2. The Vogsphere head (`git ls-remote origin`) equals the checked hash.
3. Eliott declares the project finished on the intranet.
4. He books two peer defenses, at two different times.
5. The Moulinette mark arrives after the peers accept.

## 4. Close, or not

**Validated.** The Éclaireur proposes, for Eliott's OK:
1. the `cursus_progress` update: date, mark, weak spots, unlocked
   references, thread position (what he built), and the next "Now";
2. the baseline change;
3. the layer's design, refined in `thread_map` (no personal progress
   there);
4. the KB residue, moved into `living/kb_candidates.md`;
5. then the pruning of the project's handoffs and evals.

**Failed** (a defense or the Moulinette). It is not a close:
- record the mark and the weak spots;
- prune nothing;
- return to step 3 or 4 with the latest `eval-<n>.md`.

A retry may come with a new Vogsphere repo and a waiting time: to verify
at the first retry. The Navigateur checks the repo URL again.

## 5. Speed without shortcuts

The Pace deadline is real, so the recon proposes a **minimal path**:
- courses only for the domains the baseline marks zero or shaky;
- the general atlas and the first part first;
- one batched review;
- the date tutoring starts.

**Parallel conversations.** The Professeur writes the next atlas part
while the Tuteur works on the current one, and the Examinateur reviews in
batches. Only the gates are sequential.

## 6. Pair projects

The rule for pair projects is provisional (TBD-1):
- one shared repo, and a branch and a pull request for every change;
- Strate helps on Eliott's parts and on the shared design, never on a
  teammate's part;
- Eliott is prepared to defend all the code.

It is finalised after push_swap.

— p1-project-cycle.md v1.0 · seal: dowel-93 —
