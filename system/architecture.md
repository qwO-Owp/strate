# Strate — architecture (v1.0, C1)

The reference description of how Strate is built and how it works. The
core instructions, the role docs, the protocols and the templates all
implement this document. When they disagree with it, this document wins
until the Mother changes it.

- **Status:** v1.0, C1 approved by Eliott on 2026-09-30; amended in C2a
  (pre-release) after an independent review of the role docs, in C3c
  (2026-10-02) once the core went live, and in E (2026-10-06) after the
  first public commit. It freezes the structure. C2 writes the detailed
  roles, protocols and templates; C3 composes the core instructions.
- **Sources:** decisions_log (sessions 1–3), open_questions (B5), Eliott's
  answers to the C1 questions (2026-09-29/30), the KB's own architecture
  (`KB_ARCHITECTURE.md`, `SETUP-PROJET.md`, `GABARITS.md`).

---

## 1. What Strate is, in one paragraph

Strate is a system of specialised conversations inside one Claude Project.
They share a short core of rules and a set of documents. Each conversation
plays **one role** on **one mission**. It reads the state it needs from the
documents and leaves a **report** at the end. The Mother conversation
turns those reports into improvements of the system. The goal: every
project Eliott does, and everything he builds in Univers42, becomes a layer
the next one stands on, and the system itself gets better every week.

## 2. Architectural principles

These derive from the spine and from lessons already paid for (Reloaded,
the KB). When a design choice is unclear, decide with them.

1. **Short core, detail on demand.** The instructions field is re-read on
   every message of every conversation, so every useless sentence costs
   everywhere. The core holds only what every conversation needs: identity,
   spine, integrity, the router and the handshake. Everything else lives in
   `system/` documents that a role reads when it starts.
2. **One conversation = one role = one mission.** No conversation tries to
   be tutor, professor and examiner at once. That was Reloaded's problem.
3. **Shared state lives only in documents.** Conversations do not see each
   other and nothing runs in the background. If it is not in a document,
   the rest of the system does not know it.
4. **Every conversation ends with a report.** It is written to a file
   wherever another conversation will need it (P2). The loop (report →
   inbox → Mother → improvement) is what makes the system self-feeding.
   Without reports, Strate freezes.
5. **Nothing is written without Eliott's OK.** The architecture changes
   only in the Mother conversation.
6. **Calibrated to Eliott, not to an average student.** Every role reads
   the baseline before explaining anything.
7. **Production and verification are separated.** The role that writes a
   course or a piece of code never grades it.
8. **Just in time, but always from the base.** Content is produced in the
   order projects need it. Each piece starts from the concepts beneath it
   and never skips a layer.
9. **See the whole road.** The filter of the coached surface withholds only
   solutions and not-yet-unlocked reference implementations, never the
   knowledge of where a thread leads. (This replaces the stricter session-2
   filter, which avoided naming future projects.)
10. **Private by default.** Only what is safe goes public: no 42
    pedagogical material (Article 9), nothing personal.
11. **The brake.** Infrastructure work must serve real work. If the system
    is being refined while no project work has happened since the last
    change, the Mother asks what the change actually unblocks (KB §11).

## 3. The layers

```
L0  SPINE        spine + integrity rules            (core)
L1  ROUTER       tag → role, handshake, wellbeing   (core)
L2  ROLES        7 roles, one doc each              (system/roles/)
L3  PROTOCOLS    how roles chain and hand over      (system/protocols/)
L4  STATE        what is true now                   (living/)
L5  CONTENT      courses, atlases, recon dossiers   (courses/, projects/)
L6  REFERENCE    subjects, Norm, rules, 42 docs     (reference files)
SEAMS            KB · Univers42 · git repo · tools
```

