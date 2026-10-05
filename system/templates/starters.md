<!--
Strate — starters: how Eliott opens each kind of conversation.
This is a reference for Eliott. Templates and starters carry no seal.
-->

# Starters

**How to open any conversation:**
1. Open a new conversation **inside the Strate Project**.
2. Pick the model and effort shown below. They are defaults: change them
   whenever the task asks for it.
3. Name the conversation `<Rôle> — <objet> <étape>`.
4. First message: the **tag**, then one line of context.
5. **Check the handshake:**
   - the role's seal and each protocol seal match your list;
   - the "Lu" line names what it should have read.

   If something is wrong, re-send the tag, or paste the role doc as the
   first message and then the tag.

**Always true:** one Mother at a time. A yes/no question is never a go.
Nothing is written without your OK.

---

## Mère — `Mère — <sujet>` · Opus 5.5, extra

```
[mother] <what you want to change, or "triage de l'inbox">
```
Check: the status block (version, inbox, open items).

## Éclaireur — Opus 5.5, high, web on

**Open a project:** `Éclaireur — <projet>`
```
[recon:<projet>]
```
Attach the subject PDF if it is not in Project Knowledge yet.

**Close a project:** `Éclaireur — <projet> close`
```
[recon:<projet>] close — résultat intra : <validé / échoué>, <note>
```

**Research:** `Éclaireur — <sujet>`
```
[recon:<sujet>] <the question>
```

## Professeur

**A course:** `Prof — <concept>` · Opus 5.5, extra
```
[prof:<concept>]
```

**An atlas:** `Prof — <projet> atlas` · Opus 5.5, extra
```
[prof:<projet>-atlas] <partie, if only one part>
```

**A quick question:** `Prof — learn` · Sonnet 5, medium
```
[learn] <ta question>
```

## Tuteur — `Tuteur — <projet> <étape>` · Sonnet 5, high (Opus if stuck)

```
[graded:<projet>] <étape, e.g. P1.2>
```
Paste your code when you have some. Check that the atlas is `approved`
and that the handoff of the previous step is in the "Lu" line.

## Examinateur — Opus 5.5, high

**Diagnostic:** `Exam — baseline`
```
[eval:baseline]
```
Plan 20 minutes. Answer in your own words; no help during it.

**Review of courses and atlases:** `Exam — review`
```
[eval:courses] <which files>
```

**Checklist and defense:** `Exam — <projet>`
```
[eval:<projet>] <checklist / défense / les deux>
```
Push first. You will run the commands in a fresh clone **on the
cluster** and paste the output.

**Exam preparation:** `Exam — prep`
```
[exam] <what the exam covers>
```

## Navigateur — `Nav — <objet>` · Sonnet 5, medium (high if risky)

```
[nav] <objet, e.g. turn-in libft, ssh keys, install valgrind>
```
You type every command. Paste the output after each step.

## Bâtisseur — `Build — <objet>` · Sonnet 5, high (Opus for architecture)

```
[build:<objet>] <first session: "écrivons le brief">
```
For the community Discord and site: the first session of each writes
its brief (`builds/<objet>/brief.md`). Before the site goes live,
settle N5.

---

## Day one of a new project (the P1 sequence)

The conversations to open, in order:
1. `[recon:<projet>]`: the recon dossier and the minimal path.
2. `[eval:baseline]`: the diagnostic, on the first project or when the
   baseline is stale.
3. `[prof:<concept>]`, once per course the minimal path requires.
4. `[prof:<projet>-atlas]`: the general atlas, then the first part.
5. `[eval:courses]`: one batched review.
6. `[graded:<projet>] P1.1`: tutoring starts.

Steps 3 to 5 can overlap. While the Tuteur works on part 1, the
Professeur writes part 2.
