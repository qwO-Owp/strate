# P4 — Thread unlock

Strate protocol doc. When you follow it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.** When a project opens or continues a thread, the
> Éclaireur, as part of the recon:
> 1. maps the whole thread on the graph;
> 2. mirrors it on Univers42;
> 3. proposes the updated `thread_map` entry.
>
> The map shows the whole road: every project of the thread, named, and
> what it reuses. It never holds a solution. Locked repos are seen only by
> name, description and existence.

- **Used by:** the Éclaireur (P1 step 0).
- **Trigger:** the recon of a project that opens a thread, or continues
  one whose entry is older than the thread's last validated project.

## 1. Map the thread on the graph

Sources:
- `living/cursus_map.md` and `project_data.json` (names, prerequisites,
  ranks, both tracks);
- the subjects in Project Knowledge.

List, in order:
- the projects of the thread, on his track and on the other Common Core
  track;
- the outer-circle projects that continue it;
- the exams that test it.

Mark anything uncertain as *unverified*.

## 2. Mirror it on Univers42

Sources:
- `living/univers42_map.md`;
- the public org pages.

For each project of the thread:
- the org repos that implement it, marked **locked** until Eliott
  validates that project, or one posing the same problem;
- the tools usable now (testers, visualizers), each checked for a shipped
  implementation through its README and its file list.

Also note the org conventions that apply, and the gaps: no repo yet, or
empty placeholders.

## 3. Write the entry

Propose the section of `living/thread_map.md`, for Eliott's OK:

```
### T<n> — <thread name>
- Sequence: <project → project → …> (his track) · other track: <…> · outer: <…>
- The layer: <what Eliott builds once and extends at each step>
  - now (<this project>): <the part of the layer to build now>
  - next: <what the next project will ask of it>
- Univers42: tools usable now <…> · locked until validation <…>
- Pitfalls across the thread: <typed: subject says / common practice; phrased as questions, never remedies>
- Open: <what only Eliott, staff or a later subject can settle>
- Updated: <YYYY-MM-DD>, by the recon of <project>
```

If the org changed, also propose the `univers42_map` section. **No
personal progress goes into `thread_map`:** position per thread lives in
`cursus_progress`.

## 4. Depth

- Map positions, not contents.
- Describe a future project by what it asks of the layer, never by how
  to solve it.
- Two good entry points beat forty links.

— p4-thread-unlock.md v1.0 · seal: umber-74 —
