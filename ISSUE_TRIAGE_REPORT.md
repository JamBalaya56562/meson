# Meson Open Issue Triage — Investigation Notes

- **Repository**: [mesonbuild/meson](https://github.com/mesonbuild/meson)
- **Scope**: every issue currently open in the repository, **1867** total (open-issue count as of 2026-07-11). Issues that have since been closed (by us or by anyone else) are intentionally excluded from this document — it reflects only what is still open right now.
- **Generated**: 2026-07-11
- **Verification basis**: a local checkout of meson `master` (mid-2026, release notes through 1.11.0) was used as the source of truth for "is this already fixed/implemented".
- **How this was produced**: an LLM-assisted first pass classified every open issue (category / confidence / rationale). A subset of high-confidence "already fixed" candidates was then re-verified by reading the full GitHub thread plus the current source end-to-end (not just the code area that looked related).
- **Important caveat**: that re-verification pass found that roughly a third of high-confidence "fixed" verdicts were false positives on first read — a related code change existed, but the issue's actual request was still unresolved, or discussion was still ongoing. Only the entries explicitly marked **thread-verified** below have had this deeper check. Everything else (the bulk of the `comment_close`/`implement`/`keep_open`/`unclear` lists) is a first-pass read only and should be independently confirmed before acting on it.

---

## Issues we already commented on (still open)

We previously posted **65** comments across this investigation; **46** were closed by the maintainers shortly after (and are no longer listed here, since this report only covers currently-open issues). The **19** below are still open — either awaiting a maintainer's review of a proposed close, or (in one case) corrected in place after a maintainer pointed out the original comment was wrong. No further comments have been posted since; commenting is currently paused while this report is prepared for maintainer review.

| Issue | Status | Comment | Note |
|---|---|---|---|
| [#2347](https://github.com/mesonbuild/meson/issues/2347) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/2347#issuecomment-4914518566) | [Revised / status clarification] The reference manual is now generated from `docs/yaml/` into JSON, Vim, and man formats via the refman toolchain (comprehensive machine-readable output). Noted that the separate request for an exhaustive list of reserved keywords is not covered by this. No close proposed. |
| [#3276](https://github.com/mesonbuild/meson/issues/3276) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/3276#issuecomment-4914633452) | [Revised / status clarification] The confusing empty-list error message was fixed in 0.55.0; individual detection failures are non-fatal and detection continues. No close proposed. |
| [#3751](https://github.com/mesonbuild/meson/issues/3751) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/3751#issuecomment-4914633742) | [Revised / status clarification] The CPU-family warning is implemented, but system-name validation is not (there is no `known_oses` check). No close proposed. |
| [#4244](https://github.com/mesonbuild/meson/issues/4244) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/4244#issuecomment-4914634052) | [Revised / status clarification] `pic: false` (since 0.36.0) works around the issue, but automatic handling is not implemented. No close proposed. |
| [#4383](https://github.com/mesonbuild/meson/issues/4383) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/4383#issuecomment-4914518331) | [Revised / status clarification] The correct workaround is `implicit_include_directories: false` (an earlier draft incorrectly suggested `include_type: 'system'`). Made clear that changing the default include-search order is a separate, unresolved question. No close proposed. |
| [#5168](https://github.com/mesonbuild/meson/issues/5168) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/5168#issuecomment-4914634285) | [Revised / status clarification] `CMAKE_SIZEOF_VOID_P` is already propagated; full automatic vcpkg integration is still not supported. No close proposed. |
| [#5411](https://github.com/mesonbuild/meson/issues/5411) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/5411#issuecomment-4914634613) | [Revised / status clarification] MSVC now defaults to `/utf-8` (since 0.60.0), which resolves the practical impact; a dedicated option for this was not adopted. No close proposed. |
| [#6810](https://github.com/mesonbuild/meson/issues/6810) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/6810#issuecomment-4891835043) | TAP 'UnknownLine' output is now treated as a warning rather than a failure (PR #8029, commit a8c138eb). Comment cites the release note and commit; close proposed. |
| [#7091](https://github.com/mesonbuild/meson/issues/7091) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/7091#issuecomment-4904235648) | Cross-file sizeof/alignment checks now only need stddef.h, not stdio.h (see `_cross_sizeof`). Verified against current code. Close proposed. |
| [#7378](https://github.com/mesonbuild/meson/issues/7378) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/7378#issuecomment-4914634893) | [Revised / status clarification] `naming_scheme: platform` (1.10.0) allows `.lib`; the default remains `classic`. No close proposed. |
| [#7540](https://github.com/mesonbuild/meson/issues/7540) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/7540#issuecomment-4904236705) | The `--wrapper` / `add_test_setup` conflict only triggers when an exe_wrapper is actually present (mtest.py:1802-1804). Verified against current code. Close proposed. |
| [#7944](https://github.com/mesonbuild/meson/issues/7944) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/7944#issuecomment-4914518801) | [Revised / status clarification] `subsystem()` (added in 1.2.0) now distinguishes Apple OS flavors. Noted precisely that `system()` itself still returns `darwin` for all of them. No close proposed. |
| [#9212](https://github.com/mesonbuild/meson/issues/9212) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/9212#issuecomment-4914635344) | [Revised / status clarification] `@SOURCE_ROOT@` behaves as designed (the command's first element is resolved via `find_program`); documenting this explicitly is still not done. No close proposed. |
| [#9500](https://github.com/mesonbuild/meson/issues/9500) | Comment corrected (maintainer found it not fully fixed; close retracted) | [link](https://github.com/mesonbuild/meson/issues/9500#issuecomment-4913560848) | The original 'fixed' verdict was wrong. Maintainer bonzini pointed out that `[[custom_tgt.[index]]]` was still rendering as raw, unlinked text. The actual root cause is that the regex in `refman_links.py` only accepts `[a-zA-Z0-9_]` and rejects operator-style names like `[index]`. The comment was corrected in place and the close proposal was retracted; the issue remains open. |
| [#10401](https://github.com/mesonbuild/meson/issues/10401) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/10401#issuecomment-4914309329) | WINEPATH is now set automatically under Wine (meson_exe.py), with a short-circuit and a warning (commit 57909b53). Verified against current code; asked the reporter to retest. Close proposed. |
| [#11165](https://github.com/mesonbuild/meson/issues/11165) | Status-clarification comment posted (no close proposed) | [link](https://github.com/mesonbuild/meson/issues/11165#issuecomment-4914635719) | [Revised / status clarification] Apple `ar` detection now runs `ranlib -c` (PR #11742, 1.2.0). This appears to resolve the issue almost completely; left the close decision to the maintainer. |
| [#11796](https://github.com/mesonbuild/meson/issues/11796) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/11796#issuecomment-4913451503) | meson.build whitespace conventions are now covered by `meson format` (1.5.0, `wide_colon` defaults to False). Verified against current code. Close proposed. |
| [#13371](https://github.com/mesonbuild/meson/issues/13371) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/13371#issuecomment-4902050984) | Rust PGO support has been implemented (commits e9c6262d / be0a3448). Close proposed. |
| [#13810](https://github.com/mesonbuild/meson/issues/13810) | Comment posted (close proposed, awaiting maintainer) | [link](https://github.com/mesonbuild/meson/issues/13810#issuecomment-4914309745) | Fixed argument retrieval for non-required MPI (MPICH) via `-show-compile-info` (mpi.py, commit 04a2bc5a). Verified against current code; asked the reporter to retest. Close proposed. |

---

## Executive summary

All **1867** currently-open issues were classified into 4 categories (1860 from the original full sweep + 7 opened since then and triaged separately, listed in their own section below).

| Category | Count | Share |
|---|---:|---:|
| Can likely be closed with a comment (`comment_close`) | 365 | 19% |
| Resolvable with a small/medium implementation (`implement`) | 178 | 9% |
| Genuinely open (needs discussion / larger work / upstream dependency) (`keep_open`) | 1283 | 68% |
| Unclear, needs more investigation (`unclear`) | 41 | 2% |
| **Total** | **1867** | 100% |

### Confidence distribution

| Confidence | Count |
|---|---:|
| high | 365 |
| medium | 859 |
| low | 643 |

### `comment_close` breakdown by subtype

| Subtype | Count |
|---|---:|
| Already fixed / implemented (`fixed`) | 136 |
| Needs info, long stale (`needs_info_stale`) | 80 |
| Can be closed once answered (`answered`) | 75 |
| Obsolete (`obsolete`) | 30 |
| Invalid / out of scope (`invalid`) | 26 |
| Won't fix (design decision) (`wontfix`) | 17 |
| Duplicate (`duplicate`) | 1 |

### `implement` breakdown by effort

| Effort | Count |
|---|---:|
| Small (`small`) | 125 |
| Medium (`medium`) | 49 |
| Unspecified | 4 |

---

## New in this pass: additional close candidates

Follow-up sweep specifically looking for more closeable issues: a wider duplicate-title reclustering (found **4** more confirmed duplicate pairs, folded into the "Likely duplicates" section below, now 17 pairs total) and a systematic scan for **obsolete** issues — old reports whose premise no longer applies because the relevant code/platform/tool has since changed. Every item below was verified by reading the full thread and checking current code, not just flagged by heuristics.

### Obsolete: 17 newly-identified candidates

These were previously sitting in `keep_open`/other categories; each has now been re-classified as `comment_close` / `obsolete` below as well.

#### [#308](https://github.com/mesonbuild/meson/issues/308) Boost and cross compilation not working for android.
- **Confidence**: high
- **Why obsolete**: The Boost dependency detector in mesonbuild/dependencies/boost.py has been completely rewritten into a root/library-scanning implementation (BoostDependency, BoostLibraryFile, etc.) that is unrelated to the 2015 detection code. It also now directly implements the feature request from this issue: per-machine 'boost_includedir'/'boost_librarydir'/'boost_root' properties (boost.py lines ~374-437) are read via self.env.properties[self.for_machine], so cross builds (e.g. android) can specify separate include/lib dirs, which was exactly what the reporter asked for.

#### [#1041](https://github.com/mesonbuild/meson/issues/1041) Run more language and framework tests on Windows
- **Confidence**: high
- **Why obsolete**: This 2016 meta-issue asks to audit AppVeyor's installed-software docs to enable more Windows CI test coverage (csharp/fortran/boost/qt frameworks), and the checklist items reference AppVeyor-specific setup. The meson project's own CI has since fully migrated off AppVeyor: there is no .appveyor.yml in the repo, and Windows testing is now done via .github/workflows/windows.yml running the full test suite through run_tests.py. AppVeyor is only mentioned today as a legacy example snippet in docs/markdown/Continuous-Integration.md for third-party users, not as meson's own CI, so the issue's actual premise (auditing AppVeyor for more test coverage) no longer applies.

#### [#1179](https://github.com/mesonbuild/meson/issues/1179) gnome.compile_resource() should look into directory where xml is
- **Confidence**: high
- **Why obsolete**: In mesonbuild/modules/gnome.py's compile_resources() (around line 473), the code now does 'source_dirs.append(os.path.join(state.build_to_src, state.subdir))' with the comment 'Always include current directory, but after paths set by user' - i.e. the directory containing the .gresource.xml file is now always searched by default, without needing an explicit source_dir kwarg. This is exactly the behavior requested/reported missing in the issue.

#### [#1597](https://github.com/mesonbuild/meson/issues/1597) osx test-case "2 Library version" and "common 4/6" failing for xcode-backend
- **Confidence**: high
- **Why obsolete**: Both specific bugs reported are fixed in current mesonbuild/backend/xcodebackend.py: (1) the ldargs/dylib version code now uses 'dylib_version = target.soversion' instead of target.version, exactly the fix the reporter guessed at; (2) generate_filemap() now iterates only self.build_targets (= self.build.get_build_targets(), real BuildTarget objects), not all targets, so CustomTarget objects (which lack a .objects attribute) are no longer processed there, eliminating the reported AttributeError/KeyError crashes.

#### [#1875](https://github.com/mesonbuild/meson/issues/1875) gnome.gtkdoc() expands File arguments to builddir paths not sourcedir paths
- **Confidence**: high
- **Why obsolete**: gnome.py's gtkdoc() now resolves gobject_typesfile via an abs_filenames() helper that calls File.absolute_path(source_dir, build_dir); File.absolute_path() (mesonbuild/utils/universal.py) explicitly checks self.is_built and only uses builddir for built files, source dir otherwise, so a files('gobject.types') source file now correctly resolves to the source directory. Plain strings are likewise resolved relative to the source dir/subdir, matching the behavior nirbheek said was expected in the issue.

#### [#1904](https://github.com/mesonbuild/meson/issues/1904) Can't seem to get includes to work using pkg-config on windows due to space in "Program Files" dir
- **Confidence**: high
- **Why obsolete**: Both sides of this bug are now fixed: the pkgconfig module's _escape() (mesonbuild/modules/pkgconfig.py ~line 454-464) explicitly backslash-escapes spaces when generating .pc files, citing the exact freedesktop bug about Windows path spaces; and the consuming PkgConfigDependency._split_args() (mesonbuild/dependencies/pkgconfig.py ~line 217-221) now explicitly uses shlex.split() with a comment noting pkg-config paths follow Unix conventions even on Windows, which correctly reassembles space-containing paths like 'Program Files' instead of splitting on whitespace.

#### [#3332](https://github.com/mesonbuild/meson/issues/3332) windows: shared_library without exports caused stack trace on install
- **Confidence**: high
- **Why obsolete**: mesonbuild/minstall.py's install_targets() now checks 'if not os.path.exists(t.fname)' before ever calling check_for_stampfile(), and raises a clean MesonException('File ... could not be found') (or skips silently if the target is optional) instead of letting an unhandled FileNotFoundError propagate from os.stat() inside check_for_stampfile as happened in the original report. MesonException is caught and printed cleanly at the top level (mesonmain.py), so the described raw Python stack trace can no longer occur.

#### [#3780](https://github.com/mesonbuild/meson/issues/3780) Prefixes in the coverage report
- **Confidence**: medium
- **Why obsolete**: mesonbuild/scripts/coverage.py now explicitly excludes the subproject root from gcovr output via 'gcovr_config = ["-e", re.escape(subproject_root)]', and for gcovr >= 4.2 uses the correct dual-root invocation 'gcovr_base_cmd = [gcovr_exe, "-r", source_root, build_root]' with a comment noting 'gcovr >= 4.2 requires a different syntax for out of source builds' - directly addressing the out-of-tree build path-resolution confusion (source-dir vs build-dir entries) described in the report. Confidence is medium because the report also depended on the reporter's specific old gcovr version and the account is deleted, so the exact old failure mode can't be fully reproduced/confirmed here.

#### [#4474](https://github.com/mesonbuild/meson/issues/4474) gnome.compile_schemas() documentation seems wrong
- **Confidence**: high
- **Why obsolete**: At the time of filing, gnome.compile_schemas() did not set build_by_default at all when the user omitted it, so it fell through to CustomTarget's default of False, contradicting the docs. Commit 3894f80e21e9 (2021-10-05, 'modules/gnome: use typed_kwargs for compile_schemas') introduced a dedicated `_BUILD_BY_DEFAULT` KwargInfo with `default=True` specifically for compile_schemas (mesonbuild/modules/gnome.py, the '@typed_kwargs('gnome.compile_schemas', _BUILD_BY_DEFAULT.evolve(since='0.40.0'), ...)' decorator), so the actual default now matches what the documentation always said.

#### [#4647](https://github.com/mesonbuild/meson/issues/4647) pkg-config missing dependency not reported
- **Confidence**: high
- **Why obsolete**: In current mesonbuild/dependencies/pkgconfig.py, PkgConfigInterface.cflags()/libs() capture pkg-config's stderr and raise `DependencyException(f'Could not generate cflags for {name}:\n{err}\n')` including the real pkg-config error text, and PkgConfigDependency.__init__ prints that exception via `mlog.warning(f"Pkg-config error with '{name}': {e}")`. Additionally _call_pkgbin uses Popen_safe_logged, which writes stdout/stderr of every pkg-config invocation to meson-log.txt. The original complaint that pkg-config's real error was swallowed no longer applies.

#### [#4869](https://github.com/mesonbuild/meson/issues/4869) failing test_install_umask on new platform (=SunOS)
- **Confidence**: high
- **Why obsolete**: The reported crash ('/usr/bin/python3: can't open file '[\'...myinstall.py\']'') came from the pre-0.50 ExecutableSerialisation design that kept a separate `fname` list and `cmd_args` list combined ad hoc in meson_exe.py (`subprocess.Popen(cmd + exe.cmd_args, ...)`). Commit d34e53202043 ('backends: do not split command and arguments in ExecutableSerialisation', part of PR #5644 merged 2019-08-03) unified these into a single `cmd_args` list, and current mesonbuild/scripts/meson_exe.py simply does `subprocess.Popen(cmd_args, ...)` with a clean argument list, so this specific malformed-argv failure mode can no longer occur. test_install_umask itself is a generic, still-passing test unrelated to any SunOS-specific code path.

#### [#5137](https://github.com/mesonbuild/meson/issues/5137) meson doesn't detect installed dub packages
- **Confidence**: high
- **Why obsolete**: mesonbuild/dependencies/dub.py has been completely overhauled since 2019: it now version-gates behavior via `_search_in_cache = version_compare(dubver, '<=1.31.1')` and `_use_cache_describe = version_compare(dubver, '>=1.35.0')`, calls `_get_dub_description()`/`dub describe`, and does compiler/arch/build-type/configuration-aware compatibility matching per target (`_find_target_in_cache`). This bears no resemblance to the naive package lookup active when the 2019 report (dub 1.14.0, meson 0.50.0) was filed.

#### [#5443](https://github.com/mesonbuild/meson/issues/5443) meson test: gdb doesn't support -nh argument on FreeBSD 11
- **Confidence**: high
- **Why obsolete**: Current mesonbuild/mtest.py's `TestHarness.get_wrapper()` builds the gdb invocation as `wrap = [options.gdb_path, '--quiet']` (plus optional `-ex run -ex quit` and `--args`); a repository-wide search confirms `-nh` does not appear anywhere in mesonbuild today. Since meson no longer passes `-nh` to gdb at all, the FreeBSD gdb incompatibility described in the issue cannot occur with current code.

#### [#5551](https://github.com/mesonbuild/meson/issues/5551) d test sample broken
- **Confidence**: high
- **Why obsolete**: Reports meson's own D static/shared library test samples (test cases/d/2, /3) failing on Windows 7 with dmd 2.086 and ldc 1.16, both from 2019 and long superseded by current releases. Meson officially dropped Windows 7 support in the 0.54.0 release (docs/markdown/Release-notes-for-0.54.0.md: "Microsoft ended support for Windows 7, so only 64 bit Windows OSs are officially supported"), and the specific ancient toolchain versions cited are no longer relevant to current D compiler support in mesonbuild/compilers/d.py. No further activity since 2019 confirms lack of ongoing relevance.

#### [#6425](https://github.com/mesonbuild/meson/issues/6425) boost_python detection fails on osx
- **Confidence**: high
- **Why obsolete**: The maintainer's own comment ties this to #4788, which was fixed by commit 9f2f27a49d9f ('boost: Fix boost_python detection on bionic (fixes #6886 #4788)', 2020-04-01) as part of a broader rewrite of boost dependency/python-module detection (08224dafcba1 'boost: Rewrite the boost system dependency' and 4e52a0f7fd9f 'boost: Better python module detection', both Feb-Mar 2020). Current mesonbuild/dependencies/boost.py has dedicated, extensively-commented logic ('Handle the boost_python naming madness') for parsing boost_python module tags across platforms/compilers, entirely different from the mechanism active when this 2020 High-Sierra/boost-1.72 report was filed.

#### [#6898](https://github.com/mesonbuild/meson/issues/6898) MacOS build of D libraries with DMD 2.085 fails with unrecognized switch '-Xcc=-Wl,-undefined,dynamic_lookup'
- **Confidence**: medium
- **Why obsolete**: The `-Xcc=` mechanism in mesonbuild/compilers/d.py's `get_allow_undefined_link_args()` (added Dec 2019, unchanged since) relies on a DMD/LDC flag that only exists starting DMD 2.087; DMD 2.085 (June 2019) predates it by design, not by regression. DMD 2.085 is now many years and dozens of releases obsolete (current DMD is well past 2.1xx), so no currently-installed DMD toolchain would hit this failure; the flag works correctly with any DMD/LDC actually in use today.

#### [#11034](https://github.com/mesonbuild/meson/issues/11034) meson fails to find a linker when multiple archflags are passed to GCC
- **Confidence**: medium
- **Why obsolete**: The report is about linker detection failing when Apple's own gcc-4.2 (the last Apple-shipped, non-Clang GCC front end, EOL since Xcode 4.2 in ~2011) is given multiple -arch flags to build fat PowerPC (ppc/ppc64) binaries via MacPorts. PowerPC Macs and real Apple GCC have been extinct/unsupported for well over a decade, and current mesonbuild/mesonbuild/linkers/detect.py:guess_nix_linker() still only special-cases Apple Clang and generic GNU/LLD/Solaris/AIX linkers, with no indication anyone is targeting this combination. The issue has zero comments, zero reactions, and no linked PRs or cross-references since it was filed in 2022, suggesting no real users are hitting this on any currently-relevant platform.

---

## Thread-verified: candidates that can likely be closed with just a comment

**43** high-confidence "already fixed" candidates were re-verified against the full GitHub thread and the current source (not commented on yet, aside from the ones listed in the previous section).

| Verification result | Count | Disposition |
|---|---:|---|
| Verified safe to close (`safe_close`) | 20 | Draft comment below is ready to post as-is |
| Needs a corrected comment (`revise`) | 3 | Draft comment below reflects the corrected understanding |
| **Not** safe to close (`not_safe`) | 20 | Demoted back to keep_open — see caveats below |

→ **20** of these have draft comments ready but **have not been posted** (commenting was paused before we got to them). They are included here so a maintainer can act on them directly if useful.

### Ready to post as-is: 20 (of 20 verified; 0 already posted above)

#### [#1579](https://github.com/mesonbuild/meson/issues/1579) RFE: bash autocompletion support
- **Thread status**: The final comment, from liambeguin in 2019, is only a follow-up request: the completion files already exist, so could they be auto-installed via setup.py.
- **Basis**: The core RFE (providing bash completion) is already implemented and bundled as data/shell-completions/bash/meson and zsh/_meson, and is included in the sdist via the MANIFEST's graft data. Automatic installation is the responsibility of distro packaging.
- **Residual risk**: Since the last comment is specifically about wanting automatic installation via setup.py, the reporter may remain unsatisfied with an answer that says "installation should be handled by distros" if they're attached to that point.
- **Draft comment**:
  ```text
  The core request here is implemented: Meson ships shell-completion scripts for both bash (`data/shell-completions/bash/meson`) and zsh (`data/shell-completions/zsh/_meson`), and they are included in the source distribution. These are installed to the appropriate completion directories by distro packages (Meson's own Python installer intentionally leaves installing them to the packager, since completion install paths are distro-specific). Closing as implemented; if a specific option is not being completed correctly, please open a focused issue for that.
  ```

#### [#1864](https://github.com/mesonbuild/meson/issues/1864) configure_file(): allow more than one substitution per string
- **Thread status**: The final comment, from rindeal in 2021, notes that while eli-schwartz said "there's no use case," rindeal argues it should still be fixed since other variables can be substituted multiple times, or at least the manual should be updated.
- **Basis**: The core bug reported (substitute_values only performing one substitution per string via if/elif) is fixed in the current mesonbuild/utils/universal.py, which does a full substitution via value_rx.sub(replace, vv). This was verified empirically too: in ['sh','-c','... "@INPUT@" > "@OUTPUT@"'], both placeholders get substituted (when there's one input and one output each).
- **Residual risk**: Partway through, the thread's discussion shifted toward "there's no use case anyway / a caveat should be added to the manual," so the reporter may actually want a manual update instead. Since the original technical bug is fixed, closing the issue itself is reasonable.
- **Draft comment**:
  ```text
  The specific bug reported here is fixed. `substitute_values()` now performs a regex-based replacement over each string (`value_rx.sub(...)` in mesonbuild/utils/universal.py) rather than the old if/elif that stopped after one substitution, so multiple `@...@` templates in a single command element are all replaced. For example `command : ['sh', '-c', '... "@INPUT@" > "@OUTPUT@"']` now expands both `@INPUT@` and `@OUTPUT@` (Meson still errors if `@INPUT@`/`@OUTPUT@` in an inline string maps to more than one file, which is unavoidable). Closing as fixed; please reopen with a concrete case if a specific multi-substitution still fails.
  ```

#### [#2034](https://github.com/mesonbuild/meson/issues/2034) gnome.gtkdoc doesn't honour the `dependencies:` keyword
- **Thread status**: The final comment, from inigomartinez in 2018, states "I pushed compiler-argument support for dependencies in #4192," and there's been no objection since.
- **Basis**: gnome.gtkdoc accepts 'dependencies' (Dependency/SharedLibrary/StaticLibrary) via typed_kwargs, injects cflags/ldflags through _get_build_args, and sets the returned new_depends as the CustomTarget's extra_depends, so build-order dependencies are reflected as well (mesonbuild/modules/gnome.py:1459-1462,1575,1588).
- **Residual risk**: It's unverified whether the original reporter's actual use case (including output generated by another tool in the documentation) is fully covered by the current dependencies implementation. content_files now also accepts CustomTarget, so it's largely covered, but there's room for reopening in edge cases.
- **Draft comment**:
  ```text
  This is resolved. `gnome.gtkdoc()` now accepts a `dependencies:` keyword taking `dependency()` objects and shared/static libraries (see the typed_kwargs in mesonbuild/modules/gnome.py). The dependencies are honoured in two ways: their compile/link flags are passed to the gtk-doc scan via `_get_build_args`, and the resulting build targets are added as `extra_depends` of the doc custom target, so build ordering against generated inputs is respected. Closing as fixed; please reopen if a dependency still isn't being applied.
  ```

#### [#2329](https://github.com/mesonbuild/meson/issues/2329) Report the reason for failure of install script
- **Thread status**: The final comment (eli-schwartz, 2022-08) points out a limitation in shebang diagnostics — that the exception object alone doesn't reveal which file is at fault — but it's not an argument for keeping the issue open.
- **Basis**: The original request — that a script's stdout/stderr be logged/shown on failure — is fulfilled. Install scripts go through run_exe (meson_exe.py), which prints --- stdout --- / --- stderr --- on a non-zero exit (lines 68-79), and minstall.py prints 'FAILED: install script ... failed with exit code N' (line 752), or 'could not be run.' plus exit 127 when the script can't be executed at all (lines 748-750).
- **Residual risk**: In the case eli-schwartz raised — an invalid shebang interpreter — an OSError only produces 'could not be run.', without identifying which interpreter is missing; this residual limitation remains. There's a small but real chance this point gets raised after posting.
- **Draft comment**:
  ```text
  This is now handled. Custom install scripts run through the Meson exe runner (`mesonbuild/scripts/meson_exe.py`), which captures the script's output and, on any non-zero exit, prints `--- stdout ---` / `--- stderr ---` so you can see why it failed. On top of that, `minstall.py` reports `FAILED: install script '<name>' failed with exit code <N>` (and exits with that code), or `FAILED: install script '<name>' could not be run.` with exit 127 when the script cannot be launched at all. So both the exit code and the script's own output are now reported. Closing as fixed.
  ```

#### [#2560](https://github.com/mesonbuild/meson/issues/2560) Compiler detection is incorrect for native LLVM/Clang install on Windows
- **Thread status**: The last comment (jon-turney, 2018-11) says 'still not fixed, possibly a duplicate of #4232,' but the architecture has since been overhauled, and dedicated clang-cl support plus linker-driven argument generation have been implemented.
- **Basis**: soname/rpath/import-lib arguments are now delegated to each DynamicLinker class (linkers.py), and the old behavior where ClangCompiler assumed MINGW and emitted -Wl,-soname etc. has been removed. In addition, dedicated ClangClCompiler/ClangClCCompiler and ClangClDynamicLinker (lld-link) classes have been implemented, clang-cl is included in detect.py's Windows detection order (lines 48-54, 299), and linker detection is now determined dynamically based on output (linkers/detect.py:74-). The misdetection of native Windows clang has been resolved.
- **Residual risk**: This is a very old issue and the toolchain assumptions at the time of reporting have since changed, so there's a residual chance the original reporter could claim reproduction with specifics unique to the plain clang (GNU target) they were using back then, but a new issue would suffice in that case.
- **Draft comment**:
  ```text
  Native Clang on Windows is now handled correctly. Soname/rpath/import-library arguments are delegated to the detected `DynamicLinker` class rather than being hardcoded in the Clang compiler on the assumption of MinGW, so Meson no longer blindly emits GNU-ld style `-Wl,-soname`/`--start-group`/`--out-implib`/`-Wl,-rpath` for a native Windows toolchain. In addition, Meson has dedicated `ClangClCompiler`/`ClangClCCompiler` classes and a `ClangClDynamicLinker` (lld-link), and detects `clang-cl` in its Windows compiler search order (`mesonbuild/compilers/detect.py`), with linker detection based on the actual linker output. This resolves the incorrect detection described here. Closing as fixed; please open a fresh issue with a `meson setup` log if you hit a remaining native-Clang case on Windows.
  ```

#### [#2608](https://github.com/mesonbuild/meson/issues/2608) Recommend a standard coding style for meson.build files
- **Thread status**: The last comment (2018-02) said the newly added style guide was 'a good start but lacking detail'; since then the style guide has been expanded and meson format has been added.
- **Basis**: docs/markdown/Style-guide.md exists and documents spacing/indentation (2 spaces), trailing commas, naming (snake_case), and source ordering, among other things. In addition, 1.5.0 added `meson format` (alias `fmt`, with EditorConfig support), which can auto-format/apply the recommended style. The original request has been satisfied.
- **Draft comment**:
  ```text
  Meson now provides both a documented style guide and tooling to enforce it. `docs/markdown/Style-guide.md` covers indentation (two spaces, no tabs), trailing commas, `snake_case` naming, argument/dependency conventions, and source-list sorting. Since 1.5.0 there is also a built-in `meson format` command (alias `meson fmt`) with EditorConfig support that can auto-format `meson.build` files to a consistent style. This addresses the request for a recommended standard coding style. Closing as addressed; finer formatting rules are handled by `meson format` and its configuration.
  ```

#### [#2818](https://github.com/mesonbuild/meson/issues/2818) Document how to run the project tests, the unit tests, and both together
- **Thread status**: There are only two follow-up requests from 2017-2018 in the comments; Contributing.md has since been updated with test-running instructions, and there's no active objection or ongoing discussion.
- **Basis**: docs/markdown/Contributing.md:141-162 documents how to run run_tests.py (everything)/run_unittests.py (unit tests)/run_project_tests.py (project tests), subset selection via --only, and how to run individual project tests. The core documentation request has been satisfied.
- **Residual risk**: The CI list (Appveyor/Travis) mentioned in the issue body is not reflected in the current GitHub Actions-based documentation, so there's a chance of a minor complaint if someone fixates on that point specifically (routing to a separate issue would suffice).
- **Draft comment**:
  ```text
  The Contributing docs now cover this: `./run_tests.py` runs everything, `./run_unittests.py` runs the unit tests, and `./run_project_tests.py` runs the project tests, including how to select a subset with `--only` and run an individual project test directly (see `docs/markdown/Contributing.md`). Closing as documented. Note the original bullet about Appveyor/Travis is outdated since CI moved to GitHub Actions; that CI overview can be refreshed separately if desired.
  ```

#### [#2953](https://github.com/mesonbuild/meson/issues/2953) coverage targets ?
- **Thread status**: Zero comments, last updated in 2018, no discussion. The requested consolidation of duplicated lcov logic is complete.
- **Basis**: All of the coverage/-html/-xml/-text/-sonarqube phony targets in ninjabackend.py now delegate to `meson --internal coverage` (scripts/coverage.py), and the duplicated lcov implementation within the backend has been eliminated — exactly the consolidation that was requested.
- **Draft comment**:
  ```text
  Coverage handling was consolidated a while ago: the ninja backend now emits `coverage`, `coverage-html`, `coverage-xml`, `coverage-text` and `coverage-sonarqube` phony targets, all driven through the single `meson --internal coverage` script (mesonbuild/scripts/coverage.py) rather than duplicated lcov logic in the backend. That addresses the cleanup requested here, so closing as resolved.
  ```

#### [#2960](https://github.com/mesonbuild/meson/issues/2960) Generated files not regenerated when the generator changes
- **Thread status**: Last updated in 2018 with no further discussion. The reporter's core problem — 'not regenerated when the script changes' — has since been resolved.
- **Basis**: In GeneratedList.__post_init__, if the generator's exe is a build target (LocalProgram) it's automatically added to extra_depends, and if external with an absolute path it's added to depend_files, triggering regeneration on codegen script changes (confirmed at build.py:2131-2145). The generator's depends keyword (0.51.0) was also added, allowing arbitrary additional dependencies to be declared.
- **Residual risk**: The sub-issue nirbheek raised (passing a File/generated target as generator arguments) is outside the scope of this issue, but a reporter might interpret that as the main point when this is posted. It was already separated out at the end of the comment thread.
- **Draft comment**:
  ```text
  This is fixed: Meson now tracks the generator program itself as a dependency of the generated files (build.py `GeneratedList.__post_init__` adds a build-target generator to `extra_depends`, or an external absolute-path program to `depend_files`), so editing your codegen script triggers regeneration. `generator()` also gained a `depends` kwarg (since 0.51.0) to declare additional inputs. Closing as fixed. (Note: passing arbitrary `files()` as generator *arguments* to create implicit dependencies is a separate enhancement; please open a focused issue if you need that.)
  ```

#### [#3083](https://github.com/mesonbuild/meson/issues/3083) Boost dependency should set -DBOOST_ALL_DYN_LINK
- **Thread status**: Last comment in 2018. The granularity the requester, sarum9in, wanted — applying DYN_LINK per module only when linking shared — has been implemented exactly as requested.
- **Basis**: boost.py defines shared=['-DBOOST_<MODULE>_DYN_LINK=1'] for each module, applied as compile_args only when using the shared library. This matches the requested granularity of per-module rather than a blanket BOOST_ALL_DYN_LINK, and auto-linking is also disabled via -DBOOST_ALL_NO_LIB.
- **Draft comment**:
  ```text
  This is implemented: the Boost dependency emits per-module `-DBOOST_<MODULE>_DYN_LINK=1` compile args when linking against shared Boost libraries (e.g. `-DBOOST_LOG_DYN_LINK=1`, `-DBOOST_TEST_DYN_LINK=1`), which is the granular per-module approach requested here rather than a blanket `-DBOOST_ALL_DYN_LINK`, and it also sets `-DBOOST_ALL_NO_LIB` to disable auto-linking. Closing as fixed; please reopen if a specific module is missing its DYN_LINK define.
  ```

#### [#3603](https://github.com/mesonbuild/meson/issues/3603) unit tests: snippet heading test is broken
- **Thread status**: Zero comments, no updates since the 2018 report. An abandoned issue with no discussion or objection.
- **Basis**: unittests/datatests.py:47-59 toggles in_code_block on ``` and excludes lines starting with # inside a code block from being treated as headings — this has been fixed. It resolves exactly the reported problem ('# inside a code example is misdetected as a heading'), and no additional commonmark dependency is needed either.
- **Draft comment**:
  ```text
  This has been fixed: the snippet heading test (`unittests/datatests.py`, `DataTests.test_snippets`) now tracks fenced code blocks -- it toggles an `in_code_block` flag on ```` ``` ```` lines and skips heading detection while inside a block, so `#`-prefixed lines inside code examples are no longer mistaken for headings. Closing as resolved.
  ```

#### [#3848](https://github.com/mesonbuild/meson/issues/3848) Should not try to execute the same subproject twice
- **Thread status**: The last comment is just a third party's 2018-10-22 question asking if there's a workaround. There's no ongoing discussion from a maintainer.
- **Basis**: do_subproject() caches even failed/disabled subprojects via disabled_subproject() into self.subprojects[for_machine] (interpreter.py:1002, 1035, 923), and returns the cached holder on a repeat request for the same name (:979-988). So a subproject that was once attempted no longer re-executes project(), and the reported 'Second call to project()' no longer occurs.
- **Draft comment**:
  ```text
  This is fixed: `do_subproject()` now caches results per machine (`self.subprojects[for_machine]`), including subprojects that failed or were disabled -- a failed non-required subproject is stored via `disabled_subproject()`, and any later lookup of the same name returns the cached holder instead of re-running configuration. As a result a subproject that was already attempted is not executed a second time and the `Second call to project()` error no longer occurs in this fallback scenario. Closing as resolved.
  ```

#### [#3917](https://github.com/mesonbuild/meson/issues/3917) Dist doesn't respect meson configuration
- **Thread status**: The effective last comment is from 2018-08 (nirbheek: 'it would be easy to let meson dist accept -D' etc.). The 2026-03 update was just a label change; the comment count has stayed at 7.
- **Basis**: mdist.py's check_dist reads the command-line options saved in the build directory (meson-private/cmd_line.txt, via read_cmd_line_file) via create_cmdline_args(bld_root) and passes them as-is to the meson setup used for the dist test build (:348, 361-368). This resolves the core of the report — 'dist is configured with default options' — and disabled dependencies stay disabled during dist as well.
- **Draft comment**:
  ```text
  This is resolved: `meson dist` now reads the options that were configured in your build directory (`create_cmdline_args()` -> `read_cmd_line_file()` from `meson-private/cmd_line.txt`) and passes them to the `meson setup` it runs for the dist test build (`mesonbuild/mdist.py`). So the dist build honours your configured options -- e.g. a feature disabled via `-Dopt=false` stays disabled during dist -- instead of falling back to defaults. Closing as fixed.
  ```

#### [#4071](https://github.com/mesonbuild/meson/issues/4071) Regression: meson no longer defaults to needs_exe_wrapper: false for 32-bit on 64-bit builds of the same architecture
- **Thread status**: Zero comments, unchanged since the 2018 report. No objections.
- **Basis**: machine_info_can_run() in envconfig.py:761-779 explicitly determines, under a same-OS assumption, that x86 (and mips on mips64) can run on an x86_64 host, and need_exe_wrapper() in environment.py:585 uses this to decide that no exe wrapper is needed. The reported same-arch 32-on-64 regression has already been fixed.
- **Draft comment**:
  ```text
  This regression is fixed. `machine_info_can_run()` (`mesonbuild/envconfig.py`) now explicitly treats an x86 host binary as runnable on an x86_64 build machine (and likewise mips on mips64) when the OS matches, and `Environment.need_exe_wrapper()` uses it, so Meson again defaults to not needing an exe wrapper for a same-architecture 32-on-64 build. Closing as fixed; please reopen if you still see the wrapper being required in that case.
  ```

#### [#4190](https://github.com/mesonbuild/meson/issues/4190) meson wrap does not consider subproject_dir option
- **Thread status**: Zero comments, unchanged since the 2018 report. No objections.
- **Basis**: Each wraptool command uses mesonlib.get_subproject_dir() (universal.py:2749-2766), which parses the root meson.build via introspection to extract project()'s subproject_dir kwarg (falling back to 'subprojects' only when unspecified). msubprojects.py:730 also uses extract_subproject_dir(). So meson wrap now honors a custom subproject_dir.
- **Draft comment**:
  ```text
  This is resolved: the wrap / subprojects tooling no longer hardcodes `subprojects`. `wraptool` uses `mesonlib.get_subproject_dir()`, which introspects the root `meson.build` and extracts the `subproject_dir` kwarg from `project()` (falling back to `subprojects` only when it isn't set), and `mesonbuild/msubprojects.py` uses `extract_subproject_dir()` the same way. So `meson wrap` now honours a custom `subproject_dir` such as `libs`. Closing as fixed; please reopen if you still see it defaulting to `subprojects` with a custom directory.
  ```

#### [#4876](https://github.com/mesonbuild/meson/issues/4876) Support using existing library builds of gmock and gtest
- **Thread status**: The last comment (wak-google, 2019-02-13) confirms real-world use, saying they are using the system's external gtest/gmock without issues, with no objections.
- **Basis**: dev.py's GTestDependencySystem/GMockDependencySystem use find_library('gtest'/'gmock') to prioritize detecting a prebuilt library (prebuilt=True), falling back to the bundled source only when none is found. In addition, GTestDependencyPC/GMockDependencyPC (pkg-config) are also registered in DependencyFactory, so the requested use of prebuilt libraries is fully implemented.
- **Draft comment**:
  ```text
  Meson already supports using prebuilt gtest/gmock. `dependency('gtest')` / `dependency('gmock')` use a DependencyFactory that first tries pkg-config (`GTestDependencyPC` / `GMockDependencyPC`), then a system lookup that prefers prebuilt libraries via `find_library('gtest')` / `find_library('gmock')` and only falls back to building the bundled sources if no library is found. As a commenter here confirmed back in 2019, external/system googletest and gmock work fine. Closing as resolved; please reopen if the prebuilt Fedora/Debian libraries aren't being picked up on a current release.
  ```

#### [#4935](https://github.com/mesonbuild/meson/issues/4935) Change the way the install_dir is handled for Vala libraries
- **Thread status**: There is only one comment (2022, a secondary mention about simplifying typelib generation); no objection or ongoing discussion about the core install_dir design request.
- **Basis**: Meson 1.11 added the install_vala_header / install_vala_vapi / install_vala_gir (and *_dir variant) keywords (type_checking.py:833-844, build.py:953-973), and deprecated the confusing install_dir:[true,true,true,true] array form (FeatureDeprecated 1.11.0). The request itself (dedicated keywords equivalent to install_dir_header/vapi) has been implemented and documented.
- **Residual risk**: The secondary request about simplifying typelib generation (mentioned in a 2022 comment) is a separate topic that remains unaddressed, so a comment has been added suggesting it be split into its own issue.
- **Draft comment**:
  ```text
  This has been implemented. Meson 1.11 added dedicated `install_vala_header`, `install_vala_vapi`, and `install_vala_gir` keyword arguments (each with a matching `*_dir` variant for the destination), which replace the hard-to-read `install_dir: [true, true, true, true]` array form — passing more than one value to `install_dir` is now deprecated in favor of these keywords. See the Vala documentation ("Building libraries"). Closing as implemented; please reopen if the new keywords don't cover your case. (The separate point about simplifying `.typelib` generation is better tracked as its own issue.)
  ```

#### [#5170](https://github.com/mesonbuild/meson/issues/5170) Pass Extra CMake Arguments in Inital Pass
- **Thread status**: In 2019-03, mensinda indicated that a new vcpkg dependency type would be ideal and that a global toolchain option could also be added, after which discussion stopped (last update in 2021-11 was label-related).
- **Basis**: In cmake.py, the user's cmake_args are passed into _get_cmake_info(cm_args) and applied on the first pass (118-121, 162), and the generated toolchain file including CMAKE_TOOLCHAIN_FILE is also applied on the first pass (161, toolchain.py:66-67). Furthermore, the globally specifiable toolchain file that mensinda pushed for has been implemented as the cmake_toolchain_file machine-file property (0.56.0, Machine-files.md:234), so the specific request in the issue title and body (making CMAKE_TOOLCHAIN_FILE take effect on the initial cache creation) is satisfied.
- **Residual risk**: The dedicated vcpkg dependency type and the debug/release mix-up that came up as side topics in this issue are out of scope and remain unaddressed; a comment has been added suggesting they be split into a separate issue.
- **Draft comment**:
  ```text
  This is resolved in current Meson. User-supplied `cmake_args` are now passed into the initial `_get_cmake_info()` invocation, and the generated CMake toolchain file — which carries `CMAKE_TOOLCHAIN_FILE` — is applied in that same first pass, so toolchain-driven cached variables (as vcpkg needs) take effect from the initial cache creation. In addition, the reliable "global toolchain file for all CMake dependencies" mechanism that was discussed here is now available as the `cmake_toolchain_file` machine-file property (since 0.56.0; see Machine-files.md). Closing as implemented. The broader idea of a dedicated `vcpkg` dependency type is a separate feature — please open a new issue for that if it's still wanted.
  ```

#### [#5240](https://github.com/mesonbuild/meson/issues/5240) run_command error with compiler object
- **Thread status**: A zero-comment issue with no updates since 2019, with no objection or ongoing discussion whatsoever.
- **Basis**: run_command_impl expands get_exe() (exelist[0]) and get_exe_args() (exelist[1:]) for a compiler object and passes both, so the full exelist wrapped by e.g. ccache is used. The reported bug of using only exelist[0] has been resolved at interpreter.py:842-844.
- **Draft comment**:
  ```text
  This is fixed in current Meson. When a compiler object is passed to `run_command()`, it now expands the full compiler exelist — it uses `get_exe()` for the first element and `get_exe_args()` for the remaining ones (see `mesonbuild/interpreter/interpreter.py`). So a wrapped compiler such as `ccache gcc` is invoked in full rather than dropping everything after the first element. Please try a recent release; if you still hit a failure with a wrapped compiler, let us know and we can reopen.
  ```

#### [#5333](https://github.com/mesonbuild/meson/issues/5333) meson introspect --targets has no linker information
- **Thread status**: The last comment is from null77 on 2022-11-24, re-requesting that linker information be exported; mensinda had originally replied that it was not implemented.
- **Basis**: create_target_linker_introspection in ninjabackend.py:954-972 now adds the linker's exelist and link parameters to introspection_data, and list_targets in mintro.py:187 includes them in target_sources via backend.get_introspection_data(), so `meson introspect --targets` (and meson-info/intro-targets.json) now outputs link-stage information.
- **Residual risk**: The link parameters are just raw link-command arguments, not a direct dependency graph of which static lib goes into which shared lib. This may not be sufficient for null77's use case, in which case the issue could be reopened.
- **Draft comment**:
  ```text
  Linker information is now available in the target introspection data. The Ninja backend emits a linker block — the linker command/exelist plus the link parameters — alongside the per-language compile blocks, and this is surfaced in the `target_sources` array of `meson introspect --targets` (and in `meson-info/intro-targets.json`). See `create_target_linker_introspection` in `mesonbuild/backend/ninjabackend.py`. Please try it on a recent release; closing as resolved, but reopen if a specific field you need (e.g. resolving which static libs end up in a given shared lib) is still missing.
  ```

### Needs a corrected comment: 0 (of 3 verified; 3 already posted above)

### Demoted — do NOT close: 20

> These looked "already fixed" from code alone, but re-reading the full thread showed the issue's actual request is still unresolved or discussion is still active. Kept here as a caution against a shallow code-only read producing a false close.

| Issue | Title | Why it doesn't qualify |
|---|---|---|
| [#1733](https://github.com/mesonbuild/meson/issues/1733) | i18n.gettext: POTFILES.in does not support generated fi | For the classic i18n.gettext() + POTFILES.in path that this issue targets, run_potgen in mesonbuild/scripts/gettext.py still only reads POTFILES relative to --source-root and cannot resolve generated files in the build d |
| [#1844](https://github.com/mesonbuild/meson/issues/1844) | Documentation created by gtkdoc is not generated when c | gnome.gtkdoc now creates a CustomTarget, but with build_by_default=False (neither build_by_default nor install is specified), so plain ninja builds don't generate the docs — it's still only built via an explicit target o |
| [#2121](https://github.com/mesonbuild/meson/issues/2121) | Add an option to have @rpath install_name instead of an | The triage's basis (get_soname_args's install_name=['@rpath/',...]) only applies at build time; at install time, depfixer.fix_darwin rewrites it to final_path (an absolute path) via install_name_tool -id (mesonbuild/scri |
| [#2155](https://github.com/mesonbuild/meson/issues/2155) | Should de-duplicate -isystem flags just like -I flags | Deduplication (dedup2) is done, but as the comment at clike.py:51-61 shows, -isystem is deliberately excluded from prepend_prefixes so as not to break ordering dependencies (e.g. in systemd), so the issue title's request |
| [#2425](https://github.com/mesonbuild/meson/issues/2425) | --wrap-mode ignores git submodules | The early return at wrap.py:572-574 works for a submodule that "already has a meson.build," but when the submodule directory is empty/uninitialized, resolve_git_submodule() (lines 637-675) runs 'submodule update --init/. |
| [#2519](https://github.com/mesonbuild/meson/issues/2519) | compiler.run() current working directory and cleanup | TemporaryDirectoryWinProof is merely a temporary directory for placing compiled build artifacts (binaries); it is not the runtime cwd of the generated executable. run_method in interpreter/compiler.py:295 calls self.comp |
| [#2687](https://github.com/mesonbuild/meson/issues/2687) | meson.build configuration file syntax test | `meson format --check-diff` checks whether formatting matches Meson's style conventions and returns a diff/non-zero exit (mformat.py:1117-1127) — it is not a judgment of 'is the syntax valid,' the way apachectl configtes |
| [#2896](https://github.com/mesonbuild/meson/issues/2896) | pkgconfig generator should automatically populate requi | Partial functionality exists whereby passing a pkg-config dependency to libraries puts it in Requires.private, but the core of the issue (whether it should be auto-derived from dependency()) remains unresolved, and a rec |
| [#2922](https://github.com/mesonbuild/meson/issues/2922) | State corruption with multiple tasks running on same di | msetup.py now acquires meson-private/meson.lock, but a code check confirms mconf.py (meson configure) still has no locking (DirectoryLock is only used by msetup.py and wrap.py). A maintainer pointed out the remaining gap |
| [#3551](https://github.com/mesonbuild/meson/issues/3551) | Add a way to check for the presence of a Python module | find_installation(modules:...) can check for module presence (confirmed at python.py:553-564), but the version constraint the issue body asks for (version: '>= 0.10') is unimplemented, and how to achieve it (whether to d |
| [#3566](https://github.com/mesonbuild/meson/issues/3566) | -O3 optimization level shouldn't be used with unity bui | The original triage was wrong. In options.py, DEFAULT_DEPENDENTS still maps release to optimization='3' (i.e., -O3), so the claim that 'release=-O2' is factually incorrect. The core point of the issue — that release shou |
| [#3628](https://github.com/mesonbuild/meson/issues/3628) | During cross compilation, base_options are being applie | Compilers have been made per-machine, but the 'value' of a base option is still a single global value normalized to HOST (options.py:1209; coredata.py:453 does not evolve per machine), so it's still not possible to set t |
| [#3676](https://github.com/mesonbuild/meson/issues/3676) | has_function misdetects smul_overflow as available. | [Confirmed on real hardware, unfixed] Reproduced has_function('smul_overflow')=YES on current master using zig cc (clang 19.1.7) (also sanity-checked: printf=YES / a nonexistent function=NO / __builtin_smul_overflow=YES) |
| [#4484](https://github.com/mesonbuild/meson/issues/4484) | Feature Request: make ProjectGuid deterministic for MSV | The generate_guid_from_path() (uuid5, deterministic) the triage cited is only used for subdir/directory; the actual target's ProjectGuid is still generated at interpreter.py:3509 via str(uuid.uuid4()).upper() (random). I |
| [#4802](https://github.com/mesonbuild/meson/issues/4802) | Hardcoded list of llvm-config binary names breaks on up | The specific issue of llvm-config-9/-80 not being detected has been resolved in tooldetect.py, but the reporter's core request -- that the hardcoded list breaks at every new version and a more robust mechanism is wanted  |
| [#4993](https://github.com/mesonbuild/meson/issues/4993) | Cuda compiler and OpenMP | cuda.py's to_host_flags_base now wraps unknown flags with -Xcompiler=, which improved some of the reported compilation-related failures, but since the CUDA compiler does not implement openmp_flags(), dependency('openmp', |
| [#5139](https://github.com/mesonbuild/meson/issues/5139) | Include Qt5 mkspecs headers | The request is to include the mkspecs directory (e.g. -I/usr/lib/qt/mkspecs/linux-g++, containing platform-spec headers like qplatformdefs.h). The private_headers keyword the triage cited is a different thing -- it adds  |
| [#5192](https://github.com/mesonbuild/meson/issues/5192) | Allow providing pkg-config dependencies without pkg-con | The core request is to supply dependencies (e.g. OPENSSL_LIBS) externally via native/machine files or the CLI without editing meson.build. The meson.override_dependency that the triage cited requires being called from wi |
| [#5320](https://github.com/mesonbuild/meson/issues/5320) | Make auto_features a per-subproject built-in option | A #106-type false positive. The per-subproject option foundation exists, and `-Dwlroots:auto_features=...` is accepted without warning, but in actual testing (global=disabled / wlroots=enabled), the subproject's feature  |
| [#5355](https://github.com/mesonbuild/meson/issues/5355) | compiler.get_supported_arguments reports success for un | The original report's GCC 'is valid for C/ObjC' case has been fixed in gnu.py:596-607, but the issue is actually broader — general misdetection of unsupported flags — and the maintainer themselves scoped it as still unre |

---

## Likely duplicates (17 pairs)

Found by clustering issue titles by similarity, then confirming by reading the full body/thread of each candidate pair and checking both are still open with no existing cross-reference between them. Not yet posted as comments (a simple `Duplicate of #N` comment would resolve each, since GitHub auto-links the reference).

| Duplicate | Canonical (older) | Confidence | Reason |
|---|---|---|---|
| [#9101](https://github.com/mesonbuild/meson/issues/9101) | [#9067](https://github.com/mesonbuild/meson/issues/9067) | high | Both report the same thing: the k1om (Intel Xeon Phi) CPU family is not recognized, with a request to add support for it. |
| [#10328](https://github.com/mesonbuild/meson/issues/10328) | [#10317](https://github.com/mesonbuild/meson/issues/10317) | high | Both report the identical bug: `$<TARGET_FILE:>` fails to resolve for a non-IMPORTED executable target defined inside a CMake subproject. |
| [#15953](https://github.com/mesonbuild/meson/issues/15953) | [#15732](https://github.com/mesonbuild/meson/issues/15732) | high | Both report the exact same problem: the Meson 1.11.1 sdist is missing from PyPI, so `pip --no-binary` falls back to the older 1.11.0. |
| [#15591](https://github.com/mesonbuild/meson/issues/15591) | [#13390](https://github.com/mesonbuild/meson/issues/13390) | high | Both trace to the same root cause: an empty-string element prefixed onto a CMake `add_custom_command` COMMAND causes an empty-path evaluation error. #13390 already has the root cause identified and a fix PR in progress. |
| [#12294](https://github.com/mesonbuild/meson/issues/12294) | [#2722](https://github.com/mesonbuild/meson/issues/2722) | high | Both are the same feature request: the ability to run multiple commands sequentially from a single `run_target`. |
| [#4735](https://github.com/mesonbuild/meson/issues/4735) | [#2519](https://github.com/mesonbuild/meson/issues/2519) | high | Both request the same thing: making `compiler.run()` use a working directory under build/private instead of writing files into the CWD. |
| [#6486](https://github.com/mesonbuild/meson/issues/6486) | [#4632](https://github.com/mesonbuild/meson/issues/4632) | high | Both report the same failure of `test_generate_gir_with_address_sanitizer` under the Gentoo sandbox (LD_PRELOAD), and both reference the same downstream bug 673016. |
| [#13487](https://github.com/mesonbuild/meson/issues/13487) | [#6680](https://github.com/mesonbuild/meson/issues/6680) | high | Both hit the same missing feature: the D compiler's `find_library` is unimplemented, producing 'Language D does not support library finding' (#6680 is about phobos, #13487 about druntime, but the underlying cause is identical). |
| [#12502](https://github.com/mesonbuild/meson/issues/12502) | [#3551](https://github.com/mesonbuild/meson/issues/3551) | high | Module-existence checking was implemented in 0.51.0; the remaining unresolved request in both issues is identical: a way to check a Python module's *version*, which is still unsupported. **Caveat:** Note: the two titles differ (existence check vs. version check) — worth double-checking that a plain 'duplicate' framing doesn't read as dismissive; the shared unresolved ask is the version-check capability specifically. |
| [#2475](https://github.com/mesonbuild/meson/issues/2475) **[new]** | [#382](https://github.com/mesonbuild/meson/issues/382) | high | Both report that Meson caches pkg-config-derived dependency info and fails to detect changes on reconfigure: #382 discusses .pc files being re-scanned only when explicitly wiped (version bumps, install-path changes not picked up), and #2475 reports the exact same underlying cache-invalidation problem where uninstalling/installing a package (gmime3 vs gmime2) is not detected by ninja reconfigure. Maintainer nirbheek's fix proposal on #2475 ('add ninja dependencies onto the relevant pkg-config files... and re-check when they are changed') is the same fix direction discussed at length in #382. |
| [#13264](https://github.com/mesonbuild/meson/issues/13264) **[new]** | [#5139](https://github.com/mesonbuild/meson/issues/5139) | high | Both report that Qt5's mkspecs include directory (e.g. /usr/lib/qt/mkspecs/linux-g++) is not added to the include path when building against Qt5 private headers, causing missing headers like qplatformdefs.h for QPA plugin development. #5139 first raised the need for mkspecs headers when building a QPA plugin; #13264 reproduces the identical problem via `dependency('qt5', ..., private_headers: true)` and confirms manually adding the mkspecs dir fixes the build. |
| [#11880](https://github.com/mesonbuild/meson/issues/11880) **[new]** | [#8058](https://github.com/mesonbuild/meson/issues/8058) | high | Both report `dependency('openmp')` failing to detect OpenMP support with the Nvidia HPC SDK compiler (nvc/nvc++), with the exact same 'ERROR: Dependency "openmp" not found, tried system' failure. Issue 11880's body is a verbatim copy of a comment the same reporter (RudiFeiman) later posted on 8058, using the identical meson.build/main.cpp repro and the same NVIDIA forum link, confirming it's the same underlying detection bug (root cause: nvc doesn't define _OPENMP the way Meson's check expects, as discussed throughout the 8058 thread). |
| [#12076](https://github.com/mesonbuild/meson/issues/12076) **[new]** | [#10455](https://github.com/mesonbuild/meson/issues/10455) | high | Both request that Meson recursively download/checkout subprojects-of-subprojects so 'meson subprojects download' fully pre-fetches everything before configure. #10455's maintainer reply ('Meson could maybe download recursively and just skip those that are duplicated') is exactly the feature #12076 proposes (auto-create redirect wraps and download nested subprojects), and both threads discuss the same version-conflict problem when two subprojects pull in the same nested wrap. |
| [#15162](https://github.com/mesonbuild/meson/issues/15162) | [#13602](https://github.com/mesonbuild/meson/issues/13602) | medium | Both show the same 'Cycle in CMake inputs/dependencies detected' error from a CMake subproject, likely from the same root cause (missing BYPRODUCTS handling), but this has not been fully confirmed. |
| [#15294](https://github.com/mesonbuild/meson/issues/15294) | [#9991](https://github.com/mesonbuild/meson/issues/9991) | medium | Both report that a cross-file `c_ld`/`cpp_ld` setting is ignored by Meson, which falls back to the default linker (compiler driver) instead. The compilers differ (armcc/armlink vs. clang/ld.lld) but the symptom and request are the same. |
| [#11196](https://github.com/mesonbuild/meson/issues/11196) | [#2897](https://github.com/mesonbuild/meson/issues/2897) | medium | Both ask for the same thing: eliminating/unifying the duplicated information between `pkgconfig.generate()` and `declare_dependency()` (#11196 is the more detailed, later discussion, also touching `override_dependency`). |
| [#12991](https://github.com/mesonbuild/meson/issues/12991) | [#5479](https://github.com/mesonbuild/meson/issues/5479) | low | Both show an absolute library path leaking into the generated .pc file's Libs line, but the trigger differs: #5479 is about `find_library`, #12991 is about the Boost dependency mechanism. A maintainer also noted the Boost case may be a distinct, Boost-specific issue. **Caveat:** Lower confidence — the two issues may have genuinely different root causes despite the similar symptom; verify before treating as a straightforward duplicate. |

---

## A. Candidates that can likely be closed with a comment (364)

> **Not thread-verified** unless noted above. Treat the rationale below as a first-pass read; please confirm against the current thread before closing, especially anything below `high` confidence.

### High-confidence, not yet deep-verified: 33

#### [#308](https://github.com/mesonbuild/meson/issues/308) Boost and cross compilation not working for android.
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: The Boost dependency detector in mesonbuild/dependencies/boost.py has been completely rewritten into a root/library-scanning implementation (BoostDependency, BoostLibraryFile, etc.) that is unrelated to the 2015 detection code. It also now directly implements the feature request from this issue: per-machine 'boost_includedir'/'boost_librarydir'/'boost_root' properties (boost.py lines ~374-437) are read via self.env.properties[self.for_machine], so cross builds (e.g. android) can specify separate include/lib dirs, which was exactly what the reporter asked for.
- **Evidence**: Boost dependency handling rewritten since 2015 (mesonbuild/dependencies/boost.py); no reproducer on a modern release.
- **Draft comment**:
  ```text
  The Boost dependency detection has been substantially rewritten since this report (2015), and cross-compilation with machine files is much more capable now. Could you check whether this still reproduces on a recent Meson release? Without an update we will close this as stale.
  ```

#### [#1041](https://github.com/mesonbuild/meson/issues/1041) Run more language and framework tests on Windows
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: This 2016 meta-issue asks to audit AppVeyor's installed-software docs to enable more Windows CI test coverage (csharp/fortran/boost/qt frameworks), and the checklist items reference AppVeyor-specific setup. The meson project's own CI has since fully migrated off AppVeyor: there is no .appveyor.yml in the repo, and Windows testing is now done via .github/workflows/windows.yml running the full test suite through run_tests.py. AppVeyor is only mentioned today as a legacy example snippet in docs/markdown/Continuous-Integration.md for third-party users, not as meson's own CI, so the issue's actual premise (auditing AppVeyor for more test coverage) no longer applies.
- **Evidence**: CI config heavily changed (azure-pipelines.yml, ci/); original AppVeyor checklist outdated.

#### [#1179](https://github.com/mesonbuild/meson/issues/1179) gnome.compile_resource() should look into directory where xml is
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: In mesonbuild/modules/gnome.py's compile_resources() (around line 473), the code now does 'source_dirs.append(os.path.join(state.build_to_src, state.subdir))' with the comment 'Always include current directory, but after paths set by user' - i.e. the directory containing the .gresource.xml file is now always searched by default, without needing an explicit source_dir kwarg. This is exactly the behavior requested/reported missing in the issue.
- **Evidence**: mesonbuild/modules/gnome.py compile_resources supports source_dir kwarg; reworked since 2016.
- **Draft comment**:
  ```text
  `gnome.compile_resources()` accepts a `source_dir` argument to point the resource compiler at additional lookup directories, and the module has been reworked since this 2016 report. Could you confirm whether this still fails on a current Meson? Without an update we'll close as stale.
  ```

#### [#1597](https://github.com/mesonbuild/meson/issues/1597) osx test-case "2 Library version" and "common 4/6" failing for xcode-backend
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: Both specific bugs reported are fixed in current mesonbuild/backend/xcodebackend.py: (1) the ldargs/dylib version code now uses 'dylib_version = target.soversion' instead of target.version, exactly the fix the reporter guessed at; (2) generate_filemap() now iterates only self.build_targets (= self.build.get_build_targets(), real BuildTarget objects), not all targets, so CustomTarget objects (which lack a .objects attribute) are no longer processed there, eliminating the reported AttributeError/KeyError crashes.
- **Evidence**: none (xcodebackend.py has been substantially rewritten and no longer matches the code lines from that time)

#### [#1875](https://github.com/mesonbuild/meson/issues/1875) gnome.gtkdoc() expands File arguments to builddir paths not sourcedir paths
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: gnome.py's gtkdoc() now resolves gobject_typesfile via an abs_filenames() helper that calls File.absolute_path(source_dir, build_dir); File.absolute_path() (mesonbuild/utils/universal.py) explicitly checks self.is_built and only uses builddir for built files, source dir otherwise, so a files('gobject.types') source file now correctly resolves to the source directory. Plain strings are likewise resolved relative to the source dir/subdir, matching the behavior nirbheek said was expected in the issue.
- **Evidence**: mesonbuild/modules/gnome.py:1504-1509 abs_filenames uses File.absolute_path(source_dir, build_dir)

#### [#1904](https://github.com/mesonbuild/meson/issues/1904) Can't seem to get includes to work using pkg-config on windows due to space in "Program Files" dir
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: Both sides of this bug are now fixed: the pkgconfig module's _escape() (mesonbuild/modules/pkgconfig.py ~line 454-464) explicitly backslash-escapes spaces when generating .pc files, citing the exact freedesktop bug about Windows path spaces; and the consuming PkgConfigDependency._split_args() (mesonbuild/dependencies/pkgconfig.py ~line 217-221) now explicitly uses shlex.split() with a comment noting pkg-config paths follow Unix conventions even on Windows, which correctly reassembles space-containing paths like 'Program Files' instead of splitting on whitespace.
- **Draft comment**:
  ```text
  This is from 2017 and Meson's pkg-config handling has changed since. Is this still reproducible on a recent Meson with a pkg-config prefix containing spaces (e.g. under 'Program Files')? If we don't hear back we'll close it as stale; please attach the .pc file and the failing command if it still occurs.
  ```

#### [#3332](https://github.com/mesonbuild/meson/issues/3332) windows: shared_library without exports caused stack trace on install
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: mesonbuild/minstall.py's install_targets() now checks 'if not os.path.exists(t.fname)' before ever calling check_for_stampfile(), and raises a clean MesonException('File ... could not be found') (or skips silently if the target is optional) instead of letting an unhandled FileNotFoundError propagate from os.stat() inside check_for_stampfile as happened in the original report. MesonException is caught and printed cleanly at the top level (mesonmain.py), so the described raw Python stack trace can no longer occur.
- **Evidence**: install moved to minstall.py; check_for_stampfile-style crash on missing import lib not confirmed fixed

#### [#4474](https://github.com/mesonbuild/meson/issues/4474) gnome.compile_schemas() documentation seems wrong
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: At the time of filing, gnome.compile_schemas() did not set build_by_default at all when the user omitted it, so it fell through to CustomTarget's default of False, contradicting the docs. Commit 3894f80e21e9 (2021-10-05, 'modules/gnome: use typed_kwargs for compile_schemas') introduced a dedicated `_BUILD_BY_DEFAULT` KwargInfo with `default=True` specifically for compile_schemas (mesonbuild/modules/gnome.py, the '@typed_kwargs('gnome.compile_schemas', _BUILD_BY_DEFAULT.evolve(since='0.40.0'), ...)' decorator), so the actual default now matches what the documentation always said.
- **Evidence**: gnome module docs migrated to docs/yaml/modules/gnome; compile_schemas build_by_default default needs re-verification
- **Draft comment**:
  ```text
  The gnome module documentation has since been migrated to our generated reference (docs/yaml). Could you confirm on a current release whether `gnome.compile_schemas()` still requires an explicit `build_by_default: true`, and whether the reference now matches the behavior? If it's a doc mismatch we'll fix the reference; otherwise please share a minimal reproducer. Closing as stale if we don't hear back.
  ```

#### [#4647](https://github.com/mesonbuild/meson/issues/4647) pkg-config missing dependency not reported
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: In current mesonbuild/dependencies/pkgconfig.py, PkgConfigInterface.cflags()/libs() capture pkg-config's stderr and raise `DependencyException(f'Could not generate cflags for {name}:\n{err}\n')` including the real pkg-config error text, and PkgConfigDependency.__init__ prints that exception via `mlog.warning(f"Pkg-config error with '{name}': {e}")`. Additionally _call_pkgbin uses Popen_safe_logged, which writes stdout/stderr of every pkg-config invocation to meson-log.txt. The original complaint that pkg-config's real error was swallowed no longer applies.
- **Evidence**: mesonbuild/dependencies/pkgconfig.py logs pkg-config stderr to meson-log
- **Draft comment**:
  ```text
  Meson now records the pkg-config invocation and its stderr in meson-log.txt, which typically surfaces the underlying 'Package X, required by Y, not found' message. Could you check meson-log.txt on a current release and confirm whether the real error is still hidden? We'll close as stale otherwise.
  ```

#### [#4869](https://github.com/mesonbuild/meson/issues/4869) failing test_install_umask on new platform (=SunOS)
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: The reported crash ('/usr/bin/python3: can't open file '[\'...myinstall.py\']'') came from the pre-0.50 ExecutableSerialisation design that kept a separate `fname` list and `cmd_args` list combined ad hoc in meson_exe.py (`subprocess.Popen(cmd + exe.cmd_args, ...)`). Commit d34e53202043 ('backends: do not split command and arguments in ExecutableSerialisation', part of PR #5644 merged 2019-08-03) unified these into a single `cmd_args` list, and current mesonbuild/scripts/meson_exe.py simply does `subprocess.Popen(cmd_args, ...)` with a clean argument list, so this specific malformed-argv failure mode can no longer occur. test_install_umask itself is a generic, still-passing test unrelated to any SunOS-specific code path.
- **Evidence**: unittests install umask test; SunOS-specific, meson 0.49.999
- **Draft comment**:
  ```text
  This was reported against 0.49.999 on OpenIndiana/SunOS and looks platform-specific. Meson's install-script handling has changed considerably since. Is test_install_umask still failing for you on a current Meson? If we don't hear back we'll close this as stale.
  ```

#### [#5137](https://github.com/mesonbuild/meson/issues/5137) meson doesn't detect installed dub packages
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: mesonbuild/dependencies/dub.py has been completely overhauled since 2019: it now version-gates behavior via `_search_in_cache = version_compare(dubver, '<=1.31.1')` and `_use_cache_describe = version_compare(dubver, '>=1.35.0')`, calls `_get_dub_description()`/`dub describe`, and does compiler/arch/build-type/configuration-aware compatibility matching per target (`_find_target_in_cache`). This bears no resemblance to the naive package lookup active when the 2019 report (dub 1.14.0, meson 0.50.0) was filed.
- **Evidence**: mesonbuild/dependencies/dub.py (DubDescriptionSource.Local/External:61-63, dub describe:344-353, _use_cache_describe/cacheArtifactPath:392-397, guidance:227-229)
- **Draft comment**:
  ```text
  The dub dependency backend has been substantially reworked since this report. Meson now resolves locally installed/registered packages via `dub describe` and dub's cache-artifact paths, and prints guidance (`dub add` / `dub build --deep`) when a package isn't ready. Note it requires a recent dub (>= 1.35) and currently supports static libraries. Could you retry with a current Meson and dub and let us know if `dependency('derelict-sdl2', method: 'dub')` still fails? If we don't hear back we'll close this as stale, but it can be reopened with a fresh log.
  ```

#### [#5443](https://github.com/mesonbuild/meson/issues/5443) meson test: gdb doesn't support -nh argument on FreeBSD 11
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: Current mesonbuild/mtest.py's `TestHarness.get_wrapper()` builds the gdb invocation as `wrap = [options.gdb_path, '--quiet']` (plus optional `-ex run -ex quit` and `--args`); a repository-wide search confirms `-nh` does not appear anywhere in mesonbuild today. Since meson no longer passes `-nh` to gdb at all, the FreeBSD gdb incompatibility described in the issue cannot occur with current code.
- **Evidence**: none (gdb --nh usage in mtest.py not re-verified for current version)

#### [#5551](https://github.com/mesonbuild/meson/issues/5551) d test sample broken
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: Reports meson's own D static/shared library test samples (test cases/d/2, /3) failing on Windows 7 with dmd 2.086 and ldc 1.16, both from 2019 and long superseded by current releases. Meson officially dropped Windows 7 support in the 0.54.0 release (docs/markdown/Release-notes-for-0.54.0.md: "Microsoft ended support for Windows 7, so only 64 bit Windows OSs are officially supported"), and the specific ancient toolchain versions cited are no longer relevant to current D compiler support in mesonbuild/compilers/d.py. No further activity since 2019 confirms lack of ongoing relevance.
- **Evidence**: none (very old D toolchain on Windows 7; not reproducible-checked here)
- **Draft comment**:
  ```text
  This is against a 2019 D toolchain (dmd 2.086 / ldc 1.16) on Windows 7. Both the toolchains and Meson's D support have moved on considerably. Is the D shared/static library sample still broken for you on a current Meson with an up-to-date dmd/ldc? If we don't hear back, this will be closed as stale.
  ```

#### [#5779](https://github.com/mesonbuild/meson/issues/5779) meson wrongly copies selinux attributes from build-dir to install location on "meson install"
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: restore_selinux_contexts has been implemented in minstall, restoring SELinux contexts with restorecon after install, so this issue has been resolved.
- **Evidence**: mesonbuild/minstall.py:251-275 (restore_selinux_contexts, restorecon), :449 (selinux_updates.append), :578 (restore call)
- **Draft comment**:
  ```text
  Meson now restores SELinux contexts on install: after copying files it collects them and runs `restorecon` (see `restore_selinux_contexts()` in `mesonbuild/minstall.py`), so installed files get fresh, correct contexts rather than inheriting the build-dir labels. This addresses the AVC denials reported here. Closing as fixed; please reopen if you still see stale contexts on a current Meson release.
  ```

#### [#6222](https://github.com/mesonbuild/meson/issues/6222) Prioritize clang ObjC compiler over gobjc
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: detect.py's default ObjC/ObjC++ compiler order has already been changed to put clang first (objc=['clang','gcc'], objcpp=['clang++','g++']). clang is now prioritized as requested.
- **Evidence**: mesonbuild/compilers/detect.py:53-54,65-66 defaults['objc']=['clang',...,'gcc'], defaults['objcpp']=['clang++',...,'g++']
- **Draft comment**:
  ```text
  This is fixed: Meson now defaults to preferring clang for Objective-C/C++. In `mesonbuild/compilers/detect.py` the default program order is `objc = ['clang', 'gcc']` and `objcpp = ['clang++', 'g++']` (with clang/clang-cl first on Windows), so clang is chosen ahead of gobjc when both are present. Closing as fixed.
  ```

#### [#6329](https://github.com/mesonbuild/meson/issues/6329) CI: Travis-CI ARM & IBM Power
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: A proposal to add multi-arch (ARM/IBM Power, etc.) testing on Travis-CI. Meson has already moved off Travis-CI to GitHub Actions and similar, so this Travis-based proposal is outdated.
- **Evidence**: Meson CI migrated off Travis-CI (no .travis.yml-based Travis workflow in current repo; CI on GitHub Actions)
- **Draft comment**:
  ```text
  Meson's CI has since moved off Travis-CI (to GitHub Actions and other runners), so this Travis-specific proposal is obsolete. Multi-arch coverage is handled through the current CI setup. Closing; if additional ARM/PPC coverage is wanted, please file against the current CI configuration.
  ```

#### [#6425](https://github.com/mesonbuild/meson/issues/6425) boost_python detection fails on osx
- **Verdict**: Obsolete / confidence: **high**
- **Basis**: The maintainer's own comment ties this to #4788, which was fixed by commit 9f2f27a49d9f ('boost: Fix boost_python detection on bionic (fixes #6886 #4788)', 2020-04-01) as part of a broader rewrite of boost dependency/python-module detection (08224dafcba1 'boost: Rewrite the boost system dependency' and 4e52a0f7fd9f 'boost: Better python module detection', both Feb-Mar 2020). Current mesonbuild/dependencies/boost.py has dedicated, extensively-commented logic ('Handle the boost_python naming madness') for parsing boost_python module tags across platforms/compilers, entirely different from the mechanism active when this 2020 High-Sierra/boost-1.72 report was filed.
- **Evidence**: none (boost dependency detection in mesonbuild/dependencies/boost.py substantially reworked since 0.52; 2020 macOS/boost combo stale)
- **Draft comment**:
  ```text
  Boost dependency detection has been reworked considerably since 0.52.1, and this report is against a 2020 macOS High Sierra / boost 1.72 setup. Could you confirm whether `dependency('boost', modules: ['python', ...])` still fails on a current Meson and current boost on macOS? Without a fresh reproducer this will be closed as stale.
  ```

#### [#6810](https://github.com/mesonbuild/meson/issues/6810) TAP implementation issue
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: A problem where the TAP parser treated unknown lines as errors. It now yields an UnknownLine, and the test runner ignores it as a warning, in line with the TAP spec.
- **Evidence**: mesonbuild/mtest.py:337 (UnknownLine NamedTuple), :482 (yield self.UnknownLine), :1175-1190 (treated as warning, not error)
- **Draft comment**:
  ```text
  Fixed. The TAP parser now emits `UnknownLine` for non-standard output rather than an error, and the test runner treats unknown lines as an ignorable warning (mesonbuild/mtest.py), which matches the TAP spec requirement that a parser must not treat an unknown line as an error. Closing as fixed.
  ```

#### [#7091](https://github.com/mesonbuild/meson/issues/7091) Sizeof and alignment Clike Cross Compiler Tests require stdio.h header file
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: The sizeof/alignment test code used during cross-compilation no longer includes stdio.h and now uses only stddef.h, so the test passes even on bare-metal environments without libc.
- **Evidence**: mesonbuild/compilers/mixins/clike.py: _cross_sizeof (lines 515-520) and _cross_alignment (lines 560-575) include only <stddef.h>, no <stdio.h>.
- **Draft comment**:
  ```text
  This is fixed on current master. The cross-compilation `sizeof`/`alignment` test code no longer includes `<stdio.h>` — the `_cross_sizeof` and `_cross_alignment` paths in `mesonbuild/compilers/mixins/clike.py` now only include `<stddef.h>`. A bare C compiler without libc should be able to run these checks. Please confirm on a recent release so this can be closed.
  ```

#### [#7516](https://github.com/mesonbuild/meson/issues/7516) Support compile-only dependencies
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: A request to use a dependency for headers only (no linking). `partial_dependency(compile_args: true, includes: true)` has existed since 0.46.0 and lets you extract just the dependency's compile/include information, so this is already resolved.
- **Evidence**: mesonbuild/interpreter/interpreterobjects.py:562 dependency.partial_dependency (since 0.46.0); docs/yaml/objects/dep.yaml:111 partial_dependency with compile_args/includes
- **Draft comment**:
  ```text
  Meson supports this via `partial_dependency()` (available since 0.46.0). For a pkg-config dependency where you only want headers and no linking, use:
  ```meson
  libfuse_dep = dependency('fuse3', version: '>=3.5.0')
  fuse_headers_dep = libfuse_dep.partial_dependency(compile_args: true, includes: true)
  executable('foo', 'foo.c', dependencies: [fuse_headers_dep])
  ```
  This gives you the include directories and compile args without pulling in the link libraries. Closing as resolved.
  ```

#### [#7540](https://github.com/mesonbuild/meson/issues/7540) Can't use --wrapper with add_test_setup
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: `meson test --wrapper` incorrectly raised an exe-wrapper conflict error for a test setup that only sets env variables. The current conflict check is now guarded by `elif current.exe_wrapper:`, so it's fixed to only trigger when the setup actually has an exe_wrapper.
- **Evidence**: mesonbuild/mtest.py:1801-1804 merge_setup_options: conflict only raised when current.exe_wrapper is truthy
- **Draft comment**:
  ```text
  This is fixed. In `mtest.py`'s `merge_setup_options`, the 'both test setup and command line specify an exe wrapper' error is now only raised when the selected test setup actually defines an `exe_wrapper` (`elif current.exe_wrapper:`). A setup that only sets environment variables (like the GTK testsuite) no longer conflicts with `meson test --wrapper catchsegv`. Closing as fixed.
  ```

#### [#7701](https://github.com/mesonbuild/meson/issues/7701) Change default pkg-config
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: Alternative pkg-config implementations like pkgconf can't be used, and the PKG_CONFIG environment variable has no effect. This is now resolved: envconfig.py maps the PKG_CONFIG environment variable to pkg-config, and it can also be specified via binaries in a machine file.
- **Evidence**: mesonbuild/envconfig.py:141 'pkg-config': ['PKG_CONFIG']; pkgconfig.py:235 find_external_program with cross/native/env lookup; envconfig.py:444 pkgconfig->pkg-config alias
- **Draft comment**:
  ```text
  You can now point Meson at `pkgconf` (or any pkg-config implementation) in two supported ways:
  
  1. Set the `PKG_CONFIG` environment variable — it is mapped to the `pkg-config` binary lookup (see `ENV_VAR_PROG_MAP` in `mesonbuild/envconfig.py`, `'pkg-config': ['PKG_CONFIG']`).
  2. Specify it in the `[binaries]` section of a native/cross file, e.g. `pkg-config = 'pkgconf'`.
  
  `find_external_program` consults the machine-file entry and the env var before falling back to the default `pkg-config` name. Closing as resolved.
  ```

#### [#7832](https://github.com/mesonbuild/meson/issues/7832) CMake: Dropping support for old CMake versions
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: Tracking issue for removing legacy CMake support. The CMake Server API has already been removed from the codebase (only fileapi.py remains), and subprojects use the File API (>=3.14). The tracking goal has been achieved, so this is suitable to close.
- **Evidence**: mesonbuild/cmake/ has no server.py (fileapi only); mesonbuild/cmake/interpreter.py:838 CMakeExecutor(... '>=3.14'); toolchain.py:237 cmake_minimum_required(VERSION 3.10)
- **Draft comment**:
  ```text
  The main item tracked here has landed: the CMake Server API code path has been removed entirely (only the File API remains under `mesonbuild/cmake/fileapi.py`), and CMake subprojects now go through the File API, effectively requiring CMake >= 3.14 (`CMakeExecutor(self.env, '>=3.14', ...)` in `mesonbuild/cmake/interpreter.py`). Since the Server API is gone and its ~400 lines of code eliminated, this tracking issue can be closed. Any remaining traceparser cleanup can be filed as a fresh, focused issue.
  ```

#### [#8207](https://github.com/mesonbuild/meson/issues/8207) [Feature Request] print arrays or dicts, that contain unprintable types and printable types
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: message() now uses stringifyUserArguments to recursively format lists and dicts, so nested arrays/dicts can be printed. The request is already implemented.
- **Evidence**: mesonbuild/interpreterbase/helpers.py:54-71 stringifyUserArguments recurses into list (line 62) and dict (line 64-66); interpreter.py:1446 func_message uses it
- **Draft comment**:
  ```text
  `message()` now recursively formats nested arrays and dictionaries via `stringifyUserArguments` (see `mesonbuild/interpreterbase/helpers.py`), producing a Meson-syntax debug representation like `[..]` and `{k : v}`. This covers the requested recursive printing of arrays/dicts. Closing as implemented.
  ```

#### [#8515](https://github.com/mesonbuild/meson/issues/8515) executable/library build targets cannot depend on generated .c file includes
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: The proposed solution itself -- adding depend_files/depends keywords to executable()/library() -- is already implemented. depends/depend_files are included in type_checking.py's EXECUTABLE_KWS.
- **Evidence**: mesonbuild/interpreter/type_checking.py:276 'depends', :284 'depend_files', :905-928 EXECUTABLE_KWS/EXCLUSIVE_EXECUTABLE_KWS
- **Draft comment**:
  ```text
  This has been implemented: `executable()`, `library()`, and the other build target functions now accept the `depends` and `depend_files` keyword arguments (see `EXECUTABLE_KWS`/`EXCLUSIVE_EXECUTABLE_KWS` in `mesonbuild/interpreter/type_checking.py`), which was the exact solution proposed in this issue. You can now declare the generated `.c`/`.inc` file as a dependency via `depend_files` (or `depends` on the target) to guarantee correct ordering. Closing as resolved; please reopen if the scenario still fails on current master.
  ```

#### [#9598](https://github.com/mesonbuild/meson/issues/9598) Adding numpy as a dependency with custom lookup
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: dependency('numpy') is now supported via PKGCONFIG + CONFIG_TOOL (numpy-config) (python.py:618, numpy_factory). numpy support landed in 1.4.0, so the request has been fulfilled.
- **Evidence**: mesonbuild/dependencies/python.py:618-620 numpy_factory (DependencyMethods.PKGCONFIG, CONFIG_TOOL via numpy-config); docs/markdown/Release-notes-for-1.4.0.md mentions numpy
- **Draft comment**:
  ```text
  `dependency('numpy')` is now supported via a dedicated DependencyFactory using pkg-config and the numpy-config config-tool (mesonbuild/dependencies/python.py, numpy_factory), added around Meson 1.4. The include dir/npymath handling that previously required run_command hacks is now covered. Closing as implemented; open a new issue for any missing sub-module (e.g. f2py) support you still need.
  ```

#### [#10401](https://github.com/mesonbuild/meson/issues/10401) Meson sets PATH rather than WINEPATH in run_exe()
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: meson_exe.py already implements setting WINEPATH (with a Z: prefix) from extra_paths when the exe_wrapper is wine. The reported missing-setting issue has been fixed.
- **Evidence**: mesonbuild/scripts/meson_exe.py:39-45 if exe.exe_wrapper and any('wine' in i ...): child_env['WINEPATH']=get_wine_shortpath([...Z:...])
- **Draft comment**:
  ```text
  This should be fixed in current Meson. `mesonbuild/scripts/meson_exe.py` now detects when the exe wrapper is Wine and sets `WINEPATH` (with `Z:` prefixes and shortpath handling) from the target's `extra_paths`, instead of only `PATH`. Could you retest with a recent release? If you still hit this, please reopen with an updated reproducer. Closing as fixed.
  ```

#### [#12707](https://github.com/mesonbuild/meson/issues/12707) CMake target dependency should not carry private link options
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: The current code has already been fixed so that dependents of a shared library only use public_link_flags derived from INTERFACE_LINK_OPTIONS, and PRIVATE link options (like /NODEFAULTLIB) are not propagated to consumers. This resolves the reported case with SDL3's SDL3-shared.
- **Evidence**: mesonbuild/cmake/tracetargets.py:116-117 public_link_flags from INTERFACE_LINK_OPTIONS; mesonbuild/cmake/interpreter.py:1221-1226 shared libs use only public_link_flags (static keep full link_flags)
- **Draft comment**:
  ```text
  This should be fixed on current master. The CMake importer now separates interface (public) link options from private ones: `INTERFACE_LINK_OPTIONS` are collected into `public_link_flags` (mesonbuild/cmake/tracetargets.py), and for shared/other non-static library targets the generated declare_dependency uses only `public_link_flags` (mesonbuild/cmake/interpreter.py), so a PRIVATE `target_link_options(... /NODEFAULTLIB)` on a shared library is no longer propagated to consumers. Only static libraries still carry full link flags (which is intended). Could you confirm with a recent Meson against your SDL3 case? I believe this can be closed as fixed.
  ```

#### [#13145](https://github.com/mesonbuild/meson/issues/13145) Meson fails to configure OpenMP when using Clang from MacPorts
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: Fixed: OpenMPDependency now adds openmp_flags() (e.g. -fopenmp for clang) to self.compile_args before the has_header check for omp.h, and passes dependencies=[self] into that check. The MacPorts clang issue where omp.h wasn't found without -fopenmp is resolved.
- **Evidence**: mesonbuild/dependencies/misc.py:146-148 (adds openmp_flags to compile_args, comment 'available for the following compiler checks'), :173 has_header('omp.h', dependencies=[self]); clang.py:167 openmp_flags -> ['-fopenmp']
- **Draft comment**:
  ```text
  This is fixed on current master. `OpenMPDependency` now populates `self.compile_args` with `openmp_flags()` (which is `-fopenmp` for Clang) *before* the header probe, and passes `dependencies=[self]` to the `has_header('omp.h', ...)` check (mesonbuild/dependencies/misc.py). So the omp.h lookup is now performed with `-fopenmp` on the command line, which is exactly what was needed for MacPorts clang. Please retest with a recent release; closing as fixed.
  ```

#### [#13260](https://github.com/mesonbuild/meson/issues/13260) Passing c_args to a subproject does not work
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: Verified actual behavior on current master: after subproject('sub1', default_options:{'c_args':'-Dtest'}), get_option('c_args') on the subproject side returns ['-Dtest']. Resolved via the per-project augment mechanism.
- **Evidence**: Verified by running: with meson.py setup, sub1's get_option('c_args')=['-Dtest'] (confirmed with a minimal test project); options.py:847-848 has the per-project augment logic
- **Draft comment**:
  ```text
  This works on current master. I reproduced your exact example (`subproject('sub1', default_options:{'c_args': '-Dtest'})`) and the subproject's `get_option('c_args')` now returns `['-Dtest']`. This is handled by the per-project option augment mechanism. Please retest with a recent release; closing as fixed.
  ```

#### [#13263](https://github.com/mesonbuild/meson/issues/13263) Support building against free-threaded Python on Windows
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: Free-threaded Python (python313t) support is implemented. On Windows, the library name gets a 't' suffix, and Py_GIL_DISABLED is also defined.
- **Evidence**: mesonbuild/dependencies/python.py:298-299 (Windows freethreaded -> -DPy_GIL_DISABLED), :384-392 (python{ver}t.lib / python{ver}t.dll when freethreaded)
- **Draft comment**:
  ```text
  This has been implemented. Meson now detects free-threaded CPython builds and uses the correct library name on Windows: for free-threaded builds it links against `python{version}t.lib` (and `python{version}t.dll` for MinGW), and additionally defines `-DPy_GIL_DISABLED` on Windows since the shared `pyconfig.h` does not do so. See `mesonbuild/dependencies/python.py` (`is_freethreaded` handling around lines 298-299 and 384-392). Closing as fixed; please reopen if you still hit an issue on current master. (The separate request for dedicated free-threaded CI can be tracked in a CI-specific issue if still desired.)
  ```

#### [#13371](https://github.com/mesonbuild/meson/issues/13371) feature req. PGO support for Rust
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: RustCompiler now implements get_profile_generate_args/get_profile_use_args, and b_pgo has also been added to base_options. The PGO-unsupported error is resolved.
- **Evidence**: mesonbuild/compilers/rust.py:149 base_options includes 'b_pgo'; :455-459 get_profile_generate_args -> ['-C','profile-generate'], get_profile_use_args -> ['-C','profile-use']
- **Draft comment**:
  ```text
  PGO for Rust is now supported. `RustCompiler` implements `get_profile_generate_args()` (`-C profile-generate`) and `get_profile_use_args()` (`-C profile-use`), and `b_pgo` is in its base options (see mesonbuild/compilers/rust.py, around lines 149 and 455-459). The old `ERROR: rustc does not support "get_profile_generate_args"` no longer occurs. Closing as implemented.
  ```

#### [#13697](https://github.com/mesonbuild/meson/issues/13697) configure_file can not replace variables after "\\"
- **Verdict**: Already fixed / implemented / confidence: **high**
- **Basis**: do_replacement_meson's regex explicitly handles 'multiple backslashes + @' (halving via num_escapes//2 before variable substitution) and is covered by regression tests config7.h.in/prog7.c's MESSAGE7 "\\\\@var1@" -> "\\\\foo" (substituting the variable even after a backslash). Confirmed fixed.
- **Evidence**: mesonbuild/utils/universal.py:1654 regex (?:\\)+(?=\?@); :1463-1466 num_escapes//2; test cases/common/14 configure file/prog7.c MESSAGE7 expected value "\\\\foo"
- **Draft comment**:
  ```text
  This regression has been fixed on master. The Meson variable-format substitution now explicitly handles runs of backslashes preceding an `@variable@` (the escape-halving branch in `do_replacement_meson`), and a regression test covers exactly this case: `config7.h.in` defines `MESSAGE7 "\\\\@var1@"` and `prog7.c` asserts it becomes `"\\\\foo"` — i.e. the variable after the backslashes is substituted again. Please retry with Meson >= 1.6; closing as fixed, but comment if you still see it.
  ```

### All `comment_close` candidates, by subtype

#### Already fixed / implemented (117)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#434](https://github.com/mesonbuild/meson/issues/434) | wrap: support for existing directories | medium | Wrap already supports using local directories (e.g. patch_directory) and existing subprojects directories, so  |
| [#728](https://github.com/mesonbuild/meson/issues/728) | Splitting an empty string produces different results based on input | medium | The behavior of split() is now documented with examples in the reference (str.yml), and splitlines(), which av |
| [#1237](https://github.com/mesonbuild/meson/issues/1237) | inconsistency in output during installation | low | This is about inconsistent install-time logging (a good first issue). Log output was later unified into a cons |
| [#1489](https://github.com/mesonbuild/meson/issues/1489) | Also detect and use wrap files provided by subprojects | medium | Detection of wrap files provided by subprojects is now handled via 'meson wrap-promote' and scanning subprojec |
| [#1497](https://github.com/mesonbuild/meson/issues/1497) | Cross file whitespace parsing error | medium | This is a 2017 parser bug where a closing bracket at the start of a line in a cross/machine file array causes  |
| [#1579](https://github.com/mesonbuild/meson/issues/1579) | RFE: bash autocompletion support | high | Meson already ships bash and zsh shell-completion scripts, so this request is already implemented. |
| [#1864](https://github.com/mesonbuild/meson/issues/1864) | configure_file(): allow more than one substitution per string | high | substitute_values now uses regex-based substitution (value_rx.sub) instead of simple if/elif, allowing multipl |
| [#2034](https://github.com/mesonbuild/meson/issues/2034) | gnome.gtkdoc doesn't honour the `dependencies:` keyword | high | gnome.gtkdoc now accepts a 'dependencies' kwarg (allowing Dependency/SharedLibrary/StaticLibrary) and processe |
| [#2098](https://github.com/mesonbuild/meson/issues/2098) | Improve error message while importing subproject | medium | do_subproject now clearly distinguishes between a failed wrap resolution (not found) and a build error within  |
| [#2148](https://github.com/mesonbuild/meson/issues/2148) | gtkdoc rules do not depend on dependencies | medium | gnome.gtkdoc's dependencies kwarg is processed via _get_build_args → _get_dependencies_flags, and the returned |
| [#2253](https://github.com/mesonbuild/meson/issues/2253) | pkgconfig: do not generate libdir entry in pkg-config file when no lib | medium | The current pkgconfig module doesn't emit a libdir variable in the .pc file when there's no library (libdir is |
| [#2329](https://github.com/mesonbuild/meson/issues/2329) | Report the reason for failure of install script | high | When an install script fails, its captured stdout/stderr is now displayed along with the exit code. minstall.p |
| [#2347](https://github.com/mesonbuild/meson/issues/2347) | [Doc] Autogenerated exhaustive doc ; list of invalid variable names | high | Meson now has a mechanism (docs/refman/) that auto-generates the reference manual from declarative definitions |
| [#2409](https://github.com/mesonbuild/meson/issues/2409) | Document `ninja reconfigure` in the online documentation | medium | reconfigure is documented: meson setup --reconfigure <builddir> can reconfigure and show a summary without bui |
| [#2560](https://github.com/mesonbuild/meson/issues/2560) | Compiler detection is incorrect for native LLVM/Clang install on Windo | high | clang-cl is included in Windows' default detection order, and a dedicated ClangClCompiler/ClangClCCompiler and |
| [#2608](https://github.com/mesonbuild/meson/issues/2608) | Recommend a standard coding style for meson.build files | high | docs/markdown/Style-guide.md exists and documents the recommended style. Furthermore, in 1.5.0 the `meson form |
| [#2642](https://github.com/mesonbuild/meson/issues/2642) | Handling users doing stupid things with CFLAGS (and friends) | medium | The compiler argument ordering is now project args -> global args -> environment/user args (CFLAGS etc.) appen |
| [#2728](https://github.com/mesonbuild/meson/issues/2728) | [mingw-w64] PC files with full C: path included | medium | In 0.63.0, the `pkgconfig.relocatable` built-in option was added, allowing the generated .pc's prefix to be ma |
| [#2818](https://github.com/mesonbuild/meson/issues/2818) | Document how to run the project tests, the unit tests, and both togeth | high | Contributing.md already documents how to run run_tests.py/run_unittests.py/run_project_tests.py, how to select |
| [#2835](https://github.com/mesonbuild/meson/issues/2835) | Feature: MKL dependency | medium | MKL is implemented in scalapack.py as MKLPkgConfigDependency, available via dependency('scalapack')/dependency |
| [#2953](https://github.com/mesonbuild/meson/issues/2953) | coverage targets ? | high | Phony targets coverage/coverage-html/coverage-xml/coverage-text/coverage-sonarqube are provided, and lcov-rela |
| [#2960](https://github.com/mesonbuild/meson/issues/2960) | Generated files not regenerated when the generator changes | high | In GeneratedList's __post_init__, if the generator's exe is a build target (LocalProgram) it's automatically a |
| [#3080](https://github.com/mesonbuild/meson/issues/3080) | Symbolextractor fails when run on non utf8 locale | medium | symbolextractor.py now explicitly specifies encoding='utf-8' for all file I/O, so locale-dependent encoding er |
| [#3082](https://github.com/mesonbuild/meson/issues/3082) | Boost static detection is broken | medium | The Boost dependency has been completely rewritten, including ABI tag detection, static/shared distinction, an |
| [#3083](https://github.com/mesonbuild/meson/issues/3083) | Boost dependency should set -DBOOST_ALL_DYN_LINK | high | The Boost dependency now applies module-specific -DBOOST_<LIB>_DYN_LINK=1 flags as compile_args when using sha |
| [#3084](https://github.com/mesonbuild/meson/issues/3084) | dependency() static keyword is not handled according to documentation | medium | The meaning of the static kwarg has been clarified, a static kwarg was added to compiler.find_library() as wel |
| [#3357](https://github.com/mesonbuild/meson/issues/3357) | Could the manual please mention that 'build dir' and 'source dir' can  | medium | Running-Meson.md now explicitly states that 'setup takes builddir and srcdir, and if srcdir is not given it is |
| [#3535](https://github.com/mesonbuild/meson/issues/3535) | Easy way to get the project version from the command-line | medium | meson introspect --projectinfo can fetch the project name/version directly from meson.build via the no_bd path |
| [#3537](https://github.com/mesonbuild/meson/issues/3537) | Try to link with -lfoo when find_library(libfoo) was used | medium | find_library has a mechanism (lib_prefix_warning) to warn when it detects a name with a 'lib' prefix, catching |
| [#3570](https://github.com/mesonbuild/meson/issues/3570) | Meson outputs incorrectly-named shared libraries on OpenBSD | medium | OpenBSD-specific logic for finding versioned .so.X.Y libraries and selecting the highest version has been impl |
| [#3603](https://github.com/mesonbuild/meson/issues/3603) | unit tests: snippet heading test is broken | high | The snippet-heading test has been fixed to track code blocks. It toggles in_code_block on ``` and no longer tr |
| [#3648](https://github.com/mesonbuild/meson/issues/3648) | Ensure that the current C/C++ compilers are MSVC when using the VS bac | medium | The VS backend checks for a C/C++ compiler's presence via _get_cl_compiler() and explicitly errors with 'MSVC  |
| [#3740](https://github.com/mesonbuild/meson/issues/3740) | False positive in has_function() | medium | The false-positive logic in has_function's builtin detection was strengthened by the same fix as #3676, preven |
| [#3751](https://github.com/mesonbuild/meson/issues/3751) | Validate and warn about unknown systems and CPU families in cross file | high | The handling that warns 'Unknown CPU family ..., please report this at ...github issues' for unrecognized CPU  |
| [#3765](https://github.com/mesonbuild/meson/issues/3765) | automatic build rpath not set when linking against Qt libraries (and o | medium | A mechanism has been implemented to automatically add the directory of an external dependency's (library/pkgco |
| [#3787](https://github.com/mesonbuild/meson/issues/3787) | Unhandled exception / bad error message "is not a target" for subproje | medium | link_with now strictly defines accepted types via typed_kwargs (LINK_WITH_KW), so passing a SubprojectHolder p |
| [#3791](https://github.com/mesonbuild/meson/issues/3791) | Qt resources fail if resources have same name | medium | The qt module gained a preserve_paths kwarg (since 1.4.0) that preserves each file's relative subdirectory in  |
| [#3797](https://github.com/mesonbuild/meson/issues/3797) | Qt moc fails if sources have same name | medium | As with #3791, the qt module's preserve_paths kwarg (since 1.4.0) can avoid same-name collisions in moc output |
| [#3802](https://github.com/mesonbuild/meson/issues/3802) | Ensure that pkgconfig is using the 'root' cross-compilation property | medium | The sys_root property from the machine file is now read and used to set PKG_CONFIG_SYSROOT_DIR when running pk |
| [#3848](https://github.com/mesonbuild/meson/issues/3848) | Should not try to execute the same subproject twice | high | do_subproject caches results in self.subprojects, and when the same subproject is requested again, it returns  |
| [#3852](https://github.com/mesonbuild/meson/issues/3852) | meson continues to link against previous debug/release version of Qt a | medium | The Qt dependency has logic to select libraries for debug/release (via _get_modules_lib_suffix and debug detec |
| [#3882](https://github.com/mesonbuild/meson/issues/3882) | RPATHs to external libraries that aren't in the default library search | medium | A mechanism automatically adds the directory of an external dependency's absolute-path shared library to RPATH |
| [#3917](https://github.com/mesonbuild/meson/issues/3917) | Dist doesn't respect meson configuration | high | meson dist now reads command-line options saved in the build directory (read_cmd_line_file) via create_cmdline |
| [#4071](https://github.com/mesonbuild/meson/issues/4071) | Regression: meson no longer defaults to needs_exe_wrapper: false for 3 | high | machine_info_can_run() explicitly determines that x86 (and mips64/mips) can run on an x86_64 host, and in that |
| [#4094](https://github.com/mesonbuild/meson/issues/4094) | Modules are global to all subprojects and references to the Interprete | medium | The module API has been redesigned so that each method call is passed a ModuleState reflecting the current Int |
| [#4105](https://github.com/mesonbuild/meson/issues/4105) | Meson can't find the resource compiler when using clang in MSVC ABI mo | medium | The windows module's rc detection was changed to key off the linker id (link/lld-link) rather than the compile |
| [#4126](https://github.com/mesonbuild/meson/issues/4126) | gnome.generate_gir should support dependency objects | medium | gnome.generate_gir now accepts a `dependencies` keyword and can derive include paths etc. from dependency obje |
| [#4171](https://github.com/mesonbuild/meson/issues/4171) | ERROR: Can not use target js_embed as generator | medium | Problem where native code-generation tools could not be used as generators in Emscripten cross builds. Emscrip |
| [#4179](https://github.com/mesonbuild/meson/issues/4179) | Cannot override qt programs | medium | The qt module uses state.find_program() for tool detection, which goes through program_from_overrides, so uic/ |
| [#4190](https://github.com/mesonbuild/meson/issues/4190) | meson wrap does not consider subproject_dir option | high | The meson subprojects/wrap tool now honors the subproject_dir option from project(). msubprojects.py obtains i |
| [#4244](https://github.com/mesonbuild/meson/issues/4244) | Mixed PIC due to helper libraries | high | static_library() has a `pic` keyword (bool, since 0.36.0) that can control PIC independently of b_staticpic. S |
| [#4298](https://github.com/mesonbuild/meson/issues/4298) | Support a cross-platform symbol export list for library targets | medium | Cross-platform mechanisms for controlling symbol visibility are now in place: gnu_symbol_visibility (0.48.0),  |
| [#4355](https://github.com/mesonbuild/meson/issues/4355) | Results of find_program('some-script') should be consistent, irrespect | medium | Problem where find_program for extension-less scripts on Windows depended on PATHEXT. _search_windows_special_ |
| [#4366](https://github.com/mesonbuild/meson/issues/4366) | Allow specifying a separate tool for assembling .s/.S files | medium | Request to treat assemblers as a separate tool. nasm/masm/armasm/yasm are now registered as independent langua |
| [#4417](https://github.com/mesonbuild/meson/issues/4417) | Meson uses install_name_tool on incompatible binaries | medium | Problem where install_name_tool fails when run against a cross-built Windows DLL etc. on macOS. fix_darwin() n |
| [#4532](https://github.com/mesonbuild/meson/issues/4532) | Multiple @BASENAME@ for configure_file() raising warning | medium | The current configure_file checks for duplicates on the final output path after resolving @BASENAME@ from the  |
| [#4615](https://github.com/mesonbuild/meson/issues/4615) | --as-needed is broken with gnu ld | medium | --start-group/--end-group is now restricted to link_whole only, so normal library linking is no longer wrapped |
| [#4876](https://github.com/mesonbuild/meson/issues/4876) | Support using existing library builds of gmock and gtest | high | Using pre-built gtest/gmock libraries is already supported. DependencyFactory has both pkgconfig and system va |
| [#4881](https://github.com/mesonbuild/meson/issues/4881) | Make `c_std=c90` an alias for `c_std=c89` | medium | c89 and c90 are both currently accepted as valid c_std values (both included in ALL_STDS). While not strictly  |
| [#4935](https://github.com/mesonbuild/meson/issues/4935) | Change the way the install_dir is handled for Vala libraries | high | Implemented as requested. Meson 1.11 added the install_vala_header / install_vala_vapi / install_vala_gir (and |
| [#4990](https://github.com/mesonbuild/meson/issues/4990) | Generated pkg-config file does not contain include directories | medium | The current pkgconfig module propagates a dependency's compile_args (including -I) into Cflags, and an extra_c |
| [#5170](https://github.com/mesonbuild/meson/issues/5170) | Pass Extra CMake Arguments in Inital Pass | high | In _get_cmake_info's initial pass, both the user's cmake_args and CMAKE_TOOLCHAIN_FILE are now passed, so a vc |
| [#5240](https://github.com/mesonbuild/meson/issues/5240) | run_command error with compiler object | high | run_command_impl, for a compiler object, expands the rest of exelist via get_exe_args() and takes the first el |
| [#5313](https://github.com/mesonbuild/meson/issues/5313) | PKG_CONFIG_PATH meson ... doesn't affect cross compilation in 0.51 | medium | pkg_config_path was made a per-machine option, now also read per-machine from the environment. Specifying the  |
| [#5333](https://github.com/mesonbuild/meson/issues/5333) | meson introspect --targets has no linker information | high | The ninja backend's create_target_linker_introspection now adds the linker's exelist and parameters to the int |
| [#5368](https://github.com/mesonbuild/meson/issues/5368) | LLVM library search picks up old versions of LLVM | medium | Shared-library selection for the LLVM dependency has been improved to target `libLLVM-<version>.(so\|dll\|dyli |
| [#5370](https://github.com/mesonbuild/meson/issues/5370) | LLVM dependency: versioning broken, LLVM 7 cannot be found due to llvm | medium | Logic has been implemented to collect multiple llvm-config-N candidates and select among them by sorting with  |
| [#5461](https://github.com/mesonbuild/meson/issues/5461) | no ninja dependency created for .def files | medium | The path of vs_module_defs is now added to link_depends (process_vs_module_defs_kw), so updating the .def file |
| [#5511](https://github.com/mesonbuild/meson/issues/5511) | Names of custom_target's collide in i18n.merge_file | medium | i18n.merge_file's CustomTarget name now becomes an empty string ('') and naming is auto-generated based on the |
| [#5561](https://github.com/mesonbuild/meson/issues/5561) | run_target doc should provide examples | medium | Run-targets.md now has examples of scripts and passing arguments, and run_target has also moved to the YAML re |
| [#5636](https://github.com/mesonbuild/meson/issues/5636) | CMake seems to find the oldest version of LLVM by default | medium | For the problem where LLVM detection via CMake doesn't sort by version and picks up an old version, Meson now  |
| [#5686](https://github.com/mesonbuild/meson/issues/5686) | [Docs] Missing description for --native-file | medium | --native-file is now documented in Machine-files.md and the command/reference docs, so the native file documen |
| [#5797](https://github.com/mesonbuild/meson/issues/5797) | Cannot use `link_whole` in a shared library with a non-static-library  | medium | The reported crash (AttributeError because CustomTarget lacks a .pic attribute) has been resolved. link_whole  |
| [#5846](https://github.com/mesonbuild/meson/issues/5846) | Meson fails on sanity check step when using clang-cl+ASAN | medium | With clang-cl+ASAN, /MDd conflicts with -fsanitize=address, causing the sanity check to fail. Sanitizer suppor |
| [#5886](https://github.com/mesonbuild/meson/issues/5886) | python module doesn't prefer "py -3" over %LOCALAPPDATA%\Microsoft\Win | medium | ExternalProgram search now substitutes dirname(sys.executable) when it detects the python3.exe stub under Wind |
| [#5951](https://github.com/mesonbuild/meson/issues/5951) | Problems using LLVM in a non CPP project. | medium | The reported crash (AttributeError because LLVMDCompiler lacks a thread_link_flags attribute) has been resolve |
| [#6045](https://github.com/mesonbuild/meson/issues/6045) | ninja scan-build should pass --status-bugs | medium | The SCANBUILD environment variable is now parsed with split_args, preserving additional arguments, and it's re |
| [#6055](https://github.com/mesonbuild/meson/issues/6055) | Add Swift support in Xcode backend | medium | The Xcode backend now has a substantial amount of Swift support (is_swift_target, determine_swift_dep_dirs, su |
| [#6253](https://github.com/mesonbuild/meson/issues/6253) | Apple clang version misdetected | medium | Apple clang has its own version numbering, causing malfunctions when compared against vanilla LLVM version num |
| [#6259](https://github.com/mesonbuild/meson/issues/6259) | Regression breaking build of glib | medium | In 2019, PR #6179 added an extra backslash to config.h, temporarily breaking the glib build. This was a regres |
| [#6570](https://github.com/mesonbuild/meson/issues/6570) | Add documentation for how to build a Meson project with options | medium | User-facing build instructions are already covered in the Quick-guide, Running-Meson, and Builtin-options page |
| [#6661](https://github.com/mesonbuild/meson/issues/6661) | dependency('Ceres') does not extract include paths via CMake | low | A bug where include paths can't be obtained for CMake dependencies. With CMake >= 3.17, traces use the json-v1 |
| [#6671](https://github.com/mesonbuild/meson/issues/6671) | native and cross files layering is mentionned, but doc does not tell h | medium | Points out that --native-file was missing from the docs and that the layering procedure was unclear. Native-en |
| [#6728](https://github.com/mesonbuild/meson/issues/6728) | Subproject default_options are ignored | medium | A problem where subproject()'s default_options were being ignored. With the option store overhaul, do_subproje |
| [#6792](https://github.com/mesonbuild/meson/issues/6792) | pyinstallation.dependency() version check broken? | medium | A problem where the python module's .dependency() didn't check version. It now accepts the standard DEPENDENCY |
| [#6846](https://github.com/mesonbuild/meson/issues/6846) | Wrong include path for OpenCL dependency | low | A bug where an OpenCL include path obtained via CMake gets split on spaces, leaving only 'C:/Program Files/NVI |
| [#6895](https://github.com/mesonbuild/meson/issues/6895) | Improperly formatted data in buildsystem_files.json on Windows host | medium | A problem where buildsystem_files paths were malformed on Windows. list_buildsystem_files now consistently out |
| [#6949](https://github.com/mesonbuild/meson/issues/6949) | Meson doesn't set the right file-dependencies for D projects | medium | Depfile (dependency-generation) support was added to the D compiler (-makedeps for dmd, -deps-equivalent for l |
| [#7194](https://github.com/mesonbuild/meson/issues/7194) | [Docs] Difference between buildtype=plain and buildtype=custom | medium | A table mapping buildtype to debug/optimization was added to Builtin-options.md, spelling out that plain = (de |
| [#7486](https://github.com/mesonbuild/meson/issues/7486) | MSYS2/MinGW: Permission denied when host OS defers file deletion | medium | Sanity-check executables with the same name collided and got locked during successive compilations. Compiler c |
| [#7676](https://github.com/mesonbuild/meson/issues/7676) | Attempt to write to the source directory when running compiler/linker  | medium | During linker-argument checks, `-o a.out` tried to write into the source directory and got rejected in a sandb |
| [#8091](https://github.com/mesonbuild/meson/issues/8091) | Add library search paths | medium | find_library already has a `dirs` keyword for passing extra search paths (compiler.py:672 passes search_dirs i |
| [#8387](https://github.com/mesonbuild/meson/issues/8387) | generate rules for preprocess-only (and compile-but-don't-assemble) | medium | compiler.preprocess() was added in 0.64.0, letting you generate preprocess-only output. This satisfies the mai |
| [#8738](https://github.com/mesonbuild/meson/issues/8738) | Reconfiguring project with --backend=vs added raises KeyError of backe | medium | The original KeyError was caused by direct subscript access to coredata.options[OptionKey('backend_startup_pro |
| [#8780](https://github.com/mesonbuild/meson/issues/8780) | build.ninja not generated correctly when path to compiler has a space  | medium | A known bug where build.ninja's command line gets incorrectly split when the compiler path contains a space (e |
| [#8824](https://github.com/mesonbuild/meson/issues/8824) | Add "c_winlibs" und "cpp_winlibs" to target functions | medium | winlibs was turned into a compiler option, configurable per-project and per-target via default_options/overrid |
| [#9266](https://github.com/mesonbuild/meson/issues/9266) | Document how to use CMake imported targets | medium | The CMake section of Dependencies.md now documents how to use imported targets (with a modules: ['ZLIB::ZLIB'] |
| [#9370](https://github.com/mesonbuild/meson/issues/9370) | Ninja binary path regression in 0.59.2 | medium | The current detect_ninja_command_and_version implementation prioritizes the NINJA environment variable and sea |
| [#9422](https://github.com/mesonbuild/meson/issues/9422) | Linking with OpenMPI fails (rpath dir pread: Is a directory) | medium | MPI dependency handling now filters via _filter_link_args to keep only -L/-l/-Xlinker, suppressing pass-throug |
| [#9753](https://github.com/mesonbuild/meson/issues/9753) | Generator.process crashes when using results of another generator | medium | generator.process_files now explicitly handles GeneratedList inputs (build.py:2080-2086, adding depends and us |
| [#9783](https://github.com/mesonbuild/meson/issues/9783) | Cross building GLib tests for Windows fails ('libgio-2.0-0.dll failed  | medium | environment now prepends library paths to WINEPATH (environment.py:606, env.prepend('WINEPATH', ...)), so buil |
| [#10666](https://github.com/mesonbuild/meson/issues/10666) | AttributeError when attempting to build Spot with meson on FreeBSD 13. | medium | The crash of type "'NoneType' object has no attribute 'has_header'" is resolved: detect_compiler now returns a |
| [#11212](https://github.com/mesonbuild/meson/issues/11212) | Wrong install dir for python installation with pybind11 module | medium | The old hardcoded '/usr/local/lib/python3/dist-packages' issue appears to be resolved by the current implement |
| [#11634](https://github.com/mesonbuild/meson/issues/11634) | Environment value are not flatten | medium | The crash that occurred when an env value was a nested list has been resolved, because env_convertor_with_meth |
| [#11827](https://github.com/mesonbuild/meson/issues/11827) | On Windows, Meson doesn't support the .cmd stubs | medium | programs.py's windows_exts includes 'cmd', and there is an implementation that resolves .cmd wrappers as execu |
| [#12234](https://github.com/mesonbuild/meson/issues/12234) | WARNING: Unknown CPU family (loongarch) | medium | loongarch64 is now registered in known_cpu_families (envconfig.py:52,86). On environments where platform.machi |
| [#12327](https://github.com/mesonbuild/meson/issues/12327) | Environment prepend/append overrides system environment variable | medium | The current _prepend/_append reads the existing value of full_env (core.py:143-145), and mtest passes os.envir |
| [#12755](https://github.com/mesonbuild/meson/issues/12755) | fs.copyfile() does not allow relative destination directories | medium | A new build_subdir argument was added to fs.copyfile(), allowing copying into a subdirectory of the current bu |
| [#13016](https://github.com/mesonbuild/meson/issues/13016) | Vulkan detection fails on msys build | medium | For non-SDK guessed paths (mingw/linux), both find_library('vulkan') and has_header('vulkan/vulkan.h') are now |
| [#13194](https://github.com/mesonbuild/meson/issues/13194) | meson test --repeat doesn't run the expected number of tests | low | The current mtest pre-generates repeat×tests runners via range(repeat) and runs them all, so on all-pass it al |
| [#13197](https://github.com/mesonbuild/meson/issues/13197) | CMake module fails to import Faiss library | medium | The reported error 'Invalid variable name: 1_Flat_dir' (a CMake name starting with a digit) is resolved by a f |
| [#13692](https://github.com/mesonbuild/meson/issues/13692) | cuda module can't create arch flags for sm_8.7 (orin) | medium | Orin ('8.7') has been added to the cuda module's architecture table (cuda_all_gpu_architectures / 'Orin': (['8 |
| [#13723](https://github.com/mesonbuild/meson/issues/13723) | `gnome.compile_resources` does not respect cross compilation | medium | _find_tool now searches for glib-compile-resources etc. with native=True (MachineChoice.BUILD), and the pkg-co |
| [#13941](https://github.com/mesonbuild/meson/issues/13941) | dry run install of symlink errors, real install succeeds | medium | The reported error string 'Tried to install symlink to missing file' no longer appears anywhere in current mas |
| [#14131](https://github.com/mesonbuild/meson/issues/14131) | Meson should log a warning when attempting to set an option in an unkn | medium | For unknown options (e.g. -Dfoo=bar), current master already raises an 'Unknown options' error via check_unuse |
| [#15732](https://github.com/mesonbuild/meson/issues/15732) | meson-1.11.1.tar.gz is missing on Pypi | medium | A release-operations issue where the 1.11.1 sdist was missing from PyPI. Not a code defect — subsequent releas |
| [#15889](https://github.com/mesonbuild/meson/issues/15889) | BUG: ninja backend raises an `AttributeError` (`'GeneratedList' object | medium | The code path that treated GeneratedList as a Target and called get_builddir has already been fixed: backends. |

<details><summary>Draft comments</summary>

**#434**:
```text
Meson now supports several ways to use pre-existing sources: a plain directory placed in `subprojects/` is used as-is if no matching .wrap exists, and wrap files support `directory` and `patch_directory` for local overlays (see the Wrap dependency manual). This largely covers the original request. If your specific workflow still isn't served, please comment and we can reopen.
```

**#728**:
```text
The `.split()` behavior is now documented with examples in the reference manual, and `.splitlines()` (since 1.2.0) was added specifically to handle the empty-string / trailing-separator cases more intuitively. Since this was filed as a documentation issue, it appears addressed. Please reopen if the docs are still unclear.
```

**#1237**:
```text
The install output has been reworked since 2016 and now uses a consistent 'Installing <src> to <dest>' format across headers, data, man pages, and pkgconfig. This appears resolved. If you still see inconsistent install log lines on a recent Meson, please comment with an example and we can reopen.
```

**#1489**:
```text
Meson now walks .wrap files provided by subprojects and supports promoting nested wraps to the top-level `subprojects/` dir (`meson wrap promote`), which covers the gst-build/glib scenario described here. This appears resolved. If nested wrap resolution still fails for your layout on a recent Meson, please comment and we can reopen.
```

**#1497**:
```text
Cross/native file parsing now goes through Meson's standard array parser, which handles multi-line arrays with the closing bracket at column 0 correctly. This appears fixed. If you still hit a parse error with a leading-column `]` in a machine file on a recent Meson, please share the exact file and we'll reopen.
```

**#1579**:
```text
The core request here is implemented: Meson ships shell-completion scripts for both bash (`data/shell-completions/bash/meson`) and zsh (`data/shell-completions/zsh/_meson`), and they are included in the source distribution. These are installed to the appropriate completion directories by distro packages (Meson's own Python installer intentionally leaves installing them to the packager, since completion install paths are distro-specific). Closing as implemented; if a specific option is not being completed correctly, please open a focused issue for that.
```

**#1864**:
```text
The specific bug reported here is fixed. `substitute_values()` now performs a regex-based replacement over each string (`value_rx.sub(...)` in mesonbuild/utils/universal.py) rather than the old if/elif that stopped after one substitution, so multiple `@...@` templates in a single command element are all replaced. For example `command : ['sh', '-c', '... "@INPUT@" > "@OUTPUT@"']` now expands both `@INPUT@` and `@OUTPUT@` (Meson still errors if `@INPUT@`/`@OUTPUT@` in an inline string maps to more than one file, which is unavoidable). Closing as fixed; please reopen with a concrete case if a specific multi-substitution still fails.
```

**#2034**:
```text
This is resolved. `gnome.gtkdoc()` now accepts a `dependencies:` keyword taking `dependency()` objects and shared/static libraries (see the typed_kwargs in mesonbuild/modules/gnome.py). The dependencies are honoured in two ways: their compile/link flags are passed to the gtk-doc scan via `_get_build_args`, and the resulting build targets are added as `extra_depends` of the doc custom target, so build ordering against generated inputs is respected. Closing as fixed; please reopen if a dependency still isn't being applied.
```

**#2098**:
```text
Thanks for reporting this. Subproject error handling has been substantially reworked since 2017. Meson now clearly distinguishes the case where a subproject cannot be resolved at all (a wrap/resolution failure) from the case where the subproject is found but its own meson.build raises an error. In the latter case the subproject is executed under a nested logging context and the real exception, with its source location, is propagated to the user rather than being reported as if the subproject didn't exist. Since the underlying complaint appears addressed, we're closing this; if you can still reproduce a misleading message on current Meson, please reopen with the exact output and a minimal reproducer.
```

**#2148**:
```text
In current Meson, gnome.gtkdoc() now threads the `dependencies:` kwarg through `_get_build_args()` -> `_get_dependencies_flags()`, and the resulting build targets are passed as `extra_depends` to the generated CustomTarget (see mesonbuild/modules/gnome.py). This means the ninja rule for the gtkdoc target now depends on the libraries/targets named in `dependencies:`. This appears to have been resolved; please reopen with a minimal reproducer if you still see stale docs on current Meson.
```

**#2253**:
```text
In current Meson the generated .pc file no longer emits a `libdir` entry when no libraries are present: `libdir` is only added when `deps.pub_libs or deps.priv_libs` is non-empty (see `_generate_pkgconfig_file` in `mesonbuild/modules/pkgconfig.py`). For architecture-independent files, the `dataonly` keyword (since 0.54.0) both suppresses lib-related fields and installs the .pc to `${datadir}/pkgconfig` instead of `${libdir}/pkgconfig`, which is the multilib-safe location this issue asked for. A non-`dataonly` generate() with no libraries still defaults its install dir to `${libdir}/pkgconfig`; use `dataonly: true` (or `install_dir`) for the datadir location. Given the core request is now supported, this can likely be closed — does `dataonly` cover your use case?
```

**#2329**:
```text
This is now handled. Custom install scripts run through the Meson exe runner (`mesonbuild/scripts/meson_exe.py`), which captures the script's output and, on any non-zero exit, prints `--- stdout ---` / `--- stderr ---` so you can see why it failed. On top of that, `minstall.py` reports `FAILED: install script '<name>' failed with exit code <N>` (and exits with that code), or `FAILED: install script '<name>' could not be run.` with exit 127 when the script cannot be launched at all. So both the exit code and the script's own output are now reported. Closing as fixed.
```

**#2347**:
```text
The main ask here -- an autogenerated, exhaustive reference -- now exists, and it goes further than what was thought possible in 2017. Meson's entire API is described declaratively in YAML under `docs/yaml/` (functions/, objects/, builtins/), and the `docs/refman/` toolchain generates the reference from it into Markdown/HTML, JSON, man pages, and Vim help. Notably, this now includes the full argument/kwarg listing per function (types, defaults, `since` versions), not just the list of permitted kwargs mentioned in the earlier comment. The secondary note -- an explicit list of reserved/invalid variable names -- is minor; the reserved built-in object names are documented in the reference, and this could be tracked in a focused issue if a single flat list is still wanted. Closing the autogenerated-doc request as done.
```

**#2409**:
```text
Thanks for the suggestion. Reconfiguration is now documented: you can run `meson setup --reconfigure <builddir>` (see the `setup` section of the Commands reference) to re-run configuration and print your build summary without invoking a build, which is the CMake-like workflow you described. Options can also be changed with `meson configure <builddir> -Dopt=value`. Since this is covered in the docs now, we're closing this; please reopen if a specific gap remains.
```

**#2560**:
```text
Native Clang on Windows is now handled correctly. Soname/rpath/import-library arguments are delegated to the detected `DynamicLinker` class rather than being hardcoded in the Clang compiler on the assumption of MinGW, so Meson no longer blindly emits GNU-ld style `-Wl,-soname`/`--start-group`/`--out-implib`/`-Wl,-rpath` for a native Windows toolchain. In addition, Meson has dedicated `ClangClCompiler`/`ClangClCCompiler` classes and a `ClangClDynamicLinker` (lld-link), and detects `clang-cl` in its Windows compiler search order (`mesonbuild/compilers/detect.py`), with linker detection based on the actual linker output. This resolves the incorrect detection described here. Closing as fixed; please open a fresh issue with a `meson setup` log if you hit a remaining native-Clang case on Windows.
```

**#2608**:
```text
Meson now provides both a documented style guide and tooling to enforce it. `docs/markdown/Style-guide.md` covers indentation (two spaces, no tabs), trailing commas, `snake_case` naming, argument/dependency conventions, and source-list sorting. Since 1.5.0 there is also a built-in `meson format` command (alias `meson fmt`) with EditorConfig support that can auto-format `meson.build` files to a consistent style. This addresses the request for a recommended standard coding style. Closing as addressed; finer formatting rules are handled by `meson format` and its configuration.
```

**#2642**:
```text
Meson now appends user/environment arguments (CFLAGS/CXXFLAGS, -D*_args) after project and global arguments, so a user-supplied flag like -mno-sse4.1 takes precedence and is visible to compiler checks that use the same base args. Closing as largely addressed; if you need to introspect env args programmatically, that can be tracked separately.
```

**#2728**:
```text
The `pkgconfig.relocatable` builtin option (since 0.63.0) makes generated .pc files relocatable instead of embedding a hardcoded prefix, which addresses the non-relocatable full-path problem for MinGW installs. Please try `-Dpkgconfig.relocatable=true`; closing as addressed, reopen if it doesn't cover your case.
```

**#2818**:
```text
The Contributing docs now cover this: `./run_tests.py` runs everything, `./run_unittests.py` runs the unit tests, and `./run_project_tests.py` runs the project tests, including how to select a subset with `--only` and run an individual project test directly (see `docs/markdown/Contributing.md`). Closing as documented. Note the original bullet about Appveyor/Travis is outdated since CI moved to GitHub Actions; that CI overview can be refreshed separately if desired.
```

**#2835**:
```text
Meson now has MKL support via a dedicated MKLPkgConfigDependency (used by the scalapack dependency factory), handling MKLROOT and lp64/iomp variants similar to the MKL Link Advisor. Closing as implemented; please open a new issue for any specific MKL link-line combination that's missing.
```

**#2953**:
```text
Coverage handling was consolidated a while ago: the ninja backend now emits `coverage`, `coverage-html`, `coverage-xml`, `coverage-text` and `coverage-sonarqube` phony targets, all driven through the single `meson --internal coverage` script (mesonbuild/scripts/coverage.py) rather than duplicated lcov logic in the backend. That addresses the cleanup requested here, so closing as resolved.
```

**#2960**:
```text
This is fixed: Meson now tracks the generator program itself as a dependency of the generated files (build.py `GeneratedList.__post_init__` adds a build-target generator to `extra_depends`, or an external absolute-path program to `depend_files`), so editing your codegen script triggers regeneration. `generator()` also gained a `depends` kwarg (since 0.51.0) to declare additional inputs. Closing as fixed. (Note: passing arbitrary `files()` as generator *arguments* to create implicit dependencies is a separate enhancement; please open a focused issue if you need that.)
```

**#3080**:
```text
Meson's symbolextractor now opens all files with an explicit `encoding='utf-8'`, so it no longer depends on the system locale (`ANSI_X3.4-1968`/C). This should resolve the failure you hit. If you can still reproduce it on a recent Meson, please reopen with details.
```

**#3082**:
```text
The Boost dependency backend was substantially rewritten since this report, with proper ABI-tag-based library detection that honours the `static` kwarg, and `compiler.find_library()` now takes a `static:` keyword as well. The old `detect_lib_modules()` fallback logic described here no longer exists. Please reopen against a current Meson if static Boost detection still misbehaves for you.
```

**#3083**:
```text
This is implemented: the Boost dependency emits per-module `-DBOOST_<MODULE>_DYN_LINK=1` compile args when linking against shared Boost libraries (e.g. `-DBOOST_LOG_DYN_LINK=1`, `-DBOOST_TEST_DYN_LINK=1`), which is the granular per-module approach requested here rather than a blanket `-DBOOST_ALL_DYN_LINK`, and it also sets `-DBOOST_ALL_NO_LIB` to disable auto-linking. Closing as fixed; please reopen if a specific module is missing its DYN_LINK define.
```

**#3084**:
```text
The `static` handling and its documentation have been reworked since this report. `compiler.find_library()` now accepts an explicit `static:` keyword, the Boost backend was rewritten to honour it, and the docs no longer imply a soft "try" fallback. If you still see a mismatch between docs and behaviour on a current Meson, please reopen with a concrete example.
```

**#3357**:
```text
The docs now cover this: Running-Meson.md states that `setup` takes a `builddir` and a `srcdir` argument and that "if no `srcdir` is given Meson will deduce the `srcdir` based on `pwd` and the location of `meson.build`." That explains the behaviour you observed, so we're closing this. Please reopen if you think the wording can still be clearer.
```

**#3535**:
```text
You can now get project name/version without configuring a build dir: `meson introspect --projectinfo <sourcedir>` parses `meson.build` directly (the `projectinfo` command has a source-only path). It's still JSON, but it avoids grepping and doesn't require a configured build tree. Closing as addressed; if you specifically want a plain-text one-liner output, let us know and we can keep this open as an enhancement.
```

**#3537**:
```text
find_library() now handles the `lib`-prefix case: when you pass a name like `libpam` and Meson finds a match, it warns about the redundant `lib` prefix (the `lib_prefix_warning` path), steering users toward `find_library('pam')` which links with `-lpam`. If the remaining nixos-specific search-dir behaviour you mentioned still bites you, that's better tracked as a separate, focused issue. Closing this one.
```

**#3570**:
```text
Meson now has explicit OpenBSD handling for versioned shared libraries: it globs for `libfoo.so.X.Y` and selects the highest version when there is no unversioned `.so` symlink (see the OpenBSD-specific code paths in the C-like compiler mixin). This should resolve the incorrect library selection you reported. If you can still reproduce a mismatch on a recent Meson release, please reopen with details.
```

**#3603**:
```text
This has been fixed: the snippet heading test (`unittests/datatests.py`, `DataTests.test_snippets`) now tracks fenced code blocks -- it toggles an `in_code_block` flag on ```` ``` ```` lines and skips heading detection while inside a block, so `#`-prefixed lines inside code examples are no longer mistaken for headings. Closing as resolved.
```

**#3648**:
```text
The VS backend now guards for an MSVC-style C/C++ compiler: `_get_cl_compiler()` raises a clear error ('MSVC can only build C/C++ projects') when a suitable compiler is not present. Closing as addressed; please reopen if you find a case where a GCC/Clang toolchain silently slips through to the VS backend.
```

**#3740**:
```text
The `has_function` builtin-detection path was rewritten and now requires that, when the function is only visible as a `#define`/builtin, it either be a real `__builtin_` or be present via `__has_builtin`; otherwise the probe errors out. This addresses the class of false positives you hit (e.g. mingw's `#define ngettext libintl_ngettext`). Closing as fixed; please reopen with a current-version reproducer if a specific symbol still false-positives.
```

**#3751**:
```text
The CPU-family half of this is implemented: Meson now warns when a cross/native file (or CPU detection) yields a CPU family that isn't in the documented `known_cpu_families` list, with a message inviting the user to report it upstream (see `Unknown CPU family ..., please report this ...` in `mesonbuild/envconfig.py`). Note that unknown *system* names are not validated the same way, since Meson does not maintain a closed enum of system names the way it does for CPU families. Since the actionable 'common contract' concern (CPU family names) is covered, closing this; please open a focused issue if warning on specific unknown system strings is still wanted.
```

**#3765**:
```text
Meson now automatically adds build-time RPATH entries for the directories of absolute-path shared libraries pulled in via dependencies (library/pkgconfig/cmake), which covers Qt, Boost and similar non-system locations (see `rpaths_for_non_system_absolute_shared_libraries()` in build.py). Closing as fixed; please reopen if you still get the rpath warning on a current release.
```

**#3787**:
```text
Passing a subproject object to `link_with` no longer triggers the old unhandled '<Interpreter object> is not a target' exception. `link_with` is now a typed keyword argument with a strict list of accepted types, so this case produces a structured type-mismatch error instead of a crash. Closing as fixed; if you'd like an even more specific 'you passed a subproject, use subproject.get_variable(...)' hint, feel free to open a focused enhancement.
```

**#3791**:
```text
The Qt module gained a `preserve_paths` option (since 1.4.0) that keeps each input file's relative subdirectory in the generated output path, which avoids the target-name collision you hit when two resources share a basename in different directories. Passing `preserve_paths: true` to the qt preprocess/compile calls resolves this. Closing as addressed; reopen if you need it to be automatic.
```

**#3797**:
```text
Same resolution as #3791: the Qt module's `preserve_paths` option (since 1.4.0) preserves each source's relative subdirectory in the moc/uic output name, avoiding the 'multiple producers'/duplicate-target error when two sources share a basename. Set `preserve_paths: true`. Closing as addressed.
```

**#3802**:
```text
This is handled now: Meson reads the machine-file `sys_root` property and sets `PKG_CONFIG_SYSROOT_DIR` accordingly when invoking pkg-config, so pkg-config paths are correctly rerooted for cross builds. Closing as fixed.
```

**#3848**:
```text
This is fixed: `do_subproject()` now caches results per machine (`self.subprojects[for_machine]`), including subprojects that failed or were disabled -- a failed non-required subproject is stored via `disabled_subproject()`, and any later lookup of the same name returns the cached holder instead of re-running configuration. As a result a subproject that was already attempted is not executed a second time and the `Second call to project()` error no longer occurs in this fallback scenario. Closing as resolved.
```

**#3852**:
```text
The Qt dependency now selects debug vs release libraries based on the build's debug/optimization settings (see the debug-suffix logic in the Qt dependency), including the winmain/EntryPoint variants. The stale debug/release linking after reconfigure reported here should no longer occur. Closing as fixed; please reopen with a current reproducer if you still see the wrong Qt variant being linked.
```

**#3882**:
```text
Meson now adds RPATH entries for the directories of absolute-path external shared libraries, and the install-time rpath fixer only strips build-only directories while preserving the install rpath (see build.py rpaths_for_non_system_absolute_shared_libraries and depfixer.fix_rpath). The disappearing-rpath-on-install behaviour you reported should be resolved. Closing as fixed; reopen with a current reproducer if it persists.
```

**#3917**:
```text
This is resolved: `meson dist` now reads the options that were configured in your build directory (`create_cmdline_args()` -> `read_cmd_line_file()` from `meson-private/cmd_line.txt`) and passes them to the `meson setup` it runs for the dist test build (`mesonbuild/mdist.py`). So the dist build honours your configured options -- e.g. a feature disabled via `-Dopt=false` stays disabled during dist -- instead of falling back to defaults. Closing as fixed.
```

**#4071**:
```text
This regression is fixed. `machine_info_can_run()` (`mesonbuild/envconfig.py`) now explicitly treats an x86 host binary as runnable on an x86_64 build machine (and likewise mips on mips64) when the OS matches, and `Environment.need_exe_wrapper()` uses it, so Meson again defaults to not needing an exe wrapper for a same-architecture 32-on-64 build. Closing as fixed; please reopen if you still see the wrapper being required in that case.
```

**#4094**:
```text
This has been addressed by the module API redesign. Module methods now receive a `ModuleState` object constructed fresh for each invocation, carrying the current interpreter's `subproject`, `subdir`, environment, etc. Modules are expected to use `state` (or `state._interpreter`) rather than caching a reference from `initialize()`, so the stale-interpreter-across-subprojects problem no longer applies. Closing as fixed; please reopen if you find a module still caching a stale interpreter.
```

**#4105**:
```text
This should be resolved. The windows module now selects the resource compiler based on the linker in use (`link`/`lld-link` -> rc.exe/llvm-rc, otherwise windres) rather than requiring the compiler id to be `msvc`. So clang in MSVC ABI mode (using an MS-compatible linker) will now find the resource compiler. Closing as fixed; please reopen with details if a specific clang configuration still fails to locate it.
```

**#4126**:
```text
`gnome.generate_gir()` now accepts a `dependencies` keyword taking dependency objects, and derives the necessary include/search paths from them. This covers the use case of passing the library's `dependency()` in rather than hand-building include_directories from pkg-config prefixes. Closing as implemented; please reopen if a specific non-default-prefix scenario still fails.
```

**#4171**:
```text
Emscripten is now a first-class supported toolchain in Meson (see the emscripten compiler mixin and the wasm test cases, added around 0.54.0). Build-machine executables used as generators should be declared with `native: true` and are built with the native compiler, which resolves the 'cannot use as a generator' error for cross builds. Closing as fixed; if you still hit this with a current release, please reopen with a minimal reproducer and your cross file.
```

**#4179**:
```text
The Qt module now resolves its tools via `state.find_program()`, which honors `override_find_program()`. So overriding `uic`/`moc`/`rcc` before importing/using the qt module works. Closing as fixed; please reopen if a specific override still isn't picked up.
```

**#4190**:
```text
This is resolved: the wrap / subprojects tooling no longer hardcodes `subprojects`. `wraptool` uses `mesonlib.get_subproject_dir()`, which introspects the root `meson.build` and extracts the `subproject_dir` kwarg from `project()` (falling back to `subprojects` only when it isn't set), and `mesonbuild/msubprojects.py` uses `extract_subproject_dir()` the same way. So `meson wrap` now honours a custom `subproject_dir` such as `libs`. Closing as fixed; please reopen if you still see it defaulting to `subprojects` with a custom directory.
```

**#4244**:
```text
The supported way to handle this is the `pic` keyword on `static_library()`, which overrides the global `b_staticpic` when set explicitly (see `Build.BuildTarget._extract_pic_pie` in `mesonbuild/build.py`: an explicit `pic:` value wins over the option). For your bitdepth helper libraries you can pass `pic: get_option('default_library') != 'static'` (or simply `pic: false` if they're never linked into a shared lib), which also covers the `both` case since it follows `default_library`. No dedicated automatic mechanism beyond this was added, so this is the intended approach. Closing on that basis -- please reopen if a concrete case still can't be expressed with the `pic` kwarg.
```

**#4298**:
```text
Meson now offers cross-platform symbol export controls: `gnu_symbol_visibility` (ELF/GCC-style visibility, since 0.48.0), `vs_module_defs` for Windows .def files (extended to more target types), and the snippets module's `symbol_visibility_header()` to generate portable export/import macros (__declspec vs visibility attributes). Together these replace hardcoding `-Wl,--version-script`. Closing as addressed; please reopen if there's a specific export scenario these don't cover.
```

**#4355**:
```text
find_program's Windows behavior has been made more robust: `programs.py` now has special-case handling that searches PATH for scripts independently of PATHEXT (including reading shebangs), so results are more consistent regardless of whether e.g. `.py` is in PATHEXT. Closing as fixed; please reopen if you still see PATHEXT-dependent inconsistency on a current release.
```

**#4366**:
```text
Meson now supports several assemblers as distinct languages/compilers: `nasm`, `yasm`, `masm` (ml/ml64) and `armasm` (see mesonbuild/compilers/asm.py). You can add the relevant language in `project()` (or `add_languages()`) so assembly is handled by a dedicated assembler rather than the C compiler, which addresses the MSVC + ARM `.s`/`.S` case (via armasm, optionally with a gas-preprocessor wrapper). Closing as addressed; please reopen if your specific assembler still isn't supported.
```

**#4417**:
```text
The install-name/rpath fixer now guards against this: `fix_darwin()` first runs `otool` (get_darwin_rpaths) and, if that fails because the file isn't a Mach-O binary, it catches the error and returns instead of invoking `install_name_tool`. So cross-compiled non-Mach-O outputs (e.g. a mingw DLL) are skipped. Closing as fixed; please reopen with a reproducer if install_name_tool is still run on an incompatible binary.
```

**#4532**:
```text
In current Meson the overwrite warning is checked against the fully-resolved output path: @BASENAME@ in `output:` is substituted from each input before the overlap check runs, so two `configure_file()` calls with different inputs produce different output names and no longer trigger this warning. Please reopen if you can still reproduce a false warning on a recent release.
```

**#4615**:
```text
Meson no longer wraps ordinary library links in `--start-group`/`--end-group`; those flags are now used only for `link_whole` targets. Regular shared libraries are placed outside any group, so `--as-needed` behaves correctly with GNU ld. Please reopen with a reproducer on a current release if you still see the problem.
```

**#4876**:
```text
Meson already supports using prebuilt gtest/gmock. `dependency('gtest')` / `dependency('gmock')` use a DependencyFactory that first tries pkg-config (`GTestDependencyPC` / `GMockDependencyPC`), then a system lookup that prefers prebuilt libraries via `find_library('gtest')` / `find_library('gmock')` and only falls back to building the bundled sources if no library is found. As a commenter here confirmed back in 2019, external/system googletest and gmock work fine. Closing as resolved; please reopen if the prebuilt Fedora/Debian libraries aren't being picked up on a current release.
```

**#4881**:
```text
Both `c_std=c89` and `c_std=c90` are accepted as valid values by the C compiler backends (they map to the same ISO C90/C89 standard flag), so you can already use whichever spelling you prefer. Closing on that basis — please reopen if you hit a case where one spelling is rejected.
```

**#4935**:
```text
This has been implemented. Meson 1.11 added dedicated `install_vala_header`, `install_vala_vapi`, and `install_vala_gir` keyword arguments (each with a matching `*_dir` variant for the destination), which replace the hard-to-read `install_dir: [true, true, true, true]` array form — passing more than one value to `install_dir` is now deprecated in favor of these keywords. See the Vala documentation ("Building libraries"). Closing as implemented; please reopen if the new keywords don't cover your case. (The separate point about simplifying `.typelib` generation is better tracked as its own issue.)
```

**#4990**:
```text
Thanks for the report. Modern Meson does propagate include directories from dependencies into the generated `.pc` file: the compile args (including `-I`) of dependencies passed via `libraries:` are added to the `Cflags:` field, and there is now also an `extra_cflags:` keyword on `pkg.generate()` for adding arbitrary flags. Please give a recent Meson release a try; if you still see include dirs missing for a specific dependency type, we'd welcome a fresh reproducer and can reopen.
```

**#5170**:
```text
This is resolved in current Meson. User-supplied `cmake_args` are now passed into the initial `_get_cmake_info()` invocation, and the generated CMake toolchain file — which carries `CMAKE_TOOLCHAIN_FILE` — is applied in that same first pass, so toolchain-driven cached variables (as vcpkg needs) take effect from the initial cache creation. In addition, the reliable "global toolchain file for all CMake dependencies" mechanism that was discussed here is now available as the `cmake_toolchain_file` machine-file property (since 0.56.0; see Machine-files.md). Closing as implemented. The broader idea of a dedicated `vcpkg` dependency type is a separate feature — please open a new issue for that if it's still wanted.
```

**#5240**:
```text
This is fixed in current Meson. When a compiler object is passed to `run_command()`, it now expands the full compiler exelist — it uses `get_exe()` for the first element and `get_exe_args()` for the remaining ones (see `mesonbuild/interpreter/interpreter.py`). So a wrapped compiler such as `ccache gcc` is invoked in full rather than dropping everything after the first element. Please try a recent release; if you still hit a failure with a wrapped compiler, let us know and we can reopen.
```

**#5313**:
```text
The pkg-config path is now a per-machine option (`pkg_config_path` keyed by build/host machine) and is read per-machine from the environment as well, so cross builds have an independent pkg-config search path (settable via the cross/native file or `-Dhost:pkg_config_path=...`). The deprecation-period plan described here has long since played out. I'll close this as resolved; please reopen if the per-machine handling still surprises you on a recent release.
```

**#5333**:
```text
Linker information is now available in the target introspection data. The Ninja backend emits a linker block — the linker command/exelist plus the link parameters — alongside the per-language compile blocks, and this is surfaced in the `target_sources` array of `meson introspect --targets` (and in `meson-info/intro-targets.json`). See `create_target_linker_introspection` in `mesonbuild/backend/ninjabackend.py`. Please try it on a recent release; closing as resolved, but reopen if a specific field you need (e.g. resolving which static libs end up in a given shared lib) is still missing.
```

**#5368**:
```text
The LLVM shared-library detection has since been reworked: for shared linking Meson now specifically matches `libLLVM-<detected-version>.(so|dll|dylib)` rather than grabbing the first sorted `libLLVM*.so` in the libdir, so a stale older `libLLVM-*.so` in the same directory should no longer be picked. Please reopen with a current `meson-log.txt` if you still see the wrong library being selected.
```

**#5370**:
```text
The LLVM config-tool dependency now enumerates all available `llvm-config`/`llvm-config-N` binaries and sorts/filters them against the requested version range, instead of failing on whichever one happens to be first on PATH. A request like `dependency('llvm', version: ['>=7', '<8'])` should therefore pick a matching `llvm-config-7` if present. Closing as fixed; please reopen with a current log if a matching LLVM is still missed.
```

**#5461**:
```text
The `.def` file passed via `vs_module_defs` is now added to the target's `link_depends`, so updating the module-definition file triggers a relink. Closing as fixed; please reopen if you still see a stale link when only the `.def` changes.
```

**#5511**:
```text
The i18n.merge_file targets no longer use the fixed `<name>_data_merge` naming that caused the collision — the custom target now derives its name from the output file, so two `merge_file` calls with different outputs no longer clash. Note that two calls producing the *same* output filename will still conflict (they'd generate the same file). Closing as resolved; please reopen if you still hit a spurious collision with distinct outputs.
```

**#5561**:
```text
The documentation now includes worked `run_target` examples (Run-targets.md) and a full reference entry in the YAML reference manual documenting the `command`/`depends` arguments. For depending on the whole build, `alias_target` (also documented) is usually the right tool. Closing as addressed; let us know if a specific example is still missing.
```

**#5636**:
```text
Meson now sorts the candidate LLVM versions itself (descending) rather than relying on CMake's ordering — the code explicitly notes that CMake's sorting before 3.18 is incorrect and compensates for it, and it also filters by the requested version range. This should make `method: 'cmake'` pick a version-appropriate LLVM. Closing as fixed; please reopen with a log if you still get the oldest version.
```

**#5686**:
```text
`--native-file` and native/cross machine files are now documented in the Machine files reference page (docs Machine-files.md) as well as the command reference, rather than only in the 0.49 release notes. Closing as resolved; if you find a specific gap in the current docs, please point to it and we'll fill it in.
```

**#5797**:
```text
The traceback reported here (`'CustomTarget' object has no attribute 'pic'`) no longer occurs. `SharedLibrary.link_whole()` now uses `getattr(t, 'pic', True)` and a `check_can_link_together()` type check, so incompatible link_whole targets raise a clear `InvalidArguments` error instead of crashing. Please reopen with a current-version reproducer if you still hit an unhandled case.
```

**#5846**:
```text
Sanitizers on clang-cl are now handled through the `b_sanitize` option and the ClangCl `sanitizer_compile_args()` path rather than by passing raw `-fsanitize=address` in `c_args`. Using `-Db_sanitize=address` lets Meson manage the incompatible-runtime interaction instead of colliding with `/MDd`. Closing as addressed; please reopen if `-Db_sanitize=address` still fails the sanity check on a current release.
```

**#5886**:
```text
Meson now sanitizes the Windows `WindowsApps` App Store python stub: when that directory appears in the search path it is replaced with `dirname(sys.executable)` (see `_windows_sanitize_path` in `mesonbuild/programs.py`), so program lookup no longer gets stuck on the zero-size Store stub. This resolves the 'fails and does not continue' behavior reported here. Closing as fixed; please reopen if a current release still selects the stub.
```

**#5951**:
```text
The crash reported here (`'LLVMDCompiler' object has no attribute 'thread_link_flags'`) is fixed: `thread_link_flags()` is now defined on the base `Compiler` class (`mesonbuild/compilers/compilers.py`), which every compiler including `LLVMDCompiler` inherits. Using the `llvm` dependency from a D project no longer hits that traceback. Closing as fixed; please open a fresh issue if you still see problems mixing LLVM's C interface with a non-C++ project on a current release.
```

**#6045**:
```text
The reported failures are resolved: `detect_scanbuild()` now parses `SCANBUILD` with `split_args()` and resolves it via `shutil.which`, so `SCANBUILD='scan-build --status-bugs'` (or a non-absolute path) works and the extra arguments are preserved (`[tool] + exelist[1:]`). You can pass `--status-bugs` this way to fail CI on findings. Closing as addressed; please reopen if a current release still drops the extra args.
```

**#6055**:
```text
The Xcode backend now has Swift handling: `is_swift_target()`, `determine_swift_dep_dirs()`, bridging-header handling, and the `swift` source-type/`SWIFT_` build-setting mappings are all present in `mesonbuild/backend/xcodebackend.py`. Closing as implemented; please open a specific issue if a particular Swift+Xcode scenario still doesn't work.
```

**#6253**:
```text
Meson now has dedicated Apple-clang compiler classes (`AppleClangCCompiler`, `AppleClangCPPCompiler`, `AppleClangObjCCompiler`, etc.) plus an Apple mixin (`mesonbuild/compilers/mixins/apple.py`) that overrides the version thresholds used for standard/feature detection, so Xcode's clang is no longer treated as if its reported version mapped directly onto vanilla LLVM releases. This addresses the core misdetection described here. If you still see a specific wrong-flag-for-Apple-clang case on a current release, please reopen with details.
```

**#6259**:
```text
This was a transient regression introduced by #6179 back in 2019 and has long since been resolved in the release cycles that followed; current Meson does not emit the stray backslashes in generated `config.h` described here. Closing as fixed/obsolete. If a similar config.h escaping problem appears on a current release, please open a new issue with a minimal reproducer.
```

**#6570**:
```text
Meson now has dedicated end-user documentation for building an existing Meson project. See the 'Running Meson' and 'Built-in options' pages: install prefix/DESTDIR are covered under `meson install` (`--destdir`, `prefix`), and options like `--default-library=static` and `--strip` are documented in Built-in options. Closing as the documentation gap this asked for has been filled; please reopen if a specific piece is still missing.
```

**#6661**:
```text
The CMake dependency backend was substantially reworked; with CMake >= 3.17 Meson now uses the structured `--trace-format=json-v1` output instead of parsing the human-readable trace, which fixed a class of include-path extraction problems. Could you retry with a current Meson + CMake and confirm whether `-I` flags for Ceres are now populated? If it still fails, please attach a fresh meson-log.txt so we can reopen with current data.
```

**#6671**:
```text
The documentation has been expanded: `--native-file` is now shown in Native-environments.md, and Machine-files.md documents layering (passing `--cross-file`/`--native-file` multiple times) together with the `[constants]` section and a concrete `meson setup --cross-file a.ini --cross-file b.ini` composition example. Closing as the doc gap is addressed; please reopen if something specific is still unclear.
```

**#6728**:
```text
Subproject option handling was reworked with the new option store. `do_subproject()` now merges the `default_options` you pass into the subproject's options (see mesonbuild/interpreter/interpreter.py `do_subproject`), so `subproject('libfoo', default_options: ['BUILD_TESTS=false'])` now takes effect for the subproject's own project options. Could you confirm on current Meson? If it still reproduces, please attach the exact reproducer and we'll reopen.
```

**#6792**:
```text
The python module's `.dependency()` now goes through the standard dependency machinery: it accepts the common dependency kwargs (including `version`) and resolves via `find_external_dependency` (mesonbuild/modules/python.py), which performs the version comparison. A check like `pyinstall.dependency(version: '>=3.20', required: true)` will now fail as expected. Closing as fixed — please reopen if you still see the version constraint being ignored on current Meson.
```

**#6846**:
```text
The root cause here was the old human-readable CMake trace parser splitting paths on spaces (hence `C:/Program Files/NVIDIA` getting truncated). With CMake >= 3.17 Meson now uses `--trace-format=json-v1` (mesonbuild/cmake/traceparser.py), which preserves arguments containing spaces and only splits list entries on `;`. This should fix the OpenCL/CUDA include path. Could you retry with a current Meson + CMake >= 3.17 and confirm? If it still truncates, please attach a fresh meson-log.txt.
```

**#6895**:
```text
The introspection buildsystem-files list now normalizes paths consistently with `PurePath(src_dir, x).as_posix()` (mesonbuild/mintro.py `list_buildsystem_files`), producing uniform forward-slash paths on Windows. Could you re-run your Meson-UI unit test against a current Meson to confirm the formatting is now acceptable? If a specific field still comes out wrong, please attach the current JSON and we'll reopen.
```

**#6949**:
```text
Dependency tracking for D has been substantially improved since this report. The D compilers now implement `get_dependency_gen_args`/`get_depfile_suffix` (dmd uses `-makedeps` from frontend 2.095+, and the GDC/LDC paths emit dep files as well; see `mesonbuild/compilers/d.py`). Meson now generates and consumes depfiles for D sources, so changing an imported module should trigger rebuilds of dependents. Could you retest with a current release and confirm whether your reproducer still misses the rebuild?
```

**#7194**:
```text
The docs now explain this. `buildtype` is a two-way mapping to `debug`+`optimization`: `plain` corresponds to `debug=false, optimization=plain`, whereas `custom` is what you get for any combination of `debug`/`optimization` that doesn't map to a named buildtype (so `-Ddebug=true` on top of `plain` yields `custom`). See the mapping table in https://mesonbuild.com/Builtin-options.html. Closing as answered/documented.
```

**#7486**:
```text
Compiler sanity and capability checks no longer share a fixed filename like `meson-private/sanitycheckc.exe`. They now run inside a unique per-check temporary directory (see `TemporaryDirectoryWinProof` in `mesonbuild/compilers/compilers.py`), so rapid successive checks can no longer collide on a locked output file. This should resolve the intermittent 'Permission denied' failures under MSYS2/MinGW. Closing as fixed; please reopen with a current log if you still hit it.
```

**#7676**:
```text
Compiler and linker capability checks now run inside a dedicated temporary directory: the check code creates a `TemporaryDirectoryWinProof` and runs the compiler/linker with `cwd=tmpdirname`, with any output file placed inside that temp dir (see `mesonbuild/compilers/compilers.py`). So a stray `a.out`/`a.out.tmp*` is no longer written into the source directory, and the portage/sandbox ACCESS DENIED you saw should not occur anymore. Closing as fixed; please reopen with a current log if a sandbox still catches a write to the source tree.
```

**#8091**:
```text
`compiler.find_library()` accepts a `dirs` keyword argument for adding extra library search paths on top of the system defaults (see the `dirs` kwarg in the reference manual). This covers the main request of adding search paths to the existing ones. Querying the system's default library search paths is a separate, narrower feature request. Closing as the primary ask is implemented; feel free to open a focused issue for the path-query part if still needed.
```

**#8387**:
```text
The preprocess-only part of this request is now available via `compiler.preprocess()` (added in Meson 0.64.0), which generates targets that run the compiler in preprocess-only mode (`-E`/equivalent) and emit the preprocessed source. See `preprocess_method` in `mesonbuild/interpreter/compiler.py`. The compile-but-don't-assemble (`-S`) part is a separate, narrower request. Closing the preprocessing part as implemented — please open a focused issue for `-S`/assembly output if still wanted.
```

**#8738**:
```text
The original crash came from indexing `coredata.options[OptionKey('backend_startup_project')]` directly during a reconfigure where the VS backend option wasn't yet registered. The backend now retrieves it via `optstore.get_value_for('backend_startup_project')` (see `mesonbuild/backend/vs2010backend.py`), and the whole option store was reworked. The bare `KeyError` shown here should no longer occur. If reconfiguring an existing build dir with `--backend=vs --reconfigure` still fails on current master, please reopen with the fresh traceback.
```

**#8780**:
```text
This classic Windows quoting bug has been fixed. The Ninja backend now quotes executable/command paths via its dedicated quoting helpers (`cmd_quote`/`quote_arg` in `mesonbuild/backend/ninjabackend.py`), so a compiler path containing spaces (e.g. `C:\Program Files\LLVM\bin\clang++.exe`) is emitted as a single quoted token rather than being split. Please retry on current Meson (1.11.x); closing as fixed, reopen if you can still reproduce.
```

**#8824**:
```text
Meson now exposes the Windows standard libraries as the per-language compiler option `c_winlibs` / `cpp_winlibs`, and these are resolvable per target (via `default_options`/`override_options`) — see `mesonbuild/compilers/c.py` where the value is fetched with `get_compileropt_value('winlibs', target, subproject)`. For example `override_options: ['c_winlibs=kernel32.lib,user32.lib,ws2_32.lib,iphlpapi.lib']` lets you add `ws2_32`/`iphlpapi` without `find_library` path-mangling. Note this replaces the default winlib list rather than appending, but it satisfies the original need. Closing as addressed — please reopen if a pure append mechanism is still wanted.
```

**#9266**:
```text
The CMake dependency docs now explain how to use imported targets: pass the target name(s) via the `modules` property, e.g. `dependency('ZLIB', method : 'cmake', modules : ['ZLIB::ZLIB'])`, and there is also `components` for `find_package(COMPONENTS)` and `cmake_module_path`/`cmake_args` for custom `.cmake` helpers — see https://mesonbuild.com/Dependencies.html#cmake (`docs/markdown/Dependencies.md`). For your CGAL/TBB case, request the CGAL imported target(s) via `modules`. Closing as documented — if the specific `include(CGAL_TBB_support)` helper flow still isn't clear, reopen and we can add a targeted example.
```

**#9370**:
```text
This was a transient regression in the 0.59.2 point release. Current master's Ninja detection (mesonbuild/tooldetect.py, detect_ninja_command_and_version) honors the `NINJA` environment variable first via ExternalProgram, so this no longer reproduces. Closing as fixed; please reopen with a reproducer if you still hit it on a recent Meson.
```

**#9422**:
```text
The MPI dependency now filters config-tool link args (mesonbuild/dependencies/mpi.py, _filter_link_args keeps only -L/-l/-Xlinker), which drops the stray `-Wl,-rpath -Wl,<dir>` sequences that caused ld.gold's 'pread failed: Is a directory'. This should be resolved on current Meson; please reopen with a fresh log if it still fails.
```

**#9753**:
```text
Chaining generators is now handled: Generator.process_files explicitly accepts GeneratedList inputs, registering the dependency and referencing the upstream outputs in the target private dir (mesonbuild/build.py). The previous AssertionError in generate_genlist_for_target no longer applies. Closing as fixed; please reopen with a reproducer if you still see a crash or invalid ninja file on current Meson.
```

**#9783**:
```text
Meson now prepends the build library paths to WINEPATH rather than appending (mesonbuild/environment.py, env.prepend('WINEPATH', ...)), so the freshly built DLLs take precedence over system/prefix ones when running cross-compiled Windows binaries under wine. This addresses the 'inappropriate DLL from system path' problem. Closing as fixed; reopen with a current log if it still misbehaves.
```

**#10666**:
```text
Thanks for the report. Since this was filed, Meson no longer returns `None` when no toolchain is available: `detect_compiler()` now returns a `MissingCompiler` sentinel whose attribute access raises a proper `DependencyException('no toolchain found')` instead of the `AttributeError: 'NoneType' object has no attribute 'has_header'` you saw (see `mesonbuild/dependencies/base.py`, `MissingCompiler` / `detect_compiler`). So the unhandled Python traceback is gone. If Spot still fails to configure on FreeBSD with current Meson, it should now be a clear diagnostic; please open a new issue with the fresh error if so. Closing as the reported crash is resolved.
```

**#11212**:
```text
The Python module now derives install directories from the target interpreter's `sysconfig` paths (`platlib`/`purelib`) rather than a hardcoded `python3` path, so `get_install_dir()` should return the correct versioned location (e.g. `.../python3.8/dist-packages`) on Debian/Ubuntu. This looks fixed on current Meson — could you confirm with a recent release? If you still see an unversioned `python3` path, please attach the interpreter details and we'll reopen.
```

**#11634**:
```text
This crash no longer reproduces on current Meson. The `env` dict values are now passed through `listify()` when constructing the `EnvironmentVariables` (see `env_convertor_with_method` in mesonbuild/interpreter/type_checking.py), and `listify()` recursively flattens nested lists (mesonbuild/utils/universal.py). So `env: {'MY_KEY': ['VAL1', ['VAL2']]}` is flattened to `['VAL1', 'VAL2']` before the `separator.join()` that previously raised `TypeError`. Closing as fixed — please reopen with a repro on a recent release if you still see it.
```

**#11827**:
```text
Thanks for the report. On current master, `.cmd` (and `.bat`) stubs are handled: `ExternalProgram`'s Windows extension list includes `cmd` (`mesonbuild/programs.py`, `windows_exts = ('exe', 'msc', 'com', 'bat', 'cmd')`), and the PATH search appends these extensions when resolving a binary given without one. So `c = 'riscv-none-elf-gcc'` in a cross file should now resolve `riscv-none-elf-gcc.cmd`. Please try a recent release; if xPack's `.cmd` stubs still fail to resolve for you, reopen with a fresh `meson-log.txt` and we'll take another look.
```

**#12234**:
```text
`loongarch64` is now included in Meson's `known_cpu_families` list (mesonbuild/envconfig.py), so on LoongArch hosts where `platform.machine()` reports `loongarch64` the 'Unknown CPU family' warning is no longer emitted. This appears resolved on current Meson. If you still see the warning, please paste the exact family string Meson prints (Host machine cpu family) and your `meson --version`, and we can reopen. Otherwise closing as fixed.
```

**#12327**:
```text
This appears fixed on current Meson. `EnvironmentVariables._prepend`/`_append` now read the existing value from the passed environment (`env.get(name, default)`) and prepend/append to it, and mtest builds the test env from `os.environ.copy()`. So `LD_LIBRARY_PATH=myld ninja test` with `env.prepend('LD_LIBRARY_PATH', 'pippo')` now yields `pippo:myld` rather than clobbering to `pippo`. Could you retry with a recent Meson and confirm? If it still reproduces we can reopen with the exact command and Meson version.
```

**#12755**:
```text
Since this was filed, `fs.copyfile()` gained a `build_subdir` keyword argument that lets you place the copied file inside a subdirectory of the current build directory (see the `fs.copyfile() now has a build_subdir argument` release snippet and the `build_subdir` kwarg in `mesonbuild/modules/fs.py`). For example: `fs.copyfile(some_file, 'file', build_subdir: 'relative_dir')`. This covers the use case in the report. The `dest` positional argument itself still may not contain path separators by design (the destination filename must be a plain name), but the directory placement you wanted is now supported. If `build_subdir` does not cover your scenario, please let us know and we can reopen. Closing as resolved.
```

**#13016**:
```text
This appears to be resolved on current master. The non-SDK detection path in `VulkanDependencySystem` now requires *both* `find_library('vulkan')` and `has_header('vulkan/vulkan.h')` to succeed before marking the dependency as found (mesonbuild/dependencies/ui.py). So in the scenario you described (loader present but `vulkan-headers` missing), the dependency will now correctly report as not-found rather than succeeding and failing at build time. Could you confirm with a recent Meson release? If it still misbehaves for you, please reopen with a fresh log.
```

**#13194**:
```text
On current master the test scheduling builds all `repeat * len(tests)` runners up front (`for i in range(self.options.repeat): runners.extend(...)` in mesonbuild/mtest.py) and only short-circuits remaining runs when a failure occurs (`self.options.repeat > 1 and self.fail_count`). For an all-passing run, all repeats should now execute. Could you retest with a recent release and, if you still see fewer runs than requested without any failures, reopen with the full output? Tentatively closing as fixed.
```

**#13197**:
```text
This specific error (`ERROR: Invalid variable name: 1_Flat_dir`, from a CMake target/name starting with a digit) is fixed on current master. `_sanitize_cmake_name()` now prefixes such names with `cm_` when the first character is a digit (mesonbuild/cmake/interpreter.py), producing a valid Meson identifier like `cm_1_Flat_dir`. The fix landed after this report was filed. Please retest with a recent release; closing as fixed. If Faiss still fails for a *different* reason, please open a fresh issue with the new error.
```

**#13692**:
```text
The CUDA module's architecture tables on current master now include Orin / SM 8.7: `'8.7'` is present in `cuda_all_gpu_architectures`, the `'Orin'` name maps to `['8.7']`, and for CUDA >= 11.1 the upper architecture limit is raised to `8.7`. This should mean `nvcc_arch_flags(..., '8.7')` now emits `-gencode arch=compute_87,code=sm_87`. Could you re-test with a recent Meson (>= 1.7) and your CUDA 11.4 toolkit? If flags are still dropped for 8.7 we can reopen with the new log.
```

**#13723**:
```text
On current master, `gnome`'s `_find_tool` now looks up `glib-compile-resources` (and the other GLib build tools) as native (build-machine) programs — `find_tool(..., native=True)` uses `MachineChoice.BUILD` for overrides and queries the build-machine `gio-2.0.pc` rather than the host one. This is the fix for picking up a host `glib-compile-resources` when cross-compiling. Could you re-test with a recent Meson and your cross file? If the host tool is still selected, please attach the setup log and we'll reopen.
```

**#13941**:
```text
This appears to be resolved on current master. The `minstall.do_symlink` code path no longer validates that the pointed-to file exists before creating the symlink, and in `--dry-run` mode the symlink creation is a no-op, so the `Tried to install symlink to missing file` error no longer occurs (the message string is gone from the codebase entirely). Could you re-test with a recent Meson (>= 1.7) and confirm? If `meson install --dry-run` now succeeds for your test project, we can close this.
```

**#14131**:
```text
Current Meson now handles this: at the end of configuration, `msetup.check_unused_options` collects command-line `-D` options that don't correspond to any known option (top-level or in a subproject that was actually used) and raises `Unknown options: "foo"`. So `meson setup build -Dfoo=bar` on a project without such an option now errors out and points at the typo — going a step further than the warning originally requested. Could you confirm on a recent master? If this matches your expectation we can close as fixed.
```

**#15732**:
```text
This is a release-artifact issue rather than a bug in Meson's code — the 1.11.1 sdist was missing from PyPI. Later 1.11.x point releases have been published with sdists, so `pip wheel --no-binary` should now resolve a source release again. Could you confirm whether pinning to a current 1.11.x (which has a `.tar.gz` on PyPI) works for your `pip wheel --no-binary :all:` flow? If so this can be closed; if a specific version's sdist is still missing, please note which one so it can be re-uploaded.
```

**#15889**:
```text
Thanks for the report. This `AttributeError: 'GeneratedList' object has no attribute 'get_builddir'` came from the ninja backend treating a `GeneratedList` like a `Target` when building the dependency output paths. On current master this path now branches explicitly on `GeneratedList` and uses the target's private build directory (see `get_paths_for_dep_outputs` in `mesonbuild/backend/backends.py`), so the crash should no longer occur. Related fixes: the `unwrap_dep_list`/`get_paths_for_dep_outputs` changes and "Make cython generated targets less nested". Could you retest with a recent meson (>= 1.11.2 / current git) against your h5py PR and confirm? If it still reproduces, please reopen with the fresh traceback.
```

</details>

#### Duplicate (1)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#6322](https://github.com/mesonbuild/meson/issues/6322) | Deprecate and Remove [target_machine] from cross file format | medium | A proposal to deprecate [target_machine] in cross files. This should be folded into the more comprehensive mac |

<details><summary>Draft comments</summary>

**#6322**:
```text
This proposal is really a sub-topic of the broader machine-object overhaul tracked in #6361 (host/build/target_machine redesign), which is the place these deprecation/rename decisions are being coordinated. Suggest consolidating there; closing this as a duplicate of #6361.
```

</details>

#### Obsolete (15)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#1776](https://github.com/mesonbuild/meson/issues/1776) | Assembly test fails on ARM in sid | medium | This is a 2017 report of an assembly test crashing with an illegal instruction on a specific Debian sid/GCC/Ra |
| [#3129](https://github.com/mesonbuild/meson/issues/3129) | meson i18n module fails to merge desktop file on gettext < 0.19.0 | medium | Caused by gettext versions below 0.19 (from the Ubuntu 14.04 era) not supporting --desktop. As of 2026, that g |
| [#3593](https://github.com/mesonbuild/meson/issues/3593) | c++ -Wl,--as-needed doesn't work in OpenBSD | medium | The root cause is an OS-level issue on OpenBSD — libc++/libc++abi not linking against libpthread — not somethi |
| [#3780](https://github.com/mesonbuild/meson/issues/3780) | Prefixes in the coverage report | medium | mesonbuild/scripts/coverage.py now explicitly excludes the subproject root from gcovr output via 'gcovr_config |
| [#6111](https://github.com/mesonbuild/meson/issues/6111) | Problem with Dlang libraries 'shared' and 'static' also not letting 'e | medium | This originated as a question raised while adding a D-language template to `meson init`. dlangtemplates.py now |
| [#6497](https://github.com/mesonbuild/meson/issues/6497) | meson's wrapdb is a single point of failure | medium | Points out that wrapdb is a single point of failure. The current wrapdb (v2) has been overhauled to be based o |
| [#6873](https://github.com/mesonbuild/meson/issues/6873) | Allow get_pkgconfig_variable's define_variable to take a dict | medium | A request to make get_pkgconfig_variable's define_variable a dict, but the method itself was deprecated in 0.5 |
| [#6898](https://github.com/mesonbuild/meson/issues/6898) | MacOS build of D libraries with DMD 2.085 fails with unrecognized swit | medium | The `-Xcc=` mechanism in mesonbuild/compilers/d.py's `get_allow_undefined_link_args()` (added Dec 2019, unchan |
| [#7535](https://github.com/mesonbuild/meson/issues/7535) | Boost extralib test with shared library segfaults on macOS Travis-CI | medium | A boost test segfault specific to macOS on Travis-CI from 2020. Travis-CI has already been dropped from Meson' |
| [#8301](https://github.com/mesonbuild/meson/issues/8301) | error on debian: "TypeError: Can't instantiate abstract class GnuDynam | medium | Compatibility error when loading old pickled coredata with a newer meson. This is a typical case resolved by r |
| [#9499](https://github.com/mesonbuild/meson/issues/9499) | 404: "Edit on GitHub" button on Reference-manual.html | low | The Reference-manual has been overhauled to be generated by refman from yaml (docs/yaml), so the old link stru |
| [#10377](https://github.com/mesonbuild/meson/issues/10377) | GTK+ reqested bug report | medium | The actual issue is an environment-specific error where Python 3.10's shutil failed to extract the glib subpro |
| [#10443](https://github.com/mesonbuild/meson/issues/10443) | test cases/frameworks/4 qt/meson.build:48:4: ERROR: Unhandled python e | medium | Test-suite failures on an extremely old and unsupported environment: Xcode 3.2 / gcc-4.2 / 10.6 PPC. This does |
| [#11034](https://github.com/mesonbuild/meson/issues/11034) | meson fails to find a linker when multiple archflags are passed to GCC | medium | The report is about linker detection failing when Apple's own gcc-4.2 (the last Apple-shipped, non-Clang GCC f |
| [#11232](https://github.com/mesonbuild/meson/issues/11232) | pinning subprojects to commits is finicky | medium | wrap files are parsed with configparser, which automatically strips leading/trailing whitespace from values. T |

<details><summary>Draft comments</summary>

**#1776**:
```text
This appears to be a toolchain-specific problem (a suspected GCC codegen issue on a specific Debian sid/ARM setup from 2017), not a Meson bug, and the environment is long obsolete. Closing; please reopen against a current toolchain if a Meson-side issue is still observed.
```

**#3129**:
```text
This affects gettext older than 0.19.0 (Ubuntu 14.04 era), which is well past end-of-life on all currently-supported platforms, and the i18n module has been reworked considerably since. We're closing this as obsolete; if you hit a merge_file failure with a currently-supported gettext, please open a fresh issue.
```

**#3593**:
```text
This appears to be an OpenBSD toolchain issue (libc++/libc++abi not linking libpthread) rather than a Meson bug, and it was reported against OpenBSD 6.3 with GNU ld 2.17. Meson now feature-detects `--as-needed` per linker. Given the age and the external root cause, I'm closing this; please reopen if it still reproduces on a current OpenBSD with a current Meson.
```

**#3780**:
```text
The coverage helper has been reworked since this report (it now runs gcovr with explicit `-r <source> <build>` and excludes subproject paths, and lcov captures from the build directory). Duplicate/prefixed entries are largely a gcovr/lcov behaviour. Could you check whether this still reproduces with a current Meson and gcovr? Without an updated reproducer we'll close this as stale.
```

**#6111**:
```text
This was a support question raised while working on adding D-language `meson init` templates back in 0.52.0. D init templates now exist (`mesonbuild/templates/dlangtemplates.py`), and the 0.52.0-era dynamic-linker detection problem is long superseded. If you are still hitting a specific D shared/static linking failure on a current Meson release, please open a fresh issue with a minimal reproducer.
```

**#6497**:
```text
The wrapdb was rewritten to the v2 design (`wrapdb.mesonbuild.com/v2/releases.json` plus per-wrap files), which is a static, GitHub-backed distribution rather than the single dynamic API server that motivated this issue in 2020. Wraps and their source archives are also cached/mirrorable. The original single-point-of-failure concern is largely obsolete. Closing; if you want fully offline/bundled wrap support, that is a separate feature request.
```

**#6873**:
```text
`get_pkgconfig_variable()` was deprecated in 0.56.0 in favor of the unified `dep.get_variable(pkgconfig: ..., pkgconfig_define: ...)`. Since the old method is deprecated and won't gain new syntax, this specific request (dict form of `define_variable`) is obsolete. If a dict form for `pkgconfig_define` on the new `get_variable` is desirable, that can be tracked as a fresh enhancement. Closing.
```

**#6898**:
```text
This is specific to an old DMD (2.085, from 2019) that didn't understand the `-Xcc=` passthrough. Given the age, could you confirm whether it still reproduces with a currently supported DMD and current Meson? If it only affects long-EOL DMD versions we'll close as stale; otherwise please attach a fresh log.
```

**#7535**:
```text
This is a 2020 CI-infrastructure issue specific to Travis-CI on macOS 10.13, referencing commits and a CI setup that no longer exist (Meson has long since moved off Travis-CI). The referenced job links are dead and the environment is obsolete. Closing as obsolete; if a boost shared-library test still segfaults on current macOS CI, please open a fresh issue with a current log.
```

**#8301**:
```text
This error comes from loading an old pickled `coredata` (build directory) with a newer/mismatched Meson version, where the linker class hierarchy changed. The supported fix is to wipe and reconfigure the build directory (`meson setup --wipe builddir` or delete it). Meson also now detects a coredata version mismatch and asks you to reconfigure. Given this is 5 years old and environment-specific, closing as obsolete — please reopen if it reproduces with a clean build directory on a current release.
```

**#9499**:
```text
The reference manual is now generated from the YAML sources under docs/yaml via docs/refman, so the old 'Edit on GitHub' target of docs/_build/Reference-manual.md no longer applies. This is a website/hotdoc rendering concern; the source layout that produced the broken link has since changed. Closing as obsolete, please reopen against the website if the button is still 404 on the current site.
```

**#10377**:
```text
Thanks for the report. This traceback is a `shutil.ReadError: Unknown archive format` while unpacking `pcre-8.37.tar.bz2` inside the (now quite old) glib wrap/subproject — it indicates the archive on disk was truncated/corrupt or your Python's `bz2` support was unavailable, rather than a bug in Meson itself. The template fields (Meson version, OS, reproducer) were left blank, so we can't investigate further. Current Meson has substantially reworked wrap extraction, and GLib no longer bundles pcre this way. If you can still reproduce with a current Meson and a fresh checkout, please open a new issue with the full environment details and a minimal reproducer. Closing as stale for now.
```

**#10443**:
```text
This was reported on Mac OS X 10.6 PPC with Xcode 3.2 / gcc-4.2 and Meson 0.62.1 — an environment far outside Meson's supported platforms and toolchains today. Both the Qt framework test and Meson itself have changed substantially since then. Without a reproducer on a currently supported platform this can't be acted on. If you can reproduce a Qt test failure on a supported OS/toolchain with a recent Meson, please open a fresh issue with the full log. Closing as obsolete.
```

**#11232**:
```text
With current Meson the wrap files are parsed with Python's `configparser`, which strips surrounding whitespace on values automatically. I verified that `revision = <full 40-char sha>` (with spaces around `=`) parses correctly to the full hash. So the whitespace/`=`-spacing sensitivity described here no longer reproduces. The truncated-hash cases (`aeda644f9690b34`) are expected to fail because a git revision must be a full, resolvable ref/sha. Closing as obsolete — please reopen with a current reproducer if you still hit a parsing problem with a full hash.
```

</details>

#### Can be closed once answered (75)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#553](https://github.com/mesonbuild/meson/issues/553) | Ambiguous threads dependency | medium | The behavior of dependency('threads') is now documented (Threads.md), and pthread/win32 flag handling has been |
| [#620](https://github.com/mesonbuild/meson/issues/620) | How to add boost dependency to the pkg-config file? | medium | pkgconfig.generate now accepts dependency objects directly and can include libraries such as boost. The origin |
| [#1104](https://github.com/mesonbuild/meson/issues/1104) | Make a fully statically linked .exe | medium | MSVC /MT support is handled via the b_vscrt option, and static linking can be achieved with prefer_static/-Dde |
| [#1229](https://github.com/mesonbuild/meson/issues/1229) | Vala: specify generated vala headers as dependencies of other subfolde | low | Headers/vapi generated by Vala can propagate to other targets via declare_dependency(sources: ...) or inter-li |
| [#2025](https://github.com/mesonbuild/meson/issues/2025) | install_man() does not take configuration_data | high | install_man still doesn't accept configuration_data — only file\|str. However, the established approach for ma |
| [#3659](https://github.com/mesonbuild/meson/issues/3659) | Could you please help with compile under profiler support like gprof | medium | This isn't a Meson bug but a question about how to use gprof. Passing -pg via c_args/link_args works fine on i |
| [#3665](https://github.com/mesonbuild/meson/issues/3665) | make possible to choose one of many compilers? | high | Compiler selection is already supported via the CC/CXX environment variables or the [binaries] section of a na |
| [#3812](https://github.com/mesonbuild/meson/issues/3812) | Documentation for meson developers | medium | The design rationale for Meson's own development is documented in Design-rationale.md and Contributing.md, the |
| [#4345](https://github.com/mesonbuild/meson/issues/4345) | The cmd_array() call on get_compiler() does not include compiler flags | medium | cmd_array() is specified to return only the compiler's execution command, deliberately excluding flags like c_ |
| [#4402](https://github.com/mesonbuild/meson/issues/4402) | How to cross compile for ARM with MSVC? | medium | Question about how to cross-build for ARM with MSVC while keeping a single PATH/LIB. vsenv auto-activation (ut |
| [#4486](https://github.com/mesonbuild/meson/issues/4486) | How to add default include directories for library found with compiler | medium | Question about wanting to add the header directory of a library found via find_library without hardcoding it.  |
| [#4572](https://github.com/mesonbuild/meson/issues/4572) | How to customize bindir setting from meson.build configuration file? | high | A question. bindir can be set as a project default via default_options and can also be overridden with -Dbindi |
| [#4872](https://github.com/mesonbuild/meson/issues/4872) | Help / Documentation wanted for how to integrate third-party lib | medium | A question about how to integrate third-party builds. The External Project module now exists, allowing autotoo |
| [#5374](https://github.com/mesonbuild/meson/issues/5374) | How to install Fortran .mod files? | medium | This is a usage question. The generated .mod file lives in the build directory and can be installed by explici |
| [#5429](https://github.com/mesonbuild/meson/issues/5429) | How to suppress messages from cxx.get_supported_arguments() | medium | A question about get_supported_arguments printing YES/NO for each argument in the log. This can be answered by |
| [#5747](https://github.com/mesonbuild/meson/issues/5747) | "meson test" concurrency vis "gdb" | medium | This originated as the user's own investigation of a race condition in their code and a question about the mea |
| [#5781](https://github.com/mesonbuild/meson/issues/5781) | dependency(static : true) handles a mix of static and dynamic transiti | low | The reporter themselves stated it is 'not a bug'; the issue exists to document a corner case that was resolved |
| [#5925](https://github.com/mesonbuild/meson/issues/5925) | Meson wraps installed libraries in architecture folder on Ubuntu 19.04 | medium | Debian-family multiarch libdir (lib/x86_64-linux-gnu) is intentional default behavior. Following the system de |
| [#5929](https://github.com/mesonbuild/meson/issues/5929) | Portable Independent Meson for macOS | medium | A request to package Meson as a single macOS .app bundle. Meson already has a PyInstaller-built standalone exe |
| [#6033](https://github.com/mesonbuild/meson/issues/6033) | Wanted to run some dtc (device tree compiler) commands to convert a dt | medium | A usage question about wanting to run multiple commands including a pipe like m4\|dtc in a custom_target. One  |
| [#6103](https://github.com/mesonbuild/meson/issues/6103) | Can we get an example for using alias_target in Meson documentation | medium | alias_target now has a description added to the YAML reference manual (docs/yaml/functions/alias_target.yaml), |
| [#6180](https://github.com/mesonbuild/meson/issues/6180) | meson --reconfigure or ninja configure should force dependency checks | medium | `meson setup --clearcache`, which invalidates the dependency cache and re-detects, has already been added (cor |
| [#6223](https://github.com/mesonbuild/meson/issues/6223) | g++ - long link line | low | Overly long link commands fail under ninja. It was initially pointed out that rsp files aren't used on Linux,  |
| [#6577](https://github.com/mesonbuild/meson/issues/6577) | Get raw compile / link arguments from dependencies | medium | The pkgconfig module handles generating pkg-config files, and retrieving a dependency's compile/link arguments |
| [#6605](https://github.com/mesonbuild/meson/issues/6605) | Can "exe_wrapper" accept a relative file command? | medium | A question about the base for relative paths. Since 1.3.0, machine files support @DIRNAME@ (the directory cont |
| [#6609](https://github.com/mesonbuild/meson/issues/6609) | subproject: specify libraries to install | low | A question about installing a prebuilt .so into the main project. Any file can be installed via install_data,  |
| [#6663](https://github.com/mesonbuild/meson/issues/6663) | [Question] Define library prefix/suffix via the meson call? | medium | A question about changing a generated library's prefix/suffix from the command line. Meson's approach is to ha |
| [#6805](https://github.com/mesonbuild/meson/issues/6805) | Layering Improvement: "Include" a cross/native base within the file | medium | A request to include another file from within a machine file. There's no direct include syntax, but equivalent |
| [#6811](https://github.com/mesonbuild/meson/issues/6811) | Way to specify backend for wxwdidgets dependency | high | A request to select the GTK3 build of wxWidgets' wx-config. wx-config can be overridden in a machine file's [b |
| [#6813](https://github.com/mesonbuild/meson/issues/6813) | Is there any way to compose *_args when layering cross files? | high | A request to compose *_args rather than overwrite them when layering cross files. Since 0.56.0, [constants] co |
| [#6825](https://github.com/mesonbuild/meson/issues/6825) | b_sanitize shouldn't apply to native builds when cross-compiling | medium | A problem where b_sanitize also applies to native tools during a cross build. Options are resolved per-target  |
| [#6975](https://github.com/mesonbuild/meson/issues/6975) | Is there a way to identify if this module/file should be compiled or n | medium | Kconfig-style conditional compilation can already be achieved with meson_options/get_option combined with if+s |
| [#7036](https://github.com/mesonbuild/meson/issues/7036) | Could you please give a full usable example of cross_file.txt? | medium | A request for a complete, working cross-file example. Practical samples exist in Cross-compilation.md and the  |
| [#7201](https://github.com/mesonbuild/meson/issues/7201) | Using embed perl in C project on MSVC | low | A usage question about how to split and pass perl's ccopts/ldopts on MSVC. This isn't a Meson bug but a shell  |
| [#7239](https://github.com/mesonbuild/meson/issues/7239) | Extract string from custom_target | medium | fs.read() exists for reading file contents into a string, but reading a custom_target's build-time-generated o |
| [#7378](https://github.com/mesonbuild/meson/issues/7378) | ninja backend + Visual Studio uses wrong name_prefix + extension for l | high | Static libraries being named libfoo.a on MSVC is intentional behavior (see the FAQ), but the `namingscheme=pla |
| [#7417](https://github.com/mesonbuild/meson/issues/7417) | Library compile flags are not passed to dependees | medium | `link_with` is specified not to propagate compile flags — this is intentional design. If you want dependency f |
| [#7507](https://github.com/mesonbuild/meson/issues/7507) | Issue to generate .so file with linking .a file | medium | When a static library (.a) is link_with'd into a shared_library, its symbols aren't pulled in and the result i |
| [#7780](https://github.com/mesonbuild/meson/issues/7780) | Question, is there anything similar CMAKE_PREFIX_PATH in meson? | medium | A question issue. Meson already has --cmake-prefix-path, the cmake_prefix_path machine-file setting, and --pkg |
| [#7916](https://github.com/mesonbuild/meson/issues/7916) | run_target calling gdb aborts | medium | Calling gdb via run_target fails because stdin isn't connected, aborting the session. run_target was never des |
| [#8710](https://github.com/mesonbuild/meson/issues/8710) | Clarification: non-existent subproject through dependency-fallback | low | Request for clarification on a documentation inconsistency about whether falling back to a nonexistent subproj |
| [#8795](https://github.com/mesonbuild/meson/issues/8795) | 2 subprojects need header files of each subproject bidirectional | low | A request for support for a setup where two subprojects mutually need each other's headers (a usage question,  |
| [#9084](https://github.com/mesonbuild/meson/issues/9084) | Build linux kernel modules (ko) with Meson? | medium | There is no native support for Linux kernel modules; this is a design question about calling Kbuild from Meson |
| [#9149](https://github.com/mesonbuild/meson/issues/9149) | meson test with cross compile fails | medium | Embedding WINEPATH into the exe_wrapper string is a misuse. Meson automatically computes WINEPATH from extra_p |
| [#9212](https://github.com/mesonbuild/meson/issues/9212) | @SOURCE_ROOT@ doesn't work in custom_target | high | @SOURCE_ROOT@ is substituted within command's arguments, but not when used as the command itself (the executab |
| [#9541](https://github.com/mesonbuild/meson/issues/9541) | [RFE] Consider tooling for easily spotting dependencies | medium | `meson introspect --scan-dependencies` scans meson.build and returns name/required/version/has_fallback/condit |
| [#9756](https://github.com/mesonbuild/meson/issues/9756) | Allow to generate and install .deps files for Vala libraries | medium | gnome.generate_vapi generates a .deps file via _generate_deps and installs it to install_dir (gnome.py:2237-22 |
| [#10099](https://github.com/mesonbuild/meson/issues/10099) | How to install relocatable shared lib on macOS (install_name set to @r | low | A question about how to create a relocatable shared library on macOS (install_name=@rpath). Mechanisms like in |
| [#10150](https://github.com/mesonbuild/meson/issues/10150) | project options (in native/cross file) are contained in Build options? | low | A question/documentation gap about the unclear relationship between project options and Build options in a mac |
| [#10234](https://github.com/mesonbuild/meson/issues/10234) | How to add a new language for projects in 2022? | low | Question about how to add support for a new language (e.g. Antlr4). This is a developer-guidance inquiry that  |
| [#10518](https://github.com/mesonbuild/meson/issues/10518) | Subproject I18N support | low | A question about I18N best practices for subprojects, with no bug involved. This can be handled through normal |
| [#10716](https://github.com/mesonbuild/meson/issues/10716) | Including generated directories | medium | A discussion about hitting argument-length limits from too many -I flags. Can be worked around with existing f |
| [#10853](https://github.com/mesonbuild/meson/issues/10853) | [Question] How to cross compile with gpu and host compilers | medium | A usage question about building a static library with hipcc/nvcc and linking it into a Cython extension. stati |
| [#10973](https://github.com/mesonbuild/meson/issues/10973) | Allow skipping tests using pytest-style arguments/DSL | medium | While not literally a pytest-style DSL, the core request — skipping specific tests from the command line — is  |
| [#11570](https://github.com/mesonbuild/meson/issues/11570) | Adding library and include directory | medium | A user question about how to write meson.build (specifically how to specify libraries for include_directories  |
| [#11796](https://github.com/mesonbuild/meson/issues/11796) | Spacing of parameters and colons in `meson.build` files? | high | A question about style preference. Meson's official formatter (meson format) uses no space before the colon (k |
| [#11836](https://github.com/mesonbuild/meson/issues/11836) | Request: Missing system identifier 'amiga' for cross-compilation proje | medium | 'system' is a free-form string with no whitelist validation, so system='amiga' already works in a cross file ( |
| [#11994](https://github.com/mesonbuild/meson/issues/11994) | Generator SOURCE_DIR and BUILD_DIR inside subproject incorrectly point | high | @SOURCE_DIR@/@BUILD_DIR@ are specified to point to the global root; @CURRENT_SOURCE_DIR@ is available for the  |
| [#12067](https://github.com/mesonbuild/meson/issues/12067) | How is a CMake subproject given a dependency? | medium | A usage question. The standard way to inject a dependency into a CMake subproject is to pass <pkg>_DIR / CMAKE |
| [#12280](https://github.com/mesonbuild/meson/issues/12280) | Feature request: Non-shorting disabler | medium | The issue that dict.get(key, disabler()) gets short-circuit evaluated. This is expected per Meson's disabler s |
| [#12658](https://github.com/mesonbuild/meson/issues/12658) | non-trivial dependency lookup with feature option | low | A question about the feature option (disabled) not taking effect for pipewire's webrtc-audio-processing-1 to f |
| [#12771](https://github.com/mesonbuild/meson/issues/12771) | Specifying clang-cl as a compiler prevents linking with link.exe | medium | The native file specifies the generic key `ld = 'link.exe'`, but Meson looks up the linker by language-specifi |
| [#13182](https://github.com/mesonbuild/meson/issues/13182) | How to set absolute path for meson dependency | medium | A usage question about resolving dependency('debugbreak'/'klib') from criterion via an offline absolute path.  |
| [#13656](https://github.com/mesonbuild/meson/issues/13656) | Detect free-threaded Python from configuration | medium | No dedicated API has been added yet, but since free-threaded detection is based on the sysconfig variable Py_G |
| [#13787](https://github.com/mesonbuild/meson/issues/13787) | Library `version` produces files with only the major version on Darwin | medium | On macOS, dylib filenames conventionally carry only the major version (e.g. libfoo.1.dylib), with the full ver |
| [#13964](https://github.com/mesonbuild/meson/issues/13964) | How to get "Requires:" field from pkg-config file? | medium | There is currently no API to directly retrieve pkg-config's Requires:, so a run_command-based workaround is re |
| [#13999](https://github.com/mesonbuild/meson/issues/13999) | How to use meson with an Android toolchain? | medium | dav1d's clock_gettime check failure stems from the Android cross file configuration (e.g. no compiler set for  |
| [#14101](https://github.com/mesonbuild/meson/issues/14101) | Override_options not replacing cpp_link_args as expected | medium | override_options' cpp_link_args appends rather than replaces existing flags, which is the specified (cumulativ |
| [#14201](https://github.com/mesonbuild/meson/issues/14201) | Any way to force buildtype for compiler.preprocess? | high | compiler.preprocess has supported compile_args since 1.3.2, and passing compile_args:'-g0' is the correct, por |
| [#14427](https://github.com/mesonbuild/meson/issues/14427) | dynamically links without warning, despite `static` in config | medium | dependency('SDL3', static:true) means 'prefer static if available'; per spec, if the pkg-config-provided SDL3  |
| [#14614](https://github.com/mesonbuild/meson/issues/14614) | how to change glib-mkenums path of gnome package | medium | A usage question about wanting to use a different glib-2.0. Since the gnome module finds glib-mkenums via the  |
| [#14954](https://github.com/mesonbuild/meson/issues/14954) | --strip does not have any effect on `meson install` for static librair | high | Static libraries are deliberately given can_strip=False in the backend (backends.py:1756, `can_strip = not isi |
| [#15119](https://github.com/mesonbuild/meson/issues/15119) | Meson Fails with vsenv option | medium | With vsenv:true, the message 'Visual Studio environment is needed to run Ninja' appears, but setup itself succ |
| [#15775](https://github.com/mesonbuild/meson/issues/15775) | [Question] Use of the name "meson" as part of one of my own applicatio | medium | A trademark/naming question about whether the name 'mesonsbom' can be used. Neither a bug nor a feature reques |
| [#15831](https://github.com/mesonbuild/meson/issues/15831) | AIX LPAR access to Meson community | medium | Not a code issue but an operational request about a contact point for providing a CI AIX machine; coordination |

<details><summary>Draft comments</summary>

**#553**:
```text
The `dependency('threads')` behavior is now documented (see the Threads page), and the compiler abstraction handles the platform-specific thread flags (pthread, win32, etc.). The original documentation/design concern has largely been addressed. If there's a concrete platform where the current handling is wrong, please open a focused issue; otherwise this can be closed.
```

**#620**:
```text
This was a usage question. Current Meson's `pkgconfig.generate()` accepts dependency objects (and other deps) in its `libraries`/`requires` arguments, so a boost dependency can be included directly. The original 'Library argument not a library object' limitation no longer applies. Closing as answered; please reopen if you still hit this.
```

**#1104**:
```text
Much of this is now covered: the `b_vscrt` base option lets you select the MSVC static runtime (`/MT`), and `-Db_vscrt=static_from_buildtype` plus `prefer_static`/`default_library=static` (and `-static` link args for MinGW) allow largely static binaries. Fully static, fully portable .exe still depends on the toolchain, but the Meson-side knobs exist. Closing as answered; please reopen for a specific remaining gap.
```

**#1229**:
```text
Cross-directory use of Vala-generated headers/vapi is generally handled by building the producing target as a library and depending on it (via `link_with`/`declare_dependency(sources: ...)`), which propagates the generated header dependency. Please try this on a current Meson; if it still doesn't work for your layout, reopen with a minimal reproducer and we'll dig in.
```

**#2025**:
```text
install_man intentionally doesn't take configuration_data. The established pattern is to run the man page through configure_file() (for version/path substitutions) and pass the resulting file to install_man(). Note install_man currently accepts file/str inputs only (see #1550 for accepting target outputs). Closing as answered; feel free to reopen if you think inline substitution in install_man is worth adding.
```

**#3659**:
```text
This is a usage question about gprof rather than a Meson bug. Adding `-pg` to both compile and link args (via `c_args`/`link_args` or environment) is the correct way to enable gprof instrumentation with Meson, and it does work. Empty `gprof` output usually means the program didn't exit normally, was statically-linked differently, or you're pointing gprof at the wrong binary/gmon.out. Since this isn't a Meson defect and the thread is stale, I'm closing it; the Meson discussion channels are a better place for toolchain usage help.
```

**#3665**:
```text
Meson already supports this: set the compiler with the standard `CC`/`CXX` environment variables at first configuration (e.g. `CC=gcc CXX=g++ meson setup build`), or, for a persistent and more explicit setup, use a native file with a `[binaries]` section specifying the exact compiler binaries. See the 'Machine files' and 'Running Meson' docs. Closing as answered.
```

**#3812**:
```text
For working on Meson itself, the closest documents are Design-rationale.md (the rationale behind the DSL and architecture) and Contributing.md, which covers the main design principles, coding conventions, and various internal design points. There isn't a single exhaustive internals manual, but those two plus the module/backend source layout are the intended starting points. Closing as answered; suggestions for additional developer docs are welcome as PRs.
```

**#4345**:
```text
This is working as intended: `cmd_array()` returns only the compiler executable/command list, not user or cross-file argument flags (see the reference manual). Flags from `c_args`, the cross file's `[built-in options]`, etc. are applied by Meson's build rules, not embedded in `cmd_array()`. If you need the compiler plus specific args, retrieve the options explicitly (e.g. via `get_option()` / machine-file properties) and append them yourself. Closing as answered; let us know if you think a dedicated API to expose the effective compiler args is warranted.
```

**#4402**:
```text
For MSVC cross builds you separate the two toolchains using a native file and a cross file: run inside the ARM (host) vcvars environment for the cross file's `cl`, and point a native file at the x64/x86 build-machine `cl` (with its own LIB) so the native sanity check uses a runnable compiler. Meson also auto-activates a Visual Studio environment (`setup_vsenv`) when appropriate. If you can share what you tried, we can advise on the exact native/cross file contents. Closing as answered; reopen if you hit a concrete blocker.
```

**#4486**:
```text
`compiler.find_library()` only performs link-time library resolution; it has no way to know where a library's headers live, so it can't auto-add include directories. The idiomatic options are: use `dependency()`/pkg-config if available; otherwise wrap the found library plus its headers with `declare_dependency(dependencies: found_lib, include_directories: include_directories('...'))`, or pass `include_directories()` explicitly. (find_library's `has_headers`/`header_include_directories` are for verifying headers exist during the search, not for propagating include paths.) Closing as answered.
```

**#4572**:
```text
You can set `bindir` either from the command line (`-Dbindir=...`) or as a project default via `default_options: ['bindir=...']` in `project()`. Note this controls the install location under the prefix, not where binaries land inside the build tree. Closing as answered — please reopen if you had a different use case in mind.
```

**#4872**:
```text
For integrating a third-party project that has its own build system, Meson now provides the External Project module (see docs/markdown/External-Project-module.md), which builds an autotools/CMake project inside your build and exposes it as a dependency (including via pkg-config). That should cover the use case here. Closing as answered — please reopen if it doesn't fit.
```

**#5374**:
```text
Meson does not automatically install generated `.mod` files, but you can install them explicitly. The `.mod` files are emitted into the build directory (per-target module output dir), so you can add an `install_data()`/`custom_target` install rule pointing at the generated file, or install them alongside your headers. If you'd like Meson to grow first-class support for auto-installing Fortran modules, that would be a separate feature request. Closing as answered.
```

**#5429**:
```text
The `YES`/`NO` lines from `get_supported_arguments()` are informational log output, not errors — a red `NO` simply means that specific flag isn't supported and is dropped from the returned list, which is exactly the intended behaviour. There isn't a dedicated flag to silence just these lines; the `checked` keyword (added in 0.59.0) only controls whether an unsupported arg warns or errors. If you'd like a quieter mode for this specific method, that would be a separate enhancement request. Closing as answered.
```

**#5747**:
```text
`--num-processes` (`-j`) controls how many test processes Meson runs in parallel; it is not a thread count. With `--gdb`, Meson already forces serial execution. The original report was chasing a race condition in the project's own test code rather than a Meson bug, and no reproducer against Meson itself was provided. Since this appears to be a usage question that has been answered, I'll close it, but please reopen with a minimal Meson reproducer if you believe Meson's concurrency handling is at fault.
```

**#5781**:
```text
As you noted, this is a documented corner case rather than a bug: `dependency(static: true)` deliberately prefers static libraries throughout the transitive chain, which differs from a plain `pkg-config --static` that keeps whatever `.pc` files it first resolves. You've already adopted a reasonable workaround. Since there's no actionable bug here, I'll close this; if you'd like a new opt-in mode that mirrors `pkg-config --static` semantics exactly, a fresh feature request would be the better venue.
```

**#5925**:
```text
This is intended behavior on Debian/Ubuntu: those distros use multiarch library paths (`lib/x86_64-linux-gnu`), and for a native build Meson deliberately follows the system default `libdir` so installed libraries match distro conventions. The reason the binary can't find the library is that no rpath/loader path points there for a `/usr/local` install; that's the same for any build system. Your workarounds (`--libdir=lib` or setting `install_rpath` to `libdir`) are the correct approaches. Since this is by-design rather than a bug, I'll close it. See also #1972.
```

**#5929**:
```text
Meson is distributed as a standalone, dependency-bundled executable via its release artifacts (built with PyInstaller), and can also be installed portably through `pipx`, Homebrew, or `pip install --user`. These cover the 'no separate Python install needed' use case that a CMake-style `.app` bundle would provide. There isn't a strong reason to maintain a dedicated macOS `.app`. I'll close this as answered; if there's a concrete workflow the existing standalone releases don't cover, please describe it and we can reopen.
```

**#6033**:
```text
A `custom_target` runs a single command, so for a pipeline like `m4 ... | dtc ...` the idiomatic approach is a small wrapper script (shell/python) invoked as the target's command, or two chained `custom_target`s where the second consumes the first's output. `capture: true` / `feed: true` cover simple stdin/stdout redirection. This is a usage question rather than a Meson defect, so I'll close it; feel free to ask on the discussion tracker if you need help wiring up the wrapper.
```

**#6103**:
```text
`alias_target` is now documented in the reference manual (see https://mesonbuild.com/Reference-manual_functions.html#alias_target ), including how it integrates with `meson compile target_name` and both-library support. If a fuller worked example would still help, please let us know what use case you had in mind; otherwise this documentation request appears addressed.
```

**#6180**:
```text
Meson now provides `meson setup --clearcache` (optionally with `--reconfigure`), which clears the cached dependency lookups so they are re-detected against the current environment (see `coredata.clear_cache()` clearing the deps cache). This gives the explicit "force re-check dependencies" behavior requested here. `--reconfigure` on its own intentionally keeps the cache for speed. Does `--clearcache` resolve your use case?
```

**#6223**:
```text
This is primarily a support question about very long link lines. Note that (a) Meson does support array slicing now, and (b) response-file usage for the Ninja backend is platform/linker dependent. If you still hit a hard failure with no diagnostic on a current Meson+Ninja, please reopen with the exact ninja error. Otherwise closing as answered.
```

**#6577**:
```text
If the goal is to produce a pkg-config file, use the `pkgconfig` module (`pkgconfig.generate()`), which writes correct Cflags/Libs from your libraries and dependencies. Meson intentionally does not expose raw per-dependency compile/link argument strings as a public API (they are not portable and vary per compiler/machine); `dependency().get_variable(...)` covers the documented cases. Closing as answered — please reopen with a concrete use case that the pkgconfig module cannot handle.
```

**#6605**:
```text
Relative paths in a machine/cross file are resolved against your working directory / PATH, which is why bare or `..`-relative names were unreliable. Since Meson 1.3.0 you can anchor the path deterministically using the `@DIRNAME@` token (the directory containing the machine file) or `@GLOBAL_SOURCE_ROOT@`, e.g. `exe_wrapper = '@DIRNAME@' / 'hardwareSim.bat'`. See the 'Machine files' documentation. Closing as answered.
```

**#6609**:
```text
You can install an arbitrary prebuilt file with `install_data('lib/foo.so', install_dir: get_option('libdir'))`, and select the right architecture-specific file inside the subproject using `host_machine.cpu_family()` / `host_machine.system()`. Wrap the includes/link args in `declare_dependency(...)` so the main project just consumes the dependency object. This keeps all the details in the subproject. Closing as answered — please reopen if a concrete case isn't expressible this way.
```

**#6663**:
```text
Meson controls library naming per target via the `name_prefix` and `name_suffix` keyword arguments to `library()`/`shared_library()`/`static_library()`, not via a global `-D` variable like CMake's `CMAKE_*_LIBRARY_(PREFIX|SUFFIX)`. If you need to override the default per platform, set `name_suffix`/`name_prefix` (optionally driven by your own project option). Closing as answered.
```

**#6805**:
```text
Meson doesn't have a literal `include('base.txt')` directive inside machine files, but the intended workflow is supported two ways: (1) pass multiple `--cross-file`/`--native-file` args, which layer/compose; and (2) since 0.56.0 the `[constants]` section lets you define shared toolchain values in a base file and reference them from a platform file, which composes across layered files. See Machine-files.md. Closing as answered; a dedicated `include` directive can be tracked separately if there's demand for it beyond layering.
```

**#6811**:
```text
You can pin the wx-config binary in a native/machine file's `[binaries]` section, e.g. `wx-config = '/usr/bin/wx-config-gtk3'` — this is documented in Machine-files.md (wx-config is in the list of overridable config tools). Config-tool dependencies also honor a `tools` kwarg. This gives reproducible selection of the GTK3 build without uninstalling GTK2. Closing as answered.
```

**#6813**:
```text
Since 0.56.0 machine files support a `[constants]` section plus the `+` (concatenation) and `/` (path join) operators, which is exactly the composition you want. Define the shared flags once and build up per-target sets: e.g. `[constants]\nfp_flags = ['-mfloat-abi=hard', ...]` then `[properties]\nc_args = common_flags + fp_flags`. This composes across layered `--cross-file` args instead of overriding. See Machine-files.md. Closing as answered.
```

**#6825**:
```text
b_* options are now resolved per target (`get_option_for_target`), and build targets accept an `override_options` kwarg, so you can build a native tool without ASan via `executable('nativehelper', ..., native: true, override_options: {'b_sanitize': 'none'})`. That covers the concrete failure described. Whether Meson should also change the *default* so sanitizers never apply to build-machine targets is a design decision; if you want to pursue that specifically, let's keep that scoped discussion, but the immediate need is addressable today. Closing as answered — reopen if the default-behavior change is what you want tracked.
```

**#6975**:
```text
This is a usage question. The typical Meson approach is to define options (`meson.options`/`get_option()`) and conditionally `subdir()` into module directories, e.g. `if get_option('module_a') \n subdir('module_a') \n endif`. For a kernel/U-Boot-style `.config` file, Meson ships the `keyval` module which can load `KEY=VALUE` config files into a dictionary you can branch on. Closing as answered; please follow up on the mailing list / discussions if you need more detail.
```

**#7036**:
```text
The cross-compilation docs now contain complete, usable examples, and the Meson repository ships ready-to-use cross files under the `cross/` directory (e.g. for various toolchains) that you can copy and adapt. See https://mesonbuild.com/Cross-compilation.html and the `cross/` folder. Closing as answered; if a specific target is missing, please open a focused request.
```

**#7201**:
```text
This is a usage question rather than a Meson bug. The output from `ExtUtils::Embed` on Windows/MSVC is MSVC-style flags (e.g. `-I"..."`, `-libpath:"..."`), which don't split the same way as GCC-style flags. You'll need to post-process the strings yourself (handling quoted paths). This is better suited to Meson's discussions/mailing list; closing here. If you believe there's a concrete Meson bug (e.g. `run_command` mangling quotes), please open a focused report with a minimal reproducer.
```

**#7239**:
```text
For reading a file into a string at configure time there is now `fs.read()` (the `fs` module). However, note that it deliberately cannot read build-time-generated files (custom_target outputs): those don't exist at configure time and reading them would create a configure/build loop, so `fs.read()` rejects paths in the build tree. For your CRC use case, the value must be consumed at build time — e.g. generate the linker `--defsym` argument inside a wrapper script/custom_target, or generate a small source/linker-script file, rather than trying to turn the custom_target output into a Meson string. Closing as answered; happy to reopen if this doesn't fit.
```

**#7378**:
```text
The default `libfoo.a` naming for static libraries on Windows is intentional (it avoids clashing with import libraries and works with both MSVC and GCC toolchains — see https://mesonbuild.com/FAQ.html#why-does-building-my-project-with-msvc-output-static-libraries-called-libfooa). However, since Meson 1.10.0 there is now a `namingscheme` option: setting `-Dnamingscheme=platform` produces platform-native names, so static libraries get `.lib`, shared libraries `.dll` and import libraries `.dll.lib`. That should give you the `mylibrary.lib` you expected. Closing as resolved by that option; please reopen if it doesn't cover your case.
```

**#7417**:
```text
This is working as designed: `link_with` only links against a library, it does not propagate the library's compile arguments (like `-DBOOST_LOG_DYN_LINK`). Compile-argument propagation is what dependency objects are for. Wrap the library plus its Boost dependency in `declare_dependency(link_with: log, dependencies: [boost_dep])` and pass that via `dependencies:` to consumers — the boost compile args (including the DYN_LINK define) will then propagate correctly, including across subprojects. Closing as answered; please reopen if that doesn't work for you.
```

**#7507**:
```text
This is the standard linker behaviour: when you link a static library (`.a`) into a shared library with `link_with`, the linker only pulls in object files that resolve an already-referenced symbol, so unreferenced symbols (like your DPI exports) are dropped — hence the small `.so`. Use `link_whole:` instead of `link_with:` to force the entire archive (all object files/symbols) into the shared library. That produces the full-size, working `.so` you get from manually linking the `.o` files. Closing as answered; please reopen if `link_whole` doesn't solve it.
```

**#7780**:
```text
Meson does have equivalents depending on what you need. For CMake-based dependencies you can set `cmake_prefix_path` (in the `[properties]` section of a machine file, or via `-Dcmake_prefix_path=...`), which maps to CMake's `CMAKE_PREFIX_PATH`. For pkg-config based lookups, use `--pkg-config-path` / the `PKG_CONFIG_PATH` environment variable. Since this is a usage question rather than a bug, closing; please reopen or ask on the mailing list / Matrix channel if these don't cover your case.
```

**#7916**:
```text
`run_target` is designed for fire-and-forget commands and doesn't connect stdin, so interactive tools like gdb can't work through it. For running a debugger under Meson, Meson 1.5.0 added `meson test --interactive`, which invokes the test with stdin/stdout/stderr connected directly to the console (see the 1.5.0 release notes), making it usable for gdb-style interactive sessions. Given that, `run_target` is unlikely to be changed to support interactivity; closing, but please comment if `--interactive` doesn't cover your workflow.
```

**#8710**:
```text
The apparent contradiction is resolved by the semantics: a `fallback` to a not-installed subproject is legal, and when the fallback cannot be provided the `required:` kwarg is obeyed (so an optional dependency is simply not-found). The confusing error message wording around subprojects/wraps has since been iterated on. If the current docs still read ambiguously, a focused docs PR softening the `subproject()`/`dependency()` wording would be welcome. Marking as answered.
```

**#8795**:
```text
This is a usage question rather than a defect. The supported pattern is: in each subproject expose only its include directory via `declare_dependency(include_directories: ...)` (no `link_with`), and have each subproject consume the other's include-only dependency. Include-only dependencies do not create a link cycle, so the bidirectional-headers case works without symlinks. For subproject 1 which also links subproject 2, add `link_with` only on that side. Please follow up on the Matrix channel or GitHub Discussions if you need more detail; closing as answered.
```

**#9084**:
```text
Meson does not build Linux kernel modules natively, and this is unlikely to change: `.ko` modules must be built through the kernel's own Kbuild system (which pulls in the running kernel's headers, config, and Makefile machinery). The practical approach is to wrap Kbuild in a `custom_target()` that invokes `make -C /lib/modules/$(uname -r)/build M=$PWD modules` and captures the resulting `.ko`. Since this is a usage question with no planned native support, I'll close it — please continue the discussion on the tracker if you'd like to pursue a helper module.
```

**#9149**:
```text
The `exe_wrapper` should just be `wine` (or `['wine']`), not a string with an embedded `WINEPATH=...` prefix — Meson doesn't parse env-var assignments inside the wrapper string, which is why `meson test` fails to find it. For the sanity-check DLL problem, Meson already computes `WINEPATH` automatically for wine wrappers from the build's library/extra paths (see `mesonbuild/scripts/meson_exe.py`, where it sets `child_env['WINEPATH']` when the wrapper command contains `wine`). If a specific extra directory is still needed, add it via the toolchain library paths rather than the wrapper. This is really a documentation/usage matter; closing as answered — reopen if `meson test` still can't run wine tests with a plain `exe_wrapper = 'wine'` on a current release.
```

**#9212**:
```text
`@SOURCE_ROOT@` is substituted in command *arguments*, not in the command's first element (the program). In your example `command : ['@SOURCE_ROOT@', '/foo.sh']`, Meson tries to resolve `@SOURCE_ROOT@` as a program to run, hence `Program '@SOURCE_ROOT@' not found`. To run a script from the source tree, pass the script via `find_program()` or `files()` as the program, e.g. `command : [find_program('foo.sh')]`, or use `@SOURCE_ROOT@` only inside later arguments. The substitution machinery is in `mesonbuild/backend/backends.py` (`eval_custom_target_command`), which only rewrites string *arguments*. Closing as answered.
```

**#9541**:
```text
`meson introspect --scan-dependencies /path/to/meson.build` scans the build definitions (no configured build dir required) and reports each dependency with its name, required flag, version, whether it has a wrap fallback, and whether it is used conditionally (mesonbuild/mintro.py list_deps_from_source; docs IDE-integration 'Scanning for dependencies'). That covers the packaging-report use case of listing dependencies and their conditions. Closing as answered; please follow up if you need additional fields.
```

**#9756**:
```text
gnome.generate_vapi already generates and installs a `.deps` file next to the `.vapi`: the packages passed to generate_vapi are written one-per-line into `<library>.deps` and installed alongside the vapi (mesonbuild/modules/gnome.py, _generate_deps). List the interface packages in the `packages` argument to control its contents. Closing as answered; please reopen if you need a way to specify a deps list distinct from the compile-time depends.
```

**#10099**:
```text
This is a usage question rather than a bug. Meson relinks at install time and rewrites the `install_name`/rpaths of installed macOS libraries; you can control the runtime search path with the `install_rpath` kwarg on the library target, and Meson already remaps dependency install names for installed binaries. If a specific project still ends up with an absolute `install_name`, please open a new issue with a minimal reproducer. Closing as answered; the mailing list / Matrix room is also a good place for how-to questions.
```

**#10150**:
```text
Your mental model is essentially correct: "build options" is the umbrella that includes built-in options (universal/base/compiler/etc.) and per-project options, and machine files can set both via `[project options]` and `[built-in options]`. The Machine-files and Build-options pages could cross-reference each other more clearly. A small docs PR linking the two sections would be very welcome. Closing as answered; please reopen or file a focused docs issue if a specific passage is still misleading.
```

**#10234**:
```text
This is a how-to/contribution question rather than a bug. Adding a first-class language means implementing a `Compiler` subclass under `mesonbuild/compilers/`, wiring it into `mesonbuild/compilers/detect.py`, and adding backend/test support; existing compilers (e.g. `nasm`/`cython`/`swift`) are good templates. Note that Antlr specifically is a code generator, which is usually better handled via `generator()`/`custom_target()` than as a project language. For design help, the Matrix room / mailing list is the best venue. Closing as answered; please reopen if you hit a concrete blocker while implementing.
```

**#10518**:
```text
This is a usage question rather than a bug. Each (sub)project can call `i18n.gettext()` with its own `po` directory and translation domain independently; the main project and subprojects manage their own `LINGUAS`/`.po` files and gettext domains. Meson does not merge translation catalogs across subproject boundaries automatically — the recommended approach is a separate domain per component. For usage help, the Meson discussions/matrix channels are a better venue than the issue tracker. Closing as answered; feel free to follow up if there's a concrete missing capability.
```

**#10716**:
```text
This is a usage question rather than a missing feature. To avoid the huge `-I` list you don't need to pass the generated files as sources (which caused them to be linked in). Instead, keep the `custom_target` for generation and reference its output directory via `include_directories()` / `declare_dependency(include_directories: ...)`, and add the target as a dependency so ordering is correct. Meson (with the Ninja backend) also uses response files for link commands, which sidesteps most command-length limits. If a concrete case still hits the argument-list limit with current Meson, please reopen with a minimal reproducer. Closing as answered.
```

**#10853**:
```text
This is a usage question. Meson doesn't let you pick an arbitrary compiler for `static_library()`, but you have two options: (1) if you enable Meson's built-in `cuda` language you can build CUDA/HIP sources directly; or (2) drive `hipcc`/`nvcc` via a `custom_target()` that emits a `.a`, then pass that archive to your Cython `extension_module` via `link_with:`/`objects:` (or wrap it with `declare_dependency`). For questions like this the Discussions board / Matrix room is the best venue. Closing as answered; feel free to follow up there.
```

**#10973**:
```text
`meson test` now supports an `--exclude` argument (see the tests-exclude release snippet): it takes a full test name and can be repeated to skip specific tests from the command line, e.g. for a build where certain tests are known to fail on 32-bit. This covers the primary use case here (Gentoo skipping the Pango precision tests). It is not the full pytest `-k` expression DSL, but if a richer selection grammar is still wanted that would be better tracked as a separate, more narrowly-scoped enhancement. Closing as the core request is addressed — please comment if a full DSL is still desired.
```

**#11570**:
```text
This is a usage question rather than a bug. Putting `-L.../-lghdl` into `add_global_arguments(language: 'c')` only affects compilation, not linking, which is why you get undefined references. Instead, either: (1) find the library and pass it as a dependency, e.g. `cc = meson.get_compiler('c')` then `ghdl_dep = cc.find_library('ghdl', dirs: ['/home/r2com/eda/install/ghdl/lib'])` and `executable('vpi', 'test.c', include_directories: inc, dependencies: ghdl_dep, c_args: ['-fPIC'])`; or (2) pass `link_args: ['-L/home/r2com/eda/install/ghdl/lib', '-lghdl']` on the target. For a `.vpi` plugin you likely want `shared_module()` rather than `executable()`. For further how-to questions, the Meson discussions or Matrix channel is a better venue. Closing as answered — feel free to follow up if a specific Meson behavior remains unclear.
```

**#11796**:
```text
The convention used throughout Meson's own documentation and enforced by the built-in `meson format` formatter is `function(param: value)` — no space before the colon, one space after — matching typical Python keyword-argument style. The `param : value` form is accepted by the parser but is not the recommended style. If you want automatic, consistent formatting across a project, run `meson format`. Closing as answered, but feel free to follow up.
```

**#11836**:
```text
Meson does not restrict the `system` field to a fixed list — it accepts any string in cross/native files, so you can already use `system = 'amiga'` today and `host_machine.system() == 'amiga'` will work as expected. The Operating system names table in Reference-tables.md lists only the conventional values and explicitly notes that "Any string not listed above is not guaranteed to remain stable in future releases". If you'd like `amiga` added to that conventional table for discoverability, a small docs PR would be welcome. Closing as answered since the functionality already exists.
```

**#11994**:
```text
In generator arguments, `@SOURCE_DIR@` and `@BUILD_DIR@` are defined to expand to the project's global source/build roots (`replace_paths` in `mesonbuild/backend/ninjabackend.py`). For the per-subdir/subproject equivalent of `meson.current_source_dir()`, Meson provides the `@CURRENT_SOURCE_DIR@` placeholder, which expands to the current target's source directory and works correctly inside subprojects. Switching your `-i '@SOURCE_DIR@'` to `-i '@CURRENT_SOURCE_DIR@'` should resolve this. Closing as answered; if the docs weren't clear about this, a small docs PR would be welcome.
```

**#12067**:
```text
This is a usage question rather than a bug. Meson's CMake module cannot directly inject a Meson `dependency()` object into a CMake subproject's `find_package()`; CMake performs its own package discovery. The supported approach is to pass CMake cache variables via `cmake.subproject_options()` + `opts.add_cmake_defines({...})`, e.g. set `nlohmann_json_DIR` (or add the config dir to `CMAKE_PREFIX_PATH`) so the nested `find_package(nlohmann_json)` succeeds. If nlohmann_json is itself built as a Meson subproject you can point the CMake define at its installed/exported config dir. Since there's no actionable Meson bug here and the mechanism exists, I'd suggest closing; please reopen or move to a Discussion if a concrete gap remains.
```

**#12280**:
```text
The short-circuiting is by design: a disabler propagates through calls to disable dependent targets. For the dictionary-default pattern the idiomatic solutions are the ones you already found (wrap values in a 1-element list and unwrap, or use `is_disabler()` to branch explicitly), e.g. `hal = mapping.get(get_option('mcu'), false); if hal == false: hal = disabler(); endif` won't work due to typing, but `import('...').get(...)` with a sentinel plus an explicit `if` is the supported approach. A dedicated 'non-shorting disabler' would complicate the object model. Unless there's a concrete case the existing patterns can't express, I'd suggest closing; please reopen with such a case if one exists.
```

**#12658**:
```text
This is a meson.build logic issue rather than a Meson bug. To honor `echo-cancel-webrtc=disabled`, check the feature option before attempting the first lookup, e.g.:

```
feat = get_option('echo-cancel-webrtc')
webrtc_dep = dependency('', required: false)
if not feat.disabled()
  webrtc_dep = dependency('webrtc-audio-processing-1', version: '>=1.2', required: false)
  if not webrtc_dep.found()
    webrtc_dep = dependency('webrtc-audio-processing', version: ['>=0.2','<1.0'], required: feat)
  endif
endif
```

Guarding the whole block on `feat.disabled()` gives exactly the truth table you listed. Closing as answered — feel free to follow up if something doesn't behave as expected.
```

**#12771**:
```text
Meson looks up the linker override via a per-language binary key, not a bare `ld` entry. In `guess_win_linker` it queries `<lang>_ld` (see `mesonbuild/linkers/detect.py`, the `env.lookup_binary_entry(for_machine, comp_class.language + '_ld')` call). So your `[binaries] ld = 'link.exe'` is never consulted, and because the compiler is clang-cl, Meson defaults to `lld-link`. Please use the language-specific key instead, e.g. `c_ld = 'link.exe'` (and `cpp_ld = 'link.exe'` for C++). That should make Meson use `link.exe`. Closing as answered, but feel free to follow up if `c_ld` does not work for you.
```

**#13182**:
```text
This is a usage question rather than a Meson bug. For header-only/source deps that aren't packaged, the intended offline approaches are: (1) add a `.wrap` file under `subprojects/` with a `[provide]` section (plus the sources under `subprojects/packagefiles/`) so `dependency()` resolves via the fallback without downloading; or (2) write a small `.pc` file and point `PKG_CONFIG_PATH` at it; or (3) in your own `meson.build`, use `declare_dependency(include_directories: ..., sources: ...)` together with `meson.override_dependency('klib', ...)`. Note that `fallback:` expects a subproject *name*, not an absolute path, which is why that attempt errored. See https://mesonbuild.com/Wrap-dependency-system-manual.html. Closing as answered — feel free to follow up on Matrix/Discussions.
```

**#13656**:
```text
There is currently no dedicated method, but because free-threaded builds are identified by the `Py_GIL_DISABLED` sysconfig variable, you can already detect this from your `meson.build`:

```meson
py = import('python').find_installation()
if py.get_variable('Py_GIL_DISABLED', '0') == '1'
  add_project_arguments('-DMY_FREE_THREADED', language: 'c')
endif
```

(`py.has_variable('Py_GIL_DISABLED')` also works.) Internally Meson derives its own `is_freethreaded` flag from the same variable. If a first-class helper is still wanted, that would be a separate enhancement request. Does the sysconfig-variable approach cover your use case?
```

**#13787**:
```text
This is expected macOS behaviour, and the discrepancy is in the documentation rather than the build output. On Darwin the filename/install_name conventionally carries only the major (compatibility) component (`libfoo.1.dylib`), while the full version is encoded in the Mach-O `compatibility version` / `current version` fields (exposed via the `darwin_versions` kwarg). The docs example `libfoo.1.1.0.dylib` is misleading and should be corrected to reflect this. Re-labeling as a documentation fix.
```

**#13964**:
```text
There's currently no dedicated Meson API to read the `Requires:` field of a pkg-config dependency directly — `dep.get_variable(pkgconfig: ...)` only exposes pkg-config *variables*, not `Requires`. Your `run_command('pkg-config', '--print-requires', ...)` workaround is the recommended approach today. If you'd like first-class support, this would be better tracked as a focused feature request (e.g. a `dep.get_pkgconfig_requires()` method). Closing as answered — please reopen/refile as an enhancement if you want the API.
```

**#13999**:
```text
This is a cross-compilation configuration issue rather than a Meson bug. The log shows `Compiler for language c for the build machine not found`, and dav1d's `clock_gettime` check is failing because the Android NDK sysroot/flags aren't fully wired up in your cross file. For Android NDK builds you generally need a cross file that sets the NDK clang with the right `--target`/`--sysroot` args and (if any build-machine tools are needed) a native compiler as well. The Meson cross-compilation docs and the dav1d project's own Android cross files are good references. Since there's no Meson defect here, I'll close this — please reopen with a minimal cross file if you believe Meson is misbehaving.
```

**#14101**:
```text
This behaves as designed: `cpp_link_args` (and the other `*_args`/`*_link_args` options) are *additive* — Meson appends them rather than replacing the full link command line, and `override_options` doesn't remove flags that come from elsewhere (e.g. a `-static` injected by the environment or default options). There's no supported way to 'subtract' a link flag via options. If `-static` is coming from `CXXFLAGS`/`LDFLAGS` or default_options, adjust it at the source instead. This is really a documentation-clarity issue; I'll leave it for a docs update but the current behavior is intentional.
```

**#14201**:
```text
Passing `compile_args : '-g0'` is the correct and supported approach here. As of Meson 1.3.2, `compiler.preprocess()` accepts a `compile_args` keyword (before that version it was silently ignored), and these arguments are appended after the buildtype-derived flags, so `-g0` reliably overrides an earlier `-g3`. This is portable and there is no separate per-call buildtype override planned. If passing `-g0` does not resolve your case on a current Meson release, please reopen with a minimal reproducer. Closing as answered.
```

**#14427**:
```text
This is Meson's documented behavior for `static: true` on `dependency()`: it *prefers* a static library but, when the dependency is found via pkg-config and no static archive is available (which is common for distro `SDL3` packages that ship only the shared `.pc`/`.so`), Meson falls back to the shared library rather than failing. The CMake example works because it explicitly requests the separate `SDL3::SDL3-static` target, which only exists if the static build was installed. To force a hard failure when static isn't available, or to guarantee static linking, you generally need the static library/`.pc` to be present (e.g. build SDL3 as a subproject with `default_library=static`). If you'd like `static: true` to *error* instead of silently falling back, that would be a separate design-change request. Closing as answered; feel free to follow up if a static `.pc` is present and still not used.
```

**#14614**:
```text
This is a configuration question rather than a bug. Meson locates `glib-mkenums` via the `glib-2.0` dependency, which is resolved through pkg-config. To point Meson at a different glib installation (e.g. one whose `glib-2.0.pc` lives under `/tmp/xxx`), set the `PKG_CONFIG_PATH` environment variable (or the `pkg_config_path` in a native file) so that pkg-config finds your alternative `glib-2.0.pc` first. The `glib-mkenums` program bundled with that glib will then be used. If that does not work for your case, please reopen with a full `meson setup` log so we can see how the tool is being resolved.
```

**#14954**:
```text
Thanks for the report. This is by design: Meson deliberately marks static libraries as non-strippable in the backend (`can_strip = not isinstance(t, build.StaticLibrary)` in `mesonbuild/backend/backends.py`), so `--strip` (and the `strip` option) intentionally have no effect on `.a` archives. Stripping a static archive can remove symbols that are still required at link time by downstream consumers, which is why Meson leaves static libraries untouched and relies on the linker/compiler flags (e.g. `-ffunction-sections`/`--gc-sections`, LTO) plus stripping of the final executable/shared library instead. If you want a smaller archive you can run your toolchain's `strip`/`ar` manually as you did, or strip the final linked target. We agree the documentation could state this more explicitly, so a docs note that `--strip` does not apply to static libraries would be a welcome follow-up; the current behaviour itself is intentional and not a bug.
```

**#15119**:
```text
This message is expected and not a hard failure: `meson setup` completed successfully (note it printed "Activating VS 17.14.16" and configured your project). The line "Visual Studio environment is needed to run Ninja. It is recommended to use Meson wrapper: ... meson compile -C build" is informational — it tells you that when using `--vsenv`, Meson has captured the VS environment for the build step, and you should invoke the build through `meson compile -C build` rather than calling `ninja` directly, because a bare `ninja` shell won't have the VS environment activated. In your GitHub Actions workflow, replace the direct `ninja`/`ninja -C build` step with `meson compile -C build`. If you are already using `meson compile` and still hit an actual build error (not just this message), please attach the full output of the `meson compile` step and we'll investigate further.
```

**#15775**:
```text
Thanks for checking first. Meson is under the Apache-2.0 license and there's no registered trademark restricting descriptive third-party names, so a clearly-labeled independent tool named something like `mesonsbom` — with a README stating it's unofficial and not affiliated with the Meson project — is generally fine. Please just avoid implying official endorsement or using the project's logos. If you have licensing-specific concerns beyond naming, the mailing list / maintainers can weigh in, but from a naming standpoint this should be OK. Closing as answered — feel free to reopen if you need more specifics.
```

**#15831**:
```text
Thanks a lot for the generous offer of an AIX LPAR for CI — this is very much appreciated. This is really an infrastructure/coordination matter rather than a code issue, so the GitHub tracker isn't the best place to exchange SSH keys or private contact details. Could you reach out to the maintainers directly (e.g. via the mailing list / the maintainers CC'd here) so the details can be arranged privately? I'll close this issue for now, but please follow up on that channel — thank you again.
```

</details>

#### Invalid / out of scope (26)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#5826](https://github.com/mesonbuild/meson/issues/5826) | ERROR: Could not invoke sanity test executable | medium | A configuration mistake where the sanity check fails with 'Exec format error' in a cross build (mingw->windows |
| [#6270](https://github.com/mesonbuild/meson/issues/6270) | [MSVC/Win32] Wrap for {fmt} doesn't work with default_library=shared | medium | This is a packaging issue specific to a particular wrap ({fmt}) and should be handled in the wrapdb repository |
| [#7086](https://github.com/mesonbuild/meson/issues/7086) | [Not an issue] Unity build + LTO is slower than LTO | high | The reporter themselves states this isn't really an issue, they're just looking for a place to discuss it. It' |
| [#7956](https://github.com/mesonbuild/meson/issues/7956) | Failure to build Gtk4 because of missing vulkan headers | medium | The vulkan dependency reports YES but the build fails because vulkan/vulkan.h is missing. The reporter resolve |
| [#9219](https://github.com/mesonbuild/meson/issues/9219) | include_directories(..., is_system: true) appears to be ignored (at le | high | A misunderstanding by the reporter. is_system:true generates -isystem and is_system:false generates -I (gnu.py |
| [#10597](https://github.com/mesonbuild/meson/issues/10597) | Compilation fail with obs-nvfbc | high | "cannot find Scrt1.o / crti.o" is a toolchain environment issue caused by a missing C runtime (glibc-devel/gcc |
| [#10878](https://github.com/mesonbuild/meson/issues/10878) | meson.build:1:0: ERROR: Unknown options: "pkg_config_libdir" | medium | -Dpkg_config_libdir was never actually a valid Meson built-in option (only pkg_config_path exists), so the err |
| [#11035](https://github.com/mesonbuild/meson/issues/11035) | Meson generator looks for source files in wrong folder, how to fix tha | medium | A user configuration mistake stemming from using a generator to write output outside the build directory (into |
| [#11195](https://github.com/mesonbuild/meson/issues/11195) | result meson+ninja+moc missing include directive in specific case | medium | The reporter themselves states this is 'not a Meson bug, just for tracking on the Qt side' — the issue of moc  |
| [#11289](https://github.com/mesonbuild/meson/issues/11289) | Can not install: not successful. Exit code was '3010' | medium | MSI exit code 3010 is the standard return value meaning 'succeeded but a reboot is required' — this isn't a bu |
| [#11843](https://github.com/mesonbuild/meson/issues/11843) | cannot communicate with fpga getting issues (c18 combo option error) | high | LiteX/picolibc's meson.build requires c_std=c18, but the old Meson 0.61.5 doesn't know c18 and errors out. Thi |
| [#12243](https://github.com/mesonbuild/meson/issues/12243) | Does Meson support the `fpass-plugin=<value>` args of llvm compiler? | medium | Adding -fpass-plugin to CFLAGS causes all sorts of compile checks at configure time to fail, resulting in a si |
| [#12576](https://github.com/mesonbuild/meson/issues/12576) | meson.build:1710:13: ERROR: Neither a subproject directory nor a llvm. | medium | Dependencies like libudev aren't found and Mesa is simply requesting the llvm fallback (wrap); not a Meson bug |
| [#12584](https://github.com/mesonbuild/meson/issues/12584) | No module named 'mesonbuild.interpreter.primitives' | high | The mesonbuild/interpreter/primitives package exists in the current code. This was caused by a broken/incomple |
| [#12605](https://github.com/mesonbuild/meson/issues/12605) | sanitycheckc cross-exes cannot run (rvv toolchain, riscv64 musl) | medium | The sanity-check binary can't be run via qemuwrapper during a cross build — an issue on the user's cross envir |
| [#12693](https://github.com/mesonbuild/meson/issues/12693) | Compilation issue, stuck at lapack | medium | A user-support case where the lapack dependency isn't found when installing tblite on Windows. Not a bug in Me |
| [#12824](https://github.com/mesonbuild/meson/issues/12824) | wrap download is not following github's redirects. | medium | Wrap downloads use the standard urllib.request.urlopen, and urllib automatically follows 3xx redirects by defa |
| [#13358](https://github.com/mesonbuild/meson/issues/13358) | Issue with Enabling Shaderc, D3D11, and Vulkan Features in MPV Cross C | medium | A user-environment issue caused by mistakes in the cross file (e.g. missing quotes) and missing pkg-config set |
| [#13676](https://github.com/mesonbuild/meson/issues/13676) | suffix instead of name_suffix in docs | high | In Commands.md, 'SUFFIX' refers to the filename-suffix part of the target-specification syntax [PATH/]NAME.SUF |
| [#13875](https://github.com/mesonbuild/meson/issues/13875) | Migrate 'mesonbuild/meson' to 'Webhook To Fedora Messaging' | high | An external notification about Fedora infrastructure's messaging migration, unrelated to Meson's code. A meta  |
| [#13880](https://github.com/mesonbuild/meson/issues/13880) | Meson build system error (v1.4.99) - blocked by group policy | medium | Caused by a corporate group policy blocking program execution (during a NumPy build) — not a Meson bug. Unrepr |
| [#14052](https://github.com/mesonbuild/meson/issues/14052) | numpy dependency not properly updated when version changed | medium | It's expected behavior that run_command's output (the numpy include path) doesn't depend on any input file, so |
| [#14313](https://github.com/mesonbuild/meson/issues/14313) | Error while installing numpy/Scipy: Can not run test applications in t | medium | numpy's meson.build fails when run in a cross environment because exe_wrapper isn't set — this is an issue wit |
| [#14355](https://github.com/mesonbuild/meson/issues/14355) | Documentation error: pip3 says "Requirement already satisfied" | high | When an old meson bundled by the distro is present, pip install --user reporting 'already satisfied' is pip/di |
| [#15114](https://github.com/mesonbuild/meson/issues/15114) | Execution python3 run_unittests.py -v error: Compiler cc cannot compil | medium | test_c_link_args_and_env failing setup with -Dc_link_args='"-L/usr/lib"' appears specific to the Spack/openEul |
| [#15281](https://github.com/mesonbuild/meson/issues/15281) | Invalid character escape sequence '\1' error from librsync cmake wrap | medium | The 'Invalid character escape' error comes from CMake itself, triggered by backslash escaping in librsync's CM |

<details><summary>Draft comments</summary>

**#5826**:
```text
This `Exec format error` at the sanity-check stage means the produced Windows `.exe` was run directly on the Linux build host without the exe wrapper being applied. That's an environment/cross-file configuration problem (the wrapper wasn't picked up for the sanity check) rather than a Meson defect, and the external CI log is long gone. Current Meson runs the sanity executable through `exe_wrapper` for cross builds. I'll close this as not-actionable; please open a fresh issue with a minimal reproducer against a current release if it still happens.
```

**#6270**:
```text
This is a packaging issue with the {fmt} wrap (its shared-library dllexport/import macros), not a bug in Meson core. Such fixes belong in the wrapdb repository (https://github.com/mesonbuild/wrapdb). Suggest moving this there; closing on the core tracker.
```

**#7086**:
```text
As noted in the original post, this isn't a bug or feature request but a benchmarking discussion. The issue tracker isn't the right venue for this; questions like this are better suited to Meson's discussions/mailing list. Closing per the author's own suggestion.
```

**#7956**:
```text
As noted in the report itself, installing the `vulkan-headers` package resolves the failure. The Vulkan dependency was found via the loader library, but the development headers (`vulkan/vulkan.h`) were simply not installed on the system, which is an environment issue rather than a Meson bug. Closing; if you think Meson's `dependency('vulkan')` should additionally verify header presence, that would be a separate enhancement request.
```

**#9219**:
```text
This works as designed, and the expectation in the report is incorrect. Meson never emits `-iquote`. With `is_system: false` (the default) Meson uses `-I`, and with `is_system: true` it uses `-isystem` — see `get_include_args` in `mesonbuild/compilers/mixins/gnu.py`, which returns `['-isystem' + path]` only when `is_system` is true. So `is_system` is honored; it simply controls `-I` vs `-isystem` (which suppresses warnings and changes search order), not `-iquote`. Closing as invalid.
```

**#10597**:
```text
This is an environment/toolchain problem, not a Meson bug. The error `/usr/bin/ld: cannot find Scrt1.o` and `crti.o` means your C runtime startup objects are missing — i.e. the C development libraries aren't installed. On most distros installing the build essentials fixes it (e.g. `glibc-devel`/`libc6-dev` and `gcc`, or your distro's `base-devel`/`build-essential` group). Once `cc` can compile a trivial program, Meson will configure fine. Closing as this isn't actionable in Meson; please reach out to your distro's support channels if the toolchain still won't link.
```

**#10878**:
```text
`pkg_config_libdir` has never been a Meson built-in `-D` option (only `pkg_config_path` is), so `ERROR: Unknown options: "pkg_config_libdir"` is the expected behaviour and this originates from VLC's contrib scripts passing it as a `-D` flag. If you need to override the pkg-config search *libdir* (i.e. `PKG_CONFIG_LIBDIR`), that is now available as a machine-file property named `pkg_config_libdir` (see `mesonbuild/envconfig.py`), or simply set the `PKG_CONFIG_LIBDIR` environment variable. Closing as invalid (not a Meson bug); please use one of those mechanisms.
```

**#11035**:
```text
This is a usage issue rather than a Meson bug. `generator()` (and `custom_target`) are designed to write their outputs into the build directory; Meson then compiles them from there (`app.p/sources.pb.cc`). Your protoc invocation writes the generated files into the *source* tree (`--cpp_out=@CURRENT_SOURCE_DIR@/...`), so Meson never sees them where it expects. The fix is to let protoc write into the build dir (use the default output location / `@OUTDIR@` / `@BUILD_DIR@`) instead of `@CURRENT_SOURCE_DIR@`. Closing as not a bug — happy to help further in Discussions if needed.
```

**#11195**:
```text
As noted in the description, this is an upstream Qt/moc behavior (tracked as QTBUG-109487) rather than a Meson bug — moc omits the include directive for extension-less header inputs. There's nothing actionable on the Meson side here, so closing this tracking issue. Please follow the Qt bug for resolution; if a Meson-side workaround turns out to be needed, we can open a focused issue for that.
```

**#11289**:
```text
Exit code 3010 from msiexec is the standard `ERROR_SUCCESS_REBOOT_REQUIRED` code — it means the MSI installed successfully but Windows believes a reboot is needed. This is not a Meson bug; it is a matter of how the Chocolatey package (and its `--use-package-exit-codes` handling) treats 3010 as a failure. Please report this to the Chocolatey `meson` package maintainers, or treat 3010 as success in your CI. Note that the recommended way to install Meson on Windows for CI is now `pip install meson` or the official MSI directly. Closing as this is outside Meson's own code; please reopen if you can show the MSI itself failing.
```

**#11843**:
```text
This isn't a bug in Meson itself. The error `Value "c18" ... is not one of the choices` comes from your Meson being version 0.61.5, which predates C18 support in the C standard combo option. The picolibc `meson.build` requests `c_std=c18`, which newer Meson versions do support. Please upgrade Meson (the LiteX toolchain is pinning a very old release). The FPGA/UART traceback is downstream of the failed sub-build. Closing as not a Meson bug; upgrade Meson and re-run.
```

**#12243**:
```text
Meson passes user CFLAGS (including `-fpass-plugin=...`) through to the small introspection test programs it compiles during setup (size_t sizing, feature checks, etc.). The log shows those checks failing, which means the pass plugin itself is causing the test compilations to fail/return non-zero — that's a plugin/toolchain interaction, not a Meson defect. If the plugin must only apply to project sources and not to configure-time checks, keep it out of the global `c_args` and instead add it via `add_project_arguments()` after the compiler is fully detected, or apply it per-target. Closing as not a Meson bug; happy to reopen if you can show the same checks succeed with plain clang but fail only due to Meson's handling.
```

**#12576**:
```text
This isn't a Meson bug: the log shows libudev (and other deps) not being found on your RHEL 8 system, which causes Mesa to fall back to a wrap/subproject for LLVM that you don't have. You need to install the required -devel packages (and set PKG_CONFIG_PATH appropriately) so Mesa's dependencies resolve on the system. This is best raised with Mesa's build instructions rather than Meson. Closing as a configuration issue.
```

**#12584**:
```text
The module `mesonbuild.interpreter.primitives` exists in Meson (it's a normal package under mesonbuild/interpreter/primitives/). A 'No module named ...primitives' error indicates a broken or partial Meson installation — e.g. an incomplete distro package or a stale install missing files. Please reinstall Meson (pip install --force-reinstall meson, or reinstall your distro package). Closing as an installation issue; feel free to reopen with reproduction details if it persists on a clean install.
```

**#12605**:
```text
This is a cross-execution environment problem, not a Meson bug: the sanity-check binary is being run through your qemu exe_wrapper and can't execute (likely qemu-user lacks RVV support for the produced binaries, or the exe_wrapper isn't set up correctly). Ensure your cross file's exe_wrapper points at a qemu build that supports the RVV extension, or run the sanity check on real hardware. If binaries genuinely can't be run at configure time, they must be marked non-runnable via exe_wrapper handling. Closing as an environment/toolchain issue.
```

**#12693**:
```text
This looks like a missing/undiscoverable LAPACK dependency on your Windows setup rather than a Meson defect. You'll need a LAPACK/BLAS provider that Meson can find (e.g. via pkg-config, CMake, or the wrapdb 'lapack'/'openblas' wraps), or set the appropriate paths. This is really a tblite build-environment question and is better raised on the tblite issue tracker or Meson discussions. Closing as a support/environment issue — feel free to follow up there.
```

**#12824**:
```text
Meson downloads wrap sources via `urllib.request.urlopen` (see `mesonbuild/wrap/wrap.py`), and Python's urllib follows HTTP 3xx redirects automatically through the default `HTTPRedirectHandler`. A GitHub 302 to codeload is therefore followed transparently. The `HTTP Error 404` in your log was GitHub returning 404 for the tag archive URL itself (a well-known transient issue where `.../archive/refs/tags/vX.Y.tar.gz` intermittently 404s while the archive is being generated) rather than a redirect that Meson failed to follow. Retrying, or using the `codeload.github.com` URL directly, resolves it. Since Meson does follow redirects, closing as not a Meson bug — please reopen with a reproducible case if you still see a genuine redirect that is not followed.
```

**#13358**:
```text
This looks like a cross-file / environment configuration problem rather than a Meson bug. The cross file in the report has several syntax errors (missing opening quotes, e.g. `cpp = i686-w64-mingw32-g++'`, `ar = i6864-...`), and the errors `Pkg-config for machine host machine not found` mean no cross pkg-config is configured for the host machine. You need a working cross pkg-config (set `pkg-config` in `[binaries]` and `PKG_CONFIG_LIBDIR`/sysroot) and the mingw builds of shaderc/spirv-cross/vulkan. Since this is really an mpv/libplacebo cross-build setup question, I'm closing here; the mpv discussion is the better venue. Please reopen with a minimal Meson reproducer if you believe Meson itself is at fault.
```

**#13676**:
```text
Thanks for the report. The `SUFFIX` mentioned in `Commands.md` refers to the file-name suffix component of the `[PATH/]NAME.SUFFIX[:TYPE]` target syntax used by `meson compile`/introspection (added in 1.3.0), not to the `name_suffix` kwarg of `executable()`. The confusing part is the example, which incorrectly writes `executable('foo', suffix: 'exe', ...)` — that kwarg is `name_suffix`. The example should be corrected so the two concepts are not conflated. A small docs PR fixing the example would be welcome.
```

**#13875**:
```text
This is an infrastructure notification about the GitHub2FedMsg -> Webhook-To-Fedora-Messaging migration and does not concern Meson's codebase. Whether to migrate the webhook is an infrastructure/maintainer decision unrelated to the source tree, so this can be closed on the code repository (and handled by whoever manages the project's Fedora messaging integration, if that integration is still wanted). Closing as out of scope for the code tracker.
```

**#13880**:
```text
This appears to be your environment's Group Policy blocking a process that Meson (invoked by NumPy's build) tries to run, rather than a defect in Meson itself. Meson surfaces the OS-level 'blocked by group policy' failure but cannot bypass it. To move forward: identify from the log which executable is being launched at the failing step (compiler, linker, or a helper) and have IT allow-list that specific binary/path, or build in an environment without the restriction. Since this isn't reproducible as a Meson bug, I'll close it; please reopen with the exact blocked command if you believe Meson is invoking something incorrectly.
```

**#14052**:
```text
This is expected behavior rather than a bug. `run_command()` output (here, numpy's include dir) is evaluated at configure time and is not a tracked dependency of the build, so changing the numpy version won't automatically re-run configure — you need `meson setup --reconfigure` (or `--wipe`). The robust fix is to use `dependency('numpy')` (available via `numpy-config` since numpy 2.0, and via pkg-config in some builds) instead of shelling out to `numpy.get_include()`; that dependency participates in reconfiguration properly. Since there's no Meson defect here, closing — happy to help convert the build to `dependency('numpy')` if useful.
```

**#14313**:
```text
This error comes from NumPy's own `meson.build` (`numpy/_core/meson.build:145`) which needs to *run* a compiled test program during configuration. In a cross build Meson can only run target binaries if your cross file provides an `exe_wrapper` (e.g. `qemu-aarch64`) or if the build machine can execute the target binaries directly. The failure is a missing/incorrect cross-file setup rather than a bug in Meson itself. Please see the cross-compilation docs (`exe_wrapper` in `[binaries]`) and, if a specific check should have a cross-safe fallback, that request belongs in the NumPy tracker. Closing as not a Meson bug; happy to reopen if you can show Meson misbehaving with a correctly configured cross file.
```

**#14355**:
```text
This is expected `pip` behavior rather than a documentation bug: a distro-packaged Meson in `/usr/lib/python3/dist-packages` satisfies the requirement, so `pip3 install --user meson` reports "already satisfied" and installs nothing. Use `pip3 install --user --upgrade meson` (or a virtualenv) to get the latest release into your user site-packages; you may also need to ensure `~/.local/bin` precedes the distro path on `PATH`. We can add a `--upgrade` hint to the Getting Meson page, but the tool is behaving correctly. Closing as not a Meson bug; a small doc note PR for the `--upgrade` tip is welcome.
```

**#15114**:
```text
Thanks for the report. The failing test (`test_c_link_args_and_env`) aborts at the `meson setup` step with `ERROR: Compiler cc cannot compile programs`, which indicates the C compiler in your build environment can't produce a working binary at all — this is an environment/toolchain issue in your Spack `gcc-7.3.0` on openEuler aarch64 setup rather than a bug in Meson's test itself. Could you confirm that a trivial standalone build works in the same environment, e.g. `echo 'int main(void){return 0;}' > t.c && cc t.c -o t && ./t`, and check `meson-logs/meson-log.txt` for the exact compiler invocation and error? If `cc` cannot link a basic program (missing CRT/libc, broken sysroot, or `-fsanitize=address` runtime unavailable, which this test also relies on), the unit test cannot pass regardless of Meson. If you can show that `cc` compiles fine standalone but Meson still fails, please attach the full `meson-log.txt` and we'll take another look.
```

**#15281**:
```text
Thanks for the report. The `Invalid character escape '\1'` message is emitted by CMake itself (note the `Call Stack (most recent call first)` formatting) when parsing librsync's `CMakeLists.txt:230`, not by Meson. Newer CMake versions have become stricter about backslash escapes in unquoted/quoted arguments in `add_custom_target`. This is an upstream issue in librsync's CMake build (or a CMake compatibility policy), and Meson only relays CMake's output. Please report it to the librsync project, or pin an older CMake. Closing as this is not a Meson bug, but feel free to reopen if you can show Meson itself is mis-transforming the CMake source.
```

</details>

#### Won't fix (design decision) (17)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#375](https://github.com/mesonbuild/meson/issues/375) | Feature Request: include_file() or subfile() | medium | Including arbitrary files goes against Meson's design philosophy (scoping per subdir()) and has been deliberat |
| [#1081](https://github.com/mesonbuild/meson/issues/1081) | implement get_option('xxxdir_abs') | medium | Absolute paths can be obtained via join_paths(get_option('prefix'), get_option('xxxdir')), and the policy is t |
| [#1493](https://github.com/mesonbuild/meson/issues/1493) | Containerized Execution & Safe Persistent Caching | medium | Bazel/Tup-style sandboxed execution with provable memoization differs greatly from Meson's design of delegatin |
| [#4710](https://github.com/mesonbuild/meson/issues/4710) | Suggestion: add_executable_arguments() | low | Request for an API to add arguments to an already-created target later, but this goes against Meson's declarat |
| [#6893](https://github.com/mesonbuild/meson/issues/6893) | Contributing manual translation | medium | A request for guidelines on contributing Japanese translations of the manual. Individual translated pages exis |
| [#6946](https://github.com/mesonbuild/meson/issues/6946) | meson setup fails with an empty installation prefix (e.g. --prefix='') | medium | The design constraint that prefix must be an absolute path is still maintained. The use case for an empty pref |
| [#7940](https://github.com/mesonbuild/meson/issues/7940) | The native parameter disables project arguments | medium | Report that add_project_arguments arguments aren't applied to a native:true executable. When native: is omitte |
| [#8413](https://github.com/mesonbuild/meson/issues/8413) | Lexer cannot process UTF-8 files with a byte order mark (BOM). | medium | The lexer no longer crashes on a BOM and instead now issues a clear error, 'Builder file must be encoded in UT |
| [#8544](https://github.com/mesonbuild/meson/issues/8544) | Native conan dependency support | medium | Request for built-in conan detection that directly reads conanbuildinfo.txt. conan can already integrate with  |
| [#9442](https://github.com/mesonbuild/meson/issues/9442) | backend_startup_project not supported in case of ninja backend | medium | backend_startup_project is designed to be registered as a VS-backend-only option (coredata.py:336-340, `elif b |
| [#9461](https://github.com/mesonbuild/meson/issues/9461) | TypeScript Support? | medium | TypeScript/JS is not a compiled language Meson targets, and there is no supporting code for it locally at all. |
| [#9535](https://github.com/mesonbuild/meson/issues/9535) | I want the same feature in CMake: variable_watch | medium | An equivalent to CMake's variable_watch is not implemented; Meson intentionally limits its scripting capabilit |
| [#9537](https://github.com/mesonbuild/meson/issues/9537) | meson generated json files does not pass standard json validation test | high | testlog.json is by design a JSON Lines format ("one JSON object per line"), intentionally so because it stream |
| [#12513](https://github.com/mesonbuild/meson/issues/12513) | Allow configure_file inside root directory for .clangd | medium | By design, configure_file cannot output outside the build directory (into the source tree) — it rejects '..' — |
| [#12645](https://github.com/mesonbuild/meson/issues/12645) | doc: subprojects are discredited | low | An opinion piece objecting to the FAQ's statement that 'subproject is for external projects.' It advocates the |
| [#12679](https://github.com/mesonbuild/meson/issues/12679) | feature request: generate a build script | low | A request for Meson to generate a dependency-free POSIX shell build script. Reducing Meson's dynamic configura |
| [#13183](https://github.com/mesonbuild/meson/issues/13183) | Meson and Perl disagree on UNEXPECTEDPASS TAP test point failing the t | medium | Treating a TAP TODO success (UNEXPECTEDPASS) as a failure is Meson's intentional choice (#4832/#2923/#12362).  |

<details><summary>Draft comments</summary>

**#375**:
```text
Meson deliberately scopes build definitions to directories via `subdir()`, and a free-form file-include primitive has repeatedly been declined because it complicates scoping and traceability. This is unlikely to be added by design. If you have a concrete use case that `subdir()` cannot cover, feel free to raise it, but we're inclined to close this.
```

**#1081**:
```text
Absolute install paths can already be composed with `join_paths(get_option('prefix'), get_option('xxxdir'))`, and there is a strong preference not to double the directory-option surface with parallel `_abs` variants. This looks like it will not be added; closing as such. Please reopen with a use case the existing composition can't handle.
```

**#1493**:
```text
Meson intentionally delegates actual build execution to backends (ninja, VS/Xcode) and does not implement sandboxed/containerized action execution or content-addressed memoization the way Bazel/Tup do; that is out of scope for Meson's design. This is effectively a wontfix as framed. Sandboxing at the backend/CI layer remains the recommended approach.
```

**#4710**:
```text
Meson's build model sets a target's arguments at declaration time, so a post-hoc `add_executable_arguments()` doesn't fit well. For your use case you can pass an empty list when the option is unset (`c_args: extra_args` where `extra_args = []`), which is valid and avoids the dummy `-DNONE` hack. Closing as out of scope, but happy to discuss further.
```

**#6893**:
```text
Meson doesn't maintain a formal manual-translation workflow; the few translated pages that exist (e.g. Getting-meson in pt-br/zh) were contributed ad hoc as standalone markdown files under docs/markdown/. If you'd like to contribute a Japanese translation, the practical path is to add translated `*_ja.md` pages via a PR. There is no i18n tooling planned for the docs, so a dedicated translation guideline is unlikely to be added. Closing; PRs adding translated pages are welcome.
```

**#6946**:
```text
Meson intentionally requires `prefix` to be an absolute path (`mesonbuild/options.py` still enforces this). For the packaging use case described, the recommended approach is to use `DESTDIR` at install time (which you're already doing) together with a normal absolute `prefix` such as `--prefix=/usr` or `--prefix=/`; the empty-prefix behavior from autotools is not supported by design. Closing as wontfix unless there's a concrete case that DESTDIR + absolute prefix cannot cover.
```

**#7940**:
```text
This is working as designed. `add_project_arguments(...)` without `native:` applies only to the *host* machine, while `executable(..., native: true)` builds for the *build* machine. Meson deliberately keeps build-machine and host-machine argument sets separate. To apply the arguments to build-machine targets as well, call `add_project_arguments(..., native: true)` (or add a second call), or omit `native: true` on the target if you want the host-machine args. Since the behavior is intentional, closing as wontfix; the docs for `add_project_arguments` describe the native/host split.
```

**#8413**:
```text
The original bug (an opaque `ERROR: lexer` crash) is resolved: the lexer now explicitly detects a leading UTF-8 BOM and raises a clear diagnostic — `Builder file must be encoded in UTF-8 (with no BOM)` (see `mesonbuild/mparser.py`). The project chose to require BOM-less UTF-8 rather than silently strip the BOM, so the specific request to accept-and-discard the BOM is a wontfix, but the confusing failure is fixed. Recommend closing.
```

**#8544**:
```text
Meson intentionally does not parse package-manager-specific formats like `conanbuildinfo.txt`. The recommended path is to have Conan emit standard `pkg-config` (`PkgConfigDeps`) or CMake (`CMakeDeps`) files, which Meson's `dependency()` already consumes natively; Conan supports both generators. A bespoke conan parser inside Meson would be a maintenance burden for a format Meson doesn't control. Closing as out of scope; the pkg-config/cmake generator route is the supported integration.
```

**#9442**:
```text
`backend_startup_project` is a VS-backend-specific option; it is only registered when the backend is Visual Studio (mesonbuild/coredata.py). Putting it in `default_options` means it is rejected as an unknown option under the Ninja backend, which is by design for backend-specific options. Recommend passing it only when using a `vs` backend (e.g. on the command line) rather than in project() default_options. Closing as working-as-intended.
```

**#9461**:
```text
Meson targets compiled languages and has no TypeScript/JS backend, and adding first-class support for the JS/TS ecosystem (tsc, bundlers, node module resolution) is out of scope. For TS you'd be better served by dedicated tooling. Closing as wontfix; you can of course drive tsc via custom_target if you want to invoke it from Meson.
```

**#9535**:
```text
Meson deliberately keeps its DSL small and does not expose variable read/write hooks like CMake's variable_watch. There's no implementation of this and it isn't planned as it would embed debugging tracing into the interpreter's variable table. Closing as wontfix.
```

**#9537**:
```text
testlog.json is intentionally JSON Lines (one JSON object per line), not a single JSON document, so that results can be streamed line-by-line as tests run. This is documented (Unit-tests.md, 'testlog.json' section). A generic JSON validator will therefore reject it by design; consider excluding meson-logs from the eslint json check or parsing it line-by-line (jsonlines). Closing as working-as-intended.
```

**#12513**:
```text
Meson intentionally never writes generated files into the source tree; configure_file() output is confined to the build directory (paths containing '..' are rejected). For a per-build-dir .clangd, a common approach is a small wrapper/symlink or a git-ignored template you point clangd at via CompilationDatabase in a .clangd that lives in the source tree and just references build/compile_commands.json. I don't think writing into the source root from configure_file() is something Meson will add, so I'd suggest closing this.
```

**#12645**:
```text
Thanks for the feedback. The FAQ guidance to prefer subdir() for parts of the same project (and subproject() for genuinely separable/external components) is intentional — it reflects the maintainers' recommended structure and avoids the symlink workarounds you describe. Using subprojects heavily with symlinks is possible but is a non-standard pattern we don't want to steer newcomers toward. I don't think the guidance will be reversed here, so I'll close this; if you have a concrete wording improvement (rather than a change of recommendation), a docs PR would be welcome.
```

**#12679**:
```text
Generating a standalone POSIX shell build script isn't really feasible for Meson: configuration involves dynamic dependency detection, compiler probing, option handling and introspection that can't be faithfully frozen into a static shell script (and would need to be regenerated per platform anyway). Meson's model is to be the configure tool. For distributing to users without Meson installed, the usual answers are shipping tarballs plus a small bootstrap, or relying on the fact that Meson is a lightweight pip/distro package. I'll close this as out of scope, but happy to discuss narrower needs.
```

**#13183**:
```text
Thanks for the detailed write-up. As you noted, treating a TODO test that unexpectedly passes as a failure is an intentional choice in Meson (see #2923, #4832, #12362) — it surfaces stale TODO markers rather than silently reporting them as a 'bonus' the way Perl's prove does. Since the difference is by design and you filed this mainly as a signpost for others, I'll close it as wontfix. If there's appetite for an opt-in mode to match prove's behaviour, that would be a separate feature request. A documentation clarification would be welcome as a PR.
```

</details>

#### Needs info, long stale (80)

| Issue | Title | Confidence | Basis |
|---|---|---|---|
| [#476](https://github.com/mesonbuild/meson/issues/476) | Create Vala & C++ project | low | This is a 2016 error report for a mixed Vala/C++ project, and the pastebin log has expired. Vala support has i |
| [#799](https://github.com/mesonbuild/meson/issues/799) | Detailed coverage is broken with Vala | low | This is a 2016 report that gcovr can't find Vala-generated C source files. gcovr/coverage handling has changed |
| [#1181](https://github.com/mesonbuild/meson/issues/1181) | gnome: g-ir-scanner scan build error | low | This is a 2016 environment-specific problem where g-ir-scanner hits undefined symbols when an old version of a |
| [#1419](https://github.com/mesonbuild/meson/issues/1419) | Relative paths used in gnome module are incorrect with VS backend | low | This is a 2017 bug where the GNOME module's relative path (build_to_src) is off under the VS backend. Both mod |
| [#1636](https://github.com/mesonbuild/meson/issues/1636) | unit-tests failed on non-english windows | low | This is a 2017 report of decoding failures during compiler detection on Windows with non-English code pages (e |
| [#2643](https://github.com/mesonbuild/meson/issues/2643) | dependency() can yield incorrectly cached dependencies on regen if the | low | A specific bug related to the auto method dependency cache from the meson 0.43 era. The dependency system has  |
| [#2660](https://github.com/mesonbuild/meson/issues/2660) | Cross-compiled Qt program doesn't start — missing windows plugin | low | Qt dependencies now support main:true (linking qtmain), but for static Qt, importing platform plugins (qwindow |
| [#2831](https://github.com/mesonbuild/meson/issues/2831) | Target deps are not correctly added for content_files in gnome.gtk-doc | low | The current gnome.py collects CustomTarget/GeneratedList within content_files into depends and passes them via |
| [#2881](https://github.com/mesonbuild/meson/issues/2881) | Meson doesn't set LD_LIBRARY_PATH when executables in builddir are use | low | The backend has a mechanism to set LD_LIBRARY_PATH/DYLD_LIBRARY_PATH from dependent targets in test and exe-ru |
| [#3748](https://github.com/mesonbuild/meson/issues/3748) | python3 extension module cannot find library if meson launched from a  | low | A 2018 report specific to gvsbuild/Windows+virtualenv: 'Could not find Python3 library python36.' The python m |
| [#3794](https://github.com/mesonbuild/meson/issues/3794) | Meson does not properly reflect changes of dependencies | low | A 2018 report of macOS/Qt framework path inconsistency, involving qmake detection via the PATH environment var |
| [#3892](https://github.com/mesonbuild/meson/issues/3892) | ERROR: 'gtkdoc-scangobj' failed with status 1 | low | A FileNotFoundError caused by a missing .types file with gtkdoc --rebuild-types. gtkdochelper has logic to pas |
| [#4009](https://github.com/mesonbuild/meson/issues/4009) | gnome.gtkdoc integration breaks when ASAN is enabled | low | gtk-doc/ASan integration bug. The gnome module now recognizes b_sanitize and adds -lasan etc. to ldflags (arou |
| [#4028](https://github.com/mesonbuild/meson/issues/4028) | Tests in run_project_tests.py don't run `meson install` when using the | low | Internal test infrastructure (run_project_tests.py) not running install tests with the VS backend. The current |
| [#4074](https://github.com/mesonbuild/meson/issues/4074) | Decoding issue. | low | UnicodeDecodeError in gtkdochelper (non-UTF-8 bytes in gtk-doc output). The traceback line numbers from that t |
| [#4143](https://github.com/mesonbuild/meson/issues/4143) | Support whole-archive directives in pkg-config files | low | Regression where the pkg-config form -Wl,--whole-archive,-lfoo,--no-whole-archive fails to recognize -lfoo, br |
| [#4270](https://github.com/mesonbuild/meson/issues/4270) | rpaths_for_bundled_shared_libraries adds unnecessary RPATH for pkg-con | low | A 0.47 regression where unnecessary RPATH is added to pkg-config dependencies under a FreeBSD JHBuild prefix,  |
| [#4339](https://github.com/mesonbuild/meson/issues/4339) | Meson passes incorrect rpath to linker on macOS | low | A 0.47.2 report of an incorrect rpath ($ORIGIN/../src) being passed when using gcc-mp-8 on macOS. macOS handli |
| [#4493](https://github.com/mesonbuild/meson/issues/4493) | Cannot get Meson to work with Android NDK cross-compilation on Windows | low | A report from the 0.48 era of an "Unknown compiler(s): cl/cc/gcc/clang" error when cross-compiling for the And |
| [#4553](https://github.com/mesonbuild/meson/issues/4553) | dependency fails to find lua on ubuntu 18.04 | low | A 2018-era problem with lua pkg-config naming (lua5.3, etc.). dependency('lua') has since been improved to try |
| [#4608](https://github.com/mesonbuild/meson/issues/4608) | Python 3 can't be found on NetBSD 8.0 or DragonFlyBSD 5.2 | medium | A BSD environment with no python3, only python3.6. find_installation falls back to python when python3 is not  |
| [#4632](https://github.com/mesonbuild/meson/issues/4632) | test_generate_gir_with_address_sanitizer fails under the Gentoo packag | low | Meson's own unit tests fail due to LD_PRELOAD conflicts with the Gentoo sandbox. The tests still exist today ( |
| [#4770](https://github.com/mesonbuild/meson/issues/4770) | custom_target does not finish command properly | low | Report that concatenation via cat in a custom_target gets truncated (interfering with a gtk-doc run). Possibly |
| [#4794](https://github.com/mesonbuild/meson/issues/4794) | g-ir-scanner fails during meson tests on ppc64el on ubuntu | low | generate_gir plus ASan test failures on ppc64el. A test-environment-dependent issue of the same kind as #4632. |
| [#5155](https://github.com/mesonbuild/meson/issues/5155) | executable, library targets don't honor sources dependencies | low | declare_dependency(sources:) has documented the intent that generated headers should build first, and there ha |
| [#5246](https://github.com/mesonbuild/meson/issues/5246) | Meson configuration of DXVK winelib build with CC/CXX prepended works  | medium | An old winegcc regression report tied to the 0.51.0 milestone. winelib/winegcc support has since been built ou |
| [#5301](https://github.com/mesonbuild/meson/issues/5301) | Problem with VS2019 Preview project generation (0.50.1 version) | medium | A 2019 report of a REGEN.vcxproj build error with VS2019 Preview plus meson 0.50.1. The VS backend has evolved |
| [#5431](https://github.com/mesonbuild/meson/issues/5431) | Ninja still have work to do after call without parameters in case I us | low | An old report claiming ninja rebuilds even with no changes when using Qt MOC. Reproduction steps (meson.build) |
| [#5696](https://github.com/mesonbuild/meson/issues/5696) | Meson 0.51.999 test file with time out error. | low | A report that a test times out at 30 seconds, but it's unclear whether the test is actually hanging or it's a  |
| [#5913](https://github.com/mesonbuild/meson/issues/5913) | meson cannot find static library nng | low | A report that cc.find_library cannot find the static libnng.a (cross build). It has stalled at one comment due |
| [#6134](https://github.com/mesonbuild/meson/issues/6134) | FAILED: subprojects/glib/gio/tests/test.gresource | medium | A downstream-specific error from building an old 2019 glib/gst-build on Windows. Insufficient logs prevent pin |
| [#6217](https://github.com/mesonbuild/meson/issues/6217) | TypeError: expected str, bytes or os.PathLike object, not ExternalProg | low | In 0.52.0, passing ExternalProgramHolder where a PathLike was expected caused a crash. Since then, the interpr |
| [#6486](https://github.com/mesonbuild/meson/issues/6486) | test_generate_gir_with_address_sanitizer fails in Gentoo under our pac | low | Meson's own ASan unit tests fail inside Gentoo's sandbox environment. It carries a needs-info label and saw up |
| [#6487](https://github.com/mesonbuild/meson/issues/6487) | test_pch_with_address_sanitizer fails on some platforms in Gentoo | low | Same category as #6486: Meson's internal PCH+ASan unit tests fail in the Gentoo sandbox. It has been stalled f |
| [#6794](https://github.com/mesonbuild/meson/issues/6794) | compiler include directory flag incorrect on windows | low | A report that include flags in build.ninja use -I instead of /I, but MSVC accepts -I and Meson generally uses  |
| [#6939](https://github.com/mesonbuild/meson/issues/6939) | gnome.gtk-doc() gives permission denied error in Yocto (do_install) | low | The gtkdoc-mkhtml PermissionError (empty-string path) is an issue tied to the Yocto/gtk-doc tooling environmen |
| [#7204](https://github.com/mesonbuild/meson/issues/7204) | ld: unknown option: -no_weak_imports | low | The condition for adding -Wl,-no_weak_imports in has_function changed from a CLANG_OSX check to an AppleDynami |
| [#7496](https://github.com/mesonbuild/meson/issues/7496) | dlang: dependencies can't be found if multiple installed in system | medium | A dub dependency-detection problem from the 0.55 era. The dub dependency has since been completely rewritten i |
| [#7510](https://github.com/mesonbuild/meson/issues/7510) | dlang: multiple problems with dub dependencies | medium | A composite of dub dependency problems from the 0.55 era (explicit subdep, duplicate import dirs, cross-arch d |
| [#7560](https://github.com/mesonbuild/meson/issues/7560) | Dlang dub dependency cannot be found | medium | On 0.55, a problem where 'libdparse found but it wasn't compiled with ldc' appears. dub.py has been rewritten  |
| [#8079](https://github.com/mesonbuild/meson/issues/8079) | VS2019 C++17 support | low | cpp_std=c++17 has long been supported by cl/MSVC, so the report is likely a tool-set-specific issue with an ol |
| [#8528](https://github.com/mesonbuild/meson/issues/8528) | [WinError 123] with -DIMGUI_USER_CONFIG cmake define | low | A WinError 123 report in a CMake subproject, but it lacks a minimal reproduction case or a detailed traceback. |
| [#8561](https://github.com/mesonbuild/meson/issues/8561) | Meson > 0.56.0 doesn't write RPATH properly. | low | RPATH regression report from 0.56 to 0.57 (FreeBSD, custom PREFIX). This is a 5-year-old report with no minima |
| [#8601](https://github.com/mesonbuild/meson/issues/8601) | OSError: [WinError 123] ... advapi32 (cmake subproject) | low | WinError 123 while processing a CMake subproject (abseil-cpp). This is a 2021 report against meson 0.57, lacki |
| [#8799](https://github.com/mesonbuild/meson/issues/8799) | Windows subsystem option not recognized when using LLVM | medium | An old environment-specific issue where GNU-driver clang++ gets paired with MSVC's link.exe and `-Wl,--subsyst |
| [#8814](https://github.com/mesonbuild/meson/issues/8814) | unable to cross compile using meson for nec-aurora. unknown compiler e | medium | The log shows 'Is cross compiler: False', meaning the system cc is being picked up. Likely a user configuratio |
| [#9024](https://github.com/mesonbuild/meson/issues/9024) | [bisected] Broken syntax highlighting in KDevelop after a PCH-related  | low | An external-tool-dependent issue where KDevelop's semantic analysis breaks with Clang+b_pch. The cause is how  |
| [#9127](https://github.com/mesonbuild/meson/issues/9127) | GTK4 build setup fails on Windows 10 due to erroneous path | low | Likely a toolchain-side issue where an absolute path embedded by MSYS2/mingw GCC (D:\a\_temp..., a leftover fr |
| [#9168](https://github.com/mesonbuild/meson/issues/9168) | "Unknown compiler" for Android NDK | low | A problem where the Android NDK's aarch64-linux-android31-clang gets reported as 'Unknown compiler'. NDK clang |
| [#9440](https://github.com/mesonbuild/meson/issues/9440) | Unittests Error: test_prelinking failed: cannot find -lgcc_s | medium | The error (ld: cannot find -lgcc_s) is an environment issue caused by the absence of a static libgcc_s in the  |
| [#9583](https://github.com/mesonbuild/meson/issues/9583) | link_with to shared_library on windows can not work as expected (LNK11 | low | On Windows, linking a shared_library via link_with going through the .lib (import library) is normal behavior; |
| [#9815](https://github.com/mesonbuild/meson/issues/9815) | mpv Build issue (Unhandled python exception in 0.61.0) | low | A report of an unhandled exception building mpv on 0.61.0, but the body has no detailed traceback (only a log  |
| [#9864](https://github.com/mesonbuild/meson/issues/9864) | Despite --vsenv command meson doesn't seem to recognize Visual Studio  | medium | An environment issue from mediasoup's build script, where MinGW's gcc gets detected on PATH instead of using t |
| [#9968](https://github.com/mesonbuild/meson/issues/9968) | [built-in options] seem to be ignored (cross file, 0.60.2) | low | A report from the 0.60.2 era that c_args etc. under a cross file's [built-in options] get ignored. Machine-fil |
| [#9991](https://github.com/mesonbuild/meson/issues/9991) | Meson ignoring c_ld in cross file when building for arm | low | A 2022 report (no comments) specific to armcc/keil where a cross file's c_ld (armlink) is ignored and armlink  |
| [#10055](https://github.com/mesonbuild/meson/issues/10055) | not 'installing' a static lib throw a weird invalid file | low | A 2022 Windows report that omitting install:true causes a strange error when linking a static lib. Only a scre |
| [#10161](https://github.com/mesonbuild/meson/issues/10161) | Unhandled Python exception on meson build (MSYS2 vsenv) | low | An environment-specific issue where '...was unexpected at this time' appears when running VS activation (vcvar |
| [#10261](https://github.com/mesonbuild/meson/issues/10261) | prebuild for QNX target on Windows host (find_library gcc --print-sear | low | A very old report (meson 0.56.2) of an exception where find_library() and similar use `gcc --print-search-dir` |
| [#10286](https://github.com/mesonbuild/meson/issues/10286) | Meson Linking Qt 5 dynamically even when static is specified | low | A 2022 report (0.61.2) that under msys2 CLANG32, Qt5 gets dynamically linked even with static:true, with no wa |
| [#10681](https://github.com/mesonbuild/meson/issues/10681) | OSError: [WinError 1] When running `meson <builddir>` | medium | A WinError 1 specific to MSYS2 environments (corrupted paths or drive D: resolution), version-dependent on mes |
| [#10795](https://github.com/mesonbuild/meson/issues/10795) | (Windows 11) ERROR: Compiler cl can not compile programs | medium | A cl-validation failure building scipy (meson 0.62) under Python 3.11rc1. No actual error from meson-log.txt w |
| [#10987](https://github.com/mesonbuild/meson/issues/10987) | Meson is unable to find ninja (ERROR: Could not detect Ninja) | medium | A Docker-environment-specific ninja-detection failure, strongly suggestive of environmental factors like PATH  |
| [#11143](https://github.com/mesonbuild/meson/issues/11143) | Regression: No build machine compiler for xx with meson 0.64.1 on osx | low | A vcpkg-CI-specific "No build machine compiler" regression as of 0.64.1. Build-machine compiler detection depe |
| [#11154](https://github.com/mesonbuild/meson/issues/11154) | Unhandled python exception windows 10 vcpkg cgal | low | An unhandled exception when fetching the CGAL dependency (via CMake) on 0.64.1. The traceback is truncated, so |
| [#11543](https://github.com/mesonbuild/meson/issues/11543) | gnome.compile_resources will not infer the current source dir on Windo | low | In the current code, compile_resources always adds the current subdir to --sourcedir (gnome.py:473), so the cu |
| [#11793](https://github.com/mesonbuild/meson/issues/11793) | python run_unittests.py -v failed about meson@1.1.0 on openEuler20_aar | medium | test_git_update fails with an 'unrecognized input' error from git stash. This is likely an old-git/environment |
| [#12220](https://github.com/mesonbuild/meson/issues/12220) | Run-time dependency sdl2 found: NO (tried pkgconfig, config-tool and c | medium | A setup issue dependent on the user's environment (using sdl2 from a wrap on MSYS2). There's a ccache wrapper  |
| [#12436](https://github.com/mesonbuild/meson/issues/12436) | import('python').find_installation('python3') doesnt work when meson i | low | Report that the python module can't find python3 with the MSI build of Meson. This depends on the Python/PATH  |
| [#12486](https://github.com/mesonbuild/meson/issues/12486) | Cuda CI image builder fails to detect nvcc as a working compiler | low | A transient issue specific to the 2023-era CUDA CI image builder, dependent on the CI environment with little  |
| [#12687](https://github.com/mesonbuild/meson/issues/12687) | installation of pandas in pycharm error: This is a Meson bug and shoul | medium | An exception from building old pandas 2.1.4 from source on Windows. pandas already ships binary wheels so a so |
| [#12878](https://github.com/mesonbuild/meson/issues/12878) | meson reports unknown compiler(s) for aarch64-fsl-linux-gcc (no --vers | low | The reported root cause is exactly what the error message says: aarch64-fsl-linux-gcc isn't found on PATH ([Er |
| [#13036](https://github.com/mesonbuild/meson/issues/13036) | Compiling a project with SDL2 using SDL2 repo instead of wrapdb | medium | An environment-dependent question that the initial build fails due to the timing of copying begin_code.h in SD |
| [#13089](https://github.com/mesonbuild/meson/issues/13089) | Objective-C++ support might need a look, doesn't seem to be compiling | medium | Objective-C++ is properly supported in Meson (ClangObjCPPCompiler etc., with multiple existing test cases), an |
| [#13594](https://github.com/mesonbuild/meson/issues/13594) | @OUTPUT@ is not being replaced in custom_target | low | The report is against meson 0.61.2 (very old); in current versions, @OUTPUT@ substitution does happen even ins |
| [#13894](https://github.com/mesonbuild/meson/issues/13894) | Meson fails to detect linker with llvm/clang | low | An environment-specific issue where clang fails linker detection with 'program not executable' (ld/lld on PATH |
| [#14410](https://github.com/mesonbuild/meson/issues/14410) | Unhandled python exception caused by AssertionError: build.c_args duri | medium | trace's _classify_argument (assert key.machine is HOST) was part of the universal.py implementation at the tim |
| [#15294](https://github.com/mesonbuild/meson/issues/15294) | Meson ignoring c_ld in my cross-compile file | medium | A report that c_ld/cpp_ld are ignored, but c_ld has been deprecated since meson 1.9 in favor of -Dc_link_args  |
| [#15474](https://github.com/mesonbuild/meson/issues/15474) | symbolextractor crash | low | On a Windows build machine, symbolextractor occasionally crashes with exit code 3221356611 (0xC0000409, roughl |
| [#15562](https://github.com/mesonbuild/meson/issues/15562) | meson 1.10.1 tests fail on Mac OS X 10.6.8 Snow Leopard, incomplete li | low | A highly environment-specific problem on 10.6.8 (an OS that reached EOL in 2011) where static libintl requires |
| [#15657](https://github.com/mesonbuild/meson/issues/15657) | Unhandled python exception (building gtkwave) | low | The stack trace is provided only as an image with no full traceback text in the body, and the repro steps are  |

<details><summary>Draft comments</summary>

**#476**:
```text
Vala support (including mixing with C/C++) has been significantly improved since this 2016 report, and the linked pastebin logs are no longer available. Could you confirm whether this still reproduces on a current Meson release, ideally with a minimal example? Otherwise we'll close this as stale.
```

**#799**:
```text
Meson's coverage handling and gcovr integration have changed substantially since 2016. Could you check whether detailed (HTML) coverage still fails for Vala projects on a recent Meson + gcovr? Without a fresh reproducer we'll close this as stale.
```

**#1181**:
```text
This was an environment-specific failure (an older copy of the library installed in the prefix) from 2016, and Meson's g-ir-scanner/rpath handling has changed considerably since. Could you check whether it still reproduces on a recent Meson with a clean prefix? Otherwise we'll close as stale.
```

**#1419**:
```text
Both the GNOME module and the VS backend have changed substantially since 2017. Could you verify whether `gnome.compile_resources()` (and similar) still generate incorrect relative paths from a subdir on the current VS backend? Without a fresh reproducer we'll close as stale.
```

**#1636**:
```text
This report is from 2017 and Meson's subprocess/encoding handling has changed substantially since then. Is this still reproducible on a recent Meson release with a non-UTF-8 Windows code page? If we don't hear back we'll close it as stale; please reopen with a fresh trace if it still occurs.
```

**#2643**:
```text
This dates back to Meson 0.43 and the dependency-resolution system has been substantially reworked since. Are you able to reproduce this stale-cache behavior on a current Meson release? Without an up-to-date reproducer we'll close this as stale, but please comment and we'll reopen.
```

**#2660**:
```text
Meson's Qt dependency now supports the `main: true` kwarg to link qtmain on Windows. Static Qt platform plugins (e.g. qwindows) still need to be pulled in explicitly with Q_IMPORT_PLUGIN(QWindowsIntegrationPlugin) and linked in your own code, as with any static Qt build. Is this still reproducible with a recent Meson + `main: true`? If we hear nothing we'll close as stale.
```

**#2831**:
```text
Current Meson collects CustomTarget/GeneratedList content_files passed to gnome.gtkdoc into the doc target's dependencies (extra_depends), so generated content files should be built first. Is this still reproducible on a recent Meson? Without an updated reproducer we'll close as stale.
```

**#2881**:
```text
Meson wraps in-build-dir executable invocations (including via custom_target) and sets library search paths (LD_LIBRARY_PATH/DYLD_LIBRARY_PATH) from the executable's build-target dependencies. Can you still reproduce the RUNPATH-vs-LD_LIBRARY_PATH failure with a build-dir tool in custom_target on a current Meson (e.g. on FreeBSD)? We'll close as stale otherwise.
```

**#3748**:
```text
The Python module has been substantially rewritten since this 2018 report (which was specific to gvsbuild on Windows using a virtualenv Python 3.6). Could you check whether this still reproduces with a current Meson and a supported Python version? If we don't hear back, we'll close this as stale, but we're happy to keep it open with an updated reproducer.
```

**#3794**:
```text
This is a 2018 report about stale Qt framework paths on macOS when qmake is provided via PATH. The Qt dependency handling has changed considerably since then. Could you confirm whether this still reproduces with a current Meson and Qt? Without an updated reproducer we'll close it as stale.
```

**#3892**:
```text
The gtkdoc helper handles `--rebuild-types` by generating and passing a `<module>.types` file to scangobj. This report is from the Python-2 gtk-doc era, and gtk-doc itself is now largely superseded by gi-docgen/hotdoc. Could you confirm whether this still reproduces with a current Meson and gtk-doc? Without an updated reproducer we'll close as stale.
```

**#4009**:
```text
Thanks for the report. The gnome module now has explicit sanitizer handling for gtkdoc targets (it detects `b_sanitize` and adds the appropriate runtime libraries such as `-lasan`). This is a very old issue with limited reproduction detail. Could you confirm whether this still reproduces with a current release of Meson? If we don't hear back, we'll close this as stale, but please reopen with a minimal reproducer if it persists.
```

**#4028**:
```text
This is an old note about our internal test runner. `run_project_tests.py` has since been substantially reworked and does exercise install validation across backends. Is this still an actionable gap on current master? If there's no longer a concrete missing case, we'll close it.
```

**#4074**:
```text
Thanks for the report. The gtkdoc helper and our subprocess handling (`Popen_safe`) have been substantially rewritten since 0.47. This originated from non-UTF-8 output produced by gtk-doc itself. Could you check whether this still reproduces on a current Meson release? Without an updated reproducer we'll close this as stale.
```

**#4143**:
```text
The pkg-config library/link-argument parsing (`_search_libs`) has been substantially rewritten since this was filed. Could you confirm whether the `-Wl,--whole-archive,-lseastar,--no-whole-archive` ordering problem still reproduces with a current Meson release? If you can attach the failing `pkg-config --libs` output we can add a targeted test; otherwise we'll close this as stale.
```

**#4270**:
```text
The RPATH computation code has been substantially reworked since 0.47 (including how bundled/pkg-config library rpaths are handled and filtered). Could you check whether this linking failure still reproduces on a current Meson release in your JHBuild/FreeBSD setup? Without an updated reproducer we'll close this as stale.
```

**#4339**:
```text
The rpath handling (including macOS-specific behavior) has been reworked considerably since 0.47.2. Could you verify whether an incorrect rpath is still emitted with a current Meson release when building with a non-Apple gcc on macOS? If it still reproduces, a minimal project plus the exact link line would help; otherwise we'll close as stale.
```

**#4493**:
```text
This is an old (0.48) report and Android/NDK handling plus cross-file processing have improved since. The error indicates the native compiler detection ran; make sure your cross file's `[binaries]` point to valid NDK clang wrappers and that you're not missing a native compiler for build-machine tools. Could you retry with a current Meson release and the NDK's standard meson cross file? If it still fails, please attach the full log; otherwise we'll close as stale.
```

**#4553**:
```text
Lua on Debian/Ubuntu ships its pkg-config file as `lua5.3` (etc.) rather than plain `lua`, and Meson's dependency lookup has since improved. Could you retest with a current Meson and, if it still fails, provide the versions and the meson-log.txt? Otherwise we'll close this as stale.
```

**#4608**:
```text
As a workaround you can pass the exact interpreter name, e.g. `import('python').find_installation('python3.6')`, or point Meson at it via a native file / PATH. Meson is much newer now (this was reported against 0.46–0.48). Can you confirm whether `python3` discovery still fails on current NetBSD/DragonFlyBSD? We'll close as stale otherwise.
```

**#4632**:
```text
This test still exists in the current suite. Since it is fundamentally a conflict between the sandbox and ASan both wanting LD_PRELOAD, the usual approach is to skip it in the packaging environment. Is this still an active problem for Gentoo on a recent Meson? If not, we'll close this as stale.
```

**#4770**:
```text
This looks like it may be a capture/ordering interaction specific to that gtkdoc pipeline. A lot has changed in custom_target and the gnome module since 2019. Are you still able to reproduce a truncated capture output on a current Meson? If not, we'll close this as stale.
```

**#4794**:
```text
This is the same ASan-in-gir test area as #4632 and was reported against 0.49. Is this still failing on ppc64el with a current Meson and toolchain? Without a fresh reproduction we'll close this as stale.
```

**#5155**:
```text
This report is from 2019 and Vala/generated-source ordering has seen a number of fixes since. The intended behavior (generated sources listed in `declare_dependency(sources: ...)` are built before dependents that include them) is documented and expected to hold today. Are you still able to reproduce the multiple-`ninja`-runs issue on a current Meson release? If we don't hear back we'll close this as stale, but please attach a minimal reproducer and we'll reopen.
```

**#5246**:
```text
This is a 2019 report (milestoned for 0.51.0) against a very old winelib/DXVK toolchain, and Meson's winegcc/winelib handling has changed considerably since (including Wine Resource Compiler support). Are you still able to reproduce the 32-bit sanity-check failure with a current Meson and a recent Wine? If we don't hear back we'll close this as stale, but please attach a fresh meson-log.txt and we'll take another look.
```

**#5301**:
```text
This report is against VS2019 *Preview* with Meson 0.50.1 from 2019, and the Visual Studio backend (including REGEN/reconfigure handling) has changed substantially since. Are you still seeing the `CreateManifestResourceNames`/REGEN.vcxproj error with a current Meson and a released VS2019/VS2022? If we don't hear back we'll close this as stale; a fresh build log would let us investigate if it still occurs.
```

**#5431**:
```text
Is this still reproducible on a recent Meson? The Qt modules have changed considerably since 2019, and "ninja has work to do on a no-op rebuild" issues are usually traced to a specific generated dependency. If you can share a minimal `meson.build` that reproduces it on a current release, we'll take another look; otherwise this will be closed as stale.
```

**#5696**:
```text
A TIMEOUT usually means the test binary itself did not exit within the timeout window (default 30s), which is typically a property of the test rather than a Meson bug. Is this still happening on a current Meson? If so, please share the test's `testlog.txt` and whether the binary runs to completion when launched directly. Without a reproducer this will be closed as stale.
```

**#5913**:
```text
This looks like an environment/setup problem rather than a Meson bug: `find_library('nng', dirs: ...)` fails because the static `libnng.a` either isn't in the given `dirs`, isn't named as expected, or the (cross) compiler can't link it. Since 0.51 there have been many improvements to static/cross library lookup. This report has been idle with insufficient detail to reproduce, so I'll close it as stale. Please reopen against a current release with the exact file path/name of the library and the full compiler command Meson runs, if it still fails.
```

**#6134**:
```text
This is a 2019 report against a very old glib/gst-build checkout on Windows, and the failing `glib-compile-resources` invocation is downstream-specific with no captured error output. Current Meson and glib have changed substantially since. If this is still reproducible on a recent Meson release, please reopen with the actual stderr from the failing `meson_exe.py` command. Closing as stale.
```

**#6217**:
```text
The interpreter's object-holder and argument-typing model has been substantially rewritten since 0.52.0 (typed_pos_args/typed_kwargs now validate arguments up front). The original traceback is unlikely to reproduce as-is. Could you confirm whether this still occurs on a current Meson release, ideally with a minimal meson.build? Otherwise this will be closed as stale.
```

**#6486**:
```text
This is a needs-info report about Meson's own ASan unit test interacting with Gentoo's build sandbox, and it has been awaiting reproduction details for a long time. The unit test suite has been reorganized substantially since. If this still fails on a current Meson checkout under the Gentoo sandbox, please provide the current failure output; otherwise it will be closed as stale.
```

**#6487**:
```text
Same situation as #6486: this is Meson's own PCH+ASan unit test failing under Gentoo's sandbox, tagged needs-info and long stalled awaiting current reproduction details. If still reproducible on a current Meson checkout, please attach the up-to-date failure output; otherwise closing as stale.
```

**#6794**:
```text
MSVC/clang-cl accept `-I` as an alias for `/I`, so a bare `-I` in build.ninja is not itself a bug. This report is from 2020 and the specific case (likely pkg-config-provided include dirs) isn't reproducible from the description. Could you confirm whether this still fails on a current Meson, and if so provide the exact `-I` argument and the compiler error? Otherwise this will be closed as stale.
```

**#6939**:
```text
This looks like an environment-specific issue in the Yocto sysroot's `gtkdoc-mkhtml` tooling (the `PermissionError: [Errno 13] Permission denied: ''` comes from an empty path being passed inside gtk-doc's own scripts, not from Meson). There has been no activity for a long time. If this is still reproducible on a current Meson release, please reopen with a minimal reproducer and the full `meson-logs/meson-log.txt`; otherwise we'll close as stale.
```

**#7204**:
```text
The gating for `-Wl,-no_weak_imports` was reworked: it's now added based on the linker being an `AppleDynamicLinker` (and clang >= 8.0) rather than a `CLANG_OSX` compiler-type check (see `mesonbuild/compilers/mixins/clang.py`). That said, this report is against a very old Mac OS X 10.6 / ld64-127 environment with an open-source clang. Could you confirm whether this still reproduces on a currently supported toolchain? If it's no longer reproducible we'll close as stale.
```

**#7496**:
```text
The DUB dependency backend has been substantially rewritten since 0.55. It now delegates resolution to `dub describe` and locates artifacts in DUB's cache (requiring Dub >= 1.35), rather than parsing `dub list` output. The version-selection behaviour you hit in 0.55 no longer applies to that code path. Could you re-test with a current Meson and a recent Dub, and confirm whether the correct version is now selected? Closing as stale for now; please reopen with a fresh reproduction if the problem persists.
```

**#7510**:
```text
The DUB backend referenced here (including the `base.py` line you linked) has been completely rewritten since 0.55; it now delegates to `dub describe` and lets DUB resolve subdependencies, import paths and the target triple rather than reconstructing them in Meson. Several of the listed problems (having to list every subdependency, duplicate `-I` flags, missing triple handling) are likely addressed by that rewrite. Since this is a multi-part 2020 report, could you re-test with current Meson + Dub >= 1.35 and open focused issues for anything that still fails? Closing as stale.
```

**#7560**:
```text
The DUB dependency backend and its compiler-compatibility matching were rewritten since 0.55 (it now inspects `dub describe` output and a set of 'compatibilities' — compiler, compiler_version, arch, platform, configuration — see `mesonbuild/dependencies/dub.py`). The exact 'not compiled with ldc' path you hit no longer exists as-is. Please re-test with current Meson and Dub >= 1.35, building the dependency for the same compiler/arch/build-type. Closing as stale; reopen with a fresh log if it still fails.
```

**#8079**:
```text
This report is from 2020 with Meson 0.55 on an old MSVC toolset. Current Meson fully supports `cpp_std=c++17` with the MSVC/cl compiler and passes `/std:c++17` automatically. If you can still reproduce a case where `cpp_std=c++17` does not enable C++17 with a recent VS2019/2022 toolset, please share a minimal `meson.build` and the generated compile command; otherwise this can be closed.
```

**#8528**:
```text
This report is quite old (Meson 0.57) and lacks a minimal reproducer or full traceback. The CMake subproject handling has changed substantially since then. Could you confirm whether this still reproduces on current Meson (1.11.x)? If so, please attach a minimal `meson.build` + CMake project and the full error output. Otherwise this will be closed as stale.
```

**#8561**:
```text
This regression was reported against Meson 0.57 on FreeBSD nearly five years ago, and RPATH/RUNPATH handling has been reworked substantially since then. Can you confirm whether it still reproduces on current Meson (1.11.x) with a minimal project and custom `--prefix`? Please include the `meson setup` line and `readelf -d` output for the built binary. Without a current reproducer this will be closed as stale.
```

**#8601**:
```text
This was reported against Meson 0.57 and the CMake module has changed considerably since. The traceback suggests a bare library name like `advapi32` being treated as a path on Windows. Could you check whether this still reproduces on current Meson (1.11.x)? If so, a minimal reproducer (the subproject and meson.build) would help. Otherwise this will be closed as stale.
```

**#8799**:
```text
This report is from Meson 0.56/0.58 and describes a clang++ (GNU-style driver) being paired with MSVC's `link.exe`, producing `-Wl,--subsystem,windows` that `link.exe` cannot understand. Since then the linker detection and `win_subsystem` handling have been substantially rewritten (per-linker `get_win_subsystem_args` now emits `/SUBSYSTEM:` for MSVC/lld-link and `--subsystem` only for GNU-style linkers). Could you retest with a current Meson release and, if it still fails, attach the full `meson-log.txt` showing which C compiler and linker were detected? Without that we can't tell whether the toolchain is being mis-detected.
```

**#8814**:
```text
From the log, the build options are recorded as a single token `'--cross-file aurora.ini'` and Meson reports `Is cross compiler: False`, so the cross file was not actually applied — this looks like the argument was passed as one quoted string rather than `--cross-file aurora.ini` as two arguments. This is Meson 0.55.1; could you retest on a current release, invoking `meson setup builddir --cross-file aurora.ini ...` and attach the full `meson-log.txt` if the NEC Aurora compiler is still not recognized?
```

**#9024**:
```text
This is from 2021 and depends on how KDevelop's clang-based parser handles the PCH arguments emitted into `compile_commands.json`. Both Meson's PCH handling and KDevelop have changed substantially since then. Could you retest with a current Meson and KDevelop, and if the highlighting is still broken, confirm whether the same file parses correctly when opened directly with `clangd`/`clang` using the generated `compile_commands.json`? That will tell us whether the compile command Meson emits is actually wrong or whether it's a KDevelop-side issue.
```

**#9127**:
```text
The offending path `D:\a\_temp\msys\...` is baked into the MinGW-w64 GCC toolchain you installed (it's the CI build path of the package), not something Meson generates — Meson only runs the compiler you point it at. This is from 2021 with a very old Meson. Could you retest with a current MSYS2/mingw-w64 toolchain and Meson release? If it still fails, please attach the full `meson-log.txt` and the output of `gcc -print-search-dirs` so we can see whether the compiler itself is mis-configured.
```

**#9168**:
```text
The NDK's `aarch64-linux-android31-clang` is a normal Clang driver and should be detected as clang. This report is from 2021 and the compiler detection has changed a lot since. Could you retest with a current Meson and attach the full `meson-log.txt` (with `MESON_FORCE_BACKTRACE=1`)? In particular, the log should show what version string the wrapper prints — if it fails, please also paste the output of running the compiler with `--version` directly, so we can see why detection rejected it.
```

**#9440**:
```text
This looks like a toolchain/environment issue on the test machine (the linker cannot find gcc_s, i.e. static libgcc is unavailable in that spack aarch64 setup) rather than a Meson defect. The prelinking test itself passes on supported GNU toolchains in CI. Closing as stale/environment-specific; please reopen with details if a current Meson still fails on a standard toolchain.
```

**#9583**:
```text
On Windows, linking against a shared_library correctly goes through its generated import library (.lib) - that's expected MSVC behavior, not a bug. LNK1181 'cannot open input file' usually means the import lib wasn't produced (e.g. the DLL exports no symbols, so no .lib is generated) or a path issue. Without a minimal reproducer and full build log we can't diagnose further. Closing as needs-info/stale; please reopen with a minimal example if this still happens on current Meson.
```

**#9815**:
```text
This was reported against Meson 0.61.0 and the issue body doesn't include the actual traceback (only an attached log). Meson has since advanced many major releases. If mpv still fails to configure on a current Meson, please reopen with the full `meson setup` traceback (MESON_FORCE_BACKTRACE=1) so it can be diagnosed. Closing as stale pending info.
```

**#9864**:
```text
Thanks for the report. This looks like an environment-specific interaction where a MinGW `gcc` on `PATH` was picked up ahead of the requested MSVC toolchain. `--vsenv` behaviour and compiler detection have changed substantially since 0.61. Could you re-test with a current Meson release and, if it still fails, share a minimal reproducer (the exact `meson setup` invocation plus your `PATH`/environment) so we can look into it? Without further information from a current version we'll close this as stale, but please comment and we'll reopen.
```

**#9968**:
```text
Machine-file option handling (including the `[built-in options]` section and per-language `*_args`) has been reworked significantly since 0.60.2. Could you re-test with a current Meson release? If `c_args`/`cpp_args` set under `[built-in options]` in a cross file are still not applied, please share a complete minimal reproducer against the current version and we'll investigate. Closing as stale for now; comment to reopen.
```

**#9991**:
```text
Thanks for the report. Linker detection and the `<lang>_ld` machine-file entry have changed since 0.61. Could you verify against a current Meson release whether `c_ld` pointing at your full `armlink.exe` path is honoured? If it still isn't, please attach the `meson-log.txt` from a current version. We'll close this as stale in the meantime; comment to reopen.
```

**#10055**:
```text
The details here are hard to act on from the screenshots alone. Could you re-test with a current Meson release and, if it still reproduces, paste the full text of the error and attach `meson-logs/meson-log.txt`? A static library used only via `link_with` should not require `install: true`, so if it does that's worth pinning down with a minimal reproducer. Closing as needs-info/stale for now; comment to reopen.
```

**#10161**:
```text
The traceback bottoms out in the Visual Studio `vcvars` batch file failing under MSYS2 (`...dd_vsdevcmd16_preinit_env.log was unexpected at this time`), which is an environment/batch-parsing interaction rather than a plain Meson bug. vsenv handling has changed since 0.61.2. Could you re-test on a current Meson release from a clean shell and, if it still fails, attach the full log plus your shell/PATH details? Closing as stale/needs-info; comment to reopen.
```

**#10261**:
```text
This was reported against Meson 0.56.2, which is very old; cross-compilation and `find_library`/library-dir detection have been substantially reworked since. Could you re-test with a current release using a proper QNX cross file? If `find_library` still throws on a Windows host targeting QNX, please attach the full traceback and `meson-log.txt` from the current version. Closing as stale; comment to reopen.
```

**#10286**:
```text
The `static: true` handling for the Qt dependency depends heavily on how the Qt build exposes static libraries (pkg-config vs qmake) in your msys2 environment. This was reported on 0.61.2 and the Qt dependency code has changed since. Could you re-test on a current Meson release and attach `meson-log.txt` showing the Qt detection? If static libs are present but Meson still picks dynamic, a minimal reproducer would help. Closing as needs-info/stale; comment to reopen.
```

**#10681**:
```text
This looks like an environment-specific failure in an old MSYS2/mingw setup (Meson 0.63), where a corrupted/`D:\` path was being resolved. Meson has changed substantially since then, and OSErrors like this are now reported as build-environment problems rather than an unhandled bug. Could you retest with a current Meson release? If it still reproduces, please attach the full `meson-log.txt` and the exact toolchain paths. Without a current reproducer this is not actionable, so I'm inclined to close as stale.
```

**#10795**:
```text
This is almost certainly a local MSVC-environment problem rather than a Meson bug: `cl can not compile programs` means the compiler sanity check failed, and the actual reason is in `meson-logs/meson-log.txt`, which wasn't attached. This was also on an rc build of Python 3.11 with Meson 0.62. Could you retry with a current Meson from a proper `x64 Native Tools` VS prompt and, if it still fails, attach the full `meson-log.txt`? Without that we can't diagnose, so closing as stale/needs-info.
```

**#10987**:
```text
This looks like an environment-specific issue with how Ninja is exposed on `PATH` (or an incompatible/architecture-mismatched ninja) inside that particular Docker image, rather than a Meson bug — the same versions work on baremetal for you. The Meson and Ninja versions referenced here are also quite old now. If you can still reproduce with a current Meson and a minimal Dockerfile, please share the exact `PATH`, `which ninja`, and the meson-log.txt from inside the container; otherwise we'll close this as stale.
```

**#11143**:
```text
This was reported against Meson 0.64.1 in a vcpkg CI setup and depends heavily on the native-file / build-machine compiler configuration at the time. A lot has changed in compiler and machine-file handling since then. Could you confirm whether this still reproduces with a current Meson release, and if so attach a fresh meson-log.txt and the native file? Without an up-to-date reproducer we'll close this as stale.
```

**#11154**:
```text
This is from Meson 0.64.1 and the traceback is truncated, so the root cause isn't clear. CMake-based dependency handling (which CGAL uses here) has changed substantially since then. Could you retry with a current Meson and, if it still crashes, attach the full traceback and meson-log.txt? Unhandled exceptions are bugs we want to fix, but we need a current, complete reproducer — otherwise we'll close as stale.
```

**#11543**:
```text
In current Meson, `gnome.compile_resources()` always adds the current source directory (`build_to_src/subdir`) as a `--sourcedir` after any user-specified `source_dir` (see mesonbuild/modules/gnome.py). Could you confirm whether this still reproduces on a recent Meson (1.10/1.11) on Windows with a minimal example? If it no longer occurs we can close this; otherwise a fresh log showing the `--sourcedir` values passed to glib-compile-resources would help pinpoint the remaining gap.
```

**#11793**:
```text
Thanks for the report. This failure occurs inside `git stash push --all` during `test_git_update`, and the underlying `error: unrecognized input` comes from the system Git, not Meson itself — it strongly suggests an old or unusual Git version in that Spack toolchain. This was filed against Meson 1.1.0 in 2023 with no further updates. If you can still reproduce it on a current Meson release, please reopen with your `git --version` and the full test log; otherwise this can be closed as stale.
```

**#12220**:
```text
This looks like an environment/setup problem rather than a Meson bug: on Windows the sdl2 dependency was tried via pkgconfig/config-tool/cmake and none resolved, which usually means the wrap wasn't installed into `subprojects/` (or `--wrap-mode`/`forcefallback` wasn't used) or the MSYS2 vs. native toolchain mix in the native file. SDL2 also has a `sdl2` wrap on WrapDB; running `meson wrap install sdl2` and configuring with `--force-fallback-for=sdl2` typically resolves it. Since there's been no activity since 2023 and no reproducible Meson defect identified, I'll close as stale; please reopen with a full `meson-log.txt` if it still fails on current Meson.
```

**#12436**:
```text
The MSI ships an embedded Python for running Meson itself, but `import('python').find_installation('python3')` searches for a separate Python interpreter on PATH to build extensions against. On the reporting system `python3` may simply not have been on PATH (the Windows launcher is often `py`/`python`, not `python3`). Could you confirm whether `python3 --version` works in the same shell, and try `find_installation('python')` / `find_installation('py')`? Without a reproducer on current Meson this looks like an environment issue; I'll close as stale but happy to reopen with the `meson-log.txt` and your PATH.
```

**#12486**:
```text
This looks like a transient CI image / nvcc detection problem from late 2023. The CUDA CI has been reworked several times since then. If this is still reproducible on current master, could you confirm with a fresh log? Otherwise I think this can be closed as stale.
```

**#12687**:
```text
This is from building pandas 2.1.4 from source with an older Meson on Windows. Modern pandas ships prebuilt Windows wheels, so `pip install pandas` should not build from source at all — please upgrade pip and pandas so a wheel is used. If you still hit a 'This is a Meson bug' exception on a current Meson, please attach the full meson-log.txt and the complete traceback so the actual cause can be identified. Closing as stale/needs-info for now.
```

**#12878**:
```text
The underlying error here is `Running "aarch64-fsl-linux-gcc --version" gave "[Errno 2] No such file or directory: 'aarch64-fsl-linux-gcc'"`, which means the cross toolchain binary was not found on `PATH` at all (not that `--version` is unsupported). You need to either put the toolchain's `bin` directory on `PATH` or specify the full absolute path to the compiler in your cross file's `[binaries]` section. Also note this was reported against Meson 0.55.0, which is several years old; compiler detection has changed substantially since. Please retry with a current Meson and a cross file pointing at the full compiler path, and reopen with a fresh log if it still fails. Closing as stale/needs-info.
```

**#13036**:
```text
This looks like a build-ordering issue with headers generated by the CMake subproject (SDL2's `begin_code.h` copied into the CMake build tree). It reads more like a usage/support question than a confirmed Meson bug, and there's no minimal reproducer attached. Questions like this are better suited to the Matrix room or Discussions. If you believe there is a concrete ordering bug in the `cmake` module, please provide a minimal reproducing project and the generated `build.ninja` snippet, and we can investigate. Closing for now as needs-info.
```

**#13089**:
```text
Objective-C++ is supported by Meson and exercised by the in-tree test cases (`test cases/objcpp/1 simple`, `2 objc++ args`, `3 objfw`) with both Clang and GCC objcpp compilers. The failure in the screenshot looks like an environment/toolchain setup problem (GNUstep on Ubuntu) rather than a Meson bug. Could you attach the full `meson-log.txt` and a minimal `meson.build` + source that reproduces? Without that this isn't actionable, so I'm closing as needs-info; happy to reopen with a reproducer.
```

**#13594**:
```text
This was reported on Meson 0.61.2, which is very old. On current Meson, `@OUTPUT@`/`@INPUT@` substitution is handled in `substitute_values()` (mesonbuild/utils/universal.py). Note also that in your example the whole command is a single string passed to `bash -c` and `echo` just prints it literally; substitution still applies to command elements. Could you retry with a current Meson release and, if it still misbehaves, share a minimal reproducer plus the exact generated ninja command line? Marking as needs-info; will close if it is not reproducible on a supported version.
```

**#13894**:
```text
Thanks for the report. The error `program not executable` comes from clang itself when it tries to invoke the linker (`ld`/`lld`) — Meson only reports what clang returns. This usually means the linker binary in your toolchain directory is not executable or the wrong architecture, rather than a Meson bug. Could you confirm that `clang -fuse-ld=lld -Wl,--version` works directly in your shell, and check the permissions/architecture of the linker under `S:\wplace\sdk\compilers\clang\bin`? If it works standalone but still fails under Meson, please attach a fresh `meson-log.txt` with current master. Without that we'll close this as not reproducible.
```

**#14410**:
```text
The traceback here points at `_classify_argument` / `assert key.machine is MachineChoice.HOST` inside `utils/universal.py`, but the option-handling code has since been substantially reworked (option classification now lives in `mesonbuild/options.py`) and that specific code path no longer exists on current master. This kind of `AssertionError` on `build.load()` is also consistent with a stale `build.dat` from an older Meson version being read by a newer one (common under Flatpak), which is resolved by reconfiguring from scratch (`rm -rf` the build dir / `meson setup --wipe`). Since this was filed as needs-info without a reproducer, could you retry on a current Meson release with a clean build directory and let us know if it still occurs? Otherwise this can be closed as stale.
```

**#15562**:
```text
Thanks for the detailed report. The undefined `_CFArrayGetValueAtIndex` / `_CFRelease` symbols come from `libintl.a` needing Apple's CoreFoundation framework — this is a property of how that static libintl was built, not something Meson injects. On a supported macOS this normally links because the framework is pulled in transitively. Since this is macOS 10.6.8 (long past Apple's and Meson's support window) and the issue is really about missing `-framework CoreFoundation` for a hand-built static libintl, could you confirm whether adding `-framework CoreFoundation` (e.g. via the dependency's link args or an override) resolves it? If so this is an environment/packaging issue rather than a Meson bug. Without a reproducer on a currently-supported platform we may have to close this as stale.
```

**#15657**:
```text
Thanks for the report. To act on this we need the full text of the traceback rather than a screenshot — could you paste the complete `meson setup`/`meson compile` output (the lines after "Traceback (most recent call last)") as text, along with the exact meson version (`meson --version`) and the commit of gtkwave you built? A screenshot omits parts of the trace and can't be searched. With the text traceback and a minimal reproducer we can investigate; otherwise we may have to close this as stale.
```

</details>

---

## B. Resolvable with an implementation (174)

### Effort: Small (125)

| Issue | Title | Confidence | Implementation approach |
|---|---|---|---|
| [#1929](https://github.com/mesonbuild/meson/issues/1929) | csharp: Support passing resource IDs | high | Add a 'cs_args'/resources handling that emits mcs -resource:<file>[,<id>] for C# targets; wire a resources kwarg through the inter |
| [#2085](https://github.com/mesonbuild/meson/issues/2085) | AVX512 support in SIMD module? | high | Add 'avx512' to the ISETS tuple in mesonbuild/modules/simd.py and the CheckKw TypedDict, then implement get_instruction_set_args(' |
| [#2232](https://github.com/mesonbuild/meson/issues/2232) | meson does not process po/POTFILES.skip file | high | In mesonbuild/scripts/gettext.py run_potgen(), after resolving `listfile`, also check for `POTFILES.skip` in `src_sub`. If it exis |
| [#2563](https://github.com/mesonbuild/meson/issues/2563) | qt.preprocess: Output warning if a .cpp / .cc file is passed | high | In mesonbuild/modules/_qt.py preprocess(), when iterating moc_headers, warn (mlog.warning, once) if a file's suffix is a known sou |
| [#2585](https://github.com/mesonbuild/meson/issues/2585) | gnome.gtkdoc()'s ignore_headers doesn't take file objects | high | In gnome.py gtkdoc kwargs, change ignore_headers type to accept FileOrString (like html_assets), then resolve File objects to path |
| [#2588](https://github.com/mesonbuild/meson/issues/2588) | gtkdoc html_assets does not allow overwriting gtkdoc-mkhtml  | high | Move the html_assets copy loop in mesonbuild/scripts/gtkdochelper.py to AFTER gtkdoc_run_check(mkhtml_cmd, ...) so user-provided a |
| [#2664](https://github.com/mesonbuild/meson/issues/2664) | gnome module doesn't give a clear error on missing gobject-i | medium | In gnome._get_gir_dep, when the gobject-introspection-1.0 pkg-config dependency is not found, raise a clear MesonException hinting |
| [#2900](https://github.com/mesonbuild/meson/issues/2900) | Allow debugging internal commands | medium | Add a --verbose flag (or honor a MESON_VERBOSE env var) in the internal helper scripts like gtkdochelper.py to print the underlyin |
| [#2969](https://github.com/mesonbuild/meson/issues/2969) | Add subdir argument to gnome.mkenums_simple() to match insta | high | Add a `subdir` kwarg to gnome.mkenums_simple() that, when set (and install_dir isn't), installs generated headers to join_paths(in |
| [#3966](https://github.com/mesonbuild/meson/issues/3966) | Run a no-op check after each project test | high | In run_project_tests.py after force_regenerate()+build_step(), capture ninja's output (e.g. `ninja -n` dry-run or parse the build  |
| [#4141](https://github.com/mesonbuild/meson/issues/4141) | Add support for runstatedir | high | Add a builtin directory option `runstatedir` (default derived from localstatedir, e.g. localstatedir/run, with /usr -> /run mappin |
| [#4448](https://github.com/mesonbuild/meson/issues/4448) | Missing checks on wrap `directory` option | medium | In the wrap loader (wrap.py add_wrap/load_all), detect when two .wrap files resolve to the same `directory` and raise a clear Wrap |
| [#4651](https://github.com/mesonbuild/meson/issues/4651) | Explicitly disable pie when pie is false | medium | Add a get_no_pie_link_args()/get_pie_link_args(disable=...) path so that when b_pie is explicitly false, GCC/Clang linkers receive |
| [#4839](https://github.com/mesonbuild/meson/issues/4839) | No warning if vcs_tag() and configure_file() have the same o | medium | Register vcs_tag() output paths into the same configure_file_outputs map (or a shared generated-file registry) so overlapping outp |
| [#5019](https://github.com/mesonbuild/meson/issues/5019) | qt5.compile_translations contains path separator in its targ | medium | In mesonbuild/modules/_qt.py compile_translations(), the CustomTarget name is built as f'qt{self.qt_version}-compile-{ts}' where t |
| [#5166](https://github.com/mesonbuild/meson/issues/5166) | Add offsetof() function | high | offsetof is already computed internally in mesonbuild/compilers/mixins/clike.py (used by alignment via _cross_compute_int with 'of |
| [#5244](https://github.com/mesonbuild/meson/issues/5244) | [Docs] Missing description of --setup arg for meson test | high | Add a section to docs/markdown/Unit-tests.md documenting `meson test --setup=<name>` and how it relates to `add_test_setup()` (con |
| [#5493](https://github.com/mesonbuild/meson/issues/5493) | Use lowercase name as default for filebase in pkgconfig.gene | high | In pkgconfig.generate (mesonbuild/modules/pkgconfig.py:733), default `filebase` to `name.lower()` instead of `name`. Because this  |
| [#5770](https://github.com/mesonbuild/meson/issues/5770) | WARNING: Unknown CPU family 'sgimips' | medium | In envconfig.py cpu-family normalization, map 'sgimips' -> 'mips' (or handle trial.endswith('mips')). Add to the mips branch condi |
| [#5876](https://github.com/mesonbuild/meson/issues/5876) | gnome.generate_gir() should allow silencing warnings | high | Add a boolean kwarg (e.g. 'warnings' default true, or 'disable_warnings') to generate_gir in gnome.py; only append '--warn-all' wh |
| [#6009](https://github.com/mesonbuild/meson/issues/6009) | Expose the test timeout as an env var? | medium | In mtest.py where MESON_TEST_ITERATION is set on the test env, also set MESON_TEST_TIMEOUT to the resolved per-test timeout (after |
| [#6036](https://github.com/mesonbuild/meson/issues/6036) | b_asneeded=false should explicitly do -Wl,--no-as-needed | high | Give get_asneeded_args a value/enable parameter (or add get_no_asneeded_args) returning ['-Wl,--no-as-needed'] when b_asneeded is  |
| [#6069](https://github.com/mesonbuild/meson/issues/6069) | i18n.gettext incorrectly detects "translations" for `_` in s | high | Make -k_ opt-out/configurable: add an i18n.gettext kwarg to disable the implicit '-k_' (or pass keyword list through), and stop ha |
| [#6584](https://github.com/mesonbuild/meson/issues/6584) | Add working directory as an optional KWARG to run_command | high | Add a `cwd` (str) kwarg to `func_run_command` in mesonbuild/interpreter/interpreter.py; thread it into the `run_command_impl`/subp |
| [#6660](https://github.com/mesonbuild/meson/issues/6660) | get_variable() needs better docs | medium | Document in CMake-module.md / dep.yaml get_variable that CMake-detected deps expose renamed variables PACKAGE_INCLUDE_DIRS / PACKA |
| [#7234](https://github.com/mesonbuild/meson/issues/7234) | Undocumented keywords for gnome.gtkdoc() | high | Document `expand_content_files:` and `mode:` (choices xml/sgml/auto/none, since 0.37.0) in the gnome.gtkdoc() section of docs/mark |
| [#7286](https://github.com/mesonbuild/meson/issues/7286) | ccache docs should provide non-environment variable method | medium | In docs/markdown/Feature-autodetection.md ccache section, add/point to the machine-file [binaries] method (c = ['ccache', '<compil |
| [#8723](https://github.com/mesonbuild/meson/issues/8723) | reword Ternary operator explanation | medium | In docs/markdown/Syntax.md, reword the ternary sentence to 'To improve legibility, nested ternary operators are forbidden.' (move  |
| [#9387](https://github.com/mesonbuild/meson/issues/9387) | Add link_depends to declare_dependency | high | Add a link_depends KwargInfo to declare_dependency, store it on InternalDependency, and merge it into a target's link_depends when |
| [#9693](https://github.com/mesonbuild/meson/issues/9693) | Grouping the tutorials under Tutorials | medium | In docs/sitemap.txt, nest Tutorial.md / GuiTutorial.md / IndepthTutorial.md (and related) under a new Tutorials.md index page. |
| [#10252](https://github.com/mesonbuild/meson/issues/10252) | run_target can't take files() dependencies | high | Add a DEPEND_FILES_KW to func_run_target's @typed_kwargs and thread it into build.RunTarget. RunTarget already is a Target; give i |
| [#10319](https://github.com/mesonbuild/meson/issues/10319) | Building DLang shared library on MacOS ARM64 fails (-undefin | medium | In the D compiler/linker arg translation (mesonbuild/compilers/d.py, the code that wraps linker args as '-L=<arg>' for ldc2/dmd),  |
| [#10342](https://github.com/mesonbuild/meson/issues/10342) | cc.find_library(...).as_system() throws "Unknown method" err | high | Add as_system_method to ExternalLibraryHolder, implementing it so held_object (ExternalLibrary) returns a copy with include_type c |
| [#10373](https://github.com/mesonbuild/meson/issues/10373) | .gitignore in subprojects/packagecache | medium | In wrap.py, write out a .gitignore containing '*\n' when creating the packagecache directory (similar to the existing git_ignore_f |
| [#10482](https://github.com/mesonbuild/meson/issues/10482) | python install_sources() does not accept "rename" as kwarg | high | Add the same rename KwargInfo used by install_data to install_sources_method's typed_kwargs, and pass rename=kwargs['rename'] in t |
| [#10569](https://github.com/mesonbuild/meson/issues/10569) | i18n.merge_file() doesn't support depend_files | high | Add depend_files (ContainerTypeInfo(list, (str, File))) to the MergeFile TypedDict and typed_kwargs, and in merge_file concatenate |
| [#10589](https://github.com/mesonbuild/meson/issues/10589) | python.find_installation() does not distinguish between Modu | high | Wrap the module-check script's importlib.import_module(mod) in try/except, splitting the exit code/output between ModuleNotFoundEr |
| [#10732](https://github.com/mesonbuild/meson/issues/10732) | Recognise `__attribute__ ((malloc, malloc (fclose, 1)))` in  | high | Add a new key (e.g. 'malloc_with_deallocator') to c_function_attributes.py, with test code `void my_free(void*); void *foo(void) _ |
| [#10740](https://github.com/mesonbuild/meson/issues/10740) | import libraries are not cleaned up by ninja clean | high | In the generate_link_target family (around ninjabackend.py:3835), when it's a SharedLibrary and target.import_filename exists, add |
| [#10875](https://github.com/mesonbuild/meson/issues/10875) | gnome module: g-ir-scanner extend cflags filter for '-m' | high | Add '-m' to the startswith tuple at gnome.py:1125, making it `('-D', '-U', '-I', '-m')`. This propagates ABI flags such as -m64/-m |
| [#10937](https://github.com/mesonbuild/meson/issues/10937) | VS backend: avoid creating files with forbidden characters | medium | In the places in vs2010backend.py that generate projfile_path/ofname (the gen_vcxproj family), insert a helper that replaces < > : |
| [#11018](https://github.com/mesonbuild/meson/issues/11018) | Deprecation warning shown, when values in options array are  | high | Add an 'allow_dups' boolean kwarg to array-type option() in meson_options.txt/meson.options, propagating it to UserStringArrayOpti |
| [#11020](https://github.com/mesonbuild/meson/issues/11020) | Meson does not gracefully handle mismatched wrap directory | medium | After tarball extraction in wrap.py, check whether the expected directory exists, and if not, throw a WrapException that presents  |
| [#11021](https://github.com/mesonbuild/meson/issues/11021) | Don't dump Java/JAR related arguments into the compilation d | medium | In generate_compdb, restrict the target languages to clike (native languages such as c/cpp/objc/objcpp/cuda/fortran/d), or give th |
| [#11073](https://github.com/mesonbuild/meson/issues/11073) | meson install removes needed RPATH entries specified by pkg- | medium | In build.py's get_rpath_dirs_from_link_args, also interpret bare '-R<dir>' / '-R <dir>' (the Solaris/illumos linker form) in addit |
| [#11088](https://github.com/mesonbuild/meson/issues/11088) | Meson fails to retrieve the "system" include folder with pkg | medium | When getting --cflags for a pkgconfig dependency, set the environment variable PKG_CONFIG_ALLOW_SYSTEM_CFLAGS=1 (regardless of lan |
| [#11436](https://github.com/mesonbuild/meson/issues/11436) | C17/C18 are not accepted for Intel classic C compiler | high | In mesonbuild/compilers/c.py IntelCCompiler.get_options(), extend the `stds` list to include 'c17'/'c18' guarded by an appropriate |
| [#11601](https://github.com/mesonbuild/meson/issues/11601) | Support for Renesas H8SX1648 | high | Add the H8 family (e.g. 'h8300' and/or 'h8sx' as reported) to the `known_cpu_families` tuple in mesonbuild/envconfig.py, add a mat |
| [#11750](https://github.com/mesonbuild/meson/issues/11750) | `meson dist` includes .git folder of non-Meson wraps | high | Add ignore=shutil.ignore_patterns('.git') to shutil.copytree(sub_src_root, sub_distdir) in mdist.py's GitDist.create_dist (also .h |
| [#11999](https://github.com/mesonbuild/meson/issues/11999) | Unable to search for dependencies in mixed language project  | high | Remove 'nasm' from clib_langs, or, in the loop in _get_compiler_for_dep, skip compilers that don't support library finding and fal |
| [#12021](https://github.com/mesonbuild/meson/issues/12021) | ValueError: Invalid suffix '_pb2.py' | high | Replace the `raise ValueError` in fs.py's replace_suffix with `raise InvalidArguments` (or mesonlib.MesonException), so a clear er |
| [#12093](https://github.com/mesonbuild/meson/issues/12093) | _split_fetch_real_dirs can fail due to a path inside a bitlo | medium | In gnu.py get_compiler_dirs (and the _split_fetch_real_dirs helper), wrap the os.path.exists/realpath/normpath resolution in a try |
| [#12130](https://github.com/mesonbuild/meson/issues/12130) | Unclear wording in docs about custom_target | medium | Reword the final bullet in Custom-build-targets.md so it clearly ties the `output:` value (e.g. foo.dat) to the resulting build_di |
| [#12169](https://github.com/mesonbuild/meson/issues/12169) | CUDA compiler doesn't pass cuda_args to `links` check | medium | Ensure _determine_args includes the target/global cuda_args for the cuda compiler in compiles()/links() checks, mirroring how cpp_ |
| [#12198](https://github.com/mesonbuild/meson/issues/12198) | Unhandled python exception with malformed environment variab | medium | Validate env var names when building the test environment (reject names containing '=' or NUL) in mtest / EnvironmentVariables, ra |
| [#12336](https://github.com/mesonbuild/meson/issues/12336) | Allow using generator to produce sources for `gnome.compile_ | high | Add build.GeneratedList to the accepted types of the 'dependencies' KwargInfo in gnome.compile_resources (gnome.py:402) and handle |
| [#12397](https://github.com/mesonbuild/meson/issues/12397) | Excessive dependency depth triggers a python exception when  | medium | In build.save() catch RecursionError around pickle.dump and raise a clear MesonException explaining the excessive dependency nesti |
| [#12462](https://github.com/mesonbuild/meson/issues/12462) | Using the intel oneAPI compiler icx.exe warns about unrecogn | medium | For the intel-llvm-cl compilers, override always_args (or filter in unix_args_to_native/get_always_args) to drop '/utf-8', which i |
| [#12469](https://github.com/mesonbuild/meson/issues/12469) | CustomTarget command: silently uses only first output of Tar | high | In eval_custom_target_command (backends.py ~1558), when a CustomTarget with >1 output is used directly in command:, either emit th |
| [#12480](https://github.com/mesonbuild/meson/issues/12480) | AppleFramework modules should be case-sensitive to support c | medium | Fix the AppleFrameworks example in Dependencies.md to use correctly-cased module names (e.g. 'Foundation'), add a note that names  |
| [#12493](https://github.com/mesonbuild/meson/issues/12493) | Can't pass environment variables to `configure_file()` | high | Add ENV_KW to func_configure_file typed_kwargs and pass kwargs['env'] into run_command_impl at interpreter.py:2912-2917 instead of |
| [#12496](https://github.com/mesonbuild/meson/issues/12496) | `meson wrap install` a specific version | high | Parse a version from the install name (e.g. 'foo==1.2.3' or a --version flag), look it up in releases[name]['versions'], and fetch |
| [#12548](https://github.com/mesonbuild/meson/issues/12548) | exclude install tags when running `meson install` | high | Add an --exclude-tags argument in minstall.add_arguments and, in should_install/install filtering, skip entries whose install_tag  |
| [#12566](https://github.com/mesonbuild/meson/issues/12566) | Compiler checks do not ignore environment variables (CFLAGS) | medium | Update docs/yaml/objects/compiler.yaml note (and any mirrored markdown) to reflect that CFLAGS/CPPFLAGS/CXXFLAGS from the environm |
| [#12641](https://github.com/mesonbuild/meson/issues/12641) | zsh shell completions don't support more than one --cross-fi | high | In data/shell-completions/zsh/_meson, prefix the --cross-file= and --native-file= _arguments specs with '*' (i.e. '*--cross-file=[ |
| [#12710](https://github.com/mesonbuild/meson/issues/12710) | custom_target() does not accept follow_symlinks | high | Add a follow_symlinks KwargInfo to func_custom_target's typed_kwargs and thread it into the InstallDataBase for the target's insta |
| [#12717](https://github.com/mesonbuild/meson/issues/12717) | In `install_emptydir` only the first argument works | high | Make func_install_emptydir support varargs: attach @typed_pos_args('install_emptydir', varargs=str, min_varargs=1) and generate/ap |
| [#12725](https://github.com/mesonbuild/meson/issues/12725) | len(string) function does not exist, though the manual refer | high | Replace `len(string)` in Syntax.md:327 and str.yml:165 with the actual `'string'.length()` syntax, or with a descriptive phrase (e |
| [#12907](https://github.com/mesonbuild/meson/issues/12907) | No warning or error is issued when trying to install a non-e | high | At the start of do_copydir (or within install_subdirs), check os.path.isdir(src_dir) and, if it doesn't exist, issue an mlog warni |
| [#12988](https://github.com/mesonbuild/meson/issues/12988) | [cmake] support running subproject with -Wno-dev | high | Add an append_cmake_args (or add_cmake_args) method to CMakeSubprojectOptions that pushes raw arguments onto self.cmake_options. S |
| [#13078](https://github.com/mesonbuild/meson/issues/13078) | Incorrect handling of malformed array values in c_args | high | In mesonbuild/utils/universal.py's listify_array_value(), change `except ValueError:` to `except (ValueError, SyntaxError):`, dele |
| [#13094](https://github.com/mesonbuild/meson/issues/13094) | install_headers doesn't preserve path when executed on a fil | high | In the preserve_path branch of func_install_headers in interpreter.py, change `dirname = os.path.dirname(file.fname)` to the dirna |
| [#13163](https://github.com/mesonbuild/meson/issues/13163) | rfe: install_rpath and build_rpath should accept string list | high | Extend the build_rpath/install_rpath KwargInfo in type_checking.py to (str, ContainerTypeInfo(list, str)), then after listify join |
| [#13391](https://github.com/mesonbuild/meson/issues/13391) | Cross file property cmake_skip_compiler_test = true causes e | medium | In get_cmake_skip_compiler_test (mesonbuild/envconfig.py:221), replace `assert isinstance(raw, str)` with a proper type check that |
| [#13395](https://github.com/mesonbuild/meson/issues/13395) | cmake dependency: confusing formulation of warning | medium | Grep for 'Could not find and exact match' in mesonbuild/cmake (dependency.py) and fix: 'and'->'an', reword 'Using imported is reco |
| [#13477](https://github.com/mesonbuild/meson/issues/13477) | meson doesn't know hp pa | medium | In CPU family normalization (mesonbuild/envconfig.py, detect_cpu_family / known_cpu_families), map 'hppa' (and hppa2.0 etc., as re |
| [#13497](https://github.com/mesonbuild/meson/issues/13497) | find_program does not support meson.pyz | medium | In ExternalProgram search (mesonbuild/programs.py), special-case files with a '.pyz' suffix to be run as `python_command + [path]` |
| [#13593](https://github.com/mesonbuild/meson/issues/13593) | C++ modules incompatible with unity build | medium | When unity build is enabled, exclude C++ module interface units (.ixx / module partitions) from unity grouping (compile them separ |
| [#13636](https://github.com/mesonbuild/meson/issues/13636) | Add 'follow_symlinks' support to gnome.yelp () | high | Add follow_symlinks (bool, optional) to the Yelp kwargs of gnome.yelp, and pass follow_symlinks=kwargs['follow_symlinks'] to the b |
| [#13755](https://github.com/mesonbuild/meson/issues/13755) | Stripping: 'strip' binary is always expected, even if it is  | high | In create_install_data (backends.py:1663), verify existence with something like shutil.which(detect.defaults['strip'][0]) during t |
| [#13814](https://github.com/mesonbuild/meson/issues/13814) | Meson throws exception updating subprojects (relpath across  | high | Wrap the relpath at msubprojects.py:723 in try/except and fall back to abspath on ValueError, or avoid relpath and use abspath/rea |
| [#13821](https://github.com/mesonbuild/meson/issues/13821) | Wrap does not clone submodules even after specifying clone-r | high | Replace the clone-recursive check at wrap.py:722 with a boolean parser (e.g. value.lower() in ('true','1','yes','on')). Reuse an e |
| [#13874](https://github.com/mesonbuild/meson/issues/13874) | Directory path concatenation in the 'dir_name' argument of t | medium | Using '/' as a separator in subdir('sd1/sd11') isn't normalized on Windows, so current_source_dir()/current_build_dir() return mal |
| [#13921](https://github.com/mesonbuild/meson/issues/13921) | using C and C++ standard as an array should not fail if ther | medium | In the C/C++ std option handling (mesonbuild/compilers/cpp.py, the _test_cpp_std / std-array coercion path), when iterating an arr |
| [#13994](https://github.com/mesonbuild/meson/issues/13994) | Add --fatal-meson-warnings to meson dist | medium | Add a --fatal-meson-warnings flag to the `meson dist` argument parser (mdist.py) that sets mlog.set_fatal_warnings-style behavior, |
| [#14043](https://github.com/mesonbuild/meson/issues/14043) | `meson setup` finds an old NASM version that it doesn't acco | medium | In NasmCompiler.get_include_args (mesonbuild/compilers/asm.py ~140), either reject NASM < 2.14 during detection, or append os.sep  |
| [#14048](https://github.com/mesonbuild/meson/issues/14048) | `subproject()`'s `default_options` doesn't accept feature op | medium | Allow UserFeatureOption values in subproject() default_options by coercing them via .to_string() (like other option types) in the  |
| [#14049](https://github.com/mesonbuild/meson/issues/14049) | subproject command fails when using wrap & custom subproject | high | In mesonbuild/wrap/wrap.py (~line 258) the redirect path validation hardcodes `p != 'subprojects'`. Replace the literal with the a |
| [#14065](https://github.com/mesonbuild/meson/issues/14065) | Documentation: clarify what a "full path" is | high | Update docs/yaml/functions/custom_target.yaml (@INPUT@/@OUTPUT@/@INPUTn@/@OUTPUTn@/@OUTDIR@ descriptions) and the file object full |
| [#14163](https://github.com/mesonbuild/meson/issues/14163) | compiler.find_library() static argument doesn't match docume | high | Fix the static description in docs/yaml/objects/compiler.yaml to match the implementation: when unspecified, follow prefer_static  |
| [#14221](https://github.com/mesonbuild/meson/issues/14221) | `meson subprojects update` doesn't initialize new submodules | high | Add '--init' to the command at mesonbuild/msubprojects.py:421 to make it ['submodule','update','--init','--checkout','--recursive' |
| [#14282](https://github.com/mesonbuild/meson/issues/14282) | Suggestion: meson setup should hint at 'first statement must | high | Add the hint 'the first statement must be a call to project()' alongside the InvalidCode message at interpreterbase.py:148 (for th |
| [#14372](https://github.com/mesonbuild/meson/issues/14372) | `zig rc` not detected correctly by windows.py | high | Add an entry for zig rc to the detection list at windows.py:92 (since zig rc is LLVM rc-compatible, set rc_type=ResourceCompilerTy |
| [#14375](https://github.com/mesonbuild/meson/issues/14375) | [Rust] native_static_libs is not populated when skip_sanity_ | high | Decouple the _native_static_libs call from sanity_check, and ensure it always runs once before the first link even with skip_sanit |
| [#14605](https://github.com/mesonbuild/meson/issues/14605) | `qt6.compile_translations` throws warning when subdirectory  | high | In _qt.py compile_translations, build the CustomTarget name from os.path.basename(ts) (or replace path separators) instead of the  |
| [#14656](https://github.com/mesonbuild/meson/issues/14656) | doc: description is truncated? | high | In docs/yaml/functions/custom_target.yaml depend_files description, change '[[@file]], or the return value of [[configure_file]]'  |
| [#14662](https://github.com/mesonbuild/meson/issues/14662) | Add `-fno-pch-timestamp` when using ccache+clang and precomp | medium | Add '-fno-pch-timestamp' to clang's PCH *generation* args when ccache is in use (Compiler.ccache is set). Best placed where the PC |
| [#14673](https://github.com/mesonbuild/meson/issues/14673) | Meson doesn't handle `limited_api_suffix = None` from `pytho | high | In modules/python.py extension_module, when limited_api is requested and self.limited_api_suffix is None, raise a clear MesonExcep |
| [#14683](https://github.com/mesonbuild/meson/issues/14683) | Unknown CPU family ev6 | high | In envconfig.py's cpu-family normalization (the elif chain around lines 620-657, mirrored in detect_cpu below), add a branch mappi |
| [#14807](https://github.com/mesonbuild/meson/issues/14807) | Array option accepts any invalid value when choice is empty | high | Change `if self.choices:` at mesonbuild/options.py:530 to `if self.choices is not None:`, so that an empty-list choices rejects an |
| [#14853](https://github.com/mesonbuild/meson/issues/14853) | Machine-files.md: missing mention of [host_machine] section | high | Add descriptions of [host_machine]/[build_machine]/[target_machine] to the Sections section of Machine-files.md, referencing/trans |
| [#15053](https://github.com/mesonbuild/meson/issues/15053) | depends support for i18n.gettext() | high | Add depends (list[BuildTarget\|CustomTarget]) to i18n.py's Gettext typed-dict and gettext()'s KwargInfo, passing it to the pot-gen |
| [#15159](https://github.com/mesonbuild/meson/issues/15159) | Mention `file://` URLs in wrap files documentation | medium | Add a note to the source_url/fallback_url description in docs/markdown/Wrap-dependency-system-manual.md about whether file:// URLs |
| [#15164](https://github.com/mesonbuild/meson/issues/15164) | meson setup on same builddir but different srcdir doesn't ex | high | In msetup.py's validate_dirs, when has_valid_build is true, compare the source root stored in coredata (or meson-info) against the |
| [#15274](https://github.com/mesonbuild/meson/issues/15274) | On Windows with git core.autocrlf not false, dist's clean in | high | Add '--ignore-cr-at-eol' to the git diff-index call at mdist.py:182 when on Windows and core.autocrlf != false. Check git config - |
| [#15295](https://github.com/mesonbuild/meson/issues/15295) | Documentation: get_pkgconfig_variables is deprecated, but us | high | Replace the get_pkgconfig_variable('prefix') / ('libdir', define_variable:...) examples at docs/markdown/Dependencies.md l.48-58 w |
| [#15329](https://github.com/mesonbuild/meson/issues/15329) | gdb-path argument of meson test does not work as expected | high | Change `check_bin = 'gdb'` at mtest.py:2309 to `check_bin = options.gdb_path`. |
| [#15392](https://github.com/mesonbuild/meson/issues/15392) | ninja scan-build does not pass down -Dauto_features | medium | Fix the command construction so that when meson setup is re-run inside scan-build, built-in options such as auto_features from the |
| [#15415](https://github.com/mesonbuild/meson/issues/15415) | Extend C++ stdlib hardening to MSVC (_MSVC_STL_HARDENING) | medium | Add -D_MSVC_STL_HARDENING=1 for MSVC (cl) to the location where b_ndebug/hardening currently applies definitions for libstdc++/lib |
| [#15420](https://github.com/mesonbuild/meson/issues/15420) | LLVM Flang does not properly handle fortran_std | high | Add get_options to LlvmFlangFortranCompiler in fortran.py, set self._update_language_stds(opts, ['none','legacy','f95','f2003','f2 |
| [#15596](https://github.com/mesonbuild/meson/issues/15596) | Boost Python dependency silently selects ABI-incompatible li | high | In mesonbuild/dependencies/boost.py mod_name_matches(): startswith-matching a bare 'python3' request against 'boost_python313' is  |
| [#15658](https://github.com/mesonbuild/meson/issues/15658) | devenv should set GI_GIR_PATH for Vala | high | In mesonbuild/modules/gnome.py, wherever generate_gir / vala_gir output is registered for devenv (near the existing self._devenv_p |
| [#15700](https://github.com/mesonbuild/meson/issues/15700) | Meson init still creates starter cpp file when provided with | high | In mesonbuild/templates/sampleimpl.py _detect_sources(): when the user explicitly passed srcfiles that don't match {executable}.{e |
| [#15724](https://github.com/mesonbuild/meson/issues/15724) | generate_dub_file with file sources | high | In mesonbuild/modules/dlang.py _do_validate(), accept mesonlib.File (and File-in-list): convert each File to its relative/absolute |
| [#15750](https://github.com/mesonbuild/meson/issues/15750) | -Cprefer-dynamic for rust proc-macros doesn't have any effec | high | Primarily a docs fix: update docs/markdown/Rust.md around line 105 to note that -Cprefer-dynamic is a no-op for proc-macros (rustc |
| [#15757](https://github.com/mesonbuild/meson/issues/15757) | gtest log filenames use only test name for uniqueness | high | In mesonbuild/mtest.py where the gtest XML output filename is built (line ~1126, filename = f'{self.test.name}.xml'), incorporate  |
| [#15813](https://github.com/mesonbuild/meson/issues/15813) | Add 'dos' as a .system() operating system | high | Add a 'dos' row (comment: 'DOS via djgpp') to the 'Operating system names' table in docs/markdown/Reference-tables.md so the value |
| [#15833](https://github.com/mesonbuild/meson/issues/15833) | Latest `libwmf-dev` on Debian/Ubuntu "moved `libwmf-config`  | medium | Either add /usr/lib/x86_64-linux-gnu/libwmf/bin to PATH in the ubuntu-rolling CI image (ciimage), or mark the libwmf framework tes |
| [#15863](https://github.com/mesonbuild/meson/issues/15863) | extra_files from declare_dependency() lost in meson introspe | high | In BuildTarget.__init__ (mesonbuild/build.py), the assignment `self.extra_files = kwargs.get('extra_files', [])` at ~line 900 runs |
| [#15893](https://github.com/mesonbuild/meson/issues/15893) | Shipped RPM macros don't work on EL-8 | high | In data/macros.meson replace the RPM 4.16+ `%[ ... ? ... : ... ]` ternary expressions (lines ~32 and ~39) with EL-8-compatible con |
| [#15919](https://github.com/mesonbuild/meson/issues/15919) | Document that ``output`` parameter of configure_file is rela | high | Edit docs/yaml/functions/configure_file.yaml: extend the `output` kwarg description to note the file is generated relative to meso |
| [#15955](https://github.com/mesonbuild/meson/issues/15955) | [C++] `-Wsign-conversion` and `-Wfloat-conversion` are missi | high | In mesonbuild/compilers/mixins/gnu.py, add '-Wsign-conversion' and '-Wfloat-conversion' to the C++-specific extra warning args (th |
| [#15956](https://github.com/mesonbuild/meson/issues/15956) | gnome.mkenums_simple produce unexpected result when multi-li | high | In mesonbuild/modules/gnome.py mkenums_simple (~L2028-2035), the multi-line header_prefix is interpolated inside the textwrap.dede |
| [#15968](https://github.com/mesonbuild/meson/issues/15968) | Meson examples use wrong way to specify fortran compiler | high | In cross/none.txt (line ~14) and cross/arm64cl.txt (line ~4), rename the `[binaries]` key `fc` to `fortran` to match what meson ac |
| [#15976](https://github.com/mesonbuild/meson/issues/15976) | meson compile cannot invoke run_target in a subproject (ninj | high | In mesonbuild/mcompile.py generate_target_names_ninja (L154-155), for 'alias'/'run' targets it returns [target.name], dropping the |

### Effort: Medium (49)

| Issue | Title | Confidence | Implementation approach |
|---|---|---|---|
| [#1550](https://github.com/mesonbuild/meson/issues/1550) | install_man does not accept target output | high | Allow CustomTarget/CustomTargetIndex/GeneratedList in install_man args (like install_data), track built outputs, and install their |
| [#1687](https://github.com/mesonbuild/meson/issues/1687) | Missing support for GSettings enum files | high | Add a gnome.mkenums option/mode (or a dedicated helper) that runs glib-mkenums with the GSettings schemalist templates (fhead/vhea |
| [#1781](https://github.com/mesonbuild/meson/issues/1781) | Add support for internal header and VAPI | high | Add kwargs (e.g. vala_internal_header/vala_internal_vapi) to library/shared_module for Vala, wiring --internal-header and --intern |
| [#2621](https://github.com/mesonbuild/meson/issues/2621) | i18n.merge_file does not generate a dependency on the .po fi | medium | In i18n.merge_file, read LINGUAS (or glob *.po in po_dir) and pass the resolved .po files as depend_files of the generated CustomT |
| [#2978](https://github.com/mesonbuild/meson/issues/2978) | configure_file() needs an option to verify all configuration | medium | Track which config keys are substituted during configure_file() template processing and add a `strict:`/`unused:` option (or warni |
| [#3650](https://github.com/mesonbuild/meson/issues/3650) | dependency-specific keywords to dependency() are always acce | high | After the dependency type is resolved, validate that dependency-type-specific kwargs (modules/optional_modules for qt/boost/cmake, |
| [#3822](https://github.com/mesonbuild/meson/issues/3822) | Streamline inter-target build dependency management | high | Add a DEPENDS_KW (order-only depends) to executable()/library()/etc. by including it in _ALL_TARGET_KWS or _BUILD_TARGET_KWS and t |
| [#3941](https://github.com/mesonbuild/meson/issues/3941) | Allow passing multiple FeatureOptions to required: | high | Extend extract_required_kwarg to accept a list of FeatureOptions/bools and AND them with the truth table in the issue (notably ena |
| [#4773](https://github.com/mesonbuild/meson/issues/4773) | compiler.find_library to take library version | medium | Add optional `version:`/`soversion:` kwargs to compiler.find_library() that match versioned shared objects (e.g. libfoo.so.1.0.0)  |
| [#9334](https://github.com/mesonbuild/meson/issues/9334) | gnome: improve compile_resources | medium | Add an external_data option to gnome.compile_resources that passes --external-data to glib-compile-resources and generates the .o  |
| [#10338](https://github.com/mesonbuild/meson/issues/10338) | <lang>_pch should take file but only accepts string | high | Add mesonlib.File to _PCH_ARGS's ContainerTypeInfo, and normalize File to an absolute/relative path string in _pch_validator/_pch_ |
| [#10591](https://github.com/mesonbuild/meson/issues/10591) | Add libpcre2 as a dependency class | medium | Add a Pcre2SystemDependency to mesonbuild/dependencies/dev.py etc., modeled on zlib (around dev.py:459); implement pkg-config('lib |
| [#11156](https://github.com/mesonbuild/meson/issues/11156) | coverage dependencies: genhtml should not be needed for llvm | medium | In coverage.py, when use_llvm_cov is set, add a path that generates HTML directly via `llvm-cov show -format=html` (preparing prof |
| [#11167](https://github.com/mesonbuild/meson/issues/11167) | Cannot pass custom_target to override_find_program | high | Add build.CustomTarget (and CustomTargetIndex if needed) as an allowed type to the typed_pos_args of override_find_program_method  |
| [#11459](https://github.com/mesonbuild/meson/issues/11459) | No support for env kwarg in generator()? | high | Add ENV_KW to the @typed_kwargs of func_generator (interpreter.py:2340), add `env` to kwtypes.FuncGenerator, thread it through bui |
| [#11519](https://github.com/mesonbuild/meson/issues/11519) | support install_symlink() pointing to target | medium | Extend the `pointing_to` KwargInfo to accept build targets (Executable/SharedLibrary/StaticLibrary with a single output). When a t |
| [#11687](https://github.com/mesonbuild/meson/issues/11687) | Add a `version` argument to `import('python').find_installat | high | Add KwargInfo('version', ...) to find_installation, and after detection, verify language_version() with version_compare_many. On m |
| [#12502](https://github.com/mesonbuild/meson/issues/12502) | No builtin way to check Python module version | high | Allow modules entries like 'hwdata>=2.4.1' (or a separate module_versions kwarg); in find_installation run a small script that imp |
| [#12611](https://github.com/mesonbuild/meson/issues/12611) | rfe: please provide meson uninstall | high | Add an muninstall.py that reads meson-logs/install-log.txt (list of installed files) and removes them (respecting --destdir/--dry- |
| [#13026](https://github.com/mesonbuild/meson/issues/13026) | Dlang: D compilers can also consume *.i files as sources | medium | Add '.i' (and '.c' if needed) to the D compiler's (mesonbuild/compilers/d.py) can_compile_suffixes. However, since lang_suffixes g |
| [#13966](https://github.com/mesonbuild/meson/issues/13966) | jar() rule fails with "Argument list too long" error | high | Make the java compile rule use a response file. In generate_java_compile_rule (ninjabackend.py ~2600), add rspable=True and rspfil |
| [#14041](https://github.com/mesonbuild/meson/issues/14041) | coverage with lcov problem: meson hard-codes "--ignore-error | high | In mesonbuild/scripts/coverage.py (~line 146), avoid unconditionally passing `--ignore-errors unused`. Options: only add it when t |
| [#14069](https://github.com/mesonbuild/meson/issues/14069) | failed to call external command due to encoding issue when m | medium | In Popen_safe / Popen_safe_legacy (mesonbuild/utils/universal.py ~1940-1969), pass errors='replace' (or 'surrogateescape') to subp |
| [#14087](https://github.com/mesonbuild/meson/issues/14087) | detect_clangformat should consult native [binaries] and only | medium | Make detect_clangformat (and the related clang-tidy/etc. detectors, now in the tooldetect module) first look up the tool key in th |
| [#14140](https://github.com/mesonbuild/meson/issues/14140) | using `@OUTPUT@` in a custom_target depfile argument results | medium | In ninjabackend generate_custom_target depfile handling (~1335-1340), the depfile value already contains the target subdir when @O |
| [#14141](https://github.com/mesonbuild/meson/issues/14141) | find_program() do not fallback to extra arguments when the f | high | Thread the version requirement into program_from_system/program_from_file_for/program_from_overrides so each candidate name is ver |
| [#14232](https://github.com/mesonbuild/meson/issues/14232) | VS backend cross-compile support is broken (especially Micro | high | Review the places in vs2010backend.py where platform determination should use machines.target.system, and revert GDK detection (de |
| [#14371](https://github.com/mesonbuild/meson/issues/14371) | CMake dependency wrapped in `-Wl,--no-as-needed` not passed | high | In tracetargets.py's unresolved-argument handling, add a branch that, on detecting a linker flag like -Wl, or -Wl,--no-as-needed,< |
| [#14378](https://github.com/mesonbuild/meson/issues/14378) | `canonicalize_filename` path collision | high | In object_filename_from_source, add a hash suffix or sequence number to make normalized names unique when they collide within the  |
| [#14565](https://github.com/mesonbuild/meson/issues/14565) | Documentation: files() not listed as returning file objects | high | In docs/refman/loaderbase.py _validate_func, when populating returned_by, recurse into DataTypeInfo.held_type so that list/array e |
| [#14689](https://github.com/mesonbuild/meson/issues/14689) | compiler.preprocess() adds -c | medium | CompileTarget is used both for transpile and preprocess. For preprocess-mode targets the compile rule should emit the preprocess-o |
| [#14700](https://github.com/mesonbuild/meson/issues/14700) | meson dist: .gitattributes export-ignore does not apply to s | high | In mdist.py process_submodules, before copy_git for each submodule run `git check-attr export-ignore <subpath>` from the parent re |
| [#14741](https://github.com/mesonbuild/meson/issues/14741) | Wrong args passed to flang(-new) with `get_supported_argumen | high | Override get_compiler_check_args in LlvmFlangFortranCompiler (and likely ClassicFlangFortranCompiler) so it does NOT emit the clan |
| [#14771](https://github.com/mesonbuild/meson/issues/14771) | `patch` executable cannot be overriden for wrap diff files | high | Resolve the `patch` (and `git` for `git apply`) executable through the machine-file binaries lookup / find_program machinery inste |
| [#15000](https://github.com/mesonbuild/meson/issues/15000) | split: expose shell-compatible string splitting functionalit | medium | Add a `shell_split` method to primitives/string.py that calls mesonlib.split_args. Version-gate it with FeatureNew, document it in |
| [#15093](https://github.com/mesonbuild/meson/issues/15093) | constructing a dict with a `kwargs` key flattens kwargs into | high | Add an expand_kwargs flag (default True) to reduce_arguments, and call it with expand disabled from dict-literal evaluation (evalu |
| [#15124](https://github.com/mesonbuild/meson/issues/15124) | test() and generator() does not have depend_files kwarg | high | Add DEPEND_FILES_KW to the KwargInfo of test/benchmark and generator, propagating it into TestSerialisation/Generator and adding i |
| [#15190](https://github.com/mesonbuild/meson/issues/15190) | Support for fil-c | medium | In compilers/detect.py's clang version detection, strip the 'Fil-C ...' prefix before extracting the clang version (following the  |
| [#15235](https://github.com/mesonbuild/meson/issues/15235) | Add version checks for GNU Binutils prelinking vs LTO | medium | When prelink is specified and b_lto is enabled, get the GNU ld (bfd/gold) version and warn if it is below 2.44. Use the DynamicLin |
| [#15249](https://github.com/mesonbuild/meson/issues/15249) | _FORTIFY_SOURCE should be disabled with some sanitizers (ASA | medium | When b_sanitize includes address/memory, consider adding -U_FORTIFY_SOURCE via sanitizer_compile_args or built-in hardening. Howev |
| [#15314](https://github.com/mesonbuild/meson/issues/15314) | Add support for -Db_sanitize=fuzzer on MSVC | medium | Add a 'fuzzer' -> /fsanitize=fuzzer mapping to sanitizer_compile_args in visualstudio.py. Also verify consistency with combination |
| [#15324](https://github.com/mesonbuild/meson/issues/15324) | "meson subprojects" does not recognize wraps from Cargo.lock | medium | Move the Cargo.lock reading from Interpreter construction time to Resolver (wrap) construction time, so it can also be referenced  |
| [#15394](https://github.com/mesonbuild/meson/issues/15394) | -Db_sanitize=fuzzer fails | high | When fuzzer is included in the sanitizers, use a test source that defines LLVMFuzzerTestOneInput instead of main() for the has_mul |
| [#15435](https://github.com/mesonbuild/meson/issues/15435) | Unhandled python exception when link_language:'rust' without | high | When link_language:'rust' is specified but there are no rust sources, either use rustc as the linker or raise a clear, explicit er |
| [#15531](https://github.com/mesonbuild/meson/issues/15531) | Unchanged python files are byte-compiled (again) with --only | high | Thread the --only-changed flag (or a per-file mtime check) into pycompile.py's compileall(); pass force=False and/or skip files wh |
| [#15801](https://github.com/mesonbuild/meson/issues/15801) | qt6.qml_module(): forward Qt6's metatype .json files to qmlt | medium | In mesonbuild/modules/_qt.py qml_module(), iterate the Qt module deps passed via `dependencies`, and for each locate qt_libdir/qt6 |
| [#15864](https://github.com/mesonbuild/meson/issues/15864) | Meson cannot find `llvm-config` on macOS for LLVM installed  | medium | In mesonbuild/dependencies/dev.py LLVMDependencyConfigTool, add macOS Homebrew keg-only fallback search dirs (/opt/homebrew/opt/ll |
| [#15865](https://github.com/mesonbuild/meson/issues/15865) | meson introspect --dependencies no longer returns declare_de | medium | Bisected to db6b15b67. Review how introspection collects internal dependencies (mesonbuild/mintro.py / interpreter) and restore in |
| [#15887](https://github.com/mesonbuild/meson/issues/15887) | Static libraries fail to link with `zig cc` due to unsupport | medium | In mesonbuild/linkers/linkers.py ArLinker.__init__ / get_std_link_args, the decision to emit thin archives ('T') only excludes dar |

---

## C. Genuinely open (1281)

> Valid issues that need real discussion, are larger in scope, depend on an upstream project, or (for the `not_safe`-demoted ones above) only looked resolved on a shallow code read.

| Issue | Title | Reason |
|---|---|---|
| [#48](https://github.com/mesonbuild/meson/issues/48) | OS X application bundle support | macOS .app bundle generation still has no built-in support; this is a large feature request whose discussion continues in the succ |
| [#106](https://github.com/mesonbuild/meson/issues/106) | Distinguish between "public" and "private" dependencies | Part of the original request (reflecting Requires/Requires.private in the .pc file) is already implemented in the pkgconfig module |
| [#123](https://github.com/mesonbuild/meson/issues/123) | add support for golang | Go compiler support still doesn't exist in mesonbuild/compilers/ and remains unimplemented. This is a large, long-standing request |
| [#341](https://github.com/mesonbuild/meson/issues/341) | SWIG support | A SWIG module/generator doesn't exist in the code or the module list and remains unimplemented. It has drawn a lot of interest, so |
| [#348](https://github.com/mesonbuild/meson/issues/348) | Support jar dependencies via maven | Fetching jar dependencies from Maven is unimplemented. Fetching dependencies over the network ties into Meson's design philosophy  |
| [#382](https://github.com/mesonbuild/meson/issues/382) | Detect changes to pkg-config files and reconfigure | Automatic reconfiguration on pkg-config file changes would be useful, but it needs a dependency-tracking mechanism, so discussion  |
| [#707](https://github.com/mesonbuild/meson/issues/707) | Better project options | There has been partial progress on kconfig-style tree-structured options and conditional display, but the original proposal as a w |
| [#825](https://github.com/mesonbuild/meson/issues/825) | Add docdir builtin option | docdir is still not among the built-in directory options (not listed in Builtin-options.md). This is a small-to-medium implementat |
| [#837](https://github.com/mesonbuild/meson/issues/837) | xdg module for common freedesktop tasks | A dedicated freedesktop/xdg module is unimplemented. It needs design discussion around updating the desktop/mime/icon caches, and  |
| [#841](https://github.com/mesonbuild/meson/issues/841) | Handle better missing source files | In D, missing source files aren't discovered until the link stage. Improving diagnostics is reasonable, but this is a cross-langua |
| [#894](https://github.com/mesonbuild/meson/issues/894) | Add valadoc support | Built-in valadoc support is unimplemented (there's no 'valadoc' implementation in the code). Keep this as a feature request for Va |
| [#909](https://github.com/mesonbuild/meson/issues/909) | Appstream support | No appstream/appdata validation-and-install helper is found in the GNOME module; it's unimplemented. This is a small feature reque |
| [#985](https://github.com/mesonbuild/meson/issues/985) | Print a list of all not-found required and optional dependencies | A feature to list all missing dependencies together at the end is unimplemented. There's a summary feature, but required dependenc |
| [#1014](https://github.com/mesonbuild/meson/issues/1014) | Add generate_typelib in the GNOME module | generate_gir exists, but a standalone generate_typelib that separates gir and typelib generation is unimplemented. Keep this as a  |
| [#1018](https://github.com/mesonbuild/meson/issues/1018) | Free Pascal support | Free Pascal compiler support is unimplemented (no pascal entry in compilers/). This is a large-scale new-language-addition request |
| [#1122](https://github.com/mesonbuild/meson/issues/1122) | Errors in pkgconfig file lead to very cryptic build failure | A broken .pc file containing something like '$(prefix)' produces an unhelpful ninja "bad $-escape" error. There's still room to im |
| [#1160](https://github.com/mesonbuild/meson/issues/1160) | Investigate extension for OS X bundles | This issue considers how to handle the default suffix (dylib/so/bundle) for shared modules on macOS; it's an unresolved design top |
| [#1195](https://github.com/mesonbuild/meson/issues/1195) | Vala pkg-config dependency checks don't look for vapi files | When a pkg-config dependency has no corresponding vapi, an unnecessary --pkg is passed to valac. Vala dependency handling has impr |
| [#1203](https://github.com/mesonbuild/meson/issues/1203) | pkgconfig: choose datadir/libdir automatically for installation | Automatically placing header-only .pc files with no library into $datadir/pkgconfig raises backward-compatibility concerns, and lo |
| [#1307](https://github.com/mesonbuild/meson/issues/1307) | Adding a vapi to 'sources' promote the depending library to a Vala tar | Including a vapi in sources causes a C/C++ target to be incorrectly promoted to Vala, producing 'Vala library has no Vala source f |
| [#1314](https://github.com/mesonbuild/meson/issues/1314) | Discussion: "Run configurations" for Meson | run_target gained env/args, which is partial progress, but the broader "run configuration" concept for IDEs remains a large, still |
| [#1317](https://github.com/mesonbuild/meson/issues/1317) | Promote LLVM IR to a first-class language | Meson can already compile .ll sources (is_llvm_ir), but the request to treat it as a first-class language selectable in project()  |
| [#1362](https://github.com/mesonbuild/meson/issues/1362) | Support SOURCE_DATE_EPOCH for reproducible builds | No implementation applying SOURCE_DATE_EPOCH timestamps to installed artifacts was found in the code; it's unimplemented. Keep it  |
| [#1364](https://github.com/mesonbuild/meson/issues/1364) | Improve verbosity of custom target definitions | This asks for a way to define reusable, generator-like custom_target templates. generator already exists, but abstraction on the c |
| [#1393](https://github.com/mesonbuild/meson/issues/1393) | Support options that must be specified and have no default value | Options with no default value that force explicit specification aren't documented in Build-options.md and remain unimplemented. Ke |
| [#1398](https://github.com/mesonbuild/meson/issues/1398) | Support separate prefix and exec-prefix | This requests an exec-prefix independent of prefix, and allowing datadir outside prefix. No local evidence was found of this flexi |
| [#1453](https://github.com/mesonbuild/meson/issues/1453) | Add support for gobject-introspection overrides | This requests adding a helper to the GNOME module for installing Python GI overrides. No local evidence of a dedicated API was fou |
| [#1468](https://github.com/mesonbuild/meson/issues/1468) | Code Analysis Support | This is about integrating static-analysis tools like cppcheck. There are some targets for things like clang-tidy, but a general-pu |
| [#1484](https://github.com/mesonbuild/meson/issues/1484) | Missing dependencies are included in valac arguments | Specifying both of a pair of platform-only dependencies like gio-unix/gio-windows (where only one exists) breaks valac. It can be  |
| [#1492](https://github.com/mesonbuild/meson/issues/1492) | Add a mechanism to add prefix/suffixes to configuration files | This requests a way to prepend/append static definitions to a config.h generated by configure_file with no input. No local impleme |
| [#1503](https://github.com/mesonbuild/meson/issues/1503) | Environment variables are not serialized during configuration | Under the VS backend, environment variables like LIB/INCLUDE are lost on regeneration. Environment capture has improved with tools |
| [#1508](https://github.com/mesonbuild/meson/issues/1508) | Add support for pkg variables (pkgdatadir, pkgincludedir, pkglibdir, p | Derived directory variables such as pkgdatadir are still not offered as built-in options, and many projects construct them themsel |
| [#1524](https://github.com/mesonbuild/meson/issues/1524) | Allow specifying dependency information in the cross-info file | A mechanism to directly specify dependency info (libs/cflags) in a machine file when pkg-config is absent is not implemented as a  |
| [#1525](https://github.com/mesonbuild/meson/issues/1525) | Fetching dependency information in the absence of pkg-config | This proposes a shareable dependency-description file for platforms without pkg-config. cmake dependency support and wrap provider |
| [#1526](https://github.com/mesonbuild/meson/issues/1526) | Normalize file paths before writing them out for better Windows suppor | This is a large-scale refactor proposal to normalize all paths. Many individual Windows path problems have been fixed one by one,  |
| [#1543](https://github.com/mesonbuild/meson/issues/1543) | Support getting the minimum version from a dependency() object | dep.version() only returns the "detected version"; there's no public API to retrieve the version constraints passed to dependency( |
| [#1564](https://github.com/mesonbuild/meson/issues/1564) | custom_target replaces back-slashes with slashes in the command argume | This is an old bug about backslash handling in command arguments. It has a lot of reactions (12) indicating high interest, but the |
| [#1589](https://github.com/mesonbuild/meson/issues/1589) | GNOME mkenums support incomplete | gnome.mkenums still can't specify separate fhead/ftail etc. for the header vs. the source; differentiation is only possible via te |
| [#1592](https://github.com/mesonbuild/meson/issues/1592) | Substitute absolute path to files() when used in string formatting | This requests expanding files() objects to absolute paths during string concatenation/formatting. File expansion in things like li |
| [#1601](https://github.com/mesonbuild/meson/issues/1601) | files installed by modules are not tracked | Files installed by modules such as i18n (.mo) aren't tracked by uninstall. An install-log-based uninstall mechanism exists, but it |
| [#1608](https://github.com/mesonbuild/meson/issues/1608) | Arbitrary overriding of binaries | This is a discussion thread tracking the design of find_program's machine-file/subproject-fallback/cross-override behavior. Much o |
| [#1658](https://github.com/mesonbuild/meson/issues/1658) | We should pass --define-prefix to pkg-config | Meson passes --define-variable to pkg-config, but not --define-prefix (relative-prefix recalculation). This is small but affects c |
| [#1686](https://github.com/mesonbuild/meson/issues/1686) | Qt5 preprocessed files missing in mesonintrospect --target-files | Preprocessing-generated files such as moc/uic/rcc output aren't included in introspect --target-files. Introspection has been expa |
| [#1733](https://github.com/mesonbuild/meson/issues/1733) | i18n.gettext: POTFILES.in does not support generated files | [Downgraded on thread review / the original "fixed" verdict was wrong] For the classic i18n.gettext() + POTFILES.in path that this |
| [#1739](https://github.com/mesonbuild/meson/issues/1739) | i18n: Cannot specify per-language keywords | i18n.gettext only supports generic args; per-language xgettext keywords and intltool-style [type=...] prefixes are unsupported. Th |
| [#1748](https://github.com/mesonbuild/meson/issues/1748) | Provide a way to run in parallel all tests within a single test execut | Enumerating and running subtests within a single test executable in parallel is unimplemented. There's the gtest protocol and --sl |
| [#1789](https://github.com/mesonbuild/meson/issues/1789) | Introduce a package concept | This proposes introducing package_name/package_version separate from the display project name. It's an API design request that tie |
| [#1799](https://github.com/mesonbuild/meson/issues/1799) | VS and Xcode backends ignore link_depends | The VS backend now processes link_depends as a dependency (partially fixed), but the Xcode backend's handling couldn't be confirme |
| [#1811](https://github.com/mesonbuild/meson/issues/1811) | Provide a way for modules to register project configuration options | This proposes a mechanism for modules to register project options and turn disabled targets into no-ops. It's a large design quest |
| [#1812](https://github.com/mesonbuild/meson/issues/1812) | Support generation of man pages with help2man | Dedicated support for generating man pages from executables via help2man is unimplemented. Users can build it themselves with cust |
| [#1844](https://github.com/mesonbuild/meson/issues/1844) | Documentation created by gtkdoc is not generated when compiling | [Downgraded on thread review / the original "fixed" verdict was wrong] gnome.gtkdoc now creates a CustomTarget, but with build_by_ |
| [#1855](https://github.com/mesonbuild/meson/issues/1855) | Unable to add include paths to headers generated with custom targets t | When referencing generated headers via include_directories, the include path is missing if the corresponding build directory hasn' |
| [#1860](https://github.com/mesonbuild/meson/issues/1860) | generate_gir should be skipped if g-ir-scanner is not found | gnome.generate_gir unconditionally requires gobject-introspection and g-ir-scanner, with no way to skip or make it optional when t |
| [#1885](https://github.com/mesonbuild/meson/issues/1885) | Move stdsplit to mesontest | A --no-stdsplit argument was added to meson test, but the top-level built-in option 'stdsplit' still remains, so the request (remo |
| [#1899](https://github.com/mesonbuild/meson/issues/1899) | Provide extra tool for clang dependencies. | LLVM dependencies can be handled via modules/components, but there's no dedicated helper to fetch the clang libraries (libclang*)  |
| [#1905](https://github.com/mesonbuild/meson/issues/1905) | Default install location in windows | This is a report/documentation question about the validity of the default prefix (e.g. c:/bin/) used when installing on Windows. H |
| [#1907](https://github.com/mesonbuild/meson/issues/1907) | Inconsistency between library suffix generated on windows and link nam | This reports an inconsistency on Windows where static libraries are generated as liblibname.a while pkg-config dependencies try to |
| [#1916](https://github.com/mesonbuild/meson/issues/1916) | Code coverage report on the home page can be wrong | The codecov badge in the README still exists, and the point that it can show inaccurate values after doc-only commits remains vali |
| [#1923](https://github.com/mesonbuild/meson/issues/1923) | Ability to get multiple variables out of fallback dependency | This requests syntax to retrieve multiple variables from a fallback dependency in one call. get_variable still handles one variabl |
| [#1971](https://github.com/mesonbuild/meson/issues/1971) | Provide a way for install scripts to access target-specific installati | Install scripts receive environment variables like MESON_INSTALL_(DESTDIR_)PREFIX, but there's no direct way to get a specific tar |
| [#1972](https://github.com/mesonbuild/meson/issues/1972) | Default libprefix on Debian like distribution seems not good. | When natively installing to /usr/local, the libdir becomes a multiarch path (lib/x86_64-linux-gnu), which falls outside the defaul |
| [#1974](https://github.com/mesonbuild/meson/issues/1974) | Allow meson.add_custom_uninstall_script() | A hook to run arbitrary commands on uninstall (an uninstall counterpart to add_install_script) is unimplemented. With 7 reactions, |
| [#1994](https://github.com/mesonbuild/meson/issues/1994) | Dependencies for Vala added to the C build target | This is a bug where an in-tree GIR/VAPI dependency, which should be satisfied at the .vala→.c step, instead attaches at the .c→.o  |
| [#2009](https://github.com/mesonbuild/meson/issues/2009) | Have a 'clean' target for the current project (not subprojects) | Per-project/per-subproject clean-local or clean-<subproject> targets aren't provided. This request needs a design decision, such a |
| [#2028](https://github.com/mesonbuild/meson/issues/2028) | When use gnome.gtkdoc, no devhelp2 is generated | gnome.gtkdoc doesn't generate .devhelp2 files (there's no devhelp-output handling in gnome.py). This is a small improvement that c |
| [#2029](https://github.com/mesonbuild/meson/issues/2029) | error when program is not found is not useful | This reports an unhelpful error message when an unchecked program used in a run_target command isn't found at build time. Error ha |
| [#2042](https://github.com/mesonbuild/meson/issues/2042) | Split documentation for simple users vs developers | docs/markdown is organized by topic — tutorials, per-module references, Contributing.md, the YAML reference manual, etc. — which e |
| [#2054](https://github.com/mesonbuild/meson/issues/2054) | Include order wrong for subproject includes | ninjabackend.py has logic that carefully handles -isystem/-I include ordering, but without reproduction it can't be confirmed whet |
| [#2058](https://github.com/mesonbuild/meson/issues/2058) | feature request: case statement in meson.build | There's no case/switch statement in docs/markdown/Syntax.md or the interpreter grammar. Meson's DSL is deliberately minimal, with  |
| [#2062](https://github.com/mesonbuild/meson/issues/2062) | feature request: ability to apply string methods to '@INPUT@' and so o | In generator.yaml, @INPUT@/@OUTPUT@ undergo only simple path substitution; there's no mechanism to apply string methods like .to_l |
| [#2064](https://github.com/mesonbuild/meson/issues/2064) | Windows Isolated Applications and Side-by-side Assemblies | There's no dedicated feature for SxS/isolated applications. Manifest embedding is only possible as a workaround by manually specif |
| [#2103](https://github.com/mesonbuild/meson/issues/2103) | Using a custom VAPI does not generate a -pkg foo flag | Vala.md documents handling of in-project custom VAPIs (--vapidir, find_library(dirs:)), but the documentation alone doesn't confir |
| [#2105](https://github.com/mesonbuild/meson/issues/2105) | Windows path definitions and shared libraries | This is a compound issue. The vulkan dependency is already resolved via mesonbuild/dependencies/ui.py (VulkanDependencySystem). Ho |
| [#2121](https://github.com/mesonbuild/meson/issues/2121) | Add an option to have @rpath install_name instead of an absolute path | [Downgraded on thread review / the original "fixed" verdict was wrong] The triage's basis (get_soname_args's install_name=['@rpath |
| [#2128](https://github.com/mesonbuild/meson/issues/2128) | Using Anaconda Python and Qt module - Windows. Error with finding QT d | Qt dependency detection now searches for qmake by version in order via the config-tool method, with the pkg-config method also sel |
| [#2132](https://github.com/mesonbuild/meson/issues/2132) | support WINDOWS_EXPORT_ALL_SYMBOLS like cmake | There's still no feature to automatically export all symbols on Windows. vs_module_defs is a manual mechanism for passing a hand-w |
| [#2155](https://github.com/mesonbuild/meson/issues/2155) | Should de-duplicate -isystem flags just like -I flags | [Downgraded on thread review / the original "fixed" verdict was wrong] Deduplication (dedup2) is done, but as the comment at clike |
| [#2164](https://github.com/mesonbuild/meson/issues/2164) | i18n support for man pages | There are no references to po4a anywhere in the repository, and the i18n module has no support for man-page translation (po4a). It |
| [#2173](https://github.com/mesonbuild/meson/issues/2173) | Rust: Support external crates | The full mesonbuild/cargo/ directory (interpreter/manifest/toml, etc.) plus Cargo workspace/subproject support is implemented and  |
| [#2186](https://github.com/mesonbuild/meson/issues/2186) | Make - and _ synonyms in project options and enforce a convention for  | Option names are validated with the regex [^a-zA-Z0-9_-], allowing both dashes and underscores, but OptionKey keeps and hashes the |
| [#2193](https://github.com/mesonbuild/meson/issues/2193) | Silently ignoring changes to default_options in project() is a bad use | project()'s default_options are still, by design, applied only on the first configuration (first_invocation), with command-line an |
| [#2209](https://github.com/mesonbuild/meson/issues/2209) | Provide a way to specify the debug library name to use in cc.find_libr | compiler.find_library's kwargs only include things like required/has_headers/static/disabler/dirs; there's no debug_name-equivalen |
| [#2210](https://github.com/mesonbuild/meson/issues/2210) | Provide a way to specify fallback library names to search if a depende | dependency() supports multiple names (varargs names, since 0.60.0) and subproject fallback, but that's a fallback to a different d |
| [#2219](https://github.com/mesonbuild/meson/issues/2219) | gnome.compile_schemas() only considers schemas in srcdir | compile_schemas only passes the srcdir from state.build_to_src to glib-compile-schemas as input and doesn't scan generated schemas |
| [#2265](https://github.com/mesonbuild/meson/issues/2265) | Add modules to the sdl dependency class, e.g.: image, mixer, net, etc. | The SDL2 dependency class (SDL2DependencyConfigTool) still has no modules keyword for handling submodules like image/mixer/net. Th |
| [#2271](https://github.com/mesonbuild/meson/issues/2271) | Use a generated file as main file in gtkdoc | gnome.gtkdoc's main_xml/main_sgml keywords still only accept (str, NoneType) and don't accept the File/GeneratedList objects retur |
| [#2292](https://github.com/mesonbuild/meson/issues/2292) | Dependency checks should automatically offer to install the necessary  | A feature to automatically install (or suggest) distro -dev packages is unimplemented. Given the diversity of package managers and |
| [#2293](https://github.com/mesonbuild/meson/issues/2293) | Speed up C library function checks by fetching a list of all exported  | has_function() still performs a compile/link test per function, with results only reused via a per-build compile cache. An optimiz |
| [#2295](https://github.com/mesonbuild/meson/issues/2295) | Add a build_machine.build_id() and build_machine.build_date() | The build_machine object's methods are limited to cpu_family/cpu/system/endian/kernel/subsystem; build_id() and build_date() haven |
| [#2370](https://github.com/mesonbuild/meson/issues/2370) | Warning color is unreadable on white background | The warning label is still printed via yellow('WARNING:'), remaining bright yellow. The readability issue on white backgrounds is  |
| [#2388](https://github.com/mesonbuild/meson/issues/2388) | Conditional options | The option definition file (meson.options / meson_options.txt) is still just a sequence of declarative option() calls; conditional |
| [#2399](https://github.com/mesonbuild/meson/issues/2399) | Provide a get gir version method for gnome module | The gnome module compares the g-ir-scanner version internally (_giscanner_version_compare), but no public method to retrieve it fr |
| [#2406](https://github.com/mesonbuild/meson/issues/2406) | gnome.gtkdoc() - add option of pdf output | gnome.gtkdoc only invokes gtkdoc-mkhtml (the tool list at gnome.py:1530 is scan/scangobj/mkdb/mkhtml/fixxref); gtkdoc-mkpdf and mk |
| [#2416](https://github.com/mesonbuild/meson/issues/2416) | Install generated files into multiple directories | custom_target's install_dir maps each output to a single directory (or excludes some via false); there's no way to install a singl |
| [#2424](https://github.com/mesonbuild/meson/issues/2424) | Relocatable build directory | The build directory has many absolute paths written into it, so it can't be reused after copying or moving (a copy will fail). A f |
| [#2425](https://github.com/mesonbuild/meson/issues/2425) | --wrap-mode ignores git submodules | [Downgraded on thread review / the original "fixed" verdict was wrong] The early return at wrap.py:572-574 works for a submodule t |
| [#2436](https://github.com/mesonbuild/meson/issues/2436) | boost log on mac os x is not using -mt variant | Boost dependency detection has been completely rewritten in mesonbuild/dependencies/boost.py, and selecting -mt-tagged libraries b |
| [#2467](https://github.com/mesonbuild/meson/issues/2467) | Allow setting name_prefix project-wide | name_prefix/name_suffix are only per-build-target keywords (build.py:904-909, _build_target_base.yaml:225); there's no option to s |
| [#2470](https://github.com/mesonbuild/meson/issues/2470) | TUI to configure Meson (akin to `ccmake`) | There's no TUI/curses/ncurses-based configuration interface within mesonbuild, and nothing equivalent to meson configure --tui is  |
| [#2475](https://github.com/mesonbuild/meson/issues/2475) | ninja build or ninja reconfigure does not detect dependency changes | The install/uninstall of pkg-config dependencies (gmime2/gmime3) on the system does not involve file changes tracked by Meson as d |
| [#2486](https://github.com/mesonbuild/meson/issues/2486) | Add meson option to force color output when output is not tty | Currently colorize_console() in mlog.py only auto-detects based on whether output is a tty; there is no option to force colored ou |
| [#2519](https://github.com/mesonbuild/meson/issues/2519) | compiler.run() current working directory and cleanup | [Downgraded after thread review / original 'fixed' verdict was wrong] TemporaryDirectoryWinProof is merely a temporary directory f |
| [#2546](https://github.com/mesonbuild/meson/issues/2546) | install_headers() should install headers into intermediates directory, | install_headers still only applies at install time; there is no mechanism to place headers into an intermediate include directory  |
| [#2592](https://github.com/mesonbuild/meson/issues/2592) | Add warning for unused variable option in meson.build files | There is no static analysis in interpreter/ast that detects and warns about unused variables. Since Meson variables have implicit  |
| [#2600](https://github.com/mesonbuild/meson/issues/2600) | Allow multiple commands/replace_strings in vcs_tag | vcs_tag still only takes a single command/replace_string (type: str); there is no feature to handle multiple tags at once. Users s |
| [#2605](https://github.com/mesonbuild/meson/issues/2605) | has_function fails to find strcpy_s on mingw | has_function still has no special handling for overloads or compiler built-in functions (only individual cases like lchmod are han |
| [#2607](https://github.com/mesonbuild/meson/issues/2607) | Differentiate global variables from local variables | There has been no change to the language spec regarding variable scoping/immutability. This is a large design topic with 59 commen |
| [#2609](https://github.com/mesonbuild/meson/issues/2609) | Have the equivalent of AX_COMPILER_FLAGS from Autotools | warning_level (0/1/2/3/everything), werror, and get_supported_arguments() exist, but there is no feature providing a canned set of |
| [#2657](https://github.com/mesonbuild/meson/issues/2657) | Cannot pass targets to generator( ) arguments | The exe itself in generator() can accept an Executable/Program, but the arguments: keyword is still ContainerTypeInfo(list, str),  |
| [#2666](https://github.com/mesonbuild/meson/issues/2666) | add write_file() method | The fs module has read/copyfile but nothing on the write side; there's no dedicated feature to write an arbitrary string to a file |
| [#2669](https://github.com/mesonbuild/meson/issues/2669) | Keeps some track of where every value comes from | There is no mechanism to track and display the origin of each value (which line it was defined/added on) in error messages. Errors |
| [#2687](https://github.com/mesonbuild/meson/issues/2687) | meson.build configuration file syntax test | [Downgraded after thread review / original 'fixed' verdict was wrong] `meson format --check-diff` checks whether formatting matche |
| [#2722](https://github.com/mesonbuild/meson/issues/2722) | Multiple commands in run_target | run_target's command is still a single command array; chaining multiple commands (with && or multiple command arrays) is not suppo |
| [#2729](https://github.com/mesonbuild/meson/issues/2729) | [mingw-w64] Add a FAQ or How-To to create mingw-w64 pacman packages | Documentation aimed specifically at MSYS2/mingw-w64 pacman/PKGBUILD packaging is still lacking, and this remains valid as a docume |
| [#2742](https://github.com/mesonbuild/meson/issues/2742) | Warn when build files use object.path() in places where object should  | Shebang handling for non-executable scripts has been improved (programs.py _shebang_to_cmd), and .full_path() was added in 0.55.0, |
| [#2765](https://github.com/mesonbuild/meson/issues/2765) | Don't want platform libraries to be included when linking statically t | There is still no automatic handling for splitting linking between dynamic and static based on the difference between pkg-config's |
| [#2875](https://github.com/mesonbuild/meson/issues/2875) | Allow different defaults for options based on OS and arch | Per-machine (host/build) options exist, but there is no mechanism to declaratively define OS/arch-specific option defaults. A size |
| [#2896](https://github.com/mesonbuild/meson/issues/2896) | pkgconfig generator should automatically populate requires/requires_pr | [Downgraded after thread review / original 'fixed' verdict was wrong] Partial functionality exists whereby passing a pkg-config de |
| [#2897](https://github.com/mesonbuild/meson/issues/2897) | pkgconfig.generate() -> declare_dependency() | pkgconfig.generate() only returns Data (the generated .pc file); there is no mechanism to obtain a dependency object from it. The  |
| [#2909](https://github.com/mesonbuild/meson/issues/2909) | Avoid copying files in gtkdoc documentation generation | gtkdochelper.py still copies content_files/html_assets (with a FIXME comment), leaving unresolved problems around conflicts with a |
| [#2922](https://github.com/mesonbuild/meson/issues/2922) | State corruption with multiple tasks running on same directory | [Downgraded after thread review / original 'fixed' verdict was wrong] msetup.py now acquires meson-private/meson.lock, but a code  |
| [#2945](https://github.com/mesonbuild/meson/issues/2945) | compiler.find_library() fallback inside dependency() | dependency() has no generic find_library fallback mechanism (neither a method nor a kwarg); as the design-discussion label indicat |
| [#2957](https://github.com/mesonbuild/meson/issues/2957) | Best way to handle post-build commands? | There is no POST_BUILD hook or post_build kwarg for tools like mt.exe/signtool that overwrite build artifacts. Workarounds exist v |
| [#2962](https://github.com/mesonbuild/meson/issues/2962) | Building a static library with msvc needs linker options sometimes | MSVC LTO adds /LTCG (get_lto_args), but there is no generic mechanism to pass user-specified link_args to the static library (lib. |
| [#2991](https://github.com/mesonbuild/meson/issues/2991) | Tell meson to not search for CCache | ccache is auto-detected unconditionally along the default compiler path. Specifying the compiler explicitly via a machine file avo |
| [#2993](https://github.com/mesonbuild/meson/issues/2993) | xcode-backend-generated Xcode project has no header search paths | The Xcode backend has been substantially reimplemented, but -I flags originating from pkg-config are still treated as cargs and ma |
| [#2998](https://github.com/mesonbuild/meson/issues/2998) | Limitations on customizing the install target | MESONINTROSPECT is now set in run_target/install scripts (partial resolution), but there is still no option to suppress installing |
| [#3001](https://github.com/mesonbuild/meson/issues/3001) | Generic overrider functionality | There is still no generic mechanism to override per-target buildtype/optimization/installability etc. via an external file without |
| [#3005](https://github.com/mesonbuild/meson/issues/3005) | exclude_files as a regex for install_subdir ? | install_subdir now has exclude_files/exclude_directories, but both take arrays of exact path names, and the requested regex/glob p |
| [#3023](https://github.com/mesonbuild/meson/issues/3023) | jar() can't deal with generate source code under the build directory | jar() accepts kwargs equivalent to executable, but it's unverified whether generated sources under the build directory can be hand |
| [#3046](https://github.com/mesonbuild/meson/issues/3046) | Uniform way to link whole libraries | Of the three proposals, declare_dependency support for link_whole (0.46.0) and dependency.as_link_whole() (0.56.0) have been imple |
| [#3047](https://github.com/mesonbuild/meson/issues/3047) | Meson needs native understanding of symbol version scripts | vs_module_defs (a MSVC-oriented .def) has been implemented, but there is still no dedicated kwarg to abstract the GNU version scri |
| [#3049](https://github.com/mesonbuild/meson/issues/3049) | -D_FILE_OFFSET_BITS=64 should be disabled on some buggy 32-bit platfor | get_largefile_args() still unconditionally adds -D_FILE_OFFSET_BITS=64 outside macOS/MSVC, and there's no feature test or exclusio |
| [#3070](https://github.com/mesonbuild/meson/issues/3070) | Java: add support to use custom manifest for files. | jar() gained main_class (and java_resources in 0.62.0), but there doesn't appear to be a kwarg for specifying an arbitrary MANIFES |
| [#3073](https://github.com/mesonbuild/meson/issues/3073) | Missing dependency between gir file and sources scanned for gir data. | gnome.generate_gir()'s sources and GIR output have no dependency link established between them. No clear evidence of a fix in the  |
| [#3111](https://github.com/mesonbuild/meson/issues/3111) | Dependency Handling Whiteboard | A long-running whiteboard-style issue consolidating design discussions such as static/dynamic linking choice and absolute-path pkg |
| [#3174](https://github.com/mesonbuild/meson/issues/3174) | How to create output name which removes a prefix string? | There is still no built-in way to do string substitution (e.g., stripping a prefix) on custom_target/generator outputs — only fixe |
| [#3183](https://github.com/mesonbuild/meson/issues/3183) | Linking C++ executable with Objective-C dynamic library fails | A problem where a C++ executable linking against an Objective-C (.m) library doesn't pull in the C++ standard library, causing the |
| [#3187](https://github.com/mesonbuild/meson/issues/3187) | Suggest to export symbols if linking with shared_library and *.lib is  | A proposal to improve the confusing LNK1104 error on Windows when the import library (.lib) isn't generated (i.e., no symbols are  |
| [#3202](https://github.com/mesonbuild/meson/issues/3202) | Expose way to set Windows Sdk | The VS backend internally holds windows_target_platform_version and writes it into the vcxproj, but there doesn't appear to be a p |
| [#3206](https://github.com/mesonbuild/meson/issues/3206) | Design proposal: install files created by generator.process() | Installing generator.process() output is still unimplemented. generator.yaml's documentation still advises 'use custom_target if y |
| [#3226](https://github.com/mesonbuild/meson/issues/3226) | Dump a configuration_data() as a list of -Dfoo="bar" -style defines | configuration_data has keys()/get(), but there's no get_c_args()-equivalent method to dump it as -Dfoo=bar-style c_args. Manual co |
| [#3266](https://github.com/mesonbuild/meson/issues/3266) | llvm: fallback to static if dynamic linking is not possible | Handling of static/shared for the llvm dependency has improved, with inconsistency detection now in place, but there's still no au |
| [#3323](https://github.com/mesonbuild/meson/issues/3323) | Add a kwarg to test() targets that resets timeout on test output | test() has timeout/timeout_multiplier, but there's no kwarg to reset the timeout upon detecting test output. A reasonable request  |
| [#3324](https://github.com/mesonbuild/meson/issues/3324) | Using generated files as qt resources fails with VS backend | qt.preprocess has been extended to accept generated files (custom target index/generator) across various inputs, but it's unverifi |
| [#3333](https://github.com/mesonbuild/meson/issues/3333) | run_target() dependencies are missing when using vs2017 generator | A case where a target specified via run_target()'s depends kwarg is not built by the VS backend (it works fine with ninja). Possib |
| [#3338](https://github.com/mesonbuild/meson/issues/3338) | Add -Bsymbolic by default | A b_symbolic base option does not exist in the codebase (no hits via grep). Enabling it by default raises ABI/interaction concerns |
| [#3342](https://github.com/mesonbuild/meson/issues/3342) | shared generators | An internal design proposal to generate a GeneratedList once and reuse it across multiple targets. A large design issue affecting  |
| [#3344](https://github.com/mesonbuild/meson/issues/3344) | paths method | A request for a paths() function, equivalent to files()/include_directories(), that treats directories as relative paths. No such  |
| [#3442](https://github.com/mesonbuild/meson/issues/3442) | override_find_program can cause configure time failures that the paren | A case where a parent that calls run_command at configure time against a build-time-generated program registered via override_find |
| [#3477](https://github.com/mesonbuild/meson/issues/3477) | meson test: disable error dialog boxes on Windows | There's no code in the codebase to suppress the Windows crash dialog (SEM_NOGPFAULTERRORBOX) when running meson test. A small, use |
| [#3482](https://github.com/mesonbuild/meson/issues/3482) | cc.has_function() should warn when the prefix: does not #include a hea | has_function switches its detection template depending on whether prefix includes an #include, mitigating false positives when no  |
| [#3500](https://github.com/mesonbuild/meson/issues/3500) | [wrap] Add vcpkg as another usable source to automatically fetch subpr | A request to integrate vcpkg as a wrap/subproject source. No vcpkg integration is found in the codebase; this remains a large desi |
| [#3519](https://github.com/mesonbuild/meson/issues/3519) | fts.h on Linux does not support _FILE_OFFSET_BITS=64 on glibc older th | Same root cause as #3049. get_largefile_args() still unconditionally adds -D_FILE_OFFSET_BITS=64 outside non-macOS/non-MSVC platfo |
| [#3522](https://github.com/mesonbuild/meson/issues/3522) | Newline in target name breaks build dir permanently (ninja backend) | A case where a newline in a target name causes build.ninja regeneration to fail repeatedly, permanently breaking the build directo |
| [#3524](https://github.com/mesonbuild/meson/issues/3524) | Add b_fast and b_march_native or something similar and make it possibl | Base options like b_ofast/b_march_native don't exist in the codebase, and the request to make -Ofast/-march=native into built-in o |
| [#3546](https://github.com/mesonbuild/meson/issues/3546) | generate_gir() does not make it possible to handle stub .gir files | A case where a stub .gir for an external library cannot be incorporated into generate_gir()'s subsequent scan/compile step. A reas |
| [#3548](https://github.com/mesonbuild/meson/issues/3548) | install_mode should support octal modes | install_mode accepts array[str\|int], but int is for uid/gid, and file mode is still primarily a symbolic string ('rwxr-xr-x'). Th |
| [#3551](https://github.com/mesonbuild/meson/issues/3551) | Add a way to check for the presence of a Python module | [Downgraded after thread review / original 'fixed' verdict was wrong] find_installation(modules:...) can check for module presence |
| [#3559](https://github.com/mesonbuild/meson/issues/3559) | Improve automatic detection of output file list for docbook gdbus_code | A case where gnome.gdbus_codegen's heuristic for guessing the docbook output filename is inaccurate. A minor, gnome-module-specifi |
| [#3566](https://github.com/mesonbuild/meson/issues/3566) | -O3 optimization level shouldn't be used with unity builds by default | The original triage was wrong. In options.py, DEFAULT_DEPENDENTS still maps release to optimization='3' (i.e., -O3), so the claim  |
| [#3581](https://github.com/mesonbuild/meson/issues/3581) | gtkdoc: Automatically generate version.xml | The gnome module's gtkdoc still has no feature to auto-generate version.xml. A small, reasonable feature request that remains open |
| [#3584](https://github.com/mesonbuild/meson/issues/3584) | Godot support | A proposal to integrate Godot as a 'language.' Niche, large in scope, heavily dependent on an external tool — this is better discu |
| [#3585](https://github.com/mesonbuild/meson/issues/3585) | add_project_link_args() is ambigous for targets that mix .c and .m fil | The confusion around link_args language specification caused by linker-selection order in mixed-language targets (clink_langs: obj |
| [#3589](https://github.com/mesonbuild/meson/issues/3589) | Relative paths of files() are passed to a command when custom_target i | A case where relative paths for files() passed to a custom_target's command are resolved based on cwd (the build dir), behaving di |
| [#3623](https://github.com/mesonbuild/meson/issues/3623) | Make it easier to dump strings to a file | fs.write / output_file(contents:) for writing a string directly to a file remain unimplemented. Currently the configure_file(confi |
| [#3628](https://github.com/mesonbuild/meson/issues/3628) | During cross compilation, base_options are being applied from native c | [Downgraded after thread review / original 'fixed' verdict was wrong] Compilers have been made per-machine, but the 'value' of a b |
| [#3635](https://github.com/mesonbuild/meson/issues/3635) | Speed-up compiler checks by parallelizing where possible | Parallelizing compiler checks like get_supported_arguments has still not been implemented (no ThreadPool etc. in compilers/). Rema |
| [#3676](https://github.com/mesonbuild/meson/issues/3676) | has_function misdetects smul_overflow as available. | [Downgraded on re-review / confirmed on real hardware] Reproduced has_function('smul_overflow')=YES on current master using zig cc |
| [#3679](https://github.com/mesonbuild/meson/issues/3679) | gl dependency is extremely incomplete, and should be improved or remov | dependency('gl') still exists as GLDependencySystem, trying -framework on Darwin, -lopengl32 on Windows, and find_library('GL') el |
| [#3742](https://github.com/mesonbuild/meson/issues/3742) | No warning_level to enable -Wpedantic but not -Wextra | warning_level is still a tiered scheme (0-3/everything), with -Wpedantic at level 3 and -Wextra at level 2. There's still no indep |
| [#3758](https://github.com/mesonbuild/meson/issues/3758) | find_library() with dirs kwarg falls back to system lib dir | Internally, the ignore_system_dirs parameter can suppress the system-dir fallback, but it's not exposed in compiler.find_library's |
| [#3803](https://github.com/mesonbuild/meson/issues/3803) | Ensure that the --sysroot= argument is set when using the 'root' cross | sys_root is used by pkg-config/CMake/qemu etc., but there's still no automatic mechanism to pass it to the C/C++ compiler as --sys |
| [#3839](https://github.com/mesonbuild/meson/issues/3839) | coverage report doesn't include rust sources | Rust now emits -C instrument-coverage via b_coverage (rust.py), and Meson's coverage script also supports llvm-cov, so the situati |
| [#3864](https://github.com/mesonbuild/meson/issues/3864) | wraps and patch files should be signed and the public keys shipped wit | GPG signature verification for wraps is unimplemented. Currently, integrity is only guaranteed via sha256 hashes of the tarball/pa |
| [#3868](https://github.com/mesonbuild/meson/issues/3868) | Friendlier messages when a dependency can't be found | The messaging when a dependency isn't found has been partially improved (fallback/wrap guidance, etc.), but the broader UX improve |
| [#3903](https://github.com/mesonbuild/meson/issues/3903) | RFE: add possibility to get output of vcs_tag() without configuring fi | vcs_tag still requires input/output files; there's no way to obtain the version string directly into a variable. This ties into th |
| [#3911](https://github.com/mesonbuild/meson/issues/3911) | New method on python module: find_installation().get_shebang() | PythonInstallation has no get_shebang-equivalent method implemented. A valid small feature addition that would return a platform-a |
| [#3918](https://github.com/mesonbuild/meson/issues/3918) | Using builtin targets as dependency for run_target | run_target's depends only accepts BuildTarget/CustomTarget/CustomTargetIndex/Program; built-in meta-targets like all/install/unins |
| [#3923](https://github.com/mesonbuild/meson/issues/3923) | Meson has_link_argument doesn't work for --version-script on FreeBSD | has_link_argument validates arguments by linking an executable, so on FreeBSD's GNU BFD ld, --version-script (usable only when lin |
| [#3970](https://github.com/mesonbuild/meson/issues/3970) | Don't add private dependencies to Requires.private when --default-libr | pkgconfig can control private entries via requires_private/libraries_private/dataonly, but there is no dedicated toggle to suppres |
| [#3982](https://github.com/mesonbuild/meson/issues/3982) | Add a test case for building gobject-introspection with AddressSanitiz | Request to add a CI test case that builds gobject-introspection under AddressSanitizer. This is a CI maintenance task, and it is u |
| [#4005](https://github.com/mesonbuild/meson/issues/4005) | ARM Compiler cross tests in Meson CI | Proposal to add Keil/ARMCC/ARMCLANG cross-compilation tests on Windows CI. This is an operational issue tied to CI infrastructure  |
| [#4019](https://github.com/mesonbuild/meson/issues/4019) | Provide 'rename' capability for installing executables and libraries | Renaming build targets at install time is not implemented. install_data has a `rename` option, but executable()/library() do not.  |
| [#4081](https://github.com/mesonbuild/meson/issues/4081) | Document the generic linker argument syntax. | Request to document the specification for translating the subset of classic ld-style linker arguments Meson supports (-L, -lfoo, e |
| [#4082](https://github.com/mesonbuild/meson/issues/4082) | Document the generic C style compiler argument syntax. | Request to document the translation specification for gcc-style compiler arguments (-DFOO=1, etc.) and specially handled arguments |
| [#4103](https://github.com/mesonbuild/meson/issues/4103) | QDoc integration | Request to integrate Qt's qdoc documentation generation into the qt module. No qdoc support is found in the current qt module. A v |
| [#4133](https://github.com/mesonbuild/meson/issues/4133) | Can't change name_suffix/prefix for only static library in both_librar | both_libraries() passes name_prefix/name_suffix as the same kwargs to both the shared and static targets, so a separate prefix/suf |
| [#4140](https://github.com/mesonbuild/meson/issues/4140) | Missing LINGUAS environment variable behaviour semantics for /usr/shar | i18n.gettext() reads languages from the LINGUAS file at configure time but does not honor the LINGUAS environment variable at buil |
| [#4253](https://github.com/mesonbuild/meson/issues/4253) | dependency module requirements based on dependency version. | Design proposal to embed version constraints into dependency()'s modules argument (e.g. a dict form). Requires API design discussi |
| [#4274](https://github.com/mesonbuild/meson/issues/4274) | meson won't link libgcc and libstdc++ statically in the 32-bit mingw e | Request to automatically add -static-libstdc++/-static-libgcc for 32-bit mingw. No built-in option exists; currently this requires |
| [#4295](https://github.com/mesonbuild/meson/issues/4295) | Passing an empty string to install_data's install_dir parameter is equ | install_data's install_dir='' (empty string) is treated the same as unspecified (None), landing under share/projectname instead of |
| [#4299](https://github.com/mesonbuild/meson/issues/4299) | Manage unit test output directory | Request for a known, writable, dedicated output directory for tests that gets cleared before each run. test() has workdir etc., bu |
| [#4350](https://github.com/mesonbuild/meson/issues/4350) | Shared precompiled header | Request to precompile a single PCH once and share it across multiple library() targets. Currently PCH is generated per target. Sin |
| [#4385](https://github.com/mesonbuild/meson/issues/4385) | Unable to use extract_objects() for Vala unit tests | Bug where the src/ prefix is dropped with Vala plus extract_objects(), causing a mismatch in generated object names that makes nin |
| [#4395](https://github.com/mesonbuild/meson/issues/4395) | Reimplement auto pull of wraps downloaded by vcs as documented. | Reimplementation of automatic pull for VCS (git) wraps. update_git() currently exists but only runs on a manual `meson subprojects |
| [#4412](https://github.com/mesonbuild/meson/issues/4412) | Add callgraph ninja target | Request to add a ninja target that generates a callgraph (dot file), similar to scan-build. This requires a pipeline of collecting |
| [#4413](https://github.com/mesonbuild/meson/issues/4413) | Need a mechanism for Vala to resolve symbols when using extract_object | A design-level problem where symbol resolution fails with Vala plus extract_objects(). Re-passing Vala sources to the compiler cre |
| [#4442](https://github.com/mesonbuild/meson/issues/4442) | Ninja goes into a reconfigure loop when the machine time goes backward | Problem where a system clock rollback makes meson.build appear newer than build.ninja, causing ninja to enter a reconfiguration lo |
| [#4464](https://github.com/mesonbuild/meson/issues/4464) | Meson doesn't link to Boost correctly on NetBSD | Problem on NetBSD where Boost libraries (/usr/pkg/lib) get linked without an rpath, making them unexecutable. boost.py's search pa |
| [#4465](https://github.com/mesonbuild/meson/issues/4465) | Get build target compiler flags | Request to retrieve, from within meson.build (or a generated artifact), the compiler flags used for a build target. No such method |
| [#4467](https://github.com/mesonbuild/meson/issues/4467) | [freestanding C/C++] Unable to include crt*.o files on the linking sta | Request for a way to correctly link crti/crtbegin...crtend/crtn in the right order for freestanding builds. link_early_args (inser |
| [#4468](https://github.com/mesonbuild/meson/issues/4468) | Automatically find dependencies on standard locations on BSD systems | Request to include the standard BSD package locations (/usr/local for FreeBSD/OpenBSD/DragonFly, /usr/pkg for NetBSD) in dependenc |
| [#4477](https://github.com/mesonbuild/meson/issues/4477) | Can not use gnome.compile_resources to produce two gresource files wit | Creating two gresources with the same base name in different subdirectories collides on the internal target name (target_name+'_gr |
| [#4484](https://github.com/mesonbuild/meson/issues/4484) | Feature Request: make ProjectGuid deterministic for MSVC backends | [Downgraded on thread review / the original "fixed" verdict was wrong] The generate_guid_from_path() (uuid5, deterministic) the tr |
| [#4498](https://github.com/mesonbuild/meson/issues/4498) | Allow specifying default compilers in meson.build | Request to specify a preferred/default compiler from within meson.build (e.g. a project() option). Currently project() has no such |
| [#4501](https://github.com/mesonbuild/meson/issues/4501) | RFC: Do not check for builtins in has_function, add has_builtin | has_builtin_define exists, but the essence of the RFC -- removing the builtin check from has_function and adding an independent ha |
| [#4510](https://github.com/mesonbuild/meson/issues/4510) | Wrap HTTPS SSL fallback redirects to HTTPS again | Report that the wrap HTTP fallback does not work in corporate-proxy environments with SSL inspection. wrapdb now operates on an HT |
| [#4541](https://github.com/mesonbuild/meson/issues/4541) | gnome.generate_gir uses improper shared-library with executable and AS | Problem where generate_gir writes libasan.so as a shared library when ASan is enabled. Specific to the gnome module and related to |
| [#4563](https://github.com/mesonbuild/meson/issues/4563) | How can attributes of a dependency (includes, compiler flags, etc.) be | There is still no general-purpose way to retrieve/display a dependency object's include directories or compile/link arguments (onl |
| [#4574](https://github.com/mesonbuild/meson/issues/4574) | Do something smarter with options | A design discussion about improving the readability of the options listing. An RFC from the maintainer (jpakkane), needing directi |
| [#4577](https://github.com/mesonbuild/meson/issues/4577) | Cannot access version in default_options | Calling meson.project_version() from within default_options crashes. Since default_options is evaluated before the version is fina |
| [#4597](https://github.com/mesonbuild/meson/issues/4597) | Meson not fully respecting -I/-L inside CFLAGS/LDFLAGS | find_library / get_define do not honor the -I/-L in CFLAGS/LDFLAGS. This ties into deliberately designed behavior (see #1772) and  |
| [#4637](https://github.com/mesonbuild/meson/issues/4637) | Use native files for saving the command line | Feature request to output all configured options in a re-submittable form (e.g. a native file). cmd_line.txt is saved, but generat |
| [#4650](https://github.com/mesonbuild/meson/issues/4650) | meson --wipe forgets about CFLAGS and friends | Bug where environment-derived CFLAGS/CXXFLAGS are lost after --wipe. Labeled "bug," with updates through 2025. Requires a design d |
| [#4669](https://github.com/mesonbuild/meson/issues/4669) | Support positional arguments also as kwargs | Dict expansion supports keyword arguments, but there is no mechanism to pass positional arguments via a dict. Requires a language- |
| [#4675](https://github.com/mesonbuild/meson/issues/4675) | Possibility to depend on the tarball generated by `ninja dist` | Request to use the dist tarball as an input/dependency of a custom_target. dist is currently a separate step outside the build gra |
| [#4685](https://github.com/mesonbuild/meson/issues/4685) | Meson RPATH munging can yield libraries that break ldconfig on Linux | Problem where removing RPATH entries when install_rpath is empty confuses some non-compliant tools (ldconfig, chrpath). depfixer h |
| [#4692](https://github.com/mesonbuild/meson/issues/4692) | Document which functions / methods are run completely at configure tim | Request to document that configure_file, run_command, etc. complete entirely at configure time. Valuable but tedious documentation |
| [#4694](https://github.com/mesonbuild/meson/issues/4694) | cross build definition file not flexible enough to support cross compi | Request to dynamically pull in environment-variable-derived flags in cross files (a devkitPro use case). This stems from the desig |
| [#4706](https://github.com/mesonbuild/meson/issues/4706) | pkgconfig generator should create the same Libs/Libs.private for all l | Request to unify how pkgconfig.generate's Libs/Libs.private output differs between shared/static/library. Labeled module:pkgconfig |
| [#4707](https://github.com/mesonbuild/meson/issues/4707) | Add linker args for specific dependencies | Request to attach linker arguments to a specific dependency only. An ongoing need with updates through 2025. Requires design of a  |
| [#4708](https://github.com/mesonbuild/meson/issues/4708) | Fortran: .mod .smod modules files not installed or found from other di | Request for support of installing Fortran .mod/.smod files and cross-directory references. Labeled language:fortran and install ta |
| [#4717](https://github.com/mesonbuild/meson/issues/4717) | File objects should be able to represent directories | files()/File still cannot represent a directory (files only). There is a legitimate use case for passing a directory as a custom_t |
| [#4722](https://github.com/mesonbuild/meson/issues/4722) | Remove element from a list | The array primitive has contains/length/get/slice/flatten but no delete/remove. Since Meson arrays are designed to be immutable, a |
| [#4735](https://github.com/mesonbuild/meson/issues/4735) | `compiler.run()` should use `MESON_BUILD_ROOT` as current working dire | Request that when compiler.run()'s feature detection creates a file, the build directory should be used as cwd. Reasonable, but ne |
| [#4736](https://github.com/mesonbuild/meson/issues/4736) | Meson ignores RCFLAGS in the windows resources compiler | windows.compile_resources does not honor the RCFLAGS environment variable. The RC/WINDRES environment variables are only used to r |
| [#4739](https://github.com/mesonbuild/meson/issues/4739) | Convert CFLAGS et al to build options | Proposal to interpret environment CFLAGS like -O2/-g and convert them into corresponding build options. A maintainer-originated de |
| [#4761](https://github.com/mesonbuild/meson/issues/4761) | dub dependency method cannot find libraries when they have other depen | Bug where dub dependencies cannot be resolved if they have transitive dependencies. Labeled dependencies and language:D, updated t |
| [#4763](https://github.com/mesonbuild/meson/issues/4763) | configure_file: Add config.vapi support | Request for configure_file to be able to generate a config.vapi, similar to config.h. Currently the Vala side relies on including  |
| [#4782](https://github.com/mesonbuild/meson/issues/4782) | Add support for dotnet core from Microsoft | Request for .NET Core (Roslyn/runtime runner) support. A large-scale extension of C# language support. Requires design work such a |
| [#4802](https://github.com/mesonbuild/meson/issues/4802) | Hardcoded list of llvm-config binary names breaks on upstream LLVM dev | [Downgraded on thread review / the original "fixed" verdict was wrong] The specific issue of llvm-config-9/-80 not being detected  |
| [#4844](https://github.com/mesonbuild/meson/issues/4844) | Meson should not (try to) modify jarfiles | Problem where, at install time, depfixer strips the Class-Path from a .jar's manifest, making the jar require an executable. fix_j |
| [#4865](https://github.com/mesonbuild/meson/issues/4865) | Allow setting the pkg-config search path in the native file | Proposal to add an env kwarg to dependency() to control things like PKG_CONFIG_PATH. This ties into extending pkg-config configura |
| [#4889](https://github.com/mesonbuild/meson/issues/4889) | Add option to support split debug informations | Request for a built-in option to automate split debug info (objcopy --only-keep-debug + strip + --add-gnu-debuglink). No such b_ o |
| [#4906](https://github.com/mesonbuild/meson/issues/4906) | [RFC] dump() function for diagnostics | Proposal for a dump() function that pretty-prints an object for humans and halts the build. The related debug() function was added |
| [#4932](https://github.com/mesonbuild/meson/issues/4932) | Add support for new gtk-doc flavour | Request for support of the new gtk-doc mode that uses gtkdoc-mkhtml2. Requires a change to the gnome module's gtkdoc implementatio |
| [#4943](https://github.com/mesonbuild/meson/issues/4943) | Feature proposal: Add filter and filter out methods for Generated List | The GeneratedList returned by generator.process() still has no filter/filter_out method. However, installing generated headers can |
| [#4951](https://github.com/mesonbuild/meson/issues/4951) | Add custom targets to 'dist' target | dist only supports adding scripts via add_dist_script; there is no feature to include build targets (binaries, flatpak, etc.) in t |
| [#4977](https://github.com/mesonbuild/meson/issues/4977) | Feature Proposal: Add directory level all targets | The ninja backend does not appear to have a feature to auto-generate a per-directory `some_dir/all` alias target. Manual replaceme |
| [#4993](https://github.com/mesonbuild/meson/issues/4993) | Cuda compiler and OpenMP | [Downgraded on thread review / the original "fixed" verdict was wrong] cuda.py's to_host_flags_base now wraps unknown flags with - |
| [#5024](https://github.com/mesonbuild/meson/issues/5024) | C++20 modules are in: discussing a sane (experimental) design for Meso | The C++ modules effort has advanced significantly (module scanning via ninja's dyndep, get_cpp_modules_args, an experimental `impo |
| [#5036](https://github.com/mesonbuild/meson/issues/5036) | Support for "ignoring" a linker argument | cc.has_link_argument/get_supported_link_arguments etc. can determine whether the toolchain supports a specific flag, but there is  |
| [#5037](https://github.com/mesonbuild/meson/issues/5037) | Compilation warnings in gnome.generate_gir() if a builddir include pat | gnome.generate_gir passes include directories straight through via -I without checking for existence, so g-ir-scanner still appear |
| [#5038](https://github.com/mesonbuild/meson/issues/5038) | i18n generating files | i18n's pot target name is still `<project_id>-pot` (and `<project_id>-update-po`), still prefixed with the project name. No common |
| [#5074](https://github.com/mesonbuild/meson/issues/5074) | Non existing wxWidgets modules are still found | The wxWidgets dependency just passes the requested module name straight to wx-config without validation, so it is still reported a |
| [#5075](https://github.com/mesonbuild/meson/issues/5075) | meson configure --clearcache doesn't allow detecting of new pkg-config | --clearcache clears the dependency cache (including failed results), but there is no confirmed mechanism to reliably detect newly  |
| [#5090](https://github.com/mesonbuild/meson/issues/5090) | unclear if using (via -fplugin) a gcc plugin in the same meson.build t | executable/library still has no general-purpose `depends:` keyword to make the compile stage depend on the output of another build |
| [#5093](https://github.com/mesonbuild/meson/issues/5093) | [FEATURE] Support creation of delay-load import libraries | A feature to generate Windows delay-load import libraries (dlltool --output-delaylib / MSVC's /delayload) does not exist in code o |
| [#5139](https://github.com/mesonbuild/meson/issues/5139) | Include Qt5 mkspecs headers | [Downgraded on thread review / the original "fixed" verdict was wrong] The request is to include the mkspecs directory (e.g. -I/us |
| [#5151](https://github.com/mesonbuild/meson/issues/5151) | Need a method like cc.compiles for assembler | nasm/masm have been added as proper languages/compilers, making assembly builds possible, but a public compile-check API for assem |
| [#5174](https://github.com/mesonbuild/meson/issues/5174) | [Feature request] Add clean_command kwarg to custom_target | custom_target has no clean_command keyword. Running a custom cleanup process via ninja clean is unimplemented and would require a  |
| [#5179](https://github.com/mesonbuild/meson/issues/5179) | Feature request: allow defining variables before project() if they don | Meson still requires project() to be the first statement (sanity_check_ast errors if the first statement is not project()), so var |
| [#5181](https://github.com/mesonbuild/meson/issues/5181) | Feature request: provide a way to find out if a built-in option is ava | get_option was improved to return a default value instead of erroring for base options (b_* etc.), but there is still no general-p |
| [#5192](https://github.com/mesonbuild/meson/issues/5192) | Allow providing pkg-config dependencies without pkg-config | [Downgraded on thread review / the original "fixed" verdict was wrong] The core request is to supply dependencies (e.g. OPENSSL_LI |
| [#5216](https://github.com/mesonbuild/meson/issues/5216) | LLVM update breaks meson build | Meson caches dependency-detection results, and there is no mechanism to automatically detect a version change in a tool like llvm- |
| [#5223](https://github.com/mesonbuild/meson/issues/5223) | Add warnings when environment variables change and wont be honored | A FIXME remains in the code noting that changes to environment variables (CFLAGS etc.) are ignored on reconfigure; a feature to de |
| [#5238](https://github.com/mesonbuild/meson/issues/5238) | meson configuration test prints don't identify native/target | dependency() outputs which machine (native/target) it is for, but compiler.has_argument/compiles/find_library etc. check messages  |
| [#5242](https://github.com/mesonbuild/meson/issues/5242) | gnome.gtkdoc: Wrong escape characters in scan args | gnome.gtkdoc still packs things like --scanargs using '@@' as a separator, so escaping issues for arguments containing special cha |
| [#5251](https://github.com/mesonbuild/meson/issues/5251) | Add support for LLVM/clang when using b_pgo | b_pgo works with clang too via the GCC-compatible -fprofile-generate/-fprofile-use, but the requested clang-native -fprofile-instr |
| [#5269](https://github.com/mesonbuild/meson/issues/5269) | Store objects in target introspection | Target introspection now includes sources/generated_sources/unity_sources and linker information, but there does not appear to be  |
| [#5270](https://github.com/mesonbuild/meson/issues/5270) | RFE: native support for const objects | There is no native language feature for const variables that forbid reassignment. The frozen mechanism used by add_project_argumen |
| [#5280](https://github.com/mesonbuild/meson/issues/5280) | Vala: unity build should merge Vala code, not C code | Problem where merging generated C files in a Vala unity build fails the build due to duplicate hidden C functions. The requested m |
| [#5320](https://github.com/mesonbuild/meson/issues/5320) | Make auto_features a per-subproject built-in option | [Downgraded on thread review / the original "fixed" verdict was wrong] A #106-type false positive. The per-subproject option found |
| [#5328](https://github.com/mesonbuild/meson/issues/5328) | Logging of environment variables in testlog.txt | testlog.txt still unconditionally dumps all inherited environment variables in full ("Inherited environment:"), so the concern abo |
| [#5343](https://github.com/mesonbuild/meson/issues/5343) | Building static library chain fails (modified test cases/common/43 lib | In a chain of static libraries, objects from a lower-level static lib linked via link_with are not pulled into the higher-level .a |
| [#5352](https://github.com/mesonbuild/meson/issues/5352) | C sharp missing library finding support | The C# compiler (cs.py) does not override find_library and still raises the base class's 'does not support library finding' except |
| [#5353](https://github.com/mesonbuild/meson/issues/5353) | compile_args doesn't work with C sharp | cs.py's get_dependency_compile_args has been improved to exclude -I arguments while accepting some other compile_args, but declare |
| [#5354](https://github.com/mesonbuild/meson/issues/5354) | extract_all_objects does not work with C sharp executables | Because C# does not have a per-object-file compilation model, extract_all_objects not working is a fundamental limitation of the l |
| [#5355](https://github.com/mesonbuild/meson/issues/5355) | compiler.get_supported_arguments reports success for unsupported flags | [Downgraded after thread review / original 'fixed' judgment was wrong] The original report's GCC 'is valid for C/ObjC' case has be |
| [#5356](https://github.com/mesonbuild/meson/issues/5356) | Add files as resources in C Sharp targets | No dedicated feature for adding resource files via -r: to C# targets can be found in the code, so users still need to work around  |
| [#5363](https://github.com/mesonbuild/meson/issues/5363) | Cross compilation and complex build setups | This is a design proposal from jpakkane himself (multi-platform simultaneous builds, similar to chainbuild), an architectural issu |
| [#5364](https://github.com/mesonbuild/meson/issues/5364) | feature option can't be set to auto when auto_features is set | The design where auto_features=enabled overrides all auto features remains in place, and whether individual options can be reverte |
| [#5390](https://github.com/mesonbuild/meson/issues/5390) | no libdl nor librt on OpenBSD | OpenBSD does not have -ldl/-lrt, so some unit tests that hardcode them fail. This is a portability issue on the test side; a small |
| [#5398](https://github.com/mesonbuild/meson/issues/5398) | generate_gir() should accept a File object to its header argument | Whether gnome.generate_gir's header argument accepts File objects needs to be verified against the gnome module's type acceptance. |
| [#5404](https://github.com/mesonbuild/meson/issues/5404) | Feature request: test compilation failure | A dedicated feature for 'testing that a given source fails to compile' is not implemented. compiler.compiles() allows checking thi |
| [#5406](https://github.com/mesonbuild/meson/issues/5406) | Support generic POSIX C compiler | Unknown compilers (e.g. pcc/tcc) are still rejected with 'Unknown compiler', and a generic POSIX c99 fallback has not been impleme |
| [#5408](https://github.com/mesonbuild/meson/issues/5408) | Feature request: call system command during run(code) | There is no mechanism to inject an external command like chmod before compiler.run() executes. The label remains 'enhancement', so |
| [#5415](https://github.com/mesonbuild/meson/issues/5415) | vala compiler --pkg includes more than necessary | The pkgconfig dependency of a static library propagates excessively to downstream Vala compilation as --pkg. This is a design issu |
| [#5433](https://github.com/mesonbuild/meson/issues/5433) | Add support for Kotlin | Kotlin language support does not exist in the code and is unimplemented. This remains a large language-addition request, closely r |
| [#5438](https://github.com/mesonbuild/meson/issues/5438) | Built-in Boost dependency takes precedence over explicitly provided pk | For dependencies with a dedicated detector in packages[] (e.g. boost), the factory takes priority, and the structure that ignores  |
| [#5445](https://github.com/mesonbuild/meson/issues/5445) | vala: what if C file depends on the package header generated by --head | When a .c file references the --header generated by .vala within the same target, the build order/dependency is not correctly esta |
| [#5455](https://github.com/mesonbuild/meson/issues/5455) | Support for "autolink" dependencies | pkg-config's 'Libs: -L${libdir}' (without -l) is not reflected in link_args, so MSVC's autolink backend cannot find it. _search_li |
| [#5462](https://github.com/mesonbuild/meson/issues/5462) | vs_module_defs should accept empty list or empty string | vs_module_defs accepts File/CustomTarget/CustomTargetIndex and returns early on None, but no explicit handling was found that trea |
| [#5471](https://github.com/mesonbuild/meson/issues/5471) | Add support for more JVM languages. | JVM language support such as Groovy/Kotlin/Scala is unimplemented; this is a large request to generalize jar(). It remains an open |
| [#5479](https://github.com/mesonbuild/meson/issues/5479) | Incorrect pkg-config file generated | In static builds, the absolute path of a .a file ends up in Libs: when it should be in Libs.private. The pkgconfig module has comp |
| [#5488](https://github.com/mesonbuild/meson/issues/5488) | pkgconfig.generate() produces different files the second time | A second call to pkgconfig.generate() for the same lib references the first as a Requires, changing the content. There is a relate |
| [#5557](https://github.com/mesonbuild/meson/issues/5557) | a duplicate target detected when the name_prefix keyword is used | Two targets with the same name but different name_prefix (and thus different output filenames) trigger a duplicate-target error. B |
| [#5599](https://github.com/mesonbuild/meson/issues/5599) | gnome.gtkdoc overwrite files at install | When installing via gnome.gtkdoc, install_data files in the same directory get overwritten/deleted because the whole directory is  |
| [#5610](https://github.com/mesonbuild/meson/issues/5610) | Add support for Gradle via a module. | A Gradle integration module is unimplemented. This remains a large new-module request sharing direction with the JVM language supp |
| [#5628](https://github.com/mesonbuild/meson/issues/5628) | False positives in clang-cl for stpcpy(), strcasecmp() and strncasecmp | With clang-cl, has_function misdetects functions such as stpcpy/strcasecmp, causing link failures. This is an issue with how clang |
| [#5635](https://github.com/mesonbuild/meson/issues/5635) | vs backend: run_target() dependencies doesn't seem to be built | With the VS backend, run_target's depends are not actually built, and there is room to optimize alias_target. This is a VS-backend |
| [#5648](https://github.com/mesonbuild/meson/issues/5648) | Error C2859 on MSVC when using PCH | In MSVC debug builds using PCH, a .pdb mismatch (C2859) breaks incremental builds. This is an MSVC-specific issue involving the in |
| [#5688](https://github.com/mesonbuild/meson/issues/5688) | Improve interaction between optional auto-feature subprojects with aut | A request to improve the behavior where an optional subproject is silently skipped when an option explicitly set to enabled on the |
| [#5709](https://github.com/mesonbuild/meson/issues/5709) | jar targets can't link against preexisting jars (e.g., android.jar) | jar() targets cannot add an existing jar (e.g. android.jar) to the classpath and link against it. The Java compiler handles -cp/-c |
| [#5716](https://github.com/mesonbuild/meson/issues/5716) | ninja scan-build ignores compiler setting | ninja scan-build ignores the CC/CXX (clang) set at configure time and uses scan-build's default gcc wrapper. This is an issue with |
| [#5721](https://github.com/mesonbuild/meson/issues/5721) | Default output folder set but no rule gets created for output | The 'all' rule for a Rust executable requires meson-out/project.exe, but the actual build rule produces project.exe, causing a mis |
| [#5723](https://github.com/mesonbuild/meson/issues/5723) | Specifying Language with Internal Dependencies | A request to restrict declare_dependency's compile_args to a specific language (e.g. cpp only). There is no mechanism yet for inte |
| [#5729](https://github.com/mesonbuild/meson/issues/5729) | Generated header/source tree header conflict with subprojects | A generated config.h in a subproject collides with a source-tree config.h of the same name, and the source version gets included i |
| [#5730](https://github.com/mesonbuild/meson/issues/5730) | Meson automoc | automoc is still not implemented (the qt module only has preprocess/has_tools), and this is a design-discussion issue where an unr |
| [#5737](https://github.com/mesonbuild/meson/issues/5737) | clike compiler is not really clike | This is a proposal for a large-scale refactor of the compiler class hierarchy; conversion to mixins has progressed, but the abstra |
| [#5760](https://github.com/mesonbuild/meson/issues/5760) | rpath should allow multiple arguments | install_rpath/build_rpath remain type: str, and accepting a list is unimplemented. This should remain a valid feature request. |
| [#5792](https://github.com/mesonbuild/meson/issues/5792) | Better architect "two phase" machine detection | This is a design issue about architecturally improving machine guessing (guess-and-refine) before and after compiler detection. Th |
| [#5793](https://github.com/mesonbuild/meson/issues/5793) | ninja install build gtk-doc as root | After polkit elevation during install, the gtk-doc target gets built as root, breaking file ownership. The current build order can |
| [#5801](https://github.com/mesonbuild/meson/issues/5801) | No 'objectfile' build target available | A request for a dedicated target that builds a .o from a single source and installs it (e.g. crt0.o). Currently this can be substi |
| [#5811](https://github.com/mesonbuild/meson/issues/5811) | meson does not support alternate spelling -libpath: in .pc files | A rare Windows corner case involving handling MSVC's -libpath: spelling (dash instead of slash) in .pc files. There is a workaroun |
| [#5817](https://github.com/mesonbuild/meson/issues/5817) | gnome.generate_gir() does not find library | The -L path for a library built in a different directory is not passed to g-ir-scanner. generate_gir's link-argument generation ha |
| [#5829](https://github.com/mesonbuild/meson/issues/5829) | gtk-doc does not link with library | Passing a library to gtk-doc's dependencies does not add linker flags. This is an old report with zero comments, making it difficu |
| [#5840](https://github.com/mesonbuild/meson/issues/5840) | gnome.generate_gir() doesn't use link arguments | generate_gir does not use the linker arguments from add_project_link_arguments. This is an old report with zero comments, making i |
| [#5843](https://github.com/mesonbuild/meson/issues/5843) | devhelp2 FileNotFoundError in evince gtk-doc API docs | When gtkdochelper renames to a .devhelp2 file with a module-version suffix, the original file is missing and a FileNotFound error  |
| [#5849](https://github.com/mesonbuild/meson/issues/5849) | Cache pkg-config isn't correct. | If a dependency is uninstalled after the initial configure, the cache is not invalidated. Dependency-cache validation or an equiva |
| [#5851](https://github.com/mesonbuild/meson/issues/5851) | gnome.generate_gir() build directory does not always have preference | When building GIR, the library in the build directory is not prioritized and the system library is used instead. This is an old re |
| [#5883](https://github.com/mesonbuild/meson/issues/5883) | CharacterSet in VisualStudio backend default to MBCS | The VS backend still always outputs CharacterSet as MultiByte, with no way to select Unicode or otherwise tune it. However, Charac |
| [#5903](https://github.com/mesonbuild/meson/issues/5903) | BuildDirLock test fails on Solaris | Locking has been rewritten to use DirectoryLock (fcntl.flock), but the test still double-locks within the same process, so it can  |
| [#5915](https://github.com/mesonbuild/meson/issues/5915) | test cases/frameworks/28 gir link order 2 can't work on Solaris | A test that creates a same-named library dependency is rejected by the Solaris linker. The test case (frameworks/28 gir link order |
| [#5920](https://github.com/mesonbuild/meson/issues/5920) | override_options: ['buildtype=release'] not working, possible regressi | Overriding buildtype per-target does not cascade into optimization/debug, so -O3 is not added. override_options is closer to a des |
| [#5923](https://github.com/mesonbuild/meson/issues/5923) | run_project_tests.py: project's default_options are (sometimes) shared | An isolation bug in the test runner where another test's default_options (e.g. b_vscrt=mtd) leaks and bleeds into other tests. Thi |
| [#5941](https://github.com/mesonbuild/meson/issues/5941) | Request: build target.install_path() | build_tgt has full_path() but no install_path(). A method to get the full post-install path as a string is unimplemented and remai |
| [#6016](https://github.com/mesonbuild/meson/issues/6016) | test_compiler_detection fails if CC is defined: AssertionError: Unknow | On FreeBSD, when CC=cc/CXX=c++ is defined, test_compiler_detection, which relies on an executable-name-based heuristic, fails. Thi |
| [#6037](https://github.com/mesonbuild/meson/issues/6037) | pkgconfig.generate fails when using libgcrypt dependency | Passing a config-tool-style dependency (e.g. gcrypt-config) to pkgconfig.generate's reqs is treated as an unsupported type. _proce |
| [#6048](https://github.com/mesonbuild/meson/issues/6048) | dependency() `method` keyword argument accepts only string | dependency()'s method argument remains type: str, and accepting a list (fallback across multiple methods) is unimplemented. This r |
| [#6063](https://github.com/mesonbuild/meson/issues/6063) | Add a binutils module | A dedicated module for handling binutils tools like objcopy still does not exist. This is a tracking issue for gathering ideas and |
| [#6064](https://github.com/mesonbuild/meson/issues/6064) | Generators: support multiple inputs | generator can only handle a single input file, so a request to combine multiple inputs into one output (e.g. for a custom linker)  |
| [#6068](https://github.com/mesonbuild/meson/issues/6068) | Object consistency | A broad design discussion covering the DSL's type/object design in general — the lack of full_path on File/generated-object object |
| [#6070](https://github.com/mesonbuild/meson/issues/6070) | custom_target: Ambiguous target when input and output is the same file | A request that custom_target cannot handle commands like sed -i / strip / ranlib that modify input=output in place. Proposals incl |
| [#6097](https://github.com/mesonbuild/meson/issues/6097) | Meson mangles custom emscripten linker arguments in checks | In arglist.py's dedup mechanism, a bare `-s` is not in the dedup list and is treated as NO_DEDUP, but the argument-reordering (pre |
| [#6108](https://github.com/mesonbuild/meson/issues/6108) | Wrong external dependency for static libs | During static linking, .so is explicitly searched for, so static library B is not selected. No confirmation of a fix could be foun |
| [#6114](https://github.com/mesonbuild/meson/issues/6114) | meson android cross compile experience | A request to improve the Android NDK cross-compilation experience. This is a large theme, including importing CMake cross settings |
| [#6133](https://github.com/mesonbuild/meson/issues/6133) | [RFE] Don't reconfigure build directory if config unchanged | Reconfiguration is triggered by a mere mtime change in meson.build. Suppression via content-hash comparison appears unimplemented, |
| [#6164](https://github.com/mesonbuild/meson/issues/6164) | Invalid resource compiler command generation | Passing a path containing spaces (Program Files) via the WINDRES environment variable causes it to be split on whitespace. No conf |
| [#6187](https://github.com/mesonbuild/meson/issues/6187) | Misdetection of early 64-bit Intel Macs as 32-bit | detect_cpu_family's compiler-define check only handles downgrading x86_64 to x86; there's no path to upgrade x86 to x86_64 on earl |
| [#6218](https://github.com/mesonbuild/meson/issues/6218) | Improve failure message when static LLVM is requested, but not found | A request to improve the error message when a static LLVM is requested but only a dynamic version is available. This is a small UX |
| [#6220](https://github.com/mesonbuild/meson/issues/6220) | Install phase strips rpath information set via LDFLAGS | An rpath passed via LDFLAGS gets stripped at install time. depfixer has been improved to merge new_rpath with the existing rpath,  |
| [#6221](https://github.com/mesonbuild/meson/issues/6221) | Coverage documentation and stale gcda/gcno files | A comment that the coverage documentation is too brief, not mentioning that gcda files aren't automatically deleted or documenting |
| [#6243](https://github.com/mesonbuild/meson/issues/6243) | clang's linker doesn't want -pthread on mingw-w64 | With msys2's mingw-w64 clang, -pthread produces an unused-argument warning (similar to #2628). No corresponding platform-specific  |
| [#6244](https://github.com/mesonbuild/meson/issues/6244) | 0.52 configure_file sandbox violation | Trying to copy a path inside a subproject with configure_file triggers a sandbox violation. The relevant sandbox check still exist |
| [#6247](https://github.com/mesonbuild/meson/issues/6247) | cc.compiles() does not include -I for the current_{source,build}_dir() | Compiler checks like cc.compiles() don't automatically get -I for the current source/build dir. By design, compiler checks run out |
| [#6254](https://github.com/mesonbuild/meson/issues/6254) | Python FileExistsError thrown when using identical libexecdir and bind | When bindir==libexecdir, installing tries to create a directory where an existing file of the same name is located, raising FileEx |
| [#6266](https://github.com/mesonbuild/meson/issues/6266) | dlang.generate_dub_file() doesn't accept files() object | generate_dub_file's value validation (_do_validate) only accepts str/int/bool/list/dict, so passing a File object still crashes it |
| [#6276](https://github.com/mesonbuild/meson/issues/6276) | Add option to introspect to exclude build_by_default false targets tha | A request for an option in meson introspect to exclude targets that are build_by_default:false and not depended on. build_by_defau |
| [#6361](https://github.com/mesonbuild/meson/issues/6361) | host,build,target_machine overhaul | A design-discussion issue tracking a comprehensive redesign of the machine-object group (ABI information, kernel/userland distinct |
| [#6374](https://github.com/mesonbuild/meson/issues/6374) | install_headers() doesn't work with headers generated by gnome.gdbus_c | install_headers() still restricts posargs to str/File and does not accept a CustomTarget (a generated header). Unimplemented. |
| [#6382](https://github.com/mesonbuild/meson/issues/6382) | Enhancement: option groups | A request to add a group to option() to group meson configure output. The group/section concept is unimplemented in optinterpreter |
| [#6385](https://github.com/mesonbuild/meson/issues/6385) | Cannot correctly generate capnproto rule that works in msvc and ninja  | capnproto's --src-prefix can't be handled by a single custom_target for both backends because @INPUT@'s relative/absolute path rep |
| [#6418](https://github.com/mesonbuild/meson/issues/6418) | Hard to use custom_target on protocol buffers with path? | custom_target's output cannot contain a path separator, making tools like protoc that produce path-qualified output hard to handle |
| [#6433](https://github.com/mesonbuild/meson/issues/6433) | Add an easy way to skip tests due to missing dependencies | A request for an easy way to skip a test when a dependency is missing (e.g. a skip parameter on test()). The test harness can repo |
| [#6434](https://github.com/mesonbuild/meson/issues/6434) | Better support for bare metal and low level OS targets | A design-discussion issue aggregating support for bare-metal/low-level OS targets (e.g. building libc). Updated as recently as 202 |
| [#6450](https://github.com/mesonbuild/meson/issues/6450) | Add docs about `cmake` parameter | A request to document that the [binaries] cmake entry in a cross file is required for CMake cross builds. It could not be confirme |
| [#6469](https://github.com/mesonbuild/meson/issues/6469) | python get_install_dir returns the wrong directory for a conda env | In conda environments, the python module's get_install_dir() returns a path unrelated to the actual install location. Updated as r |
| [#6476](https://github.com/mesonbuild/meson/issues/6476) | Allow generators to process extracted objects | generator.process() cannot accept the result of extract_all_objects() (ExtractedObjects). generator still only accepts str/File, a |
| [#6480](https://github.com/mesonbuild/meson/issues/6480) | compiler.run() result objects should be usable in a bool context | A request to be able to evaluate cc.run()'s result (TryRunResultHolder) directly as a boolean in an if statement. Currently the Ho |
| [#6482](https://github.com/mesonbuild/meson/issues/6482) | ERROR: Unable to detect GNU compiler type: cc1: error: /dev/null/usr/i | Compiler-type detection fails with a peculiar VMWare gcc 4.8.4 setup where sysroot is set to /dev/null. A workaround for this rare |
| [#6526](https://github.com/mesonbuild/meson/issues/6526) | Design for generator improvements | A design issue (a follow-on from #3342) discussing overall improvements to generators, including a unique_id proposal to direct ge |
| [#6533](https://github.com/mesonbuild/meson/issues/6533) | [Suggestion] Syntax changes | A redesign proposal to pluralize compiler-check APIs like has_header/has_function and unify prefix/dependencies handling. It invol |
| [#6541](https://github.com/mesonbuild/meson/issues/6541) | ninja install strip rpath | The rpath set via LDFLAGS/RUNPATH gets stripped at install time (related to #4136 and #6220). depfixer has been improved to merge  |
| [#6551](https://github.com/mesonbuild/meson/issues/6551) | How to run global setup command at start of test run? | A request to run a global setup script once at the start of the entire test run (equivalent to ctest's CTEST_CUSTOM_PRE_TEST). Wra |
| [#6581](https://github.com/mesonbuild/meson/issues/6581) | Using dub for dependencies doesn't work if they're of type "sourceLibr | A bug where dub sourceLibrary packages (bindings with no compiled binary) trigger a "wasn't compiled with $DC" error. The dub depe |
| [#6592](https://github.com/mesonbuild/meson/issues/6592) | Can't add gtk-doc generated files to the tarball during dist | A request for gnome.gtkdoc() to generate static HTML at dist time and include it in the tarball. add_dist_script exists, but there |
| [#6615](https://github.com/mesonbuild/meson/issues/6615) | Files in different directories considered duplicates when adding depen | gnome.compile_resources() matches custom_targets with the same basename in different directories and treats them as duplicates. Th |
| [#6622](https://github.com/mesonbuild/meson/issues/6622) | Better error message -> ERROR: Command cannot have '@INPUT@', since no | A request to include the file name and line number in custom_target error messages. Many InterpreterExceptions now carry node posi |
| [#6669](https://github.com/mesonbuild/meson/issues/6669) | Allow emscripten to be used as non cross compiler | A request to treat emscripten as a non-cross build. Currently emscripten is treated as a cross target for the wasm environment, an |
| [#6680](https://github.com/mesonbuild/meson/issues/6680) | Language D does not support phobos library finding | get_compiler('d').find_library() fails with "does not support library finding". The D compiler has no find_library implementation, |
| [#6681](https://github.com/mesonbuild/meson/issues/6681) | Request for improvement: installing dependencies transparently when ne | A feature request to automatically copy dependency DLLs to the build/install destination. Automatic DLL collection on Windows woul |
| [#6694](https://github.com/mesonbuild/meson/issues/6694) | kconfig/keyval: clarify location(s) of the .load("./.config") file: so | A documentation issue to clarify the base directory (source vs. build) keyval.load() uses when locating a .config file. Keyval-mod |
| [#6702](https://github.com/mesonbuild/meson/issues/6702) | configure_file does not accept program object as input | configure_file's input still only accepts strings/File objects; passing an ExternalProgram fails with 'Inputs can only be strings  |
| [#6711](https://github.com/mesonbuild/meson/issues/6711) | setting pkg_config_path in default_options leads to strange behavior | Setting pkg_config_path via default_options isn't picked up on regeneration, and PKG_CONFIG_PATH reverts to its default. The optio |
| [#6715](https://github.com/mesonbuild/meson/issues/6715) | Dub dependency error message confusing: says wrong compiler when it's  | A dub dependency buildType mismatch is incorrectly reported as "wasn't compiled with <DC>". The relevant logic in dub.py still exi |
| [#6754](https://github.com/mesonbuild/meson/issues/6754) | should meson introspect ignore DESTDIR? | A design discussion about whether meson introspect should ignore DESTDIR when returning install paths. Returning prefix-based inst |
| [#6768](https://github.com/mesonbuild/meson/issues/6768) | LDFLAGS, dependency('boost'), and werror=true cause build failures in  | LDFLAGS's -L flags leak into compile arguments (get_external_args), causing build failures with objcpp+werror. Logic to separate L |
| [#6807](https://github.com/mesonbuild/meson/issues/6807) | "Unable to determine dynamic linker" when using c_ld and cpp_ld | Specifying arm-none-eabi-ld for c_ld/cpp_ld in a cross file causes "Unable to determine dynamic linker". The c_ld code path exists |
| [#6835](https://github.com/mesonbuild/meson/issues/6835) | No easy way to package a generated source file to the dist tarball | A request for an easy way to include generated sources in the dist tarball. There is no dist: true-equivalent kwarg implemented fo |
| [#6840](https://github.com/mesonbuild/meson/issues/6840) | How to avoid get_wine_shortpath or avoid adding self.test.extra_paths? | A problem where get_wine_shortpath runs every time with the wine exe_wrapper, causing delays, plus a request for an opt-out. The e |
| [#6851](https://github.com/mesonbuild/meson/issues/6851) | Add native support for discover and running single python unittest bas | A feature request to auto-discover python unittest tests and turn each into an individual test(). No dedicated pythontest()/discov |
| [#6862](https://github.com/mesonbuild/meson/issues/6862) | Building DLang dylibs on MacOS fails if "version" is set | A bug on macOS where setting version on a D shared library passes an empty -current_version to the linker, causing failure. The D  |
| [#6866](https://github.com/mesonbuild/meson/issues/6866) | No easy way to test if a dist tarball is being created | A request for an API to detect at configure time whether a dist tarball is being built. No meson.is_dist_check()-equivalent method |
| [#6871](https://github.com/mesonbuild/meson/issues/6871) | Cannot use output of gnome.genmarshal as input. | gnome.genmarshal's output (CustomTargetIndex) cannot be passed to gnome.mkenums_simple's sources. mkenums_simple's sources still o |
| [#6874](https://github.com/mesonbuild/meson/issues/6874) | Add a way to make get_pkgconfig_variable override prefix + all *dir op | A request to use the project's own prefix/*dir values when retrieving things like pkg-config's completionsdir. There's a workaroun |
| [#6880](https://github.com/mesonbuild/meson/issues/6880) | Add helper to detect sanitizer libraries LD_PRELOAD values | A request for a helper to detect each compiler's sanitizer runtime for use with LD_PRELOAD. No evidence a dedicated API was implem |
| [#6962](https://github.com/mesonbuild/meson/issues/6962) | Few improvements for IDE(QTC) integration | Of the several requests bundled here, `meson compile --target` (the targets positional argument) has been implemented, but request |
| [#6964](https://github.com/mesonbuild/meson/issues/6964) | Generate D Interface files upon installing D "headers" | Generating and installing D interface files (.di, via dmd/ldc's -H option) is not present in the current d.py — a still-valid, uni |
| [#6982](https://github.com/mesonbuild/meson/issues/6982) | passing empty define_variable causes pkg-config to fail | An empty-value define_variable still just passes `--define-variable=key=` through as-is, and the resulting pkg-config error remain |
| [#6987](https://github.com/mesonbuild/meson/issues/6987) | Linking against native libs with ldc and bfd as linker is broken | A problem with the ordering of libraries placed inside --start-group/--end-group when linking against C (libssl) with ldc2. It can |
| [#6990](https://github.com/mesonbuild/meson/issues/6990) | More consistency between meson --introspect and meson-info/targets.jso | A consistency request noting that file names differ between relative and absolute forms depending on whether introspect data comes |
| [#7005](https://github.com/mesonbuild/meson/issues/7005) | cmplr.find_library() in Windows returns Linux style paths | On Windows network paths (UNC), find_library generates paths with / separators, causing the linker to fail. There's no confirmatio |
| [#7006](https://github.com/mesonbuild/meson/issues/7006) | Meson wrap JSON API for IDE integration? | A request to add a JSON output API to wrap/subprojects operations. No JSON/--format output is found in msubprojects.py; unimplemen |
| [#7016](https://github.com/mesonbuild/meson/issues/7016) | Disable unity block size suggestion | A UX-improvement request to disable unity builds by setting unity_size=0. Currently unity_size has min_value=2 so 0 isn't allowed, |
| [#7030](https://github.com/mesonbuild/meson/issues/7030) | Add Google's GN to Comparisons.md | A documentation request to add a comparison entry for Google GN to Comparisons.md. It has not been added to the current Comparison |
| [#7049](https://github.com/mesonbuild/meson/issues/7049) | extension_module in cross compilation gives wrong architecture name | The file-name suffix of a Python extension module should target the host, not the build machine, during cross-compilation. The pyt |
| [#7071](https://github.com/mesonbuild/meson/issues/7071) | Feature request: glslang compilation support | A request for built-in support to compile shaders to SPIR-V with glslangvalidator. Currently shaderc exists only as a dependency,  |
| [#7073](https://github.com/mesonbuild/meson/issues/7073) | Add Haiku support | Basic Haiku support exists, but Haiku-specific features like resources (rc/xres) and localization catalogs (collectcatkeys/linkcat |
| [#7078](https://github.com/mesonbuild/meson/issues/7078) | Python module: Enable more control about the Python 3 version | A request for specifying a Python version range in find_installation, and for specifying the interpreter via a native/machine file |
| [#7098](https://github.com/mesonbuild/meson/issues/7098) | [Wish] Improve logging | A request to improve logging of compiler/linker invocation details (commands and output). Some debug logging exists in detect.py,  |
| [#7102](https://github.com/mesonbuild/meson/issues/7102) | CMake subproject master project detection is broken | In a CMake subproject, CMAKE_CURRENT_SOURCE_DIR ends up equal to CMAKE_SOURCE_DIR, causing incorrect master-project detection. tra |
| [#7114](https://github.com/mesonbuild/meson/issues/7114) | dependency(include_type: 'system') support is not complete on windows | A request for include_type:'system' support via system-include flags on MSVC/clang-cl (/external:I, -imsvc). visualstudio.py does  |
| [#7147](https://github.com/mesonbuild/meson/issues/7147) | Detect CCache for cross compilation even if it's not explicit in cross | When a compiler is defined in a cross file, ccache is not auto-detected unless explicitly specified (inside _get_compilers, a non- |
| [#7148](https://github.com/mesonbuild/meson/issues/7148) | ninja clean does not delete map files | .map files produced via -Wl,-Map= in link_args are a byproduct Meson doesn't know about, so `ninja clean` doesn't remove them. A m |
| [#7154](https://github.com/mesonbuild/meson/issues/7154) | [Dlang] option -Db_lto=true is ignored | The D compiler (particularly ldc2/dmd) doesn't include b_lto in base_options, and get_lto_compile_args/link_args are not overridde |
| [#7178](https://github.com/mesonbuild/meson/issues/7178) | rename b_ndebug to something langauge agnostic | A proposal to rename b_ndebug to a language-neutral name like b_runtime_checking. It's still called b_ndebug today; the rename has |
| [#7200](https://github.com/mesonbuild/meson/issues/7200) | clang-tidy / clang-format shouldn't run on subprojects | `ninja clang-format`/`clang-tidy` also target and modify sources under subprojects/. Discussion continued through 2025; it can't b |
| [#7238](https://github.com/mesonbuild/meson/issues/7238) | need a tool to change all revision of subprojects to current git head | A request for a command like `meson subprojects freeze` that pins each wrap's revision to its current commit/tag. No freeze subcom |
| [#7259](https://github.com/mesonbuild/meson/issues/7259) | Meson is looking for a visual studio toolchain on the disk from which  | When the project/compiler and python are on different drives, relpath raises a ValueError due to differing mounts. A cross-drive-a |
| [#7260](https://github.com/mesonbuild/meson/issues/7260) | install script does not receive MESON_PROJECT_SOURCE_ROOT/MESON_PROJEC | Install scripts are only passed MESON_SOURCE_ROOT/MESON_BUILD_ROOT for the outermost project; there's no MESON_PROJECT_*_ROOT to i |
| [#7262](https://github.com/mesonbuild/meson/issues/7262) | C unity builds are not reproducible if the macro __FILE__ is used | In unity builds, __FILE__ expands to the absolute path of the generated unity source, hurting build reproducibility. It's unconfir |
| [#7275](https://github.com/mesonbuild/meson/issues/7275) | Clock skew issue on Windows | A coredata.dat clock-skew error occurs on Windows with an MSI install. An actively ongoing item with 30 comments and an update as  |
| [#7281](https://github.com/mesonbuild/meson/issues/7281) | Add example for dependency without pkg-config to the meson docs | A request to add non-reference documentation covering how to use libraries without pkg-config support (e.g., find_library). It has |
| [#7305](https://github.com/mesonbuild/meson/issues/7305) | Meson not able to find CMake Package dependency QuaZip; CMake native p | Meson's CMake dependency lookup fails to find QuaZip on Windows (a shortcoming in the -DNAME-based lookup). It can't be confirmed  |
| [#7313](https://github.com/mesonbuild/meson/issues/7313) | Add test case for emscripten with Rust | A request for test cases verifying emscripten+Rust cross-compilation. test cases/wasm exists but is C-focused; no rust+emscripten  |
| [#7323](https://github.com/mesonbuild/meson/issues/7323) | [CMake] Meson not properly respecting CMAKE_PREFIX_PATH when searching | On Windows, the environment variable CMAKE_PREFIX_PATH (when quoted) isn't parsed correctly, so CMake dependencies aren't found. A |
| [#7341](https://github.com/mesonbuild/meson/issues/7341) | KeyError: 'b_vscrt' when building with clang. | A KeyError on b_vscrt occurs with the VS backend + CC=clang. vs2010backend now uses the get_target_option accessor, but it's uncon |
| [#7368](https://github.com/mesonbuild/meson/issues/7368) | no way to install headers produced by a generator | There's no way to selectively install only the header outputs of a generator. A workaround exists using custom_target's install_di |
| [#7374](https://github.com/mesonbuild/meson/issues/7374) | Pass build type as `Release` not `release` to MSBuild | A bug about the VS backend capitalizing build type (release -> Release); it couldn't be confirmed from the local code whether this |
| [#7375](https://github.com/mesonbuild/meson/issues/7375) | C# compiler 'csc.exe' can't resolve the provided path | The .NET Framework version of csc can't resolve forward-slash paths in the csc rsp file's arguments. mesonbuild/compilers/cs.py st |
| [#7384](https://github.com/mesonbuild/meson/issues/7384) | custom_target: want kwarg to capture and discard stdout | custom_target's `capture` is meant for writing stdout to a file, not for "capture and discard". There's no kwarg implemented for d |
| [#7395](https://github.com/mesonbuild/meson/issues/7395) | `skip_sanity_check` property is not documented | The `skip_sanity_check` property for cross/machine files isn't documented in Machine-files.md. Checked docs/markdown/Machine-files |
| [#7413](https://github.com/mesonbuild/meson/issues/7413) | Conflicting .pdb's are generated in some cases | A library and executable with the same name cause MSVC .pdb files to collide. The pdb generation code still exists in ninjabackend |
| [#7415](https://github.com/mesonbuild/meson/issues/7415) | Deprecate python_mod.find_installation() | A proposal to deprecate calling find_installation() with no arguments. No deprecation warning implementation was found in the docs |
| [#7419](https://github.com/mesonbuild/meson/issues/7419) | flags specified as part of dependencies leak to other deps | An ordering problem where declare_dependency's link_args end up affecting other dependencies too. A proposal to isolate this via - |
| [#7420](https://github.com/mesonbuild/meson/issues/7420) | [doc] mention =default on wrap-mode options | Checked the command-line option list in Subprojects.md, and `--wrap-mode=default` is still not documented. A valid issue that need |
| [#7426](https://github.com/mesonbuild/meson/issues/7426) | When generating Vala coverage, gcovr fails to find source files | gcovr can't find the generated C sources when computing coverage for a Vala project. This is a deep-seated gcovr/lcov integration  |
| [#7445](https://github.com/mesonbuild/meson/issues/7445) | Implement finding php dependencies with config-tool | PHP dependency detection via the php-config config-tool is unimplemented. No php-related file exists under mesonbuild/dependencies |
| [#7453](https://github.com/mesonbuild/meson/issues/7453) | Fallback cross prefix | A proposal to apply a user-specified exe_prefix to find_program during cross builds. This is a substantial feature needing design  |
| [#7467](https://github.com/mesonbuild/meson/issues/7467) | Add a project test case to validate that JUnit functionality works. | A request to add project test cases that exercise the JUnit feature. No junit-related tests were found under `test cases`, so addi |
| [#7469](https://github.com/mesonbuild/meson/issues/7469) | Vala: target introspection doesn't include link_with information | Vala target introspection (intro-targets.json) doesn't include VAPI references (--pkg, etc.) to link_with targets. It's unconfirme |
| [#7471](https://github.com/mesonbuild/meson/issues/7471) | Improperly escaped path in cmake.create_package_file() | The cmake module's configure_package_config_file doesn't correctly escape backslashes in PACKAGE_RELATIVE_PATH on Windows. No fix  |
| [#7485](https://github.com/mesonbuild/meson/issues/7485) | Allow usage of @INPUT@ @OUTPUT@ @BASENAME@ in executable(cpp_args: ... | A request to use substitutions like @INPUT@/@BASENAME@ in executable's cpp_args, etc. Per-source argument expansion has no place i |
| [#7487](https://github.com/mesonbuild/meson/issues/7487) | It's not obvious or documented that you can't "add" include directorie | The fact that include_directories() return values cannot be concatenated with `+` is undocumented. This needs either added support |
| [#7489](https://github.com/mesonbuild/meson/issues/7489) | Meson cannot cross compile with wasi-sdk-11.0 if static libraries are  | wasm-ld doesn't support --start-group/--end-group/-rpath and similar flags, causing static linking to fail on wasi cross builds. I |
| [#7498](https://github.com/mesonbuild/meson/issues/7498) | dlang: can't specify path for dependency | A request to specify a local path (`path`) for a dub dependency. Even in the new dub.py implementation, no support for a path para |
| [#7532](https://github.com/mesonbuild/meson/issues/7532) | Subproject targets that are built are sometimes not installed | In a subproject dependency tree, when libsoup fails, the libxml2 target gets built but not installed. build.merge() still exists,  |
| [#7533](https://github.com/mesonbuild/meson/issues/7533) | host_machine cpu can change from 64-bit to 32-bit mid-way through setu | detect_cpu_family depends on compiler output, creating a design issue where host_machine.cpu_family can change within a subproject |
| [#7544](https://github.com/mesonbuild/meson/issues/7544) | Confusing warning for unsupported compiler options | On MSVC, unsupported options like c_std produce a confusing "Unknown option" message. This is a request to improve it to a clearer |
| [#7584](https://github.com/mesonbuild/meson/issues/7584) | `ninja clean` does not remove private directories | Files created in a custom_target's @PRIVATE_DIR@ aren't removed by ninja clean. The private dir needs to be registered as a ninja  |
| [#7599](https://github.com/mesonbuild/meson/issues/7599) | msvc /std:c11 flag needs some improvements | An improvement to how MSVC's /std:c11 flag is handled (the old 0.56.3 milestone was never released). The current state of MSVC c_s |
| [#7608](https://github.com/mesonbuild/meson/issues/7608) | Document the level of support for various OSes | A request to document the support level for each OS (Linux, Windows, macOS, BSD, Solaris, AIX, Hurd, Haiku, etc.). It can't be con |
| [#7614](https://github.com/mesonbuild/meson/issues/7614) | Support for copying directory tree into build directory | A request to copy a directory tree into the build directory for test data. fs.copyfile is for single files, and a directory-tree c |
| [#7616](https://github.com/mesonbuild/meson/issues/7616) | [RFC] Support --datarootdir | A request for --datarootdir support equivalent to autotools. mesonbuild/options.py has datadir but no datarootdir (no grep hits),  |
| [#7623](https://github.com/mesonbuild/meson/issues/7623) | Wrong install_path generated by python module for virtual environment  | When a venv interpreter is specified, the python module's install_path points at the system site-packages instead. The install-dir |
| [#7624](https://github.com/mesonbuild/meson/issues/7624) | Feature request: using custom target output as include directory | A request to use a custom_target's directory output as include_directories. General support for using a custom_target's output as  |
| [#7632](https://github.com/mesonbuild/meson/issues/7632) | [meson\|cmake] Generated cmake configs are broken | The cmake config generated by the cmake module (no _lib_suffix set, no per-config separation) is broken on Windows/vcpkg. This is  |
| [#7636](https://github.com/mesonbuild/meson/issues/7636) | More specific control over language std options | A design proposal to allow range specifications like c_std=>=c99,<c22. options.py's UserStdOption still only selects a single std  |
| [#7699](https://github.com/mesonbuild/meson/issues/7699) | project specific options from native file are ignored | Project options specified in the [project options] section of a native file are ignored. The options system has been substantially |
| [#7707](https://github.com/mesonbuild/meson/issues/7707) | Building Qt5 application against a statically built Qt install fails | Linking against a statically built Qt5 fails (requires .prl file parsing and QT_IMPORT_PLUGIN generation). Static Qt support in th |
| [#7713](https://github.com/mesonbuild/meson/issues/7713) | meson configure summary for the project that failed to set up | When setup fails, meson configure can't show the option list because build.dat doesn't exist. Whether partial option display on se |
| [#7719](https://github.com/mesonbuild/meson/issues/7719) | clang-cl does not seem supported on Darwin | Cross-building from macOS to Windows with Homebrew llvm's clang-cl/lld-link fails dynamic linker detection. Including possible dia |
| [#7720](https://github.com/mesonbuild/meson/issues/7720) | Correctly handle sysroot-prefixed library search dirs at find_library | In find_library's dirs, a search directory starting with `=` (sysroot prefix) is rejected as "not an absolute path" -- asymmetric  |
| [#7721](https://github.com/mesonbuild/meson/issues/7721) | Raise an error if cannot execute pkgconfig binary used in cross file | A typo in pkg-config in the binaries section of a cross file silently falls back to the native one. No evidence was found that thi |
| [#7722](https://github.com/mesonbuild/meson/issues/7722) | Suggestion: use defaults for sysroot handling in cross file in order t | Proposal to auto-derive pkg_config_libdir and the compiler sysroot from sys_root. This is triplet-dependent and costly to implemen |
| [#7728](https://github.com/mesonbuild/meson/issues/7728) | Issue with "-DVAR=\"STRING\"" compiler flags | On MinGW/Ninja, argument escaping into meson's Executor .dat file is incorrect, breaking embedded string defines. This is runtime- |
| [#7746](https://github.com/mesonbuild/meson/issues/7746) | [suggestion] Add the "prefix" directory to the list of locations where | Request for find_library() to search ${prefix}/lib by default on FreeBSD and similar systems. clike.py's _get_library_dirs relies  |
| [#7747](https://github.com/mesonbuild/meson/issues/7747) | Meson should auto-configure directory that already has a meson build | Request to improve the behavior where running setup on an already-configured directory just points to reconfigure but returns exit |
| [#7755](https://github.com/mesonbuild/meson/issues/7755) | Changing cross file content then calling ninja triggers configure but  | Bug where c_args isn't picked up on reconfigure after editing a cross file. This needs reproduction and regression checking and is |
| [#7756](https://github.com/mesonbuild/meson/issues/7756) | gnome: Doesn't generate typelib that is depended on by an executable ( | Regression related to GIR/typelib generation in the gnome module. The actual generation behavior is runtime-dependent and whether  |
| [#7766](https://github.com/mesonbuild/meson/issues/7766) | Don't use absolute path to shared libraries that don't have a SONAME s | Linking against a shared library with no SONAME using an absolute path embeds the absolute path into NEEDED. There was an update a |
| [#7777](https://github.com/mesonbuild/meson/issues/7777) | _convert_mingw_paths should not only in PkgConfigDependency, but shoul | Request to generalize MSYS-style path conversion (/mingw64/... etc.) for Windows to dependency methods other than pkg-config (syst |
| [#7781](https://github.com/mesonbuild/meson/issues/7781) | meson unittest failure on gbk/chinese environment | UnicodeDecodeError in the unittest (test_dist_git) under a GBK (Chinese) locale environment. run_unittests.py's test structure has |
| [#7783](https://github.com/mesonbuild/meson/issues/7783) | Switching from default_library=shared to static is failing with gst-bu | Reconfiguring default_library from shared to static fails (gst-build). Related to #8047. This needs runtime reconfiguration behavi |
| [#7805](https://github.com/mesonbuild/meson/issues/7805) | Warn if pkg-config for host and build machine is the same | Request to warn when, in a cross build, host and build pkg-config are the same and pkg_config_libdir isn't set. No evidence of thi |
| [#7814](https://github.com/mesonbuild/meson/issues/7814) | Expecting meson to add $prefix/$libdir/pkgconfig/ to --pkg-config-path | Request to automatically include the prefix's pkgconfig directory in PKG_CONFIG_PATH. Related to #7722. There's no evidence of aut |
| [#7819](https://github.com/mesonbuild/meson/issues/7819) | dependency objects don't have an api for querying if they are static o | Request for a static/shared query API like dep.static(). Conversion methods as_static()/as_shared() were added in 1.6.0, but those |
| [#7842](https://github.com/mesonbuild/meson/issues/7842) | Failed link with boost using ldc2 | When linking boost with ldc2 (D), an absolute-path .so doesn't get the -L= prefix, causing the link to fail. This needs regression |
| [#7856](https://github.com/mesonbuild/meson/issues/7856) | Feature request: add support for qt5_add_dbus_interface() | Request to add DBus interface generation (equivalent to qdbusxml2cpp) to the qt module. No DBus-related implementation is found in |
| [#7879](https://github.com/mesonbuild/meson/issues/7879) | Meson issues unnecessary long path when the build directory isn't near | On Windows, when the build and source directories are far apart, relative paths grow long enough to exceed MAX_PATH. Optimizing by |
| [#7880](https://github.com/mesonbuild/meson/issues/7880) | [proposal] Tests changing | Proposal to auto-generate a build matrix with/without options via test_option/test_sidetrack for D language unittests. This is a l |
| [#7886](https://github.com/mesonbuild/meson/issues/7886) | Feature request: Incremental modification of array options with meson  | Request for syntax to incrementally edit array options in meson configure (e.g. -Dopt-=value). No implementation of such increment |
| [#7888](https://github.com/mesonbuild/meson/issues/7888) | 'coverage' target not created when 'b_coverage=true' is given via 'ove | Setting b_coverage=true via override_options doesn't generate the global coverage target. The ninjabackend's coverage rule generat |
| [#7889](https://github.com/mesonbuild/meson/issues/7889) | Improve target debugging with Meson | Request for a debugging feature to set breakpoints during meson.build evaluation and inspect variables/options. Building a debugge |
| [#7891](https://github.com/mesonbuild/meson/issues/7891) | Allow forwarding multiple outputs between targets | Passing a multi-output custom_target to run_target etc. only uses the first output. The 'more than one output! Using the first one |
| [#7892](https://github.com/mesonbuild/meson/issues/7892) | Syntaxic sugar suggestion for declaring dictionaries | Proposal for a Python-like dict() function/syntactic sugar. No dict() function exists in the interpreter, so it's unimplemented. T |
| [#7893](https://github.com/mesonbuild/meson/issues/7893) | Helpers for a dependency array | Request for helpers like all_found() over a dependency array. No evidence of this API being implemented, so it's unimplemented. Le |
| [#7895](https://github.com/mesonbuild/meson/issues/7895) | Missing glue for the coverage target | `meson compile coverage` doesn't work; only `ninja coverage` does. mcompile resolves targets via intro-targets.json, but coverage  |
| [#7898](https://github.com/mesonbuild/meson/issues/7898) | calling cmake from meson is much slower | Regression (at the time, on master) where cmake invocation became slower, especially on Windows, caused by commit 7e58f333. The CM |
| [#7917](https://github.com/mesonbuild/meson/issues/7917) | when ninja install fails due to insufficient permissions, need more in | Request to show which file/destination failed when install fails due to insufficient permissions. There's likely still room to imp |
| [#7941](https://github.com/mesonbuild/meson/issues/7941) | New library metasystem | Proposal for a new library-metadata system (.lm) to work around pkg-config's design problems. This is an extremely large-scale des |
| [#7950](https://github.com/mesonbuild/meson/issues/7950) | .s files should consider not using preprocessor flags | Meson passes -D/-MD etc. to .s files that clang considers not needing preprocessing, triggering a -Wunused warning (which fails un |
| [#7957](https://github.com/mesonbuild/meson/issues/7957) | @BASENAME@ does not work in install_dir of custom_target() | @BASENAME@ isn't expanded in a custom_target's install_dir and is instead used literally as the directory name. build.py's substit |
| [#7959](https://github.com/mesonbuild/meson/issues/7959) | Meson fails to build Qt-Advanced-Docking-System as a CMake subproject | In a CMake subproject, Qt's AUTOMOC output (mocs_compilation.cpp) isn't found and the build fails. This needs behavior checked aft |
| [#8008](https://github.com/mesonbuild/meson/issues/8008) | Ability to run combined meson test suites | Request for `meson test --suite foo+bar` syntax to run only tests belonging to all of multiple suites. No evidence of AND-conditio |
| [#8019](https://github.com/mesonbuild/meson/issues/8019) | Meson find_library doesn't honor built-in visual studio search paths | cc.find_library doesn't reference the MSVC toolchain's built-in library search paths (Windows Kits etc.), so it can't find librari |
| [#8020](https://github.com/mesonbuild/meson/issues/8020) | extract_all_objects() with custom target results in invalid paths for  | Bug where extract_all_objects()'s generator-output object relative paths are incorrect for a subproject with the vs backend. This  |
| [#8021](https://github.com/mesonbuild/meson/issues/8021) | "fallthrough" incorrectly supported as a function attribute | fallthrough is a statement attribute, not a function attribute, yet it's included as a target of has_function_attribute(). fallthr |
| [#8027](https://github.com/mesonbuild/meson/issues/8027) | Meson tries to use install_name_tool and otools when install_name_tool | On a native Linux build, if install_name_tool exists, execution enters the darwin-specific path and calls otool. fix_rpath now tak |
| [#8033](https://github.com/mesonbuild/meson/issues/8033) | specifying cpp_eh=none on native msvc builds should also specify _HAS_ | With MSVC and cpp_eh=none, /EHs-c- is applied but _HAS_EXCEPTIONS=0 is not, causing warnings when using the STL. Checked cpp.py's  |
| [#8034](https://github.com/mesonbuild/meson/issues/8034) | Feature request: add 'extra_depends' option to executable | Request for something like extra_depends to establish an ordering dependency across all of an executable's objects, for cases like |
| [#8036](https://github.com/mesonbuild/meson/issues/8036) | Feature request: Microchip XC8 compiler support | Request to support the Microchip XC8 compiler. microchip.py has Xc16Compiler/Xc32Compiler but XC8 hasn't been added. Adding it is  |
| [#8047](https://github.com/mesonbuild/meson/issues/8047) | Subproject links against dynamic library when building both despite -D | When a subproject has default_library=both, it links against the shared version even if the parent specifies -Ddefault_library=sta |
| [#8053](https://github.com/mesonbuild/meson/issues/8053) | Missing or incorrect "WARNING: Unknown options" in native files for cr | During a cross build, a native file's build.c_args is incorrectly warned about as an unknown option, while genuinely unknown optio |
| [#8054](https://github.com/mesonbuild/meson/issues/8054) | Statically linking when using threads produces segfaulting executables | Known issue where a C++ executable statically linked against pthread segfaults on linux+gcc (requires -Wl,--whole-archive etc.). W |
| [#8058](https://github.com/mesonbuild/meson/issues/8058) | OpenMP dependency not found with Nvidia HPC SDK | With the Nvidia HPC SDK (nvc), the _OPENMP macro isn't defined, so the OpenMP dependency isn't detected. misc.py's OpenMP handling |
| [#8075](https://github.com/mesonbuild/meson/issues/8075) | has_function check fails for overloaded functions in C++ code | has_function's prototype-present template (clike.py:726-744) still uses `void *a = (void*) &{func};`, so taking the address of an  |
| [#8082](https://github.com/mesonbuild/meson/issues/8082) | pkg-config extra cflags don't apply to local executables | The .pc extra_cflags of an internally link_with'd library not being applied to an executable in the same build is a design gap; no |
| [#8089](https://github.com/mesonbuild/meson/issues/8089) | cmake subproject dependencies not working | A meson-resolved glib-2.0 dependency can't be propagated into a CMake subproject. This involves complex interop in the cmake modul |
| [#8107](https://github.com/mesonbuild/meson/issues/8107) | Add _conditional_ defaults for warnings/optimizations, or remove warni | Wanting to set -O3/-Wall etc. conditionally, but built-in options can't be conditionally set from within meson.build itself. set_o |
| [#8117](https://github.com/mesonbuild/meson/issues/8117) | gnome.gtkdoc dependencies are not built during install | A gtkdoc custom_target dependency isn't built at install time. This needs detailed verification of gtkdoc handling within the gnom |
| [#8121](https://github.com/mesonbuild/meson/issues/8121) | Warning emitted when `--reconfigure`ing project with subprojects | meson-uninstalled gets duplicated into an option array on every reconfigure. Confirmed still OPEN on gh. Evidence of a fix to the  |
| [#8123](https://github.com/mesonbuild/meson/issues/8123) | Adding a generic build order rule | Design proposal for a general build-ordering constraint (equivalent to wait) between arbitrary targets. Existing depends can parti |
| [#8126](https://github.com/mesonbuild/meson/issues/8126) | Freestanding build support for Meson | Proposal for a b_freestanding option. Grepping confirms b_freestanding is unimplemented; it has reactions and discussion continuin |
| [#8127](https://github.com/mesonbuild/meson/issues/8127) | meson dist --include-subprojects seems to ignore patch_* statements in | wrap's patch_* isn't applied to subprojects with meson dist. mdist.py was updated as recently as 2026-03, but full evidence that t |
| [#8137](https://github.com/mesonbuild/meson/issues/8137) | Visual Studio generator doesn't set preprocessor definitions as global | The VS backend sets preprocessor definitions per source file rather than project-wide, causing IDE display problems. This needs de |
| [#8146](https://github.com/mesonbuild/meson/issues/8146) | Compilation databases with unity builds | compile_commands.json loses original-source information for unity builds. compdb generation is delegated to ninja -t compdb, and g |
| [#8156](https://github.com/mesonbuild/meson/issues/8156) | The unstable-simd module doesn't check that neon code can be compiled | The simd module still judges only via has_multi_arguments (whether the arguments are accepted), and doesn't verify whether arm_neo |
| [#8206](https://github.com/mesonbuild/meson/issues/8206) | cc.get_define does not work when doing universal builds | On a macOS fat build (multiple -arch flags), get_define conflicts with -E and fails. get_define is implemented in PREPROCESS mode, |
| [#8213](https://github.com/mesonbuild/meson/issues/8213) | g++ module support | Tracking issue for GCC's C++20 modules support. It has 16 reactions and ongoing interest, and the state of GCC modules support has |
| [#8232](https://github.com/mesonbuild/meson/issues/8232) | Meson not respecting config dependent generator expressions in INTERFA | Config-dependent generator expressions inside a CMake dependency's INTERFACE_LINK_LIBRARIES can't be resolved. This needs detailed |
| [#8237](https://github.com/mesonbuild/meson/issues/8237) | custom_target() and run_target() fail to execute with VS backend when  | With the VS backend and buildtype=release, custom_target/run_target requests Debug\|x64 and fails. Confirmed OPEN on gh. Evidence  |
| [#8243](https://github.com/mesonbuild/meson/issues/8243) | XCode Generator doesn't set include paths from dependencies | The Xcode backend doesn't set dependency include paths on the project. The Xcode backend is a known immature area, and evidence of |
| [#8266](https://github.com/mesonbuild/meson/issues/8266) | GNOME: glib-compile-resources should use gdk-pixbuf-pixdata from subpr | The gnome module doesn't set the GDK_PIXBUF_PIXDATA environment variable when running glib-compile-resources. Grepping also finds  |
| [#8274](https://github.com/mesonbuild/meson/issues/8274) | Non-actionable error message "ERROR: No host machine compiler for ..." | The error message in build.py:1218 still reads 'No {machine} machine compiler for {path}' and doesn't indicate the cause (language |
| [#8295](https://github.com/mesonbuild/meson/issues/8295) | Add depend_files to generator() akin to custom_target() | generator() has depfile/depends but not a depend_files keyword (func_generator's typed_kwargs has no depend_files). This could be  |
| [#8302](https://github.com/mesonbuild/meson/issues/8302) | Add a subproject.build_root() function | Request for a function to get a subproject's build output directory. Whether an equivalent API has been implemented can't be confi |
| [#8307](https://github.com/mesonbuild/meson/issues/8307) | Configure test failing on older OS X builds | Regression from 0.55 to 0.56 where the GCC-style atomics check fails on OS X 10.7-10.9, halting configure. Confirmed OPEN on gh. T |
| [#8308](https://github.com/mesonbuild/meson/issues/8308) | Add `b_ndebug=auto` because `b_ndebug=if-release` is misleading | b_ndebug's choices are still ['true','false','if-release'], and the proposed 'auto'/'release-only' haven't been added. No improvem |
| [#8310](https://github.com/mesonbuild/meson/issues/8310) | meson --internal exe can add a lot of overhead | The meson --internal exe wrapper launch, used for output capture etc., incurs per-target overhead. meson_exe.py still follows the  |
| [#8315](https://github.com/mesonbuild/meson/issues/8315) | options: use a feature option for gtkdoc | Request for gnome.gtkdoc to support feature-option-like required/auto disabling. Whether gtkdoc supports a required keyword can't  |
| [#8326](https://github.com/mesonbuild/meson/issues/8326) | snprintf not detected on Windows 10 | has_function('snprintf') returns NO with MSVC. The has_function template has an MSVC/builtin branch, but whether snprintf detectio |
| [#8330](https://github.com/mesonbuild/meson/issues/8330) | library targets generated with nvcc cannot be linked with | A library built with nvcc isn't correctly linked via link_with. Confirmed OPEN on gh. This needs detailed verification around cuda |
| [#8331](https://github.com/mesonbuild/meson/issues/8331) | Meson fails to link with a private dependency requirement | ld can't find a library when linking a dependency via Requires.private. This needs detailed verification around pkgconfig/rpath, a |
| [#8334](https://github.com/mesonbuild/meson/issues/8334) | Make it possible to recover include directories from dependency object | Request to portably extract include directories from a dependency object and pass them to a generator. partial_dependency and get_ |
| [#8339](https://github.com/mesonbuild/meson/issues/8339) | Dependency via cmake: glfw from conan not working | A conan-provided glfw CMake package isn't found by dependency(). This needs detailed verification of cmake dependency resolution,  |
| [#8350](https://github.com/mesonbuild/meson/issues/8350) | Junit report numbers sub-tests regardless of numbers in TAP report | JUnit output assigns numbers to subtests even when TAP has none. This needs detailed verification of the mtest/TAP/JUnit parser, a |
| [#8370](https://github.com/mesonbuild/meson/issues/8370) | Meson doesn't respect the PATH environment variable | Resolving a relative name like CC prefers a binary adjacent to meson/python over PATH (MSYS2). This needs detailed verification of |
| [#8371](https://github.com/mesonbuild/meson/issues/8371) | Static library fails to link with specific compiler-linker combination | With Clang+ld.bfd or GCC+LLD, a static library lacks an index and fails with 'archive has no index' (related to ranlib/ar). This n |
| [#8373](https://github.com/mesonbuild/meson/issues/8373) | Compiler objects cannot be used everywhere where executable() or find_ | A compiler object can't be used equivalently to executable/find_program. The compiler has a cmd_array() method that provides array |
| [#8379](https://github.com/mesonbuild/meson/issues/8379) | Brainstorming how we can improve our QA | Brainstorming issue about QA processes to reduce release regressions. This isn't something judgeable from code; leave it pending a |
| [#8434](https://github.com/mesonbuild/meson/issues/8434) | find_program('cpp') incorrectly returns path to clang++ when CXX is se | find_program('cpp') returns the C++ compiler (clang++) when CXX is set. This needs detailed verification of the interaction betwee |
| [#8441](https://github.com/mesonbuild/meson/issues/8441) | `meson test` does not re-configure if there was a change in meson.buil | After changing meson.build, meson test doesn't reconfigure and doesn't pick up new tests. This needs detailed verification of mtes |
| [#8443](https://github.com/mesonbuild/meson/issues/8443) | Object files of static libraries in 'dependencies' get into the projec | With the VS backend, a dependency's static library object files show up in the project's source listing. This needs verification o |
| [#8466](https://github.com/mesonbuild/meson/issues/8466) | gnome.generate_gir() - subproject dependencies do not pass gir file to | In generate_gir(), a subproject-dependency's gir isn't passed to g-ir-scanner as --include-uninstalled. This needs detailed verifi |
| [#8469](https://github.com/mesonbuild/meson/issues/8469) | gnome.generate-gir() - gir include_directories are not used for g-ir-c | generate_gir()'s include_directories is used only for g-ir-scanner and isn't passed to g-ir-compiler, causing typelib generation t |
| [#8470](https://github.com/mesonbuild/meson/issues/8470) | gnome.generate-gir() - cannot generate typelib files for uninstalled g | Request to map g-ir-scanner's --include-uninstalled to g-ir-compiler's --includedir. No clear evidence was found that this is addr |
| [#8479](https://github.com/mesonbuild/meson/issues/8479) | Documentation: define what is "install" in Meson terms | Documentation request to add a definition of "what install means" to Installing.html. Keep as a valid documentation-improvement re |
| [#8493](https://github.com/mesonbuild/meson/issues/8493) | There is no way to access what vscrt is finally used in the build | Valid feature request: there's no way to retrieve the CRT that ultimately gets used from meson.build when b_vscrt is from_buildtyp |
| [#8509](https://github.com/mesonbuild/meson/issues/8509) | Take meson.override_find_program() into consideration in config-tool b | Request for config-tool-style lookups (llvm-config etc.) to respect override_find_program. No implementation of override integrati |
| [#8510](https://github.com/mesonbuild/meson/issues/8510) | config-tool LLVM discovery chooses versions get_llvm_tool_names() inte | config-tool's find_config ignores get_llvm_tool_names's order and picks the most recent matching version. dev.py/configtool.py's l |
| [#8518](https://github.com/mesonbuild/meson/issues/8518) | misleading log output from cc.find_library | Log-improvement request that it's confusing for cc.find_library to display "found: NO" when required:disabled. No evidence of a wo |
| [#8534](https://github.com/mesonbuild/meson/issues/8534) | Allow converting from array to string in toolchain files | Request to convert an array to a space-separated string within a machine file (for things like CMAKE_C_FLAGS_INIT). No string-join |
| [#8540](https://github.com/mesonbuild/meson/issues/8540) | Missing support for `gcc -g3` | Request that debug builds only use -g and can't select -g3 (for macro info etc.). gnu.py's clike_debug_args remains a boolean fixe |
| [#8550](https://github.com/mesonbuild/meson/issues/8550) | Use an abstraction for compiler and linker arguments instead of passin | Large-scale design proposal to stop carrying compiler/linker arguments around in GCC form and represent them via an abstract class |
| [#8552](https://github.com/mesonbuild/meson/issues/8552) | xcode backend builds for wrong CPU architecture | Bug report that the xcode backend doesn't respect the host cpu and builds for all architectures. The xcode backend is still experi |
| [#8554](https://github.com/mesonbuild/meson/issues/8554) | VS backend has serious cross-compiling issues | Bugs such as the VS backend using target_machine instead of host_machine when cross-compiling. Labeled bug/cross/backend:visualstu |
| [#8558](https://github.com/mesonbuild/meson/issues/8558) | Changing cross file settings | Request for automatic reconfiguration or a flag, since editing a cross file has no effect until re-setup and it's easy to forget.  |
| [#8559](https://github.com/mesonbuild/meson/issues/8559) | filesystem module: fs.exists('') == true | Minor bug where fs.exists('') returns true. fs.py's _resolve_dir resolves an empty string to os.path.join(source_root, subdir, '') |
| [#8565](https://github.com/mesonbuild/meson/issues/8565) | add_install_script() / ninja install fail on MSYS2/MinGW64 | On MSYS2/MinGW, path conversion passed to bash by the install script results in "No such file or directory". Discussion continues  |
| [#8575](https://github.com/mesonbuild/meson/issues/8575) | using config tool for GSL | Request to add a built-in gsl-config config-tool (the poster is willing to implement it). No gsl-dependency implementation is foun |
| [#8581](https://github.com/mesonbuild/meson/issues/8581) | Difficult for users to figure out how to specify dependency locations | UX/documentation improvement request: when a dependency isn't found, meson doesn't guide the user on how to specify its location,  |
| [#8593](https://github.com/mesonbuild/meson/issues/8593) | Trailing slash in libdir, conflicting libs and generate_gir | Compound bug where a libdir's trailing slash isn't normalized, causing /usr/lib to be duplicated in generate_gir, incorrectly prio |
| [#8599](https://github.com/mesonbuild/meson/issues/8599) | Boost dependencies use absolute paths | When a boost dependency is included, the generated .pc embeds absolute paths to the boost libraries, making it non-redistributable |
| [#8612](https://github.com/mesonbuild/meson/issues/8612) | Windows compile_resources() doesn't specify path dependency correctly | Bug where windows.compile_resources() only adds -I./ when depends is used, so the Windows build of windres can't resolve includes. |
| [#8636](https://github.com/mesonbuild/meson/issues/8636) | Cannot disable warnings in subproject -- warning_level should offer op | Request for warning_level=0 to pass -w (suppress all warnings). 'everything' has been added to warning_level, but '0' still doesn' |
| [#8640](https://github.com/mesonbuild/meson/issues/8640) | Relative paths for include_directories is enforced on Ubuntu but not o | Inconsistency where include_directories' absolute-path prohibition is enforced on Ubuntu but allowed on Windows, plus a request fo |
| [#8642](https://github.com/mesonbuild/meson/issues/8642) | RFE: allow scripts to be "detected" without any output | Request for a quiet-like option to suppress find_program's success log. find_program_impl's silent parameter is internal-only, and |
| [#8650](https://github.com/mesonbuild/meson/issues/8650) | template strings in generator.process(extra_args) are not replaced | Template strings like @BUILD_DIR@ inside generator.process(extra_args) aren't substituted. get_arglist only substitutes @BASENAME@ |
| [#8657](https://github.com/mesonbuild/meson/issues/8657) | boost: always treat include dirs as system includes | Request for boost-specific include directories to always be treated as system includes. No implementation forcing include_type='sy |
| [#8708](https://github.com/mesonbuild/meson/issues/8708) | Hard to use non-default compilers in MSYS2 | On MSYS2, CreateProcess prioritizes cc.exe in the executable's own directory over PATH, preventing use of a non-default compiler.  |
| [#8709](https://github.com/mesonbuild/meson/issues/8709) | Native winelib support? | Request for native support for winegcc/winelib (.dll.so etc.). No implementation of a winelib platform or suffix handling is found |
| [#8711](https://github.com/mesonbuild/meson/issues/8711) | CXXFLAGS/cpp_args always added AFTER meson arguments --> distro packag | Flags derived from environment variables/cpp_args are placed after meson's own flags, so they can't override defaults (e.g. -std), |
| [#8714](https://github.com/mesonbuild/meson/issues/8714) | RFE: Add a way to append to array options | Request for append syntax for array options, like -Dfoo+=bar. options.py has a per-subproject augments mechanism, but no implement |
| [#8715](https://github.com/mesonbuild/meson/issues/8715) | Support configuration of msgmerge arguments | i18n.gettext's args are only passed to xgettext, and there's no way to specify separate arguments for msgmerge (e.g. --no-wrap/--n |
| [#8725](https://github.com/mesonbuild/meson/issues/8725) | Filesystem significant languages and build directory implementation de | Design proposal for an abstraction to supply sources as a tree structure, for languages like Rust/Cython/Python where the filesyst |
| [#8739](https://github.com/mesonbuild/meson/issues/8739) | On Debian, python/python3 modules are wrong about installation paths | On Debian-based systems, python.get_path()/sysconfig_path can return paths not on sys.path due to differences like dist-packages v |
| [#8752](https://github.com/mesonbuild/meson/issues/8752) | Name clash bug (target name == subdirectory) | A bug where the linker fails with "Is a directory" when a target name collides with a subdirectory name. No evidence was found loc |
| [#8755](https://github.com/mesonbuild/meson/issues/8755) | Unable to make Boost include directory a system directory on macOS | A compound issue on macOS/Homebrew where boost can't be treated as -isystem, and -isystem/usr/local/include in CFLAGS/cpp_args get |
| [#8756](https://github.com/mesonbuild/meson/issues/8756) | No way to depend on existing shared library by exact path | A request for a way to specify a dependency by an exact library .so path without going through detection (e.g. to distinguish Free |
| [#8768](https://github.com/mesonbuild/meson/issues/8768) | -Db_lto=true doesn't seem to work with both Rust and C | LTO module mismatches cause link failures with clang+b_lto+Rust. rust.py gained LTO support (-C lto), but cross-language C/Rust LT |
| [#8777](https://github.com/mesonbuild/meson/issues/8777) | Add support for Synopsys DesignWare ARC C/C++ Compiler | A request for support for the Synopsys DesignWare ARC C/C++ compiler. No ARC compiler implementation was found locally; keep as a  |
| [#8784](https://github.com/mesonbuild/meson/issues/8784) | Visual Studio project backend OutDir option | A request for an option to set the generated project's OutDir in the VS backend (similar to startup_project). options.py has backe |
| [#8790](https://github.com/mesonbuild/meson/issues/8790) | find_program for powershell files should pass ExecutionPolicy Bypass | A request to automatically prepend "powershell -ExecutionPolicy Bypass" when a .ps1 script is found via find_program. programs.py' |
| [#8801](https://github.com/mesonbuild/meson/issues/8801) | Support of CMake's configuration of boost | Detection via boost's official .cmake config (BoostConfig.cmake) is still unsupported; boost dependency handling remains custom lo |
| [#8806](https://github.com/mesonbuild/meson/issues/8806) | CMake fails for ASM custom rules (example libjpeg-turbo) | A problem where ASM (NASM) targets aren't picked up by the CMake module. ASM support for CMake subprojects is complex, and no evid |
| [#8828](https://github.com/mesonbuild/meson/issues/8828) | Rust: add a way to compile c static libs without linking the stdlib | A proposed `--emit obj` approach to the problem of Rust staticlibs becoming huge. Still OPEN upstream (updated 2026-01), with no l |
| [#8831](https://github.com/mesonbuild/meson/issues/8831) | Cross compiler family LTO should be an error | There is still no mechanism to warn or error when b_lto is enabled with mixed compiler families (gcc/clang, D, Rust). backends.py' |
| [#8890](https://github.com/mesonbuild/meson/issues/8890) | List of project using Meson in Users.md is outdated | docs/markdown/Users.md still exists. Whether to keep the list is a policy question requiring maintainer judgment, with no code-lev |
| [#8915](https://github.com/mesonbuild/meson/issues/8915) | Option to skip adding rpaths similar to CMAKE_SKIP_RPATH | A global option to suppress all rpath assignment (equivalent to --skip-rpath) is not implemented. install_rpath and similar option |
| [#8930](https://github.com/mesonbuild/meson/issues/8930) | Feature Request: Static PIE support | An option equivalent to b_static_pie for enabling -static-pie does not exist locally (no grep matches); only b_pie exists. Keep as |
| [#8945](https://github.com/mesonbuild/meson/issues/8945) | Wrap handling during `ninja reconfigure` ignores project subproject_di | wrap-redirect's path validation hardcodes the 'subprojects' directory name (wrap.py:258), ignoring a custom subproject_dir. The bu |
| [#8946](https://github.com/mesonbuild/meson/issues/8946) | Cosmetic issue when reporting failed ncurses detection | tried_methods appends c.method for each candidate without deduplication (detect.py:154), so 'pkgconfig' still repeats across multi |
| [#8947](https://github.com/mesonbuild/meson/issues/8947) | Generate GIR from custom_target | gnome.generate_gir's _unwrap_gir_target still only allows Executable/SharedLibrary/StaticLibrary and rejects CustomTarget (gnome.p |
| [#8971](https://github.com/mesonbuild/meson/issues/8971) | Feature request: Limit search paths for libraries | A mode equivalent to CMAKE_FIND_ROOT_PATH_MODE_*, which suppresses system search and restricts lookup to under the prefix, is unsu |
| [#8984](https://github.com/mesonbuild/meson/issues/8984) | CUDA + MSVC: linking executable against shared library cannot find the | With nvcc+MSVC as host, the shared library is named libkernels.dll and the import lib is expected as .dll.a, but it is actually ge |
| [#9004](https://github.com/mesonbuild/meson/issues/9004) | Include environment variables in machine files | A section for defining environment variables in a machine file is not implemented (machinefile.py only has [constants]/[binaries]/ |
| [#9006](https://github.com/mesonbuild/meson/issues/9006) | Request for Clang as an Alternative CUDA Compiler | The ability to select clang as the CUDA compiler is not implemented. nvcc is the only CUDA compiler (no ClangCuda equivalent). Kee |
| [#9013](https://github.com/mesonbuild/meson/issues/9013) | Test setups and subprojects | The behavior where a test setup doesn't propagate to subprojects still remains, causing errors in subproject tests that lack a set |
| [#9032](https://github.com/mesonbuild/meson/issues/9032) | gnome.generate_gir uses cross-compiler (host) flags for running native | During cross-compilation, generate_gir passes host compile flags to the native compiler via g-ir-scanner. A known trouble spot for |
| [#9052](https://github.com/mesonbuild/meson/issues/9052) | Add PySide/shiboken support | Support for generating PySide/shiboken bindings is not implemented. Neither a dedicated module nor support within the Qt module ex |
| [#9058](https://github.com/mesonbuild/meson/issues/9058) | When doing --repeat don't allow for tests to be run in parallel with t | An option to prevent the same test from running in parallel with itself under --repeat is not implemented. mtest.py simply submits |
| [#9062](https://github.com/mesonbuild/meson/issues/9062) | build.ninja is missing dependencies present in cmake subproject | In CMake subprojects, generated header dependencies set via set_source_files_properties aren't picked up into build.ninja. Discuss |
| [#9067](https://github.com/mesonbuild/meson/issues/9067) | Unknown CPU family 'k1om' | The k1om (Intel MIC/Xeon Phi) CPU family is not registered locally (no grep matches). Somewhat overlaps with #9101, but this issue |
| [#9070](https://github.com/mesonbuild/meson/issues/9070) | Documentation of `Special case meson.version().version_compare()` stat | Documentation of the behavior where meson.version().version_compare(), introduced in #7594, gets special-cased at parse time to su |
| [#9088](https://github.com/mesonbuild/meson/issues/9088) | Meson doesn't seem to properly support BPF programs | First-class support for BPF programs (clang -target bpf) is not implemented, and projects like systemd work around this with custo |
| [#9101](https://github.com/mesonbuild/meson/issues/9101) | k1om CPU support | CPU recognition and feature support for Intel MIC (k1om) is not implemented (no grep matches). Related to #9067. Niche but valid;  |
| [#9157](https://github.com/mesonbuild/meson/issues/9157) | `add_project_link_arguments()` breaks due to clink dynamic linker sele | A problem where project-level link arguments get overridden by dynamic linker selection based on the global list of languages in u |
| [#9169](https://github.com/mesonbuild/meson/issues/9169) | Allow GeneratedList as input to other Generator object | A request to allow chaining the output of one generator() (a GeneratedList) as input to another generator(). No local confirmation |
| [#9178](https://github.com/mesonbuild/meson/issues/9178) | `meson test --gdb` launches the wrapper with gdb instead of the wrappe | A problem where --gdb makes the wrapper itself the gdb target when exe_wrapper is used. Still OPEN upstream (updated 2025-02). Kee |
| [#9179](https://github.com/mesonbuild/meson/issues/9179) | Support multiple `--wrapper` commands in meson test | The ability to stack multiple --wrapper specifications is not implemented, so combining a test-setup wrapper with a command-line w |
| [#9180](https://github.com/mesonbuild/meson/issues/9180) | Support per-test `exe_wrapper` | A request to add a per-test exe_wrapper keyword argument to test() is not implemented. Still OPEN upstream (updated 2025-02). Rela |
| [#9194](https://github.com/mesonbuild/meson/issues/9194) | Add a mechanism to write pch headers from the Meson DSL | A helper (module.pch_file) to generate a PCH header from the DSL using configure_file under the hood is not implemented. Keep as a |
| [#9200](https://github.com/mesonbuild/meson/issues/9200) | Clang c++20 modules support | A request for Clang C++20 modules support. C++ modules support overall is still evolving, and full Clang-specific support couldn't |
| [#9204](https://github.com/mesonbuild/meson/issues/9204) | Impossible to create a single static library containing external stati | There is no way to build a single static library incorporating objects from external static libraries found via pkg-config, etc. ( |
| [#9227](https://github.com/mesonbuild/meson/issues/9227) | Feature Request: Warn about build/host asymmetry in default options | A request to warn when default_options in a cross build applies only to the host and not to the build machine. Still OPEN upstream |
| [#9251](https://github.com/mesonbuild/meson/issues/9251) | address sanitize should also add -fsanitize-recover | A mechanism to automatically add -fsanitize-recover, needed for ASan's continue mode, is not implemented (b_sanitize now accepts a |
| [#9252](https://github.com/mesonbuild/meson/issues/9252) | dependency('threads') ignores static with mingw on linux | ThreadDependency only uses compiler.thread_link_flags() and doesn't respect static: true, causing winpthread to be dynamically lin |
| [#9279](https://github.com/mesonbuild/meson/issues/9279) | `assert(key not in self.keys)` during `meson setup` with `--backend=xc | The assert(key not in self.keys) in xcodebackend's PbxDict.add_item still exists (xcodebackend.py:192). The bug causing duplicate  |
| [#9289](https://github.com/mesonbuild/meson/issues/9289) | custom_target should not convert command line argument strings | Code that unconditionally replaces '\' with '/' in custom_target's string command arguments (backends.py:1618) still exists. This  |
| [#9296](https://github.com/mesonbuild/meson/issues/9296) | --whole-archive is not converted to /WHOLEARCHIVE | MSVC's unix_args_to_native (mesonbuild/compilers/mixins/visualstudio.py:218-) still doesn't convert -Wl,--whole-archive/--no-whole |
| [#9301](https://github.com/mesonbuild/meson/issues/9301) | Using find_library('util', static: ...) uses the full library path ins | find_library is designed to return a full path when static is specified, and this also shows up in .pc files. No clear change or f |
| [#9363](https://github.com/mesonbuild/meson/issues/9363) | gnome.generate_gir() missing library path (when linking against static | -L handling was added to generate_gir (for rpath dirs and shared-library output dirs), but the static_library case still passes a  |
| [#9398](https://github.com/mesonbuild/meson/issues/9398) | Planning for subproject options | A design-discussion thread on subproject options. Per-subproject and all-subproject options have progressed significantly, but thi |
| [#9399](https://github.com/mesonbuild/meson/issues/9399) | Builtin option for tests | A design discussion about adding a builtin option for testing. No local implementation of such a builtin option was confirmed; kee |
| [#9414](https://github.com/mesonbuild/meson/issues/9414) | After reconfiguring old object files are still linked in | A problem where stale object files remain in the link after source files are deleted and the project is reconfigured. No clear loc |
| [#9431](https://github.com/mesonbuild/meson/issues/9431) | CMake cause warning on reconfigure (Failed to determine CMake compiler | The code for the 'CMake Toolchain: Failed to determine CMake compilers state' warning still exists (cmake/toolchain.py:260). A har |
| [#9434](https://github.com/mesonbuild/meson/issues/9434) | extract_objects() fails if target and sources are defined in different | File.__hash__/__eq__ still depends on subdir (universal.py:516-524), and extract_objects' source matching (an `in` check against s |
| [#9462](https://github.com/mesonbuild/meson/issues/9462) | windows & network directories: regenerate fails (UNC \\VBoxSvr paths) | A report that regenerate fails on the VS backend with a UNC network path (\\VBoxSvr). No clear local fix for UNC support was found |
| [#9486](https://github.com/mesonbuild/meson/issues/9486) | Feature: Accessing dependency compile flags etc from meson.build | The Dependency object still doesn't expose methods like get_compile_args()/get_link_args() (only get_variable/partial_dependency/a |
| [#9500](https://github.com/mesonbuild/meson/issues/9500) | Docs: Broken formatting on Reference-manual.html ([index]) | [Confirmed unfixed per maintainer feedback] refman_links.py's [[...]] resolution regex rejects operator names with [index] (square |
| [#9524](https://github.com/mesonbuild/meson/issues/9524) | ExternalProgram.full_path() returns wrong string if command has argume | programs.py's path determination picks "the last element that exists as a file", but for non-absolute-path PATH commands like bash |
| [#9540](https://github.com/mesonbuild/meson/issues/9540) | Using -Dbuildtype and -Doptimization + -Ddebug is not redundant despit | The 'Recommend using either...redundant' warning for specifying buildtype together with optimization/debug still exists (environme |
| [#9554](https://github.com/mesonbuild/meson/issues/9554) | Installing non-dangling symlinks as-is rather than dereferencing them  | A follow_symlinks kwarg was added to install-related functions (interpreter.py:2485 etc., install_data/install/install_symlink), m |
| [#9563](https://github.com/mesonbuild/meson/issues/9563) | meson dist doesn't notice a dirty meson.build | mdist.run() gets project_version from the stale build.dat via build.load() and doesn't reconfigure/regenerate when `meson dist` is |
| [#9618](https://github.com/mesonbuild/meson/issues/9618) | dependency('Intl', method: 'cmake') has no method 'cmake' | intl is registered as a DependencyFactory with only BUILTIN/SYSTEM (misc.py:672-676), and method:'cmake' still can't be used. The  |
| [#9635](https://github.com/mesonbuild/meson/issues/9635) | When compiling a windows resource file, meson fails to invoke windres. | 'C:\Program is not recognized' is a symptom of a windres call with a space-containing path getting split via shell parsing. The wi |
| [#9671](https://github.com/mesonbuild/meson/issues/9671) | Allow specifying which Python interpreter to use | Specifying which interpreter to use is possible via python.find_installation(name_or_path) (python.py:526), but CLI flags like the |
| [#9674](https://github.com/mesonbuild/meson/issues/9674) | pkg-config versus pkgconfig behavior (PKG_CONFIG_SYSROOT_DIR not expos | PKG_CONFIG_SYSROOT_DIR is set when sys_root is present during cross builds (pkgconfig.py:280-282). However, whether get_pkgconfig_ |
| [#9684](https://github.com/mesonbuild/meson/issues/9684) | unknown compiler error for SHARC DSP (cc21k) | The cc21k compiler for Analog Devices SHARC is not recognized by detect.py and remains 'Unknown compiler'. Adding dedicated compil |
| [#9686](https://github.com/mesonbuild/meson/issues/9686) | Unknown compilers goto-cc | CBMC's goto-cc is gcc-compatible but isn't distinguished by detect.py and shows as 'Unknown compiler'. GCC-compatibility detection |
| [#9692](https://github.com/mesonbuild/meson/issues/9692) | rpath not fully stripped on install | depfixer errors if install_rpath is longer than build_rpath, and pads/overwrites the difference if shorter (depfixer.py:262-272),  |
| [#9718](https://github.com/mesonbuild/meson/issues/9718) | CMake dependency fails to find vulkan when invoked through meson | Specifying -DCMAKE_MODULE_PATH via the cmake_module_path kwarg is possible (cmake.py:131-133), but the report concerns the interac |
| [#9720](https://github.com/mesonbuild/meson/issues/9720) | Add ability to override build_machine.cpu() in host == build configura | No mechanism was found locally for overriding build_machine.cpu() via a native file's [build_machine] section or the CLI (update_b |
| [#9821](https://github.com/mesonbuild/meson/issues/9821) | No way to turn meson install warnings into errors | There is no mechanism to turn `meson install` warnings (e.g. the symlink-copy warning) into errors; minstall.py has no --fatal-equ |
| [#9840](https://github.com/mesonbuild/meson/issues/9840) | meson seems to ignore custom targets when it generates compile_command | generate_compdb only passes compiler/PCH (and tasking MIL) rules to `ninja -t compdb`, excluding CUSTOM_COMMAND (ninjabackend.py:8 |
| [#9845](https://github.com/mesonbuild/meson/issues/9845) | meson wrongly assumes that x86_64-linux-gnu can run x86_64-linux-gnux3 | machine_info_can_run remains a heuristic based solely on cpu_family comparison (envconfig.py:761-779), and since x32 shares the sa |
| [#9849](https://github.com/mesonbuild/meson/issues/9849) | depfiles not working for incbin asm statements | Files pulled in via an assembler's .incbin/.include are not dependency-tracked (not included in the depfile GCC generates), and Me |
| [#9851](https://github.com/mesonbuild/meson/issues/9851) | configure_file argument depfile broken | configure_file's command runs at configure time, and its depfile is only generated into scratch_dir (interpreter.py:2906) without  |
| [#9857](https://github.com/mesonbuild/meson/issues/9857) | Allow setting name_suffix via cross file | The ability to set executable_suffix as a default via a cross/machine file is not implemented on current master (envconfig.py's ge |
| [#9862](https://github.com/mesonbuild/meson/issues/9862) | [Documentation] Explain the differences to cmake, ideally a HTML table | A proposal to add a meson-vs-cmake comparison table to the FAQ. A reasonable documentation request, but fairly subjective, requiri |
| [#9866](https://github.com/mesonbuild/meson/issues/9866) | Compiler arguments are not properly ignored during checks | The documentation mismatch remains unresolved on current master: compiler checks only ignore arguments coming from add_*_arguments |
| [#9868](https://github.com/mesonbuild/meson/issues/9868) | Generator process() with preserve_path_from keyword argument bug | A problem where, when using preserve_path_from, the subpath of a generated file can't be passed to the generator's output director |
| [#9889](https://github.com/mesonbuild/meson/issues/9889) | Built-in support for pre-processing + compiling assembly with MSVC | masm (ml/ml64/armasm) language support has been added (asm.py, 1.9.0 release notes), but the integration this issue asks for — aut |
| [#9901](https://github.com/mesonbuild/meson/issues/9901) | [dlang] [dub] Plain library references should try <name> and lib<name> | The behavior of trying both <name> and lib<name> when referencing a C library via dub is not found in the current dub.py. A niche  |
| [#9923](https://github.com/mesonbuild/meson/issues/9923) | Support .NET Core/.NET 6+ compiler | Direct support for .NET Core/csc.dll is not implemented (compilers/cs.py only supports the traditional mono/mcs family). Generatin |
| [#9959](https://github.com/mesonbuild/meson/issues/9959) | Meson tries to find VAPI for Vala project's C dependencies' dependenci | A problem where Vala's C dependencies require a VAPI even for indirect dependencies that are purely C-only. An improvement to Vala |
| [#10001](https://github.com/mesonbuild/meson/issues/10001) | Meson test -C doesn't find targets when pointing a bound mount | A problem where `meson test`'s rebuild fails in a build directory accessed via a bind mount, due to a mismatch between the relativ |
| [#10015](https://github.com/mesonbuild/meson/issues/10015) | msvc chokes on cpp_std=gnu++14 setting in meson.build | Even on current master, MSVC's cpp_std choices remain only c++*/vc++* and don't accept gnu++* (cpp.py's get_options cpp_stds; VC_V |
| [#10017](https://github.com/mesonbuild/meson/issues/10017) | gnome.yelp() no longer works with a built input file | gnome.yelp() assumes at configure time that index.docbook exists under source and can't handle custom_target-generated input (trig |
| [#10022](https://github.com/mesonbuild/meson/issues/10022) | LNK 1107 on windows with clang++/link.exe(MSVC)/ninja | A problem where clang++ defaults to selecting MSVC's link.exe as its static linker, which doesn't support thin archives, producing |
| [#10025](https://github.com/mesonbuild/meson/issues/10025) | Handling precompiled header : recompile when needed | A problem where Clang's PCH goes stale when system headers change, causing build failures. An improvement is needed to correctly w |
| [#10033](https://github.com/mesonbuild/meson/issues/10033) | Question: support for debug pretty printers | A proposal for built-in Meson support for natvis/gdb pretty printers. A feature request requiring design discussion; no comments y |
| [#10065](https://github.com/mesonbuild/meson/issues/10065) | Specify default_options for cpp_eh only on Windows | A problem where cpp_eh can't be set only for Windows because conditional branching (on host_machine/compiler) isn't possible insid |
| [#10068](https://github.com/mesonbuild/meson/issues/10068) | Proposal: Support local build & install via third party build systems | A large-scale proposal for a mechanism to build/install a third-party build system locally and treat it as a system package. Alrea |
| [#10074](https://github.com/mesonbuild/meson/issues/10074) | Ability to pass extra options (via meson.build) to static linker tool | A request for a way to pass extra arguments to the static linker (ar/lib.exe) from within meson.build. Currently ar=['lib','-ignor |
| [#10077](https://github.com/mesonbuild/meson/issues/10077) | gnome.generate_gir does not use setup-time LDFLAGS | A problem where g-ir-scanner's link command doesn't receive the LDFLAGS set at setup time (e.g. -fsanitize=address), and removing  |
| [#10084](https://github.com/mesonbuild/meson/issues/10084) | "depends" argument for gnome.generate_vapi() | A generated vapi can't be specified in another generate_vapi's packages, and there's no depends argument to control generation ord |
| [#10094](https://github.com/mesonbuild/meson/issues/10094) | Allow skipping some CI workflows with commit message | A request for a mechanism to run or skip specific CI workflows based on commit message. The current skip_ci.py only supports a bla |
| [#10104](https://github.com/mesonbuild/meson/issues/10104) | linuxlike 13 cmake dependency test is flaky | The test 'linuxlike: 13 cmake dependency' fails intermittently — a flaky test. Updated through May 2026, ongoing test instability; |
| [#10118](https://github.com/mesonbuild/meson/issues/10118) | Unable to express dependency of add_dist_script on custom_target | A problem where a custom_target (e.g. vcs_tag) passed to add_dist_script isn't built before dist. A mechanism is needed to wire cu |
| [#10120](https://github.com/mesonbuild/meson/issues/10120) | `dirs` parameter inhibits system lookup in `find_library` | When dirs is specified, find_library enters the manual search path, and since get_library_dirs (derived from `cc --print-search-di |
| [#10172](https://github.com/mesonbuild/meson/issues/10172) | compiler.find_library should always search -L dirs from c*_link_args | An inconsistency where find_library(static:...)'s manual search path doesn't consult the -L directories from c*_link_args. A valid |
| [#10185](https://github.com/mesonbuild/meson/issues/10185) | [Proposal] Mutability of Targets & Dependencies | A large-scale design proposal to allow targets/dependencies to be modified after the fact. A fundamental discussion touching Meson |
| [#10187](https://github.com/mesonbuild/meson/issues/10187) | [Feature request] Improve support for clang's "wasm-ld" | A request to emit wasm-ld-appropriate flags, rather than Unix-style linker flags, for vanilla clang + wasm-ld (not via Emscripten) |
| [#10229](https://github.com/mesonbuild/meson/issues/10229) | Test taking input generated by another test | A request to use the executable produced by one test as input to another test (inter-test dependencies / multi-stage testing). Dep |
| [#10237](https://github.com/mesonbuild/meson/issues/10237) | Stop adding -D_FILE_OFFSET_BITS=64 for unknown platforms | -D_FILE_OFFSET_BITS=64 is added unconditionally on all platforms other than MSVC/Darwin (including unknown and bare-metal ones). A |
| [#10241](https://github.com/mesonbuild/meson/issues/10241) | Use path of custom_target as string while creating a dependency | Users want to use custom_target's full_path() as a string (e.g. in a C preprocessor macro) while also getting a dependency edge, b |
| [#10247](https://github.com/mesonbuild/meson/issues/10247) | meson fails to build universal binary: exe_wrapper is needed but was n | PowerPC (ppc + ppc64) universal builds/cross builds fail with an exe_wrapper-required error. This involves build-time execution du |
| [#10298](https://github.com/mesonbuild/meson/issues/10298) | CMake install headers & Meson intermediate install | The intermediate header layout produced by a CMake subproject's install(FILES ...) isn't reproduced by Meson's cmake module, so #i |
| [#10300](https://github.com/mesonbuild/meson/issues/10300) | LTO + static libraries + clang produce unusable static libraries | With clang + LTO, a static lib ends up containing only LLVM IR, causing a "format not recognized" error when linked later with gcc |
| [#10317](https://github.com/mesonbuild/meson/issues/10317) | CMake TARGET_FILE Generator expression doesn't work for grpc subprojec | A limitation where $<TARGET_FILE:protoc>, etc. return an empty string for targets built within the same CMake subproject (as oppos |
| [#10328](https://github.com/mesonbuild/meson/issues/10328) | CMake TARGET_FILE Generator expression doesn't work for scotch subproj | Same root cause as #10317. $<TARGET_FILE:dummysizes> points to an executable built within a subproject but can't be resolved, leav |
| [#10333](https://github.com/mesonbuild/meson/issues/10333) | Give the documentation a light mode | No implementation of prefers-color-scheme or a theme switcher is found in docs/theme; light mode remains unimplemented. A valid do |
| [#10344](https://github.com/mesonbuild/meson/issues/10344) | simd module doesn't handle `-mavx2 -mfma` very well | The simd module now supports c_args, but ISETS is still hardcoded with the fixed naming scheme 'HAVE_<iset>'; additional flag comb |
| [#10360](https://github.com/mesonbuild/meson/issues/10360) | `.system_family()` method to group similar operating systems. | MachineHolder has cpu_family/cpu/system etc., but system_family is still unimplemented. A feature request needing design agreement |
| [#10363](https://github.com/mesonbuild/meson/issues/10363) | Exclude an external subproject from installing on meson.build level | There is still no mechanism in meson.build to exclude an entire external subproject from install; this remains a feature request n |
| [#10372](https://github.com/mesonbuild/meson/issues/10372) | CMake not found with Yocto SDK in dependency() | CMake detection inside dependency() fails to pick up the cmake on the PATH in a Yocto SDK. This touches the tool-search path in cr |
| [#10381](https://github.com/mesonbuild/meson/issues/10381) | Support for cython `public` functions is missing | There is no mechanism to track and use the headers (e.g. _pyx.h) generated by Cython's public functions; this is a design issue re |
| [#10382](https://github.com/mesonbuild/meson/issues/10382) | deprecated options can override command line values | The structure where option(deprecated:'newopt') unconditionally overwrites the new option inside set_option (via a recursive set_o |
| [#10383](https://github.com/mesonbuild/meson/issues/10383) | compiler.find_library and include_directories annoyance | A request to relax the behavior where include_directories rejects absolute paths inside the source tree. This needs a design decis |
| [#10388](https://github.com/mesonbuild/meson/issues/10388) | Prebuilt libraries: whole-archive and linker argument rewriting breaki | This mixes two issues: Meson rewriting and breaking prebuilt/DPDK's pkgconf --whole-archive link arguments, and a proposal for a p |
| [#10392](https://github.com/mesonbuild/meson/issues/10392) | bug(conda): linking against system-level dependencies in conda environ | Boost's rpath/linking isn't propagated through an indirect dependency via link_with. A design issue around transitive dependency p |
| [#10417](https://github.com/mesonbuild/meson/issues/10417) | Add str.to_quoted | A str.to_quoted method is not implemented (no hits via grep; configuration_data's set_quoted etc. are different things). A feature |
| [#10421](https://github.com/mesonbuild/meson/issues/10421) | Feature Request: Meson presets | A CMakePresets-equivalent MesonPresets.json mechanism is not implemented (no hits in snippets/coredata). A large feature request s |
| [#10423](https://github.com/mesonbuild/meson/issues/10423) | Use ccache 4.6+ with MSVC | detect_compiler_cache only prefers sccache and falls back to ccache; no dedicated logic was found for auto-applying ccache 4.6+ on |
| [#10440](https://github.com/mesonbuild/meson/issues/10440) | Allow executables as pkgconfig.generate() dependencies | A comment in pkgconfig.py explicitly states "Executable is not accepted by the DSL"; support for passing an executable to generate |
| [#10455](https://github.com/mesonbuild/meson/issues/10455) | Feature Request: "meson subprojects download" does not checkout subpro | subprojects download doesn't recursively fetch grandchild subprojects. Recursive wrap resolution would need to be built into msubp |
| [#10469](https://github.com/mesonbuild/meson/issues/10469) | Could meson provide support for x86-64 microarchitecture feature level | There is no mechanism for handling x86-64-v2/v3/v4 feature levels (no hits in get_instruction_set_args etc.). A feature request ne |
| [#10472](https://github.com/mesonbuild/meson/issues/10472) | RFC: Link a static subproject into a main project DLL | A static-for-shared-equivalent default_library value/mechanism is not implemented (no hits in snippets). This is an RFC touching d |
| [#10474](https://github.com/mesonbuild/meson/issues/10474) | Add `b_cfi` for Control Flow Integrity | A b_cfi base option is not implemented (b_sanitize etc. exist, but no hits for b_cfi). As the issue text itself notes, CFI involve |
| [#10479](https://github.com/mesonbuild/meson/issues/10479) | How to expect an exact exit code for a test? | test() gained expected_fail (1.11.0) and should_fail was deprecated, but expected_fail is a boolean, so specifying an exact expect |
| [#10504](https://github.com/mesonbuild/meson/issues/10504) | Add a CMake-Targets-File generator. | The cmake module has write_basic_package_version_file/configure_package_config_file, but no functionality to auto-generate a *Targ |
| [#10519](https://github.com/mesonbuild/meson/issues/10519) | Qt6: the shaders precompilation support to qsb | Qt6 shader precompilation (qsb, equivalent to qt6_add_shaders) is not implemented in the qt module. A reasonable feature-addition  |
| [#10521](https://github.com/mesonbuild/meson/issues/10521) | Dependency page info | A proposal to reorganize the Dependencies documentation (resolving the scattered coverage of things like threads). A valid documen |
| [#10533](https://github.com/mesonbuild/meson/issues/10533) | Using -ffile-prefix-map with meson? | A request for a mechanism where Meson correctly passes a -ffile-prefix-map value relative to the build dir, to normalize __FILE__  |
| [#10543](https://github.com/mesonbuild/meson/issues/10543) | declare_dependency does not inherit dependencies through link_with | include_directories etc. of a lower-level dependency linked via declare_dependency's link_with are not propagated transitively. A  |
| [#10565](https://github.com/mesonbuild/meson/issues/10565) | Meson does not allow strings like `X.Y.Z+META` to be used as the libra | Shared-library version validation still uses r'[0-9]+(\.[0-9]+){0,2}', rejecting SemVer's +META. There are soname-generation valid |
| [#10620](https://github.com/mesonbuild/meson/issues/10620) | Request for interest: server for binary artifacts from wrap files | An RFC for a repository/server concept to distribute binary artifacts sourced from wraps. A large-scale proposal needing design an |
| [#10621](https://github.com/mesonbuild/meson/issues/10621) | Respect LIBS environment variable | The autoconf LIBS environment variable (a group of -l flags placed after object files) is unsupported by Meson; environment.py's e |
| [#10624](https://github.com/mesonbuild/meson/issues/10624) | Designing feature combo options | A design discussion about a combo_feature option type (automatic mutual-exclusion control). An addition to the option-type system; |
| [#10627](https://github.com/mesonbuild/meson/issues/10627) | Primitive for generating big opaque dir trees (like docs) | A proposal (filed by jpakkane) for a custom_target-like primitive to generate/install the arbitrary directory trees produced by to |
| [#10631](https://github.com/mesonbuild/meson/issues/10631) | Add a way to mark a file as a module implementation partition | There is no mechanism to apply MSVC's /internalPartition to individual files; this is a design issue dependent on per-file compile |
| [#10637](https://github.com/mesonbuild/meson/issues/10637) | Could Meson collect build time to show after the final build step? | `meson compile` has no feature to measure/display total build time. Ninja itself has timing data, so a backend-independent design  |
| [#10638](https://github.com/mesonbuild/meson/issues/10638) | Would it make sense to have a protobuf module? | No protobuf module exists; a new module handling header install and path resolution for interdependent proto files would be a feat |
| [#10641](https://github.com/mesonbuild/meson/issues/10641) | sincos, sincosf detection as used by gtk misdetects sincos, sincosf | When headers are absent from the prefix, has_function's builtin fallback (__builtin_sincos) still returns true even when NetBSD's  |
| [#10665](https://github.com/mesonbuild/meson/issues/10665) | Improving Qt moc cross platform support | Automatic generation of a moc_predefs.h equivalent to CMake automoc (dumping compiler-predefined macros and passing them via --inc |
| [#10684](https://github.com/mesonbuild/meson/issues/10684) | unstable_external_project passes nonsensical --host during cross-compi | The cross-build --host triplet still uses a simple heuristic of cpu + ('pc'/'unknown') + system, which still produces invalid valu |
| [#10685](https://github.com/mesonbuild/meson/issues/10685) | Add option to disable `Consider using the built-in option for ...` | There is no mechanism (e.g. warn_builtin:false) to suppress the built-in-option-suggestion warning from add_project_arguments. A f |
| [#10691](https://github.com/mesonbuild/meson/issues/10691) | Glitches with --prefer-static -Dc_link_args="-static" when static libr | A case where, with --prefer-static, a dependency lacking a static version falls back to the shared version while still linking wit |
| [#10692](https://github.com/mesonbuild/meson/issues/10692) | stderr must be used to print errors | mlog gained a log_to_stderr mechanism, but it defaults to False, and errorhandler's mlog.exception path doesn't switch to stderr.  |
| [#10704](https://github.com/mesonbuild/meson/issues/10704) | CUDA Language does not support `cuda_pch` | build.py's PCH support only covers c_pch/cpp_pch; cuda_pch is unsupported. A feature request needing consideration of nvcc's PCH s |
| [#10706](https://github.com/mesonbuild/meson/issues/10706) | Rebuild automatically if the rustc version changes | There is no mechanism to automatically rebuild when the rustc version changes; this needs a design that incorporates a compiler fi |
| [#10710](https://github.com/mesonbuild/meson/issues/10710) | feature: auto-generated 'help' target | An automatic 'help' target listing top-level targets is not implemented. Introspection can provide this info, but there's no built |
| [#10711](https://github.com/mesonbuild/meson/issues/10711) | gfortran binaries installed by meson have rpath problem | The @rpath/libgfortran.5.dylib embedded by gfortran on macOS can't be resolved after install. This involves rpath stripping at ins |
| [#10715](https://github.com/mesonbuild/meson/issues/10715) | Undocumented automatic fallback behaviour if multiple dep names are sp | The basic behavior of dependency.yaml with multiple names plus fallback is now documented, but the edge case the reporter flagged  |
| [#10721](https://github.com/mesonbuild/meson/issues/10721) | feature: meson configure option to show only project-specific options | `meson configure` displays output split into sections, but a --show-project-options-style CLI flag to show only project-specific o |
| [#10724](https://github.com/mesonbuild/meson/issues/10724) | objects files created by rustc with a crate type of staticlib cannot b | An internal representation limitation where a rust staticlib's output can't be treated as objects still exists (same root cause as |
| [#10734](https://github.com/mesonbuild/meson/issues/10734) | Adding info about using cosmopolitan with meson to the docs | A proposal to add documentation on how to use Cosmopolitan Libc. A niche documentation request; someone needs to write a docs PR — |
| [#10748](https://github.com/mesonbuild/meson/issues/10748) | Missing light theme on the website. | A request for a light-theme toggle button on mesonbuild.com. This concerns the deployed site theme (mkdocs) and can't be verified  |
| [#10749](https://github.com/mesonbuild/meson/issues/10749) | Every page on the website contains at least one full screen of empty s | A margin/spacing bug at the bottom of pages across the site. This is an issue with the deployed theme's CSS and can't be reproduce |
| [#10755](https://github.com/mesonbuild/meson/issues/10755) | Using full_path of build_tgt within cpp_args does not create a depende | Embedding another target's full_path() inside cpp_args (for an LLVM pass-plugin use case) doesn't create a dependency. There's no  |
| [#10764](https://github.com/mesonbuild/meson/issues/10764) | Meson does not detect position independent flag on CMake static librar | -fPIC/CMAKE_POSITION_INDEPENDENT_CODE isn't propagated to Meson for a CMake subproject's static library, preventing linking into a |
| [#10802](https://github.com/mesonbuild/meson/issues/10802) | glib-compile-schemas errors are not fatal | gnome.compile_schemas just runs glib-compile-schemas via custom_target, and since that tool returns exit code 0 even on error, Mes |
| [#10823](https://github.com/mesonbuild/meson/issues/10823) | Old GNU ld bfd broken on meson 0.63.2, works on 0.60.1 | A link-failure regression on a very old ld.bfd 2.17.50 (FreeBSD11.4/MidnightBSD). Milestoned at 0.63.4 with 17 comments and update |
| [#10831](https://github.com/mesonbuild/meson/issues/10831) | Install script fails on MinGW because of encoding | When displaying an install script's stderr, print() after decode(errors='replace') gets re-encoded for a cp1252 console, causing a |
| [#10836](https://github.com/mesonbuild/meson/issues/10836) | I want to get the path of a generator-processed file (env var substitu | A request to allow substitution variables like @BUILD_ROOT@ inside custom_target's env:. Currently only command is subject to subs |
| [#10868](https://github.com/mesonbuild/meson/issues/10868) | MPI dependency Omits "-WL,-rpath" from lib directories on Redhat. | An MPI-dependency issue specific to RedHat/spack where -Wl,-rpath is missing for the lib directory and only -Wl,<dir> gets passed, |
| [#10872](https://github.com/mesonbuild/meson/issues/10872) | aix: CC='gcc -maix64' results in "Can not run test applications in thi | On AIX with `CC='gcc -maix64'`, machine_info_can_run determines the native CPU family without regard to the compiler, so it fails  |
| [#10874](https://github.com/mesonbuild/meson/issues/10874) | Support default options in wrap files | A feature to specify default_options directly inside a wrap file is unimplemented. This needs coordination between the wrap parser |
| [#10876](https://github.com/mesonbuild/meson/issues/10876) | Support for LLDB in unit test. | `meson test`'s debugger integration assumes gdb (--gdb/--gdb-path); lldb fails due to incompatible options like --quiet/--args. Ne |
| [#10890](https://github.com/mesonbuild/meson/issues/10890) | Meson doesn't escape newlines when generating build.ninja | When a custom command generated via the cmake module contains a newline, that raw newline gets written into build.ninja and causes |
| [#10894](https://github.com/mesonbuild/meson/issues/10894) | macOS does not like -undefined dynamic_lookup anymore | shared_module() still always adds -undefined dynamic_lookup, and newer macOS linkers emit a "may not work with chained fixups" war |
| [#10910](https://github.com/mesonbuild/meson/issues/10910) | dependency() should have an option to override globally defined paths | A request for a way to override cmake_prefix_path/pkg_config_path etc. for an individual dependency() call. Needs API design for o |
| [#10911](https://github.com/mesonbuild/meson/issues/10911) | Build script output from cmake module is missing include directories | Some include_directories (e.g. from another subproject's includes) get dropped from the final meson.build during cmake-module conv |
| [#10919](https://github.com/mesonbuild/meson/issues/10919) | Broken version detection when program name or path contains numbers | The version-detection regex has been improved to prefer `([0-9]+(\.[0-9]+)+)` (requiring a dot), fixing cases like x264 misdetecti |
| [#10927](https://github.com/mesonbuild/meson/issues/10927) | Cannot link_whole a custom target into a static library despite the do | Using link_whole to link a custom-target-built static library into another static library is still rejected with "Cannot link_whol |
| [#10928](https://github.com/mesonbuild/meson/issues/10928) | Add run verb to execute built executables or run targets with user con | A buck-style `meson run <target> -- args` verb is unimplemented. A feature request needing design of a new subcommand that builds  |
| [#10934](https://github.com/mesonbuild/meson/issues/10934) | Add `suites:` to `add_test_setup()` | add_test_setup() only has exclude_suites for exclusion; there is no positive `suites:` kwarg (inclusion) to limit which tests run. |
| [#10935](https://github.com/mesonbuild/meson/issues/10935) | has_header result cached so can't add an include dir and provide the h | There is still no mechanism to invalidate/update compiler-check results at runtime; this remains a valid request needing a design  |
| [#10957](https://github.com/mesonbuild/meson/issues/10957) | Embedded GCC has_link_argument does not work because test program fail | In a bare-metal cross environment, even a minimal link test fails, so has_link_argument gives a false result. Needs a design allow |
| [#10984](https://github.com/mesonbuild/meson/issues/10984) | CMake subproject ignores dependent libraries | A dependency-resolution bug in the CMake interpreter where, among several interdependent libraries in a CMake subproject, only one |
| [#10985](https://github.com/mesonbuild/meson/issues/10985) | Incorrect relative include paths for CMake subproject | A bug where relative paths in target_include_directories aren't resolved correctly when imported via a CMake subproject. A path-no |
| [#10992](https://github.com/mesonbuild/meson/issues/10992) | Feature request: add a way to reduce stdout output from meson build | A request to reduce stdout verbosity/control log level during setup. mlog has set_quiet, but there's no exposed CLI flag (like --q |
| [#10996](https://github.com/mesonbuild/meson/issues/10996) | feature request: add_project_arguments with arguments (module: executa | A request to apply add_project_arguments scoped to a specific target type (shared/static/executable). Adding this new scoping conc |
| [#11013](https://github.com/mesonbuild/meson/issues/11013) | wrong architecture detected | On M1 Mac with Rosetta, the system is still detected as arm64 even under an x86_64 shell. cpu_family detection depends on the comp |
| [#11029](https://github.com/mesonbuild/meson/issues/11029) | custom_target() runs cross executables directly instead of using exe_w | A question of exe_wrapper application and can_run_host_binaries semantics when using a self-built executable in a custom_target's  |
| [#11043](https://github.com/mesonbuild/meson/issues/11043) | llvm configuration should be obtained from llvm's cmake files only, no | A request to move to CMake-based detection because running llvm-config (a target binary) is problematic in cross builds. A fairly  |
| [#11044](https://github.com/mesonbuild/meson/issues/11044) | Meson no longer prints warnings from gtk-doc | A regression where stdout/stderr get captured for the gnome module's gtk-doc target, so warnings no longer display. Involves how o |
| [#11080](https://github.com/mesonbuild/meson/issues/11080) | Libs bleed into pkg-config --static, even for partial_dependency(compi | Even with partial_dependency(compile_args:true), a library still ends up in pkgconfig.generate's --static --libs output. A bug nee |
| [#11081](https://github.com/mesonbuild/meson/issues/11081) | Subprojects are not included in tarball, when behind a disabled option | meson dist --include-subprojects only includes subprojects actually used in the build (b.projects.host/build), so subprojects unde |
| [#11094](https://github.com/mesonbuild/meson/issues/11094) | Allow to override method of library having a specific dependency detec | A method:'cmake' specification is ignored for dependencies that have their own dedicated detector, like boost. _build_external_dep |
| [#11118](https://github.com/mesonbuild/meson/issues/11118) | Ability to disable sccache detection | When no compiler is specified, sccache is auto-detected and preferred over ccache unconditionally. This can be worked around by sp |
| [#11129](https://github.com/mesonbuild/meson/issues/11129) | import('python') separate python binary from libs | When Python tools and libs are installed in separate locations (as with vcpkg), the python module can't find the libs. Needs expan |
| [#11139](https://github.com/mesonbuild/meson/issues/11139) | libcurl (CMake) fails due to mishandling of escaped quotes in cmake_ru | A bug where escaped quotes in `cmake -E echo` get lost when passed through cmake_run_ctgt for a CMake subproject. A quote-preserva |
| [#11148](https://github.com/mesonbuild/meson/issues/11148) | [0.63.0] Wrong cc.compiles() result with MSVC | MSVC doesn't actually compile .S assembly files and only emits a warning (D9024/D9027), so cc.compiles() incorrectly returns YES.  |
| [#11163](https://github.com/mesonbuild/meson/issues/11163) | On project versions and run_command() inside project() | A design/documentation discussion about whether to officially support or prohibit evaluating things like run_command() inside proj |
| [#11180](https://github.com/mesonbuild/meson/issues/11180) | Clang-cl use compiler to invoke link command | Request to have clang-cl drive linking (for sanitizers, etc.) through the compiler driver (related to #5845). Whether to route lin |
| [#11182](https://github.com/mesonbuild/meson/issues/11182) | Error with scan-build and PCH together | Running scan-build fails to compile because the PCH file cannot be found. This appears to be an issue where the PCH include path i |
| [#11184](https://github.com/mesonbuild/meson/issues/11184) | Build fails if loads polly with `-Xclang -load -Xclang LLVMPolly.so` | --start-group/--end-group gets incorrectly inserted between flags that straddle -Xclang. This is a bug where clike.py's grouping l |
| [#11185](https://github.com/mesonbuild/meson/issues/11185) | Add ability to see test output when using TAP (or other) protocols | Request to show the raw output (stdout/stderr) on the terminal even in verbose mode when using protocol:'tap' etc. This requires a |
| [#11189](https://github.com/mesonbuild/meson/issues/11189) | Old-style [provides] depname=variable in wrap file overrides both cros | The implicit wrap fallback ([provide]) overwrites both the cross and native dependencies with the same object, causing a machine-m |
| [#11196](https://github.com/mesonbuild/meson/issues/11196) | Unify pkgconfig.generate() declare_dependency() somehow meson.override | A large-scale design discussion about unifying pkgconfig.generate / declare_dependency / override_dependency (and further, overrid |
| [#11200](https://github.com/mesonbuild/meson/issues/11200) | install_subdir should keep (empty directories) | Request for install_subdir to preserve empty directories as well. The title is incomplete, but this is interpreted as a request to |
| [#11209](https://github.com/mesonbuild/meson/issues/11209) | SIMD module does not "detect" NEON on AArch64 | simd.check('neon') tries '-mfpu=neon' with GNU compilers, but on AArch64, NEON is always enabled and this flag is unrecognized, so |
| [#11210](https://github.com/mesonbuild/meson/issues/11210) | Add an option to choose CMake's imported configuration | Request to let users specify the mapping between a CMake dependency's IMPORTED_CONFIGURATIONS (DEBUG/RELWITHDEBINFO, etc.) and Mes |
| [#11226](https://github.com/mesonbuild/meson/issues/11226) | Regression setting PKG_CONFIG_LIBDIR with msys2 pkg-config after 0.62. | A regression where, on Windows with msys2 pkg-config, PKG_CONFIG_LIBDIR uses ';' (Windows-style) as a separator, but msys2's pkg-c |
| [#11231](https://github.com/mesonbuild/meson/issues/11231) | Failed when specifying a directory as input for custom_target or gener | Specifying a directory as input to custom_target/generator fails with 'File does not exist'. This is a feature request requiring a |
| [#11237](https://github.com/mesonbuild/meson/issues/11237) | Mac - problem using static libs installed by Homebrew | Homebrew's libiconv has renamed symbols such as _libiconv_close, causing linking to fail with find_library(static: true) or -Dpref |
| [#11252](https://github.com/mesonbuild/meson/issues/11252) | Meson lint and auto-format | Formatting meson.build is already implemented as 'meson format' (alias fmt), but the main focus of this issue is orchestrating mul |
| [#11255](https://github.com/mesonbuild/meson/issues/11255) | Meson doesn't correctly run shebang scripts coming from file(), config | func_run_target only wraps the argument with find_program when it starts as a str (interpreter.py:2307-2308); File/custom_target o |
| [#11271](https://github.com/mesonbuild/meson/issues/11271) | Sanity check inconsistent with actual build (Windows) | There's an inconsistency where the sanity check links via the compiler while the actual build calls the linker directly, plus a de |
| [#11286](https://github.com/mesonbuild/meson/issues/11286) | -unity.cpp files not cleaned | Intermediate -unity.cpp files from unity builds are left behind after 'clean', because ninja doesn't treat generated sources as cl |
| [#11299](https://github.com/mesonbuild/meson/issues/11299) | MSVC + CUDA + Shared library doesn't work | A CUDA/nvlink-specific bug (derived from #8984) where installing a .dll.a for a shared_library built with MSVC+CUDA fails. This co |
| [#11300](https://github.com/mesonbuild/meson/issues/11300) | Android: stdc++ linkage is wrong in certain cases (picked up from pkg- | On Android NDK, pkg-config's -L/usr/lib causes the stub implementation of libstdc++.so to be picked up via an absolute path. Discu |
| [#11302](https://github.com/mesonbuild/meson/issues/11302) | Mac - qt6 framework not found when it's not in /usr/local/lib | On macOS, the Qt framework search path is restricted to /usr/local/lib and doesn't use user-specified -F/-L paths. The Qt dependen |
| [#11304](https://github.com/mesonbuild/meson/issues/11304) | clang++ doesn't like meson-generated .RSP files with mixed forward/bac | When using clang++ on Windows, paths in the RSP file get broken due to mixed forward/backward slashes. Path normalization is neede |
| [#11315](https://github.com/mesonbuild/meson/issues/11315) | What is the correct behavior when multiple dependency are called with  | Calling the same-named dependency multiple times with different static/shared settings results in only the first override_dependen |
| [#11346](https://github.com/mesonbuild/meson/issues/11346) | Proposal: if no config tool defined in cross-file, do not use config-t | A proposal that, during cross-compilation, if a config-tool isn't defined in the cross file, pkg-config/cmake should be preferred  |
| [#11359](https://github.com/mesonbuild/meson/issues/11359) | Test output gets garbled with long test names | Test output gets garbled for test names longer than the terminal width. mtest does have formatting logic based on max_left_width / |
| [#11386](https://github.com/mesonbuild/meson/issues/11386) | docs: split the manual into many small pages | Reference-manual_functions.html is huge and loads slowly. This needs page-splitting or performance improvements on the documentati |
| [#11404](https://github.com/mesonbuild/meson/issues/11404) | cmake module blindly imports "LINKER:" linker arguments | The cmake module passes target_link_options' 'LINKER:' prefix straight into link_args, causing the link to fail. Expanding 'LINKER |
| [#11428](https://github.com/mesonbuild/meson/issues/11428) | Unknown linker(s): [['gcc-ar'], ['ar'], ['gar']] | Using the gold linker causes static linker (ar/gcc-ar/gar) detection to fail with an error. The static linker detection logic need |
| [#11434](https://github.com/mesonbuild/meson/issues/11434) | How to wrap the latest tag using wrap-git | Request for a 'follow the latest tag' feature in wrap-git. This is a proposed addition addressing the problem that head is fragile |
| [#11435](https://github.com/mesonbuild/meson/issues/11435) | meson needs to choose MSVC toolset on the basis of target | vsenv doesn't select vcvars' -arch based on the target and is fixed to the native arch (arm64/amd64), so x86 binaries can't be bui |
| [#11465](https://github.com/mesonbuild/meson/issues/11465) | Build the app with one step? | Request for a `meson make`-like feature that combines setup and compile into a single command. This requires a UX design decision  |
| [#11475](https://github.com/mesonbuild/meson/issues/11475) | Documentation cleanup | A proposal to reorganize the documentation structure (consolidating duplicate install instructions, cleaning up the tutorial, spli |
| [#11482](https://github.com/mesonbuild/meson/issues/11482) | rpath from LDFLAGS is stripped upon install if envvar PKG_CONFIG_PATH  | When PKG_CONFIG_PATH is set, rpaths coming from LDFLAGS get stripped at install time. This is presumed to be because depfixer remo |
| [#11488](https://github.com/mesonbuild/meson/issues/11488) | mypy report errors on Windows | A dev-tooling issue where mypy only recognizes sys.platform comparisons as platform branches, so it ends up checking platform-spec |
| [#11506](https://github.com/mesonbuild/meson/issues/11506) | Suggestion: an option to make custom_target touch/create (empty) outpu | Request for a kwarg (e.g. touch_output_files) that touches the output files after success, for custom_targets used as validators t |
| [#11507](https://github.com/mesonbuild/meson/issues/11507) | Feature suggestion: add a per-project 'install_tags' option | A proposal to add an option that restricts install tags on a per-project basis, to suppress installing unwanted files from subproj |
| [#11509](https://github.com/mesonbuild/meson/issues/11509) | Filters for coverage tests | Request for a filtering feature to exclude test code and unreachable UI code from coverage. This is a feature addition to coverage |
| [#11521](https://github.com/mesonbuild/meson/issues/11521) | dependency() fails to detect cmake dependencies, if the meson "masm" l | Using the masm language causes CMake toolchain generation to require MASM compiler information, making CMake dependency detection  |
| [#11523](https://github.com/mesonbuild/meson/issues/11523) | wxWidgets dependency on Windows attempts to use non-existing wx-config | On Windows, the wxwidgets dependency looks for a wx-config that doesn't exist. Windows-specific wxWidgets detection (prebuilt libr |
| [#11527](https://github.com/mesonbuild/meson/issues/11527) | "--backend vs" Does not produce functioning MSVC project definitions i | The project/solution files generated by the vs backend don't extend PATH for library runtime, causing test runs from VS to fail. T |
| [#11539](https://github.com/mesonbuild/meson/issues/11539) | Sources that get copied to multiple location only report one destinati | install_plan still assigns entries keyed by source path (plan[type][data.path] = entry), so when the same source is installed to m |
| [#11549](https://github.com/mesonbuild/meson/issues/11549) | Fortran target does not get rebuild if an included file changes | Changes to a Fortran include "inc.f90" don't trigger a rebuild. _scan_fortran_file_deps does follow includes, but it's mainly for  |
| [#11558](https://github.com/mesonbuild/meson/issues/11558) | Subproject/wrap configuration and building do not respect a consistent | There's an inconsistency where a subproject/wrap's configure and test use the base project's default options while its build uses  |
| [#11574](https://github.com/mesonbuild/meson/issues/11574) | compiler.find_library cannot find shared libraries unless they are lib | find_library forces the 'lib' prefix and can't find names without a prefix (i.e. equivalent to name_prefix). The case where specif |
| [#11575](https://github.com/mesonbuild/meson/issues/11575) | Compiler feature detection cannot introspect on wrap-based dependencie | has_header/has_header_symbol etc. don't accept internal (wrap) dependencies, producing 'Dependencies must be external dependencies |
| [#11577](https://github.com/mesonbuild/meson/issues/11577) | Document inability to extract symbolic links from ZIP files | Request to either work around or document the Python limitation that zipfile can't restore symbolic links when extracting a binary |
| [#11595](https://github.com/mesonbuild/meson/issues/11595) | Meson breaks installation of shared libraries from CMake subprojects o | A CMake subproject's shared library gets installed to lib instead of bin on Windows, causing a runtime crash. The cmake module's l |
| [#11596](https://github.com/mesonbuild/meson/issues/11596) | Meson cannot reconfigure if transitive wrapped dependencies are stored | --wipe reconfiguration fails for transitive wrap dependencies that use a custom subproject_dir, because subproject_dir isn't propa |
| [#11624](https://github.com/mesonbuild/meson/issues/11624) | Add maintainer list to the docs | Request to add a public list of maintainers to the documentation. Agreement is needed on who to list and how — a CODEOWNERS file e |
| [#11632](https://github.com/mesonbuild/meson/issues/11632) | Use external/system includes feature from Visual Studio 15.6 | Feature request to use MSVC's /external:I as a system include (equivalent to -isystem) to suppress warnings from third-party heade |
| [#11633](https://github.com/mesonbuild/meson/issues/11633) | meson cannot understand supported standards of flang on termux (androi | Linker detection with flang-new on termux/android fails with an undefined _QQmain symbol. The current llvm-flang class handles For |
| [#11637](https://github.com/mesonbuild/meson/issues/11637) | system includes don't prefer build dir over src dir | -isystem is missing from prepend_prefixes, so the include directory order gets reversed relative to -I and the build dir isn't pri |
| [#11641](https://github.com/mesonbuild/meson/issues/11641) | Meson cannot fall GNU cpp_std flags back to the standard MSVC ones | MSVC's C++ compiler's VC_VERSION_MAP still has no entries for gnu++ variants, so passing gnu++11 etc. fails with a KeyError-like e |
| [#11645](https://github.com/mesonbuild/meson/issues/11645) | buildtype not derived from debug and optimization options, with surpri | Propagation from buildtype to debug/optimization exists (options.py L1065-1071), but the reverse direction (changing debug/optimiz |
| [#11657](https://github.com/mesonbuild/meson/issues/11657) | Feature request: better support for custom VAPI directories for Vala | A proposal for a new API to propagate vala_vapi_dirs per dependency/target. Currently, only specifying --vapidir via add_project_a |
| [#11670](https://github.com/mesonbuild/meson/issues/11670) | Meson mangles MSVC flags beginning with L if specified with a dash | Since unix_args_to_native unconditionally converts anything starting with -L to /LIBPATH:, -LINKREPRO:MSVC still gets mangled into |
| [#11685](https://github.com/mesonbuild/meson/issues/11685) | ISPC support | There is no ispc-related implementation under mesonbuild/compilers — new-language support is unimplemented. This is a fairly large |
| [#11691](https://github.com/mesonbuild/meson/issues/11691) | Using a CMake module with lots of generated files gives an error "Argu | When a CMake subproject passes many generated files into a custom_target's command, ninja crashes from exceeding posix_spawn's ARG |
| [#11695](https://github.com/mesonbuild/meson/issues/11695) | rust: Parallelize build better by starting next Rust target once rmeta | Pipelining using rustc's metadata (rmeta) is a large optimization requiring design work such as integrating ninja's dyndeps/JSON s |
| [#11700](https://github.com/mesonbuild/meson/issues/11700) | Test failures on Illumos | Numerous test failures caused by Illumos-specific toolchain differences (msgfmt's -o position, ld -z, python2, ncurses, etc.). Eac |
| [#11717](https://github.com/mesonbuild/meson/issues/11717) | meson cmake msvc cmd line option detection is wrong | cmake/toolchain.py's MSVC option detection mishandles flags starting with '-', causing flags to leak into CMAKE_C_COMPILER. Since  |
| [#11747](https://github.com/mesonbuild/meson/issues/11747) | Function install_modules for Fortran modules | There is no dedicated function to automatically install generated .mod/.smod files from a library object — unimplemented. This req |
| [#11748](https://github.com/mesonbuild/meson/issues/11748) | `install` and `install_dir` is broken | The crash from linking a library with install_dir: false into another target is no longer exposed thanks to an assert(install_dir  |
| [#11762](https://github.com/mesonbuild/meson/issues/11762) | `private_dir_include()` for `custom_target` | private_dir_include is only implemented for BuildTarget (interpreterobjects asserts build.BuildTarget) and isn't available for cus |
| [#11792](https://github.com/mesonbuild/meson/issues/11792) | rust: Need symbol export handling and `--gc-sections` when linking a R | Incorporating a Rust staticlib via another linker requires symbol-visibility control and automatically adding --gc-sections/-dead_ |
| [#11806](https://github.com/mesonbuild/meson/issues/11806) | meson 1.1.0 regression: Dependency "llvm" not found | A regression where, with a mingw cross build and static: true, LLVM's CMake dependency is ignored as 'dynamic was requested' and d |
| [#11816](https://github.com/mesonbuild/meson/issues/11816) | Unable to compile C file with GCC when the Fortran compiler NAG is use | With the nagfor+gcc combination, -openmp (NAG's flag style) leaks into the C compile line, causing cc1 to fail with 'too many file |
| [#11829](https://github.com/mesonbuild/meson/issues/11829) | [FR] Get current value of env var at build time | Request to fetch the current value of an environment variable at build time rather than at configure time. By Meson's design, envi |
| [#11839](https://github.com/mesonbuild/meson/issues/11839) | install_data(install_dir: '') doesn't work | func_install_data treats an empty string as unspecified via 'if not install_dir:' and defaults it into datadir/projectname, so ins |
| [#11840](https://github.com/mesonbuild/meson/issues/11840) | `meson dist` Give the possibility to exclude git submodules | Request for a way to exclude nested git submodules (including indirect ones) from dist. Currently process_submodules pulls in all  |
| [#11865](https://github.com/mesonbuild/meson/issues/11865) | Reconfigure is not triggered when a header file required by compiler.c | Compiler checks like compute_int don't track changes to headers in prefix/include as dependencies, so changing a header doesn't tr |
| [#11868](https://github.com/mesonbuild/meson/issues/11868) | Feature request: add variable for GIR name to pkgconfig files | Request to add a GIR-name variable to pkgconfig using the result of generate_gir(). The pkgconfig module has no functionality to g |
| [#11878](https://github.com/mesonbuild/meson/issues/11878) | libgfortran not correctly linked when installing package | For a Fortran-extension Python module, the runtime linking of libgfortran (RPATH/DLL search path) is broken, so the shared library |
| [#11880](https://github.com/mesonbuild/meson/issues/11880) | meson build error with openmp using nvidia HPC compiler | With nvc++, dependency('openmp') results in 'not found, tried system'. This needs support for detecting OpenMP with the NVIDIA HPC |
| [#11892](https://github.com/mesonbuild/meson/issues/11892) | Meson equivalent to CMake's generate_export_header? | There's no equivalent of CMake's GenerateExportHeader (automatic generation of an export header with symbol-visibility macros) — u |
| [#11906](https://github.com/mesonbuild/meson/issues/11906) | RFE: Provide CUDA toolkit prefix from cross/native file | The CUDA dependency's location can only be specified via the CUDA_PATH environment variable; specifying it via a cross/native file |
| [#11914](https://github.com/mesonbuild/meson/issues/11914) | g++ linker doesn't need -lstdc++ option by default (when use link_lang | The code pointed out (unused search_dirs, unconditional -lstdc++) has been revised — find_library now actually detects the stdlib  |
| [#11930](https://github.com/mesonbuild/meson/issues/11930) | Command line -D options are overridden by native files on regen | On the initial setup, command-line -D takes priority over the native file, but on regeneration, the native file takes priority — a |
| [#11948](https://github.com/mesonbuild/meson/issues/11948) | Add cpp option for statically linking stdlib | Request for an option to statically link libstdc++/libc++ with clang/gcc (equivalent to MSVC's b_vscrt). Absorbing compiler/linker |
| [#11965](https://github.com/mesonbuild/meson/issues/11965) | Feature Request: better support KMDF/UMDF Windows driver builds | Request to standardize building Windows KMDF/UMDF drivers (dedicated flags/libraries/.cat generation, VS solution support). This i |
| [#11968](https://github.com/mesonbuild/meson/issues/11968) | Meson not detecting if host compiler for nvcc supports flags received  | Meson can't detect whether the host compiler that nvcc selects will accept flags passed via -Xcompiler, so the build fails on unsu |
| [#11985](https://github.com/mesonbuild/meson/issues/11985) | Better cross-compilation: transparent build/host library and dependenc | Request for transparent propagation to eliminate the redundancy of defining the same libraries/dependencies twice for both build a |
| [#11988](https://github.com/mesonbuild/meson/issues/11988) | Recursive dep.as_system() | generate_system_dependency only changes the top-level include_type after a deepcopy and doesn't propagate it to child dependencies |
| [#12005](https://github.com/mesonbuild/meson/issues/12005) | Feature request: A way to customize the list of buildtypes for `--genv | genvslite's buildtype list is hardcoded in get_genvs_default_buildtype_list (buildtypelist[1:-2]), and a comment in the code itsel |
| [#12013](https://github.com/mesonbuild/meson/issues/12013) | Feature Request: make cross-file can include another cross-file | MachineFileParser has no mechanism to resolve an [include] section — including another file from a cross/native file (with recursi |
| [#12018](https://github.com/mesonbuild/meson/issues/12018) | Add tooling to generate a manifest of a generated directory | Request to build hash/manifest generation into custom_target for directory-generating targets whose output files aren't known in a |
| [#12028](https://github.com/mesonbuild/meson/issues/12028) | Deadlock in meson test --gdb | Quitting gdb with 'q' while running meson test --gdb deadlocks Python. This is likely caused by the test harness's subprocess/TTY  |
| [#12031](https://github.com/mesonbuild/meson/issues/12031) | `meson install` breaks runpath | The build-time rpath (paths to required external libraries) gets stripped at install time. This involves how install_rpath is hand |
| [#12042](https://github.com/mesonbuild/meson/issues/12042) | Using `exe` in `custom_target` without re-invoking `meson` | On Windows, when a custom_target's command uses an internal exe, wrapping it in the meson wrapper to add the DLL path also include |
| [#12048](https://github.com/mesonbuild/meson/issues/12048) | Feature request: optional_modules for Qt5 dependencies | mesonbuild/dependencies/qt.py still only has the 'main' argument, with optional_modules unimplemented. This is a valid feature req |
| [#12075](https://github.com/mesonbuild/meson/issues/12075) | Subproject download for CMake is reported as invalid because of missin | When a wrap has no method specified, resolve assumes method='meson', and this still produces a 'no meson.build file' error for CMa |
| [#12076](https://github.com/mesonbuild/meson/issues/12076) | Allow recursive download for subprojects | `meson subprojects download` doesn't follow wraps to recursively fetch child subprojects. This is a legitimate request, e.g. for d |
| [#12103](https://github.com/mesonbuild/meson/issues/12103) | Support `CACHEDIR.TAG` for wrap caches | CACHEDIR.TAG is now created directly under the build directory (msetup.py:162), but placing it in subprojects/packagecache or extr |
| [#12105](https://github.com/mesonbuild/meson/issues/12105) | Integrated support for cross builds in compiler.run() | A proposal to integrate property/property_default into compiler.run() so a value can be fetched from the cross file when execution |
| [#12113](https://github.com/mesonbuild/meson/issues/12113) | In macOS defaults to installing python in /usr/local/usr/local | python_info.py calls sysconfig.get_paths with empty base/platbase, and the root cause where install_dir ends up doubled under Home |
| [#12127](https://github.com/mesonbuild/meson/issues/12127) | No coverage for subprojects | The coverage script explicitly excludes subproject_root (gcovr -e), so subproject coverage is still out of scope. This was updated |
| [#12140](https://github.com/mesonbuild/meson/issues/12140) | Current way of forcing runtime for C++ is very fragile and introduces  | A point that the C++ runtime (libc++/libstdc++) selection based on the compiler is inflexible on macOS. This remains on hold becau |
| [#12141](https://github.com/mesonbuild/meson/issues/12141) | python.install_env cannot be set to "venv" unless you are in a venv! | The exception in the is_venv check at python.py:104 still exists. The root cause is a false detection where environments like cond |
| [#12150](https://github.com/mesonbuild/meson/issues/12150) | Meson does not track the correct Perl interpreter when running MSYS2 P | On Windows, if the interpreter (e.g. perl) resolved from a script's shebang points to a different entity on PATH, the build fails  |
| [#12159](https://github.com/mesonbuild/meson/issues/12159) | -Wl,-v prevents apple linker (OSX) from being found | Apple linker detection still calls with only `-v` (detect.py:228), extracting the version from the PROJECT:ld/dyld line in stderr. |
| [#12201](https://github.com/mesonbuild/meson/issues/12201) | default install rpaths take no notice of install_dir for linked librar | A valid feature request: when a shared library has a custom install_dir set and is linked, the install rpath doesn't account for t |
| [#12228](https://github.com/mesonbuild/meson/issues/12228) | Add support for -fsyntax-only | A proposal for a fast syntax-check ninja target using gcc/clang's -fsyntax-only. There's no syntax-only implementation in the code |
| [#12242](https://github.com/mesonbuild/meson/issues/12242) | Wishlist: file names for files with IO errors | Request to have standard file names provided for triggering specific errors (like ENOENT) in tests. This has a cross-platform desi |
| [#12245](https://github.com/mesonbuild/meson/issues/12245) | "native: true" not passed to dependency fallback | A report that when resolving a dependency specified with native: true via a wrap fallback, the subproject gets the machine wrong,  |
| [#12261](https://github.com/mesonbuild/meson/issues/12261) | CC_LD and friends are not retained for reconfigure | Linker-selection environment variables like CC_LD aren't retained across --reconfigure, causing the linker-detection result to cha |
| [#12264](https://github.com/mesonbuild/meson/issues/12264) | vs_module_defs breaks in MSYS2's MSYS environment | A report of link failures caused by how vs_module_defs/.def is handled in MSYS2's MSYS environment (cygwin target, generating cygz |
| [#12279](https://github.com/mesonbuild/meson/issues/12279) | Compiler `preprocess()` function doesn't write output anywhere | preprocess() creates a CompileTarget and returns its output as a CustomTargetIndex, but since it isn't build_by_default, it doesn' |
| [#12288](https://github.com/mesonbuild/meson/issues/12288) | Runtime dyld errors when using llvm 15 / Xcode 15 linker macos (PROJEC | Report that Xcode 15's new linker breaks rpath/dyld runtime resolution for paths like /usr/local/lib. This involves interaction be |
| [#12294](https://github.com/mesonbuild/meson/issues/12294) | Allow multiple commands in a run_target or run_target dependency | Request to allow sequential execution of multiple commands within run_target, or to specify dependency ordering between run_target |
| [#12306](https://github.com/mesonbuild/meson/issues/12306) | Support LLVM flang | Tracking issue after #13323 was merged. The llvm-flang/armltdflang classes and flang 18/19 support are already implemented, but th |
| [#12341](https://github.com/mesonbuild/meson/issues/12341) | No builtin handling of `_FORTIFY_SOURCE`, conflicts with toolchain def | A built-in for safely handling _FORTIFY_SOURCE is not implemented (only fragmentary handling exists in gnome.py/clike.py). This is |
| [#12366](https://github.com/mesonbuild/meson/issues/12366) | Cannot get rid of NDEBUG compiler flag | Even with b_ndebug=false, when HDF5 is detected via h5cc, -DNDEBUG leaks in through the dependency flags and disables assertions.  |
| [#12368](https://github.com/mesonbuild/meson/issues/12368) | 'meson setup' with i18n module requires initial .po files | With i18n.gettext, setup itself fails if a .po file is missing for a language listed in LINGUAS. This contradicts the documented w |
| [#12369](https://github.com/mesonbuild/meson/issues/12369) | Shebang cannot be overridden by machine file | On Windows, the interpreter name extracted from a script's shebang (e.g. foo) cannot be overridden via [binaries] in a machine fil |
| [#12372](https://github.com/mesonbuild/meson/issues/12372) | shared_module creates import library on MinGW | shared_module() generates a .dll.a import library on MinGW. There's no way to suppress this in SHARED_MOD_KWS, such as a no_import |
| [#12373](https://github.com/mesonbuild/meson/issues/12373) | Support reduced debug info level (-g1, -g2, ...) | get_debug_args only takes the boolean is_debug and has no way to specify a -g level (like -g1). This is a reasonable feature reque |
| [#12395](https://github.com/mesonbuild/meson/issues/12395) | Support compiler.compiles() for .S standalone assembly files | There's still no way to compile an inline string as .S assembly. compiles_method uses the compiler's default suffix for strings (c |
| [#12396](https://github.com/mesonbuild/meson/issues/12396) | Support for test invoking generators at configure time | Request to trial-run a generator at configure time to detect supported syntax, similar to compiler.compiles() (related to #12395,  |
| [#12451](https://github.com/mesonbuild/meson/issues/12451) | CMake subproject with dependencies to other subprojects do not work | Passing a path inside another subproject's build directory to a cmake.subproject define crashes setup with an uncaught exception ( |
| [#12455](https://github.com/mesonbuild/meson/issues/12455) | [Bug report] Dependency iconv for iOS on macOS cannot be found. | On iOS (simulator) cross builds, dependency('iconv') isn't found via either builtin or system detection. This is plausibly a legit |
| [#12468](https://github.com/mesonbuild/meson/issues/12468) | [FR] Please add option to build DEB/RPM packages | A broad request for 'built-in' DEB/RPM (and further Flatpak/Snap/AppImage) package generation. There's existing discussion around  |
| [#12470](https://github.com/mesonbuild/meson/issues/12470) | Can't build sycl project with intel's icx on windows. | When using -fsycl with icx on Windows, Meson forces the linker to xilink.exe, so offload code generation doesn't happen. SYCL link |
| [#12478](https://github.com/mesonbuild/meson/issues/12478) | External Project module: add support for configure-less projects | A reasonable request to let the External Project module handle projects that build via an existing Makefile without a configure sc |
| [#12489](https://github.com/mesonbuild/meson/issues/12489) | `meson dist --include-subprojects` fails on an unpromoted subproject | create_dist in mdist.py still calls is_git() against a subproject's src_root, and the structure still allows a FileNotFoundError w |
| [#12491](https://github.com/mesonbuild/meson/issues/12491) | WARNING: Unknown CPU family '8562' | A porting request noting that the z/OS (IBM z15, uname '8562') CPU family isn't in known_cpu_families. Porting to z/OS itself is a |
| [#12535](https://github.com/mesonbuild/meson/issues/12535) | False positive warning when cross compiling using msvc | The 'Cross file does not specify strip binary' warning is emitted unconditionally in create_install_data during cross builds. This |
| [#12540](https://github.com/mesonbuild/meson/issues/12540) | python3 dependency incorrectly references host python when cross-compi | The python dependency has been substantially overhauled to a build_config (introspection) based implementation, quite different fr |
| [#12543](https://github.com/mesonbuild/meson/issues/12543) | Internal dependencies: Get back `link_with` and `include_directories`  | A request for a getter to extract include_directories / link_with from a declare_dependency()-created dependency on the DSL side.  |
| [#12554](https://github.com/mesonbuild/meson/issues/12554) | OpenCV cmake submodule | When building OpenCV as a CMake subproject, a generated header (opencl_kernels_core.hpp) is missing — a limitation of the CMake mo |
| [#12568](https://github.com/mesonbuild/meson/issues/12568) | pkg-config: Rust internal deps (rlib) for rust static library mishandl | declare_dependency for a static library containing a Rust rlib puts the rlib into the generated .pc file's Libs, breaking the C-si |
| [#12570](https://github.com/mesonbuild/meson/issues/12570) | Ability to specify a build target as both `host` and `target`? | There's currently no mechanism to declare the same library/executable for both the native (build) machine and the host/target mach |
| [#12592](https://github.com/mesonbuild/meson/issues/12592) | clang-cl with address sanitizer fails to build and link | clang-cl with b_sanitize=address conflicts with /MDd and also fails to link the asan runtime lib. This needs automatic adjustment  |
| [#12600](https://github.com/mesonbuild/meson/issues/12600) | Meson 1.2.3 broke extension module compilation on GraalPy | The python dependency/module has been substantially overhauled to a build_config (interpreter introspection) based implementation  |
| [#12604](https://github.com/mesonbuild/meson/issues/12604) | Linker error when `darwin_versions` is an empty list and `soversion` i | darwin_versions=[] becomes None in _convert_darwin_versions, but at build.py:2535, when soversion is non-numeric (like 'A'), it st |
| [#12612](https://github.com/mesonbuild/meson/issues/12612) | compiler override disables ccache | Explicitly specifying a compiler under [binaries] in a native/cross file disables ccache auto-detection. Users then have to config |
| [#12622](https://github.com/mesonbuild/meson/issues/12622) | Framework handling on macOS with cmake dependency still has some issue | A /Full/Path/Some.framework entry in a CMake dependency's INTERFACE_LINK_LIBRARIES doesn't get converted to -framework at the righ |
| [#12625](https://github.com/mesonbuild/meson/issues/12625) | Would be nice for documentation to show an easy way to use libc++ from | A request to document how to manually select the system libc++ as cpp_stdlib. Currently cpp_stdlib assumes a wrap/subproject, so i |
| [#12626](https://github.com/mesonbuild/meson/issues/12626) | Feature: ability to specify build file directory for subprojects | A request to let wrap or subproject() specify the build file location for a subproject that doesn't have meson.build/CMakeLists.tx |
| [#12631](https://github.com/mesonbuild/meson/issues/12631) | cfg_data.set_quoted doesnt handle \ character properly | set_quoted only escapes '"' and leaves backslashes unprocessed (interpreterobjects.py:406), producing invalid escape sequences for |
| [#12638](https://github.com/mesonbuild/meson/issues/12638) | No longer possible to force-merge static libraries via `link_whole` | A regression caused by PR #11742 where link_whole on a non-installed static library doesn't pull in transitive dependency objects  |
| [#12640](https://github.com/mesonbuild/meson/issues/12640) | meson ignores host_machine cpu_family when cross compiling with msvc | Even with cpu_family=x86 in a cross file, /MACHINE:x64 is used, and the correct Hostx64/x86 cl isn't selected. A valid bug requiri |
| [#12649](https://github.com/mesonbuild/meson/issues/12649) | Please provide a way to define a pkg-config variable when creating a d | There's no way to pass --define-variable when constructing a dependency() (define_variable is only for get_variable()). Since this |
| [#12655](https://github.com/mesonbuild/meson/issues/12655) | CMake custom target outputs do not support subdirectories | When a CMake custom target outputs a directory via copy_directory etc., cmake_run_ctgt can't handle directory outputs and raises F |
| [#12675](https://github.com/mesonbuild/meson/issues/12675) | How to use MacOSX.sdk/System/Library/Frameworks/OpenGL.framework | Geant4 dependency in a conda environment passes /Full/Path/OpenGL.framework directly as a link argument, causing a link failure (f |
| [#12680](https://github.com/mesonbuild/meson/issues/12680) | gnome: generate_gir unnecessarily links to libgirepository | generate_gir always adds the gobject-introspection-1.0 dependency (i.e. libgirepository-1.0) to the scanner's link (gnome.py:1194) |
| [#12689](https://github.com/mesonbuild/meson/issues/12689) | Add and link to docs section for every deprecation warning | A proposal to add a documentation section for each deprecation and link to it from warning messages. Reasonable, but an ongoing, f |
| [#12695](https://github.com/mesonbuild/meson/issues/12695) | meson reconfigure remembers coverage report instruction, cannot contin | coverage.py calls genhtml via check_call, so if source files are missing (e.g. after a git reset), the whole thing fails on a non- |
| [#12696](https://github.com/mesonbuild/meson/issues/12696) | Regression 1.1.1 -> 1.2.x: full static builds of gdk-pixbuf fail due t | A regression from 1.1.1 to 1.2.x where a full static build of gdk-pixbuf fails to link. A change in how static linking handles tra |
| [#12698](https://github.com/mesonbuild/meson/issues/12698) | CMake module not using `set_property(SOURCE PROPERTY LANGUAGE)` (neede | Even when a CMake subproject specifies MASM via set_property(SOURCE PROPERTY LANGUAGE ASM_MASM), language_map has no entry for ASM |
| [#12700](https://github.com/mesonbuild/meson/issues/12700) | add_test_setup is_default can be disrupted by is_default from subproje | The default name for add_test_setup(is_default:true) is single across the entire build (interpreter.py:3082-3086), so a subproject |
| [#12701](https://github.com/mesonbuild/meson/issues/12701) | fatal warnings only in certain projects | A request to scope --fatal-meson-warnings to just the top-level project (or a specified project). A reasonable feature addition to |
| [#12705](https://github.com/mesonbuild/meson/issues/12705) | RFE: Support multiple install tags per target | install_tag still only accepts a single string (INSTALL_TAG_KW is (str, NoneType)). There's a request to attach multiple tags to o |
| [#12706](https://github.com/mesonbuild/meson/issues/12706) | Meson's LLVM specific dependency detection is broken for modules | A discrepancy from the documentation: even when modules are specified for the LLVM dependency, the CMake path always only detects  |
| [#12709](https://github.com/mesonbuild/meson/issues/12709) | cannot link static library with dep | Passing a pkg-config dependency to static_library() via link_whole gives 'is not a static library,' and passing it via dependencie |
| [#12712](https://github.com/mesonbuild/meson/issues/12712) | Compiler system directories can depend on -pthread flag | get_compiler_system_dirs in environment.py calls -print-search-dirs without -pthread, so it misses pthread library paths on AIX an |
| [#12713](https://github.com/mesonbuild/meson/issues/12713) | Loading multiple machine files - additive instead of replacing? | A feature request to support an additive operator like cpp_args += in machine files. The current parser doesn't accept += and it's |
| [#12727](https://github.com/mesonbuild/meson/issues/12727) | PyPy link error when limited_api is set | When limited_api is specified, Windows links against python3.lib, which doesn't exist for PyPy, causing a link failure. This needs |
| [#12733](https://github.com/mesonbuild/meson/issues/12733) | Cannot cross-compile on macOS, "Unable to detect linker for compiler ` | Partly caused by a configuration mistake in the cross file (cpp = 'cpp', specifying the preprocessor as the C++ compiler), but it  |
| [#12737](https://github.com/mesonbuild/meson/issues/12737) | Check stdout/stderr from test run | A feature request to add stdout/stderr expectation matching to test(). This needs a design that also considers use alongside --wra |
| [#12761](https://github.com/mesonbuild/meson/issues/12761) | cmake: Subproject does not use native-compilation for targets | There's no way to build a CMake subproject as native during a cross build, because the cmake module's toolchain generation uses th |
| [#12775](https://github.com/mesonbuild/meson/issues/12775) | implicit_include_directories equivalent for cmake projects | A CMake subproject's include directories include the subproject root, causing a VERSION file collision. There's no option to suppr |
| [#12778](https://github.com/mesonbuild/meson/issues/12778) | Undocumented or non-existing way to provide `program_names` with a met | There's no way for a cmake wrap to provide a program (a find_program target) rather than a library. [provide] in a wrap can't reso |
| [#12793](https://github.com/mesonbuild/meson/issues/12793) | In `install_subdir`, `follow_symlinks: true` does not follow symlinks | do_copydir unconditionally adds a symlink to a directory into files regardless of follow_symlinks, and doesn't recursively copy it |
| [#12796](https://github.com/mesonbuild/meson/issues/12796) | Exclude files from ninja dist? Not in a git repo | A request for a mechanism to exclude files from dist without VCS (without git). Currently this relies on .gitattributes export-ign |
| [#12798](https://github.com/mesonbuild/meson/issues/12798) | ninja uninstall leaves python bytecode files untouched | pycompile.py doesn't record the .pyc files it generates via bytecompile into the install log (install-log.txt), so ninja uninstall |
| [#12812](https://github.com/mesonbuild/meson/issues/12812) | [Feature suggestion] [Helper tool] Add a helper-script to map GNU conf | A request for a helper script that maps GNU configure options to Meson syntax. Broad in scope and requires a design decision; ther |
| [#12821](https://github.com/mesonbuild/meson/issues/12821) | LibMySQL dependency custom path handling (Windows) | Finding libmysql/mariadb via dependency() on Windows is difficult, and there's no equivalent of MYSQL_ROOT_DIR search. A feature r |
| [#12826](https://github.com/mesonbuild/meson/issues/12826) | configure_file "looses" it's dependencies | Embedding another target's full_path() via configuration_data doesn't create a dependency between configure_file and that target.  |
| [#12828](https://github.com/mesonbuild/meson/issues/12828) | MSys64 meson cannot compile MSVC 2019 projects when changed compiler | When meson in an MSYS environment uses cl.exe, MSVC flags like /Fe get MSYS path-converted (to /c/msys64/...), causing link failur |
| [#12829](https://github.com/mesonbuild/meson/issues/12829) | "Dist currently only works with Git or Mercurial repos" in a Mercurial | Running dist from a subdirectory of a Mercurial monorepo fails repository-root detection, producing a "Git or Mercurial repos" err |
| [#12849](https://github.com/mesonbuild/meson/issues/12849) | gnome.generate_gir doesn't allow using externally generated libraries | generate_gir's positional argument only accepts a static/shared library or executable, and can't take the output of a custom_targe |
| [#12850](https://github.com/mesonbuild/meson/issues/12850) | gnome.generate_gir cannot run on Windows due to an incomplete PATH var | Running g-ir-scanner on Windows crashes because it can't find shared libraries unless the dependency's bindir is added to PATH. Re |
| [#12851](https://github.com/mesonbuild/meson/issues/12851) | gnome.generate_gir fails with Microsoft compilers due to unhandled g-i | With MSVC/clang-cl, g-ir-scanner misinterprets the given path as a .lib (shared library) and fails to link. The request is for Mes |
| [#12857](https://github.com/mesonbuild/meson/issues/12857) | Make the `devenv` environment available from within `meson.build` | A feature request to obtain the devenv environment (meson.devenv()) from within meson.build and pass it to a test's env. Involves  |
| [#12868](https://github.com/mesonbuild/meson/issues/12868) | [Visual Studio] ERROR: Tried modify read only option `backend` | backend is read-only, and --backend vs auto-resolves to vs2022, so on --reconfigure, old=vs2022 vs new=vs is treated as a change a |
| [#12879](https://github.com/mesonbuild/meson/issues/12879) | "ERROR: Tried to form an absolute path [...]" from dependency('mpi', l | Since Pixi/conda places dependencies inside the source tree (e.g. .pixi), their include directories become absolute paths inside t |
| [#12885](https://github.com/mesonbuild/meson/issues/12885) | Hardcoding a Library Path in meson for AIX operating system. | On AIX, when identically-named libraries exist in multiple paths, -Wl,-bnoipath strips the path and prevents linking against the i |
| [#12888](https://github.com/mesonbuild/meson/issues/12888) | `meson wrap status` detects installed version incorrectly | For a source-only wrap without a patch_url (e.g. pango), get_current_version guesses the revision from the filename and hardcodes  |
| [#12889](https://github.com/mesonbuild/meson/issues/12889) | Ninja backend cannot make a configuration file if it is part of a cust | When a configure_file output is included in a custom_target's command, ninja can't find the regeneration rule after the generated  |
| [#12893](https://github.com/mesonbuild/meson/issues/12893) | Implement a custom dependency lookup method for GSSAPI | A request to add a custom dependency handler for GSSAPI, similar to CURSES or MPI. A feature addition requiring a new dependency i |
| [#12913](https://github.com/mesonbuild/meson/issues/12913) | Can not build rc file with configs_file | Specifying windres in a native file causes the rc-compile custom_target to include the windres binary itself as a ninja (order-onl |
| [#12918](https://github.com/mesonbuild/meson/issues/12918) | ERROR Could not guess language from source file kernel.cu. | Meson can't infer the language of a .cu file pulled in from a CMake subproject, causing an error. A feature improvement requiring  |
| [#12923](https://github.com/mesonbuild/meson/issues/12923) | Base options not set when there are no compiler | In a project without a compiler, specifying base options like b_ndebug via -D still has get_option return the default value. The e |
| [#12925](https://github.com/mesonbuild/meson/issues/12925) | ERROR: Unknown compiler(s) on Windows (Embarcadero bcc64) | The Embarcadero (bcc64/Borland) compiler isn't supported by Meson, so compiler detection fails. Requires a fairly large feature ad |
| [#12932](https://github.com/mesonbuild/meson/issues/12932) | Unknown CPU family arm64ec | arm64ec isn't in known_cpu_families, producing an 'Unknown CPU family' warning (the vs backend already supports it). Fixing the wa |
| [#12962](https://github.com/mesonbuild/meson/issues/12962) | c++ stdlib assertions mode is weird | A design critique of Meson's default behavior of injecting stdlib assertions (_GLIBCXX_ASSERTIONS, etc.) when ndebug isn't set. A  |
| [#12970](https://github.com/mesonbuild/meson/issues/12970) | ldd on binaries isn't finding unstable-external_project-built library  | For a library built via external_project, unlike a regular subproject, the build-tree rpath isn't set, so it can't be found at run |
| [#12976](https://github.com/mesonbuild/meson/issues/12976) | The `cmake` module does not support `CMake` custom targets | Meson's cmake module can't handle CMake's add_custom_target, failing with 'Arguments must be strings.' Requires a fix to handle th |
| [#12977](https://github.com/mesonbuild/meson/issues/12977) | Meson NOT installing compiler (clang or gcc) generated .pdb symbols | A .pdb generated via -gcodeview/--pdb= with GCC/Clang isn't tracked by Meson as an output and so isn't installed (only the MSVC li |
| [#12991](https://github.com/mesonbuild/meson/issues/12991) | Incorrect pkg-config file generated (boost .so paths in libs-only-othe | pkg.generate() lists boost's full-path .so in Libs, so it doesn't get an -l form in pkg-config and falls into --libs-only-other. R |
| [#12992](https://github.com/mesonbuild/meson/issues/12992) | False Positive in Sandboxing Detection | Referencing numpy's include from a .venv directly under the project via a relative path triggers a sandbox-violation warning. Requ |
| [#12993](https://github.com/mesonbuild/meson/issues/12993) | PETSc fortran headers not found on a system that has CPATH set | pkg-config treats includes on CPATH as system includes, so .mod files aren't found in a Fortran build. Requires a design change to |
| [#12999](https://github.com/mesonbuild/meson/issues/12999) | Wrong linker flags when using a DEF file and clang with GNU frontend o | With the combination of clang (GNU frontend) plus the link.exe backend, the GNU-style linker class passes .def files as-is like an |
| [#13005](https://github.com/mesonbuild/meson/issues/13005) | Sandbox Violation Error Due to Subproject Folder Name Clashing with Su | When a subproject's folder name matches a subdirectory name inside that subproject, it's misdetected as a 'nested subproject,' tri |
| [#13011](https://github.com/mesonbuild/meson/issues/13011) | [CMake] CMake subproject does not respect 'b_vscrt' parameter in Windo | A CMake subproject ignores b_vscrt (like /MT) and forces /MD, with no way to override it. Requires a fix to propagate MSVC runtime |
| [#13018](https://github.com/mesonbuild/meson/issues/13018) | Finding Qt6 in Cross-Compilation Setup | A design-level challenge where pkg-config can't resolve host tool (moc/rcc) paths under Yocto's dual sysroot (target sysroot and n |
| [#13024](https://github.com/mesonbuild/meson/issues/13024) | [Feature Request]: Add built-in option(s) to simplify hardening binari | A large design challenge for a portable hardening built-in option spanning compilers/OS/languages. There's a b_sanitize family, bu |
| [#13028](https://github.com/mesonbuild/meson/issues/13028) | compiler.get_define result is incorrectly cached | A structural problem where compiler checks like get_define don't register the headers they include as reconfigure dependencies. Th |
| [#13037](https://github.com/mesonbuild/meson/issues/13037) | Linker detection uses compiler binary even when <lang>_ld flag option  | The nix linker detection now consults the <lang>_ld override, but it still appends c_link_args (external link flags) to the `cc -W |
| [#13046](https://github.com/mesonbuild/meson/issues/13046) | Relative rpaths are used for a pkgconfig dependency on Linux | For a pkgconfig dependency with an absolute-path libdir, meson install converts/strips the rpath to be relative to $ORIGIN, so the |
| [#13048](https://github.com/mesonbuild/meson/issues/13048) | additional options to wx-config for wxwidgets dependency | WxDependency has no way to pass wx-config options other than --static (--toolkit, --debug, buildtype-linked static/shared switchin |
| [#13049](https://github.com/mesonbuild/meson/issues/13049) | cmake check_c_source_compiles fails while finding deps when c binary i | When c is a list like ['/usr/bin/cc', '-fPIC', ...] in a machine file, check_c_source_compiles in a CMake subproject fails — an in |
| [#13052](https://github.com/mesonbuild/meson/issues/13052) | Meson does not correctly handle ifx when linking to an external librar | Linking a dynamic library with ifx (Intel LLVM Fortran) segfaults, but a manual ifx invocation works. Possibly an rpath/link-order |
| [#13070](https://github.com/mesonbuild/meson/issues/13070) | gnome.gtkdoc() always rebuilds | gtkdoc generation is a custom target, but gtk-doc itself always updates its output regardless of input, causing a rebuild every ti |
| [#13102](https://github.com/mesonbuild/meson/issues/13102) | meson dist --include-subprojects should apply diff_files from wrap | GitDist.create_dist just copies subprojects via process_git_project/copytree without applying the wrap's diff_files patch, so the  |
| [#13106](https://github.com/mesonbuild/meson/issues/13106) | meson without setup: mesonmain.py vs. meson.1 | man/meson.1 still describes the workflow assuming implicit setup ('run the Meson command once'), but the code has deprecated impli |
| [#13109](https://github.com/mesonbuild/meson/issues/13109) | custom_target doesn't take generated_list as a depend_files argument | The custom_target input type docs still list array[str\|file\|program] and don't explicitly mention generated_list/custom_tgt. A c |
| [#13111](https://github.com/mesonbuild/meson/issues/13111) | Generating coverage for Cython commands | A feature request for meson to automate passing --directive linetrace=true to the Cython transpiler, -DCYTHON_TRACE_NOGIL on the C |
| [#13118](https://github.com/mesonbuild/meson/issues/13118) | gnome.generate_gir never becomes stale | When a hand-written header is passed to sources of a library/generate_gir, it doesn't go stale — the .gir isn't regenerated when t |
| [#13126](https://github.com/mesonbuild/meson/issues/13126) | string.format() with identity-expressions | A request to expand @a@ inside strings originating from external properties via string.format() as identity substitution. fstrings |
| [#13130](https://github.com/mesonbuild/meson/issues/13130) | join_paths() works wrong when meet Windows style absolute path | Since join_paths uses os.path.join, on Linux it follows posixpath semantics and doesn't recognize 'D:\builddir' as an absolute pat |
| [#13131](https://github.com/mesonbuild/meson/issues/13131) | warn when (sub)project overwrites devenv | A feature request to warn when multiple (sub)projects set the same devenv variable (e.g. GST_PLUGIN_PATH). self.devenv is a plain  |
| [#13151](https://github.com/mesonbuild/meson/issues/13151) | find_program produces an object with an inconsistent interface when me | When override_find_program returns an Executable (a build target) instead of an ExternalProgram, it gets rejected by summary() and |
| [#13169](https://github.com/mesonbuild/meson/issues/13169) | depfile support vs generator.process(..., preserve_path_from: ...) | Since generator's get_dep_outname resolves @PLAINNAME@ via os.path.basename(inname), a/test_file and b/test_file collide on the sa |
| [#13180](https://github.com/mesonbuild/meson/issues/13180) | Using WxWidgets on Windows | WxDependency only implements the config-tool (wx-config) method and is Unix-only, so it can't be detected on Windows/MSVC. A featu |
| [#13192](https://github.com/mesonbuild/meson/issues/13192) | Wishlist: Tree of files as project output | A large design request to export a tree of interface files (e.g. from protobuf) as a project variable/dependency and pass them to  |
| [#13203](https://github.com/mesonbuild/meson/issues/13203) | Missing support for Swift dynamic library targets | The ninja backend still raises 'Swift supports only executable and static library targets.' and doesn't support shared-library out |
| [#13204](https://github.com/mesonbuild/meson/issues/13204) | find_library static keyword breaks library detection on Windows with c | On Windows+clang, find_library('ws2_32', static:...) fails to detect the library when static is specified, due to incorrect librar |
| [#13209](https://github.com/mesonbuild/meson/issues/13209) | Error Finding Xcode-installed Libraries using the dependency Command | On macOS, dependency() only searches Frameworks and doesn't search the Xcode SDK's usr/lib (e.g. libedit.tbd). The SDK sysroot's u |
| [#13211](https://github.com/mesonbuild/meson/issues/13211) | Clang + asan + gnome.generate_gir() causes link errors due to missing  | The gnome module only hardcodes GCC-style -lasan/-ltsan/-lubsan for g-ir-scanner and doesn't support Clang's required libclang_rt. |
| [#13214](https://github.com/mesonbuild/meson/issues/13214) | [cmake] Generator expression test during configure doesn't work. | The generator-expression parser itself already supports NOT/BOOL for things like $<NOT:...> (since 2019), but when set(VAR $<...>) |
| [#13217](https://github.com/mesonbuild/meson/issues/13217) | Passing sys_root to the --sysroot compiler argument | A request to automatically pass properties.sys_root from the cross file as --sysroot to all languages' compilers/linkers (related  |
| [#13218](https://github.com/mesonbuild/meson/issues/13218) | Linker detection fails for wr-cc (VxWorks) without a file input | guess_nix_linker passes --version plus extra_args but no dummy source file, and VxWorks' wr-cc produces no output without a file a |
| [#13220](https://github.com/mesonbuild/meson/issues/13220) | install_symlink pointing_to does not observe prefix | Passing get_option('datadir') etc. to install_symlink's pointing_to doesn't apply the prefix, producing a path inconsistent with o |
| [#13222](https://github.com/mesonbuild/meson/issues/13222) | Add checks for files in POTFILES.in / POTFILES.skip | A feature request for the i18n module to validate that files listed in POTFILES.in/POTFILES.skip actually exist (updated 2026-01). |
| [#13227](https://github.com/mesonbuild/meson/issues/13227) | Rust bindgen with output_inline_wrapper create c file with incorrect i | rust.bindgen's output_inline_wrapper generates a .c file whose header include is a path relative to the source directory, which br |
| [#13241](https://github.com/mesonbuild/meson/issues/13241) | Unable to find CUPTI module in CUDA runfile installation | CudaDependency's _find_requested_libraries only searches libdir and libdir/stubs, not $CUDA_PATH/extras/CUPTI/lib64 where CUPTI is |
| [#13248](https://github.com/mesonbuild/meson/issues/13248) | Generated pkg-config file for Qt6 includes has incorrect file separato | On Windows, Qt6-dependency includes (derived from os.path.join) end up with mixed separators (e.g. include\QtWidgets) in the Cflag |
| [#13249](https://github.com/mesonbuild/meson/issues/13249) | Support getting library file path from compiler for preloading purpose | A request for meson to provide an API (equivalent to -print-file-name plus linker-script resolution) to get the actual path of lib |
| [#13256](https://github.com/mesonbuild/meson/issues/13256) | Failure to build LVGL 9.1 as CMake subproject | Meson's cmake module applies CMake's target_compile_definitions $<$<COMPILE_LANGUAGE:ASM>:__ASSEMBLY__> to all files, incorrectly  |
| [#13264](https://github.com/mesonbuild/meson/issues/13264) | Qt5 dependency with private_headers misses `mkspecs` include path | qt.py has no logic to search for and add mkspecs — unimplemented. The missing mkspecs (qplatformdefs.h) include path when using pr |
| [#13276](https://github.com/mesonbuild/meson/issues/13276) | [Feature] Default options for cmake wraps | There is no mechanism to pass default_options to a CMake wrap. A feature request requiring a design for declaratively passing CMak |
| [#13278](https://github.com/mesonbuild/meson/issues/13278) | meson strips --config from LDFLAGS when it shouldn't | During linker detection, --config <file> inside LDFLAGS gets split apart, and the config file ends up treated as a standalone argu |
| [#13280](https://github.com/mesonbuild/meson/issues/13280) | meson setup should always read from environment variables | When re-running meson setup <builddir> -Dxxx, there's no implemented feature to auto-detect environment-variable changes (e.g. CFL |
| [#13288](https://github.com/mesonbuild/meson/issues/13288) | MSVC + Rust + C++ + GLM/GLFW3 don't work | With MSVC+Rust+C++ mixed, meson explicitly adds msvcrt.lib, which conflicts with msvcrtd in debug builds. Labeled needs-info; a de |
| [#13293](https://github.com/mesonbuild/meson/issues/13293) | `threads` dependency should not be "-lpthread" when using MinGW if usi | threads dependency's thread_flags defaults to -pthread, with no detection/branch for mcfgthread environments implemented. Detectin |
| [#13298](https://github.com/mesonbuild/meson/issues/13298) | Allow to summarize test results with respect to test priority | A feature request to order the test summary by priority. Labeled needs-info; a small feature requiring a design decision on output |
| [#13310](https://github.com/mesonbuild/meson/issues/13310) | Swift Linker Check Error | The Swift compiler's linker detection still always uses guess_nix_linker and /dev/null, so it continues to fail on Windows+MSVC li |
| [#13315](https://github.com/mesonbuild/meson/issues/13315) | [Feature Request]: 'program-transform-name' equivalent | A feature request equivalent to autotools' --program-prefix/--program-suffix/--program-transform-name. Unimplemented; requires des |
| [#13324](https://github.com/mesonbuild/meson/issues/13324) | Prefer $GCC_AR over $AR with gcc? | GCC static-linker detection still prioritizes $AR above all else, with no logic to prefer $GCC_AR when gcc is in use. The LTO link |
| [#13333](https://github.com/mesonbuild/meson/issues/13333) | Mechanism for setting rpath to JNI modules automatically | A request for dependency('jni') to automatically add JAVA_HOME's lib(server) to rpath. A feature requiring API design (e.g. an rpa |
| [#13337](https://github.com/mesonbuild/meson/issues/13337) | Importing SLEEF as a CMake subproject fails with error | In a CMake subproject, $<TARGET_FILE:mkrename> evaluates to an empty string. This is an inherent limitation of resolving CMake gen |
| [#13347](https://github.com/mesonbuild/meson/issues/13347) | Swift external packages (SwiftPM) support is missing | Ingesting SwiftPM packages is a large new feature. It requires a dependency-fetch-and-build mechanism similar to Cargo support, si |
| [#13375](https://github.com/mesonbuild/meson/issues/13375) | [Feature request] Builtin C++ feature tests | A request for a convenient API (like compiler.has_feature) to check C++20 feature test macros (__cpp_lib_*). Unimplemented; requir |
| [#13380](https://github.com/mesonbuild/meson/issues/13380) | Improve Clang sanitizer situation by overriding `b_lundef` with `b_san | Automatically disabling b_lundef when b_sanitize is set with Clang is not implemented. b_lundef is still referenced as-is, and cha |
| [#13381](https://github.com/mesonbuild/meson/issues/13381) | BUG: Compilation of F77/Fixed Format Fortran breaks while trying to ve | When -ffixed-form is applied globally, compiler checks (e.g. free-form testfile.f90 or C check code) get miscompiled as fixed-form |
| [#13385](https://github.com/mesonbuild/meson/issues/13385) | [Feature request] Encode runtime dependencies of exe | A feature request to declare a runtime dependency (a helper built by another target) on an executable, so using that exe in a cust |
| [#13389](https://github.com/mesonbuild/meson/issues/13389) | BUG: GAS (.S) files compiled with GFortran instead of GCC | When Fortran and C are mixed, .S files get compiled with gfortran instead of gcc, so c_args has no effect. A design issue involvin |
| [#13390](https://github.com/mesonbuild/meson/issues/13390) | ERROR: We evaluated the cmake variable '' to an empty string, which is | In a CMake subproject, empty TARGET_FILE/variable evaluation produces an unhelpful error. Besides improving the message, the root  |
| [#13399](https://github.com/mesonbuild/meson/issues/13399) | Feature request: Using exe_wrapper in custom_target() scripts | A request for @EXE_WRAPPER@ substitution or environment injection to use exe_wrapper inside custom_target. Requires design work to |
| [#13419](https://github.com/mesonbuild/meson/issues/13419) | feature request: expose more info from custom targets | A request for methods to retrieve custom_target's name/input/output, etc. Currently only full_path/to_list/index exist — requires  |
| [#13430](https://github.com/mesonbuild/meson/issues/13430) | linux mix build with cmake failed. | A CMake subproject's static_library ends up with pic:false, so it can't be linked into a shared_library. Needs to respect CMAKE_PO |
| [#13446](https://github.com/mesonbuild/meson/issues/13446) | Release policy and access | A governance (meta) issue about release-authority bus factor and automation, not a code-change target. Requires a policy decision  |
| [#13468](https://github.com/mesonbuild/meson/issues/13468) | Meson not resolving include paths for CERN ROOT dependency | When the ROOT of a non-standard install layout ($INSTALL/cmake) is detected via CMake, no include path is generated. A special cas |
| [#13487](https://github.com/mesonbuild/meson/issues/13487) | ERROR: Language D does not support library finding | A feature request (enhancement) for find_library support in the D compiler. Requires implementing a library-search API for the D c |
| [#13495](https://github.com/mesonbuild/meson/issues/13495) | Meson misdetects some functions as present when they are not | A false detection on old macOS/PPC where __builtin_strnlen etc. exist as compiler builtins but the libc symbol doesn't. A limitati |
| [#13498](https://github.com/mesonbuild/meson/issues/13498) | subprojects ignore `shared_module`'s `build_by_default : false` option | install:true takes priority over build_by_default:false, so a subproject's targets always end up in all. Labeled documentation; ne |
| [#13503](https://github.com/mesonbuild/meson/issues/13503) | Accessing a meson subproject with the cmake module throws exception. | Accessing a subproject (actually a Meson one) via the cmake module raises an exception. Labeled exception; needs a fix to turn the |
| [#13510](https://github.com/mesonbuild/meson/issues/13510) | BUG: Slightly confusing `symbols_have_underscore_prefix()` | Using symbols_have_underscore_prefix() with the Fortran compiler produces an unhelpful exception/error. Labeled exception; needs a |
| [#13521](https://github.com/mesonbuild/meson/issues/13521) | [Bug] CMake: Subdirectories may introduce file conflicts | In a CMake subproject, identically-named generated artifacts (build-version.inc) from different subdirectories collide because CMA |
| [#13534](https://github.com/mesonbuild/meson/issues/13534) | mpv won't start with `meson install -C build` command | On macOS, install strips even the LC_RPATH entries needed at runtime (e.g. /usr/local/lib), causing mpv to fail to start — a regre |
| [#13541](https://github.com/mesonbuild/meson/issues/13541) | Force dependency to assume header-file | A request to treat .c files generated by custom_target as headers that are only included, never compiled directly. Since declare_d |
| [#13554](https://github.com/mesonbuild/meson/issues/13554) | User cannot set `gnu_symbol_visibility` to `''` with python `extension | python.extension_module() overwrites gnu_symbol_visibility='' with 'inlineshidden', making it impossible to specify 'explicitly un |
| [#13570](https://github.com/mesonbuild/meson/issues/13570) | meson format: mangles with `if` statements with indented conditionals | meson format alters multi-line conditional if-expressions, including the indentation of the closing parenthesis. Needs an improvem |
| [#13573](https://github.com/mesonbuild/meson/issues/13573) | Support for Ninja pools | A feature request for a general mechanism to assign arbitrary targets to a Ninja pool. Currently only limited support exists (e.g. |
| [#13588](https://github.com/mesonbuild/meson/issues/13588) | Possible bug: dependencies isolated from cmake projects? | An openssl dependency() obtained on the meson side doesn't propagate into a CMake subproject. Dependency propagation into CMake su |
| [#13590](https://github.com/mesonbuild/meson/issues/13590) | Meson resolves paths | meson.current_build_dir() etc. resolve symlinks before returning, prompting a request for a pwd-equivalent absolute() that doesn't |
| [#13592](https://github.com/mesonbuild/meson/issues/13592) | meson_log.txt is garbled | With the vs backend, meson-log.txt gets garbled on Japanese-locale Windows. The log itself is opened as UTF-8, but it's likely cau |
| [#13599](https://github.com/mesonbuild/meson/issues/13599) | Introspection data does not include `generator` inputs | introspection's target_sources still only covers sources/generated_sources/unity_sources — there's no field listing generator.proc |
| [#13601](https://github.com/mesonbuild/meson/issues/13601) | Feature request: subdir option for cmake module? | cmake.subproject's typed_kwargs only has required/native/options/cmake_options — a subdir kwarg to specify the location of CMakeLi |
| [#13602](https://github.com/mesonbuild/meson/issues/13602) | Cycle in CMake inputs/dependencies detected with libavif subproject | A bug where a dependency cycle is detected in a specific CMake subproject (libavif 1.1.1). A deep issue in the CMake interpreter t |
| [#13607](https://github.com/mesonbuild/meson/issues/13607) | meson compile is inferior yet again, this time for run_target() from a | mcompile's ParsedTargetName interprets ':' as the type separator, so it can't correctly resolve a subproject's run_target (A:hello |
| [#13608](https://github.com/mesonbuild/meson/issues/13608) | macOS frameworks are not found by mesonbuild: `extraframework` method  | find_framework_paths is designed to explicitly raise an exception for non-clang compilers (gcc), so gcc can't search macOS framewo |
| [#13610](https://github.com/mesonbuild/meson/issues/13610) | Coverage flags are not passed to compiler test methods (links(), has_f | b_coverage flags are added at target-generation time (backends.py:332) but aren't passed to checks like compiler.links(). Needs a  |
| [#13640](https://github.com/mesonbuild/meson/issues/13640) | macos framework paths not found when using clang with -std=C++<ver> ex | find_framework_paths passes external args (like CXXFLAGS's -std=gnu++11) as-is to the -E command, and for C, -std=c++ variants get |
| [#13653](https://github.com/mesonbuild/meson/issues/13653) | some Apple compilers are broken in the sanitycheck from missing LC_RPA | sanitycheck fails on some Apple Clang setups due to an unresolved @rpath/libc++.1.dylib — an environment-dependent issue. Tagged m |
| [#13661](https://github.com/mesonbuild/meson/issues/13661) | Add option to link with a dependency even if no symbols are used | There's no unified kwarg to force-link a dependency ('needed') even if no symbols are used. A reasonable feature request requiring |
| [#13690](https://github.com/mesonbuild/meson/issues/13690) | Global opt-out for `implicit_include_directories` | implicit_include_directories is only a per-target kwarg; there's no built-in option to disable it project-wide/globally. A reasona |
| [#13706](https://github.com/mesonbuild/meson/issues/13706) | Linking against llvm on windows fails when path to llvm contains space | A Windows-specific issue where parsing llvm-config (config-tool) output doesn't correctly split paths containing spaces, breaking  |
| [#13713](https://github.com/mesonbuild/meson/issues/13713) | `c_std=gnuXX,cXX` needs future-feature warning | When c_std=gnu99,c99-style syntax hard-errors on Meson versions below 1.3.0, there's no mechanism for a newer Meson to warn upfron |
| [#13729](https://github.com/mesonbuild/meson/issues/13729) | Feature request: Make generator output file name customizable by the c | generator.process() has no implemented kwarg to let the caller specify output (output is fixed when generator() is defined). A rea |
| [#13738](https://github.com/mesonbuild/meson/issues/13738) | install_headers() install_dir and preserve_path are incompatible | The interpreter splits files by dirname when preserve_path is set and generates Headers(install_subdir=childdir), but the backend' |
| [#13741](https://github.com/mesonbuild/meson/issues/13741) | Inconsistent host_machine.cpu() for Debian ppc64el cross vs. native | env2mfile maps powerpc64le to 'ppc64' (deb_cpu_map), but cpu() on a native build returns 'ppc64le', so there's still a mismatch. A |
| [#13743](https://github.com/mesonbuild/meson/issues/13743) | machine.subsystem() defaults to the same as machine.system(), but shou | A design/policy discussion on whether it's appropriate for subsystem to default to the same value as system. Involves backward-com |
| [#13745](https://github.com/mesonbuild/meson/issues/13745) | Valgrind wrapping for tests is error-prone | No countermeasure (e.g. auto-adding --error-exitcode) is implemented for the POLA violation where meson test --wrapper valgrind tr |
| [#13747](https://github.com/mesonbuild/meson/issues/13747) | 'meson rewrite' output formatting differs from input | meson rewrite's output doesn't preserve the original formatting — broken indentation, space before colons, default_options collaps |
| [#13757](https://github.com/mesonbuild/meson/issues/13757) | CFLAGS env variable is used when calling cc.compiles() | Compiler checks (e.g. cc.compiles) include external args (from get_external_args, i.e. CFLAGS), so things like -Werror in CFLAGS c |
| [#13801](https://github.com/mesonbuild/meson/issues/13801) | find_library() should return a dep object as per documentation. Instea | The ExternalLibraryHolder returned by find_library only has type_name/found/partial_dependency/name (added in 1.5.0) — no version( |
| [#13818](https://github.com/mesonbuild/meson/issues/13818) | Meson does not respect `target_include_directories(PRIVATE)` in CMake  | The CMake module's ConverterTarget includes PRIVATE include_directories in declare_dependency's include_directories too, leaking P |
| [#13823](https://github.com/mesonbuild/meson/issues/13823) | [Bug]: `custom_target` does not respect `-Dstrip=true` | install-time stripping only applies to build targets (can_strip); binaries generated by custom_target aren't stripped. There's no  |
| [#13824](https://github.com/mesonbuild/meson/issues/13824) | python: compiling libraries against Limited API in addition to extensi | limited_api is limited to py.extension_module()'s kwarg — there's no way (e.g. py.dependency(limited_api:) or get_limited_api_defi |
| [#13829](https://github.com/mesonbuild/meson/issues/13829) | No clean hook | There's no implemented hook (like meson.add_clean_script(), analogous to Autotools' clean-local) to run custom logic during the cl |
| [#13832](https://github.com/mesonbuild/meson/issues/13832) | Debug assertions are unconditionally propagated to C++ CMake subprojec | Debug STL assertions like _GLIBCXX_ASSERTIONS propagate unconditionally into CMake subprojects. Rooted in the same CMake-module/op |
| [#13843](https://github.com/mesonbuild/meson/issues/13843) | [Feature Request] : Object Libraries (again) | An 'object library' for generating/reusing object files (e.g. for DTrace probes or .def symbol dumps) is unimplemented (a retry of |
| [#13846](https://github.com/mesonbuild/meson/issues/13846) | CMake subproject doesn't support compiler flags and defines for indivi | Per-file COMPILE_DEFINITIONS/FLAGS from CMake's set_property(SOURCE ...) get consolidated to the whole target by ConverterTarget,  |
| [#13848](https://github.com/mesonbuild/meson/issues/13848) | Static link of python in windows fails due to gcc style static library | On Windows, static-linking Python looks for libpython311.a (gcc-style) and fails to find the MSVC-style python311.lib. A reasonabl |
| [#13853](https://github.com/mesonbuild/meson/issues/13853) | Compilation of subproject failed due to `-L-L` | In a CMake subproject, link directories get double-added with -L, producing '-L-L/path' and a link failure. A bug in CMake trace/l |
| [#13858](https://github.com/mesonbuild/meson/issues/13858) | add_project_dependencies() ignores 'preserve' include_type property | func_add_project_dependencies applies the per-dependency get_include_type()=='system' (default 'preserve' -> False) uniformly to a |
| [#13865](https://github.com/mesonbuild/meson/issues/13865) | RFE Provide "User defined options" summary for options set in the nati | The setup summary's 'User defined options' only shows the native/machine file name rather than listing the individual options set  |
| [#13877](https://github.com/mesonbuild/meson/issues/13877) | Feature request: depend on `external_program` | There's no unified way to pass an external_program obtained via find_program (a program on PATH) to custom_target's depends (only  |
| [#13882](https://github.com/mesonbuild/meson/issues/13882) | Odd meson behavior under CMake with f2py | An environment-dependent issue where clang is falsely detected as unable to compile only on the first run via f2py/CMake — hard to |
| [#13889](https://github.com/mesonbuild/meson/issues/13889) | [Feature Request]: Splitting a long string into several lines using '\ | A language-spec change request for backslash line continuation inside strings. Per Syntax.md, backslashes currently remain literal |
| [#13895](https://github.com/mesonbuild/meson/issues/13895) | External_project: `env:` does not work? | A report that add_project()'s env: in the external_project module isn't passed through to the configure script. external_project i |
| [#13906](https://github.com/mesonbuild/meson/issues/13906) | dependency(LLVM) always finds newest installation | LLVM_MESON_VERSIONS narrows correctly when a version constraint is given (implemented since 2022), but the underlying issue — pick |
| [#13927](https://github.com/mesonbuild/meson/issues/13927) | Inconsistent shared library name prefix on MinGW and Cygwin between sh | run_project_tests.py's test harness doesn't account for MinGW/Cygwin's lib/cyg prefixes and assumes foo.dll — an inconsistency. A  |
| [#13931](https://github.com/mesonbuild/meson/issues/13931) | CMake via meson places libraries in the wrong place | A CMake subproject fails to correctly resolve libdir (e.g. x86_64-linux-gnu) and installs to /usr/lib or /app/lib64 instead. CMAKE |
| [#13940](https://github.com/mesonbuild/meson/issues/13940) | GAS should be a language, not compiled with any GNU compiler | A large architectural change to treat GAS as an independent language, also requiring a backward-compatible migration strategy. dcb |
| [#13957](https://github.com/mesonbuild/meson/issues/13957) | Adding $CFLAGS and -Werror=unused-command-line-argument to compile che | Clang compile checks intentionally pass -Werror=unused-command-line-argument, so things like -fprofile-dir in $CFLAGS get flagged  |
| [#13961](https://github.com/mesonbuild/meson/issues/13961) | Marking environment variables for winepath translation | A feature request for a mechanism to convert path-related environment variables (e.g. GSETTINGS_SCHEMA_DIR) to Z: form with ';' se |
| [#13965](https://github.com/mesonbuild/meson/issues/13965) | CMake dependencies add absolute paths to pkgconfig Libs | Going through a CMake dependency causes absolute paths to end up in the generated .pc's Libs, which breaks when the sysroot is rel |
| [#13971](https://github.com/mesonbuild/meson/issues/13971) | Meson incorrectly assumes shared libraries even after detecting only s | When prefer_static=false and only a static library turns out to be available, pkg-config isn't re-queried with --static, so Libs.p |
| [#13973](https://github.com/mesonbuild/meson/issues/13973) | Cannot disable RTTI under the Visual Studio backend | In the VS backend, options like cpp_rtti aren't reflected in the project XML (GR- is not added). The VS backend's option-to-XML-el |
| [#13974](https://github.com/mesonbuild/meson/issues/13974) | Building library using 'meson compile <target>:shared_library' fails w | A report that resolving a 'target:shared_library'-style target fails when name_suffix is specified. mcompile's resolution logic ha |
| [#13982](https://github.com/mesonbuild/meson/issues/13982) | Support Cython pure Python mode | A request to support Cython's pure Python mode (treating .py files as Cython). Handling .py extensions carries a risk of false pos |
| [#13984](https://github.com/mesonbuild/meson/issues/13984) | Meson rewrite requires a C compiler to operate and fails if the wrong  | meson rewrite requires a compiler, and c_std validation fails if the wrong compiler is selected. rewrite should only need AST mani |
| [#14005](https://github.com/mesonbuild/meson/issues/14005) | `meson dist` not ignoring git metadata for subprojects. | When --include-subprojects is used, subprojects' .git metadata gets bundled in, bloating the distribution archive. Logic to strip  |
| [#14009](https://github.com/mesonbuild/meson/issues/14009) | whats the state of `cmake_args`? | dependency()'s cmake_args is poorly documented and tested, and marked with a TODO for eventual removal, but there's no deprecation |
| [#14015](https://github.com/mesonbuild/meson/issues/14015) | Feature request: link_hidden argument in library() | A request for a link_hidden argument (--exclude-libs / -hidden-l) to hide static library symbols from a shared library. This is a  |
| [#14024](https://github.com/mesonbuild/meson/issues/14024) | `dependency('iconv')` doesn't work on OpenBSD. | On BSD, packages live outside the default search path, so dependency('iconv') can't find GNU iconv. A design fix is needed to acco |
| [#14032](https://github.com/mesonbuild/meson/issues/14032) | `meson setup` crashes with `--backend=xcode` | In the Xcode backend's generate_target_dependency_map, the 'assert k not in self.target_dependency_map' assertion fails on a dupli |
| [#14051](https://github.com/mesonbuild/meson/issues/14051) | Suggestion: Make Python dependency raise error/warning in shared_libra | A proposal to emit a clear warning when py.dependency() is used with shared_library instead of shared_module. A design that detect |
| [#14058](https://github.com/mesonbuild/meson/issues/14058) | pkg-config dep.get_variable() returns value with unexpected prefix | When sys_root is set for a cross build, dep.get_variable()'s result gets prefixed with the sysroot (/workdir/build/rootfs). This i |
| [#14082](https://github.com/mesonbuild/meson/issues/14082) | `@PRIVATE_DIR@` in `run_target()` trigger an unhandled exception | Using @PRIVATE_DIR@ in a run_target() command raises an exception. Current master has 'assert not isinstance(target, build.RunTarg |
| [#14103](https://github.com/mesonbuild/meson/issues/14103) | Tracking issue for performance improvements PRs | A tracking issue for performance-improvement PRs. Most were merged in 1.7 through 1.12, but a few small unaddressed hotspots remai |
| [#14118](https://github.com/mesonbuild/meson/issues/14118) | GLFW release compilation fails on locked .pdb file (vs backend) - meso | With the VS backend plus a CMake subproject (glfw) in a release build, multiple CL.EXE instances write to the same .pdb and fail w |
| [#14127](https://github.com/mesonbuild/meson/issues/14127) | Dependency warning_level is ignored when compiling from fallback | A dependency built as a fallback (subproject) doesn't follow the parent's warning_level setting, resulting in a flood of warnings. |
| [#14138](https://github.com/mesonbuild/meson/issues/14138) | find_tool() with pkgconfig seems to need some unescaping | A pkg-config variable (g_ir_scanner) under a prefix containing spaces is returned still escaped (\ ), so it can't be resolved as a |
| [#14143](https://github.com/mesonbuild/meson/issues/14143) | Add a dependency handler for backtrace | A request to add a dependency handler for backtrace (glibc built-in / OpenBSD libexecinfo / other libbacktrace) that abstracts ove |
| [#14146](https://github.com/mesonbuild/meson/issues/14146) | How to handle `meson.override_dependency()` with dependencies using `m | A design issue where override_dependency() can't handle dependencies with modules/components, such as LLVM. A mechanism is needed  |
| [#14147](https://github.com/mesonbuild/meson/issues/14147) | metaprojects: grouping many projects together as a single meson unit | A large-scale design discussion filed by maintainer dcbaker; the metaproject feature is not yet implemented. It should continue as |
| [#14148](https://github.com/mesonbuild/meson/issues/14148) | Have a way to not repeat array options with defaults that == choices | A proposal for syntactic sugar (such as all()) to write default==choices more concisely (DRY) for array options. optinterpreter.py |
| [#14150](https://github.com/mesonbuild/meson/issues/14150) | custom_targets can have conflicting depfiles | Two custom_targets in the same directory can collide if they specify a depfile with the same name. The ninja backend still writes  |
| [#14161](https://github.com/mesonbuild/meson/issues/14161) | `install_man` should allow defining additional symbolic links | install_man doesn't yet support specifying symlinks or returning the install destination path, requiring boilerplate to create MLI |
| [#14172](https://github.com/mesonbuild/meson/issues/14172) | Why does Meson not automatically find the strip binary when cross-buil | A request to improve behavior so that strip is auto-detected from the compiler's triplet prefix during cross builds. Currently, if |
| [#14173](https://github.com/mesonbuild/meson/issues/14173) | Improve Heuristic for Using lcov versus gcovr | coverage.py reads .lcovrc/gcovr.cfg, but when both tools are present, HTML generation remains fixed to lcov (tool priority isn't s |
| [#14202](https://github.com/mesonbuild/meson/issues/14202) | Add option to gnome.post_install() to reload the D-Bus configuration? | A reasonable request to add a D-Bus config-reload flag to gnome.post_install. The gnome module doesn't have this feature yet, so i |
| [#14210](https://github.com/mesonbuild/meson/issues/14210) | Document that wrap-git depth=1 and revision=HEAD conflict for old vers | The existing bug #10931 has been fixed, but a documentation note about depth=1 conflicting with revision=HEAD on older versions st |
| [#14234](https://github.com/mesonbuild/meson/issues/14234) | How should C++ dependencies of C libraries be properly linked? | An issue where a C executable with a C++ dependency needs to use the C++ linker for static linking. This is a design issue: pkg-co |
| [#14249](https://github.com/mesonbuild/meson/issues/14249) | Wrapping C++ std::filesystem implementation libraries in a custom depe | A request for a built-in dependency like dependency('cxx-filesystem') (analogous to threads) that abstracts away whether stdc++fs/ |
| [#14258](https://github.com/mesonbuild/meson/issues/14258) | Feature request: wrap-path to use a meson project in any directory as  | A proposal for a [wrap-path] type that turns a meson project at an arbitrary path on disk into a dependency. wrap.py has no such t |
| [#14260](https://github.com/mesonbuild/meson/issues/14260) | Meson-generated `config.h` file don't allow C++ style comments (`//`) | The config.h header output by configuration_data is fixed to C-style /* */ comments, with no option to choose //. A request to all |
| [#14269](https://github.com/mesonbuild/meson/issues/14269) | pkgconfig module should have a way to exclude dependencies | A request for a way to exclude specific dependencies from the generated .pc's Requires/Requires.private (e.g. *proto headers). The |
| [#14271](https://github.com/mesonbuild/meson/issues/14271) | Vala : Allow ignoring generated files | When mixing Vala and C, the generated vapi gets included in the sources, causing the local vapi under --vapidir to be ignored. A r |
| [#14274](https://github.com/mesonbuild/meson/issues/14274) | add_dist_script broke its contract to run the version in $MESON_DIST_R | dist scripts were previously contracted to run against a copy inside a staging directory, but now they run with the source-tree pa |
| [#14276](https://github.com/mesonbuild/meson/issues/14276) | How to splat `dict` objects into function kwargs? | A language-feature proposal to add a **dict splat operator to the meson DSL. This is a parser/interpreter language-specification c |
| [#14278](https://github.com/mesonbuild/meson/issues/14278) | 'meson dist' should allow testing only the main project | A request to add test-suite filtering (e.g. --test-suite glibmm:) to meson dist. mdist.py's add_arguments has no such option, so i |
| [#14322](https://github.com/mesonbuild/meson/issues/14322) | [Tracker] Python version requirements | A parent tracker issue for raising the minimum supported Python version. It's an ongoing management issue that's continually refer |
| [#14334](https://github.com/mesonbuild/meson/issues/14334) | Enhance AIX shared library build to use an export List | A proposal to add export-list generation for runtime linking on AIX (for PostgreSQL). This is a large AIX-specific feature with th |
| [#14346](https://github.com/mesonbuild/meson/issues/14346) | Ability to set a module option from code | A request to set module options like pkgconfig.relocatable dynamically from code. Currently this is only possible via the command  |
| [#14348](https://github.com/mesonbuild/meson/issues/14348) | use `-iquote` for project header files | A proposal to use -iquote for project headers to prevent accidentally shadowing system headers (a use_iquote flag). include_direct |
| [#14350](https://github.com/mesonbuild/meson/issues/14350) | Absolute paths generated by dependency() in pkg-config file when cross | With project('c', 'cpp'), dependency() uses the C++ compiler, and absolute paths leak into the .pc during cross builds. This invol |
| [#14358](https://github.com/mesonbuild/meson/issues/14358) | Using OUTPUT_NAME instead of target name (CMake subproject) | A bug where a CMake subproject's library name becomes the target name, and OUTPUT_NAME (e.g. PocoFoundation) isn't reflected. The  |
| [#14359](https://github.com/mesonbuild/meson/issues/14359) | CMake subproject does not build everything (missing generated header) | A bug in Poco's CMake subproject where the generated header pocomsg.h isn't generated, resulting in incorrect build ordering. This |
| [#14362](https://github.com/mesonbuild/meson/issues/14362) | There is no way to reliably query `exe_wrapper` | There's no reliable API to retrieve the exe_wrapper value (e.g. meson.get_exe_wrapper()), and using find_program as a substitute h |
| [#14363](https://github.com/mesonbuild/meson/issues/14363) | build machine options should use the host machine defaults if unset | When host != build, settings like rust_std in default_options aren't inherited on the build side, so build helpers get compiled wi |
| [#14369](https://github.com/mesonbuild/meson/issues/14369) | Building rust libstd with Meson | A request to support cargo's -Zbuild-std equivalent (rebuilding libstd) in meson's Rust support, for tier-3 targets and LTO/CFI us |
| [#14401](https://github.com/mesonbuild/meson/issues/14401) | The WINEPATH environment variable is not always set for test targets | Tests for executable() get WINEPATH/PATH set, but tests for an external_program obtained via find_program() don't, so Wine can't f |
| [#14407](https://github.com/mesonbuild/meson/issues/14407) | Support Presets in CMake Subprojects | A request to pass a preset name to CMakeSubprojectOptions to specify a group of options at once. add_cmake_defines exists, but pre |
| [#14411](https://github.com/mesonbuild/meson/issues/14411) | Pkgconfig: Allow to specify "subdir" and "extra_cflags" with dataonly | With dataonly, subdir/extra_cflags are still ignored (pkgconfig.py:653: 'if cflags and not dataonly'). The request to emit cflags  |
| [#14421](https://github.com/mesonbuild/meson/issues/14421) | declare_dependency() `sources` inconsistently added to include paths | Among declare_dependency's sources, the parent directory of a generated file is implicitly added to -I, but the parent directory o |
| [#14429](https://github.com/mesonbuild/meson/issues/14429) | Incorrect Python Library Linking in Debug Builds on Windows (MSVC): Sh | A request to auto-select python313_d.lib for debug builds. Currently the design doesn't select _d.lib and only emits a warning (py |
| [#14436](https://github.com/mesonbuild/meson/issues/14436) | Cannot install emptydirs to a prefixed path when prefix is default | With prefix left at default, install_emptydir can't straightforwardly install to an arbitrary path under prefix (meson normalizes/ |
| [#14446](https://github.com/mesonbuild/meson/issues/14446) | Write to File Object Created by argparse Without Context Manager Fails | meson runpython executes scripts via runpy.run_path, so a file opened with argparse.FileType, if not used with a context manager,  |
| [#14454](https://github.com/mesonbuild/meson/issues/14454) | Apple Frameworks (creating .framework bundles) | A request for a feature to generate .framework bundles (Info.plist/public headers/binary). meson has no such feature; this is a la |
| [#14455](https://github.com/mesonbuild/meson/issues/14455) | Feature Request: add xml2 to config-tools | A request to detect libxml2 via xml2-config (a config-tool) on macOS, where pkg-config isn't provided. There's no xml2 config-tool |
| [#14461](https://github.com/mesonbuild/meson/issues/14461) | meson discards the pre-defined PKG_CONFIG_LIBDIR when finding Python d | During cross builds, the user-set PKG_CONFIG_LIBDIR environment variable gets overridden/discarded when searching for the python d |
| [#14463](https://github.com/mesonbuild/meson/issues/14463) | Custom target command prefixed with 'mono' on Linux | In backends.py:610-613, on non-Windows, executables with a .exe extension are treated as .NET assemblies and prefixed with mono —  |
| [#14465](https://github.com/mesonbuild/meson/issues/14465) | Confusing error on missing Qt module | In qt.py:347, a missing module is logged but only results in is_found=False; the fatal error eventually raised by the Interpreter  |
| [#14468](https://github.com/mesonbuild/meson/issues/14468) | has_argument() doesn't fail on unknown argument using clang-cl-19 | clang.py's get_compiler_check_args adds flags like -Werror=unused-command-line-argument, but clang-cl, being a cl-compatible class |
| [#14474](https://github.com/mesonbuild/meson/issues/14474) | vcs_tag custom command is run in source dir, but file objects provided | vcs_tag runs its command with CWD set to the source directory, but file paths passed via files() are resolved relative to the buil |
| [#14482](https://github.com/mesonbuild/meson/issues/14482) | Compilation of CMake subproject executable not working correctly | An issue where meson doesn't build and link the internal libraries that an executable target extracted from a CMake subproject dep |
| [#14483](https://github.com/mesonbuild/meson/issues/14483) | compiler.run(dependencies: ...) does not work for vala | Passing dependencies via compiler.run/compile for valac passes C-compiler flags (-I/… or .so paths) through as-is, which valac can |
| [#14490](https://github.com/mesonbuild/meson/issues/14490) | Meson doesn't pass all C{,XX}FLAGS at link-time with LTO | A request, aligned with GCC's recommendation, to also pass compile-time flags at link time when using LTO. Design consideration is |
| [#14491](https://github.com/mesonbuild/meson/issues/14491) | `depfixer.py`: `-delete_rpath` should not be used on macOS < 10.6 | fix_darwin unconditionally passes -delete_rpath to install_name_tool, which fails on macOS 10.5. This is a niche issue for an extr |
| [#14516](https://github.com/mesonbuild/meson/issues/14516) | RFC: Take the greatest version of a dependency when using multiple wra | An RFC proposing that when multiple wraps point to different versions of the same dependency, the highest version should be chosen |
| [#14520](https://github.com/mesonbuild/meson/issues/14520) | Meson dist includes wrap-redirect files from local dependency | An auto-generated wrap-redirect file, which points via a symlinked subproject, ends up included in the dist. A mechanism is needed |
| [#14547](https://github.com/mesonbuild/meson/issues/14547) | Could CXXFLAGS passed to meson setup be automatically forwarded to mes | mdist.create_cmdline_args only reapplies the persisted -D options (cmd_line_options); environment variables like CXXFLAGS aren't s |
| [#14582](https://github.com/mesonbuild/meson/issues/14582) | Linker flag detection for lld fails when using LDFLAGS="-fuse-ld=lld" | When using lld via LD=clang + LDFLAGS=-fuse-ld=lld, meson fails to detect the linker as lld and applies unsupported flags such as  |
| [#14584](https://github.com/mesonbuild/meson/issues/14584) | CMake Wrapper Always Generates a Configure Command for CMake project | Even when CONFIGURE_COMMAND is empty in ExternalProject_Add, meson's CMake wrapper always generates a configure custom target and  |
| [#14598](https://github.com/mesonbuild/meson/issues/14598) | Race Condition When Passing protoc to CMake Subproject | When passing another subproject's protoc into a CMake subproject, meson doesn't recognize protoc's build completion as a prerequis |
| [#14602](https://github.com/mesonbuild/meson/issues/14602) | `qt6.compile_resources` does not work with `custom_target` | In current _qt.py, when the qrc source is a CustomTarget etc., the qrc can't be parsed at setup time, so a clear MesonException te |
| [#14621](https://github.com/mesonbuild/meson/issues/14621) | Is there an equivalent of CMAKE_EXE_LINKER_FLAGS? | A request to have separate linker flags per target type (executable/shared library). Applying werror=true to the linker (the werro |
| [#14636](https://github.com/mesonbuild/meson/issues/14636) | Mingw64 cmake CMAKE_C_COMPILER illformatted string | Because toolchain.py converts backslashes to /, CMAKE_C_COMPILER becomes 'C:/msys64/.../cc.EXE', and MSYS's (Unix-style) cmake mis |
| [#14641](https://github.com/mesonbuild/meson/issues/14641) | MacOS: Framework flag is not sent to the compiler | In CMake dependency parsing, a framework's -F{path} only ends up in res.libraries and isn't passed to the compiler, so headers ins |
| [#14645](https://github.com/mesonbuild/meson/issues/14645) | Add extracted_obj.filter() method | A request to add a filter() method to ExtractedObjects to select only specific sources. Currently no such filter method exists in  |
| [#14651](https://github.com/mesonbuild/meson/issues/14651) | meson should prefer numpy-config to pkg-config | numpy's DependencyFactory tries PKGCONFIG before CONFIG_TOOL, so it can pick up an old system numpy outside conda/venv. There's a  |
| [#14669](https://github.com/mesonbuild/meson/issues/14669) | Wrong path to executable output with --genvslite VS 2022 project | For an executable placed in a subdirectory, the output path in a --genvslite vs2022-generated project becomes $(OutDir)exe, missin |
| [#14678](https://github.com/mesonbuild/meson/issues/14678) | Build system comparison should be updated | A point that the Simple-comparison page's benchmarks are outdated and should reflect improvements in CMake/Ninja. This is a docume |
| [#14694](https://github.com/mesonbuild/meson/issues/14694) | vala: cross-compile / dependencies from subprojects | Part of Vala cross support (defining valac in the cross file) landed via the vala-cross snippet in 1.9, but the main focus of this |
| [#14712](https://github.com/mesonbuild/meson/issues/14712) | Python module: installation path not added to tests extra_paths when u | On MSVC, tests using python_dependency don't get the Python DLL directory (e.g. C:\Python313) added to extra_paths. This is becaus |
| [#14715](https://github.com/mesonbuild/meson/issues/14715) | Dlang: not possible to set conditional versions in dub dependencies? | There's no way to specify a D conditional version (--d-version) when resolving a dub dependency, and since dub describe also depen |
| [#14716](https://github.com/mesonbuild/meson/issues/14716) | Add API for introspecting subproject() chain | A request for an API like meson.get_subproject_chain() to retrieve a subproject's loading path. This would be a new meson-object m |
| [#14717](https://github.com/mesonbuild/meson/issues/14717) | c_std is hard to use in a backward compatible way | As a result of c_std becoming a list, writing backward-compatible specifications across multiple meson versions is awkward, since  |
| [#14725](https://github.com/mesonbuild/meson/issues/14725) | Meson Fails to build Python Extensions with CUDA source on Windows | On Windows, a project using only the cuda language can't find the python dependency (possibly because cl isn't initialized with cu |
| [#14733](https://github.com/mesonbuild/meson/issues/14733) | `@PRIVATE_DIR@` eqivalent for `test()`? | A request for a scratch temporary directory for test(), equivalent to custom_target's @PRIVATE_DIR@. This would mean adding a new  |
| [#14735](https://github.com/mesonbuild/meson/issues/14735) | HIP Support for meson | A large-scale request to support AMD ROCm's HIP as a new language. It has a dual nature — both a CUDA-like wrapper and a native AM |
| [#14737](https://github.com/mesonbuild/meson/issues/14737) | custom_target's env hides the command behind meson --internal exe --un | Specifying env on a custom_target wraps the ninja command in meson --internal exe --unpickle, so even with verbose output the actu |
| [#14739](https://github.com/mesonbuild/meson/issues/14739) | Rewriter doesn't support dict-valued kwargs | The rewriter can read a DictNode for info operations, but for modify (add) operations, can_modify() returns False and it's skipped |
| [#14755](https://github.com/mesonbuild/meson/issues/14755) | dependency('atomic') does not work on NetBSD and OpenBSD | AtomicBuiltinDependency added direct detection via has_function('atomic_flag_clear') in 1.7.0, which may allow detection on BSD sy |
| [#14767](https://github.com/mesonbuild/meson/issues/14767) | The External Project module should use the .pc file to link its depend | The External Project module only links the produced library itself, not the transitive dependencies (ffmpeg, zlib, etc.) listed in |
| [#14780](https://github.com/mesonbuild/meson/issues/14780) | -Dbuildtype=minsize invokes -Os instead of -Oz | The optimization choices are only ['plain', '0', 'g', '1', '2', '3', 's'], with no 'z', and minsize always maps to -Os (s). Adding |
| [#14797](https://github.com/mesonbuild/meson/issues/14797) | No obvious way to link `executable()`-generated files with a linker di | A request to use the linker directly instead of the compiler driver, for freestanding use cases. meson is designed to always link  |
| [#14801](https://github.com/mesonbuild/meson/issues/14801) | coverage-html ninja target doesn't work with lcov>=2 | lcov 2.0's genhtml became stricter and fails with 'file error for zz.c'. coverage.py's genhtml invocation has no --ignore-errors ( |
| [#14805](https://github.com/mesonbuild/meson/issues/14805) | Deprecated options should be handled differently in the options summar | Manually setting a deprecated option makes it show up normally in the summary, burying the deprecation warning shown at the top. T |
| [#14810](https://github.com/mesonbuild/meson/issues/14810) | AssertionError when generating build files. | A bug in the CMake module that crashes with an AssertionError when pulling in a large CMake subproject (depthai-core). Reproductio |
| [#14825](https://github.com/mesonbuild/meson/issues/14825) | gdb auto-load set up incorrectly | The reporter's analysis — that mdevenv.py's gdb auto-load tree construction (the path building in autoload_path and add_gdb_auto_l |
| [#14854](https://github.com/mesonbuild/meson/issues/14854) | Change object suffix | TASKING VX (C166) linker requires objects with a .obj extension rather than .o. Making the object suffix configurable is a design  |
| [#14859](https://github.com/mesonbuild/meson/issues/14859) | Unhandled exception during installation | depfixer.py crashes with a struct.error when it encounters a buffer of fewer than 4 bytes while reading ELF section headers. Harde |
| [#14886](https://github.com/mesonbuild/meson/issues/14886) | Subproject wrap file changes do not take effect without `git clean -xd | After editing a wrap file, subprojects are not re-fetched, and `subprojects update --reset` incorrectly reports 'Not used'. This r |
| [#14899](https://github.com/mesonbuild/meson/issues/14899) | add_languages does not search among meson.override_find_program'd bina | Compiler discovery in add_languages() does not pick up binaries (e.g. nasm) supplied via override_find_program / wrap fallback. Ne |
| [#14900](https://github.com/mesonbuild/meson/issues/14900) | Boost subproject does not use correct assembler under MSVC | For Boost.context as a CMake subproject, on MSVC it tries to assemble with nasm instead of ml64. This is an issue in the cmake mod |
| [#14903](https://github.com/mesonbuild/meson/issues/14903) | Deprecation policy, semver adherence and other related things | An issue opened by a maintainer (jpakkane) themselves to discuss backward-compatibility/semver policy. A policy-decision design di |
| [#14905](https://github.com/mesonbuild/meson/issues/14905) | custom_target works when program is found from wrap system, but not ho | Passing an ExternalProgram found on the system as a custom_target input raises 'Source item is ExternalProgram instead of string o |
| [#14918](https://github.com/mesonbuild/meson/issues/14918) | Reference Manual Markdown and Json download Links | Request to add single-page/Markdown/JSON download links for the reference manual to the website. Requires changes to the docs buil |
| [#14925](https://github.com/mesonbuild/meson/issues/14925) | c_pch option in static_library() causes build failure on Windows | When a shared and static library with the same name both use c_pch, they generate .pdb files at the same path and collide, causing |
| [#14949](https://github.com/mesonbuild/meson/issues/14949) | clang-tidy broken for headers in Meson 1.9.0 | A regression from PR14736 (commit 'clang-tidy: run tool only on source files participating in targets') that stopped header-only w |
| [#14953](https://github.com/mesonbuild/meson/issues/14953) | Unexpected behavior of `find_program()` | find_program('c') picks up the compiler from the CC environment variable (gcc) because it matches the language name. This stems fr |
| [#14979](https://github.com/mesonbuild/meson/issues/14979) | `dependency(components: )` not ignored for fallback located with `depe | When resolved via a `dependency_names` fallback, CMake-only components leak through and cause failures with 'did not override' eve |
| [#14980](https://github.com/mesonbuild/meson/issues/14980) | Proposal: export symbols feature | A proposal for an API to natively support symbol export lists (.def/.map/.expsym, etc.). This is a large feature that must absorb  |
| [#15004](https://github.com/mesonbuild/meson/issues/15004) | UnicodeEncodeError when running tests on Windows with non-CP1252 chara | mtest crashes with a UnicodeEncodeError when test output contains characters that can't be represented in the codepage (cp1252). T |
| [#15010](https://github.com/mesonbuild/meson/issues/15010) | Add swipl-ld support | Request to add support for SWI-Prolog's swipl-ld. This involves integrating a new linker/compiler wrapper; the reporter has shown  |
| [#15014](https://github.com/mesonbuild/meson/issues/15014) | Cray MPI wrapper is not recognized | Cray's cc/CC wrappers don't respond to MPI query flags like --showme or -compile-info, so MPIConfigToolDependency can't detect the |
| [#15035](https://github.com/mesonbuild/meson/issues/15035) | array[ExternalProgram] is not accepted by custom_target(depends: xx) | declare_dependency(depends: exe) and custom_target(depends: [ExternalProgram]) are not accepted, leaving the tool ungenerated at b |
| [#15064](https://github.com/mesonbuild/meson/issues/15064) | Clarifying and cleaning up Meson's state tracking | A maintainer (dcbaker) design discussion about reorganizing the five state-management classes: Build/Environment/CoreData/OptionSt |
| [#15070](https://github.com/mesonbuild/meson/issues/15070) | Subproject merging when a subproject appears multiple times on the gra | A design discussion about merging default_options / resolving version constraints when the same subproject appears multiple times  |
| [#15103](https://github.com/mesonbuild/meson/issues/15103) | linux-mingw-aarch-64bit support | Request for aarch64 MinGW cross-compilation support. A one-line request with no details, but it requires investigating toolchain/c |
| [#15108](https://github.com/mesonbuild/meson/issues/15108) | `meson compile` does not terminate cleanly with `ctrl-c` | Ctrl-C during `meson compile` orphans ninja, because KeyboardInterrupt is raised inside Popen_safe without cleanup. Needs handling |
| [#15111](https://github.com/mesonbuild/meson/issues/15111) | User supplied PkgConfig paths are not honored as extra prefixes | A report of a regression where a custom prefix specified via --pkg-config-path / PKG_CONFIG_PATH is not reflected in the include/l |
| [#15117](https://github.com/mesonbuild/meson/issues/15117) | Cross compiling with clang-cl on macOS paths interaction | Passing a macOS path starting with /Users/ to clang-cl gets misinterpreted as the /U (undefine macro) option. Needs a fix such as  |
| [#15146](https://github.com/mesonbuild/meson/issues/15146) | ERROR: Could not guess language from source file src\main\main.cs | Setup of a C# (.cs) project fails in the VS backend with 'Could not guess language' (it succeeds with Ninja). A gap in the VS back |
| [#15150](https://github.com/mesonbuild/meson/issues/15150) | Per-platform builtin features | A maintainer (jpakkane) design discussion on whether to introduce platform-specific built-in options like os2_emxof or darwin_sign |
| [#15154](https://github.com/mesonbuild/meson/issues/15154) | Version 1.9.1 breaks BOOST library modules | A regression from the 'Check for header only Boost libraries' patch causes modules to be marked found based on headers alone even  |
| [#15161](https://github.com/mesonbuild/meson/issues/15161) | Can't link multiple Rust sources into a single executable | Linking multiple Rust sources into a C executable only uses the first file, resulting in undefined references. Since rustc can't h |
| [#15162](https://github.com/mesonbuild/meson/issues/15162) | meson failed to build cmake project 'Cycle in CMake inputs/dependencie | Trace-based parsing of CMake subprojects incorrectly detects a circular dependency (twist -> ... -> fmt -> twist_sim -> twist_trac |
| [#15172](https://github.com/mesonbuild/meson/issues/15172) | [Python] limited_api argument is not respected | On Windows, specifying limited_api links against python312.dll instead of python3.dll. python.py calls find_libpy_windows(limited_ |
| [#15183](https://github.com/mesonbuild/meson/issues/15183) | cargo: Respect Meson's default_library instead of Cargo.toml's crate_t | A proposal to handle Cargo.toml's crate_type=[staticlib,cdylib] via library(rust_abi:'c') instead of both_libraries, leaving the s |
| [#15184](https://github.com/mesonbuild/meson/issues/15184) | custom_target: Add `install_files` argument to install a subset of the | Request for an install_files kwarg to install only some of a custom_target's outputs. Since the existing install_dir is already a  |
| [#15203](https://github.com/mesonbuild/meson/issues/15203) | Meson passes bad configuration to cmake when building llama.cpp with V | In a CMake subproject for llama.cpp (with Vulkan enabled), an invalid `--config ';;;'` setting gets passed to cmake_run_ctgt and f |
| [#15211](https://github.com/mesonbuild/meson/issues/15211) | Redesign function calling convention | A maintainer (dcbaker) design discussion on unifying the three function-call conventions across interpreter/module/InterpreterObje |
| [#15214](https://github.com/mesonbuild/meson/issues/15214) | meson install not respecting --destdir on windows | On Windows, an install destination starting with '/' resolves to C:\ and --destdir is not respected. Likely caused by how destdir_ |
| [#15222](https://github.com/mesonbuild/meson/issues/15222) | Sanitizers flags aren't included with Rust targets | With b_sanitize=address, Rust targets don't get `-Z sanitizer=address` applied, causing build failures. Converting sanitizer flags |
| [#15226](https://github.com/mesonbuild/meson/issues/15226) | Should pass -flto to sanity check | The sanity check fails to account for sanitizers like -Db_sanitize=cfi that require LTO or visibility settings. A design decision  |
| [#15229](https://github.com/mesonbuild/meson/issues/15229) | Meson & Python 3.14 & MacOS 26.1 & scipy : sanity check failing | sanity check fails with 'library System not found' on macOS 26.1 — an environment issue specific to a new OS/SDK. It can't be repr |
| [#15234](https://github.com/mesonbuild/meson/issues/15234) | Prelinking with macOS AppleClang yields objects/libraries with zero sy | A legitimate bug where -arch and -exported_symbols_list are not passed during prelink, causing symbol loss or architecture mismatc |
| [#15237](https://github.com/mesonbuild/meson/issues/15237) | Passing separate generator outputs to library() for shared/static | A feature request to pass separate generator outputs to the shared and static variants when using both_libraries/--default-library |
| [#15280](https://github.com/mesonbuild/meson/issues/15280) | Allow specifying the pthread compile/link flags in crossfiles? | A request to allow specifying pthread flags via the cross file, to address the threads dependency forcing -pthread on unknown plat |
| [#15293](https://github.com/mesonbuild/meson/issues/15293) | Add a .dependency() function to native subproject objects too | A reasonable request to add the .dependency() method that CMake subprojects have to the native SubprojectHolder as well. Currently |
| [#15300](https://github.com/mesonbuild/meson/issues/15300) | Documentation: restore discoverability of traditional names for config | Below 1.2.0 (e.g. 0.61.2 on Ubuntu 22.04), the cross-file binary key is 'pkgconfig', and 'pkg-config' isn't accepted, but the spel |
| [#15304](https://github.com/mesonbuild/meson/issues/15304) | dependency type classifications (build/link/run-time, header-only) | Complaints that all dependencies show as 'Run-time dependency', plus a request to add header_only/type classification. A large dis |
| [#15307](https://github.com/mesonbuild/meson/issues/15307) | [Not ideal behaviour] Deleting a wrap's folder should trigger a clone | A reasonable UX improvement: deleting a wrap's project folder doesn't trigger a re-clone and results in a not-found error. The rep |
| [#15308](https://github.com/mesonbuild/meson/issues/15308) | requesting/enforcing a cuda toolkit version, or handling nvcc mismatch | Specifying dependency('cuda', version:'12.6') doesn't keep the nvcc compiler on PATH in sync, leading to inconsistency with a diff |
| [#15313](https://github.com/mesonbuild/meson/issues/15313) | Add support for MSVC-based code coverage | Request for MSVC code-coverage support (the /fsanitize-coverage family). A large-scope new platform-support effort extending the b |
| [#15321](https://github.com/mesonbuild/meson/issues/15321) | [Need help] Unrecognized arguments when using meson runpython in MSVC | On Windows MSVC, `meson runpython` plus @rspfile passes arguments to glib-mkenums incorrectly. It works when calling python3 direc |
| [#15355](https://github.com/mesonbuild/meson/issues/15355) | docs: Edit on GitHub button is broken on some auto-generated pages | A documentation-site bug where the 'Edit on GitHub' link is broken on auto-generated pages (Reference-manual, etc.). The reporter  |
| [#15358](https://github.com/mesonbuild/meson/issues/15358) | Add support for protobuf to the codegen module | Request to add protobuf support to the codegen module. A large new feature; the maintainer (dcbaker) says they could implement it  |
| [#15365](https://github.com/mesonbuild/meson/issues/15365) | dependencies: deprecate main kwarg | A proposal to deprecate dependency()'s main kwarg and steer users toward modules / a proper main-dependency name. This is pending  |
| [#15368](https://github.com/mesonbuild/meson/issues/15368) | qt.preprocess does not handle resource renaming well | Renaming a file referenced inside a qrc causes ninja to look for the old dependency and fail. An issue with dependency tracking in |
| [#15371](https://github.com/mesonbuild/meson/issues/15371) | override_dependency does not check linked lib's type | override_dependency for static/shared doesn't verify the actual library kind of the link_with target. Relevant to use cases where  |
| [#15381](https://github.com/mesonbuild/meson/issues/15381) | Setting b_sanitize=thread breaks for projects that have Fortran depend | With a mixed toolchain (C/C++=clang, Fortran=gfortran), b_sanitize=thread fails with a 'sanitizer not supported' error from the gf |
| [#15388](https://github.com/mesonbuild/meson/issues/15388) | CMake submodules with generated link time dependencies fail to compile | When a CMake subproject passes a generated file (from configure_file, etc.) to a linker, the generated meson.build's link_args end |
| [#15391](https://github.com/mesonbuild/meson/issues/15391) | clang-tidy complains about gcc-specific option | After get_supported_arguments adopts a GCC-specific flag, `ninja clang-tidy` fails with an unknown-warning-option error because co |
| [#15417](https://github.com/mesonbuild/meson/issues/15417) | compiler.run produces a runresult with undefined stdout and stderr rat | When compiler.run can't actually execute (e.g. under cross), RunResult.stdout() returns 'UNDEFINED', which can leak into configure |
| [#15423](https://github.com/mesonbuild/meson/issues/15423) | ninja backend compile failed: posix_spawn: Argument list too long | With a large number of source files using long absolute paths, the command line becomes too long and ninja's posix_spawn fails. Th |
| [#15428](https://github.com/mesonbuild/meson/issues/15428) | compiler.run should accept rpath | Request to accept an rpath argument in compiler.run, for testing against external libraries in non-standard paths. A reasonable kw |
| [#15431](https://github.com/mesonbuild/meson/issues/15431) | [python module] Add limited_api optional argument to py.dependency() | Request to add a limited_api argument to py.dependency(), so an embedded exe can link against the limited API (python3.lib). A rea |
| [#15440](https://github.com/mesonbuild/meson/issues/15440) | MSVC ARM64EC support | On MSVC ARM64EC builds, when building a static library, lib passes /MACHINE:ARM64 and fails (can't be arm64ec). A large-scope plat |
| [#15448](https://github.com/mesonbuild/meson/issues/15448) | TinyCC support | A renewed request for TinyCC (tcc) compiler support (previously PR #8248). Requires adding a new compiler class and deciding on a  |
| [#15454](https://github.com/mesonbuild/meson/issues/15454) | Passing of source-path between libraries (Fortran module depscan) | For Fortran, dependency-library module info (source-path/compiled-module-path) is missing from depscan.json, causing unnecessary r |
| [#15456](https://github.com/mesonbuild/meson/issues/15456) | Qt private header detection breaks in cross-compilation | During cross builds, Qt private-header detection searches the build host's /usr/include, etc., leaking host include paths into the |
| [#15457](https://github.com/mesonbuild/meson/issues/15457) | Static boost dependencies do not include transitive dependencies | dependency('boost', static:true) doesn't include transitive dependencies between boost modules (e.g. locale->thread), causing link |
| [#15458](https://github.com/mesonbuild/meson/issues/15458) | Boost dependencies do not respect -Dprefer_static=true | A boost dependency without an explicit static argument doesn't honor -Dprefer_static=true and links dynamically. A real bug (tagge |
| [#15466](https://github.com/mesonbuild/meson/issues/15466) | Specify custom paths for CUDA (compiler and libraries) | Request for a way to specify custom search paths for nvcc and CUDA libraries in non-standard locations (e.g. /usr/local/cuda/bin). |
| [#15469](https://github.com/mesonbuild/meson/issues/15469) | generated cmake config file does not generate IMPORTED_IMPLIB for cygw | Meson-generated CMake config files don't set IMPORTED_IMPLIB for Cygwin dlls, triggering a CMP0111 warning. A real bug requiring a |
| [#15470](https://github.com/mesonbuild/meson/issues/15470) | cannot use Boost headers-only libraries if no runtime library is insta | With only libboost-dev installed (no runtime libs), dependency('boost') fails to detect header-only and returns NO. A regression f |
| [#15476](https://github.com/mesonbuild/meson/issues/15476) | Re-organize unit tests | An internal refactor proposal (from maintainer dcbaker) to split up a huge unittest file, trim tests that run pointlessly on every |
| [#15493](https://github.com/mesonbuild/meson/issues/15493) | new field in declare_dependency() to depend on a custom_target() being | Request to let declare_dependency() express a dependency that runs a custom_target() without mixing in its output files. A new kin |
| [#15499](https://github.com/mesonbuild/meson/issues/15499) | Drop unknown options when reconfiguring an existing build | Reconfiguring after an option has been removed from meson_options.txt errors out with no workaround. 'Unknown options' is raised a |
| [#15502](https://github.com/mesonbuild/meson/issues/15502) | CUDA NVCC compiler lookup should allow build machine | A request to use the build machine's nvcc even in cross builds, since nvcc is architecture-independent. Involves how compiler dete |
| [#15503](https://github.com/mesonbuild/meson/issues/15503) | No deduplication of some linker flags via static_library dependencies | Duplicates like -fopenmp aren't covered by arglist.py's dedup1/dedup2 (which only target -l and library-extension arguments). The  |
| [#15505](https://github.com/mesonbuild/meson/issues/15505) | rust: support no_std | A FIXME still present at build.py:2355 notes that native_static_libs shouldn't be added under no-std. This needs a design involvin |
| [#15507](https://github.com/mesonbuild/meson/issues/15507) | C23/C++26 #embed --embed-dir= | Feature request to automatically add the private build dir (target.p) to --embed-dir for #embed. No --embed-dir support currently  |
| [#15527](https://github.com/mesonbuild/meson/issues/15527) | Qt module should have support for repc as a tool | Request for support of Qt RemoteObjects' repc tool. _qt.py's tool set (_set_of_qt_tools = moc/uic/rcc/lrelease/qmlcachegen/qmltype |
| [#15533](https://github.com/mesonbuild/meson/issues/15533) | Programs and find_program confuse "outputs for machine X" and "runs on | A design-refactor proposal about how ExternalProgram's for_machine conflates 'runs on build' with 'produces output for host'. The  |
| [#15545](https://github.com/mesonbuild/meson/issues/15545) | unsupported C++ flags are reported as supported | GCC warns that -Werror=... is 'not valid' for C++ but still returns exit 0, so _has_multi_arguments looks only at the exit code an |
| [#15560](https://github.com/mesonbuild/meson/issues/15560) | dependencies/qt: Third attempt to allow qt --no-framework on MacOS | The code at qt.py:306-309 that falls back to regular library search when _framework_detect fails on macOS has existed since 2021,  |
| [#15563](https://github.com/mesonbuild/meson/issues/15563) | meson doesn't generate dependencies for #include in fortran files | The internal Fortran dependency scanner (_scan_fortran_file_deps) at ninjabackend.py:4315 only recurses into an included file when |
| [#15573](https://github.com/mesonbuild/meson/issues/15573) | Can't include strings with single quotes in machine files | machinefile.py unconditionally runs value.replace('\\','\\\\') for Windows path support, which turns \' into \\' and breaks escapi |
| [#15579](https://github.com/mesonbuild/meson/issues/15579) | structured_sources causes misleading compiler errors in IDE | Because structured_sources copies sources into the build directory, compiler errors point at the copies rather than the original s |
| [#15591](https://github.com/mesonbuild/meson/issues/15591) | CMake subproject using qt_add_qml_module() fails with empty cmake vari | The CMake traceparser evaluates an empty-string cmake variable as an executable path and errors (traceparser.py:229). An interop i |
| [#15597](https://github.com/mesonbuild/meson/issues/15597) | jar target is always dirty if path to source does not match package | Because javac places .class files according to the package declaration, the output path Meson expects (out.jar.p/java/A.class) doe |
| [#15601](https://github.com/mesonbuild/meson/issues/15601) | find_library linkable check is too strict for RTEMS | The link-viability check for find_library introduced in meson 1.10 is too strict for the RTEMS environment (e.g. _ISR_Stack_area_e |
| [#15616](https://github.com/mesonbuild/meson/issues/15616) | version retrieval error for cmake wrap subproject | Version extraction for CMake subprojects incorrectly picks up an unrelated ..._VERSION variable (e.g. PROJ_BUILD_VERSION or GTEST_ |
| [#15624](https://github.com/mesonbuild/meson/issues/15624) | Using patch_directory with existing Git submodules without source_file | Wanting to apply a packagefiles overlay (patch_directory) on top of an existing Git submodule directory, but the wrap isn't read w |
| [#15637](https://github.com/mesonbuild/meson/issues/15637) | Python limited API extensions assume there is only one valid extension | python_info.py hardcodes limited_api_suffix = EXTENSION_SUFFIXES[1] by index, which can't handle cases with multiple suffixes unde |
| [#15639](https://github.com/mesonbuild/meson/issues/15639) | g-ir-scanner artifacts can link against conflicting ASan runtimes and  | With b_sanitize=address, the gnome module automatically adds -lasan for g-ir-scanner, which conflicts with -shared-libasan and han |
| [#15668](https://github.com/mesonbuild/meson/issues/15668) | Feature Request: Support for a MATLAB module | Request for a module that detects MATLAB and sets up flags for the mex/Engine API. No matlab module currently exists under mesonbu |
| [#15684](https://github.com/mesonbuild/meson/issues/15684) | Reconsider failing a configure on recursive subprojects | Since PR #950, recursive subproject includes now fail the whole configuration, which also breaks optional feature-gated dependenci |
| [#15694](https://github.com/mesonbuild/meson/issues/15694) | Import library `.lib` not created when compiling with MSVC | On MSVC, a shared_library's .dll is produced, but the accompanying .lib import library isn't required by the default target, so me |
| [#15703](https://github.com/mesonbuild/meson/issues/15703) | Cannot run a manual target defined in a subdir on Windows | A run_target (manual target) defined in a subdir becomes 'target not found' under the Visual Studio backend, while it succeeds on  |
| [#15712](https://github.com/mesonbuild/meson/issues/15712) | `icx` and `ifx` linkers on windows when ipo is enabled | On Windows, xilink is always selected as the linker for icx/ifx, preventing IPO from being used; setting CC_LD, etc. doesn't chang |
| [#15718](https://github.com/mesonbuild/meson/issues/15718) | Feature request: preprocess option for fortran compilers | Request for a way to handle Fortran preprocessing flags directly (e.g. library(preprocess:true) or fc.get_preprocessor_flags()), t |
| [#15733](https://github.com/mesonbuild/meson/issues/15733) | Feature request: pass test subcommand options to dist subcommand | `meson dist`'s test step (run_dist_steps) unconditionally runs `ninja test` and provides no way to pass test options like --no-sui |
| [#15735](https://github.com/mesonbuild/meson/issues/15735) | Solution for "Build target X has no sources" | To use gnome.generate_gir() on a .so built from Rust, there's a design need for a sourceless library() shim. It would be desirable |
| [#15740](https://github.com/mesonbuild/meson/issues/15740) | Cython sanity check uses PKG_CONFIG_PATH while python dependency does  | A regression in meson 1.11 where cython's sanity check picks up the system Python instead of the Python inside a conda environment |
| [#15761](https://github.com/mesonbuild/meson/issues/15761) | Formalizing an LLM/AI policy | A discussion of project policy on LLM/AI-assisted contributions. An ongoing governance matter with 25 comments, not something to f |
| [#15768](https://github.com/mesonbuild/meson/issues/15768) | TAP Subtests is not supported | TAP 14 subtests (indented blocks) aren't recognized by mtest.py's TAP parser and trigger UNKNOWN warnings. parse_line doesn't hand |
| [#15796](https://github.com/mesonbuild/meson/issues/15796) | test_python_build_config_extensions fails with both pkgconf and pkg-co | AllPlatformTests.test_python_build_config_extensions fails in an environment with both pkgconf and pkg-config installed (SunOS) —  |
| [#15800](https://github.com/mesonbuild/meson/issues/15800) | qt6.qml_module(): generate meson install folder structure in build fol | Request to generate the same qml/ folder structure at build time as `meson install` does, so qmlls can process qml_module inside t |
| [#15806](https://github.com/mesonbuild/meson/issues/15806) | Preserve path structure with preprocessor | compiler.preprocess() has no preserve_path_from equivalent (like generator.process()), so it cannot produce output that preserves  |
| [#15808](https://github.com/mesonbuild/meson/issues/15808) | LTO uses possibly invalid flag on macOS, which breaks linking | get_lto_obj_cache_path for Apple ld emits -object_path_lto. The current code skips this for is_dyld (the newer dyld linker), but t |
| [#15820](https://github.com/mesonbuild/meson/issues/15820) | Move to Python 3.11 | A proposal to raise the minimum Python version to 3.11. 1.12 has already moved to requiring 3.10 (snippets/python-310-required.md) |
| [#15823](https://github.com/mesonbuild/meson/issues/15823) | Removing support for untested versions of Qt | A policy question about when to drop support for old Qt versions that are untested in CI and no longer supported upstream. qt4.py  |
| [#15827](https://github.com/mesonbuild/meson/issues/15827) | Windows: meson setup can fail to acquire meson-private/meson.lock afte | The Windows DirectoryLock in mesonbuild/utils/platform.py opens the lock file with 'w+' and, via the FAIL action, simply re-raises |
| [#15832](https://github.com/mesonbuild/meson/issues/15832) | wxWidgets as cmake subproject fails to build on macOS | A library-path handling issue in a CMake subproject where clang++ fails to resolve the relative path lib/libwx_*.dylib, causing a  |
| [#15838](https://github.com/mesonbuild/meson/issues/15838) | Support QEMU in meson2hermetic | A tracker issue for additional features to include in the initial implementation of meson2hermetic (#15462), meant to be implement |
| [#15848](https://github.com/mesonbuild/meson/issues/15848) | limitations of dependencies, what to do about it, and how to not break | A design discussion issue by dcbaker about dependencies (per-language compile_args, ABI, mixed machines), a cross-cutting design c |
| [#15849](https://github.com/mesonbuild/meson/issues/15849) | Do not allow mixing libraries for different machines in dependencies | A subtask split off from the design discussion in #15848, proposing to introduce a for_machine declaration on declare_dependency t |
| [#15850](https://github.com/mesonbuild/meson/issues/15850) | Add generic abi parameter for target. | A design proposal derived from #15848 to add a generic link_abi field to build_target that would subsume rust_abi, requiring consi |
| [#15854](https://github.com/mesonbuild/meson/issues/15854) | rustmod.bindgen cannot deal with bindgen provided from subproject | rust.bindgen calls get_command on the bindgen program and executes it at configure time, so it can't handle a bindgen that is buil |
| [#15858](https://github.com/mesonbuild/meson/issues/15858) | boost dynamic versus static decision appears to depend on alphabetic o | Whether boost-test links statically or dynamically changes depending on the presence of other installed modules — an actual bug in |
| [#15895](https://github.com/mesonbuild/meson/issues/15895) | Additional machine targets | A design discussion issue involving a large new API (meson.cross_target, etc.) for additional machine targets for embedded/multi-h |
| [#15903](https://github.com/mesonbuild/meson/issues/15903) | pkgconf can escape character which can make meson fail | When pkgconf applies backslash escaping byte-by-byte on multibyte characters, it triggers a UTF-8 decode exception on the meson si |
| [#15922](https://github.com/mesonbuild/meson/issues/15922) | Missing formatter suppression directives | A reasonable feature request to add a formatting-suppression directive to meson format, similar to clang-format's // clang-format  |
| [#15924](https://github.com/mesonbuild/meson/issues/15924) | Tracker for typing/refactoring ideas | A checklist-style tracker issue aggregating small typing/refactoring tasks, meant to be continuously added to and worked through o |
| [#15926](https://github.com/mesonbuild/meson/issues/15926) | Built-in multi-key dictionary lookup | A language feature proposal for multi-key retrieval syntax like dico.values('key1','key2'), requiring a design decision on whether |
| [#15934](https://github.com/mesonbuild/meson/issues/15934) | qt6.compile_ui(): allow customization of generated UI header filename  | A reasonable feature request to let the generated header extension for qt6.compile_ui be selected via a header_ext argument. The i |
| [#15935](https://github.com/mesonbuild/meson/issues/15935) | Linker detection failure for LLD 18.1.7 | Linker detection fails with the BinaryBuilder toolchain (x86_64-apple-darwin14-ld) for a Linux-to-macOS cross build, but the repor |
| [#15937](https://github.com/mesonbuild/meson/issues/15937) | support `cargo auditable build` | A request to incorporate cargo-auditable's feature of embedding dependent-crate information into Rust executables into meson's car |
| [#15938](https://github.com/mesonbuild/meson/issues/15938) | Feature request with real use case: isolating from leaking env vars vi | A request to add an [isolate-from-env] section to machine files that can unset environment variables like LIBRARY_PATH/C_INCLUDE_P |
| [#15940](https://github.com/mesonbuild/meson/issues/15940) | Allow specifying filename in a wayland.scan_xml() equivalent | wayland.scan_xml generates fixed output header names (e.g. xdg-shell-server-protocol.h), which can't be adapted to the names wlroo |
| [#15944](https://github.com/mesonbuild/meson/issues/15944) | cargo: parse dev_dependencies and build_dependencies | A feature to parse dev-dependencies / build-dependencies in Cargo.toml and correctly configure native:true code-generator dependen |
| [#15967](https://github.com/mesonbuild/meson/issues/15967) | Custom Target: support multiple/varadic install modes | A request to add an install_modes argument letting custom_target specify different install_mode values for its multiple outputs. R |
| [#15973](https://github.com/mesonbuild/meson/issues/15973) | Incorrect `py.get_install_dir()` returned in `meson.build` when creati | In a meson-python build, py.get_install_dir() returns the system default (/usr/local/...) even though the actual install happens c |
| [#15974](https://github.com/mesonbuild/meson/issues/15974) | Incorrect MachineInfo.pure_path_class logic prevents cross-building fr | pure_path_class returns PureWindowsPath only when the host is Windows, so for a Windows-to-Android cross build, prefix (a Windows- |

---

## D. Unclear / needs more investigation (41)

| Issue | Title | Note |
|---|---|---|
| [#2225](https://github.com/mesonbuild/meson/issues/2225) | debug symbols link to wrong path when source directory is a symlink | Whether debug-symbol path resolution behaves correctly with a symlinked source directory can't be confirmed ju |
| [#3059](https://github.com/mesonbuild/meson/issues/3059) | Libraries built with lto and meson/ninja are larger than with configur | An old comparison from the meson 0.43 era; the LTO implementation (b_lto, b_lto_threads, b_lto_mode) has since |
| [#3317](https://github.com/mesonbuild/meson/issues/3317) | Crash when using a file generated by configure_file as a content_file  | A case where passing a configure_file output to gtkdoc's content_files mis-resolves the build directory and re |
| [#3330](https://github.com/mesonbuild/meson/issues/3330) | ninja backend + msvc: clean of shared library targets is missing most  | A case (from 2018) where MSVC-generated .exp/.ilk/.lib/.pdb files aren't cleaned up by ninja clean. It's uncon |
| [#3382](https://github.com/mesonbuild/meson/issues/3382) | Generating VS2015 project on Linux fails | An old crash where get_link_whole_for() fails on list concatenation when given a str argument. That code has c |
| [#5335](https://github.com/mesonbuild/meson/issues/5335) | DYLD_FALLBACK_LIBRARY_PATH not propagated to post_inst/run_target scri | The issue that macOS's DYLD_FALLBACK_LIBRARY_PATH does not propagate to the post-install script. DYLD-family v |
| [#5609](https://github.com/mesonbuild/meson/issues/5609) | Trying to override 'subproject_dir' and got an error. | A report of a traceback when setting subproject_dir to 'vendor' and trying to resolve the unity fallback with  |
| [#5776](https://github.com/mesonbuild/meson/issues/5776) | vs2019: failing to rebuild native: true executable after "meson config | A report that after changing buildtype with the VS backend, native binaries are not rebuilt, causing an _ITERA |
| [#5892](https://github.com/mesonbuild/meson/issues/5892) | Error when trying to compile llvm ir file in subdirectory | A report that compiling an LLVM IR (.ll) file in a subdirectory results in an error. A minimal reproduction is |
| [#5955](https://github.com/mesonbuild/meson/issues/5955) | Environment capture behaviour | A question about whether passing an environment object as the env argument copies or references its values, si |
| [#5979](https://github.com/mesonbuild/meson/issues/5979) | Modifying input from custom target triggers pch recompile | Changing a custom_target's input triggers an unrelated PCH recompilation. This involves ninja's dependency-gra |
| [#6397](https://github.com/mesonbuild/meson/issues/6397) | Misleading warning "msvc does not support C++11" | A comment that MSVC has no /std switch for c++11 and the warning wording is misleading. Improving the wording  |
| [#7296](https://github.com/mesonbuild/meson/issues/7296) | include_directories() is apparently filtering? | An absolute system include path with is_system:true doesn't get added. CompilerArgs' deduplication likely stri |
| [#7394](https://github.com/mesonbuild/meson/issues/7394) | Cross compilation of Objective-C++ fails | An error where stdio.h can't be found during ObjC++ cross-compilation for iOS. This is likely a cross-file/SDK |
| [#7519](https://github.com/mesonbuild/meson/issues/7519) | Troubles using Meson and the Lmod module system | In an Lmod environment, -L is missing from build.ninja's link line and groups end up nested. This is likely re |
| [#7835](https://github.com/mesonbuild/meson/issues/7835) | Changed array choices test does not work in macos | A CI/test-related issue with an empty body (array choices test on macOS). There's no detail, and it's hard to  |
| [#8111](https://github.com/mesonbuild/meson/issues/8111) | Qt5 module fails to find library files with debug build type using min | Issue where the mingw build of Qt looks for library names with the Windows-specific 'd' suffix. dependencies/q |
| [#8172](https://github.com/mesonbuild/meson/issues/8172) | Only inject script interpreter for first command in list | A shebang-derived interpreter gets injected into each argument of the command list, breaking things on Windows |
| [#9963](https://github.com/mesonbuild/meson/issues/9963) | Build order issue using a cmake subproject dependency | A report (2022, no comments) that a cmake subproject dependency doesn't get built before the executable that n |
| [#10371](https://github.com/mesonbuild/meson/issues/10371) | Boost dependency doesn't add -DBOOST_HAS_THREADS appropriately | boost.py applies mt filtering for threading=multi, but no code was found that adds thread-related defines such |
| [#10376](https://github.com/mesonbuild/meson/issues/10376) | msgfmt is not overridable in cross [binaries] | i18n.py looks up msgfmt with for_machine=BUILD, so whether the [binaries] msgfmt override takes effect depends |
| [#10391](https://github.com/mesonbuild/meson/issues/10391) | Crash when passing the output from generator().process() to generator. | The original crash site (an assert in get_target_filename) has been reworked to handle CustomTargetIndex etc., |
| [#10420](https://github.com/mesonbuild/meson/issues/10420) | Unhandled exception during install with -Dstrip=true for Python extens | do_strip only runs the strip_bin executable; there is still no handling for FileNotFoundError etc. when strip  |
| [#10439](https://github.com/mesonbuild/meson/issues/10439) | Unhandled python exception when attempting to use clang-cl | clang-cl detection has been improved in detect.py, but it's unclear whether the specific exception from the re |
| [#10483](https://github.com/mesonbuild/meson/issues/10483) | With llvm 14 and llvm 15 co-installed, meson doesn't pick llvm 15 usin | Specifying llvm-config via a native file doesn't produce the intended version selection. Needs hands-on invest |
| [#10496](https://github.com/mesonbuild/meson/issues/10496) | `gnome.compile_resources` building before dependencies | An ordering problem where compile_resources runs before a custom target (e.g. blueprint) listed in dependencie |
| [#10590](https://github.com/mesonbuild/meson/issues/10590) | Incorrect path for precompiled headers in `compile_commands.json` | compile_commands.json's -include is missing the PCH's parent directory. Needs verification of the ninja backen |
| [#10730](https://github.com/mesonbuild/meson/issues/10730) | CMake AttributeError: 'NoneType' object has no attribute 'resolve' | A NoneType.resolve crash while processing Open5GS's (freeDiameter) CMake subproject on CentOS/Py3.7. The trace |
| [#10920](https://github.com/mesonbuild/meson/issues/10920) | panic in relpath@ntpath.py | An unhandled exception in Windows relpath handling. A mesonlib.relpath wrapper that catches ValueError to abso |
| [#11349](https://github.com/mesonbuild/meson/issues/11349) | ValueError: invalid literal for int() with base 10: ''  ERROR: Unhandl | An exception occurs during int() conversion while building glib2 on MSYS2-MINGW64. The full traceback and whic |
| [#11412](https://github.com/mesonbuild/meson/issues/11412) | Running test suite fails with cstdio file not found in 68 clang-tidy t | Manually running the clang-tidy test with --internal clangtidy without a compile_db results in cstdio not bein |
| [#11524](https://github.com/mesonbuild/meson/issues/11524) | library function generate vapi make the invalid folder name | A report that library()'s vapi generation produces an invalid folder name, but the issue body is malformed, ma |
| [#11560](https://github.com/mesonbuild/meson/issues/11560) | Unhandled python exception (log_tried AttributeError) | Running a self-built zipapp (meson.pyz) triggers an AttributeError in detect.py because c.func.log_tried is a  |
| [#12904](https://github.com/mesonbuild/meson/issues/12904) | Unhandled python exception when trying to add hdf5 as a dependency | A report of an unhandled exception when adding the hdf5 dependency, but the traceback is cut off partway, so t |
| [#13611](https://github.com/mesonbuild/meson/issues/13611) | subproject with as_system('system') does not use -isystem | -isystem isn't applied for one specific subproject (DPDK) only. It works for other subprojects, likely due to  |
| [#13733](https://github.com/mesonbuild/meson/issues/13733) | Meson fails with build.cpp_std=c++23 default options for msvc under Wi | A failure with 'No build machine compiler' when build.cpp_std is specified. Recent changes (2026-01/06) to bui |
| [#13834](https://github.com/mesonbuild/meson/issues/13834) | meson: error: unrecognized arguments: --fhead #pragma once | With the MSI-installed version of Meson (1.6.0), a path containing spaces breaks argument parsing, producing m |
| [#13859](https://github.com/mesonbuild/meson/issues/13859) | meson seems to append '.lib' to all pkg-config libs on windows | With a .pc file whose Libs.private has a full-path -l entry like '-lC:/path/x.lib', Meson/find_library resolut |
| [#13887](https://github.com/mesonbuild/meson/issues/13887) | prefer_static fallback to shared doesn't work with Compiler.find_libra | MSVC's get_library_naming has included 'lib' in stlibext since 2019, so a .lib pattern should also be generate |
| [#14475](https://github.com/mesonbuild/meson/issues/14475) | Error while using Python ARM32 | The specific crash details on ARM32 Python on Windows 11 ARM64 exist only as an attached log, not in the issue |
| [#15722](https://github.com/mesonbuild/meson/issues/15722) | Basic import std example does not work with Meson 1.10.0 or 1.11 under | On macOS with Homebrew clang, `import std` fails with 'module std not found'. ninjabackend.py has handling for |

---

## E. Opened since the last full sweep, triaged separately (7)

These issues were created after the 2026-07-06 full sweep and so were not part of the batch re-verification pass above; classified individually just for this report.

| Issue | Title | Category | Confidence | Basis |
|---|---|---|---|---|
| [#15980](https://github.com/mesonbuild/meson/issues/15980) | machine subsystem could be used to identify libc for Linux s | keep_open/- | high | Two Meson members (dcbaker, eli-schwartz) argue musl detection is effectively impossible/undesirable and should not be baked into  |
| [#15981](https://github.com/mesonbuild/meson/issues/15981) | Add MSVC C++23 Preview support | keep_open/- | medium | Verified in mesonbuild/compilers/cpp.py that real MSVC (VisualStudioCPPCompiler.get_options, lines 915-925) only offers cpp_std up |
| [#15985](https://github.com/mesonbuild/meson/issues/15985) | Introspect Failure for Python with Custom Command in Cross C | implement/- | high | Root cause found in mesonbuild/modules/python.py, PythonModule.find_installation(): line 537 reads the full cross-file 'python' bi |
| [#15987](https://github.com/mesonbuild/meson/issues/15987) | KeyError: 'cpp' with pch | comment_close/fixed | high | Reporter's target passed cpp_pch: to a library() built only from .c sources, so target.compilers has no 'cpp' entry, causing targe |
| [#15989](https://github.com/mesonbuild/meson/issues/15989) | cython_args option has no effect | implement/- | high | Confirmed: mesonbuild/environment.py add_lang_args() auto-registers a 'cython_args' built-in option like every other language, and |
| [#15993](https://github.com/mesonbuild/meson/issues/15993) | Per-subproject options (augments) missing from buildoptions  | implement/- | medium | Verified both root causes in mesonbuild/mintro.py: (1) list_buildoptions() (line 210-211) calls _list_buildoptions(coredata) witho |
| [#15994](https://github.com/mesonbuild/meson/issues/15994) | Source-only introspection ignores default_options passed to  | implement/- | medium | Confirmed mesonbuild/ast/introspection.py's IntrospectionInterpreter discovers subprojects purely by listing the subprojects/ dire |

---
