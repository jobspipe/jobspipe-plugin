# JobsPipe for Claude

![JobsPipe](assets/logo.png)

Search live job postings from 30+ job boards and company career sites, and
detect the technologies a company runs on its domain.

This repository is the Claude plugin for JobsPipe. It bundles the hosted
JobsPipe MCP connector together with skills and slash commands that teach
Claude how to query it well. It contains no server code; the connector is
remote and hosted at `https://mcp.jobspipe.dev/mcp`.

## Install

From Claude's plugin directory: open **Customize > Plugins > Discover** on
claude.ai, or run `/plugin directory` in Claude Code, and add **JobsPipe**. A
plugin added on claude.ai also appears in your Claude Code sessions.

Or install straight from this repository, which is its own marketplace:

```
claude plugin marketplace add jobspipe/jobspipe-plugin
claude plugin install jobspipe@jobspipe
```

Inside a Claude Code session the same two steps are one command:

```
/plugin install jobspipe --marketplace jobspipe/jobspipe-plugin
```

## Setup

The connector is authenticated, so you need a JobsPipe account before the tools
return data. Sign up at [jobspipe.dev/signup](https://jobspipe.dev/signup); a
free account starts with 1,000 credits that never expire, and no card is
needed.

The first time Claude calls a JobsPipe tool it walks you through OAuth: you
sign in at jobspipe.dev and approve, and no credential is pasted into the
client. If you would rather use an API key, create one at
[jobspipe.dev/dashboard](https://jobspipe.dev/dashboard) and send it as an
`Authorization: Bearer` header. Both paths bill the same account and the same
credit balance.

## What it adds

**Tools**, from the connector. Searches and tech stack scans draw credits from
the connected account; the other tools are free to call.

| Tool | Purpose |
| --- | --- |
| `search` | Find postings from a plain-language request, best matches first |
| `fetch` | Read one posting in full by the id a `search` result returned |
| `search_jobs` | Filter open postings by title, company, description keyword, skills, country, seniority, employment type, remote status and freshness |
| `detect_company_tech_stack` | Report frameworks, CDNs, analytics, payments and SaaS widgets served on a domain, each with a confidence score |
| `search_documentation` | Look up filter names, accepted values and limits in the JobsPipe docs |
| `list_pricing_plans` | Current JobsPipe plans, credit allowances and per-request result limits |
| `get_account_info` | The connected account, its plan and remaining credits |
| `list_signals` | Saved searches on the connected account |
| `create_signal` | Save a search as a signal so new matches are delivered by email, Slack or webhook instead of polling |
| `upgrade_plan` | Return a checkout link for a larger credit package; it never charges anything itself |

Every tool is read-only except `create_signal`, which saves a search on your
own account, and `upgrade_plan`, which only returns a link.

**Commands:**

| Command | Purpose |
| --- | --- |
| `/jobspipe:find-jobs` | Search postings by role, skill, location or freshness |
| `/jobspipe:hiring-signal` | Profile a company from its open roles and its tech stack |
| `/jobspipe:tech-stack` | Detect the technologies a company serves on its domain |

**Skills:** `job-market-research` covers the real filter set and how to avoid
reporting stale postings as open. `hiring-signals` covers reading a company
from postings plus stack together. `jobspipe-setup` handles connecting and
diagnosing auth failures.

## Examples

```
/jobspipe:find-jobs remote backend engineers using Rust, posted in the last week
/jobspipe:hiring-signal stripe.com
/jobspipe:tech-stack vercel.com
```

## Privacy Policy

JobsPipe's privacy policy is at <https://jobspipe.dev/privacy>.

This plugin ships no telemetry of its own and runs nothing on your machine.
When you use it, your queries are sent to the JobsPipe API at
`mcp.jobspipe.dev` in order to return results, and searches are charged to
your account's credit balance. The connector returns employer and job posting
data only. It does not return personal contact information for individuals.

## Support

- Documentation: <https://docs.jobspipe.dev/ai-agents/connect>
- Contact: <https://jobspipe.dev/contact>
- Terms: <https://jobspipe.dev/terms>

## License

MIT. See [LICENSE](LICENSE).