- **L0–L1 are the core** (the Project's instruction field). Its target size
  is at most a third of v0.1's.
- **L2–L3 are the machine:** they change only through the Mother.
- **L4–L5 are the memory:** they change with use, always with Eliott's OK.
- **L6 is the ground truth:** it changes when 42 changes it.

## 4. The router (L1)

### 4.1 Tags

The first message of a conversation starts with a tag. The tag selects the
role; the subject after the colon names the mission's object.

| Tag | Role | Example |
|---|---|---|
| `[mother]` (also `[MÈRE]`, `[MERE]`, `[MOTHER]`) | Mère | `[mother] C2 roles` |
| `[recon:<project>]` | Éclaireur: open (step 0) | `[recon:libft]` |
| `[recon:<project>] close` | Éclaireur: close (step 6) | `[recon:libft] close` |
| `[recon:<topic>]` | Éclaireur: research on demand | `[recon:testers]` |
| `[prof:<subject>]` | Professeur | `[prof:pointers]`, `[prof:libft-atlas]` |
| `[graded:<project>] <step>` | Tuteur | `[graded:libft] P1.2` |
| `[eval:<subject>]` | Examinateur | `[eval:libft]`, `[eval:baseline]`, `[eval:courses]` |
| `[exam]` | Examinateur, exam-prep mode | `[exam]` |
| `[nav]` | Navigateur | `[nav] ssh keys` |
| `[build:<object>]` | Bâtisseur | `[build:site]`, `[build:discord]`, `[build:dotfiles]` |
| `[learn]` | Professeur, quick-answer mode | `[learn] what is size_t` |
| `[audit]` | no role: read-only audit (C3a) | `[audit] C5` |

- **No tag:** the conversation infers the role from the request and states
  it in its first line ("Rôle : Professeur, mode réponse rapide"). If it is
  unclear, it asks with one question.
- **`[audit]` has no role doc**, so its handshake carries **no role seal**.
  It states its mission, the documents it read with their seals, and that
  it is read-only. It writes nothing: its findings go to `inbox/` with
  Eliott's go. Used by C5.
- **WELLBEING overrides every role**, at any moment (exhaustion,
  discouragement, grinding): drop the format, talk straight, one small next
  step, point to real people.

### 4.2 Loading a role

1. **Primary:** the tag alone. The core tells the conversation to read
   `system/roles/<role>.md`, then `living/baseline.md`, then whatever the
   role doc lists, before answering.
2. **Fallback:** if a role behaves wrongly, Eliott pastes the role doc as
   the first message. This is the proven pattern of the KB
   (`SETUP-PROJET.md`: the platform has no automatic personas).
3. **Seal.** Every sealed doc (the architecture, the roles, the
   protocols, `tools.md`) ends with a line
   `— <file> v<x.y> · seal: <word-nn> —`. The seal appears nowhere else
   (templates and examples show `<seal>`), and it changes with every
   edit. The handshake quotes it, so a missing or wrong seal means the doc
   was not read to the end.
   - Templates and starters carry no seal: they get copied into working
     files, where a seal would leak and defeat the check.
   - To check a seal, Eliott needs the real list. The Mère gives it to him
     at each release, and he keeps it outside the Project (a note on his
     phone). It never goes in a file the roles read — `decisions_log`
     included, since a search in retrieval mode could surface a seal from
     it and let a role quote one it never read.
   - Protocol docs carry seals too. Each role doc lists the protocols it
     uses. The role reads them before the step that needs them, and
     quotes their seals in the "Lu" line.
   - This matters because the Project is already in retrieval mode
     (verified at C1): a conversation that only searches the documents
     gets fragments instead of whole files. Role docs stay short and put
     their essentials first.

### 4.3 The handshake

The **first reply of every role** starts with a 3–5 line handshake, so
Eliott sees at a glance that the right role loaded the right state:

```
Rôle : Tuteur · sceau : <seal> · Mission : libft P1.2
Lu : baseline, cursus_progress, recon, atlas-libft-p1 (approved), handoff P1.1, P1 (<seal>), P5 (<seal>)
Règles : IA étape 1 · fonctions autorisées : <…> · verrous : libft (org)
Prochain pas : …
```

A wrong or missing line means the role did not load. Re-tag, or paste the
role doc. The core gives this shape; where a role doc states its own
version of a line, **the role doc wins** (C3b).

### 4.4 Conversation naming

`<Rôle> — <objet> <étape>`, for example `Tuteur — libft P1.2`, `Prof —
pointeurs`, `Éclaireur — libft`, `Mère — v1.0`. **One Mother conversation
at a time;** as many others as there are missions in progress.

## 5. The roles (L2)

Seven roles. Each one has a doc in `system/roles/` (written in C2) with
the same sections: mission, tag, what it reads, how it works, what it
never does, what it produces, its report.

| Role | Mission | Behaviour | Never |
|---|---|---|---|
| **Mère** (Mother) | Evolve the system; triage the inbox; version | architect, brake | touch cursus work itself |
| **Éclaireur** (Scout) | Open (step 0: recon dossier) and close (step 6) every project; thread research | researcher | give solutions; read locked or not-yet-validated implementations anywhere |
| **Professeur** (Professor) | Concept courses, project atlases, deep explanations | generous teacher, visual | write the graded deliverable |
| **Tuteur** (Tutor) | Walk Eliott through a project, step by step | GRADED coach | hand over the solution, even in pieces |
| **Examinateur** (Examiner) | Everything that verifies (5 parts, below) | rigorous, fair | grade its own work; help during a real exam |
| **Navigateur** (Navigator) | Operations: Git, GitHub, Vogsphere, cluster, intra, tools | step by step, Eliott types | type commands for him |
| **Bâtisseur** (Builder) | Univers42 and non-graded building | full collaborator | build a graded project in disguise |

**The Examinateur's five parts** (one role for now; whether to split it is
reassessed after Libft):
1. the pre-submission checklist (Norm, flags, relink, forbidden
   functions, leaks, edge cases, the README's AI section), run in a fresh
   clone on the exact commit to turn in;
2. the defense simulation, playing the peer evaluator;
3. understanding checks (Eliott explains back, short quizzes);
4. exam preparation (TBD-2);
5. **review of the Professeur's courses and atlases**: only this review
   sets them `approved`.

**The Navigateur's situations:**
- Git and GitHub daily (commits, branches, PRs, conflicts);
- the Vogsphere turn-in (a wrong push can cost a 0);
- the cluster (installing without sudo, goinfre, dotfiles);
- the intra (registrations, evaluation slots, Pace);
- installing tools;
- owner of `friction_log`.

**Navigateur or Bâtisseur?** The Navigateur operates the environment: a
one-off fix, "how do I do X". The Bâtisseur builds something durable, such
as a versioned dotfiles repo. A friction starts with the Navigateur; when
its fix deserves to become a tool, it moves to the Bâtisseur.

**Modes (v0.1) → roles (v1.0):**

| v0.1 mode | v1.0 role(s) |
|---|---|
| LEARNING | Professeur |
| GRADED | Tuteur, plus the Examinateur's checklist and defense parts |
| EXAM | Examinateur (exam prep) |
| BUILDING | Bâtisseur |
| NAVIGATION | Navigateur |
| MOTHER | Mère |
| WELLBEING | stays a global override |

## 6. The protocols (L3)

Each one has a doc in `system/protocols/` (written in C2).

### P1 — Project cycle

```
0  Éclaireur    recon dossier, "Now" update      [recon:<p>]
0b Examinateur  diagnostic (P7): first project,  [eval:baseline]
                or baseline stale
1  Professeur   missing concept courses          [prof:<concept>]
2  Professeur   atlas, numbered steps P<part>.<n> [prof:<p>-atlas]
   Examinateur  review → approved                [eval:courses]
3  Tuteur       one conversation per atlas step, [graded:<p>] <step>
                handoff per step; last step:
                Eliott writes the README AI section
4  Examinateur  checklist (fresh clone from       [eval:<p>]
                Vogsphere, exact commit) + defense simulation
5  Navigateur   turn-in: Vogsphere head = checked [nav]
                hash, then Eliott declares the project
                finished; two peer defenses, then the Moulinette
6  Éclaireur    close, after the intranet result  [recon:<p>] close
                → cursus_progress, unlocks, baseline,
                  thread layer, KB residue, pruning
```

**Gates:**
- no step 3 without an **approved** atlas part;
- no turn-in without the checklist passed **on that commit**;
- no unlock without Eliott's statement that the project is validated;
- no close without the project's handoffs. A failed evaluation is not a
  close: nothing is pruned, and the work goes back to the Tuteur.

**The project slug** is the project's name as the intranet writes it,
lowercased, spaces and hyphens as underscores: `libft`, `push_swap`,
`get_next_line`, `born2beroot`. Every role uses it for `projects/<p>/`
and in its tag, so two conversations never create two directories
(decided 2026-10-02; the subject's filename is not a reliable source —
`GetNextLine.pdf` would give the wrong slug). The rule itself lives in
P1 §1.

**The recon dossier** (step 0) contains:
- where the project sits in its thread: what it builds on, where it leads,
  which layer to build now so the next project can stand on it;
- **the rules card** (its canonical home): AI stage, allowed functions,
  libft yes/no, group size, files and README to turn in, locked
  references (same project and same problem). `cursus_progress` "Now"
  keeps a one-line summary and a pointer;
- the prerequisite concepts, so the list of courses that exist and courses
  to write (provisional until the diagnostic, step 0b);
- the Univers42 tools usable now;
- known pitfalls, phrased as questions;
- the workload against the Pace deadline, **Strate's own pipeline
  included**, with a minimal path and the date tutoring starts.

It is the mission brief for the Professeur and the Tuteur.

### P2 — Session report

Every conversation ends with it, in a fixed format:
- done;
- learned;
- weak spots;
- AI use (for the README);
- decisions;
- next step;
- **→ Mère** proposals, allowed from any role, about anything;
- KB residue (ideas worth an atom later).

**Where it goes: where it will be consumed.** Always written with
Eliott's OK, one file each, never a shared file.

In short:
- project sessions report in the project's files (handoffs, evals, the
  recon);
