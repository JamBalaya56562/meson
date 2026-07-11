# Meson Open Pull Request Triage — Investigation Notes

- **Repository**: [mesonbuild/meson](https://github.com/mesonbuild/meson)
- **Scope**: all **521** currently open pull requests.
- **Generated**: 2026-07-11
- **Method**: this is a metadata-driven triage, not a code review of each PR's diff. For every open PR we pulled: draft status, mergeable state, review decision, CI rollup state, review/comment counts and authors, and the timestamp of the last human comment or review. PRs were bucketed by that metadata into the categories below.
- **A note on staleness**: GitHub's `updatedAt` field for these PRs is **not usable** as an activity signal — on 2025-08-19 the repository maintainer force-pushed the base branch, which bumped `updatedAt` on effectively every open PR at once regardless of whether anyone had touched it. Instead, "last activity" below is computed from the timestamp of the most recent actual comment or review, whichever is later (falling back to the PR's creation date if it has never received either).
- **Not covered**: this pass does not evaluate code quality, correctness, or whether a given change is desirable — only its process state (review/CI/conflict status) and how long it has sat without human interaction. Treat this as a worklist for triage, not a merge recommendation.

---

## Executive summary

| Bucket | Count | Share |
|---|---:|---:|
| Approved, not yet merged (`approved_ready`) | 11 | 2% |
| CI failing (`ci_failing`) | 32 | 6% |
| Merge conflict with base branch (`conflicting`) | 106 | 20% |
| Changes requested (`changes_requested`) | 57 | 10% |
| Draft (`draft`) | 66 | 12% |
| No review or comment yet (`awaiting_first_review`) | 19 | 3% |
| Commented on, but no formal review (`commented_no_formal_review`) | 126 | 24% |
| Reviewed (other state) (`other_reviewed`) | 104 | 19% |
| **Total** | **521** | 100% |

- **397** PRs have had no comment or review in over a year; **307** in over two years.
- **2** PRs appear to compete for the same target issue (see the dedicated section below).
- **9** PRs were verified as already resolved elsewhere / moot (see the dedicated section right below) — direct close candidates.

---

## Already resolved elsewhere / moot — close candidates (9)

Found by scanning each PR body for `Fixes #N` / `Closes #N` / `Resolves #N`, then checking whether that target issue is already closed even though this PR was never merged — a strong signal the fix landed a different way, or the issue no longer needs this change. Each entry below was verified by reading the issue's closing history and the PR's actual diff/intent (not just the cross-reference).

- **8** `superseded` — the target issue was resolved by a *different* PR/commit; this PR's diff is now redundant.
- **1** `moot` — the target issue was closed as invalid/wontfix/not-planned/duplicate; this PR no longer has a reason to exist.

