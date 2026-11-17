# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Stephen Gyekye

## Featured Tools

I'm featuring issue-scout, repro-check, and plan-check because they are the three tools that actually did work on a real contribution this term. The fourth installed tool — pr-precheck — I used once and it did not evolve, so it belongs in the Inventory. Issue-scout is the one that moved the most: it started life as issue-select at Unit 1, got rebuilt into a search-and-grade tool at Unit 9, and then taught me a lesson about freshness at Unit 10 that I had not written into its filters. Repro-check and plan-check did less visible evolution but were load-bearing on the contribution I actually shipped, PR #11 on sprocguard.

---

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout searches GitHub for first-contribution candidate issues, ranks them cheaply against a written search strategy, and grades the top candidates against a written rubric. The judgment I wrote is the rubric and the fit profile: four required checks (Maintainer activity, Project in use, Newcomer-sized scope, No active claimant), each with a pass condition a stranger could apply and get the same answer I would, plus a fit profile that says what counts as mine to pick up — Python, small libraries and dev tools, bug reports with concrete reproductions.

**How it evolved, dated:**
- 2026-10-03 — Installed `issue-select` and wrote the rubric and scope files (commits `6a61915`, `32e6780`). Four required checks: Maintainer activity, Project in use, Newcomer-sized scope, No active claimant. Friction: the installed scaffold shipped empty — without the rubric it could not grade anything.
- 2026-11-03 — Replaced `issue-select` with `issue-scout` (commit `16c59a4`). Carried the fit profile forward and wrote three `gh search issues` queries each traced to a sentence of the profile, plus five ranking filters including fewest-comments-first ordering. Friction: issue-select could grade a candidate I handed it but could not find one.
- 2026-11-14 — Added a freshness-filtered search by hand (`--created ">=2026-11-10"`) and logged the gap in `scan-notes.md`. Friction: eight consecutive picks from the Issue Selection site were rejected on "No active claimant" because the ranking filters had no freshness signal.

**Evidence:** First scan on 2026-11-03 returned 294 candidates → 245 after filters → top 5 graded (2 accept, 3 reject on scope or active-claimant). Rubric excerpt from `tools/issue-select/rubric.md`:

```
| Check              | Pass condition (abridged)                                                     | Weight   |
| Maintainer activity| non-bot default-branch commit within 365d OR maintainer on this issue         | required |
| Project in use     | not archived AND (release within 18mo OR push within 180d)                    | required |
| Newcomer scope     | one bounded change with identifiable result; not umbrella/tracking            | required |
| No active claimant | no assignee, no open linked PR, no claim comment within 90d                   | required |
```

The catch it actually made (2026-11-14): sprocguard#8 surfaced via the freshness-filtered search and passed all five checks, after eight prior picks from the Issue Selection site had been rejected on "No active claimant." That became PR #11.

---

**repro-check**

**What it is, and the judgment hole I wrote:** repro-check takes an issue and decides whether I can reproduce the claim it makes. The judgment I wrote is what counts as reproduced for the kind of issue I pick: for a documentation issue, "reproduced" means every command, setting, and path the issue body mentions is still present in the current code at the version I'm reading. That turned out to matter — sprocguard#8 named four ODBC/auth/safety scenarios and the only way to vouch for them was to pin each one to a line in `src/sprocguard/config.py`.

**How it evolved, dated:**
- 2026-10 — Installed `repro-check` at Unit 2 (placeholder in `tools/repro-check/`).
- 2026-11-14 — First real use, on sprocguard#8. The judgment I applied: for a documentation issue, reproduction means confirming the issue body's claims are still true in the current code. Cross-checked every command and setting against `src/sprocguard/config.py`.

**Evidence:** All four Troubleshooting entries verified at specific lines: driver strings at 152–153, `password_env` default at 30, `allowed_databases` refusal at 41 and 137–139, `TrustServerCertificate=yes` in sample config at 153. These file:line pins traveled into the PR body's Evidence block: https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/pull/11

---

**plan-check**

**What it is, and the judgment hole I wrote:** plan-check takes a planned fix and decides whether it's ready to post and build from. The judgment I wrote is a rule that every claim in the plan has to tie back to a line of code a reviewer could check on their own, not to my memory or to the issue text. For sprocguard#8 that meant the plan was literally a map: four Troubleshooting entries to four `config.py` locations, which became the PR's Evidence block verbatim.

