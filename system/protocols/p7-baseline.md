# P7 — Baseline and diagnostic

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** `living/baseline.md` says, domain by domain, what Eliott
> already masters, what is shaky and what is at zero. Every role reads it
> before explaining anything, so nothing is re-explained that is solid
> and nothing is skipped that is missing. It is checked by a 20-minute
> diagnostic, and updated at every project close. It is private.

- **Used by:**
  - every role (to read it);
  - the Examinateur (the diagnostic);
  - the Éclaireur (the update at close).

## 1. The document

`living/baseline.md`, private and never in a repo. One block per domain:

```
## <domain> — solid | shaky | zero
- Solid: <do not re-explain>
- Shaky: <knows the words, not the mechanism>
- Zero: <start from the base>
- Preferred depth: <intuitive | technical | formal>
- Source: <Piscine record / diagnostic / close of <project>> · <YYYY-MM-DD>
```

**The domains:**
1. C basics: types, operators, control flow, functions;
2. memory and pointers: addresses, arrays, arithmetic, stack and heap,
   `malloc`/`free`;
3. strings: `char` arrays, `'\0'`, the string functions;
4. compilation and Makefiles: preprocessor, compile, link, `ar`, rules,
   relink;
5. shell and git: navigation, permissions, pipes, the everyday git
   commands;
6. debugging: reading errors, ASan, valgrind, gdb;
7. the Norm and the 42 constraints: norminette, the limits per file and
   per function, `static` helpers, forbidden functions, the turn-in
   rules.

Add a domain when a thread opens one (networking, Python, algorithms),
or when a constraint applies across a whole family of projects, as the
Norm does.

## 2. The first version

C3 writes a first draft from the Piscine record Eliott gave: the modules
done, the exam results, the Reloaded weak spots. Every level in it is
marked *provisional* until the diagnostic.

## 3. The diagnostic (`[eval:baseline]`)

- **When:** at the start of the first project (P1 step 0b), and again
  when the baseline is stale:
  - older than two projects;
  - or Eliott finds the explanations miscalibrated.
- **Timing:** about 20 minutes, plus a short debrief.

**How:**
1. **One question per domain,** about three minutes: "explain or
   predict" ("what does this print, and why?") or "spot the problem"
   ("what is wrong in these four lines?"). Add one follow-up only where
   the answer looks shaky.
2. **Answers in the chat,** in Eliott's own words. No help and no hints
   during the diagnostic.
3. **Scoring per domain:**
   - *solid:* right, with the right reason;
   - *shaky:* partial, or right for a wrong reason;
   - *zero:* no model yet.
4. **The debrief:** each answer corrected in one or two lines. The deeper
   gaps become courses, not a lecture.
5. **Output:** the proposed `baseline.md`, with the sources dated,
   written with Eliott's OK.

The questions and corrections test mechanisms. None of them implements a
function that a graded project not yet validated must turn in.

## 4. Updating

- **At every close** (P1 step 6), the Éclaireur proposes the change, from
  the Examinateur's findings and the weak spots in the handoffs.
- **Anytime:** Eliott can say "this is solid now" or "I'm lost on X".
  The role adapts at once, and notes it in its handoff or eval.
- **A role that finds a clear gap** notes it the same way.
- Only the writers in architecture §8 edit the baseline: the Examinateur
  (diagnostic) and the Éclaireur (close), with OK.

— p7-baseline.md v1.0 · seal: spandrel-36 —
