## 1.5.2

dev into master

This PR brings `dev` into `master`. It is the 1.5.2 release: one release-blocker fix, one correctness sweep, plus gate hardening and docs.

**The 1.5.2 fix: the packed Customer backend could crash at boot on real machines.** The dest-minify step packed the backend into a single executable that hit a class of crashes on real installs, and the bundled MySQL extract could fail silently, leaving a half-extracted engine. The packer now produces a bootable artifact, and a failed extract fails loudly instead of limping on. The product version bumps to 1.5.2.

**"Today" is now the Nest server's calendar day, everywhere it is compared.** MySQL `CURDATE()` reads the database server's clock, which does not match the clock that stamps the invoice date — that mismatch made the previous-invoice navigation intermittently wrong near midnight. Every "today" comparison now binds the app-local calendar day (`getLocalDateString()`) as a parameter: the sale and money neighbor walks, the dashboard counters, reminders, the expiry countdown, competitor analysis and intelligence, and the purchase planner. Date storage is unchanged — strings are stored verbatim; only comparisons and the userless stamps changed. The same class of defect was fixed on the write paths: competitor invoices fell back to the UTC calendar day, sale quotes stored an unvalidated `invoice_date` (an absent date stored the literal `undefined`), and the invoice date formatter shifted a day for timezones west of UTC. The ruling ("today" = the Nest server's calendar day) is recorded in `docs/project_context.md`.

**The golden-flow pre-promote gate was made less flaky.** The manufacture daily-table assertion now polls past in-flight reloads; the permission-flags previous-invoice and cashier previous-invoice assertions tolerate the neighbor-navigation refusal toast (`لا توجد فاتورة سابقة` is an accepted refusal outcome); assertions are unchanged — poll semantics only.

**Docs and skills.** The PR-body rule is descriptive prose — what and why, not a list of commit subjects. The release flow is documented, and the five frontend skills are wired into the flow skills that govern frontend_tauri work.

No schema changes and no customer-facing UI behavior changes in this range.

## 1.5.1

dev into master

Bump product SemVer to 1.5.1.

## 0.1.1

Promote dev into master

## Summary

- Bring current `dev` into `master`.
- Retire Catalog confirm. The اشتراكي page stays a local status view, and confirm goes through the newer subscription steps.
- Enforce one licensed-device claim before a license file is written. Cloud trials use the 30-day constant, and an owner subscription type is refused before the file is sealed.
- Unwrap a sealed client license on Nest disk reads, accept the website Firebase ID token on desktop Google sign-in, reject a Remote support host that contains `%`, and drop the Support user when the four-hour cap elapses.

## Test plan

- [ ] Confirm a subscription from the newer steps on a machine whose client license is sealed under AppData.
- [ ] Activate a second device on a one-device subscription and confirm it is rejected.
- [ ] Sign in with Google from the desktop handoff and confirm the same account still works on the website.
- [ ] Open Break-glass on a Remote database and confirm a host containing `%` is refused, and that the Support user is dropped at four hours without the dialog staying open.
- [ ] Issue a cloud trial and confirm the end date is 30 days.

# storify-releases
Public Customer package Update feed host (NSIS setup.exe, .sig, latest.json). No product source.