**How it evolved, dated:**
- 2026-10 — Installed `plan-check` at Unit 3 (placeholder in `tools/plan-check/`).
- 2026-11-14 — Used on sprocguard#8 to plan the fix from the code, not the issue text. Tied each of the four Troubleshooting entries to a line or block in `config.py` so a reviewer could verify each one against the code.

**Evidence:** The plan became the PR's Evidence block. Reviewers can verify every claim without reading the issue — each Troubleshooting entry points at a line in `src/sprocguard/config.py`. See PR #11.

---

## Inventory

- pr-precheck: Installed at Unit 4 (`tools/pr-precheck/`). Used once on 2026-11-14 to draft the PR #11 body (Summary + Evidence + Testing + Notes). Did not evolve this term.
- issue-select: Superseded by issue-scout at Unit 9 (2026-11-03). Rubric and scope carried forward; files still in `tools/issue-select/` as the starting state.

## The Arc

**Beat 1**
Date: 2026-10-03
Friction: Unit 1 required a first-issue selection skill but the installed `issue-select` scaffold had no rubric and no scope. Without them it could not grade anything.
Change: Wrote the four-check rubric (Maintainer activity, Project in use, Newcomer-sized scope, No active claimant) and the scope file for the installed tool, and committed them.
Result: Unit 1 submission finalized at commit `32e6780`; the tool had the judgment it needed to grade individual issues I handed it.

**Beat 2**
Date: 2026-11-03
Friction: `issue-select` could grade a candidate I handed it but could not find one. I was supplying candidates by hand, which is not a toolkit.
Change: Replaced the tool with `issue-scout`, carried the fit profile forward, and wrote three `gh search issues` queries plus five ranking filters so the tool could surface its own candidates. Committed as `16c59a4`.
Result: First scan returned 294 candidates → 245 after filters → top 5 graded (2 accept, 3 reject). The search half worked; the picks I was feeding in by hand did not.

**Beat 3**
Date: 2026-11-14
Friction: Eight consecutive picks from the Issue Selection site rejected, almost all on "No active claimant" — classmates and outside contributors were already on the popular `good first issue` lists.
Change: Stopped picking from the site and ran `gh search issues --label "good first issue" --language python --state open --created ">=2026-11-10"` to find Python issues opened in the last four days, then re-applied the scout's ranking filters by hand.
Result: sprocguard#8 surfaced — a fresh Python Troubleshooting-README issue with no PRs, no comments, no assignees. The scout accepted it on all five checks.

**Beat 4**
Date: 2026-11-14
Friction: A documentation issue is only as good as its claims; the Troubleshooting entries named specific commands and settings that had to match what the code actually accepts.
Change: Used `repro-check` and `plan-check` against `src/sprocguard/config.py` to tie every Troubleshooting entry to a specific line, then pinned those file:line references into the PR body.
Result: PR #11 opened upstream the same day with an Evidence block pinning every claim to a `config.py` line. Awaiting review as of 2026-11-16.

## Limitations and What's Next

The honest shape of this toolkit is that it is thin in evolution — three of my four tools got used once, on one contribution, and did not change. Only issue-scout saw real iteration, and even there the iteration happened at Unit 10 in the field rather than in a patch to `search-strategy.md`. What I'd build next: write the freshness filter into `search-strategy.md` so I don't catch it by hand again, and run repro-check and plan-check against a code-behavior bug on my next contribution so they are tested on something other than a docs change. The pr-precheck loop stays open until PR #11 gets a review — that feedback is what will tell me whether the tool's PR-body shape actually earns a quicker merge.

**Tool limits.**

issue-scout: ranking filters still have no freshness signal — I caught the gap manually in Unit 10 and logged it in `scan-notes.md`, but I have not yet patched `search-strategy.md` to prefer "created within the last 14 days."
repro-check: only exercised on a documentation issue where reproduction meant confirming file:line references; untested on a code-behavior bug where reproduction would need a failing test.
plan-check: same single-exposure limit — used only on a docs change whose plan was a line-by-line map. Untried on a multi-file code change where the plan would need to sequence edits across files.
pr-precheck: no feedback loop closed yet — PR #11 is still awaiting review, so the tool has not been tested against a real maintainer response.
