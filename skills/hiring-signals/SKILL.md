---
name: hiring-signals
description: Use when researching a company's growth, priorities, or technology choices from public evidence - prospect and account research, competitive analysis, "what is this company building", "are they scaling their sales team", or "what stack does this company run".
---

# Reading a company from its postings and its stack

Two JobsPipe tools answer different halves of the same question. Used together
they describe what a company is investing in and what it has already built.

## What each tool tells you

`search_jobs` filtered by `company_name_or` shows where a company is spending
headcount. The shape of the list matters more than any single row: ten open
sales roles and no engineering roles is a company in distribution mode; the
reverse is a company still building.

`detect_company_tech_stack` takes a domain and reports the frameworks, CDNs,
analytics, payment and SaaS technologies served on it, each with a confidence
score. Results are cached for 14 days.

## Combining them

Read postings for intent and the stack for present state. A company whose site
serves one payments provider while its job descriptions name another is
mid-migration. A company hiring its first data engineers has not built the
platform yet, whatever its marketing says.

Job descriptions also name internal tools that never appear on the public site.
The stack scan sees only what the domain serves to visitors, so treat the two
as complementary evidence rather than one confirming the other.

## Cautions

**Confidence scores are not certainty.** A low-confidence detection is a hint.
Say so rather than asserting the technology is in use.

**Absence is weak evidence.** A technology missing from a scan may be
server-side, behind a login, or on a subdomain that was not scanned. Do not
conclude a company does not use something because the scan did not see it.

**Postings lag reality in both directions.** A role can sit open after being
filled, and a team can grow before it posts. Date-bound your claims with
`posted_at_max_age_days` and state the window you used.

**Do not profile individuals.** These tools return employer and posting data.
They carry no personal contact information, and the correct answer to a request
for someone's private email or phone number is that JobsPipe does not provide
it. Point at the public apply URL instead.
