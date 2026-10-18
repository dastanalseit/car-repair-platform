# API Design

Status: Proposed contract for the first website version. Endpoints are not implemented.

## Conventions

- Base path: `/api/v1/`. All paths below are relative to this base.
- JSON request/response bodies; snake_case fields; positive integer IDs.
- Timestamp fields use ISO 8601 UTC strings. Documentation examples omit literal calendar dates.
- Successful reads and updates: 200; creation: 201; logout: 204 with no body.
- Lists use `{"count": 0, "next": null, "previous": null, "results": []}`.
- Pagination: page (default 1), page_size (default 20, maximum 100). Invalid values return 400.
- Reject unknown write fields and attempts to set protected fields. Treat comments/descriptions as plain text.
- Public endpoints do not expose email addresses, telephone numbers, password hashes or private request details.
- Endpoint tables describe the initial contract. Input-length limits and throttle thresholds will be fixed before implementation.

## Authentication and CSRF

Proposed approach: Django server-side sessions for this browser-only website, with React and the API deployed under the same origin. Use a development proxy for local frontend requests.

React obtains a CSRF token, sends cookies with requests, and supplies X-CSRFToken on POST/PATCH operations. Explicitly protect registration and login even for anonymous clients. Rotate the session on login, obtain a fresh CSRF token after login, and invalidate the session on logout. Production session cookies use Secure, HttpOnly and SameSite=Lax; deploy over HTTPS. Session identifiers are never returned in JSON or stored in localStorage.

Use DRF SessionAuthentication with explicit permission classes. This contract uses 403 for missing authentication under session authentication; distinguish it using `authentication_required`. Login failure uses 400 `invalid_credentials` with a generic message. CSRF failures use 403 `csrf_failed`. Configure a JSON CSRF failure response and exception handler to match the envelope below.

