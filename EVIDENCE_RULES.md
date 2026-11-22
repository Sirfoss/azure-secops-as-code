# Evidence rules

This repo is a public portfolio. Everything in it is either built in my own lab
or rewritten from work experience so that nothing identifies my employer, its
systems or its people. These rules apply to every commit, screenshot and doc.

## 1. Never publish

- My employer's name next to any technical detail, config or number
- Tenant IDs, subscription IDs, object IDs, app (client) IDs: work **or** lab
- Domain names, hostnames, internal URLs, IP addresses, device names
- Usernames, email addresses, display names or any real person's data
- Logs, sign-in records, alerts or exports from the work environment
- Screenshots taken in the work tenant
- Work policy names, ticket numbers, vendor or contract details
- Secrets of any kind: keys, passwords, connection strings, tokens, certificates
- Terraform state, plan files or real `.tfvars`

## 2. How identifiers are handled

- The lab belongs to a fictional company described in `docs/threat-model.md`.
  Lab accounts, devices and resources use that company's fictional names.
- Tenant and subscription IDs come from variables or the pipeline, never from code.
  `example.tfvars` holds placeholders; real `.tfvars` files are git-ignored.
- Pipelines sign in with OIDC. No client secrets exist to leak.
- App secrets live in Key Vault and are read through managed identity.

## 3. Work-derived material

- Work projects appear only as sanitized case studies in `docs/case-studies/`,
  labeled **Work (sanitized)**, describing the approach, not the environment.
- Numbers are shown as percentages or before/after changes, and only ones my
  manager has reviewed.
- My manager approves a work case study in writing before it is published.
- Scripts written for work are published only as a rewritten lab version that
  runs against the lab tenant (for example `scripts/graph-mfa-report/`).

## 4. Labels and honesty

- Every artifact is labeled **Lab**, **Simulated** or **Work (sanitized)**.
- Lab results are never described as production scale or production impact.
- Every title and claim matches my resume and LinkedIn.

## 5. Authorized testing only

- Attack simulations run only against resources I own in my lab subscription.
- No scanning, testing or tooling aimed at systems I don't own or am not authorized to test.

## 6. Screenshots

- Use lab accounts and the fictional company only.
- Crop to what proves the point. Cover the address bar, tenant switcher,
  account picker and any IDs with **solid boxes**, not blur.
- Strip image metadata before committing.
- Name files after what they prove: `evidence/d03-alert-fired.png`.

## 7. What counts as evidence

Every detection ships with:

| Item | Where |
|---|---|
| Rule (KQL, ATT&CK technique, severity) | `detections/rules/<id>.yaml` |
| How to fire it, and the expected alert | `detections/tests/<id>.md` |
| Screenshot of the alert firing | `evidence/` |
| False-positive and tuning notes | `detections/tests/<id>.md` |
| Date last tested | `detections/tests/<id>.md` |

Posture work shows before-and-after (secure score, policy compliance) with the date.

## 8. Enforcement

- GitHub secret scanning and push protection are on.
- A pre-commit hook runs gitleaks with this repo's rules **plus** a private
  blocklist kept outside the repo (my work domain, work tenant ID and
  internal names), so the sensitive values never appear in the repo itself.
- `main` is protected: changes land through pull requests that pass checks and
  the checklist in `.github/pull_request_template.md`.

## 9. If something leaks

1. Revoke or rotate the secret immediately. Removing the commit is not enough.
2. Remove it from history (`git filter-repo`) and force-push.
3. If it came from work, tell my manager the same day.
4. Write down what happened and which rule or check would have caught it.

## 10. Borrowed work

Queries or ideas adapted from others are credited in the file that uses them,
with a link. The repo is MIT licensed.
