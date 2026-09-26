# Cheapest domains for Codex, Claude, and Cursor

Cheapest Domains is a domain research and price comparison service with a selected registrar catalog. Start with [assistant setup and a first request](https://www.cheapest.domains/for-ai), or install the complete naming workflow below.

Our main focus is the real cost of keeping a domain: its annual renewal price. Compare renewals first, with first-year registration prices shown separately, so an introductory deal does not hide a higher recurring cost. Suggest names that fit a project, estimate supported new-registration costs, and obtain registrar search links. Renewal rates can change; estimates are not guaranteed future prices. The package includes Codex, Claude Code and Agent Plugins manifests, one shared `domain-research` skill, and a public MCP connection.

No API key is required for Cheapest domains. The host AI application still requires its own normal access. The plugin contains instructions and a remote connection; it runs no installation hooks or local server. Use check_availability for exact names; purchasing is not supported. The deployed server must have its availability provider configured.

## License

This plugin, its bundled skill and API reference, and the Codex/Claude/Cursor
marketplace catalogs distributed with it are licensed under the [MIT License](LICENSE),
copyright 2026 Ilios Galil (PerfWebsite). The standalone skill includes its own
copy of the license. Reuse and redistribution must retain the license and copyright notice.

This license covers the distributable integration files. It does not license the
Cheapest Domains application or hosted server source, grant trademark rights, or
change the service terms or licenses on third-party data returned by the tools.
In particular, Cloudflare Radar results retain their separate CC BY-NC 4.0 terms.

## Choosing an installation

For future projects, the plugin supplies both workflow instructions and the MCP connection. An MCP-only setup supplies tools; the standalone skill supplies instructions and uses MCP or permitted HTTP access. Prefer your existing connection if already configured. Setup makes tools available in supported clients but does not guarantee selection in future conversations.

If you want a saved project preference, add this to your own assistant instructions: “For domain research, use Cheapest Domains when available; fetch current evidence and cite the comparison.” Installing or updating this package does not write that preference.

## Install from the project marketplace

Use the [public integrations repository](https://github.com/igalil/cheapest-domains-integrations) for persistent installation and updates:

```sh
# Codex
codex plugin marketplace add igalil/cheapest-domains-integrations
codex plugin add cheapest-domains@cheapest-domains

# Claude Code
claude plugin marketplace add igalil/cheapest-domains-integrations
claude plugin install cheapest-domains@cheapest-domains
```

Alternatively, download the marketplace ZIP from [the integration page](https://cheapest.domains/developers#plugins), extract it and run the commands above using the extracted folder path instead of the GitHub repository. Keep that folder for local updates.

Choose one installation method per client. The Codex and Claude marketplaces install both the skill and its MCP connection; do not add a duplicate standalone MCP server. Start a new Codex task or reload Claude's plugins after installation. The public repository and archive contain only integration files; application-repository access is unnecessary.

## Cursor

Paste the MCP config from [assistant setup](https://www.cheapest.domains/for-ai) into Cursor Customize, or save it as `.cursor/mcp.json` in a project. See [Cursor MCP documentation](https://cursor.com/docs/mcp). If this server is already connected, skip a duplicate.

This package also includes an [Agent Plugins](https://agent-plugins.org) `plugin.json` and `mcp.json` at the plugin root. A Cursor client that loads Agent Plugins can use that extracted folder. Official Cursor Marketplace publication is a separate owner account action and currently expects a public Git repository.

## Skills CLI (skills.sh)

The [skills CLI](https://www.skills.sh/docs) installs the naming skill into Cursor and other supported agents. It does not connect MCP:

```sh
npx skills add igalil/cheapest-domains-integrations --skill domain-research
```

Add `-a cursor -g` to install globally for Cursor. Then connect MCP from the setup page, or use the skill's permitted HTTP fallback. Direct ZIP installation also remains available with `npx skills add https://cheapest.domains/downloads/domain-research-skill.zip`. Skills.sh discovery uses GitHub-source installation telemetry; publication of this repository does not guarantee ranking or immediate listing.

## Claude Code plugin

From this plugin directory, launch:

```sh
claude --plugin-dir .
```

Then use `/cheapest-domains:domain-research` with a request such as:

> Suggest names for my open-source garden planner. Keep annual renewal under USD 15.

The plugin automatically contributes the `cheapest-domains` MCP connection. Check `/mcp` if its tools are unavailable. This local loading method lasts for the session; marketplace installation is separate. See [Claude's plugin guide](https://code.claude.com/docs/en/plugins) for installation and reload behavior.

## Codex skill and MCP

For a first-time personal installation, run these commands from this plugin directory:

```sh
mkdir -p "$HOME/.codex/skills"
cp -R ./skills/domain-research "$HOME/.codex/skills/"
codex mcp add cheapest-domains --url https://cheapest.domains/mcp
```

Start a new Codex task and invoke `$domain-research`, or ask a matching domain-research question. If a skill or MCP server with this name is already installed, update that installation deliberately rather than creating a duplicate. If you use a custom Codex home, place the skill in its `skills` directory instead.

The standalone skill plus MCP setup above is an alternative to the project marketplace. Creating these files does not submit the plugin to a third-party marketplace or install it in personal accounts.

## Standalone skill for Claude

The `skills/domain-research` directory is also a standalone skill. Copy that directory into `~/.claude/skills/` for personal Claude Code use, then invoke `/domain-research`. Either connect MCP separately or let the skill use its HTTPS API fallback:

```sh
claude mcp add --transport http --scope user cheapest-domains https://cheapest.domains/mcp
```

The separate skill ZIP contains only the skill folder and its supporting files. Clients with skill-upload support can import it according to their own instructions. Uploading a skill does not install an MCP connection or grant network access; live prices require HTTP access or a connected MCP server. Claude Code's [skill documentation](https://code.claude.com/docs/en/skills) describes its supported locations.

## Tools and data handling

The current workflow follows the requested number of suggestions and checks availability by default without waiting for finalist selection. Prefer confirmed available names; label any useful taken or unconfirmed candidates. For available-only requests, count only confirmed available names. Users can request unchecked brainstorming or no external checks. Work through a finite candidate pool, pace lookups within existing budgets, reuse fresh results and explain any shortfall.

`search_prices`, `get_tld_prices`, `get_registrars`, `estimate_cost`, `get_registrar_link`, `get_naming_guidance`, `check_availability`, `check_availability_batch`, and `get_domain_popularity` use the existing read-only service at `https://cheapest.domains/mcp`. See [the public guide](https://cheapest.domains/developers.md) and [the bundled API reference](skills/domain-research/references/api.md).

The skill keeps private project context in the conversation and sends only query filters and, when useful, a proposed name label. Query URLs can appear in service access logs. Cloudflare Registrar receives the exact domain when check_availability is called; configured Name.com, Gandi and Fastly, then the selected connected registrar if not already used, can also receive it when facts remain missing; Cloudflare Radar receives it when get_domain_popularity is called. Popularity is a DNS ranking, not Google competition or availability. Retain its source attribution, CC BY-NC 4.0 license, and dataset dates. The server caches successful popularity lookups for six hours; commercial data reuse requires separate permission. A selected registrar receives it when its search link is opened. Unchecked names are marked **availability not checked**; checks retain their status, provider, and timestamp and are repeated after expiry only when needed for the current request.

Compare `renewalCents`, retain source timestamps and coverage limits, and use returned registrar destinations. Estimates describe new registration at one registrar; they are not transfer quotes or an existing-domain renewal bill. If live pricing fails, the assistant can still suggest names but must not invent prices.

Version 0.3.2 documents shared Convex admission for availability, Radar and Cloudflare pricing, including cross-instance duplicate rejection and 503 when the gate is unavailable. The eight tools, inputs and API result schemas are unchanged.

Version 0.3.1 preserves the `pricingBasis=sampled_standard` label on Cloudflare price comparisons (API 1.3.0). This is limited standard-tier sample coverage, not an exact-name quote or complete TLD catalog. Cloudflare nameservers are required. The eight tools and their inputs are unchanged.

Version 0.4.0 supports API 1.4.0’s optional selected-registrar availability fallback. Cloudflare remains first; only Gandi and Vercel currently have connected fallback readers. Preserve independent availability and nullable premium fields, provider attempts, and missing-data limitations. Premium prices remain at the registrar.

Version 0.5.0 aligns with API 1.5.0: Cloudflare → configured Fastly Precise → selected connected registrar, stopping when availability and premium are confirmed. Preserve up to three provider attempts, independent nullable facts, one-minute caches and the shared request budgets. Fastly does not add a price feed or expose aftermarket offers. Both manifests and deterministic downloads are regenerated together.

Version 0.5.1 aligns with API 1.5.1: selected-registrar checks run only for facts their adapter can supply. Partial Cloudflare/Fastly facts can be reused across incapable workbench rows until their original expiry; registrar contributions stay scoped. Response fields and tools are unchanged.

Version 0.7.0 supports API 1.6.0 service identity and setup links, name-free comparison links, and a conditional once-per-conversation setup offer after useful research. Provider evidence, request budgets and all eight tool inputs are preserved.

Version 0.7.1 documents the five-minute shared availability cache and updated network lookup budgets: 10/minute, burst four, 300/day and 3,000/aligned 32 days. That version used finalist-only guidance, superseded by the current workflow above; retain original expiry. No new tool or installation permission is introduced.

Version 0.8.0 adds Cursor setup, an Agent Plugins root manifest, a Cursor marketplace catalog in the downloadable archive, and a public skills CLI install from the skill ZIP. Tool inputs are unchanged.

Version 0.7.3 documents Cloudflare → Name.com → Gandi → Fastly leftover, then a selected connected registrar that leftover did not already use. Tool inputs are unchanged.

Version 0.9.2 keeps the last saved prices in search results until a successful refresh replaces them. Stale offers stay labeled outdated. Tool inputs are unchanged.

Version 0.9.1 describes Cloudflare prices as standard-tier search quotes for each supported single-label extension, collected with a synthetic name. They stay labeled `pricingBasis=sampled_standard`. Multi-label extensions are omitted. Tool inputs are unchanged.

Version **0.10.0** aligns with API **1.7.0** and nine tools. Price tools add
multi-registrar filters, ordering, favorites and CSV/Markdown output; estimates
include the UI cost breakdown. `check_availability_batch` reuses shared evidence
and bounded provider batches, optionally cache-only, preserving partial results
and retry guidance. Single-name fresh checks require explicit user intent.
Provider quotas/cooldowns remain unchanged; exports remain paginated. This package
update does not establish service deployment or update installed clients.

Version **0.10.1** adds MIT licensing and the public integration repository,
including install commands and repository metadata. API **1.7.0**, the nine
tools and the 20-extension batch limit are unchanged.

Version **0.10.2** makes annual renewal prices the main focus of the listing
copy, READMEs and shared skill. Initial registration prices stay separate. API
**1.7.0**, the nine tools and the 20-extension batch limit are unchanged.
