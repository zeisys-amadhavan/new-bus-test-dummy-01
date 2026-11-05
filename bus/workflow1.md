# Workflow 1 — One small verified improvement to the README (live test workflow)

## 1. Purpose
Produce one tiny change to `README.md` whose score under `bus/criteria.md` is verified by the scorer to be higher, delivered as one draft pull request. This is the shortest cycle that makes all four agents act under their own Apps: a score, an issue, an approval, a commit, a rescore and a pull request. It exists to test the bus live; the content of the README does not matter.

## 2. Request
| Field | Value |
|---|---|
| Request | a request issue made from `bus/request-template.md` (the issue is supplied at launch) |
| Owner | zeisys-amadhavan |
| Status | active |

## 3. Subject and yardstick
| Field | Value |
|---|---|
| Subject | `README.md` |
| Yardstick | `bus/criteria.md` |
| Must survive | none |
| Checks | none |
| Log | none |
| One result is | a draft pull request changing at most 12 lines of the subject whose unrounded total under the yardstick is at least 0.25 higher than the scorer's baseline for the exact `main` commit it was built from, with the reviewer approving the proposal |

## 4. Team
| Role | Agent | Responsibility | Independent of |
|---|---|---|---|
| scorer | claude | scores the baseline and the candidate; its score is the gate | implementer |
| proposer | chatgpt | proposes one tiny change as an issue | reviewers |
| reviewers | grok | approves or rejects the proposal | proposer, implementer |
| implementer | chatgpt | applies the approved change on a branch | scorer, reviewers |
| pr_creator | gemini | opens the draft pull request with the evidence | — |

Approvals: the reviewer, on the proposal. Closes an issue: only its opener. Merges: the owner only.

## 5. Steps
1. **Scorer** — score the unchanged subject at the current `main` commit against the yardstick; return the unrounded total, the criterion scores and the criterion-level weaknesses — produces a score — passes when the result is valid.
2. **Proposer** — from the baseline, pick the single weakness that one extremely small change can address; state the exact modification, the criterion, the rationale and the predicted gain; if no legitimate small change remains, say so — produces an issue — passes when it does not duplicate a pending proposal; otherwise REJECTED.
3. **Reviewers** — review the issue; approve only a small change that should raise the score — produces a comment — passes when all reviewers approve; otherwise step 7.
4. **Implementer** — apply only the approved change, as the full new file, on a new branch from the baseline's `main` commit; link the issue — produces a branch — passes when at most 12 lines changed and only the subject changed; otherwise step 7.
5. **Scorer** — rescore the entire candidate against the unchanged yardstick; return the unrounded total, the criterion scores, coverage, quoted evidence and criterion-level weaknesses — produces a score — passes when the gain over step 1 is at least 0.25; otherwise step 7.
6. **PR creator** — open a draft pull request against `main` with the evidence — produces a pull request — passes when always; then ACCEPTED.
7. **Proposer** — close the issue it opened with the reason the cycle stopped — produces nothing — passes when always; then REJECTED.

## 6. Progress in one cycle
| Step | Done when this exists | Where to see it |
|---|---|---|
| 1 | baseline score receipt by the claude App | ledger |
| 2 | issue opened by the chatgpt App, label `improvement-proposal` | issues |
| 3 | one approval comment by the grok App | the issue |
| 4 | branch with one commit by the chatgpt App, at most 12 lines | branches |
| 5 | score receipt by the claude App, gain at least 0.25 | ledger |
| 6 | draft PR by the gemini App | PR list |
| 7 | (only when the cycle stops early) issue closed by the chatgpt App with the reason | the issue |

## 7. Limits and stop
| Field | Value |
|---|---|
| Starts | on an admitted request issue that names this workflow |
| One cycle ends when | the pull request is open (accepted), or step 7 ran (rejected), or a turn was blocked |
| Money per cycle (USD) | 3 |
| Paid model calls per cycle | 6 |
| Hours per cycle | 1 |
| Revisions of a rejected proposal | 0 |
| Waits for a human | never; a blocked turn stops the request immediately with its reason |

## 8. Rules
**Always**
- One issue, one narrowly scoped change, one pull request per successful cycle.

**Never**
- Modify the yardstick or manufacture a gain.

The cardinal rules in `bus/bus.md` apply on top of these and cannot be loosened here.

## 9. Report
After every cycle, one line on the request issue: cycle number, accepted or rejected or blocked, the PR link or the reason, the gain. Every number comes from receipts.

## 10. Places
| Thing | Where |
|---|---|
| Branch per result | `improvement-started-YYYYMMDDHHMM-<run>-<cycle>-<attempt>` (UTC) from `main` |
| Pull requests | draft against `main`; never merged by the bus |
| Issues | label `improvement-proposal` |
| Run records | branch `ontolibrary-com-x-bus-ledger` |
| Final report | comments on the request issue |
