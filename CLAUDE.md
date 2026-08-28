# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A LaTeX lecture-notes project (`book` class) for **21-651, General Topology**, taught
by James Cummings at Carnegie Mellon in **Fall 2025**, scribed by Sidharth Hariharan
and Teresa Pollard. Derived from [Lecture-Notes-Template-2026][tpl]. There is no code,
no tests, and no linter — the deliverable is `main.pdf`.

**Two people scribe these notes**, which is true only of this repository and
ModelTheoryNotes among the siblings. Be careful about reformatting anything you did
not otherwise need to touch.

At ~3,900 lines across five chapters this is the largest of the sibling repositories,
and its structure is settled. The course is over.

## Building

`latexmk`, `pdflatex`, `biber`, and `make4ht` are all available locally.

```bash
# Full build with bibliography, output into TeX_Outputs/ (matches .vscode config)
latexmk -pdf -outdir=TeX_Outputs main.tex
```

Compile **at least twice**: `cleveref` and the ToC depend on the `.aux` files, and
citations need a `biber` pass in between. `latexmk` works that out for itself, which
is why CI uses it.

`TeX_Outputs/main.pdf` is **committed** (a general `*.pdf` ignore is deliberately
commented out in `.gitignore`); CI republishes it as `public/LastLocallyCompiled.pdf`.
Keep it refreshed when making substantive content changes.

## Structure

`main.tex` defines course metadata as macros (`\COURSENUMBER`, `\COURSENAME`,
`\LECTURER`, `\SCRIBE`, `\UNIVERSITY`, `\TERM`) consumed by the title block, then
`\input`s the four preamble files in a fixed order — `packages.tex`, `format.tex`,
`environments.tex`, `shortcuts.tex` — which are not interchangeable.

```
Chapters/1_Intro/                       A Recap of Undergraduate Topology
  1_1_Metric_Spaces.tex                   Metric Spaces
  1_2_Topological_Spaces.tex              Introduction to Topological Spaces
  1_3_Topologies.tex                      A Closer Look at Topologies
  1_4_Connectedness.tex                   Connectedness
  1_5_Compactness_and_Completeness.tex    Compactness and Completeness
Chapters/2_Nets/                        Nets and Filters
  2_1_Combinatorics.tex                   Some ``Completely Trivial Combinatorics''
  2_2_Gen.tex                             Generalising Properties of Metric Spaces
  2_3_Filters.tex                         Filters and Ultrafilters
  2_4_Filters_and_Nets.tex                Relating Filters to Nets
Chapters/3_Separation_and_Countability/ More Topological Properties
  3_1_Sep_Revisited.tex                   (More) Separation Properties
  3_2_Countability.tex                    Countability Properties
Chapters/4_Func_Anal/                   Topologies on Sets of Functions
  4_1_First_Examples.tex                  Motivation and First Examples
  4_2_Compactness.tex                     A Study in Compactness
  4_3_Arzela_Ascoli.tex                   Families of Functions
Chapters/5_Algebraic_Topology/          An Introduction to Algebraic Topology
  5_1_Cat_Thy.tex                         A Word on Category Theory
  5_2_Paths.tex                           Homotopy
  5_3_Fund_Group.tex                      The Fundamental Group
  5_4_Covering_Spaces.tex                 Covering Spaces
Chapters/Appendices/                    rendered -- see below
  A_Cat_Thy.tex                           A Categorical Perspective
  B_Gen_Tips.tex                          Professor Cummings's Top(ological) Tips
```

**No template scaffolding remains.** Unlike its siblings, this repository's
`\input{Chapters/Appendices/Appendices.tex}` is **live** in `main.tex`, so the
appendices do reach the PDF. Two of the four siblings comment theirs out; this one is
the exception and that is deliberate, so do not "fix" it.

`TeX_Setup/packages.tex` loads `appendix`, which no sibling does — accounted for in
the template's shared manifest.

## Authoring conventions

Every theorem-like environment has a plain form and a boxed `box*` form; **prefer the
boxed form in the notes** — that is what the existing content uses.

- Orange box: `boxtheorem`, `boxproposition`, `boxlemma`, `boxcorollary`
- Cyan box: `boxdefinition`
- Magenta box: `boxconvention`, `boxnotation`, `boxlnotation` (local notation), `boxabbrev`
- Green/red box: `boxexample`, `boxnexample` (non-example), `boxcexample` (counterexample)
- Gray/red box: `boxexercise`, `boxproblem`, `boxwarning`

Numbering: `theorem` and everything sharing its counter number per *section*;
`remark`, `solution`, `convention`, `notation`, `warning`, `abbreviation` are unnumbered.
Cross-reference with `cleveref` — **always `\Cref`, never `\cref`** — and label as
`Ch<N>:<Kind>:<Name>`, with chapters as `Ch<N>:CH`.

Two reference files under `.claude/` carry the conventions, and the skills point at
them rather than restating them:

- **`.claude/STYLE.md`** — how a passage *reads*: the prose voice, the LaTeX
  mechanics, the label scheme and the macro naming conventions. It names four sibling
  repositories as the corpus to imitate, and **this repository is one of them**, so
  its own settled chapters are the nearest corpus there is.
