# P3 — Improvement loop

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** Any role may propose an improvement to anything. Every
> proposal reaches the Mère through `inbox/`. The Mère triages each one
> into applied, open question or rejected, always with a reason. An inbox
> file older than two weeks means the loop is dead. The brake applies:
> the system improves to serve the work, never instead of it.

- **Used by:** every role (to propose), the Mère (to triage).

## 1. Proposing

**Any role, about anything:** a role, a protocol, a template, the core,
the pedagogy, a living document.

A good proposal has three parts:
- **what** would change;
- **why,** meaning what went wrong or was missing;
- **evidence:** the moment it happened, a quote, a file.

Write it in the session's inbox file (P2). In the chat, a one-line
"→ Mère: …" is enough for Eliott to see it.

**Signals that deserve a proposal:**
- a handshake with a missing or wrong seal;
- a role that forgot its rules or read the wrong state;
- Eliott confused, or explanations that are too long or too short;
- a gate that slowed real work with no benefit;
- a friction repeated twice.

## 2. Triage (the Mère)

For each proposal, exactly one outcome:

| Outcome | What happens |
|---|---|
| applied | a diff and a reason, Eliott's go, the write, a `decisions_log` entry (P9) |
| open question | added to `living/open_questions.md`, with a deadline or a trigger |
| rejected | one line with the reason, in the triage entry of `decisions_log` |

Then the inbox file is deleted, with OK.

**The brake.** Before applying anything, ask what real work has happened
since the last change, and what this change unblocks. Fixes that unblock
the current project come first. Polish waits for the milestone.

## 3. Rhythm

Proposed; decided in phase D (TBD-8):
- **event-driven:** at every project close, at every milestone, and
  whenever the inbox holds five files or more (visible in the Project's
  document list);
- **weekly:** one short triage, even with no event.

A Mother session that only triages leaves a one-line `decisions_log`
entry.

## 4. Health

- **Inbox age:** a file older than two weeks means the loop is dead. The
  Mère says so first, in her status.
- **Silence:** no proposal for a month, while the work goes on. That is
  suspicious: ask Eliott what annoyed him.

— p3-improvement-loop.md v1.0 · seal: ferrule-21 —
