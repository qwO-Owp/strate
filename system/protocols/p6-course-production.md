# P6 — Course and atlas production

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Courses and atlases are written in English.
> - They are produced from a plan Eliott validates, section by section.
> - Every code example is really run, every fact anchored, every claim
>   typed.
> - The Examinateur reviews them before they are `approved`, in one
>   trip: it corrects them within its edit scope (§3) and settles the
>   file, or sends it back.
> - They are delivered as a private page plus a downloaded HTML file. The
>   markdown source lives in Project Knowledge.
>
> No example or twin reproduces a file (a function, a Makefile, a
> header) that a graded project not yet validated must turn in. An atlas
> stays below N2 (§4), and an atlas is never shared (Article 9).

- **Used by:** the Professeur (to produce), the Examinateur (to review).

## 1. The flow

1. **Plan.** Propose the outline: sections, figures, examples, twins. Also
   say what the baseline lets you skip. Eliott validates it.
2. **Sections.** Write them over several turns, one or two at a time.
   Never one giant output: token limits cut depth. Each round goes to
   Eliott as a file, not printed in the chat, and is written to the
   Project from that file after his go.
3. **Run and anchor** as you go (§3).
4. **Assemble** the markdown source, with status `draft`, and write it
   with OK.
5. **Review** (P1 step 2r), in one trip. Set the status to `in review`.
   The Examinateur reviews the whole source, corrects it within its edit
   scope (§3), and writes it as `approved`, its edits listed in the
   Review block. When a fix lies outside that scope, the verdict is
   `changes needed`: the source goes back to the Professeur with a Review
   block of numbered findings.
6. **Render and deliver** (§5), in a new Professeur conversation that
   first checks the Examinateur's edits.

## 2. Files and structure

**Names:**
- courses: `courses/<concept>.md`, in kebab-case English, for example
  `courses/pointers-and-arrays.md`;
- atlases: `projects/<p>/atlas.md` (general), then `atlas-<part>.md`, for
  example `atlas-p1.md` or `atlas-bonus.md`.

**Size.** About 30 KB is the guide for one composition turn (§1, step 2),
not for a file: one file per concept, and one per part atlas, wins over
the size. The review notes a source's size; splitting a large one waits
for the consolidation pass (N12).

**Every source starts with:**

