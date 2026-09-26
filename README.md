# Cheapest Domains integrations

Find domain names you can afford to keep. These integrations give an AI assistant
domain-research instructions and access to the public [Cheapest Domains](https://www.cheapest.domains)
service, focused on the real cost of keeping a domain: its annual renewal price.
Compare renewals first, with initial registration prices shown separately,
supported multi-year estimates, exact-name
availability and registrar destinations. Your assistant generates the name ideas;
Cheapest Domains supplies the evidence. Purchases happen at the registrar.

This repository contains the installable integrations for Codex, Claude Code,
Cursor and other Agent Skills/MCP clients. It includes no application/server
implementation, installation hooks, credentials or local service. Cheapest Domains
requires no account or API key; your AI client has its own access requirements.

## Install the plugin

Choose the commands for your client. The plugin includes both the skill and its
remote MCP connection, so skip a duplicate standalone connection.

```sh
# Codex
codex plugin marketplace add igalil/cheapest-domains-integrations
codex plugin add cheapest-domains@cheapest-domains

# Claude Code
claude plugin marketplace add igalil/cheapest-domains-integrations
claude plugin install cheapest-domains@cheapest-domains
```

Start a new Codex chat or reload Claude's plugins after installation. In Claude
Code, invoke `/cheapest-domains:domain-research`. In Codex, ask to use the
Cheapest Domains domain-research skill.

## Install only the skill

```sh
npx skills add igalil/cheapest-domains-integrations --skill domain-research
```

This installs instructions, not an MCP connection. Use a connected MCP server or
the skill's public HTTPS fallback when your client permits network access. Skills.sh
directory discovery depends on installation telemetry; this repository is not
proof of a listing in any third-party directory.

## Connect only MCP

Use `https://cheapest.domains/mcp`, Streamable HTTP, with no authentication.
For Cursor or another compatible client, see the [setup instructions](https://www.cheapest.domains/for-ai).
The same service is available through the [public REST API](https://www.cheapest.domains/developers).

## Try it

> Use Cheapest Domains to show three extensions with annual renewals at or below
> USD 15. Include source times and a comparison link. Do not check exact names.

For name suggestions, tell the assistant about your project, preferred style and
budget. It checks suggestions by default within service limits. Ask for unchecked
brainstorming if you do not want proposed names sent to checking providers.

## Scope and privacy

The service compares selected registrars, not the whole market. Preserve original
source dates, stale/partial coverage, premium uncertainty and minimum terms.
Availability is temporary and does not reserve a name. The tools cannot buy,
register, transfer or renew domains. Radar popularity is DNS activity, not SEO
competition or availability, and retains its separate CC BY-NC 4.0 license.

The skill keeps project briefs local and sends only the query inputs needed for
research. Exact-name checks can send a domain to the service and its checking
providers. Query URLs may appear in hosting logs. See the [privacy policy](https://www.cheapest.domains/privacy)
and [terms](https://www.cheapest.domains/terms).

## Documentation and support

- [Plugin installation, data handling and license scope](plugins/cheapest-domains/README.md)
- [Bundled skill](plugins/cheapest-domains/skills/domain-research/SKILL.md)
- [API reference](plugins/cheapest-domains/skills/domain-research/references/api.md)
- [Public setup guide](https://www.cheapest.domains/for-ai)
- [Integration issues](https://github.com/igalil/cheapest-domains-integrations/issues)
- Service support: [hello@cheapest.domains](mailto:hello@cheapest.domains)

## License

The integration files, documentation and marketplace catalogs are MIT licensed,
copyright 2026 Ilios Galil (PerfWebsite). See [LICENSE](LICENSE). Keep its notice
when redistributing copies. This grant does not cover the private application or
hosted server source, grant trademark rights, or replace service/third-party data
terms. Forks should identify their own publisher rather than imply endorsement.
