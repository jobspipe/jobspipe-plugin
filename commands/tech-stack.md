---
description: Detect the technologies a company serves on its domain
---

Detect the tech stack for: $ARGUMENTS

Call `detect_company_tech_stack` with the domain. URLs and a leading `www.` are
normalized for you, so `https://www.stripe.com/pricing` and `stripe.com` are
the same input.

Group the findings by category - frameworks, CDN and hosting, analytics,
payments, and other SaaS widgets - and give the confidence for each. Call out
low-confidence detections as hints rather than facts.

Note that the scan sees only what the domain serves to an anonymous visitor.
Anything server-side or behind a login will not appear, so absence is not
evidence that a technology is unused. Results may come from a 14-day cache.
