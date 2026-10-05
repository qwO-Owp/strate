# Strate

*Strate* is French for stratum: a layer laid on the layers beneath it.

Strate is a system of specialised AI conversations running inside one
Claude Project. It supports one student through the 42 cursus and his
work in Univers42, an independent student community. Each conversation
plays one role on one mission (scout, professor, tutor, examiner,
navigator, builder), reads the shared state it needs from documents,
and ends with a report. A "Mother" conversation turns those reports into
changes to the system itself, each one a diff with a reason.

## What is in this repository

- `system/core.md`: the core instructions (the Project's instruction field).
- `system/architecture.md`: how Strate is built, and why.
- `system/roles/`: one document per role.
- `system/protocols/`: P1–P9, how roles chain, report and hand over.
- `system/templates/`: skeletons (recon, atlas, course, eval, brief) and conversation starters.
- `system/tools.md`: the toolbox.

## What is not

- No 42 pedagogical material: no subjects, exams, evaluation sheets or
  Piscine material, and no solutions to graded projects.
- No personal state: progress, levels and results stay in the private Project.

Strate is built to make the student independent of it. It never writes
graded work, and it follows each subject's own rules on AI use.

## Status

- Version 1.0-rc, in service since 2026-10-02. See `CHANGELOG.md`.
- Not affiliated with 42 or 42 Madrid.
- License: none yet. MIT is planned at 1.0; until then, all rights reserved.
