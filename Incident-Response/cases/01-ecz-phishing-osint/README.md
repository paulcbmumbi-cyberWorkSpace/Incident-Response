# Case 1: ECZ Phishing Attack (Real-World OSINT Case)

**Status:** Resolved · **Reported:** 2 Apr 2026 · **Confirmed:** 8 Sep 2026

A phishing site impersonating the Electoral Commission of Zambia's careers portal, aimed at citizens looking for government jobs.

## Summary
Starting from a real phishing email, I used passive OSINT to trace the site to a free GitHub Pages repository. I documented the evidence and reported it through three channels. GitHub Trust & Safety suspended the account and removed the repository.

## Timeline
| Date | Action |
|---|---|
| 2 Apr 2026 | Discovered the site, ran DNS resolution, inspected the repo |
| 2 Apr 2026 | Compiled the report; submitted to GitHub abuse form, support chat and abuse@github.com |
| 8 Sep 2026 | GitHub confirmed the account was suspended and the repo removed |

## Key findings
- The domain (`ecz-career[.]alloffer[.]org`) is a CNAME to a `kenblogme[.]github[.]io` Pages site, so the attacker's infrastructure sat behind GitHub's trusted CDN.
- The repo had 24 commits. Its files covered the full attack:
  - `CNAME` pointed the spoofed domain at the site.
  - `job.html` held fake job listings.
  - `staff.html` held a fake staff directory.
  - `offer.js` captured form data and sent it out.
- **Attack chain:** victim visits the site → sees ECZ branding and listings → submits credentials and personal data → `offer.js` sends it to the attacker.

## What I did
Evidence gathering, documentation, multi-channel reporting, and tracking through to closure, using passive OSINT only.

## Lessons learned
- Free, trusted hosting makes phishing harder for users to spot.
- Reporting through several channels creates a paper trail.
- The 5-month response time came from the platform, not the analysis. Future cases should include proactive follow-ups.

📄 [Full report (PDF)](report.pdf)
