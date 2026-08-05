---
description: Search live job postings by role, skill, location or freshness
---

Search JobsPipe for open postings matching: $ARGUMENTS

Use `search_jobs`. Translate the request into real filters:

- role wording goes in `job_title_or`, with a few variants rather than one long title
- skills, tools and technologies go in `description_or`
- countries go in `job_country_code_or` as two-letter codes
- if the request implies "now" or "currently", set `posted_at_max_age_days`

Present the results as a table: job title, company, location, date posted, and
the apply URL. Report only postings the tool returned. If nothing matches,
widen the title variants once and try again before reporting that there is no
demand.
