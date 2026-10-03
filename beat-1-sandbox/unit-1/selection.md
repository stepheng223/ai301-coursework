# Issue selection write-up

## Chosen issue

- Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/61
- Verdict from the skill: accept
- Why it fits: the report is narrow, actionable, and clearly tied to a concrete bug in the health check route; it does not rely on broad product decisions or unresolved design debates, and the repo still looks active.

## Run history

My rubric was first evaluated with the full harness command:

```bash
python3 /Users/stephen/ai301-unit1-starter/eval/run_eval.py --rubric /Users/stephen/.claude/skills/issue-select/rubric.md --save-run eval-run.txt
```

That full run produced the transcript saved in `eval-run.txt`. The result was 18/20 scored items in agreement, which is exactly at the course bar, with the main disagreements coming from issue-19 and issue-20. I used that output to check which checks were too strict or too permissive, then kept the rubric focused on the four core families the course emphasizes: maintainer health, repo liveness, newcomer-sized scope, and no active claimant, while also keeping the policy check explicit.

## Issue analysis

I used issue-19 as the example of a scored disagreement because it is a good illustration of why the rubric needs to be conservative on scope. Gold label: accept. My rubric: reject.

- Gold verdict: accept
- Rubric verdict: reject
- Reasoning: the issue is a performance bug with a named cause and a bounded fix area, but my rubric was still worried that the issue sounded slightly broader than a pure “small patch” task. The wording in the “Newcomer-sized scope” check is intentionally conservative, so I treated the issue as a borderline scope case rather than a clean accept. That was the wrong call on the instructor’s side, and it showed me that the rubric needs to reward clearly bounded defects even when the issue report is brief.

This is exactly the sort of trade-off the assignment warns about: a small but real bug can still be a strong first issue if the actual work is narrow and the fix is testable.

## Check rationale

The current rubric wording that mattered most was the “Newcomer-sized scope” check:

> "Pass if the requested contribution is one bounded change with an identifiable outcome. Fail for a tracking/umbrella issue, a pure usage question, work whose design is still actively unsettled, an issue that makes a maintainer-confirmed broad/core-internals change the task, or a product decision with no stated requirements. Do not fail only because a report is brief, lacks reproduction steps, or lacks a detailed checklist."

This wording is what steers the rubric away from rejecting every terse or lightly documented bug report. It also explains why issues with real scope ambiguity need special scrutiny: if the task is not one bounded, identifiable change, the rubric should reject it even if the repo is lively and the issue seems legitimate.

## Trade-offs

The main trade-off in this rubric is that it prioritizes “safe rejects” over “optimistic accepts.” That makes sense for a first-issue selection tool: a repo with missing liveness or ambiguous scope is a bad first contribution even when the bug looks tempting. The cost is that a few genuinely good, small bugs will be filtered out as borderline scope cases, which is why issue-19 was a useful calibration point.

The final rule is therefore conservative but not overly rigid: it accepts only issues that show clear maintainer activity, a living repo, bounded work, no active claimant, and no policy conflict. The chosen issue, #61, fits that standard cleanly and is a good example of the kind of small bug a newcomer can confidently take on.
