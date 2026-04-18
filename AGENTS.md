<!--
This file is for students using OpenAI's Codex CLI instead of (or alongside)
Claude Code. The MOOC is taught with Claude Code, but the patterns in this
repo work with any agentic CLI that reads a project context file.
-->

# AGENTS.md

This repo works with OpenAI Codex CLI too.

Codex reads `AGENTS.md` the same way Claude Code reads `CLAUDE.md`. If you
want to use Codex on this repo, you have two options:

1. Symlink it: `ln -s CLAUDE.md AGENTS.md` (then delete this file)
2. Copy it: keep both files in sync by hand

Either works. The symlink is less effort. The copy lets you keep two
slightly different briefings if you want one tone for Claude and another
for Codex.

## One-shot runs

Codex supports a `-p` flag for non-interactive prompts, the same way
Claude Code does:

```
codex exec -p "draft a short brief from the docs in sample-docs/"
```

That's the pattern Module 4 uses for cross-model review — fire the same
prompt at Claude, Codex, and Copilot CLI in parallel and compare what
each one catches.

## Worked example

See `examples/worked-claude-md/CLAUDE.md` for a fully filled-in context
file. The same content drops into `AGENTS.md` without changes.

## More

- Course site: https://mooc.amditis.tech
- Cross-model review walkthrough: `docs/cross-model-review.md`

## Beat

I cover information technology for small and medium-sized businesses in Tampa, Florida. My primary focus is cloud adoption, cybersecurity, governance, risk, and compliance, automation, IT cost control, and practical implementation for lean teams. I write for SMB owners, IT managers and directors, and managed service providers serving the Tampa Bay region.

Key people and institutions:
- SMB owners, IT managers, IT directors, and operations leaders across Tampa Bay companies with lean budgets and small internal IT teams
- Managed service providers, virtual chief information officers, security consultants, and cloud partners serving small and midsize organizations in Tampa, St. Petersburg, and Clearwater
- Regional business groups, chambers of commerce, economic development organizations, and local technology associations that track SMB conditions, adoption trends, and hiring
- Regulators, standards bodies, and major vendors relevant to SMB IT, including the National Institute of Standards and Technology, the International Organization for Standardization, Amazon Web Services, Microsoft Azure, Google Cloud Platform, and Microsoft 365 vendors and partners

## Style

- AP style for all writing
- Use the Oxford comma
- Spell out numbers under 10 unless AP style calls for numerals
- Dollar amounts: $2.3 million, not $2,300,000
- Default to concise outputs and plain English
- Define acronyms on first reference, including SMB, MSP, SaaS, PaaS, IaaS, IAM, GRC, CapEx, and OpEx
- Use "the company" on second reference for businesses
- Avoid vendor hype, marketing language, and unqualified claims about transformation, innovation, or seamless adoption
- Prioritize actionable guidance, implementation steps, trade-offs, and cost implications
- When writing about Tampa or Tampa Bay businesses, be geographically precise and distinguish Tampa from the broader region when it matters

## Source standards

- Attribute all claims to named sources unless the information comes from a document, filing, benchmark, or official dataset that can be cited directly
- Flag unverified claims separately from verified ones
- If a source makes a factual claim about pricing, savings, incident counts, compliance status, staffing, or deployment timelines, note whether it can be verified independently
- Do not rely on vendor press releases alone for claims about return on investment, security effectiveness, or market adoption
- Cross-check security and compliance claims against primary sources such as official documentation, filings, audit reports, standards, or direct customer evidence when available
- For breach, outage, ransomware, or fraud claims, distinguish confirmed facts from early statements, and include what is still unknown
- Do not grant anonymity without a clear reason, and explain the source's role as specifically as possible without exposing identity
- Treat product roadmaps, launch dates, pricing, and feature availability as time-sensitive and verify them before publication

## Terminology

- Distinguish software as a service, platform as a service, and infrastructure as a service; do not use "cloud" as a vague catchall when a more precise term fits
- Distinguish governance, risk, and compliance; they are related but not interchangeable
- Distinguish hybrid cloud from multi-cloud
- Distinguish identity and access management from zero trust; zero trust is a security model, not a product
- Distinguish operating expense from capital expense when writing about IT budgeting
- Use ransomware, phishing, business email compromise, endpoint detection and response, and multifactor authentication precisely
- Use Microsoft 365, not Office 365, unless a source is referring to an older product name
- For SMB coverage, "implementation" means real deployment, staffing, integration, user training, and maintenance, not just product purchase

## Avoid

- Avoid buzzwords such as "game-changing," "revolutionary," "seamless," "robust," and "cutting-edge"
- Do not write "experts say" or "officials say" without naming the source
- Do not present vendor case studies as neutral evidence
- Avoid implying that a tool is simple, cheap, or easy to deploy without evidence from actual SMB use
- Do not collapse Tampa, Tampa Bay, and Florida into one geography when the distinction matters
- Avoid overstating compliance by implying that buying a product equals meeting a standard
- Avoid vague references to artificial intelligence, automation, or the cloud when the specific technology, workflow, or business impact can be named
- Do not frame SMB constraints as failures; explain budget, staffing, and operational trade-offs clearly

## Lessons learned

- Always define whether "small business" means employee count, revenue band, or both if the distinction matters to the story
- Always separate vendor claims from independently verified outcomes
- Never assume a Florida or Tampa business faces the same regulatory exposure as a national enterprise; specify the relevant rules and scope
- When covering cybersecurity incidents, state what happened, what evidence supports it, and what remains unconfirmed
- When discussing cloud costs, include the trade-off between direct savings, labor needs, and ongoing management overhead
