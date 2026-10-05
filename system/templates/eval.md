<!--
Strate template — eval file (Examinateur, on a project).
Copy below the line into `projects/<p>/eval-<n>.md` (n = 1, 2, 3…).
Eliott runs every command and pastes the output. Put the subject's own
requirements first; the rows below are the generic fallback (commands in
`system/tools.md`). Delete this comment. Templates carry no seal.
-->
---

# Eval <n> — <project> · <YYYY-MM-DD>

- **Commit checked:** `<hash>`, from a fresh clone from Vogsphere
- **Machine:** cluster · `cc` <version> · norminette <version>
- **Parts run:** checklist / defense simulation / quiz

## Checklist

| Check | How | Result |
|---|---|---|
| Subject requirements | <from the rules card> | <…> |
| Norm | `norminette` on every file | <…> |
| Makefile rules | `make`, `make clean`, `make fclean`, `make re` | <…> |
| No relink | `make` twice | <…> |
| Flags | `-Wall -Wextra -Werror` | <…> |
| Forbidden functions | `nm -u` vs. the allowed list | <…> |
| Files | `git ls-files`: exact set, right place | <…> |
| Globals, guards, `static` | read the sources | <…> |
| Memory | valgrind or ASan on his tests | <…> |
| Edge cases | his tests, then testers | <…> |
| README | required sections; AI use vs. the recon, handoff and eval lines | <…> |

**Verdict:** pass / fail. <What to fix, numbered.>

## Defense simulation

- **Score:** <…>
- **Weak points:** <…>
- **Debrief:** <…>

## Quiz / explain-back

<questions, his answers in short, what was solid or shaky>

## Proposed baseline change

<domain: before → after, and why>

## Next step

<turn-in / back to the Tuteur on <…> / back to the Professeur on <…>>

## Learned

<…, or "none">

## Decisions

<…, or "none">

## AI use of this session

<one line>

## KB residue

<…, or "none">

## → Mère

<proposals, also written to `inbox/` (P2); or "none">
