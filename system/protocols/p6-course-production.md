# P6 — Course and atlas production

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Courses and atlases are written in English.
> - They are produced from a plan Eliott validates, section by section.
> - Every code example is really run, every fact anchored, every claim
>   typed.
> - The Examinateur reviews them before they are `approved`.
> - They are delivered as a private page plus a downloaded HTML file. The
>   markdown source lives in Project Knowledge.
>
> No example or twin implements a function that a graded project not yet
> validated must turn in. An atlas stays at N1, and an atlas is never
> shared (Article 9).

- **Used by:** the Professeur (to produce), the Examinateur (to review).

## 1. The flow

1. **Plan.** Propose the outline: sections, figures, examples, twins. Also
   say what the baseline lets you skip. Eliott validates it.
2. **Sections.** Write them over several turns, one or two at a time.
   Never one giant output: token limits cut depth.
3. **Run and anchor** as you go (§3).
4. **Assemble** the markdown source, with status `draft`, and write it
   with OK.
5. **Review** (P1 step 2r). Set the status to `in review`. The Examinateur
   returns `approved`, or a Review block with numbered findings.
6. **Render and deliver** (§5).

## 2. Files and structure

**Names:**
- courses: `courses/<concept>.md`, in kebab-case English, for example
  `courses/pointers-and-arrays.md`;
- atlases: `projects/<p>/atlas.md` (general), then `atlas-<part>.md`, for
  example `atlas-p1.md` or `atlas-bonus.md`.

Keep a source under about 30 KB: split a concept that grows beyond.

**Every source starts with:**

```
# <Title>
- Status: draft | in review | approved (Examinateur, <YYYY-MM-DD>)
- Page: <private page link, once published>
- Prerequisites: <courses/... it stands on>
- Calibrated on: baseline <YYYY-MM-DD> · <domain> = <level>
```

**A course, in order:**
1. **Why it matters:** what it is for, and where it comes back on the
   road.
2. **The model:** the mental model, one analogy, the key figure.
3. **The details:** claims typed and anchored.
4. **Code, run:** examples with their real output.
5. **Twins:** with Python Tutor instructions.
6. **Traps:** undefined behaviour, classic errors.
7. **Check yourself:** questions, with answers at the end.
8. **Anchors:** the man pages and standard clauses used.
9. **KB candidates.**
10. **Review:** written by the Examinateur.

**The general atlas:**
- the project's place on the road, and a pointer to the rules card;
- the shape of the deliverable: files, library, Makefile rules and flags,
  as contracts;
- the numbered steps `P<part>.<n>`, each sized for one tutoring
  conversation (roughly three to six functions), with their order and
  dependencies;
- the testing plan (his own tests first);
- the README plan: the sections the subject requires;
- the evaluator's likely questions.

**A part atlas,** for each function or exercise:
- the **N1 contract:** prototype, parameters, return value, edge cases,
  man reference, allowed functions;
- what is new in it;
- **pitfalls, as questions;**
- **test ideas, as inputs to try;**
- an evaluator question.

## 3. The three locks and claim typing

- **Run.**
  - Compile every example with `cc -Wall -Wextra -Werror`, adding
    `-g -fsanitize=address` when memory is involved.
  - Run it and paste the real output.
  - Mark each block `tested (<compiler>, <YYYY-MM-DD>)` only if it
    actually ran in this conversation; otherwise `not tested`.
  - The cluster's `cc` is clang; if the behaviour depends on the
    compiler, say so.
- **Anchor.**
  - Man pages as `man 3 memmove`.
  - The standard as C11 (the N1570 draft), for example "N1570 §7.24.2.2".
  - Also the Norm, the subject, 42 documents.
- **Review:** by the Examinateur only (§1, step 5).
  - The reviewer opens every anchor for real: the workspace `man` when
    installed, otherwise the web (man7.org, open-std.org for N1570).
  - An anchor it could not open is marked `anchor unchecked`. That
    blocks `approved`.
- **Claim types,** put in brackets after the claim: `[standard]`,
  `[implementation]`, `[UB]`, `[42 rule]`, `[advice]`.

## 4. Pedagogy rules

- **Calibrate on the baseline:** skip what is solid, start from the base
  where it is zero.
- **Figures.** Each figure must earn its place: memory and stack layouts,
  arrays, pointer arrows, execution tables. The source keeps each figure
  as a short ASCII sketch with its caption; the page draws it properly.
- **Twins.**
  - A twin is the same mechanism on another task and other data, small
    enough for Python Tutor (pythontutor.com, C mode).
  - If renaming or retyping it gives a deliverable function, it is not a
    twin.
- **Integrity:**
  - no example, twin or check-yourself answer implements a function a
    graded project not yet validated must turn in;
  - no pseudocode of the deliverable;
  - an atlas never goes beyond N1.

## 5. Delivery: page and file

**The private page.** Build the page as a self-contained HTML artifact.
When the session offers the `artifact-design` and `artifact-diagramming`
skills, load them first. Publish the page and record its link in the
source's "Page" line.
- It is private by default: only Eliott opens it, on any of his devices.
- Updating means republishing to the same link. From another
  conversation, read the page first.
- The **final page is rendered from the approved source.** An earlier
  page carries a visible DRAFT banner.
- **An atlas is never shared.** A course stays private unless Eliott
  decides otherwise.
- The "Page" line is metadata: updating it after approval needs no new
  review.

**The file.** Also send the HTML file, which Eliott archives: a folder on
the cluster for now, the KB's `outputs/` later.

**Storage.** Only the markdown source goes into Project Knowledge. The
HTML never does.

— p6-course-production.md v1.0 · seal: gimlet-45 —