- builds report in their handoffs;
- courses keep their KB residue in their "KB candidates" section;
- the Mère reports in `decisions_log`;
- `inbox/` receives only proposals for the Mère.

The full routing table is in `system/protocols/p2-session-report.md`.
Anything with no reader stays in the chat.
- If the conversation cannot write, it prints the full file with its
  path; it never claims a write without a tool result.
- A file is deleted once consumed: inbox files after triage, project
  files at close.

This settles N8: the AI-use lines live in the project files (the recon
has one for the pipeline; each handoff, each eval and each atlas's Review
block has its own). The
Tuteur's last step gathers them and asks about any `[learn]` use, so that
Eliott writes the README's AI-use section **before** the turn-in.

### P3 — Improvement loop

- Any role puts its proposals in a file in `inbox/`.
- The Mother triages the inbox. Each item is either applied (logged in
  `decisions_log`), sent to `open_questions` (needs a decision) or rejected
  with its reason.
- **Rhythm:** TBD-8, decided in phase D (proposed: event-driven plus a short
  weekly triage).
- **Health signal:** an inbox item older than 2 weeks means the loop is
  dead.

### P4 — Thread unlock

This is part of P1 step 0 whenever a project opens or continues a thread.
The Éclaireur:
1. maps the whole thread on the graph;
2. mirrors it on Univers42;
3. updates the thread's entry in `thread_map` (and `univers42_map` if the
   org changed).

