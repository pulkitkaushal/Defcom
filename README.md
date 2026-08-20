# Defcom

**Defcom** is a lightweight browser-based decision-support tool for bug disposition from **Pre-DHB triage through Post-DHB review**.

Current version: **v1.5.1**

## What Defcom does

Defcom separates the defect decision into two stages:

### Pre-DHB
Determines whether a defect can be handled within the current release or should move to DHB.

The Pre-DHB decision uses:

- **Fix Readiness**
  - Root cause understood
  - Fix identified
  - Confidence in proposed fix
  - Regression risk
  - Verification complexity
- **Release Fit**
  - Level of effort
  - Release timeline impact
  - Release phase
- **Governance override**
  - Confirmed or potential Safety impact
  - Confirmed or potential Regulatory / Compliance impact

Possible outcomes:

- `FIX WITHIN RELEASE`
- `TAKE TO DHB`
- `REQUIRES FORMAL REVIEW`

### Post-DHB
Uses **Issue Impact × Change Risk** to generate a tool recommendation.

Issue Impact considers:

- Severity
- Customer impact
- Safety impact
- Regulatory / Compliance impact
- Workaround
- Occurrence / exposure

Change Risk considers:

- Level of effort
- Regression risk
- Release timeline impact
- Release phase

Possible recommendations:

- `FIX NOW`
- `FIX SOON`
- `FIX LATER`
- `ESCALATE`

## v1.2 changes

- Added **Summary of determination** to both Pre-DHB and Post-DHB results.
- Added an **Entered values** section so the assessment can be reviewed without returning to the form.
- Added automatic **Pre-DHB → Post-DHB field carryover** for shared criteria.
- Added translation of Pre-DHB timeline values into Post-DHB risk values:
  - None → Low
  - Manageable → Medium
  - Significant → High
- Improved POPM override summaries so they read as concise decision rationale rather than a count of Yes/No responses.
- Preserved the prior override log when a Post-DHB assessment is rerun.
- Added `ESCALATE` as an available final POPM disposition.
- Help modal contains separate **Pre-DHB scoring/determination** and **Post-DHB scoring** tabs.
- Safety or Regulatory/Compliance governance rules remain explicit and auditable.
- Existing browser history remains stored in `localStorage`.

## Decision transparency

Defcom intentionally separates:

- **Tool recommendation**
- **Final POPM disposition**
- **Override rationale**
- **Override history**

The original recommendation remains unchanged when a POPM override is recorded.

## Data storage

This prototype stores assessment history in the browser using `localStorage`.

This means:

- Data stays on the local browser/device.
- Clearing browser storage can remove saved history.
- Different users or devices do not share history.
- This is not yet a centralized audit database.

## Run locally

No build tools are required.

Open:

`defcom_v1.2.html`

in any modern browser.

## GitHub Pages hosting

For GitHub Pages, the easiest setup is:

1. Put the HTML file in the repository.
2. Rename the production file to `index.html`.
3. Commit and push it to the branch used by GitHub Pages.
4. In **Settings → Pages**, deploy from that branch/folder or use a GitHub Actions Pages workflow.

You do **not** need to manually upload the HTML through the GitHub website every time. Once the repository is cloned locally, you can update the file and use normal Git commands:

```bash
git add .
git commit -m "Update Defcom"
git push
```

GitHub Pages will publish the updated version automatically after the push.

## Other hosting options

Defcom is currently a static single-file web app, so it can also be hosted on:

- Netlify
- Vercel
- Cloudflare Pages
- Azure Static Web Apps
- AWS S3 / CloudFront
- Any standard web server

Most of these services can connect directly to the GitHub repository and automatically redeploy whenever changes are pushed.

## Current architecture

- HTML
- CSS
- Vanilla JavaScript
- Browser `localStorage`
- No backend
- No build process
- No external dependencies

## Future options

Potential future enhancements include:

- Jira integration / MCP-backed bug lookup
- Centralized shared history instead of browser-local storage
- Authentication / role-based access
- Exportable assessment reports
- Release-level dashboards
- Analytics across defect dispositions

## Governance note

Defcom is a decision-support tool. Final disposition remains subject to the applicable organizational, quality, safety, regulatory, and release-governance processes.
