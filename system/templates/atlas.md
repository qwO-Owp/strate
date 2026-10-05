<!--
Strate template — atlases (P6, Professeur).
Part A becomes `projects/<p>/atlas.md` (the general atlas). Part B
becomes `projects/<p>/atlas-<part>.md`, one file per part. Delete this
comment and every <placeholder>. An atlas stays at N1: no code and no
pseudocode of the deliverable, and pitfalls are written as questions.
Templates carry no seal.
-->

# PART A — general atlas

# Atlas — <project>

- **Status:** draft | in review | approved (Examinateur, <YYYY-MM-DD>)
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

## 4. Testing plan

<his own tests first: what to test and how to organise it; testers only
after>

## 5. README plan

<the sections the subject requires and what each must cover, as a
contract. Eliott writes the text.>

## 6. What evaluators ask

- <question?>

## Review

<written by the Examinateur only>

---

# PART B — part atlas

# Atlas — <project>, <part>

- **Status:** draft | in review | approved (Examinateur, <YYYY-MM-DD>)
- **Page:** <link>
- **Prerequisites:** <`courses/...`>
- **Calibrated on:** baseline <YYYY-MM-DD>. <domain> = <level>.

## <function or exercise> (step P<part>.<n>)

- **N1 contract**
  - Prototype: `<…>`
  - Parameters: <…>
  - Returns: <…>
  - Edge cases: <…>
  - Reference: `man 3 <…>`. Allowed functions: <…>.
- **What is new here:** <…>
- **Pitfalls (as questions):** <…?>
- **Test ideas (inputs to try):** <…>
- **An evaluator may ask:** <…?>

<repeat for every function of the part>

## Review

<written by the Examinateur only>
