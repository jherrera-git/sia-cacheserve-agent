# SIA/CacheServe Test Engineer Agent

A Copilot CLI custom agent for operating and certifying Akamai SIA and DNSi CacheServe/AMC-X labs over SSH. It encodes safety tiering (Pass 1/2/3), `nom-tell` quirks, packet-capture discipline, and a dual-deliverable reporting pattern.

## Install

Pick one:

| Scope | Location |
|---|---|
| This repo/team | Keep `sia-cacheserve-test-engineer.agent.md` in `.github/agents/` and clone the repo |
| Whole org | Put the file in `agents/` of the org's `.github-private` repo |
| Just you | Copy the file to `~/.copilot/agents/` |

## Use

1. Start the Copilot CLI (`copilot`) in the repo.
2. Run `/agent` and select **sia-cacheserve-test-engineer**.
3. The agent will ask for SSH details, docs, test checklist, host roles, scope, and report preferences. Supply your own lab values; none are stored in the agent.

## Templates

Starter files for the dual-artifact pattern are in [`templates/`](templates/):

- `runbook-template.md` — internal execution runbook (one per test category)
- `customer-report-template.md` — customer-facing report (convert with `pandoc file.md --toc --toc-depth=3 -o file.docx`)

## Contributing

Don't commit hostnames, IPs, credentials, or customer names. Propose improvements by pull request so learnings are reviewed before they reach the shared agent.
