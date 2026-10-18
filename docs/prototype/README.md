# Website interface prototype

[Open or download the standalone source](index.html). GitHub displays HTML as source: download it and open it in a browser to interact with the prototype. It uses no external dependencies or network requests.

AutoSenim is a provisional interface name. The official diploma title remains unchanged. The interface is in Kazakh for this review; the final interface language remains to be confirmed.

## Screens and interactions

- Home and directory: city/service filters, rating sort, empty results.
- Specialist profile: service description, rating, review count and verified-review labels.
- Demo sign-in: customer or specialist; this explicitly substitutes for real registration/authentication.
- Request form: required vehicle make/model, problem description and sample contact field.
- Customer dashboard: own requests, cancellation where allowed, completion confirmation/dispute, one review after completion, complaints and history.
- Specialist dashboard: selected specialist's assigned requests, profile description editing, request acceptance/decline, work progress and completion submission.
- Administrator view: complaint decisions with reasons and optional hiding of reported reviews; hidden scores leave the public rating.

## Walkthrough

1. Browse the catalogue, optionally filter by Almaty and auto electrical repair, and open Ayan's profile.
2. Choose Request service, enter Demo sign-in as Customer, then submit a sample request.
3. In the demo toolbar choose Specialist. Accept the new request, start work, and mark work finished.
4. Switch to Customer. Confirm completion and submit a text review with a score. The profile rating and count update; the same request cannot receive a second review.
5. To explore disagreement, use the seeded request awaiting confirmation. Dispute completion with a reason. The specialist can resume work; the customer can later confirm completion.
6. Report a review from its profile, switch to Administrator, and record a decision. If a reported review violates rules, hide it with a recorded reason and observe the recalculated rating.

The specialist demo follows the most recently selected profile. The role switch is a preview control, not a production feature. The single customer persona is Dastan. Every specialist, review and request is fictional demonstration content.

## Limits

This is an interface prototype, not the finished website. State is held in browser memory and is lost on reload. No real account, password check, server, database, telephone message, service booking, payment or external complaint is created. The contact field is not retained. Do not enter real personal data.

The prototype demonstrates client-side interactions only. It cannot demonstrate secure authorisation, concurrent duplicate protection, server validation, persistent audit records, email uniqueness or performance targets. Production implementation must satisfy [requirements.md](../requirements.md) independently. Registration and sign-out screens are represented by the demo session controls; password recovery and optional review editing are not implemented.

## Verification

See verification-notes.md for the checks actually performed. Unchecked browser and responsive conditions must not be presented as passed.
