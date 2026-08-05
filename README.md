# JobsPipe for Claude

Search live job postings from 30+ job boards and company career sites, and
detect the technologies a company runs on its domain.

This repository is the Claude plugin for JobsPipe. It bundles the hosted
JobsPipe MCP connector together with skills and slash commands that teach
Claude how to query it well. It contains no server code; the connector is
remote and hosted at `https://mcp.jobspipe.dev/mcp`.

## Install

From the official Anthropic marketplace in Claude Code:

```
/plugin install jobspipe
```

Or add this repository as a marketplace directly:

```
/plugin marketplace add jobspipe/jobspipe-plugin
```

## Setup

The connector is authenticated, so you need a JobsPipe account before the tools
return data. Sign up at [jobspipe.dev](https://jobspipe.dev); the free plan
includes 100 requests per month.

The first time Claude calls a JobsPipe tool it walks you through OAuth: you
sign in at jobspipe.dev and approve, and no credential is pasted into the
client. If you would rather use an API key, create one at
[jobspipe.dev/dashboard](https://jobspipe.dev/dashboard) and send it as an
`Authorization: Bearer` header. Both paths bill the same account and the same
plan quota.

## What it adds

**Tools** (from the connector, all read-only):

| Tool | Purpose |
| --- | --- |
| `search_jobs` | Filter open postings by title, company, description keyword, skills, country, seniority, employment type, remote status and freshness |
| `detect_company_tech_stack` | Report frameworks, CDNs, analytics, payments and SaaS widgets served on a domain, each with a confidence score |
| `list_pricing_plans` | Current JobsPipe plan prices, request quotas and per-request result limits |

**Commands:**

| Command | Purpose |
| --- | --- |
| `/find-jobs` | Search postings by role, skill, location or freshness |
| `/hiring-signal` | Profile a company from its open roles and its tech stack |
| `/tech-stack` | Detect the technologies a company serves on its domain |

**Skills:** `job-market-research` covers the real filter set and how to avoid
reporting stale postings as open. `hiring-signals` covers reading a company
from postings plus stack together. `jobspipe-setup` handles connecting and
diagnosing auth failures.

## Examples

```
/find-jobs remote backend engineers using Rust, posted in the last week
/hiring-signal stripe.com
/tech-stack vercel.com
```

## Privacy Policy

JobsPipe's privacy policy is at <https://jobspipe.dev/privacy>.

This plugin ships no telemetry of its own. When you use it, your queries are
sent to the JobsPipe API at `mcp.jobspipe.dev` in order to return results, and
requests are counted against your account's monthly quota. The connector
returns employer and job posting data only. It does not return personal contact
information for individuals, and it makes no writes: every tool is annotated
`readOnlyHint: true`.

## Support

- Documentation: <https://jobspipe.dev>
- Contact: <https://jobspipe.dev/contact>
- Terms: <https://jobspipe.dev/terms>

## License

MIT. See [LICENSE](LICENSE).