This is the protocol formalized from session 2 (N1, N9).

### P5 — Handoff

When a conversation reaches the end of its step, or grows long, it writes
a handoff:
- state;
- decisions;
- open points;
- the exact next step;
- files touched;
- plus the P2 fields (weak spots, AI use, KB residue).

The next conversation starts from it.
- **Tuteur:** systematic, one conversation per atlas step. The file is
  named by step ID (`handoff-P1.2.md`), so the next step finds it
  directly.
- **Bâtisseur:** one per session of a multi-day build.
- **Professeur:** `courses/<concept>-handoff.md` for a course that spans
  conversations, deleted once the course is approved.
- **Mother:** `living/mother_handoff.md`, when the conversation degrades.
- Handoffs never go into `inbox/`.

### P6 — Course and atlas production

1. The plan, validated by Eliott.
2. Sections produced over several turns: never one giant output, because
   of token limits and quality.
3. Assembly: a markdown source (the agents read it) plus an HTML render
   with visuals (Eliott reads it).
4. **The three locks:**
   - every code example compiled and run. It is marked `tested` only if
     it actually ran in that conversation; otherwise `not tested`;
   - every technical fact anchored (man page, C standard, Norm, 42
     doc). The reviewer opens each anchor for real; one it cannot open
     is `anchor unchecked`, which blocks approval;
   - review by the Examinateur (several courses can be reviewed in one
     `[eval:courses]` conversation).
