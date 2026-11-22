# Evidence rules

This repo is a public portfolio. Everything in it runs in my own lab, built for
a fictional company. These rules apply to every commit, screenshot and doc.

## 1. Never publish

- Data, names, screenshots or configuration from any real organization
- Tenant, subscription, object or app IDs (including my lab's)
- Domain names, hostnames, internal URLs, IP addresses or device names
- Real people's names, usernames or email addresses
- Secrets of any kind: keys, passwords, connection strings, tokens, certificates
- Terraform state, plan files or real `.tfvars`

## 2. How identifiers are handled

- Lab accounts, devices and resources use the fictional company's names
  (see `docs/threat-model.md`).
- IDs come from variables or the pipeline, never from code. `example.tfvars`
  holds placeholders; real `.tfvars` files are git-ignored.
- Pipelines sign in with OIDC, so there are no client secrets to leak.
- App secrets live in Key Vault and are read through managed identity.

## 3. Case studies

Case studies drawn from professional experience are generalized, contain no
identifying details, show results only as percentages or before-and-after
changes, and are published only with permission.

## 4. Labels and honesty

- Every artifact is labeled **Lab**, **Simulated** or **Case study**.
- Lab results are never presented as production scale or impact.

## 5. Authorized testing only

Attack simulations run only against resources I own in my lab subscription.

## 6. Screenshots

- Lab accounts and the fictional company only.
- Crop to what proves the point; cover IDs and the address bar with solid
  boxes, not blur.
- Strip image metadata before committing.

## 7. What counts as evidence

Every detection ships with:

| Item | Where |
|---|---|
| Rule (KQL, ATT&CK technique, severity) | `detections/rules/<id>.yaml` |
| How to fire it, and the expected alert | `detections/tests/<id>.md` |
| Screenshot of the alert firing | `evidence/` |
| False-positive and tuning notes | `detections/tests/<id>.md` |
| Date last tested | `detections/tests/<id>.md` |

Posture work shows before-and-after results (secure score, policy compliance) with the date.

## 8. Enforcement

- GitHub secret scanning and push protection are on.
- A pre-commit hook runs gitleaks, plus a private blocklist of sensitive terms
  kept outside the repo.
- `main` is protected: changes land through pull requests with the checklist
  in `.github/pull_request_template.md`.

## 9. If something leaks

Revoke or rotate it first, then remove it from history and force-push.

## 10. Borrowed work

Queries or ideas adapted from others are credited in the file that uses them.
The repo is MIT licensed.
