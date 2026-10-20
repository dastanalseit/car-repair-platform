# Website interface prototype

AutoSenim is a provisional interface name; the diploma title remains unchanged. The prototype now includes Russian and Kazakh interfaces, a yellow-and-graphite theme, an inline vehicle illustration and a search reset control.

## Open the prototype

- [Russian interface](ru.html)
- [Kazakh interface](kk.html); `index.html` also opens the Kazakh version in this repository.
- [Hosted preview on Sites](https://autosenim-dastan-prototype.magic-coin-2293.chatgpt.site) — private, owner-only access. This is not a public committee-access link. The hosted entry page defaults to Russian.

Download the repository ZIP or clone this branch, then open `docs/prototype/ru.html` in a browser. Keep `index.html`, `ru.html`, `kk.html` and `theme.css` together in the same folder. GitHub's file view displays source rather than running the interface. No installation, build step or external assets are required.

Alternatively, from the repository root run:

```sh
python3 -m http.server 8768 --bind 127.0.0.1
```

Open `http://127.0.0.1:8768/docs/prototype/ru.html`. Stop the local server with Ctrl+C when finished.

The language links load a separate page and reset demonstration state. These are prototype language options; the final production language scope remains to be agreed.

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

The visual refresh and Russian translation have not undergone browser scenario or responsive testing. Earlier notes are historical and do not establish validation of this revision. See [verification-notes.md](verification-notes.md) for prior review notes. Unchecked browser and responsive conditions must not be presented as passed.
