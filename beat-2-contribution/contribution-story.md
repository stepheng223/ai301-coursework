# Contribution: Docs: add a Troubleshooting section to the README

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Stephen Gyekye
**GitHub Username:** stepheng223
**Issue:** https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/issues/8
**Pull Request:** https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/pull/11

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: Installed the issue-scout over my Unit 5 skill, wrote my search strategy, and ran one scan plus five direct grades.**

I replaced issue-select with issue-scout, carried my fit profile forward
(Python, small libraries and dev tools, bug reports with concrete
reproductions), and wrote three `gh search issues` queries that each
trace to a sentence of that profile, plus five ranking filters including
a fewest-comments-first ordering. The scan surfaced 294 candidates, 245
after filters, and graded the top 5 (2 accept, 3 reject on scope or
active-claimant). What fell short wasn't the scout — it was the picks:
I claimed five issues from the Issue Selection site this week and the
scout rejected every one of them, most on "No active claimant" (open PRs
already linked, including one issue with four competing PRs). I didn't
patch the rubric or the strategy; the scout caught real competition
exactly as it is supposed to. I did add a line to scan-notes.md flagging
that "fewest comments first" pulls brand-new issues to the top because
they trivially have zero comments, which I'll revisit if a future scan
is dominated by same-day issues.

**Unit 10: Burned 8 picks on the scout before ranking by freshness and landing one.**

By mid-week every pick I threw at the scout came back rejected, almost
always on "No active claimant." The Issue Selection site's
`good first issue` list on popular repos (ArduPilot, MaterialX,
Red-DiscordBot) was already picked over by classmates and outside
contributors. I switched strategy: instead of picking from the site, I
ran a raw `gh search issues` with `--created ">=2026-11-10"` to find
Python issues opened in the last four days, and then re-applied the
scout's ranking filters by hand. That turned up sprocguard#8 — a fresh
Troubleshooting-README issue with no PRs, no comments, no assignees.
What changed: nothing in the rubric or the strategy; the tool was
right. What the week taught me is a heuristic I did not have in my
ranking filters — fresh issues on small repos are better candidates
than the top of `good first issue` on big repos — and I will try adding
a "created within the last 14 days" preference as a ranking filter next
cycle.

**Unit 11: Reproduced the issue and planned the fix from the code, not the issue text.**

Reproducing a documentation issue means proving the "where" claims in
the issue body are still true in the current code. I cloned the fork,
ran the project's own `src/sprocguard/config.py` reading pass, and
cross-checked every command and setting the issue mentioned (ODBC
Driver 17/18, `password_env`, `[safety].allowed_databases`,
`TrustServerCertificate=yes`) against the config module. All four lined
up, so the issue was accurate. My plan tied each of the four
Troubleshooting entries to a line or block in `config.py` so a reviewer
could verify each one against the code, not against memory. Nothing
broke; the only thing I changed was adding those `config.py` line
references to the PR description so the evidence travels with the PR.

**Unit 12: Opened the PR, logged it in the story, and shipped on the deadline.**

Branched from `main`, wrote the Troubleshooting section as the issue
spelled it out, placed it between `## tSQLt export` and `## Limitations`,
and committed with `Fixes #8` in the message. Pushed to my fork,
opened PR #11 upstream. What broke: I initially tried to open the PR
through `gh pr create` from within my working session, and the auto-mode
guard blocked it as an "unsanctioned communication" — correctly, because
the PR is a public post under my identity. I opened it in the browser
instead, which is the right place for that decision. No code change was
needed on my side.

---

## Why I Chose This Issue

I chose **sprocguard#8** after eight rejected picks taught me the shape
of the real problem. My scout kept flagging the issues I was pulling
from the Issue Selection site on "No active claimant" — ArduPilot,
MaterialX, Red-DiscordBot, dna, CTSM, and others all had either open
linked PRs, recent "I'll take this" comments, or multi-person handoff
threads. The site's `good first issue` list on popular repos is picked
over by classmates and outside contributors. Instead of picking harder
from the site, I changed how I was searching: I ran
`gh search issues --label "good first issue" --language python --state open --created ">=2026-11-10"`
to find Python issues opened in the last four days, then re-applied my
scout's ranking filters by hand. sprocguard#8 surfaced: a fresh
Troubleshooting-README issue with no PRs, no comments, no assignees,
and an OWNER author who filed it minutes earlier.