| PR | Title | Classification | Confidence | Reason |
|---|---|---|---|---|
| [#5305](https://github.com/mesonbuild/meson/pull/5305) | compilers/c: fix clang-cl openmp | superseded | high | PR 5305 tried to fix clang-cl OpenMP support (issue #5298) by passing '-Xclang -fopenmp' as a compile flag. The issue was instead fixed by merged PR #12723 ('fix openmp dependency for clang-cl'), which uses a different, more complete approach: find_library('libomp') combined with openmp_link_flags/openmp_flags. This is confirmed in the current codebase (mesonbuild/compilers/mixins/visualstudio.py: ClangClCompiler.openmp_link_flags calling self.find_library('libomp')), making PR 5305's simpler flag-only approach redundant. |
| [#5854](https://github.com/mesonbuild/meson/pull/5854) | Compilers: Add support for b_sanitize to the ClangCL co | superseded | high | PR 5854 added b_sanitize support for ClangCL compilers via -Xclang flags to fix issue #5845. The issue was later fixed by a different merged commit, 'compilers: use GCC-style sanitizer arguments with clang-cl' (d0ca9be23dc3), which is now present in mesonbuild/compilers/mixins/visualstudio.py (ClangClCompiler.sanitizer_compile_args() emitting /clang:-fsanitize=...). This was confirmed directly in a 2026-07-06 issue comment identifying the fixing commit, verified against the current codebase, making PR 5854 redundant. |
| [#6367](https://github.com/mesonbuild/meson/pull/6367) | Properly handle the case of linking static library with | superseded | high | PR 6367 (yshui) attempted to fix issue #6365 (AttributeError linking a static library with an uninstalled custom_target). The issue was ultimately resolved by a different, merged PR #7769 ('Custom target link' by Sahnvour, merged exactly at the issue's closedAt timestamp), whose description explicitly states 'Continuation of #6367, fixes #6365' and implements both is_internal and extract_all_objects_recurse more completely. The original author (yshui) had handed off the work in the issue thread ('please go ahead'), and #7769 is what actually landed. |
| [#8782](https://github.com/mesonbuild/meson/pull/8782) | Fail upon encountering unknown options, add --allow-unk | superseded | high | PR 8782 proposed making unknown options fatal by default with an --allow-unknown-options opt-out, targeting the same issue #7288 as PR 8973. As with 8973, the issue was actually resolved by merged PR #8974 ('coredata: throw a MesonException on unknown options'), which implemented the equivalent behavior (hard error on unknown options) directly in coredata without the extra --allow-unknown-options escape hatch, making this PR's diff redundant. |
| [#8973](https://github.com/mesonbuild/meson/pull/8973) | mconf: add --fatal-meson-warnings (just as msetup) | superseded | high | PR 8973 added an opt-in --fatal-meson-warnings flag to 'meson configure' so unknown options would become fatal, targeting issue #7288. The issue was instead fixed by merged PR #8974 ('coredata: throw a MesonException on unknown options', merged the same moment the issue was closed), which makes unknown options a hard error unconditionally rather than requiring a flag. This is a stronger, unconditional fix that supersedes the opt-in approach in PR 8973. |
| [#13262](https://github.com/mesonbuild/meson/pull/13262) | Defer evaluating ModuleState.project_version | superseded | high | PR 13262 tried to fix issue #5134 (crash when invoking a module method inside project()) by deferring evaluation of ModuleState.project_version so the pattern would actually work. Instead, issue #5134 was fixed by merged PR #13647 ('Prevent raw exception during project()', commit 74dd77ed), which takes the opposite approach: it explicitly forbids module method calls during project() declaration with a clean MesonException. Current code (mesonbuild/interpreter/interpreterobjects.py:961-964) confirms this restriction is what shipped, making PR 13262's 'make it work' approach moot/redundant. |
| [#15691](https://github.com/mesonbuild/meson/pull/15691) | Fix regression in `Requires.private` for library(), and | superseded | high | PR 15691 was bonzini's comprehensive fix for the Requires.private pkgconfig regression (issue #15690). The issue was actually resolved by a different, minimal PR #15692 ('interpreter: revert shared_library_only=True for library()', merged commit 97802a56), described by bonzini himself as 'the minimal change requested by @nirbheek.' DimStar77 confirmed the minimal revert fixed most of the openSUSE/GNOME build failures, so the smaller merged PR superseded this broader one for the same issue. |
| [#9228](https://github.com/mesonbuild/meson/pull/9228) | Patch dir names independent from subprojects dir names | moot | medium | PR 9228 proposed making wrap patch-archive extraction robust to archives whose top-level directory name differs from the subproject directory name (issue #9085). The issue thread shows maintainer eli-schwartz repeatedly and firmly rejecting the underlying use case (personal wrap-overlay repositories with mismatched directory names), offering alternative workflows instead of a code fix. No PR/commit implementing this specific approach was ever merged, and current mesonbuild/wrap/wrap.py still contains the same naive try/except unpack logic that PR 9228 aimed to replace, indicating the request was effectively declined rather than fixed elsewhere. |
| [#10202](https://github.com/mesonbuild/meson/pull/10202) | mdist: allow passing options to setup, allow specifying | superseded | medium | PR 10202's stated purpose was to fix issue #10181 (meson dist failing due to python.platlibdir/install_env conflict) alongside broader mdist option-passing features. The specific bug was fixed by a different, much smaller commit (1420d0d, same author eli-schwartz) titled 'mdist: use better approach to finding original configured options', which reads the private coredata file instead of intro-buildoptions.json and explicitly says 'Fixes #10181'. This targeted fix was merged instead of the larger unmerged PR 10202, whose extra proposed features (passing setup options from meson.build) also don't appear to exist in the current codebase. |

---

## Ready to merge: approved, nothing blocking (11)

Reviewer approved (`reviewDecision: APPROVED`), no merge conflict, and CI is not in a failing state as of this snapshot. These are the lowest-effort wins for a maintainer — worth a final look and merge, or finding out why they're still sitting open.

| PR | Title | Author | Last activity | CI | Labels |
|---|---|---|---|---|---|
| [#7615](https://github.com/mesonbuild/meson/pull/7615) | RFC: Rewrite buildtype as debug+optimization pair in user inputs | xclaesse | 5.9y ago | — | — |
| [#7855](https://github.com/mesonbuild/meson/pull/7855) | Allow to cross-compile with C sharp | kgarlinski | 5.7y ago | — | bug, cross, language:C# |
| [#10670](https://github.com/mesonbuild/meson/pull/10670) | pkg-config: support multiple variables in `pkgconfig_define` kwar | jtojnar | 3.9y ago | — | — |
| [#9423](https://github.com/mesonbuild/meson/pull/9423) | Deprecate wrap-redirect and stop creating them | xclaesse | 3.3y ago | — | — |
| [#12667](https://github.com/mesonbuild/meson/pull/12667) | Make skipping of LinuxCrossMingwTests more robust | petere | 2.5y ago | — | — |
| [#13904](https://github.com/mesonbuild/meson/pull/13904) | dependencies: Improve error message when variable is not found | xclaesse | 1.6y ago | — | — |
| [#13864](https://github.com/mesonbuild/meson/pull/13864) | cmake/common: Add language map entry for nasm | res2k | 1.4y ago | — | module:cmake |
| [#14753](https://github.com/mesonbuild/meson/pull/14753) | new custom dependency lookup for libexecinfo | neheb | 322d ago | SUCCESS | — |
| [#14500](https://github.com/mesonbuild/meson/pull/14500) | improve gcovr coverage handling | Jannik2099 | 241d ago | SUCCESS | — |
| [#15695](https://github.com/mesonbuild/meson/pull/15695) | python: Add test cases for PEP 803/820 ft-compatible limited API | mgorny | 18d ago | SUCCESS | — |
| [#15990](https://github.com/mesonbuild/meson/pull/15990) | backends: apply per-subproject language args to targets | MaxandreOgeret | 0d ago | SUCCESS | — |

---

## CI failing (32)

| PR | Title | Author | Last activity | Review | Merge state |
|---|---|---|---|---|---|
| [#14677](https://github.com/mesonbuild/meson/pull/14677) | Add `lupdate` to Qt tools | JakobDev | 1.1y ago | — | UNKNOWN |
| [#14368](https://github.com/mesonbuild/meson/pull/14368) | Allow initializing languages per-machine | dcbaker | 1.0y ago | — | UNKNOWN |
| [#14832](https://github.com/mesonbuild/meson/pull/14832) | Fix meson compile for subproject run/alias targets, add unit | julianneswinoga | 352d ago | — | MERGEABLE |
| [#13392](https://github.com/mesonbuild/meson/pull/13392) | modules/gnome.py: Fix generating .gir with latest Windows SD | fanc999-1 | 350d ago | — | UNKNOWN |
| [#14831](https://github.com/mesonbuild/meson/pull/14831) | dist: Ensure modification time matches git commit time | fortysixandtwo | 348d ago | CHANGES_REQUESTED | MERGEABLE |
| [#14873](https://github.com/mesonbuild/meson/pull/14873) | CI: Use YAML aliases (anchors) for path filters | andy5995 | 340d ago | CHANGES_REQUESTED | MERGEABLE |
| [#14926](https://github.com/mesonbuild/meson/pull/14926) | windows: Add support for Zig's builtin rc compiler | meator | 326d ago | — | MERGEABLE |
| [#14934](https://github.com/mesonbuild/meson/pull/14934) | docs: Consistently spell "localisation" with an s in Localis | Newbytee | 318d ago | — | MERGEABLE |
| [#14968](https://github.com/mesonbuild/meson/pull/14968) | add cpp-filesystem and cpp-experimental-filesystem dependenc | na-trium-144 | 316d ago | — | MERGEABLE |
| [#12560](https://github.com/mesonbuild/meson/pull/12560) | add description kwarg to custom_target function | bruchar1 | 269d ago | — | UNKNOWN |
| [#15139](https://github.com/mesonbuild/meson/pull/15139) | Add a `hash` method for strings | rruuaanng | 264d ago | CHANGES_REQUESTED | MERGEABLE |
| [#11610](https://github.com/mesonbuild/meson/pull/11610) | docs: add example for specifying multiple dependencies | andy5995 | 194d ago | — | UNKNOWN |
| [#15432](https://github.com/mesonbuild/meson/pull/15432) | Add 'limited_api' argument to dependency method | AraHaan | 192d ago | — | MERGEABLE |
| [#14773](https://github.com/mesonbuild/meson/pull/14773) | Add support for BLAS and LAPACK dependencies (continued) | mgorny | 181d ago | — | MERGEABLE |
| [#15604](https://github.com/mesonbuild/meson/pull/15604) | msetup: fix invalid directory message | stephanlachnit | 123d ago | — | MERGEABLE |
| [#15333](https://github.com/mesonbuild/meson/pull/15333) | environment: Add env.prepend_library_path() method | xclaesse | 111d ago | — | MERGEABLE |
| [#15748](https://github.com/mesonbuild/meson/pull/15748) | Update CI actions | dcbaker | 74d ago | — | MERGEABLE |
| [#15771](https://github.com/mesonbuild/meson/pull/15771) | modules: qt: probe libexec before bin for Qt6 | jrosdahl | 67d ago | — | MERGEABLE |
| [#15862](https://github.com/mesonbuild/meson/pull/15862) | modules/rust: use absolute path for bindgen input when outpu | simonfrechette-dev | 41d ago | — | MERGEABLE |
| [#15876](https://github.com/mesonbuild/meson/pull/15876) | GnuCompiler.has_arguments: detect "not supported for this ta | lzwind | 38d ago | — | MERGEABLE |
| [#13351](https://github.com/mesonbuild/meson/pull/13351) | structured_sources: Allow build_tgt to be added as source | sp1ritCS | 32d ago | CHANGES_REQUESTED | UNKNOWN |
| [#15875](https://github.com/mesonbuild/meson/pull/15875) | mtest: avoid GTest XML filename collisions across suites | ChandruRavi3708 | 31d ago | — | MERGEABLE |
| [#15914](https://github.com/mesonbuild/meson/pull/15914) | cmake: support LINK_ONLY generator expression | millaker | 31d ago | — | MERGEABLE |
| [#15821](https://github.com/mesonbuild/meson/pull/15821) | i18n: add support for passing --no-fuzzy-matching to msgmerg | bluca | 29d ago | — | MERGEABLE |
| [#15930](https://github.com/mesonbuild/meson/pull/15930) | Replace duck typing with protocols for target and CustomTarg | bonzini | 24d ago | — | MERGEABLE |
| [#15812](https://github.com/mesonbuild/meson/pull/15812) | mtest: Add subtest totals to summary | Grillo-0 | 22d ago | — | MERGEABLE |
| [#15529](https://github.com/mesonbuild/meson/pull/15529) | Allow to use deterministic mtime in jar | bmwiedemann | 21d ago | — | MERGEABLE |
| [#15881](https://github.com/mesonbuild/meson/pull/15881) | compiler: correctly mark a run() result as `compiled=False`  | dcbaker | 18d ago | — | MERGEABLE |
| [#15961](https://github.com/mesonbuild/meson/pull/15961) | Add options for Rust compiler features and Cargo.toml [profi | bonzini | 14d ago | — | MERGEABLE |
| [#15958](https://github.com/mesonbuild/meson/pull/15958) | cmake/interpreter: propagate object library pie flag | pobrn | 11d ago | — | MERGEABLE |
| [#14426](https://github.com/mesonbuild/meson/pull/14426) | Bugfix: Generated binaries should not depend on devel packag | hpkfft | 5d ago | CHANGES_REQUESTED | MERGEABLE |
| [#15996](https://github.com/mesonbuild/meson/pull/15996) | tighten the typing of DSL operator implementations | dcbaker | 0d ago | — | MERGEABLE |

---

## Changes requested (57; 52 with no follow-up in 6+ months)

A reviewer asked for changes and, per this metadata, the author hasn't posted a new comment/review since. These are candidates for a nudge, or for closing as abandoned if long stale enough.

### No follow-up in 6+ months (52)

| PR | Title | Author | Since changes requested / last activity |
|---|---|---|---|
| [#5008](https://github.com/mesonbuild/meson/pull/5008) | [WIP]: add SunOS support. | chincheta0815 | 7.3y ago |
| [#6343](https://github.com/mesonbuild/meson/pull/6343) | Add options for overriding default pkg-config directories | lantw44 | 6.2y ago |
| [#7848](https://github.com/mesonbuild/meson/pull/7848) | Add $prefix/$libdir/pkgconfig to PKG_CONFIG_PATH | zeehio | 5.5y ago |
| [#7773](https://github.com/mesonbuild/meson/pull/7773) | dependencies/curses: Fixes curses detection properly on msys2/min | lygstate | 5.5y ago |
| [#8931](https://github.com/mesonbuild/meson/pull/8931) | Automatically added the build dir to include directories in the c | LessiKai | 5.0y ago |
| [#9030](https://github.com/mesonbuild/meson/pull/9030) | find_program: fix search order according to doc | kynzie | 4.9y ago |
| [#9512](https://github.com/mesonbuild/meson/pull/9512) | interpreter: void holder | mensinda | 4.7y ago |
| [#9625](https://github.com/mesonbuild/meson/pull/9625) | Allow building gtkdoc during build | pabloyoyoista | 4.4y ago |
| [#9969](https://github.com/mesonbuild/meson/pull/9969) | Properly error out when cross file is missing a compiler. | jpakkane | 4.4y ago |
| [#10236](https://github.com/mesonbuild/meson/pull/10236) | subprojects: Create `subprojects` directory if missing | otherJL0 | 4.3y ago |
| [#10073](https://github.com/mesonbuild/meson/pull/10073) | Take into account coredata-based args for external projects | tristan957 | 4.1y ago |
| [#9940](https://github.com/mesonbuild/meson/pull/9940) | interpreter: deprecate using an array for project(license:) | dcbaker | 4.1y ago |
| [#10568](https://github.com/mesonbuild/meson/pull/10568) | Add metadata support in shared library version | DieTime | 4.0y ago |
| [#8551](https://github.com/mesonbuild/meson/pull/8551) | Check for, and prefer, pkgconf when looking for pkg-config | dcbaker | 4.0y ago |
| [#6267](https://github.com/mesonbuild/meson/pull/6267) | Wip/jehan/special case set4glib | Jehan | 3.9y ago |
| [#10622](https://github.com/mesonbuild/meson/pull/10622) | Add static analyzer support for gnu. | AmitShukla87622 | 3.9y ago |
| [#8699](https://github.com/mesonbuild/meson/pull/8699) | interpreter: Add dependency_fallbacks() | xclaesse | 3.8y ago |
| [#11008](https://github.com/mesonbuild/meson/pull/11008) | change `mlog.log`s to `mlog.debug`s | djacobs010 | 3.7y ago |
| [#10767](https://github.com/mesonbuild/meson/pull/10767) | Turn on a lot more pylint | dcbaker | 3.4y ago |
| [#11135](https://github.com/mesonbuild/meson/pull/11135) | zsh completion: complete build options, various updates and fixes | bonktree | 3.4y ago |
| [#11425](https://github.com/mesonbuild/meson/pull/11425) | allow unity_size=0 and unity for subprojects | bruchar1 | 3.4y ago |
| [#9257](https://github.com/mesonbuild/meson/pull/9257) | Add -B option to all subcommands that needs a build directory | xclaesse | 3.3y ago |
| [#10607](https://github.com/mesonbuild/meson/pull/10607) | Making $<TARGET_FILE:some_target> work for non imported targets | Volker-Weissmann | 3.3y ago |
| [#11883](https://github.com/mesonbuild/meson/pull/11883) | Fix local unit tests | bruchar1 | 3.1y ago |
| [#12074](https://github.com/mesonbuild/meson/pull/12074) | Update Quick-guide.md | tzugen | 2.9y ago |
| [#11875](https://github.com/mesonbuild/meson/pull/11875) | Fix mypy running on Windows | bruchar1 | 2.8y ago |
| [#11984](https://github.com/mesonbuild/meson/pull/11984) | New 'build' and 'source' bool args for include_directories() | GertyP | 2.8y ago |
| [#12444](https://github.com/mesonbuild/meson/pull/12444) | windows: shorten .res output name to basename.res | dvrogozh | 2.7y ago |
| [#12588](https://github.com/mesonbuild/meson/pull/12588) | Add Perl dependency support | nevapadonak | 2.6y ago |
| [#12669](https://github.com/mesonbuild/meson/pull/12669) | Improve caching of compiler.find_library | petere | 2.4y ago |
| [#12043](https://github.com/mesonbuild/meson/pull/12043) | Support LTO on windows with clang | GertyP | 2.3y ago |
| [#12840](https://github.com/mesonbuild/meson/pull/12840) | Refactor mdist for Mercurial | paugier | 2.3y ago |
| [#7650](https://github.com/mesonbuild/meson/pull/7650) | WIP: Add native pkg-config implementation | xclaesse | 2.3y ago |
| [#12623](https://github.com/mesonbuild/meson/pull/12623) | Allow overriding programs from the command line | tristan957 | 2.2y ago |
| [#12721](https://github.com/mesonbuild/meson/pull/12721) | interpreter: handle multiple dirs in install_emptydir | Hi-Angel | 2.2y ago |
| [#13237](https://github.com/mesonbuild/meson/pull/13237) | Meson support for wxwidgets on Windows added | bilaljo | 2.1y ago |
| [#13384](https://github.com/mesonbuild/meson/pull/13384) | cpp: add support for .tpp file extension | stephanlachnit | 2.0y ago |
| [#13120](https://github.com/mesonbuild/meson/pull/13120) | Improve Swift support | oleavr | 2.0y ago |
| [#13482](https://github.com/mesonbuild/meson/pull/13482) | Add a new kwarg `error_if:` to `warning()` similar to `required:` | nirbheek | 1.9y ago |
| [#9728](https://github.com/mesonbuild/meson/pull/9728) | `dep.get_variable()` for qmake | bb010g | 1.8y ago |
| [#13725](https://github.com/mesonbuild/meson/pull/13725) | refman: make man generator reproducible | Tachi107 | 1.7y ago |
| [#13909](https://github.com/mesonbuild/meson/pull/13909) | dependencies/factory: Skip PkgConfig if pkg-config is not availab | sp1ritCS | 1.6y ago |
| [#9993](https://github.com/mesonbuild/meson/pull/9993) | clike compilers: Add default sysroot include directory | thierryreding | 1.6y ago |
| [#13937](https://github.com/mesonbuild/meson/pull/13937) | Ninja: default pool depth for link.exe | lb90 | 1.6y ago |
| [#13997](https://github.com/mesonbuild/meson/pull/13997) | gnome: Add support for gi-compile-repository for generate_gir | ewlsh | 1.6y ago |
| [#7177](https://github.com/mesonbuild/meson/pull/7177) | gnome: Add support for Valadoc | nielsdg | 1.5y ago |
| [#13960](https://github.com/mesonbuild/meson/pull/13960) | build: Support 'rename' in configure_file, build_target and custo | keith-packard | 1.4y ago |
| [#14225](https://github.com/mesonbuild/meson/pull/14225) | dependencies/jni: Properly resolve jni dependency on android | sp1ritCS | 1.4y ago |
| [#14295](https://github.com/mesonbuild/meson/pull/14295) | interpreter: handle ExternalProgram commands in run_command | alexandre-janniaux | 1.4y ago |
| [#14692](https://github.com/mesonbuild/meson/pull/14692) | zos: initial support for z/OS | AidoP | 1.0y ago |
| [#14513](https://github.com/mesonbuild/meson/pull/14513) | Two meson test improvements for running integration tests | daandemeyer | 357d ago |
| [#11213](https://github.com/mesonbuild/meson/pull/11213) | rust: add new 'object' type crate | bluca | 272d ago |

### More recently active (5)

<details><summary>Show list</summary>

| PR | Title | Author | Last activity |
|---|---|---|---|
| [#14001](https://github.com/mesonbuild/meson/pull/14001) | automatic build requires for  macros.meson | solomoncyj | 149d ago |
| [#13948](https://github.com/mesonbuild/meson/pull/13948) | uninstall: handle elevation to root like minstall | rmader | 18d ago |
| [#15952](https://github.com/mesonbuild/meson/pull/15952) | mtest: warn on TAP unknown lines instead of erroring | mayank-dev-15 | 17d ago |
| [#15462](https://github.com/mesonbuild/meson/pull/15462) | meson2hermetic: the world's premiere build system converter | gurchetansingh | 14d ago |
| [#15982](https://github.com/mesonbuild/meson/pull/15982) | Link against the latest Boost Python version. | jpakkane | 3d ago |

</details>

---

## Merge conflicts with base branch (106; 72 inactive 1+ year)

`mergeable: CONFLICTING` as of this snapshot — needs a rebase before it can be merged. The stale subset (no human activity in over a year, on top of a conflict) are reasonable candidates for closing and asking the author to reopen if still interested.

### Conflicting AND inactive 1+ year (72)

| PR | Title | Author | Last activity |
|---|---|---|---|
| [#4712](https://github.com/mesonbuild/meson/pull/4712) | Avoid some assuptions about using the GNU ld linker | rib | 6.6y ago |
| [#8688](https://github.com/mesonbuild/meson/pull/8688) | Allow C# projects to contain multiple file types | tschoonj | 5.2y ago |
| [#1757](https://github.com/mesonbuild/meson/pull/1757) | i18n: Introduce i18n.files() metedata wrapper | sardemff7 | 4.4y ago |
| [#10202](https://github.com/mesonbuild/meson/pull/10202) | mdist: allow passing options to setup, allow specifying options t | eli-schwartz | 4.2y ago |
| [#10938](https://github.com/mesonbuild/meson/pull/10938) | compilers: Allow overriding a compiler with an external program | xclaesse | 3.7y ago |
| [#11012](https://github.com/mesonbuild/meson/pull/11012) | Draft: external_project: Add kbuild support and build_by_default  | xclaesse | 3.7y ago |
| [#11061](https://github.com/mesonbuild/meson/pull/11061) | custom_target: Deprecate depend_files kwarg | xclaesse | 3.6y ago |
| [#11056](https://github.com/mesonbuild/meson/pull/11056) | Add depend_files argument to generator | touilleMan | 3.6y ago |
| [#11276](https://github.com/mesonbuild/meson/pull/11276) | Warn if has_link_argument() is used for --version-script | xclaesse | 3.5y ago |
| [#11175](https://github.com/mesonbuild/meson/pull/11175) | mconf: hide deprecated options that have no description | Akaricchi | 3.5y ago |
| [#11327](https://github.com/mesonbuild/meson/pull/11327) | Support using generate_gir from gobject-introspection | ylatuya | 3.4y ago |
| [#11390](https://github.com/mesonbuild/meson/pull/11390) | configure_file: Support autoconf format | xclaesse | 3.4y ago |
| [#11279](https://github.com/mesonbuild/meson/pull/11279) | Allow feature options to accept boolean values | dcbaker | 3.4y ago |
| [#11439](https://github.com/mesonbuild/meson/pull/11439) | mdevenv: Add --relocate option | xclaesse | 3.4y ago |
| [#11589](https://github.com/mesonbuild/meson/pull/11589) | `message(var)` with complex types | Volker-Weissmann | 3.3y ago |
| [#11604](https://github.com/mesonbuild/meson/pull/11604) | Allow ```revision``` profiles in wrap | mtribiere | 3.3y ago |
| [#11707](https://github.com/mesonbuild/meson/pull/11707) | WIP: Rust: Make rlib depends on rmeta intermediary output | xclaesse | 3.2y ago |
| [#11771](https://github.com/mesonbuild/meson/pull/11771) | WIP: Typing and refactoring for coredata UserOption | xclaesse | 3.2y ago |
| [#10846](https://github.com/mesonbuild/meson/pull/10846) | Do not drop StructuredSources from internal dependencies | xclaesse | 3.1y ago |
| [#11093](https://github.com/mesonbuild/meson/pull/11093) | qt: Fix tool lookup method | xclaesse | 3.1y ago |
| [#10899](https://github.com/mesonbuild/meson/pull/10899) | Warn when meson.override_find_program() with exe that cannot be r | xclaesse | 3.1y ago |
| [#11354](https://github.com/mesonbuild/meson/pull/11354) | Cleanup envconfig usage | dcbaker | 3.1y ago |
| [#11398](https://github.com/mesonbuild/meson/pull/11398) | qt module: add support for qwaylandscanner | Decodetalkers | 3.1y ago |
| [#11838](https://github.com/mesonbuild/meson/pull/11838) | Rework exception handling through meson main | dcbaker | 3.1y ago |
| [#11848](https://github.com/mesonbuild/meson/pull/11848) | Add ExternalProgram.cmd_array() | tristan957 | 3.1y ago |
| [#11870](https://github.com/mesonbuild/meson/pull/11870) | pkg-config: Allow system program if pkg_config_libdir is set | xclaesse | 3.1y ago |
| [#11931](https://github.com/mesonbuild/meson/pull/11931) | Fix command line vs. native file precedence error on regen | blue42u | 3.0y ago |
| [#11433](https://github.com/mesonbuild/meson/pull/11433) | Refactor compiler check code | xclaesse | 3.0y ago |
| [#11990](https://github.com/mesonbuild/meson/pull/11990) | CI: Cross compile Rust tests | xclaesse | 3.0y ago |
| [#12014](https://github.com/mesonbuild/meson/pull/12014) | Add meson.implementation() method | tristan957 | 3.0y ago |
| [#12059](https://github.com/mesonbuild/meson/pull/12059) | BuildTarget: get_all_link_deps() to get_runtime_dependencies() | xclaesse | 2.9y ago |
| [#11484](https://github.com/mesonbuild/meson/pull/11484) | Add support for runstatedir | wally-mageia | 2.9y ago |
| [#11446](https://github.com/mesonbuild/meson/pull/11446) | mintro: dump ast of subdir meson.build files | bruchar1 | 2.9y ago |
| [#12086](https://github.com/mesonbuild/meson/pull/12086) | Add feature.to_string() | tristan957 | 2.9y ago |
| [#11972](https://github.com/mesonbuild/meson/pull/11972) | Use bindings to libpkgconf, when available | bruchar1 | 2.9y ago |
| [#12064](https://github.com/mesonbuild/meson/pull/12064) | Preliminary command handling cleanup | xclaesse | 2.9y ago |
| [#12071](https://github.com/mesonbuild/meson/pull/12071) | backend: Print warning when using a CustomTarget with multiple ou | xclaesse | 2.9y ago |
| [#12167](https://github.com/mesonbuild/meson/pull/12167) | Add linker detection for older Darwin linkers | cellularmitosis | 2.9y ago |
| [#12207](https://github.com/mesonbuild/meson/pull/12207) | msubprojects: Redirect stdout instead of queueing messages | xclaesse | 2.9y ago |
| [#12079](https://github.com/mesonbuild/meson/pull/12079) | interpreter: Take args as positional argument in test() | xclaesse | 2.8y ago |
| [#12227](https://github.com/mesonbuild/meson/pull/12227) | pkgconfig: Add support for Requires.internal | xclaesse | 2.8y ago |
| [#9611](https://github.com/mesonbuild/meson/pull/9611) | Allow "backend_startup_project" option when not using the VS back | lukester1975 | 2.8y ago |
| [#11400](https://github.com/mesonbuild/meson/pull/11400) | i18n: Do not modify po files nothing changed | xclaesse | 2.8y ago |
| [#12309](https://github.com/mesonbuild/meson/pull/12309) | Use posix paths in devenv's PATH variable | DFOVIT | 2.8y ago |
| [#12319](https://github.com/mesonbuild/meson/pull/12319) | Update options on reconfigure when default_options changes | xclaesse | 2.8y ago |
| [#12358](https://github.com/mesonbuild/meson/pull/12358) | Add an ExperimentalFeature type and use it for cargo | dcbaker | 2.7y ago |
| [#12487](https://github.com/mesonbuild/meson/pull/12487) | ci: Test arm rust cross compilation | xclaesse | 2.7y ago |
| [#12557](https://github.com/mesonbuild/meson/pull/12557) | Normalize File inputs | dcbaker | 2.6y ago |
| [#11675](https://github.com/mesonbuild/meson/pull/11675) | msvc: prevent conversion of -L... options | bruchar1 | 2.5y ago |
| [#12847](https://github.com/mesonbuild/meson/pull/12847) | Use isort, take 2 | dcbaker | 2.4y ago |
| [#12841](https://github.com/mesonbuild/meson/pull/12841) | mdist: Check for git binary in meson dist | pevik | 2.3y ago |
| [#12536](https://github.com/mesonbuild/meson/pull/12536) | rust: Rebuild targets when compiler got updated | xclaesse | 2.2y ago |
| [#13172](https://github.com/mesonbuild/meson/pull/13172) | Do not replace backslashes when joining posix path | bruchar1 | 2.2y ago |
| [#12853](https://github.com/mesonbuild/meson/pull/12853) | Compose Interpreter and State | dcbaker | 2.2y ago |
| [#12756](https://github.com/mesonbuild/meson/pull/12756) | DependencyHolder: add link_args method | stsp | 2.2y ago |
| [#12190](https://github.com/mesonbuild/meson/pull/12190) | python module: Use sys_root's Python sysconfigdata to get EXT_SUF | chewi | 2.2y ago |
| [#12022](https://github.com/mesonbuild/meson/pull/12022) | Start adding `native : 'both'` | dcbaker | 2.1y ago |
| [#13340](https://github.com/mesonbuild/meson/pull/13340) | macros.meson: use setup --reconfigure for in-place builds | keszybz | 2.0y ago |
| [#13396](https://github.com/mesonbuild/meson/pull/13396) | Add support for PGO to rust, fix clang pgo | dcbaker | 2.0y ago |
| [#12154](https://github.com/mesonbuild/meson/pull/12154) | Improve the error reporting in meson | alexandre-janniaux | 1.9y ago |
| [#12780](https://github.com/mesonbuild/meson/pull/12780) | gnome: use the devenv to run g-ir-scanner | ylatuya | 1.8y ago |
| [#13896](https://github.com/mesonbuild/meson/pull/13896) | external-project: Test env kwarg | xclaesse | 1.7y ago |
| [#13861](https://github.com/mesonbuild/meson/pull/13861) | Fix handling of Dependency's include_type in few places | artem | 1.6y ago |
| [#12135](https://github.com/mesonbuild/meson/pull/12135) | Update example to GTK4 | Chasarr | 1.6y ago |
| [#12549](https://github.com/mesonbuild/meson/pull/12549) | Fix linking custom_targets from extract_all_objects in a subproje | arch1t3cht | 1.6y ago |
| [#14209](https://github.com/mesonbuild/meson/pull/14209) | haiku: fix devel lib install path | X547 | 1.4y ago |
| [#12691](https://github.com/mesonbuild/meson/pull/12691) | Add compiler.get_crt() method | bruchar1 | 1.3y ago |
| [#13885](https://github.com/mesonbuild/meson/pull/13885) | Add "meson run" command | xclaesse | 1.2y ago |
| [#11456](https://github.com/mesonbuild/meson/pull/11456) | fs: Add fs.join_absolute() | xclaesse | 1.0y ago |
| [#14713](https://github.com/mesonbuild/meson/pull/14713) | Draft: ExternalDependency: add get_runtime_paths method | lb90 | 1.0y ago |
| [#14760](https://github.com/mesonbuild/meson/pull/14760) | gnome: Cache tools | ZanderBrown | 1.0y ago |
| [#14770](https://github.com/mesonbuild/meson/pull/14770) | Draft: GNOME: A utility for GApplication D-Bus Services | ZanderBrown | 1.0y ago |

### Conflicting, more recently active (34)

<details><summary>Show list</summary>

| PR | Title | Author | Last activity |
|---|---|---|---|
| [#14833](https://github.com/mesonbuild/meson/pull/14833) | Add darwin_dylib_path_policy option | mortie | 350d ago |
| [#14893](https://github.com/mesonbuild/meson/pull/14893) | haiku: fix `executable.export_dynamic` and `dynamic_module` behav | X547 | 334d ago |
| [#14889](https://github.com/mesonbuild/meson/pull/14889) | RFE: feat: Add selinux module | elmarco | 327d ago |
| [#14919](https://github.com/mesonbuild/meson/pull/14919) | Add distconfdir option | JustSoup312 | 326d ago |
| [#14927](https://github.com/mesonbuild/meson/pull/14927) | permit empty `name_suffix` | X547 | 326d ago |
| [#14951](https://github.com/mesonbuild/meson/pull/14951) | Allow explicit selection of Java compiler | jpalus | 319d ago |
| [#14844](https://github.com/mesonbuild/meson/pull/14844) | cuda: Also search `extras/CUPTI` for `cupti` | blue42u | 316d ago |
| [#15003](https://github.com/mesonbuild/meson/pull/15003) | wip: ci: added arm64 image | MaxandreOgeret | 309d ago |
| [#14983](https://github.com/mesonbuild/meson/pull/14983) | Warn when using sh/bash without MSYS2_ENV_CONV_EXCL in run_comman | moi15moi | 294d ago |
| [#15122](https://github.com/mesonbuild/meson/pull/15122) | is_disabler: do not flatten positional args | xclaesse | 266d ago |
| [#13779](https://github.com/mesonbuild/meson/pull/13779) | cargo: Run build.rs to get extra --cfg args | xclaesse | 256d ago |
| [#15176](https://github.com/mesonbuild/meson/pull/15176) | ninja: Fix multiline arguments | xclaesse | 255d ago |
| [#14933](https://github.com/mesonbuild/meson/pull/14933) | [V2 RESEND] gnome: support generate_gir on cross builds | sp1ritCS | 251d ago |
| [#15204](https://github.com/mesonbuild/meson/pull/15204) | C++20 Modules Support for Clang/libc++ | mccakit | 250d ago |
| [#15205](https://github.com/mesonbuild/meson/pull/15205) | C++ import std support for clang/Libc++ | mccakit | 250d ago |
| [#15207](https://github.com/mesonbuild/meson/pull/15207) | cargo: Use library() for C ABI | xclaesse | 249d ago |
| [#13682](https://github.com/mesonbuild/meson/pull/13682) | vsenv: fix ValueError parsing multi-line env variables | ylatuya | 227d ago |
| [#15034](https://github.com/mesonbuild/meson/pull/15034) | Add compiler Diab | per42 | 182d ago |
| [#15197](https://github.com/mesonbuild/meson/pull/15197) | Fix Boost modules with libraries | bredelings | 182d ago |
| [#15303](https://github.com/mesonbuild/meson/pull/15303) | Add local_program() function | xclaesse | 139d ago |
| [#9218](https://github.com/mesonbuild/meson/pull/9218) | Allow as_link_whole() on external dependencies | xclaesse | 134d ago |
| [#15243](https://github.com/mesonbuild/meson/pull/15243) | ci: Run tests against Android NDK | sp1ritCS | 134d ago |
| [#12116](https://github.com/mesonbuild/meson/pull/12116) | python module: Respect PATH when python is not given in machine f | chewi | 116d ago |
| [#15660](https://github.com/mesonbuild/meson/pull/15660) | fix linker args for `lld-link` + `clang-cl` + `flang` | lucascolley | 103d ago |
| [#15691](https://github.com/mesonbuild/meson/pull/15691) | Fix regression in `Requires.private` for library(), and differenc | bonzini | 94d ago |
| [#15598](https://github.com/mesonbuild/meson/pull/15598) | Draft: Android module which can generate apks | sp1ritCS | 58d ago |
| [#14261](https://github.com/mesonbuild/meson/pull/14261) | Mixed Swift/C++ targets support | dblsaiko | 51d ago |
| [#15824](https://github.com/mesonbuild/meson/pull/15824) | CI & test fixes: split libwmf and Qt, update dependencies and ski | mgorny | 49d ago |
| [#15837](https://github.com/mesonbuild/meson/pull/15837) | cargo: Pass env vars in the env when --env-set is not available | nirbheek | 39d ago |
| [#15057](https://github.com/mesonbuild/meson/pull/15057) | mypy: further work on filling in missing types | eli-schwartz | 29d ago |
| [#15933](https://github.com/mesonbuild/meson/pull/15933) | start cleaning up the ast/interpreter.py type mess | bonzini | 21d ago |
| [#15110](https://github.com/mesonbuild/meson/pull/15110) | linkers: don't include absolue RPATH on cross-compiling | Ansuel | 13d ago |
| [#15964](https://github.com/mesonbuild/meson/pull/15964) | Add BuildTarget and Deependency keyword for search directories fo | dcbaker | 13d ago |
| [#15900](https://github.com/mesonbuild/meson/pull/15900) | Move structured sources handling to Build | bonzini | 5d ago |

</details>

---

## Drafts (66; 41 inactive 1+ year)

| PR | Title | Author | Last activity |
|---|---|---|---|
| [#6241](https://github.com/mesonbuild/meson/pull/6241) | Ninja backend: stop doubling backslashes | marc-h38 | 6.6y ago |
| [#6362](https://github.com/mesonbuild/meson/pull/6362) | RFC: what happens when c_args/ld_args come from multiple location | marc-h38 | 6.6y ago |
| [#7901](https://github.com/mesonbuild/meson/pull/7901) | add fs.expand method | bonzini | 5.7y ago |
| [#6967](https://github.com/mesonbuild/meson/pull/6967) | RFC: generator_targets | jpakkane | 5.6y ago |
| [#8181](https://github.com/mesonbuild/meson/pull/8181) | Added workaround for Nvidia HPC SDK OpenMP support | nordmoen | 5.5y ago |
| [#7822](https://github.com/mesonbuild/meson/pull/7822) | Replace ad-hoc find program functionality with centralized, cache | dcbaker | 5.5y ago |
| [#2573](https://github.com/mesonbuild/meson/pull/2573) | Add a decorator to warn on wrong file extension | jeandet | 4.6y ago |
| [#9669](https://github.com/mesonbuild/meson/pull/9669) | gnome module: add global option to choose when to build gtkdoc HT | eli-schwartz | 4.4y ago |
| [#10246](https://github.com/mesonbuild/meson/pull/10246) | Add new message kwargs for status-message logging | ePirat | 4.3y ago |
| [#10498](https://github.com/mesonbuild/meson/pull/10498) | Add @BASENAMES@ and @PLAINNAMES@ to custom_target | dcbaker | 4.1y ago |
| [#9978](https://github.com/mesonbuild/meson/pull/9978) | cmake: add generate_export() | Tachi107 | 4.1y ago |
| [#10690](https://github.com/mesonbuild/meson/pull/10690) | Add page listing Meson usage in proprietary projects. | jpakkane | 3.9y ago |
| [#10674](https://github.com/mesonbuild/meson/pull/10674) | Check for conditionally-inlined compiler builtins | lb90 | 3.9y ago |
| [#7779](https://github.com/mesonbuild/meson/pull/7779) | Add a non-mutable list type for mypy checking | dcbaker | 3.7y ago |
| [#9137](https://github.com/mesonbuild/meson/pull/9137) | Lfortran | HaoZeke | 3.7y ago |
| [#11311](https://github.com/mesonbuild/meson/pull/11311) | feat: support command like qt_add_resources in cmake | Decodetalkers | 3.5y ago |
| [#8203](https://github.com/mesonbuild/meson/pull/8203) | Do not use absolute path to shared libraries that don't have a SO | hwti | 3.4y ago |
| [#7981](https://github.com/mesonbuild/meson/pull/7981) | Add a perl dependency | dcbaker | 3.1y ago |
| [#12097](https://github.com/mesonbuild/meson/pull/12097) | backend: Stop converting all "\" to "/" in command | xclaesse | 2.9y ago |
| [#12138](https://github.com/mesonbuild/meson/pull/12138) | add .git-blame-ignore-revs file to ignore blame for automated com | eli-schwartz | 2.9y ago |
| [#12276](https://github.com/mesonbuild/meson/pull/12276) | dedup linked libs | bruchar1 | 2.8y ago |
| [#12435](https://github.com/mesonbuild/meson/pull/12435) | fix variable substitution for devenv for vscode | bruchar1 | 2.7y ago |
| [#12453](https://github.com/mesonbuild/meson/pull/12453) | gnome: Allow generate_vapi() packages to be deps | nielsdg | 2.6y ago |
| [#12617](https://github.com/mesonbuild/meson/pull/12617) | Make b_pie a feature argument | bonzini | 2.6y ago |
| [#13013](https://github.com/mesonbuild/meson/pull/13013) | RFC: Module to allow for templating custom targets | dcbaker | 2.2y ago |
| [#13165](https://github.com/mesonbuild/meson/pull/13165) | Join paths kwargs | bruchar1 | 2.2y ago |
| [#13134](https://github.com/mesonbuild/meson/pull/13134) | Add specific dependency handling for clang | dcbaker | 2.0y ago |
| [#13687](https://github.com/mesonbuild/meson/pull/13687) | compilers: Pass all options to links/compiles | amcn | 1.8y ago |
| [#13929](https://github.com/mesonbuild/meson/pull/13929) | VS: Add support for /utf-8 | lb90 | 1.6y ago |
| [#13932](https://github.com/mesonbuild/meson/pull/13932) | Add new targets to run rustfmt for Rust projects | bonzini | 1.6y ago |
| [#14026](https://github.com/mesonbuild/meson/pull/14026) | Add start-group/end-group flags when linking a program with rustc | bonzini | 1.6y ago |
| [#14226](https://github.com/mesonbuild/meson/pull/14226) | Updated support for Zig | dcbaker | 1.4y ago |
| [#14257](https://github.com/mesonbuild/meson/pull/14257) | gnome: fix gtkdoc dependencies on static libraries | alyssais | 1.4y ago |
| [#13199](https://github.com/mesonbuild/meson/pull/13199) | Add local and global variable support | dcbaker | 1.3y ago |
| [#11307](https://github.com/mesonbuild/meson/pull/11307) | modules: The 'features' module | seiko2plus | 1.3y ago |
| [#14585](https://github.com/mesonbuild/meson/pull/14585) | modules: Add a module for DSL introspection | dcbaker | 1.2y ago |
| [#14604](https://github.com/mesonbuild/meson/pull/14604) | WIP: qt: properly handle generated sources as inputs for resource | dcbaker | 1.2y ago |
| [#14619](https://github.com/mesonbuild/meson/pull/14619) | Add `qt6.generate_qrc` | JakobDev | 1.1y ago |
| [#13029](https://github.com/mesonbuild/meson/pull/13029) | Dlang: .c and .i files can be processed by D compilers | denizzzka | 1.1y ago |
| [#14684](https://github.com/mesonbuild/meson/pull/14684) | poc: executable_linker_args | matt-sm | 1.1y ago |
| [#14121](https://github.com/mesonbuild/meson/pull/14121) | Add support for building Apple bundles | dblsaiko | 1.1y ago |
| [#15101](https://github.com/mesonbuild/meson/pull/15101) | gnome: Look for new gobject-introspection tools names | xclaesse | 268d ago |
| [#15008](https://github.com/mesonbuild/meson/pull/15008) | compiler: add 'b_time64' base option | dvdhrm | 259d ago |
| [#15157](https://github.com/mesonbuild/meson/pull/15157) | docs: support for QtHelp (qch) documentation book format generati | MatusGuy | 237d ago |
| [#15309](https://github.com/mesonbuild/meson/pull/15309) | wrap: warn on deprecated wraps | bgilbert | 225d ago |
| [#15463](https://github.com/mesonbuild/meson/pull/15463) | WIP: depend on BMI files instead of object files in depaccumulate | dcbaker | 179d ago |
| [#15558](https://github.com/mesonbuild/meson/pull/15558) | Cpp20 modules clang attempt2 | mccakit | 144d ago |
| [#14748](https://github.com/mesonbuild/meson/pull/14748) | Internal IR for compiler args | dcbaker | 137d ago |
| [#15575](https://github.com/mesonbuild/meson/pull/15575) | Swift documentation | dblsaiko | 137d ago |
| [#15577](https://github.com/mesonbuild/meson/pull/15577) | make -isystem behave like -I | bonzini | 133d ago |
| [#12151](https://github.com/mesonbuild/meson/pull/12151) | CI: Cygwin: use a fixed set of packages | jon-turney | 115d ago |
| [#15613](https://github.com/mesonbuild/meson/pull/15613) | Build a shared library for find_library link tests | thesamesam | 102d ago |
| [#15686](https://github.com/mesonbuild/meson/pull/15686) | Draft: gnome: link to libclang_rt.asan_dynamic-x86_64 when using  | Zaburunier | 95d ago |
| [#15755](https://github.com/mesonbuild/meson/pull/15755) | Make meson crosss build  simple | taozuhong | 74d ago |
| [#15766](https://github.com/mesonbuild/meson/pull/15766) | Merge C++, ObjC language arguments | kode54 | 68d ago |
| [#15773](https://github.com/mesonbuild/meson/pull/15773) | docs: Add documentation on LTS support | dcbaker | 67d ago |
| [#15822](https://github.com/mesonbuild/meson/pull/15822) | Sanity for source_Strings_to_files | dcbaker | 53d ago |
| [#15559](https://github.com/mesonbuild/meson/pull/15559) | Cpp23 import std attempt2 | mccakit | 45d ago |
| [#15844](https://github.com/mesonbuild/meson/pull/15844) | Update ci action rebase | bonzini | 44d ago |
| [#14989](https://github.com/mesonbuild/meson/pull/14989) | Add modules support (with order resolution, etc.) and 'import std | germandiagogomez | 43d ago |
| [#15916](https://github.com/mesonbuild/meson/pull/15916) | Allow buildtargets in generator's process function | bonzini | 25d ago |
| [#14462](https://github.com/mesonbuild/meson/pull/14462) | Enhance AIX shared library build to use an export List. | KamathForAIX | 22d ago |
| [#15936](https://github.com/mesonbuild/meson/pull/15936) | [experiment] Validate Any at runtime for Cargo dataclasses | bonzini | 21d ago |
| [#15678](https://github.com/mesonbuild/meson/pull/15678) | type safe option value getters | dcbaker | 17d ago |
| [#15954](https://github.com/mesonbuild/meson/pull/15954) | Make strict_optional opt out for mesonbuild, not opt in | bonzini | 17d ago |
| [#15957](https://github.com/mesonbuild/meson/pull/15957) | Strict null checking part 2 | dcbaker | 14d ago |

---

## Never reviewed or commented on (19)

| PR | Title | Author | Age |
|---|---|---|---|
| [#3408](https://github.com/mesonbuild/meson/pull/3408) | Add 'get_generated_warn_args' (fix #3407) | arteymix | 8.2y |
| [#6831](https://github.com/mesonbuild/meson/pull/6831) | Make headers install better for make dependencies | hwti | 6.3y |
| [#7500](https://github.com/mesonbuild/meson/pull/7500) | Add 'dub_root_path' as dependency argument | deviator | 6.0y |
| [#9386](https://github.com/mesonbuild/meson/pull/9386) | [WIP]: envconfig: Add support for secure operation system | hizukiayaka | 4.7y |
| [#11357](https://github.com/mesonbuild/meson/pull/11357) | Avoid replacing symlinks when installing with --only-changed | mattiasj-axis | 3.4y |
| [#11525](https://github.com/mesonbuild/meson/pull/11525) | Meson manual reorganisation | bruchar1 | 3.3y |
| [#12656](https://github.com/mesonbuild/meson/pull/12656) | add --buildoption argument to introspect | mortie | 2.6y |
| [#12899](https://github.com/mesonbuild/meson/pull/12899) | Add support to rewrite MethodNodes and AssignmentNodes | tobiasdiez | 2.4y |
| [#12990](https://github.com/mesonbuild/meson/pull/12990) | cmake: add append_cmake_args method to subproject options | stephanlachnit | 2.3y |
| [#13232](https://github.com/mesonbuild/meson/pull/13232) | clike compiler args: ignore -Xclang it and whatever comes after i | aleden | 2.1y |
| [#13605](https://github.com/mesonbuild/meson/pull/13605) | utils/vsenv: fix: UnicodeDecodeError: 'gbk' codec can't decode by | Demonese | 1.9y |
| [#13768](https://github.com/mesonbuild/meson/pull/13768) | Add recursive option to as_link_whole | eerii | 1.8y |
| [#13769](https://github.com/mesonbuild/meson/pull/13769) | Add get_link_targets and get_link_whole_targets options to build  | eerii | 1.8y |
| [#13911](https://github.com/mesonbuild/meson/pull/13911) | nasm: Avoid changing multipass optimization levels | Gramner | 1.6y |
| [#13918](https://github.com/mesonbuild/meson/pull/13918) | Enable support for C++23 in clang/ObjC | randomairborne | 1.6y |
| [#14551](https://github.com/mesonbuild/meson/pull/14551) | Add --skip-if-not-found to meson install | julianneswinoga | 1.2y |
| [#15039](https://github.com/mesonbuild/meson/pull/15039) | external_project: fix properties | stsp | 291d |
| [#15983](https://github.com/mesonbuild/meson/pull/15983) | Fix strict null typing issues in symbol extractor script | dcbaker | 4d |
| [#15995](https://github.com/mesonbuild/meson/pull/15995) | mintro: include per-subproject options in buildoptions introspect | MaxandreOgeret | 1d |

---

## Commented on, but never formally reviewed (126; 115 inactive 1+ year)

<details><summary>Show full list</summary>

| PR | Title | Author | Last activity |
|---|---|---|---|
| [#2929](https://github.com/mesonbuild/meson/pull/2929) | Expose a way for distributors to override default directories | TingPing | 8.1y ago |
| [#3913](https://github.com/mesonbuild/meson/pull/3913) | Allow cross file from stdin | bruce-richardson | 7.9y ago |
| [#3361](https://github.com/mesonbuild/meson/pull/3361) | Add module argument to library() | xclaesse | 7.8y ago |
| [#4485](https://github.com/mesonbuild/meson/pull/4485) | Link with runtimeobject.lib by default with MSVC | robUx4 | 7.6y ago |
| [#4421](https://github.com/mesonbuild/meson/pull/4421) | extend implib output support platform (not only windows), and fun | pbl-pw | 7.5y ago |
| [#4799](https://github.com/mesonbuild/meson/pull/4799) | Add 'feature-combo' option type | xclaesse | 7.5y ago |
| [#4786](https://github.com/mesonbuild/meson/pull/4786) | WIP Add dotnet 2.x support for meson | felipealmeida | 7.5y ago |
| [#5346](https://github.com/mesonbuild/meson/pull/5346) | try self.compilers first and then all_compilers | clouds56 | 7.2y ago |
| [#5405](https://github.com/mesonbuild/meson/pull/5405) | i18n: add an update-mini-po target | hanetzer | 7.1y ago |
| [#5441](https://github.com/mesonbuild/meson/pull/5441) | pkgconfig: accept pkgconfig variables with empty value | ueno | 7.1y ago |
| [#5906](https://github.com/mesonbuild/meson/pull/5906) | RFC: Check test case compatible | mine260309 | 6.8y ago |
| [#5994](https://github.com/mesonbuild/meson/pull/5994) | tls_model function attribute support | dcbaker | 6.7y ago |
| [#6136](https://github.com/mesonbuild/meson/pull/6136) | Simplify has_function and fix SDK targeting on macOS | ePirat | 6.6y ago |
| [#6436](https://github.com/mesonbuild/meson/pull/6436) | Prevent passing an invalid linker to gcc. | jameshilliard | 6.5y ago |
| [#6590](https://github.com/mesonbuild/meson/pull/6590) | Use unix style glob patterns to exlcude file and dirs for install | infirit | 6.4y ago |
| [#6664](https://github.com/mesonbuild/meson/pull/6664) | WIP: Add batch get_supported_headers/functions() and parallelize  | xclaesse | 6.4y ago |
| [#6624](https://github.com/mesonbuild/meson/pull/6624) | custom_target: Do substitutions in command while in interpreter | xclaesse | 6.3y ago |
| [#7121](https://github.com/mesonbuild/meson/pull/7121) | build: always use lib prefix for GCC import libraries | yselkowitz | 6.2y ago |
| [#7257](https://github.com/mesonbuild/meson/pull/7257) | fix visual studio additional options for cpp_std. | agokjr | 6.1y ago |
| [#7157](https://github.com/mesonbuild/meson/pull/7157) | WIP: gobject-introspection cross with pkg-config | Ericson2314 | 6.0y ago |
| [#7429](https://github.com/mesonbuild/meson/pull/7429) | [RFC] Add --enable/--disable syntax sugar for features | haasn | 6.0y ago |
| [#7003](https://github.com/mesonbuild/meson/pull/7003) | WIP: Create enum to use instead of strings for language | Ericson2314 | 5.9y ago |
| [#7529](https://github.com/mesonbuild/meson/pull/7529) | WIP: Remove uneeded `parse_cmd_line_options` | Ericson2314 | 5.9y ago |
| [#5267](https://github.com/mesonbuild/meson/pull/5267) | filter and filter_out impl for string lists | jml1795 | 5.9y ago |
| [#7205](https://github.com/mesonbuild/meson/pull/7205) | [RFC] Add 'prebuilt' keyword for gtest/gmock dependencies | falconindy | 5.9y ago |
| [#7685](https://github.com/mesonbuild/meson/pull/7685) | tests: add 'd/12 dub static library' test case | ljmf00 | 5.8y ago |
| [#7914](https://github.com/mesonbuild/meson/pull/7914) | Feature/extend string checks with isupper islower functions | brainelectronics | 5.7y ago |
| [#7079](https://github.com/mesonbuild/meson/pull/7079) | dependency: Add dep.get_include_paths() function. | drmoose | 5.4y ago |
| [#8342](https://github.com/mesonbuild/meson/pull/8342) | Refactor handling of command serialisation | xclaesse | 5.4y ago |
| [#8553](https://github.com/mesonbuild/meson/pull/8553) | Tests: add (broken) override_options test case | MathieuDuponchelle | 5.3y ago |
| [#8610](https://github.com/mesonbuild/meson/pull/8610) | dependencies: Check for pthread.h | xclaesse | 5.3y ago |
| [#8643](https://github.com/mesonbuild/meson/pull/8643) | Add MONO_PATH when running C# executables under Linux or MacOS | steffen-kiess | 5.2y ago |
| [#8654](https://github.com/mesonbuild/meson/pull/8654) | OpenMP: do a compile test before declaring the dependency found | dcbaker | 5.2y ago |
| [#8973](https://github.com/mesonbuild/meson/pull/8973) | mconf: add --fatal-meson-warnings (just as msetup) | Flowdalic | 5.0y ago |
| [#8906](https://github.com/mesonbuild/meson/pull/8906) | fixes coverage with gcovr under Windows | msuesskraut | 5.0y ago |
| [#4324](https://github.com/mesonbuild/meson/pull/4324) | backends: Use raw_link_args to check for the need of RPATH | lantw44 | 4.9y ago |
| [#9173](https://github.com/mesonbuild/meson/pull/9173) | docs: Use a custom hotdoc theme | mensinda | 4.9y ago |
| [#8139](https://github.com/mesonbuild/meson/pull/8139) | Qt: Pass include directories from dependency to moc compiler prop | stream009 | 4.8y ago |
| [#9163](https://github.com/mesonbuild/meson/pull/9163) | compile: Add MESONFLAGS equivalent of MAKEFLAGS | xclaesse | 4.7y ago |
| [#9589](https://github.com/mesonbuild/meson/pull/9589) | Check correct directory for wrap install | piotrrak | 4.6y ago |
| [#9689](https://github.com/mesonbuild/meson/pull/9689) | don't spew pathlib internal state if $HOME is not readable | eli-schwartz | 4.6y ago |
| [#3595](https://github.com/mesonbuild/meson/pull/3595) | WIP: Add 'dlang' module to generate D bindings from GIR | ximion | 4.6y ago |
| [#5206](https://github.com/mesonbuild/meson/pull/5206) | RFC: A way to instantiate custom "feature" objects | Akaricchi | 4.6y ago |
| [#9907](https://github.com/mesonbuild/meson/pull/9907) | partial rollback on clang-tidy that not work as clang-format (fix | mdionisio | 4.4y ago |
| [#6102](https://github.com/mesonbuild/meson/pull/6102) | python: add automatic dependency tracking for scripts | elmarco | 4.4y ago |
| [#10009](https://github.com/mesonbuild/meson/pull/10009) | Add public kwarg to set_variable() | xclaesse | 4.4y ago |
| [#10059](https://github.com/mesonbuild/meson/pull/10059) | compiler/d: add a test case for a shlib linked into a shlib with  | Panke | 4.4y ago |
| [#9342](https://github.com/mesonbuild/meson/pull/9342) | install_man: add support for building man pages via internal cust | eli-schwartz | 4.3y ago |
| [#10177](https://github.com/mesonbuild/meson/pull/10177) | string: Add length() method | 3v1n0 | 4.3y ago |
| [#9170](https://github.com/mesonbuild/meson/pull/9170) | optinterpreter: Normalize options and check for dups | xclaesse | 4.2y ago |
| [#10308](https://github.com/mesonbuild/meson/pull/10308) | Remove deprecated python3 module. | jpakkane | 4.2y ago |
| [#5227](https://github.com/mesonbuild/meson/pull/5227) | Adds ninja all target at each level of build tree | jml1795 | 4.1y ago |
| [#10442](https://github.com/mesonbuild/meson/pull/10442) | mesonbuild: fix ppc64 case for 10.5 and bring ppc/ppc64 trials to | barracuda156 | 4.1y ago |
| [#10534](https://github.com/mesonbuild/meson/pull/10534) | Draft: Fixed cmake2meson.py | Volker-Weissmann | 4.0y ago |
| [#10744](https://github.com/mesonbuild/meson/pull/10744) | Add keyword for setting the mode of a file copied by fs.copyfile  | dcbaker | 3.9y ago |
| [#10833](https://github.com/mesonbuild/meson/pull/10833) | pylint: clean up import order and groupings | dcbaker | 3.8y ago |
| [#10609](https://github.com/mesonbuild/meson/pull/10609) | ci: try to update CI to latest packages | rilian-la-te | 3.8y ago |
| [#10146](https://github.com/mesonbuild/meson/pull/10146) | compilers: add .pxd as a cython header extensions | dcbaker | 3.7y ago |
| [#6099](https://github.com/mesonbuild/meson/pull/6099) | Remove naive dedup across compiler and linker args | Akaricchi | 3.7y ago |
| [#11095](https://github.com/mesonbuild/meson/pull/11095) | Respect method argument of dependency if specified | adriendelsalle | 3.6y ago |
| [#10189](https://github.com/mesonbuild/meson/pull/10189) | Dub dependency configuration | rtbo | 3.6y ago |
| [#11124](https://github.com/mesonbuild/meson/pull/11124) | dependencies: Always force PKG_CONFIG_ALLOW_SYSTEM_CFLAGS | amyspark | 3.6y ago |
| [#5789](https://github.com/mesonbuild/meson/pull/5789) | gnome: prefer glib-genmarshal location from pkg-config | stapelberg | 3.5y ago |
| [#11343](https://github.com/mesonbuild/meson/pull/11343) | Set vcproj's default workdir and args based on a matching test. | lukester1975 | 3.5y ago |
| [#11222](https://github.com/mesonbuild/meson/pull/11222) | Tests handle external meson | eli-schwartz | 3.4y ago |
| [#11287](https://github.com/mesonbuild/meson/pull/11287) | delete unused unity files | bruchar1 | 3.4y ago |
| [#11474](https://github.com/mesonbuild/meson/pull/11474) | simd: Detect NEON on AArch64 | entrope | 3.4y ago |
| [#10271](https://github.com/mesonbuild/meson/pull/10271) | coredata: Abort when setting value on yielding option | xclaesse | 3.3y ago |
| [#10520](https://github.com/mesonbuild/meson/pull/10520) | Set project(meson_version : ) to default to 0.37 | dcbaker | 3.3y ago |
| [#10195](https://github.com/mesonbuild/meson/pull/10195) | compiler.find_library: Also search lib dirs from link_args | blue42u | 3.3y ago |
| [#3588](https://github.com/mesonbuild/meson/pull/3588) | Make language kwarg optional for add_*_link_arguments() | xclaesse | 3.1y ago |
| [#8124](https://github.com/mesonbuild/meson/pull/8124) | WIP: externalproject: Add program() method | xclaesse | 3.1y ago |
| [#8625](https://github.com/mesonbuild/meson/pull/8625) | Add missing rpath when using link_whole | xclaesse | 3.1y ago |
| [#10242](https://github.com/mesonbuild/meson/pull/10242) | find_program: Add from_dependency kwarg | xclaesse | 3.1y ago |
| [#11769](https://github.com/mesonbuild/meson/pull/11769) | Sort commands in the --help output alphabetically | whot | 3.0y ago |
| [#10064](https://github.com/mesonbuild/meson/pull/10064) | WIP: Add meson install --dbg | xclaesse | 2.9y ago |
| [#12287](https://github.com/mesonbuild/meson/pull/12287) | Add a `file_argument` function | dcbaker | 2.7y ago |
| [#12432](https://github.com/mesonbuild/meson/pull/12432) | add devenv to introspection data | bruchar1 | 2.7y ago |
| [#12281](https://github.com/mesonbuild/meson/pull/12281) | Remove include_directories absolute path validation | GertyP | 2.6y ago |
| [#10989](https://github.com/mesonbuild/meson/pull/10989) | change paths section to built-in options section | djacobs010 | 2.6y ago |
| [#11918](https://github.com/mesonbuild/meson/pull/11918) | linker: support "zig cc" | motiejus | 2.6y ago |
| [#12573](https://github.com/mesonbuild/meson/pull/12573) | Don't link to pgmath with armflang | matz-e | 2.6y ago |
| [#12642](https://github.com/mesonbuild/meson/pull/12642) | Add malloc debug support on macOS | petere | 2.6y ago |
| [#12694](https://github.com/mesonbuild/meson/pull/12694) | vsenv: check the version of vswhere and raise an error if it is t | eli-schwartz | 2.5y ago |
| [#12657](https://github.com/mesonbuild/meson/pull/12657) | Fix / CMake custom targets can output directories, not just files | markmaker | 2.5y ago |
| [#12734](https://github.com/mesonbuild/meson/pull/12734) | Support for Orc files | turran | 2.4y ago |
| [#12646](https://github.com/mesonbuild/meson/pull/12646) | Fix coverage with lcov 2.0 and uncovered folders | alekrudnik | 2.4y ago |
| [#12732](https://github.com/mesonbuild/meson/pull/12732) | Replace debug option with debuginfo | bruchar1 | 2.4y ago |
| [#12776](https://github.com/mesonbuild/meson/pull/12776) | use host gobject-introspection-1.0.pc for looking up g-ir-scanner | josch | 2.4y ago |
| [#12699](https://github.com/mesonbuild/meson/pull/12699) | Update buildtype from debug and optimization | bruchar1 | 2.4y ago |
| [#13000](https://github.com/mesonbuild/meson/pull/13000) | Improved detection of external program version. | Machapet | 2.3y ago |
| [#13122](https://github.com/mesonbuild/meson/pull/13122) | interpreter: Fix dependency(..., modules: x) fallback | oleavr | 2.2y ago |
| [#13124](https://github.com/mesonbuild/meson/pull/13124) | doc/Threads: avoid `dependency('threads')` with MinGW + Win32 thr | bgilbert | 2.2y ago |
| [#12708](https://github.com/mesonbuild/meson/pull/12708) | fix an issue where -isystem parameter could be removed incorrectl | roothide | 2.1y ago |
| [#13464](https://github.com/mesonbuild/meson/pull/13464) | Use werror for gnome.generate_gir(fatal_warnings:) | tristan957 | 2.0y ago |
| [#13511](https://github.com/mesonbuild/meson/pull/13511) | clike: Add F77 snippet for underscore_prefix check | HaoZeke | 1.9y ago |
| [#13576](https://github.com/mesonbuild/meson/pull/13576) | Implement SYSTEM handler for `cmake` dependencies. | luigifcruz | 1.9y ago |
| [#13612](https://github.com/mesonbuild/meson/pull/13612) | Can make deprecations into hard errors based on version. | jpakkane | 1.9y ago |
| [#13262](https://github.com/mesonbuild/meson/pull/13262) | Defer evaluating ModuleState.project_version | QuLogic | 1.8y ago |
| [#10556](https://github.com/mesonbuild/meson/pull/10556) | Make --help output more consistent and narrower | keszybz | 1.8y ago |
| [#9229](https://github.com/mesonbuild/meson/pull/9229) | gnome: Fix expand-content-files in gtkdoc generation | inigomartinez | 1.8y ago |
| [#12906](https://github.com/mesonbuild/meson/pull/12906) | meson subprojects: add status and gitignore commands | gerion0 | 1.7y ago |
| [#13831](https://github.com/mesonbuild/meson/pull/13831) | add basic support for rgbds assembly | terinjokes | 1.7y ago |
| [#13873](https://github.com/mesonbuild/meson/pull/13873) | Add .po file creation to Localization doc | ferdnyc | 1.6y ago |
| [#14040](https://github.com/mesonbuild/meson/pull/14040) | Support for UEFI target | RossComputerGuy | 1.5y ago |
| [#14190](https://github.com/mesonbuild/meson/pull/14190) | symbolextractor: detect DLL name with llvm-nm/nm | robUx4 | 1.4y ago |
| [#14044](https://github.com/mesonbuild/meson/pull/14044) | Add support for .hg_archival.txt to detect_vcs | grimmy | 1.4y ago |
| [#9494](https://github.com/mesonbuild/meson/pull/9494) | WIP: Paralellize some compiler checks | xclaesse | 1.3y ago |
| [#14119](https://github.com/mesonbuild/meson/pull/14119) | find_program: add a kwarg to skip searching the source dir | pks-t | 1.2y ago |
| [#14311](https://github.com/mesonbuild/meson/pull/14311) | mtest: improve interrupting tests on Win32 | pks-t | 1.2y ago |
| [#14567](https://github.com/mesonbuild/meson/pull/14567) | Remove CODEOWNERS | bruchar1 | 1.2y ago |
| [#14102](https://github.com/mesonbuild/meson/pull/14102) | Allow for cmake w-flags addition | ligazetom | 1.2y ago |
| [#8386](https://github.com/mesonbuild/meson/pull/8386) | Summarize passed subtests even on overall failure | ldrumm | 1.1y ago |
| [#14676](https://github.com/mesonbuild/meson/pull/14676) | Add `qt6.find_tool` | JakobDev | 1.1y ago |
| [#14445](https://github.com/mesonbuild/meson/pull/14445) | fix(dependencies:python): Use python{vernum}_d.lib in MSVC debug  | zicowarn | 1.0y ago |
| [#14817](https://github.com/mesonbuild/meson/pull/14817) | [cmake] Properly handle OSX -framework in target_link_libraries | TheRealEfaust | 356d ago |
| [#15095](https://github.com/mesonbuild/meson/pull/15095) | Workaround typelib generation for vala libraries | albfan | 275d ago |
| [#13344](https://github.com/mesonbuild/meson/pull/13344) | coverage: Ignore errors (lcov2.0) | ewalkusx | 241d ago |
| [#4393](https://github.com/mesonbuild/meson/pull/4393) | Stop "fixing" command line in CustomTargets again. | QuLogic | 172d ago |
| [#15390](https://github.com/mesonbuild/meson/pull/15390) | boost: allow headers only installation | sgn | 140d ago |
| [#12891](https://github.com/mesonbuild/meson/pull/12891) | Add a system dependency for numpy | rgommers | 126d ago |
| [#15737](https://github.com/mesonbuild/meson/pull/15737) | ast/interpreter: Use match statements | dcbaker | 47d ago |
| [#14699](https://github.com/mesonbuild/meson/pull/14699) | SharedModule should not generate import lib | bruchar1 | 30d ago |
| [#15623](https://github.com/mesonbuild/meson/pull/15623) | Resolves bug #15560 - evaluate qt dependencies without qt framewo | boulette42 | 21d ago |
| [#15949](https://github.com/mesonbuild/meson/pull/15949) | msetup: honor b_colorout option for setup output color | mayank-dev-15 | 16d ago |
| [#15970](https://github.com/mesonbuild/meson/pull/15970) | universal.py: search_version: make the version regex a bit more r | jmarcoscosta | 4d ago |

</details>

---

## Reviewed, other state (COMMENTED/DISMISSED reviews, no clear decision) (104)

<details><summary>Show full list</summary>

| PR | Title | Author | Last activity | Review states seen |
|---|---|---|---|---|
| [#2092](https://github.com/mesonbuild/meson/pull/2092) | vala: Extend the GIR test to include 'install_dir' and  | arteymix | 8.8y ago | COMMENTED |
| [#3402](https://github.com/mesonbuild/meson/pull/3402) | Check for header folder and add rpath for macOS framewo | Breakthru | 8.1y ago | COMMENTED |
| [#3891](https://github.com/mesonbuild/meson/pull/3891) | Developer documentation | behlec | 7.8y ago | COMMENTED |
| [#3557](https://github.com/mesonbuild/meson/pull/3557) | Add include() function | BeChris | 7.4y ago | COMMENTED |
| [#4747](https://github.com/mesonbuild/meson/pull/4747) | Add support for symbol visibility export files | jpakkane | 7.1y ago | COMMENTED |
| [#4991](https://github.com/mesonbuild/meson/pull/4991) | [WIP] CUDA dependency support | obilaniu | 7.1y ago | COMMENTED |
| [#5713](https://github.com/mesonbuild/meson/pull/5713) | Add metadata to project | thiblahute | 6.9y ago | COMMENTED |
| [#5954](https://github.com/mesonbuild/meson/pull/5954) | New built-in option `b_debuginfo` | agurtovoy | 6.8y ago | COMMENTED |
| [#4973](https://github.com/mesonbuild/meson/pull/4973) | gnome.generate_gir: allow to specify python executable | nachogarglez | 6.7y ago | COMMENTED |
| [#5305](https://github.com/mesonbuild/meson/pull/5305) | compilers/c: fix clang-cl openmp | dcbaker | 6.7y ago | APPROVED |
| [#6258](https://github.com/mesonbuild/meson/pull/6258) | Depend on the .vapi files of each library to build a ta | tintou | 6.6y ago | COMMENTED |
| [#5071](https://github.com/mesonbuild/meson/pull/5071) | WIP: interpreter: warn if a cross property default valu | rossburton | 6.5y ago | APPROVED |
| [#6905](https://github.com/mesonbuild/meson/pull/6905) | gnome.gtkdoc(): Pass --html-dir to fixxref | jtojnar | 6.2y ago | COMMENTED |
| [#7065](https://github.com/mesonbuild/meson/pull/7065) | Rework vcs_tag to better handle disablers in command/fa | jameshilliard | 6.2y ago | COMMENTED |
| [#3865](https://github.com/mesonbuild/meson/pull/3865) | Add include_symbols argument to build targets | torokati44 | 6.1y ago | COMMENTED |
| [#5967](https://github.com/mesonbuild/meson/pull/5967) | ExternalProgram: do not log locally found programs | elmarco | 5.9y ago | COMMENTED |
| [#6367](https://github.com/mesonbuild/meson/pull/6367) | Properly handle the case of linking static library with | yshui | 5.8y ago | COMMENTED |
| [#5854](https://github.com/mesonbuild/meson/pull/5854) | Compilers: Add support for b_sanitize to the ClangCL co | dcbaker | 5.7y ago | COMMENTED |
| [#6798](https://github.com/mesonbuild/meson/pull/6798) | Site-wide native file configuration | dcbaker | 5.5y ago | COMMENTED |
| [#7845](https://github.com/mesonbuild/meson/pull/7845) | compilers/d: Correctly pass shared libraries to DMD and | dcbaker | 5.4y ago | COMMENTED |
| [#8607](https://github.com/mesonbuild/meson/pull/8607) | wrap: Use Linux path separator even on Windows for wrap | seungha-yang | 5.2y ago | COMMENTED |
| [#8782](https://github.com/mesonbuild/meson/pull/8782) | Fail upon encountering unknown options, add --allow-unk | Flowdalic | 5.1y ago | COMMENTED |
| [#7518](https://github.com/mesonbuild/meson/pull/7518) | Meson AppImage releases | mensinda | 4.8y ago | COMMENTED |
| [#9324](https://github.com/mesonbuild/meson/pull/9324) | Fix CPU detection on iOS | Torrekie | 4.8y ago | COMMENTED |
| [#9526](https://github.com/mesonbuild/meson/pull/9526) | vs: Add b_vstoolset parameter to support setting vs too | deadash | 4.7y ago | COMMENTED |
| [#8895](https://github.com/mesonbuild/meson/pull/8895) | Improve Error message of invalid user build option | GithubMaddin | 4.6y ago | COMMENTED |
| [#9453](https://github.com/mesonbuild/meson/pull/9453) | Restore the possibility of forcing "fat" static library | obilaniu | 4.6y ago | COMMENTED |
| [#7733](https://github.com/mesonbuild/meson/pull/7733) | Add support for linking against static Qt install. Reso | hdhauk | 4.5y ago | APPROVED, COMMENTED |
| [#10056](https://github.com/mesonbuild/meson/pull/10056) | mpi: fix usage of intel-mpi installed via spack | dguibert | 4.4y ago | COMMENTED |
| [#9784](https://github.com/mesonbuild/meson/pull/9784) | Fix order of paths passed to applications running with  | rhabacker | 4.3y ago | COMMENTED |
| [#9372](https://github.com/mesonbuild/meson/pull/9372) | Add  a module of xorg helpers | dcbaker | 4.3y ago | COMMENTED |
| [#10272](https://github.com/mesonbuild/meson/pull/10272) | Add include-what-you-use usage info to FAQ | alex-tee | 4.2y ago | COMMENTED |
| [#10428](https://github.com/mesonbuild/meson/pull/10428) | find_library: Add has_headers include dirs if available | nirbheek | 4.1y ago | COMMENTED |
| [#10686](https://github.com/mesonbuild/meson/pull/10686) | Add kwarg to disable warning about built-in options | mkoncek | 3.9y ago | COMMENTED |
| [#5859](https://github.com/mesonbuild/meson/pull/5859) | Add --cross-file-constant and --native-file-constant ar | xclaesse | 3.8y ago | COMMENTED |
| [#10733](https://github.com/mesonbuild/meson/pull/10733) | Freebsd ci | eli-schwartz | 3.8y ago | COMMENTED |
| [#11001](https://github.com/mesonbuild/meson/pull/11001) | allow empty `name_suffix` | X547 | 3.7y ago | COMMENTED |
| [#10893](https://github.com/mesonbuild/meson/pull/10893) | Iccrl78 support | gall1 | 3.6y ago | COMMENTED |
| [#9865](https://github.com/mesonbuild/meson/pull/9865) | Clarify compiler check argument ignores | ePirat | 3.6y ago | COMMENTED |
| [#11419](https://github.com/mesonbuild/meson/pull/11419) | Documentation update for find_program with subprojects | telegraphic | 3.4y ago | COMMENTED |
| [#10642](https://github.com/mesonbuild/meson/pull/10642) | Add option to generate profile information | andy5995 | 3.3y ago | COMMENTED |
| [#11489](https://github.com/mesonbuild/meson/pull/11489) | correctly handle rebuild dependencies on LINGUAS | eli-schwartz | 3.3y ago | COMMENTED |
| [#11491](https://github.com/mesonbuild/meson/pull/11491) | Add subprojects syncwrap command | DFOVIT | 3.3y ago | COMMENTED |
| [#9357](https://github.com/mesonbuild/meson/pull/9357) | WIP: interpreter: don't flip user-specified 'auto' with | havardgraff | 3.3y ago | COMMENTED |
| [#11683](https://github.com/mesonbuild/meson/pull/11683) | devenv: generates the dump file in the workdir | dabrain34 | 3.2y ago | COMMENTED |
| [#3520](https://github.com/mesonbuild/meson/pull/3520) | BuildTarget: Add ignore_project_(link_)args() kwarg | xclaesse | 3.1y ago | COMMENTED |
| [#7513](https://github.com/mesonbuild/meson/pull/7513) | Fix wrap file and machine file syntax inconsistency | xclaesse | 3.1y ago | COMMENTED |
| [#9622](https://github.com/mesonbuild/meson/pull/9622) | Cleanup the dlang module and add annotations | dcbaker | 3.1y ago | COMMENTED |
| [#11885](https://github.com/mesonbuild/meson/pull/11885) | modules/features: Add a module of functions for complex | dcbaker | 3.1y ago | COMMENTED |
| [#11912](https://github.com/mesonbuild/meson/pull/11912) | Add a prefix keyword argument to typeslistify | dcbaker | 3.0y ago | COMMENTED |
| [#11780](https://github.com/mesonbuild/meson/pull/11780) | qt.compile_moc ignores system includes | lanedis | 3.0y ago | COMMENTED |
| [#11946](https://github.com/mesonbuild/meson/pull/11946) | Forward werror to clang-tidy | kiwixz | 3.0y ago | APPROVED, COMMENTED |
| [#11932](https://github.com/mesonbuild/meson/pull/11932) | cmake: Compare whole paths instead of just filenames | Volker-Weissmann | 2.9y ago | COMMENTED |
| [#12019](https://github.com/mesonbuild/meson/pull/12019) | cmake: add libraries from dependencies in the cmake-fil | kiwixz | 2.9y ago | COMMENTED |
| [#9228](https://github.com/mesonbuild/meson/pull/9228) | Patch dir names independent from subprojects dir names | xggrnx | 2.9y ago | COMMENTED |
| [#11485](https://github.com/mesonbuild/meson/pull/11485) | mintro: allow argument to be source dir | bruchar1 | 2.9y ago | COMMENTED |
| [#12299](https://github.com/mesonbuild/meson/pull/12299) | Hack `resolve_cmake_trace_targets` to fix pytorch linki | zasdfgbnm | 2.7y ago | APPROVED |
| [#12375](https://github.com/mesonbuild/meson/pull/12375) | Force posix_prefix sysconfig scheme on Homebrew | robtaylor | 2.7y ago | COMMENTED |
| [#11191](https://github.com/mesonbuild/meson/pull/11191) | CMake: TraceTargets: Don't assume valid library list | blobfish | 2.7y ago | COMMENTED |
| [#12503](https://github.com/mesonbuild/meson/pull/12503) | qt module: add support for external tool specification | dv1 | 2.7y ago | COMMENTED |
| [#12362](https://github.com/mesonbuild/meson/pull/12362) | add skip kw to test function | bruchar1 | 2.6y ago | COMMENTED |
| [#12428](https://github.com/mesonbuild/meson/pull/12428) | gnome.compile_resources: support using generated lists | v1993 | 2.5y ago | COMMENTED |
| [#12809](https://github.com/mesonbuild/meson/pull/12809) | Add `find_framework()` method to compiler object | judemille | 2.4y ago | COMMENTED |
| [#12887](https://github.com/mesonbuild/meson/pull/12887) | Improve the test for a bug in Python module | bruchar1 | 2.4y ago | COMMENTED |
| [#12764](https://github.com/mesonbuild/meson/pull/12764) | docs: show "Returned by" for objects returned in lists | blmaier | 2.4y ago | COMMENTED |
| [#12873](https://github.com/mesonbuild/meson/pull/12873) | Materialize strings to generated sources in custom_targ | dcbaker | 2.4y ago | APPROVED, COMMENTED |
| [#9021](https://github.com/mesonbuild/meson/pull/9021) | pkg-config dependency consistency | xclaesse | 2.3y ago | COMMENTED |
| [#10122](https://github.com/mesonbuild/meson/pull/10122) | Store include and compile arguments separately in non-i | dcbaker | 2.2y ago | COMMENTED |
| [#13075](https://github.com/mesonbuild/meson/pull/13075) | dependencies/openmp: more robust check for Fortran | dcbaker | 2.2y ago | COMMENTED |
| [#12837](https://github.com/mesonbuild/meson/pull/12837) | Add section on modifying source archives to "Creating r | rgommers | 2.2y ago | COMMENTED |
| [#13032](https://github.com/mesonbuild/meson/pull/13032) | Allow -Dunity_size=-1 to generate one unity file per la | dcbaker | 2.2y ago | APPROVED, COMMENTED |
| [#7174](https://github.com/mesonbuild/meson/pull/7174) | Query the threading model from dependency('threads') | dcbaker | 2.2y ago | COMMENTED |
| [#13040](https://github.com/mesonbuild/meson/pull/13040) | Allow custom_target and generator to accept include_dir | dcbaker | 2.2y ago | COMMENTED |
| [#12170](https://github.com/mesonbuild/meson/pull/12170) | Use HOMEBREW_PREFIX for searching if it's set | robtaylor | 2.2y ago | COMMENTED |
| [#12155](https://github.com/mesonbuild/meson/pull/12155) | gnome: propagate 'include_directories' also to the type | pbor | 2.1y ago | APPROVED |
| [#13450](https://github.com/mesonbuild/meson/pull/13450) | Fix llvm-rc Matching Error | CaptainNeil | 2.0y ago | COMMENTED |
| [#13493](https://github.com/mesonbuild/meson/pull/13493) | linkers: Disable -rpath-link with ld.zigcc | RossComputerGuy | 1.9y ago | COMMENTED |
| [#13105](https://github.com/mesonbuild/meson/pull/13105) | compilers: Use a dataclass instead of tuple for cached  | dcbaker | 1.8y ago | COMMENTED |
| [#13674](https://github.com/mesonbuild/meson/pull/13674) | [tools] Fixed the Lexer of cmake2meson | shouhuanxiaoji | 1.8y ago | COMMENTED |
| [#9904](https://github.com/mesonbuild/meson/pull/9904) | modules/python: Deprecate find_installation without pos | jtojnar | 1.8y ago | COMMENTED |
| [#13377](https://github.com/mesonbuild/meson/pull/13377) | Fix full dependencies that should be order only in ninj | dcbaker | 1.8y ago | APPROVED, COMMENTED |
| [#13439](https://github.com/mesonbuild/meson/pull/13439) | Cleanups and Speedup for python unittests | dcbaker | 1.8y ago | COMMENTED |
| [#13839](https://github.com/mesonbuild/meson/pull/13839) | If invalid value given to clone-recursive, raise except | andy5995 | 1.7y ago | COMMENTED |
| [#9468](https://github.com/mesonbuild/meson/pull/9468) | Delete static library archives also on Windows | lb90 | 1.6y ago | COMMENTED |
| [#13842](https://github.com/mesonbuild/meson/pull/13842) | test cases/linuxlike/14 static dynamic linkage: Add mat | dememax | 1.6y ago | COMMENTED |
| [#13958](https://github.com/mesonbuild/meson/pull/13958) | Test fixes for Windows | lb90 | 1.6y ago | COMMENTED |
| [#14018](https://github.com/mesonbuild/meson/pull/14018) | Simplify and clean up some of the logic around finding  | dcbaker | 1.6y ago | COMMENTED |
| [#13953](https://github.com/mesonbuild/meson/pull/13953) | Introduce user-defined wrapdb source | klokik | 1.5y ago | COMMENTED |
| [#14076](https://github.com/mesonbuild/meson/pull/14076) | Support DiaSDK for cross-compiling with mstorsjo/msvc-w | vid512 | 1.4y ago | COMMENTED |
| [#11862](https://github.com/mesonbuild/meson/pull/11862) | Add support for LLVM's wasm-ld | GuilleX7 | 1.4y ago | COMMENTED |
| [#14318](https://github.com/mesonbuild/meson/pull/14318) | Honor includes in partial_dependency of externals depen | bruchar1 | 1.3y ago | COMMENTED |
| [#13128](https://github.com/mesonbuild/meson/pull/13128) | add support for fstring-like identity-expressions in st | akaessens | 1.3y ago | COMMENTED |
| [#14573](https://github.com/mesonbuild/meson/pull/14573) | Fix hash() and __eq__() for File object | daandemeyer | 1.2y ago | COMMENTED |
| [#14572](https://github.com/mesonbuild/meson/pull/14572) | Print environment variables in log for autoconf subproj | tobiasdiez | 1.2y ago | COMMENTED |
| [#13425](https://github.com/mesonbuild/meson/pull/13425) | _pathlib: fix missing PosixPath/WindowsPath on Windows | lazka | 361d ago | COMMENTED |
| [#14381](https://github.com/mesonbuild/meson/pull/14381) | qt module: look for qt tools only on build machine | QSchulz | 309d ago | COMMENTED |
| [#14643](https://github.com/mesonbuild/meson/pull/14643) | interpreter: add dependency.as_dict() | virtuald | 277d ago | COMMENTED |
| [#15151](https://github.com/mesonbuild/meson/pull/15151) | dependencies/cuda: Add support for disabling the cuda r | dcbaker | 261d ago | APPROVED, COMMENTED |
| [#14176](https://github.com/mesonbuild/meson/pull/14176) | python: add `limited_api` kwarg to `find_installation() | lgarrison | 241d ago | COMMENTED |
| [#14493](https://github.com/mesonbuild/meson/pull/14493) | Unstable gobuild module | antonysigma | 211d ago | COMMENTED |
| [#15714](https://github.com/mesonbuild/meson/pull/15714) | compilers: force clang to error on unknown warning opti | tristan957 | 84d ago | COMMENTED |
| [#2491](https://github.com/mesonbuild/meson/pull/2491) | Add color option | liugang | 16d ago | COMMENTED |
| [#15951](https://github.com/mesonbuild/meson/pull/15951) | envconfig: warn on unknown system in cross files | mayank-dev-15 | 11d ago | COMMENTED |
| [#15966](https://github.com/mesonbuild/meson/pull/15966) | Clean up the calling interface of the Optintepreter | dcbaker | 10d ago | COMMENTED |

</details>

---

## PRs competing for the same target issue (2)

Detected by scanning PR bodies for `Fixes #N` / `Closes #N` / `Resolves #N` references and finding issue numbers claimed by more than one open PR.

| PR | Title | Author | Target issue | Bucket |
|---|---|---|---|---|
| [#8782](https://github.com/mesonbuild/meson/pull/8782) | Fail upon encountering unknown options, add --allow-unk | Flowdalic | #7288 | Reviewed (other state) |
| [#8973](https://github.com/mesonbuild/meson/pull/8973) | mconf: add --fatal-meson-warnings (just as msetup) | Flowdalic | #7288 | Commented on, but no formal review |

---
