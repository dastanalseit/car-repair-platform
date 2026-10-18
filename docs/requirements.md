# Website Requirements

Project: Car Repair Platform  
Author: Dastan  
Supervisor: Botagoz Mirzagalikova  
Version: Initial requirements, 18 October 2026

## Purpose and Scope

The project is a responsive website accessed through a browser on a computer or smartphone. No separate application installation is required. These requirements describe the planned first version; they are not a statement that the features have been implemented or tested.

The main workflow is: find a specialist, submit a service request, receive the service, confirm completion, and leave a review. A review is linked to a completed request owned by the reviewing customer. This establishes a recorded service relationship, not independent proof of repair quality.

Online payments, live chat, native mobile applications and automated recommendations are outside the initial scope. The customer and specialist may agree on price and appointment time by telephone. The website records the request and its progress; it does not process payment.

## Roles and Access

| Role | Allowed activities |
|---|---|
| Visitor | Browse published specialist profiles, services, ratings and reviews; search without registering. |
| Customer | Submit and view own requests, confirm completion, review eligible requests and submit complaints. |
| Specialist | Edit own profile and services, view requests addressed to them, accept or decline requests and update permitted work statuses. |
| Administrator | Review complaints, moderate content that violates rules and record decisions. Administrator access cannot be selected during public registration. |

Private request details and contact information are accessible only to the relevant customer, assigned specialist and authorised administrator. Public reviews do not expose telephone numbers or full private request details.

## Main User Journey

1. A visitor selects a city and repair service, such as Almaty and auto electrical repair.
2. The visitor opens a specialist profile and checks services, location, description, rating and review count.
3. The visitor signs in as a customer and submits the vehicle make, model, problem description and contact telephone number. Vehicle year is optional.
4. The specialist accepts or declines the request. Price and timing may be agreed by telephone.
5. The specialist starts the work and later marks it as awaiting customer confirmation.
6. The customer confirms that the service took place, or reports a disagreement about completion.
7. After confirmation, the customer can leave one text review with an integer score from 1 to 5.

Confirming completion does not mean being satisfied. A customer who received poor service can confirm completion and leave a low score or negative review. No positive score is required to complete a request.

## Request Statuses

| Current status | Action and authorised actor | Next status |
|---|---|---|
| New | Assigned specialist accepts | Accepted |
| New | Assigned specialist declines with a reason | Declined |
| New | Customer cancels | Cancelled |
| Accepted | Assigned specialist starts work | In progress |
| Accepted | Customer or assigned specialist cancels before work starts, with a reason | Cancelled |
| In progress | Assigned specialist reports work finished | Awaiting customer confirmation |
| Awaiting customer confirmation | Request owner confirms service completion | Completed |
| Awaiting customer confirmation | Request owner disputes completion and provides a reason | Completion disputed |
| Completion disputed | Assigned specialist resumes work after discussion | In progress |
| Completion disputed | Request owner confirms that the service was completed | Completed |

Completed, Declined and Cancelled are terminal states in the initial version. A complaint is tracked separately and does not automatically change a request status. In-progress requests cannot be silently cancelled; a disagreement can be reported to the administrator. Lack of a customer response does not automatically complete a request. Administrators cannot create customer confirmation on the customer's behalf.

Each successful status change records the previous status, new status, actor and time. Unlisted transitions are rejected. Handling abandoned or unresolved requests beyond this basic workflow remains a design question for supervisor review.

## Functional Requirements and Acceptance Criteria

Must means required for the first version. Should means desirable after the core workflow is reliable.

