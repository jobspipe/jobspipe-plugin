---
name: job-market-research
description: Use when searching for open job postings, researching hiring demand for a role or skill, comparing job markets across countries, or answering questions like "who is hiring for X", "find me remote Y jobs", or "how many companies are posting Z roles".
---

# Researching the job market with JobsPipe

`search_jobs` queries live postings collected from 30+ job boards and company
career sites, normalized into one schema. It is read-only.

## Filters that actually exist

Do not invent parameters. The tool accepts exactly these:

| Filter | Use |
| --- | --- |
| `job_title_or` | Match any of several titles. Prefer several short variants over one long title |
| `job_title_not` | Exclude titles, e.g. drop "Senior" when looking for junior roles |
| `description_or` | Match words in the posting body. This is where skills and tools live |
| `company_name_or` | Restrict to named employers |
| `job_country_code_or` | Two-letter codes, e.g. `["DE","NL"]` |
| `job_location_or` | Free-text city or region |
| `employment_type_or` | Full-time, contract, and so on |
| `job_seniority_or` | Seniority bands |
| `include_unlabeled_seniority` | Include postings whose seniority could not be classified |
| `skills_or` | Match extracted skills |
| `occupation_code_or`, `isic_division_or` | Standard occupation and industry codes |
| `remote` | Boolean |
| `posted_at_gte`, `posted_at_max_age_days` | Freshness |
| `limit`, `offset`, `include_total_results` | Paging |

All filters are optional and combine with AND. Values inside one `_or` filter
combine with OR.

## Getting good results

**Search titles and descriptions differently.** A title filter finds the role;
a description filter finds the requirement. "Backend engineers who use Rust" is
`job_title_or: ["backend engineer"]` plus `description_or: ["rust"]`, not a
single title string.

**Always bound freshness for "now" questions.** Job boards keep stale postings
around. When the user says "currently", "right now", or "this week", set
`posted_at_max_age_days`. Without it you will report roles that closed months
ago as if they were open.

**Widen titles before concluding nothing exists.** Employers name the same job
many ways. Zero results for "Staff Backend Engineer" often means the posting
says "Senior Software Engineer, Platform". Retry with broader variants before
telling the user there is no demand.

**Check `include_total_results` for counting questions.** If the user asks how
many, ask the API for the count instead of counting the rows you happened to
fetch, which is capped by `limit`.

## Reporting rules

Report only what the tool returned. If `data` is empty, say so plainly. Never
supplement with what you know about a company's hiring from training data, and
never estimate a salary the posting did not state. Link users to the returned
apply URL rather than describing how to find the posting.

When results are truncated by `limit`, say so, rather than presenting a partial
list as the complete picture.