5. **Claim typing** on every statement (courses are in English):
   `standard` · `implementation` · `UB` · `42 rule` · `advice`.
6. **Status:** `draft` → `in review` → `approved`. Only the Examinateur
   sets `approved`. Its only edits are the status line and a Review block
   at the end of the source.
7. **Integrity:**
   - no example, twin, check-yourself answer or diagnostic correction
     reproduces a file that a graded project not yet validated must turn
     in: a function, its Makefile or its header;
   - an atlas stays at N1, its pitfalls written as questions.
8. **Delivery:**
   - the final HTML is rendered from the approved source and checked
     against it before its link is recorded (P6 §5); an early render
     carries a visible DRAFT banner;
   - the HTML is downloaded and archived by Eliott (later in the KB
     `outputs/`); the markdown source stays in the Project Knowledge.

### P7 — Baseline and diagnostic

- `living/baseline.md` is the declaration of level per domain, modelled on
  the KB's `_baseline` template: already solid / shaky / zero / preferred
  depth.
- It is built from the Piscine record, then **checked by a diagnostic**
  (`[eval:baseline]`, about 20 minutes, possibly in targeted blocks) at
  the start of Libft.
- It is updated at every project close. Every role reads it before
  explaining.

### P8 — Exam preparation

Placeholder (TBD-2, to decide at the latest when push_swap starts).
Known: unlimited attempts; 100% is needed to move to the next milestone.

### P9 — Change control

- Changes to the core, `system/` or the architecture happen only in the
  Mother, as a diff with a reason.
- Eliott's OK, then an entry in `decisions_log`.
- **Numbering:** 0.x bootstrap; **1.0-rc from the first paste of the
  core** (2026-10-02); `1.0-rc.N` for fixes released before 1.0; 1.0 once
  the C5 fixes are in, committed in D2; minor versions (1.1, 1.2) for
  calibrations; a major version for a new layer, seam or core rule.

## 7. Pedagogy: how learning is organised

- **Courses by concept, not by project.** They are complete, in HTML with
  abundant visuals (memory, arrays, pointers, execution tables). Each one
  opens with a **prerequisites** header linking to earlier courses, so
  together they form a **course tree** grown from the Piscine base.
- **Bootstrapping the tree (C4).** The recon's prerequisite list, checked
  against the baseline, gives the first courses. They start at the
  foundations Libft stands on (for example the memory model, types and
  sizes, pointers and arrays, strings, compilation and libraries), even
  where the Piscine already touched them. After that, each project adds
  only the courses it needs, each standing on the existing ones.
- **Atlases by project**, split when the project is large (Libft: a general
  atlas plus one per part of the subject). An atlas is a complete roadmap
  with no solution; it must let Eliott start alone. It numbers its steps
  `P<part>.<n>`, each sized for one tutoring conversation.
- **The skeleton ladder:**
  - **N1, the contract** (prototype, inputs, outputs, edge cases, the man
    page): in the atlas, for every function.
  - **N2, the steps in words:** the Tuteur gives it after an attempt. For
    a short function, N2 points at the wrong or missing step in *his*
    steps instead of listing them all.
  - **N3, a code-shaped skeleton with holes:** only for non-trivial
    functions, never when it would already be the solution.
  - **N0, the goal:** Eliott writes N1–N2 himself and the Tuteur critiques
    (the scaffolding fades).