These are design choices, not existing configuration. See [DRF authentication](https://www.django-rest-framework.org/api-guide/authentication/) and [Django CSRF guidance](https://docs.djangoproject.com/en/5.2/howto/csrf/).

| Method and path | Access | Input | Success |
|---|---|---|---|
| GET auth/csrf/ | Public | None | 200: csrf_token; sets CSRF cookie, no account session required |
| POST auth/register/ | Anonymous | email, password, display_name, role | 201: Account; does not sign in automatically |
| POST auth/login/ | Anonymous | email, password | 200: Account; sets session cookie |
| POST auth/logout/ | Signed-in user | Empty object | 204 |
| GET auth/me/ | Signed-in user | None | 200: Account |

Account response: id, email, display_name, role. Never return the password or hash. Registration accepts only customer or specialist. Reject administrator, is_staff and is_superuser inputs. Require unique normalised email and Django password validation. Staff accounts are provisioned separately. Registering as a specialist creates an account; the profile endpoint below completes their profile.

## Public catalogue

| Method and path | Access | Query | Success |
|---|---|---|---|
| GET cities/ | Public | Pagination | List of id/name |
| GET service-categories/ | Public | Pagination | List of id/name |
| GET specialists/ | Public | city_id, service_category_id, ordering, pagination | List of SpecialistSummary |
| GET specialists/{id}/ | Public | None | SpecialistDetail |
| GET specialists/{id}/reviews/ | Public | Pagination | List of PublicReview |

Filters combine with AND and include only published profiles of active accounts. A service filter matches active offerings. Supported ordering: rating (default) or name. Rating uses unrounded average descending, review count descending and ID ascending; unrated profiles are last. Name uses public_name then ID ascending. Unknown filters/orderings return 400; valid filters with no matches return an empty list.

SpecialistSummary: id, public_name, city {id,name}, description, active services [{id,category_id,category_name,description}], rating (one-decimal string or null), review_count. SpecialistDetail uses these fields; paginated reviews are fetched separately.

PublicReview: id, customer_display_name, score, comment, created_at, updated_at, verified_request=true. Do not return request_id publicly. Hidden reviews and unpublished specialist profiles return no public content; inaccessible profile IDs return 404.

## Specialist profile and services

All routes require specialist role and operate on the current user's profile. No owner ID is accepted from the client.

| Method and path | Input | Success |
|---|---|---|
| GET specialist/profile/ | None | 200: own profile, including publication flag and inactive services; 404 if not created |
| POST specialist/profile/ | public_name, city_id, description | 201: unpublished profile; 409 if already present |
| PATCH specialist/profile/ | Any of public_name, city_id, description, is_published | 200: updated own profile |
| GET specialist/services/ | Pagination | 200: own active and inactive services |
| POST specialist/services/ | category_id, description | 201: active offering |
| PATCH specialist/services/{id}/ | description and/or is_active | 200: updated offering |

Publishing requires a complete profile, active account and at least one active service. Duplicate specialist/category pairs return 409. Category and specialist references are immutable; deactivate an offering instead of deleting it. Changes affect future catalogue visibility but preserve existing request access and history.

## Requests and status history

| Method and path | Access | Input/query | Success |
|---|---|---|---|
| POST requests/ | Customer | specialist_service_id, vehicle_make, vehicle_model, problem_description, contact_phone; optional vehicle_year | 201: RequestDetail in new state |
| GET requests/ | Customer or specialist | Optional status; pagination | 200: own submitted or assigned requests, newest first with ID tie-breaker |
| GET requests/{id}/ | Owner, assigned specialist or authorised administrator | None | 200: RequestDetail |
| GET requests/{id}/history/ | Same as detail | Pagination | 200: chronological HistoryEvent list |
| POST requests/{id}/actions/ | Permitted actor below | action; reason where required | 200: updated RequestDetail |

The server assigns customer_id from the session and derives the assigned specialist from the selected offering. The offering must be active and its profile published at creation. Required strings must be nonblank; validate telephone format, not real ownership of the number. vehicle_year may be omitted/null; otherwise it must be a plausible integer under a documented validation policy.

RequestDetail: id, customer {id,display_name}, specialist {id,public_name}, specialist_service_id, service_category_name, vehicle_make, vehicle_model, vehicle_year, problem_description, contact_phone, status, created_at, updated_at, confirmed_at, review_id (null until submitted), available_actions. review_id remains present if the review is hidden. This response is private.

HistoryEvent: id, from_status, to_status, actor {id,display_name,role}, reason, created_at. Initial from_status is null. Users cannot create or edit history directly. available_actions helps the interface; it never replaces server checks.

### Actions and permitted transitions

| action | Actor | From | To | Reason |
|---|---|---|---|---|
| accept | Assigned specialist | new | accepted | Optional |
| decline | Assigned specialist | new | declined | Required |
| cancel | Customer | new | cancelled | Optional |
| cancel | Customer or assigned specialist | accepted | cancelled | Required |
| start | Assigned specialist | accepted | in_progress | Optional |
| submit_completion | Assigned specialist | in_progress | awaiting_confirmation | Optional |
| confirm_completion | Customer | awaiting_confirmation or completion_disputed | completed | Optional |
| dispute_completion | Customer | awaiting_confirmation | completion_disputed | Required |
| resume | Assigned specialist | completion_disputed | in_progress | Optional |

These machine-readable states map to the labels in the requirements. Completed, declined and cancelled are terminal. There is no automatic completion for inactivity and administrators cannot confirm on a customer's behalf.

Lock the request and save the state change and history together in one transaction. Set confirmed_at only on customer confirmation. Invalid current-state transitions return 409; a disallowed actor returns 403 after access checks. Unrelated users receive 404. No general PATCH or DELETE endpoint for requests is offered.

Example request creation (illustrative data):

```json
{
  "specialist_service_id": 12,
  "vehicle_make": "Toyota",
  "vehicle_model": "Corolla",
  "vehicle_year": null,
  "problem_description": "The left headlight does not turn on.",
  "contact_phone": "+77000000000"
}
```

Example completion action:

```json
{"action": "confirm_completion"}
```

## Verified reviews

| Method and path | Access | Input | Success |
|---|---|---|---|
| POST requests/{id}/review/ | Request-owning customer | score, comment | 201: own ReviewRecord |
| GET requests/{id}/review/ | Owner, assigned specialist or authorised administrator | None | 200: ReviewRecord; 404 if absent |

ReviewRecord: id, request_id, customer_display_name, score, comment, visibility, created_at, updated_at, verified_request=true. This private representation can show a hidden review to the request parties. Public responses use PublicReview instead.

Require completed status, confirmed_at, score as an integer 1–5 and nonblank comment. Derive the author and specialist from the request. Reject client-supplied author, visibility and verification flags. Accept negative comments and low scores.

Lock and validate the request inside the insertion transaction. A unique non-null review.request_id enforces one review, including concurrent submissions and hidden reviews. Return 409 review_already_exists for a duplicate and 409 request_not_completed for an ineligible state. Recalculate the published aggregate; the client cannot set rating or count.

Example review:

```json
{"score": 2, "comment": "The repair was completed, but the problem returned."}
```

Review editing is FR-14 (Should) and is excluded from this initial contract. No customer or specialist endpoint deletes or hides a review.

## Complaints and administration

| Method and path | Access | Input/query | Success |
|---|---|---|---|
| POST complaints/ | Signed-in user | Exactly one of request_id or review_id; reason | 201: ComplaintDetail with status open |
| GET complaints/ | Signed-in user | Optional status; pagination | 200: only the submitter's complaints |
| GET complaints/{id}/ | Submitter or authorised administrator | None | 200: ComplaintDetail |
| GET admin/complaints/ | Authorised administrator | Optional status; pagination | 200: all complaints, newest first |
| POST admin/complaints/{id}/decision/ | Authorised administrator | outcome, reason, review_action | 201: Decision |

For request targets require ownership or assignment. For review targets require a currently published review on a public profile. Reject both/neither targets with 400. Inaccessible targets return 404. reason must be nonblank.

ComplaintDetail: id, target {type,id}, reason, status (open/resolved/dismissed), created_at, decision (null or Decision). Do not include the submitter's email or the target request's private contact details.

Decision: id, complaint_id, outcome, reason, review_action, administrator_display_name, created_at. outcome is resolved or dismissed; review_action is none or hide. Hide requires a resolved review-target complaint and a documented violation. A low score alone is not a violation. Invalid combinations return 400; an already decided complaint returns 409 complaint_already_decided.

Save the decision and any visibility change in one transaction, locking relevant records. A complaint does not modify request status. Hidden scores leave the public aggregate, while the review and decision history remain.

Django Admin at /admin/ is the planned staff interface, not a React admin dashboard. The admin API routes define the same operations for API access; both must call shared permission and business-rule code. General admin editing must not bypass request confirmation or moderation history.

## Errors and retries

Proposed common error envelope:

```json
{
  "error": {
    "code": "validation_error",
    "message": "Check the submitted fields.",
    "fields": {"score": ["Enter an integer from 1 to 5."]}
  }
}
```

fields is an empty object when the error is not field-specific. Implement this shape with explicit DRF exception handling; it is not a claim about default DRF responses.

| HTTP status | Typical codes |
|---|---|
| 400 | validation_error, invalid_credentials, invalid_target |
| 403 | authentication_required, permission_denied, csrf_failed |
| 404 | not_found (including inaccessible private objects) |
| 409 | invalid_transition, request_not_completed, review_already_exists, complaint_already_decided, profile_already_exists, service_already_exists |
| 405 | method_not_allowed |
| 429 | throttled; include Retry-After |
| 500 | internal_error; no stack traces or secrets |

Lists are filtered before pagination. Access checks precede private object-specific error details. Apply bounded throttling to authentication and writes; exact limits remain to be selected.

After an uncertain network result, refetch the relevant state before retrying an action or review. Actions return 409 if already applied; review uniqueness prevents a second review. General request and complaint creation do not yet provide idempotency keys: do not retry these POSTs automatically. A repeated creation can produce another record.

## Requirement mapping and implementation order

| Requirements | API area |
|---|---|
| FR-01 | Authentication |
| FR-02–04 | Catalogue and specialist profile/services |
| FR-05–08 | Requests and actions |
| FR-09–10, FR-13 | Reviews and derived ratings |
| FR-11–12 | Complaints and administration |
| NFR-02–05 | Server permissions, validation, transactions, response privacy |

Implementation order: custom user model and PostgreSQL migrations; authentication; catalogue; request lifecycle; reviews; complaints and staff actions. Then connect React and perform the separately documented acceptance checks when scheduled.

This is a design document, not an implemented or tested API. Generate an OpenAPI specification from the implementation and reconcile it with this contract before frontend integration.

[Requirements](requirements.md) · [Database design](database-design.md) · [Technology choices](technology-comparison.md)
