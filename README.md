# PRECISION FS AUTOS — GitHub + Vercel website

Professional body repairs for motorists and independent dealers, plus a dedicated
commercial fleet repair service in Bolton. Mobile-responsive static site with a
Vercel Serverless Function for enquiry emails.

## Business details used

- PRECISION FS AUTOS
- Unit 5, St Bartholomew Building, Off Nelson Street, Bolton, Greater Manchester, UK, **BL3 2AH**
- **contact@precisionfsautos.co.uk** (ASSUMPTION: based on the previously supplied `contact@` local part)
- Proposed domain: `precisionfsautos.co.uk` — verify that you control it before connecting.

## Pages

- `index.html` — general services and fleet call-to-action
- `services.html` — accident repair, panels, scuffs, paintwork, dealer work
- `ev-repairs.html` — conditional EV/hybrid body repair enquiries and safety
- `fleet.html` — couriers, depot operators, rental businesses, fleets
- `our-work.html` — process; illustrated placeholders until genuine photos supplied
- `contact.html` — enquiry form; standard and fleet-related fields
- `privacy.html`, `thank-you.html`, `404.html`
- `api/contact.js` — Vercel Function that calls Resend's transactional email API

## Deploy via GitHub and Vercel

1. Unzip this folder and create a **new GitHub repository** (e.g. `precision-fs-autos`).
2. Upload **the contents of this folder to the repository root**, including `index.html`, `api/`, `vercel.json` and `package.json`.
   Do not upload an additional enclosing folder unless that is the Vercel Root Directory.
3. In Vercel choose **Add New → Project → Import Git Repository** and select the GitHub repo.
4. Framework Preset: **Other**. Keep the root directory set to the repo root. No build command or output directory is needed for this static project.
5. Deploy. Vercel publishes the HTML/CSS/JS pages and automatically serves `api/contact.js` at `/api/contact`.
6. In Vercel Project → Settings → Domains, add `precisionfsautos.co.uk` (and `www.precisionfsautos.co.uk` if desired). Follow Vercel's displayed DNS record instructions with your DNS provider. **Do not assume the domain has been connected already.**
7. Configure the mail service as below, redeploy and test the form.
8. Open a new Incognito browser session and check mobile navigation, all page links, form errors and a real email reaching your inbox.

Every GitHub push to the production branch can trigger a new Vercel deployment; pull requests produce previews (subject to Vercel project settings).

## Set up email enquiries — REQUIRED BEFORE FORM WORKS

The website does NOT rely on PHP or GoDaddy hosting. It also does not
pretend a message was delivered if the email integration is incomplete.

1. Create an account at **Resend** (https://resend.com) and verify the sending domain you control, e.g. `precisionfsautos.co.uk`. Configure the DNS records Resend provides.
2. Verify that **contact@precisionfsautos.co.uk** is an existing, monitored mailbox.
3. In Vercel → Project → Settings → Environment Variables, set:
   - `RESEND_API_KEY` — your Resend key (NEVER commit it to Git)
   - `CONTACT_FROM_EMAIL` — a sender on your **verified** domain, e.g. `enquiries@precisionfsautos.co.uk`
   - `CONTACT_TO_EMAIL` — `contact@precisionfsautos.co.uk`
4. Redeploy after saving variables; send a test enquiry and confirm it appears in your inbox.
5. Configure your email host's SPF, DKIM and DMARC records properly. Domain verification and mailboxes are independent services.

Without these variables, users see a clear error message with a direct email alternative.
The form does not upload photographs: customers can email photos directly.
The current server-side abuse protection is basic (honeypot, length/type validation).
Before high-volume paid traffic, add managed anti-bot/rate-limit protection.

## Edit website content

- All branding/contact details: search the repository for `PRECISION FS AUTOS` and `contact@precisionfsautos.co.uk`.
- Styles: `assets/css/styles.css`.
- Enquiry labels/options: `contact.html` and `api/contact.js` service whitelist.
- Website copy: each top-level `.html` page.
- Illustrations: `assets/img/*.svg` are diagrams/illustrations, **not photos of completed jobs**.
- Add genuine workshop photographs only with suitable permission, especially for registration plates.

## Confirm before publishing

- The **email local part** (`contact@`) was inferred, not independently confirmed by the user.
- No telephone number or business opening hours were supplied; none are invented.
- Confirm workshop capacity for large vans and the competence/equipment needed for EV/hybrid damage assessments.
- No Amazon/insurer/manufacturer/BS 10125 approval is claimed.
- Review the privacy notice against actual retention, hosting, and email practice. Update if analytics, cookies or advertising are added.
- Only use illustrations and genuine permitted images, not simulated customer case studies.

## Local preview / tests

Run `python -m http.server 8000` from this folder, then visit
`http://localhost:8000`. The forms require Vercel's serverless runtime and
won't send in a static local preview.

Run `npm test` to execute basic function tests (no third-party dependencies).

## References

- Vercel Git deployments: https://vercel.com/docs/git
- Vercel Node.js Functions: https://vercel.com/docs/functions/runtimes/node-js
- Resend email API: https://resend.com/docs/api-reference/emails/send-email

Generated 13 October 2026.
