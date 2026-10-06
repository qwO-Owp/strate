# Tools — the toolbox

Strate reference doc. When you use it, quote its seal (last line) in the
"Lu" line of your handshake.

> **Essentials.**
> - Tools come in one at a time, when a real need shows up: `man` first,
>   because it is what remains at exams.
> - Eliott's own tests always come before any tester.
> - The final check of anything graded runs on the cluster: evaluators use
>   its compiler (clang) and its norminette version.
> - Which tool exists on which machine lives in `living/environment.md`
>   (private).

- **Used by:** the Tuteur (introducing tools), the Examinateur (the
  checklist), the Navigateur (installing), the Professeur (examples).

## 1. Where code runs

| Place | What runs there | Notes |
|---|---|---|
| Eliott's machines (cluster, laptop) | his code, his tests, the turn-in | the cluster is the reference for anything graded |
| the conversation's workspace | course examples, twins, his pasted code (with his own `main`) | gcc, clang, valgrind, gdb; man pages once installed (below), otherwise man7.org; norminette only after `pip install norminette==<cluster version>` (see `environment`) |

Compilers warn differently, and the cluster's `cc` is clang. Something
that compiles cleanly elsewhere may fail there, so compile on the cluster
before any turn-in.

**Man pages in the workspace** (about a minute; tested 2026-10-06). The
image drops them; lift the exclusion, install, and read with `man.REAL`,
since the image's `man` is a wrapper that refuses. `apt-get update` may
report an error for an unrelated repository; the install works anyway.

```
mv /etc/dpkg/dpkg.cfg.d/excludes /etc/dpkg/dpkg.cfg.d/excludes.off
apt-get update
apt-get install -y man-db manpages manpages-dev manpages-posix-dev \
  libbsd-dev make-doc libclang-rt-18-dev
man.REAL 3 memmove
```

`libclang-rt-18-dev` is also what lets clang link an
`-fsanitize=address` build there. Versions follow the image (gcc 13,
clang 18 on 2026-10-06).

## 2. The toolbox, in order of introduction

| Tool | What for | Introduced | At exams |
|---|---|---|---|
| `man` | the contract of a function | first, always | expected (verify at the first exam) |
| `cc` flags | catching mistakes at compile time | from the first file | yes |
| Python Tutor | watching memory and pointers step by step | first pointer or array confusion | no (web) |
| `make`, `ar`, `nm` | building and checking a library | the first Makefile | verify at the first exam |
| norminette | the Norm | before any turn-in, and early | verify at the first exam |
| ASan (and UBSan) | memory errors and undefined behaviour, at run time | the first crash or strange output | verify at the first exam |
| valgrind | leaks and invalid accesses, without recompiling | leak hunting | verify at the first exam |
| gdb / lldb | stopping a program and looking inside | when `printf` debugging stops helping | verify at the first exam |
| testers | a second opinion on edge cases | **after** his own tests | no |

## 3. Commands

**man**
- `man 3 strlen` for the C library, `man 2 write` for system calls.
- `man -k <word>` to search.
- On a machine you administer, install the man pages with its package
  manager (see `environment`).

**Compiling**
- `cc -Wall -Wextra -Werror -c ft_x.c`: one file alone. Each file must
  compile alone.
- `cc -Wall -Wextra -Werror -g -fsanitize=address,undefined *.c` for a
  test build with ASan and UBSan. Never ship this build.
- ASan aborts on an oversized or failed allocation by default. To test
  how the code handles `malloc` returning `NULL`, run with
  `ASAN_OPTIONS=allocator_may_return_null=1`, or under valgrind.

**Library and Makefile**
- `ar rcs libft.a *.o` builds the archive.
- `nm -u libft.a` lists each member's undefined symbols.
  - Run it on the normal cluster build, never on a sanitizer build.
  - Ignore the `ft_*` symbols the library defines itself (see
    `nm libft.a | grep ' T '`) and compiler-inserted `__*` symbols.
  - What remains must be in the allowed list.
- **Relink check:** run `make` twice. The second run must rebuild nothing.
- Then `make clean`, `make fclean`, `make re`.

**norminette**
- `norminette` in the project folder, or `norminette <files>`.
- On a machine you administer, install the cluster's version (see
  `environment`), so every machine judges the same way. The cluster's run
  is final.

**Python Tutor** (pythontutor.com, C mode)
- Paste a small, complete program: a twin, or his function plus his own
  tiny `main`.
- Never use its AI-help button on graded code.
- Step forward and back, and watch the stack, the heap and the arrows.
- Keep programs small: it is a microscope, not a test bench.

**valgrind**
- `valgrind --leak-check=full --show-leak-kinds=all ./a.out`
- Run it on a build **without** ASan: the two do not mix.
- If missing on a machine you administer, install it with its package
  manager (see `environment`).

**gdb**
- Compile with `-g -O0`.
- `gdb ./a.out`, then:
  - `break <function>`, `run`;
  - `next` / `step`;
  - `print <expr>`;
  - `backtrace`;
  - `quit`.
- On the cluster, lldb works the same way with slightly different
  commands.

## 4. Rules

- **Own tests first.** Eliott writes his tests before running any tester.
  A tester is a second opinion, not the plan.
- **Check before trusting.** Before using a tester during a project not
  yet validated, check its README and its file list: no shipped
  implementation of the project.
- **One sanitizer at a time.** ASan builds and valgrind runs are
  separate.
- **The cluster decides.** The norminette version and the compiler of the
  cluster are what evaluators see.

— tools.md v1.0 · seal: quoin-71 —