```
# <Title>
- Status: draft | in review | approved (Examinateur, <YYYY-MM-DD>[; <n> edits by the Examinateur])
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

**A part atlas** (atlas v2, from 1.0-rc.3; `system/templates/atlas.md`,
Part B). It is the bridge between the courses and each function:
- **for each step:**
  - what its functions share, and what is new;
  - a **mechanism map:** each mechanism, the course section that teaches
    it, and where it shows up in this step;
  - a **twin** for each new mechanism, given in full and walked line by
    line, unless a course already shows it as this step uses it;
- **for each function or exercise:**
  - the contract **in plain words**, with a figure when it helps;
  - the **N1 contract:** prototype, parameters, return value, edge cases,
    man reference, allowed functions;
  - **examples:** inputs and expected outputs, some left to derive, their
    answers in a fold;
  - the **decisions** Eliott will make, as questions grouped by theme;
  - **his library:** a shortlist of his own functions, decoys included;
  - **cost,** as a question;
  - **traps, as questions;**
  - a **test plan,** inputs grouped from normal to undefined;
  - the questions an evaluator may ask.
- **The noise rule.** The body keeps what changes what Eliott does on the
  cluster. How a fact was established (compiler versions, dates, runs),
  and details that change nothing for him, go to the notes for the
  review.
- **Size:** one step per composition turn.

**Both atlas files** end with **Notes for the review (author)**, before
the Review block: the anchors opened in the session and those cited from
knowledge; what was run, with the machine, the versions and the date;
what the noise rule moved out of the body; the integrity points the
reviewer should check, the twins first.

## 3. The three locks and claim typing

- **Run.**
  - Compile every example with `cc -Wall -Wextra -Werror`, adding
    `-g -fsanitize=address` when memory is involved.
  - Run it and paste the real output.
  - Every variant the text asks the reader to make ("Try", "add this
    line", "remove this") is compiled and run exactly as worded, and its
    result is the one the text states.
  - Mark each block `tested (<compiler>, <YYYY-MM-DD>)` only if it
    actually ran in this conversation; otherwise `not tested`.
  - The cluster's `cc` is clang; if the behaviour depends on the
    compiler, say so.
- **Anchor.**
  - Man pages as `man 3 memmove`.
  - The standard as C11 (the N1570 draft), for example "N1570 §7.24.2.2".
    A `[standard]` claim cites a normative paragraph. Footnotes, notes
    and EXAMPLEs are informative (N1570 Foreword p8): they may stand
    beside a normative paragraph, never alone.
  - Also the Norm, the subject, 42 documents.
- **Review:** by the Examinateur only (§1, step 5), in one trip.
  - The reviewer opens every anchor for real: `man` in the workspace
    (installed per `tools.md` §1), otherwise man7.org; N1570 from the
    Project's `n1570.pdf`, whose `project_read` writes its full text to
    the workspace (the web copies stop early or refuse).
  - An anchor it could not open is marked `anchor unchecked`. That
    blocks `approved`.
  - **The edit scope.** The Examinateur corrects the source itself when
    the fix corrects what is already there:
    - a wording, a claim type, an anchor, an overstatement, a missing
      caveat or condition;
    - a stated output, re-run;
    - an existing code block or variant that does not do what the text
      says: the smallest edit that makes it so, re-run;
    - a sentence moved or split for clarity.

    Every edit is verified in the session: each anchor it names opened,
    each output it states run.
  - **Outside the scope,** the verdict is `changes needed`, and the
    source goes back to the Professeur:
    - a new section, example, twin, figure or check-yourself question;
    - an explanation or a model that must be rethought, not corrected;
    - a calibration that misses the baseline;
    - any integrity finding: what replaces an example too close to a
      deliverable is the Professeur's design, never the reviewer's.
  - **The write.** The Examinateur shows Eliott the verdict and the list
    of edits. With his go, it applies them (each current text found once,
    outside the Review block), re-runs what they touch, and writes the
    source once:
    - status `approved (Examinateur, <date>; <n> edits by the
      Examinateur)`;
    - the Review block lists every edit, with its current and new text,
      and records the source's size before the edits.
  - **The second eye.** The Professeur's render session checks every
    listed edit before it renders (§5). Every change is seen by a role
    that did not make it.
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
  - When the concept lives between files or tools (compiler stages, `.o`
    files, archives, links, `make`), the twin is a **terminal lab**: a few
    files and the commands to run on them, with their real output.
  - If renaming or retyping it gives a deliverable file, it is not a twin.
- **Integrity:**
  - no example, twin or check-yourself answer reproduces a file a graded
    project not yet validated must turn in: a function, and equally its
    Makefile or its header;
  - a twin of such a file has another shape (another graph, other kinds
    of files, another job), not the same file under other names, and no
    combination of a course's examples, its twins and the courses it
    stands on adds up to the deliverable. The review checks the
    combination;
  - when Eliott's own validated work already holds such a file (a
    Reloaded Makefile), the atlas sends him there;
  - no pseudocode of the deliverable;
  - **an atlas stays below N2.** It gives the contract and everything
    around it (§2), never the steps:
    - no code and no pseudocode of a deliverable function;
    - no answer to its decision questions;
    - no decision questions in the order the code runs, nor one per line
      of the function;
    - a shortlist never says which of its candidates fit;
  - **an atlas twin** works on another task, with another contract. It is
    not a twin if renaming, retyping, or changing its stop condition, its
    return value or a single line gives a deliverable function. The
    review checks each step as a whole: its twin, its examples and its
    decision questions together never add up to a function.

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
- **Before rendering,** the Professeur checks the Examinateur's edits
  (§3): each one in place as the Review block writes it, and nothing else
  changed (applied in reverse, the edits give back the source's size
  before them). An edit it disagrees with goes to Eliott, and the render
  waits for his call.
- **The render check** comes before the "Page" line is filled, and its
  result is reported to Eliott:
  1. the local file: its text, drawings and controls aside, equals the
     source as rendered by an independent markdown parser; code blocks
     are byte-identical; each drawing's words equal its sketch's;
  2. the page as served, read back after publishing;
  3. the live page, in a browser, when the session has one; otherwise
     the report says "not checked live".
- **An atlas is never shared.** A course stays private unless Eliott
  decides otherwise.
- The "Page" line is metadata: updating it after approval needs no new
  review.

**The file.** Also send the HTML file, which Eliott archives: a folder on
the cluster for now, the KB's `outputs/` later.

**Storage.** Only the markdown source goes into Project Knowledge. The
HTML never does.

— p6-course-production.md v1.0 · seal: purlin-47 —