- **`.claude/ORGANIZATION.md`** — where a passage *lives*: the generality ladder that
  decides what earns a chapter, a section and a subsection, plus the naming
  conventions and the format and ownership of `TOPICS.md`.

## The skills

`.claude/skills/`, shared with [Lecture-Notes-Template-2026][tpl] and the sibling
notes repositories. Seven of them:

| Skill | Acts on | Latitude |
| --- | --- | --- |
| `/post-lecture` | one lecture, end to end | composition; owns scope and order only |
| `/address-comments` | `% [CLAUDE]` directives | do exactly what the directive says |
| `/fill-sorries` | `\sorry` markers | work out the mathematics; decide and report |
| `/check-correctness` | what is already written | fix what is false; every change adjudicated |
| `/integrate` | one lecture's raw notes | place new material; never restructure |
| `/organize` | the notes as they stand | rearrange only; add and delete nothing |
| `/americanise` | British spellings | spelling only; never the mathematics |

**This course is over, so two of the seven have nothing to do here.**
`/post-lecture` is the after-lecture pipeline — fill, address, check, respell,
integrate, on one branch and one pull request — and `/integrate` is its last phase.
Both need a lecture to process. They also read from a reusable inbox
(`todays_lecture.tex`) that the template ships and this repository deliberately does
not have; if the author resumes writing up material, copy it from the template first.

The other five all apply to settled notes.

**Two skills do mathematics, under opposite constraints.** `/fill-sorries` supplies an
argument that does not exist, so it has the freest hand in the repository.
`/check-correctness` overwrites one that does, so it changes as little as it can, puts
*every* candidate correction to an independent agent before applying it, and — if it
changed anything — has the result reviewed by two further independent agents on the
pull request. It is the only skill whose subject is whether what is written is *true*.

`\sorry` is the red marker for an unfilled gap. **There are 28 here**, which makes
`/fill-sorries` immediately useful — though with the course over and the notes read
several times, `/check-correctness` is the better first pass over settled chapters.

`% [CLAUDE]` is the other inline marker — a small, specific writing job the author
delegated during a lecture. There are none here at present. Do not treat one as
ordinary commented-out content, and do not delete one without addressing it.

Three markers record where the notes are no longer purely the lecturer's, and a skill
writes all of them:

| Marker | Written by | Means |
| --- | --- | --- |
| `% [FILLED]` | `/fill-sorries` | an argument supplied that the lecture did not give |
| `% [CORRECTED]` | `/check-correctness` | a statement changed, original quoted for revert-by-eye |
| `% [SUSPECT]` | `/check-correctness` | believed wrong, left unchanged, awaiting the author |

Never write a `% [CLAUDE]` marker: that is the author's channel, and one written by a
skill is work the next run will silently do.

**There is no `TOPICS.md` here yet.** It is the running map of topic to
chapter/section, `/organize` owns it, and `/organize` creates it on its first run
following the format in `ORGANIZATION.md`. It was left uncreated rather than written
from the outside, because every line in it has to be traceable to a lecture and this
course's lecture dates are not recoverable from the repository.

New macros go in `TeX_Setup/shortcuts.tex`, never inline. Topology-specific macros are grouped **per chapter** here (`% Ch 4`, `% Ch 5`, …) rather than under one course banner; add to the block for the chapter that needs them, following the naming conventions in `STYLE.md`.

## Publishing

`.github/workflows/publish-latex.yml` runs on every push/PR to `main`. It is a
**caller**: the build itself is a reusable workflow published by
[Lecture-Notes-Template-2026][tpl] and shared with the sibling notes repositories, so
a fix to the build reaches all of them rather than having to be applied seven times.
**To change how the notes are built, change the template.**

[tpl]: https://github.com/thefundamentaltheor3m/Lecture-Notes-Template-2026

The build compiles `main.pdf` with `latexmk` (so `biber` runs and the bibliography
resolves) and uploads it as an artifact; where that PDF then goes depends on the
trigger:

- **push to `main`** — published to the `gh-pages` root, so
  `https://thefundamentaltheor3m.github.io/TopologyNotes/main.pdf` updates, and
  attached to the `Current` release. The committed `TeX_Outputs/main.pdf` is
  republished alongside it as `LastLocallyCompiled.pdf`.
- **pull request** — published to `preview-<PR number>/` on the same site and linked
  from a comment on the pull request, so an unmerged draft never overwrites the
  published notes. `preview-cleanup.yml` deletes the directory when the PR closes.

The build fails loudly (`-halt-on-error`), so a broken document breaks CI rather than
publishing a broken PDF — compile locally before pushing.

CI does not install `texlive-full`; it installs exactly the packages listed in the
template's `.github/texlive-packages.txt` into a cached tree. That manifest is
**shared**, so **adding a `\usepackage` to `TeX_Setup/packages.tex` means accounting
for it in the template**. A repository-local copy would override the shared one and
then have to be maintained separately; prefer adding upstream.
