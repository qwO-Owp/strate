<!--
Strate template — concept course (P6, Professeur).
Copy below the line into `courses/<concept>.md` (kebab-case English).
Keep it under about 30 KB: split a concept that grows beyond. Delete
this comment and every <placeholder>. Templates carry no seal.

Rules: every claim typed [standard] [implementation] [UB] [42 rule]
[advice]; every fact anchored; every code block marked `tested
(<compiler>, <date>)` only if it really ran in this conversation,
otherwise `not tested`. No example, twin or check-yourself answer
implements a function a graded project not yet validated must turn in.
-->
---

# <Title>

- **Status:** draft | in review | approved (Examinateur, <YYYY-MM-DD>)
- **Page:** <private page link, once published>
- **Prerequisites:** <`courses/...`, the courses it stands on>
- **Calibrated on:** baseline <YYYY-MM-DD>. <domain> = <level>.

## 1. Why it matters

<what this is for, and where it comes back on the road>

## 2. The model

<the mental model in plain words, one physical, mechanical or
architectural analogy, and the key figure>

```
<ASCII sketch of the figure, with its caption; the page draws it properly>
```

## 3. The details

<the precise rules, each typed and anchored, e.g. "… [standard] (N1570
§6.5.6)">

## 4. Code, run

```c
<example>
```
`tested (<compiler>, <YYYY-MM-DD>)`

Output:
```
<real output>
```

## 5. Twins

<the same mechanism on another task, small enough for Python Tutor
(pythontutor.com, C mode). What to watch while stepping.>

## 6. Traps

<undefined behaviour, classic errors, how they show up>

## 7. Check yourself

1. <question>

<answers at the very end of the course>

## 8. Anchors

- `man 3 <…>` · N1570 §<…> · <Norm / subject / 42 doc>

## 9. KB candidates

One block per candidate, in the shape below (TBD-5, closed 2026-10-01).
Strate proposes; Eliott edits and files it in the vault. Strate never
writes into the KB, and never fills `id`, `created`, `domains`,
`sources` or `claim_status` — those are the KB's own.

```
- **<title: a complete assertion, in English — "A static local variable
  keeps its value between calls", not "static variables". If it cannot
  be written as an assertion, split it.>**
  - <3–8 lines, in Eliott's words where possible, not a lecture>
  - anchors: <a primary reference he can reopen: a man page section, an
    N1570 §, the Norm, a 42 doc, or file:line in his own code. No
    anchor, no note.>
  - relations: <supports | contradicts | refines | example-of> [[<note>]]
  - open: <what is still unresolved; "none">
```

## Review

<written by the Examinateur only>

## Answers to "Check yourself"

1. <…>