- **Twins and Python Tutor.** A twin is the same mechanism with another task
  and other data, never the solution with renamed variables: if renaming
  or retyping it gives the deliverable, it is not a twin. It is stepped
  through in Python Tutor, or run as a terminal lab when the concept lives
  between files or tools (compiler stages, archives, `make`). The Professeur uses twins in courses; the Tuteur
  uses them when Eliott is stuck. Python Tutor is also for stepping through
  Eliott's *own* function to see his bug.
- **The toolbox** (`system/tools.md`), introduced progressively:
  - `man` first (per 42's AI test, docs and man pages are what remains at
    exams);
  - Python Tutor;
  - `-g -fsanitize=address`, valgrind;
  - gdb;
  - norminette;
  - testers and Torturette, after Eliott's own tests, never instead of them.
- **The AI stage per project** follows the subject's AI chapter, recorded
  in the rules card: stage 1 (reason first; no direct answers) up to
  Libft, ft_printf and GNL; stage 2 from push_swap.
- **The help ladder** climbs one rung per message, the next after Eliott's
  next try, and never reaches the solution (details in `tuteur.md`).

## 8. State (L4) and content (L5)

| Document | Holds | Writer | Visibility |
|---|---|---|---|
| `living/cursus_progress.md` | position, validations, marks + weak spots, the rules card's one-line summary and pointer, Pace | Éclaireur (open, close); **"Now" only**, any role, with OK | **private** |
| `living/baseline.md` *(new)* | level per domain | Examinateur (diagnostic) and Éclaireur (close), with OK | **private** |
| `inbox/<date>-<role>-<object>.md` *(new)* | proposals for the Mère, one file each | any role, with OK; deleted after triage | **private** |
| `living/open_questions.md` | pending decisions | Mère | private (personal dates inside) |
| `living/decisions_log.md` | the changelog, from C3c onward | Mère | **private** (it records marks, Pace and dates); the repo's `CHANGELOG.md` is the public history |
| `living/decisions_log-bootstrap.md` *(frozen 2026-10-02)* | the bootstrap record, phases A to C3b | **nobody: frozen, never written to again** (N13) | **private** |
| `living/environment.md` | machines, accounts, setup | Navigateur, with OK | **private** |
| `living/friction_log.md` *(since 2026-10-05)* | frictions and their fixes | Navigateur | private |
| `living/univers42_log.md` *(created at Discord V1.1)* | Eliott's own verified contributions, one dated line each | Bâtisseur, with OK | **private** (N3) |
| `living/cursus_map.md` | the holy graph, both tracks | Mère / Éclaireur | **private** (intranet-derived) |
| `living/thread_map.md` | the threads and their layers | Éclaireur | **private** (subject-derived) |
| `living/univers42_map.md` | the org, public data | Éclaireur | **private until N5 is settled** (see open_questions) |
| `living/kb_candidates.md` *(new, at first close)* | KB residue kept from closed projects | Éclaireur only (close) | private |
| `living/mother_handoff.md` *(new, when needed)* | the Mother's handoff | Mère only | private |
| `living/roadmap.md` *(since 2026-10-05)* | the route to the current project's close: stages, their exits, target dates | Mère only | **private** |
| `courses/<concept>.md` | concept course sources | Professeur → Examinateur | private by default; generic C knowledge could go public later |
| `projects/<project>/recon.md`, `atlas*.md`, `handoff-<step>.md`, `eval-<n>.md` | project work; the rules card lives in `recon.md` | Éclaireur, Professeur, Tuteur, Examinateur | **private** (project tutorials fall under Article 9) |
| `builds/<object>/brief.md`, `handoff-<n>.md` *(new)* | non-graded builds | Bâtisseur | **private** |
| `courses/<concept>-handoff.md`, `projects/<p>/research-<topic>.md` *(new)* | a course in progress; research serving a project | Professeur; Éclaireur | **private** |

**Write discipline.** A Project Knowledge write replaces the whole
document. So:
- re-read a document right before writing it, never from a copy read
  earlier in the conversation;
- anything several conversations produce goes in one file each (reports,
  handoffs), never appended to a shared file;
- no write tool: print the full file with its path, and never claim a
  write without a tool result.