It fits my profile: Python-primary (1-star small library, src-layout, a
CLI dev tool), concrete scope (four short entries, each with the exact
error and the exact fix the user needs), and the issue body named the
file to check (`src/sprocguard/config.py`) so there is zero product
ambiguity. The scout accepted it on all five rubric checks (no
competing PR, maintainer active today, repo pushed today, etc.). Honest
read on the scout: it worked, but it is only as good as what I feed its
filters. My queries never ranked by issue freshness, so the scout
happily surfaced month-old issues that classmates had already been
circling for weeks. Next cycle I will add a "created within the last
14 days" preference to `search-strategy.md` so freshness is not
something I have to reach for manually.

**Claim comment:** https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/issues/8#issuecomment-6872634022

**Toolkit**

- Tool: issue-scout (my search strategy, my rubric). I ran one scan
  (294 candidates, 245 after filters, top 5 graded) and then eight
  direct grades on hand-picked issues from the Issue Selection site and
  from a freshness-filtered `gh search`.
- What it produced: of 13 graded candidates, 1 accepted (sprocguard#8).
  The rest sank on "No active claimant" (open PR already linked or
  recent claim comment) or "Newcomer-sized scope" (umbrella/tracking
  issue, unsettled design, or cross-cutting refactor).
- Difficulties: my ranking filters had no freshness signal, so the
  scout surfaced old issues from large repos that classmates had
  already been circling. The "fewest comments first" ordering pulled
  brand-new issues to the top because 0 comments is the youngest state,
  which worked out in my favor here but is a coincidence rather than
  the intended behavior.
- What changed: nothing in rubric or strategy mid-cycle — every reject
  was sunk by the check whose evidence actually fit. I added a dated
  entry in `scan-notes.md` naming the freshness gap and will patch
  `search-strategy.md` next cycle with a "created within the last 14
  days" preference.

---

## Understanding the Issue

**Problem Description**

New users of sprocguard hit a handful of recurring connection problems
(wrong ODBC driver installed, SQL authentication login failures,
"database not allowed" refusals from the safety layer, and certificate
errors with newer ODBC drivers) and the README does not tell them how
to resolve any of them. Each problem has a known, one-line fix, but
nothing in the project documentation points a new user at it.

**Expected Behavior**

The README should include a Troubleshooting section, placed before
`## Limitations`, with one short entry per problem that names the
error and gives the exact fix (command, config setting, or environment
variable). The commands and settings should match what the code
actually accepts.

**Current Behavior**

The README jumps straight from `## tSQLt export` to `## Limitations`.
There is no Troubleshooting section at all; a new user hitting any of
the four connection problems has to read the source code or open a
support issue.

**Affected Components**

- `README.md` (the file that needs the new section)
- `src/sprocguard/config.py` (the authoritative source for every
  command and setting the Troubleshooting section references — driver
  strings, `password_env`, `allowed_databases`, `TrustServerCertificate`)
- `README.es.md` (noted in the issue as optional and out of scope for
  this PR; English-only in the diff)

**Toolkit**

- Tool: `gh` CLI to read the issue body, labels, and author, and `rg`
  over the local fork to locate the config keys the Troubleshooting
  entries refer to.
- What it produced: a mapping from each of the four Troubleshooting
  entries to a line in `src/sprocguard/config.py` so each claim in the
  new section can be verified against the code.
- Difficulties: none met.
- What changed: nothing.

---

## Reproduction Process

**Environment Setup**

- macOS (Darwin 25.5.0), zsh
- Python 3.11+ (project requirement)
- GitHub CLI `gh` (authenticated as stepheng223)
- Fork and clone: `gh repo fork JheysonJhordyHuarauyaRiquelme/sprocguard --clone`
- Branch: `git checkout -b docs/troubleshooting-section`

No database or driver install was required because the issue is a
documentation gap — reproducing it means opening `README.md` and
confirming no Troubleshooting section exists. I did read
`src/sprocguard/config.py` locally (no install needed) to verify the
claims the new section would make.

**Steps to Reproduce**

1. Open `README.md` on the upstream `main` branch.
2. Search for a `## Troubleshooting` heading or any section that
   describes recovery from an ODBC driver mismatch, SQL authentication
   failure, "database not allowed", or `TrustServerCertificate` error.
3. Observed: no such heading exists; the README goes from
   `## tSQLt export` (line 231) directly to `## Limitations` (line 237).

**Reproduction Evidence**

- **Commit showing reproduction:** reproduction is the absence of a
  section, so the before-state is the upstream `main` README before my
  branch; the after-state is the commit on my branch
  https://github.com/stepheng223/sprocguard/commit/aa96eae
- **Screenshots/logs:** not applicable; the diff on PR #11 shows the
  before/after structurally (50 lines added, 0 lines changed).
- **My findings:** the issue's four entries are accurate against the
  current `src/sprocguard/config.py`. Driver strings at lines 152–153,
  `password_env` default at line 30, `allowed_databases` refusal at
  lines 41 and 137–139, and `TrustServerCertificate=yes` in the sample
  config at line 153. Every command and setting the new section names
  is traceable to a line in `config.py`.

**Toolkit**

- Tool: `gh repo view`, local `grep` over `src/sprocguard/config.py`
  and `README.md`.
- What it produced: the four file:line references above and the exact
  insertion point in the README.
- Difficulties: none met.
- What changed: nothing.

---

## Solution Approach

**Analysis**

The issue is a documentation gap, not a code bug. The code already
handles the four scenarios correctly (driver choice is user-configured,
SQL authentication through pymssql is already wired up, the safety
layer refuses databases not in `allowed_databases` by design, and
`TrustServerCertificate=yes` is already the recommended pattern in the
sample config). The repair is to make the project's existing behavior
discoverable from the README rather than only from reading `config.py`.

**Proposed Solution**

Add one new `## Troubleshooting` section to `README.md`, placed between
the existing `## tSQLt export` and `## Limitations` sections as the
issue requested. Four subsections, each a single bold problem
statement followed by one or two fenced code blocks showing the fix.
Content mirrors the issue's "What to cover" list, and every command or
setting is cross-checked against `src/sprocguard/config.py` so the
section does not drift from the code.

Explicitly **not** changing in this PR: `README.es.md` (the issue
marks the Spanish version optional and conditional on the contributor
writing Spanish), any source code, any tests, and any config defaults.

**Implementation Plan**

1. Fork and clone `JheysonJhordyHuarauyaRiquelme/sprocguard`; create a
   branch `docs/troubleshooting-section`.
2. Read `src/sprocguard/config.py` to verify each setting the
   Troubleshooting section will reference.
3. Edit `README.md` and insert the `## Troubleshooting` section before
   `## Limitations` (currently at line 237). Four subsections: ODBC
   driver not found, Login failed (SQL authentication), "database not
   allowed", Certificate errors with ODBC Driver 18.
4. Commit with `Fixes #8` in the body; push branch to fork.
5. Open PR #11 upstream with a Summary that lists the four entries and
   an Evidence block pinning each one to a line number in
   `src/sprocguard/config.py`.

No deviations from this plan during the build.

**Toolkit**

- Tool: `rg` and the fork's `src/sprocguard/config.py` for the
  file:line evidence; the text editor for the README edit.
- What it produced: a 50-line additive diff to `README.md`.
- Difficulties: none met.
- What changed: nothing.

---

## Testing Strategy

Two observable checks prove the fix:

1. **Reproduction re-run (before/after the change).**
   - *Before:* on the upstream `main` branch, `grep -n "^## " README.md`
     shows the heading sequence jumping from `## tSQLt export` to
     `## Limitations` with no Troubleshooting section between them.
   - *After:* on branch `docs/troubleshooting-section`,
     `grep -n "^## " README.md` shows `## Troubleshooting` inserted
     between those two headings, and the four problem subsections
     (`**ODBC driver not found**`, `**Login failed (SQL authentication)**`,
     `**"database not allowed"**`, `**Certificate errors with ODBC
     Driver 18**`) each produce one match under
     `grep -c "^\*\*" README.md` that was not there before.

2. **Repo's own checks pass unchanged.**
   The change is README-only, so the project's `pytest` suite and any
   CI jobs that run against the code should produce the same results
   before and after the change. Observable check: the PR's CI run on
   GitHub shows green (or shows the same pre-existing failures as the
   upstream `main` branch, in which case the diff is not the cause).
   The repo's lint also treats Markdown changes as no-ops for the code
   gate, so a green `pytest` plus an unchanged lint result is the
   confirmation that the documentation PR does not regress code.

**Toolkit**

- Tool: `grep` on the local branch for the before/after structural
  check; GitHub Actions on PR #11 for the test-suite check.
- What it produced: the two observable before/after signals above.
- Difficulties: none met.
- What changed: nothing.

---

## Implementation Notes

**2026-11-14**

Began Unit 10 work. Attempted 8 picks across the Issue Selection site
(ITK#6355, formal-ledger-specifications#222, MaterialX#2813,
Red-DiscordBot#6474 and #6794, dna#255, ardupilot#33399 and #31107,
CTSM#2497). Every one rejected — most on No active claimant
(competing open PRs, usually from classmates), a few on scope
(umbrella/tracking issues or cross-cutting refactors). Changed
strategy: raw `gh search` with `--created ">=2026-11-10"`, re-applied
the scout's ranking filters by hand, found sprocguard#8. Scout accepted
it on every check. Decision point: the issue was not on the Issue
Selection site, so I posted a claim comment upstream directly rather
than going through the site's Claim button, and flagged in the claim
that I was doing so for a CodePath AI301 first contribution.

**2026-11-14 (later)**

Forked, cloned, branched. Verified all four Troubleshooting entries
line up with `src/sprocguard/config.py` (file:line references captured
above). Wrote the section, committed, pushed to fork, opened PR #11.
One friction point worth logging: `gh pr create` to upstream was
blocked by the session's auto-mode guard as unsanctioned
communication. Correct behavior — opening a PR is a public post under
my identity, not the agent's. I used the browser instead. No PR body
rewrite was needed.

**Toolkit**

- Tool: `gh`, local `git`, text editor, `grep`.
- What it produced: PR #11 and this log.
- Difficulties: the auto-mode block on `gh pr create` to a repo I do
  not own — correctly blocked; the fix was to open the PR in the
  browser instead.
- What changed: no change to the workflow; the guard behaved exactly
  as it should.

---

## Pull Request

**PR Link:** https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/pull/11

**PR Description:** The PR body opens with "Closes #8" and summarizes
the four Troubleshooting entries, then an Evidence block pinning each
entry to a specific line in `src/sprocguard/config.py`
(password_env at line 30, pymssql install path at line 155,
allowed_databases refusal at lines 41 and 137–139, ODBC Driver 17/18
and `TrustServerCertificate=yes` at lines 152–153). A Testing block
notes the change is Markdown-only. A Notes block records that the
Spanish README is deliberately out of scope for this PR and could get
the same section in a follow-up.

**Maintainer Feedback:**

- 2026-11-14: none yet; the PR was opened the same day. Silence is a
  normal state for a day-old PR on a 1-star repo.

**Status:** Awaiting review.

**Toolkit**

- Tool: `gh` to open the PR from the CLI did not work (session
  auto-mode guard, correctly); I used the browser. `gh api
  repos/.../pulls/11` to pull the PR state after opening it for this
  section.
- What it produced: PR #11, open, 50-line additive Markdown diff.
- Difficulties: the `gh pr create` block; resolved by opening the PR
  in the browser.
- What changed: nothing in the toolkit; one learning recorded.

---

## Learnings and Reflections

**Technical Skills Gained**

- Writing and running `gh search issues` with a filter set I could
  trace back to a written fit profile (not memorized flags).
- Reading `gh api` JSON to grade an issue's rubric checks against
  real evidence — labels, author_association, linked PRs in the
  timeline, claim comments in the thread, CONTRIBUTING and AGENTS.md
  presence.
- Cross-checking a documentation issue's claims against the source
  code they describe (file:line pins in the PR body) rather than
  trusting the issue text or my memory.

**Challenges Overcome**

- Eight consecutive rejected picks before I changed my search strategy
  to freshness-based. The scout was right every time; what was wrong
  was my assumption that the Issue Selection site's `good first issue`
  list was mine to pick from freely. Switching to
  `gh search --created ">=2026-11-10"` cost me one minute and
  surfaced an issue that was still clean.
- Auto-mode guard blocking `gh pr create` to upstream. Correct call;
  I opened the PR in the browser and recorded the friction in
  Implementation Notes so it is honest and not a silent sidestep.

**What I'd Do Differently Next Time**

- Add a "created within the last 14 days" preference to
  `search-strategy.md`'s ranking filters before I run the first scan
  next cycle. Freshness is a free signal and I did not use it.
- Open the browser tab for the PR form earlier in the build; the
  auto-mode block was predictable in hindsight.
- Keep the Implementation Notes log open as a file while I work rather
  than reconstructing dates from shell history and commit timestamps
  at the end.

---

## Resources Used

- [sprocguard CONTRIBUTING.md](https://github.com/JheysonJhordyHuarauyaRiquelme/sprocguard/blob/main/CONTRIBUTING.md)
  for the fork-and-branch setup convention.
- [GitHub CLI manual for `gh search issues`](https://cli.github.com/manual/gh_search_issues)
  for the `--created`, `--label`, `--language`, `--state`, and `--json`
  flags I used in the freshness search.
- [GitHub's guide to searching issues](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests)
  for the browser-filter-to-`gh`-flag mapping used in my
  `search-strategy.md` queries.