| ID | Priority | Requirement | Acceptance criteria |
|---|---|---|---|
| FR-01 | Must | Registration, sign-in and sign-out | A user can register as a customer or specialist with a unique email and password, sign in with correct credentials and sign out. Duplicate emails and incorrect credentials are rejected. Public registration cannot create administrators. |
| FR-02 | Must | Public specialist profiles | Visitors can view a published profile showing name, city, services and description. A specialist can update only their own profile; changes persist after reloading. |
| FR-03 | Must | Search and filtering | Selecting city and service returns only published profiles matching both. Clearing filters restores the wider list. No matches produces a clear empty-state message. |
| FR-04 | Must | Ratings and sorting | Profiles display rating and published verified review count. Rating sorting places higher scores first, uses count as a tie-breaker and places unrated specialists last. Unrated profiles display “Not yet rated”. |
| FR-05 | Must | Service request submission | A signed-in customer can submit a request to a published specialist with make, model, problem description and contact number. Missing required fields prevent submission. The request appears in both parties' accounts as New. |
| FR-06 | Must | Customer dashboard | The customer can view only their own requests, assigned specialist, current status and history. Accessing another customer's request directly is rejected. |
| FR-07 | Must | Specialist dashboard | The specialist sees requests addressed to them and can accept, decline or update work only according to the transition table. Attempts to change another specialist's requests are rejected. |
| FR-08 | Must | Completion confirmation | Only the request owner can confirm completion from Awaiting customer confirmation or Completion disputed. The specialist cannot confirm on the customer's behalf. No review is allowed before Completed. |
| FR-09 | Must | Verified review submission | Only the request owner can submit one review for a Completed request. A text comment and integer score from 1 to 5 are required. Duplicate submissions, including concurrent attempts, create at most one review per request. Other users and requests in other statuses are rejected. |
| FR-10 | Must | Rating calculation | The rating is the arithmetic mean of published eligible scores, displayed to one decimal place. Scores 5, 4 and 3 yield 4.0 with count 3. If the score 3 is hidden after moderation, the result becomes 4.5 with count 2. Zero published reviews shows “Not yet rated”. |
| FR-11 | Must | Complaints | A signed-in user can report a review or their own service request with a reason. The complaint receives an identifier and starts as Open. The submitter can see its status. Unrelated private requests cannot be reported by guessing their identifiers. |
| FR-12 | Must | Complaint moderation | Only an administrator can resolve or dismiss a complaint, recording a reason, actor and time. A specialist cannot edit or delete a customer's review. A negative score alone is not grounds for hiding a review. |
| FR-13 | Must | Review visibility | Published reviews show customer display name, date, score, text and a verified-request label. Hidden reviews are excluded from the public list and rating, but their moderation records remain. Hiding a review does not allow another review for the same request. |
| FR-14 | Should | Review editing | If implemented, the review owner can edit the existing review without creating a second review; the updated time is recorded and rating recalculated. The initial release may keep submitted reviews read-only. |

## Non-functional Requirements

The thresholds below are initial project targets to confirm with the supervisor. They are acceptance targets, not measured results.

| ID | Priority | Requirement | Acceptance criteria |
|---|---|---|---|
| NFR-01 | Must | Responsive layout | Search, profile, request form and dashboards remain usable at viewport widths of 360, 768 and 1440 pixels without page-level horizontal scrolling or overlapping primary controls. |
| NFR-02 | Must | Access protection | Permissions are checked on the server for each private operation. Direct requests from unauthorised users fail even if they bypass hidden interface controls. Passwords are stored as salted hashes, never plaintext. The deployed site uses HTTPS. |
| NFR-03 | Must | Input and output handling | Invalid scores, missing required fields and invalid status transitions are rejected on the server. User-supplied script markup is displayed safely and is not executed. |
| NFR-04 | Must | Consistent records | Repeated or concurrent review submissions cannot bypass the one-review rule. Review creation, request ownership and status checks remain consistent. Status changes and moderation decisions are retained with actor and timestamp. |
| NFR-05 | Must | Privacy | Public pages and responses expose no private request contact numbers, passwords or credentials. Access to request details is limited to the relevant parties and authorised administrators. |
| NFR-06 | Should | Search performance | In a documented test environment with 1,000 specialist profiles and 10 concurrent users, the 95th percentile search response time should be at most 2 seconds across at least 100 measured requests after warm-up. Record hardware, dataset and method with results. |
| NFR-07 | Must | Basic accessibility | Primary flows can be completed using a keyboard. Inputs have labels, focus is visible, and validation messages identify the field and problem without relying only on colour. |
| NFR-08 | Must | Browser support | The main flows are checked in Chrome and Safari versions available at evaluation time. Record exact versions and any failures. |

## Website Pages

| Page | Purpose | Related requirements |
|---|---|---|
| Home and search results | Choose city and service; browse and sort specialists | FR-02–FR-04 |
| Specialist profile | View services, location, rating and reviews; open request form | FR-02, FR-04, FR-05, FR-13 |
| Registration and sign-in | Create an account and access private functions | FR-01 |
| Service request form | Enter vehicle and problem details | FR-05 |
| Customer dashboard and request details | Follow own requests, confirm completion, review or complain | FR-06, FR-08–FR-11 |
| Specialist dashboard | Manage profile, services and incoming requests | FR-02, FR-07 |
| Administrator panel | Review complaints and record moderation decisions | FR-12, FR-13 |

## Basis and Open Decisions

The roles and main journey reflect the project scope discussed with the author. The detailed acceptance rules and numerical targets are an initial specification for review. They have not yet been approved by the supervisor or validated in formal user interviews.

The [existing system comparison](existing-system-comparison.md) supports location and service discovery, visible review counts and complaint handling. The [README](../README.md) describes the overall project scope.

Before implementation, confirm the initial service categories and cities, interface language, moderation rules, and handling of abandoned requests. Create YouTrack tasks referencing the requirement IDs. Then prepare the Use Case Diagram, system context diagram, component diagram and interface prototype.
