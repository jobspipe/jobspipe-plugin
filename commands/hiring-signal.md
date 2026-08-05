---
description: Profile what a company is investing in, from its open roles and its tech stack
---

Research this company: $ARGUMENTS

Build a picture from public evidence:

1. Call `search_jobs` with `company_name_or` set to the company, bounded by
   `posted_at_max_age_days: 90`, to see where headcount is going.
2. Call `detect_company_tech_stack` on the company's domain to see what is
   already built.

Then report:

- **Where they are investing** - the breakdown of open roles by function, and
  what the mix implies about their stage
- **What they run** - notable technologies, with confidence noted for weak
  detections
- **Tensions worth flagging** - a stack that disagrees with the job
  descriptions usually means a migration in progress

State the date window you used. Draw only on what the tools returned, and say
so plainly when a section has no evidence behind it.
