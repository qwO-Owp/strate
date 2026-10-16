<!--
Strate template — atlases (P6, Professeur). Atlas v2, from 1.0-rc.3.
Part A becomes `projects/<p>/atlas.md` (the general atlas). Part B
becomes `projects/<p>/atlas-<part>.md`, one file per part. Delete this
comment and every <placeholder>. Templates carry no seal.

The line (P6 §4): an atlas gives everything below N2, the contract and
all that surrounds it, and never the steps of a deliverable function.
- No code and no pseudocode of a deliverable function.
- Twins work on another task, with another contract. Renaming, retyping,
  or changing a twin's stop condition, its return value or one line
  must never give a deliverable function.
- Decision questions are grouped by theme, never in the order the code
  runs, never one per line of the function, and never answered.
- A shortlist of Eliott's functions holds decoys and never says which
  candidates fit.
- Pitfalls are questions.
- Each step as a whole: its twin, its examples and its decision questions
  together never add up to a function. The review checks this.

The noise rule (P6 §2): the body keeps what changes what Eliott does on
the cluster. How a fact was established (compiler versions, dates, runs)
and details that change nothing for him go to the notes for the review.
Size: one step per composition turn.
-->

# PART A — general atlas

# Atlas — <project>

- **Status:** draft | in review | approved (Examinateur, <YYYY-MM-DD>[; <n> edits by the Examinateur])
- **Page:** <private page link, once published>
- **Rules card:** `projects/<p>/recon.md` §2
- **Prerequisites:** <`courses/...`>
- **Calibrated on:** baseline <YYYY-MM-DD>. <domain> = <level>.

## 1. The project on the road

<what it is for, what it builds on, where it leads; 5 lines at most>

## 2. The deliverable, as contracts

<files, library, header, Makefile rules and flags: what each must do and
guarantee, never how>

## 3. Steps

| Step | Functions / exercises | Depends on | Part atlas |
|---|---|---|---|
| P1.1 | <3–6 items> | — | `atlas-p1.md` |
| P1.2 | <…> | P1.1 | `atlas-p1.md` |

<a figure: which course opens which steps>

## 4. Testing plan

<his own tests first: what to test and how to organise it; testers only
after>

## 5. README plan

<the sections the subject requires and what each must cover, as a
contract. Eliott writes the text.>

## 6. What evaluators ask

- <question?>

## Notes for the review (author)

<written by the Professeur: the anchors opened and those cited from
knowledge; what was run, with machine, versions and date; the integrity
points the reviewer should check>

## Review

<written by the Examinateur only>

---

# PART B — part atlas

# Atlas — <project>, <part>

- **Status:** draft | in review | approved (Examinateur, <YYYY-MM-DD>[; <n> edits by the Examinateur])
- **Page:** <link>
- **Prerequisites:** <`courses/...`, with the sections each step uses>
- **Calibrated on:** baseline <YYYY-MM-DD>. <domain> = <level>.

**How to use this atlas.** For each step: read the mechanism map, then
step through the twin in Python Tutor until every line makes sense. Then,
for each function: the contract, the examples (derive the `?` before you
open the fold), the decisions, and only then your code. Test it with the
plan, then answer the defense questions aloud. Stuck after a real try:
`[graded:<p>] <step>`.

## P<part>.<n> — <step title>

### At a glance

<what the step's functions share, and what is new in it, in 3–5 lines;
one figure when it helps>

### Mechanism map

| Mechanism | Taught in | Where it shows up in this step |
|---|---|---|
| <e.g. a block the caller must free> | <`courses/<…>.md` §<…>> | <which function, which parameter or result; never how the step uses it> |

### Twin — <its task, in a few words>

<one twin per new mechanism of the step, shared by its functions. None
when a course already shows the mechanism as this step uses it: point to
that course section instead.>

- **Its task and its contract:** <a different task, with a contract no
  deliverable has>
- **The code:** a complete program, short enough for Python Tutor.

```c
<the twin>
```
`tested (<compiler>, <YYYY-MM-DD>)`

Output:
```
<real output>
```

- **Line by line:**

| Line | What it does | Its type, and why | Why this way |
|---|---|---|---|
| <n> | <…> | <…> | <…> |

- **In Python Tutor:** <what to watch, step by step: which arrow moves,
  which value changes, when a block appears or disappears>
- **What transfers, what does not:** <questions on the differences
  between the twin and this step's functions; never their answers>

### `<function>` (step P<part>.<n>)

- **In plain words:** <2–4 sentences: what goes in, what comes out, what
  it changes, who owns the result. A figure of the inputs and of the
  result when it helps.>
- **N1 contract**
  - **Prototype:** `<…>`
  - **Parameters:** <each one: its type, what it means, what the function
    may do with it>
  - **Returns:** <…>
  - **Edge cases:** <…>
  - **Reference:** `man 3 <…>`, or the subject, p. <…>. **Allowed
    functions:** <…>.
- **Examples:**

| Input | Expected | Which line of the contract |
|---|---|---|
| <…> | <…> | <…> |
| <…> | ? | derive it |

<details><summary>Answers: derive them first</summary>

<the expected value of each `?` row, and where it comes from: the
contract, or the reference libc as run (machine and date in the notes
for the review)>

</details>

- **Decisions you will make** (questions, grouped by theme):
  - **Types:** <which values does your function hold, and which type does
    each need?>
  - **Bounds:** <where may it read and write, and what stops it?>
  - **Failure:** <what can fail, and what must reach the caller then?>
  - **Ownership:** <who frees what, and when?> (allocating functions)
  - **Return:** <what comes back in each case?>
- **Your library:** <a shortlist of Eliott's own functions, decoys
  included. Which fit, and what does each cost here?>
- **Cost:** <how many passes over the data does your version make? Could
  it make fewer, and is that worth it here?>
- **Traps (as questions):** <the ones that change what he writes or
  tests; a compiler or libc detail only when it changes what happens on
  the cluster>
- **Test plan:**
  - normal: <…>
  - boundaries: <…>
  - edges of the contract: <…>
  - undefined, kept out of the automated run: <…>
- **At the defense:** <2–3 questions an evaluator may ask>

<repeat for every function of the step, then for every step of the part>

## Notes for the review (author)

<the anchors opened and those cited from knowledge; what was run, with
machine, versions and date; what the noise rule moved out of the body;
the integrity points the reviewer should check, each twin first>

## Review

<written by the Examinateur only>
