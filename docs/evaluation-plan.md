# Evaluation Plan

**Project:** Development of a Platform for Finding Car Repair Specialists with a Rating System Based on Verified Customer Reviews  
**Author:** Dastan  
**Supervisor:** Botagoz Mirzagalikova  
**Related task:** [CRP-5](https://dastan-car-repair.youtrack.cloud/issue/CRP-5)  
**Status:** Proposed plan for review. No evaluation results are reported.

## 1. Purpose and boundaries

The evaluation will examine whether the website enforces its requirements and whether representative users can understand and complete its main workflows. It will distinguish software correctness, usability and understanding of review verification.

A verified review establishes a link to a completed, customer-confirmed platform request. It does not independently establish repair quality, review honesty or the absence of collusion. This evaluation will not claim a reduction in real-world repair fraud, improved mechanical outcomes or representative findings for all drivers.

The current standalone prototype can support preliminary interface feedback. Server permissions, persistence, concurrency and performance must be assessed against the implemented website and backend; prototype behaviour cannot establish those properties.

## 2. Evaluation questions

| ID | Question | Planned evidence |
|---|---|---|
| EQ-1 | Does the website enforce role, ownership, status and review-eligibility rules? | Functional and API case records, rejected-operation evidence and persistent-state checks |
| EQ-2 | Are published ratings and review counts calculated consistently? | Known-score examples before and after moderation, including an unrated profile |
| EQ-3 | Can representative users find a specialist, submit a request and review completed service? | Unassisted task completion, time, errors, help requests and comments |
| EQ-4 | Does an explicit verification explanation improve understanding compared with a label alone? | Paired comprehension scores with counterbalanced presentation order |
| EQ-5 | Are the core flows usable across the specified layouts and browsers? | Responsive, keyboard, browser and bounded performance checks |

## 3. Preparation and evaluation environment

Before execution, record the evaluated commit, environment, relevant dependency versions, browser versions, operating system, viewport, hardware and any outstanding defects. Use a separate evaluation environment with fictional accounts, contacts, specialists, requests and reviews. Do not use real repair bookings or publish participant responses as genuine customer reviews.

Prepare two customer accounts, two specialist accounts, an administrator and an anonymous session. Include published, unpublished and unrated specialists; requests in every specified status; and published and hidden reviews. Restore a documented starting state before each case. For concurrent cases, inspect persistent records as well as HTTP responses.

The [requirements](requirements.md) and [API contract](api-design.md) are the acceptance baseline. Resolve differences before execution, recording any approved requirement change. Freeze the user-study wording, scoring rubric and success criteria before the first recorded session. Any pilot used to revise the protocol will be excluded from the main analysis and documented separately.

## 4. Functional verification matrix

These cases are planned, not executed. Expand each grouped row into individually recorded cases during implementation. Check both permitted and rejected actions; a hidden button alone is not evidence of server protection.

| Case | Requirements | Planned procedure and expected outcome |
|---|---|---|
| F-01 | FR-01; NFR-02 | Register each public role, sign in and sign out. Reject duplicate email, incorrect credentials and attempts to register as administrator. A logged-out session loses private access. |
| F-02 | FR-02–04 | Edit only the current specialist's profile; reload to check persistence. Search by city and service together, clear filters and try no matches. Only eligible published profiles appear. Check descending unrounded mean, count tie-breaker, final ID tie-breaker and unrated-last ordering against the API contract. |
| F-03 | FR-05–07 | Submit a valid customer request: both parties see New. Reject missing required fields and an unavailable offering. Another customer or specialist cannot retrieve or change the private request, including through direct API calls. |
| F-04 | FR-07–08; NFR-03–04 | Exercise every allowed transition with its authorised actor; verify history and persistence. Exercise unlisted transitions and wrong actors. Completed, Declined and Cancelled remain terminal. No response must not cause automatic completion; an administrator cannot supply customer confirmation. |
| F-05 | FR-08–09 | Only the owning customer may review Completed service. Attempt review submission in every other status and by anonymous, unrelated customer, assigned specialist and administrator sessions. Reject each ineligible attempt without creating a record. |
| F-06 | FR-09; NFR-03 | Accept integer scores 1–5 with nonblank text, including negative feedback. Reject 0, 6, fractional scores, blank comments and forged author or verification fields. |
| F-07 | FR-09, FR-13; NFR-04 | Submit the same review sequentially, after a simulated uncertain response and through two simultaneous requests. At most one review exists for that request. Repeat after hiding the review: hiding does not release eligibility. Repeat simultaneous trials 20 times with fresh eligible requests and record every outcome. |
| F-08 | FR-10, FR-13 | Scores 5, 4 and 3 give mean 4.0 and count 3. Hiding score 3 gives 4.5 and count 2; hiding all scores gives “Not yet rated” and count 0. Confirm catalogue, profile and review list agree after reload. Check one-decimal display separately from sorting by the unrounded mean. |
| F-09 | FR-11–12 | Submit a valid complaint: it receives an identifier and Open status. Reject missing reasons, invalid targets and unrelated private request identifiers. Only the submitter and administrator can read private complaint details. Only an administrator can resolve or dismiss with a recorded reason. |
| F-10 | FR-12–13; NFR-04 | Moderate a documented rule violation and retain the decision history. A specialist cannot edit or hide customer feedback. Low scores alone are not grounds for removal. Hiding removes a review from public display and aggregates without deleting its retained record or changing request status. |
| F-11 | NFR-02–05 | Attempt direct unauthorised operations and invalid status updates. Check CSRF rejection for unsafe requests without a valid token, logout invalidation, deployed HTTPS/cookie settings and salted password storage. Inspect public responses for private contact details and credentials. Harmless script-markup probes must render safely without execution. Record limits: this is not a comprehensive security audit. |

FR-14 review editing is optional and excluded from the initial API contract. If implemented, add cases for owner-only editing, one retained review identity, updated timestamp and aggregate recalculation before evaluating that feature.

### Functional acceptance rule

All Must acceptance cases must pass before claiming first-version conformance. Report counts of passed, failed, blocked and not-run cases; pass rate is passed / executed cases, accompanied by coverage of planned cases. A blocked or omitted case is not a pass. Any ownership breach, unauthorised confirmation, duplicate review, private-information exposure or incorrect rating is a release-blocking defect. Fixes require rerunning the affected cases and relevant regression cases.

## 5. Usability sessions

### Participants and procedure

Recruit a convenience sample of **6–8 adult drivers with experience of arranging vehicle repair**. This is a feasible formative sample for an individual project, not a statistically representative survey. Participation is voluntary. Explain the purpose and fictional scenarios, obtain consent, allow withdrawal and use anonymous participant codes in notes. Do not collect vehicle registration numbers, real contact details or passwords. Record audio or video only with separate consent; otherwise take notes. Keep consent information separate from study notes, restrict access and agree a retention period before recruitment. Publish only anonymised summaries.

Where feasible, obtain separate feedback from **1–2 repair specialists** on their dashboard workflow. If unavailable, report that gap; developer role-play is a functional walkthrough, not specialist validation. Administrator actions will be checked by the developer against the specification and must not be described as independent expert evaluation.

Use the same scripted instructions, starting states and fictional accounts for each driver. Record device and prior experience without identifying the participant. Allow silent task performance for timing, followed by a short retrospective discussion. Do not explain the verification label before the comprehension comparison in Section 6.

### Driver tasks

| Task | Scenario | Observable success | Time cap |
|---|---|---|---|
| U-01 | Find a specialist for a specified city and repair category; open the profile and report its score and review count | Correct matching profile and correct reading of score/count | 3 minutes |
| U-02 | Using a provided signed-in account, submit a request with fictional vehicle and problem details | Request saved once and visible as New | 4 minutes |
| U-03 | Open a prepared request awaiting confirmation; service occurred but was unsatisfactory | Confirm completion and leave a low score with a concrete comment | 4 minutes |
| U-04 | Open a different prepared request where the service did not occur | Dispute completion with a reason instead of confirming or reviewing | 3 minutes |
| U-05 | Report a prepared service problem and locate the complaint status | Correct complaint submitted and status found | 3 minutes |

The moderator resets each scenario so that failure on one task does not prevent the next. If help is requested, record it before giving a standard hint. Completion after help is assisted success. Stop at the cap or participant withdrawal; record failure or withdrawal explicitly. Do not count a capped or abandoned task as successfully completed.

Measure per task: unassisted successes / attempts, assisted completions, failures, elapsed time from instruction completion to success or cap, critical errors, other errors and help requests. A critical error reaches the wrong consequential outcome, such as confirming service that did not occur. Report median and range of time for successful attempts separately from failures and capped attempts. Collect a post-task ease rating from 1 (very difficult) to 5 (very easy) and one short explanation.

Proposed formative target: at least **80% unassisted completion per task**, rounded up to a whole participant count (5/6 or 7/8), and no observed critical misunderstanding in U-03/U-04. These are project decision thresholds, not published industry benchmarks. Failure triggers interface revision and a documented follow-up; even a passing small sample does not prove universal usability.

## 6. Verification-label comparison

### Baseline and proposed variant

- **A — baseline:** specialist profile with a “Verified request” label and no explanatory text.
- **B — proposed variant:** the same profile with the label and this explanation: “This review is linked to a completed service request confirmed by the customer. Confirmation does not guarantee repair quality or review honesty. Negative reviews are allowed.”

Keep specialist information, review scores/counts, review wording, ordering, layout and all other controls identical within each matched scenario. Only the explanation changes. Run both variants in the same interface and on the same device for a participant. This comparison evaluates explanation comprehension; it does not isolate the effect of server enforcement or compare the platform with a commercial competitor.

Conduct this comparison before the workflow tasks that teach confirmation rules. Allocate participants as evenly as possible to A→B and B→A, using two matched fictional scenarios. Rotate scenario-to-variant assignment so that one specialist is not always paired with B. Record order and scenario assignment. Do not give correctness feedback between variants; use neutral instructions and the same question wording.

### Primary outcome and scoring

After each variant, ask the participant to answer True, False or Not sure:

1. The reviewer is linked to a completed request confirmed by that customer. **True.**
2. The platform independently checked that the mechanical repair was correct. **False.**
3. This label guarantees that the review is honest. **False.**
4. A customer can confirm completed service and still leave a negative review. **True.**

Score one point per correct answer and zero for incorrect or Not sure responses: **0–4 per variant**. Retain item-level responses so harmful misconceptions remain visible. Ask for a brief explanation after the answers. An optional trust rating from 1 to 5 is secondary and must not replace comprehension as the primary outcome.

### Analysis and decision

Report each anonymised participant's A score, B score and paired difference B−A; also report medians, ranges, correct-answer proportions and misconception counts. Show presentation-order groups separately. Summarise qualitative explanations and contradictory cases. Do not impute missing answers; state the number of complete pairs and reasons for missing sessions where known.

The proposed target for B is at least 80% of participants scoring at least 3/4, with no participant endorsing the repair-quality guarantee. Report whether B improved, matched or worsened comprehension relative to A. A target pass alone does not show improvement. With this small convenience sample, interpret differences descriptively and avoid claims of statistically established superiority.

Carryover remains possible: a participant seeing B first may learn how to answer under A. Counterbalancing reduces but does not remove this problem. If order effects are apparent, report them and recommend a larger between-participant comparison rather than attributing all differences to the explanation.

## 7. Non-functional evaluation

| Requirement | Procedure | Acceptance and evidence |
|---|---|---|
| NFR-01 | Inspect search, profile, request form and dashboards at 360, 768 and 1440 CSS-pixel widths | No page-level horizontal scrolling or overlapping primary controls; retain screenshots and issue records |
| NFR-07 | Complete primary flows with keyboard only; inspect labels, focus and validation messages | All primary controls reachable and usable; visible focus; errors identify the field and do not rely only on colour. This does not constitute a full accessibility certification. |
| NFR-08 | Repeat core flows in available Chrome and Safari versions | Record exact versions, OS, viewport and pass/fail by flow; a missing browser is “not run”, not a pass |
| NFR-06 (Should) | Search against 1,000 fictional specialist profiles with 10 concurrent users; use fixed documented filters, 20 warm-up requests and at least 100 measured requests | Target p95 ≤2 seconds. Measure client-observed API round-trip time, including server and network; exclude warm-up. Sort measured durations and use the nearest-rank 95th percentile. Report request count, errors, timeouts, duration, environment, cache conditions and tool configuration. Do not silently discard failures or timeouts. |

Use multiple representative filter combinations in the performance run, including no-match results. Keep the workload and environment identical when comparing revisions. Report first-page rendering separately if measured; API latency does not establish page-rendering speed. Failure of a Should target must be disclosed without being confused with passing all Must criteria.

## 8. Evidence records and reporting

Create the following records when execution begins; no completed records are implied by this plan:

- **Functional case record:** case/subcase ID, requirement, commit, starting state, actor, steps, expected result, actual result, persistent-state evidence, pass/fail/blocked/not run, issue reference.
- **Usability record:** anonymous participant code, device, task, outcome, assistance, elapsed seconds, error category, ease rating and anonymised note.
- **Comparison record:** participant code, variant order, scenario assignment, item responses, score and paired difference.
- **Non-functional record:** environment, procedure, measurements, screenshots and limitations.

Store only sanitised evidence in the repository. Create an evaluation-results document after actual execution, separating observations from interpretation. Link defects and revisions to YouTrack and the evaluated commits. Include negative results and unresolved cases. Record supervisor feedback only when it is actually received.

## 9. Execution sequence and outstanding decisions

1. Review the protocol and confirm interface language, recruitment approach, consent wording and retention period.
2. Implement the core website and prepare isolated fictional scenarios.
3. Execute functional checks; resolve blocking defects before inviting participants.
4. Pilot the instructions, then freeze the main-session protocol.
5. Conduct the label comparison and driver tasks; collect specialist feedback where feasible.
6. Complete responsive, browser, keyboard and performance checks.
7. Analyse the evidence, document limitations and prioritise revisions. Retest changed behaviour without presenting repeat participants as independent new observations.

No sessions, measurements, approvals or successful test outcomes have been invented. Numerical targets and participant counts are proposals for this project and remain subject to review before execution.

[Requirements](requirements.md) · [API design](api-design.md) · [Prototype guide](prototype/README.md)