**A log that only grows gets split.** When a living document's cost per
entry becomes a full read plus a full rewrite, the Mère proposes freezing
the closed part in a sibling file and restarting the live one, choosing a
boundary that means something. Done once, for `decisions_log`, on
2026-10-02 (N13).

**Storage budget.** The Project Knowledge has a 2 MB cap (0.33 MB used at
C1; 0.91 MB on 2026-10-06, `n1570.pdf` included). Only markdown sources live there; HTML renders do not.
Handoffs and reports of finished projects are deleted at close, once the
close step has kept what matters. A bigger Project also pushes claude.ai
toward retrieval mode (§4.2), one more reason to stay lean.

## 9. Reference (L6)

All of it is private and never goes in the git repo:
- the subject PDFs;
- the Norm v4 (`es_norm-2.pdf`);
- `n1570.pdf`, the C11 draft (N1570) that reviewers open (P6 §3);
- the campus rules;
- the peer-evaluation guide;
- the security charter;
- the Vogsphere manual;
- the campus FAQ;
- `AI_in_42`;
- the 42Next FAQ;
- `project_data.json`;
- the KB docs (`KB_ARCHITECTURE`, `SETUP-PROJET`, `GABARITS`).

## 10. Seams

- **KB:**
  - Strate is understanding in action; the KB is the residue.
  - The KB starts on its own corpus first (Eliott's decision). Until
    then, Strate's residue waits in the courses' "KB candidates" sections
    and in `living/kb_candidates.md`.
  - When the KB is ready: courses are archived in `outputs/`, atoms are
    drawn from the reports, and the anchor proposal for code knowledge
    (man section, C standard §, file:line) goes to the KB's Mother.
  - Strate never writes into the vault.
- **Univers42:**
  - maps and integrity locks live in `univers42_map`;
  - building work goes through the Bâtisseur (`[build:discord]`,
    `[build:site]`, contributions);
  - the league is independent: candidates excluded, independence stated;
  - Strate never acts on a Univers42 space itself: Eliott acts, Strate
    drafts. A bot is a V2 build at the earliest (decided 2026-10-06).
- **Git repo (`strate`, on Eliott's GitHub, public since 2026-10-05;
  MIT from D2):**
  - it contains only what is marked public: the core's public projection,
    `system/` (architecture, roles, protocols, templates, tools), a
    README, a CHANGELOG and, from D2, the LICENSE;
  - **first lock:** private documents live only in the Project Knowledge,
    never in the git tree, so nothing can leak through a mistaken
    `git add`;
  - **second lock:** a whitelist `.gitignore`. Everything is ignored
    except `.gitignore`, `README.md`, `CHANGELOG.md`, `system/` and, from
    D2, `LICENSE`; `*.pdf` and `*.odt` are refused even inside `system/`;
  - **the public projection:** the repo's core is the Project's core with
    its "Who Eliott is" section reduced to one line, his first name. That
    is the only difference allowed (Eliott, 2026-10-05), so everything
    private about him lives in that section. **Everything finer — level
    per domain, the Piscine record, marks, weak spots, Pace and
    deadlines — stays in the private `baseline.md` and
    `cursus_progress.md`.**
- **Tools:** see §7.

## 11. The trees

**Project Knowledge (target v1.0):**

```
system/
  core.md                  the release copy of the instruction field
  architecture.md          this document
  roles/                   mere, eclaireur, professeur, tuteur,
                           examinateur, navigateur, batisseur
  protocols/               p1-project-cycle … p9-change-control
  templates/               recon (rules card inside), atlas, course,
                           eval, brief, starters (the report and
                           handoff formats live in P2 and P5)
  tools.md
living/                    the state documents of §8
inbox/                     proposals for the Mère, one file each
courses/                   concept course sources (markdown)
projects/<project>/        recon (with the rules card), atlases,
                           handoffs, evals
builds/<object>/           brief, handoffs
(reference files)          §9
```

**Git repo `strate` (public):**

```
README.md                  what Strate is and why
CHANGELOG.md               public history of versions
LICENSE                    MIT (from D2)
.gitignore                 second lock: a whitelist (§10)
system/core.md             the core's public projection (§10)
system/                    architecture, roles, protocols, templates, tools
```

**One file, three places.** The **instruction field is authoritative**.
`system/core.md` is its release copy in the Project, written in the same
gesture as the paste — never one without the other (C3b). The repo's
`system/core.md` is its public projection (§10), committed at each
release after a `diff` that shows one hunk, "Who Eliott is", and nothing
else (P9 §3).

`univers42_map` may join the repo later (`docs/`), once N5 is settled.

## 12. Quality and integrity gates

- **Rules card per project** (AI stage, allowed functions, locks),
  written at step 0 in `recon.md`.
- **Locks:**
  - same project and same problem (e.g. `philosopher` ↔ Codexion);
  - opened only by a validation Eliott states, recorded in
    `cursus_progress` at close;
  - they cover the whole web, not only Univers42: no full implementation
    of a not-yet-validated project is read anywhere;
  - no clone, fork or submodule that puts a locked reference on disk
    (hellish carries the org's libft).
- **Courses:** the three locks, claim typing, and no example that
  reproduces a deliverable file (a function, a Makefile, a header).
- **Turn-in:** the Examinateur's checklist on the exact commit, and the
  defense simulation.
- **Understanding:** "Could I reproduce it without AI, with just the man
  pages, like at the exam?", the 42 test, used by every role.
- **Transparency:** an AI-use line in every handoff, gathered for the
  README before the turn-in.

## 13. Failure modes and their countermeasures

| Failure | Countermeasure |
|---|---|
| A role does not load, or loads the wrong state | the handshake; the fallback paste |
| Retrieval mode: a role reads only fragments of its doc | the seal in the handshake; short role docs, essentials first; the paste fallback |
| A draft atlas drives tutoring | the gate: approved atlas parts only |
| The pipeline is too slow for the deadline | the recon's minimal path |
| A course example is a deliverable in disguise | the P6 integrity rule, checked in review |
| Two conversations overwrite the same document | one file per report or handoff; re-read before writing |
| Two conversations write two directories for one project | the project slug rule (§6, P1 §1) |
| A long conversation degrades | a handoff per step (P5) |
| Explanations too hard or too easy (Reloaded) | baseline plus diagnostic (P7) |
| Wrong facts in a course | the three locks, claim typing |
| One conversation doing everything | one role, one mission |
| The loop dies | reports are mandatory; inbox-age signal; weekly triage |
| Infrastructure instead of work | the brake principle (§2.11) |
| Leak on the public push | private docs never in the git tree; the projection diff and the private-term check before every commit (P9 §3) |
| Project Knowledge full | markdown sources only; handoffs pruned at close |
| A living document too big to rewrite | freeze the closed part, restart the live one (§8) |
| Token limits on big documents | sectioned production (P6) |
| A shortcut around the pedagogy | rules card, locks, skeleton ladder, twin rule |

## 14. What comes next

- **C2** wrote `system/roles/` (7), `system/protocols/` (P1–P9),
  `system/templates/` (the starters included) and `system/tools.md`.
- **C3 is complete** (2026-10-02). It composed the core (L0–L1) as a diff
  against v0.1 plus `baseline.md`, released it, and ran its knock-on lot.
  **It did not create `inbox/`:** the folder is born with the first
  proposal, because an empty placeholder would age into P3's two-week
  alarm.
- **C4** is the real start on Libft: recon, diagnostic, first courses,
  atlas, with a stop at the first red flag. **Running since 2026-10-02.**
- **D1**, the public repo and its first commit, was done on 2026-10-05.
  Then **K**, every open conversation closed with its report, and **E**,
  the decisions of 2026-10-05 applied and the inbox emptied
  (`1.0-rc.2`).
- **C5**, the external audit (Fable 5.1 MAX, with a pre-mortem), is split
  so that it audits real material: **V1**, light, after Libft's Part 1;
  **V2**, the full audit, after Libft's close.
- **D2** follows C5: its fixes make 1.0, with the MIT license and TBD-8.
- The dated route lives in `living/roadmap.md`.

— architecture.md v1.0 · seal: corbel-62 —
