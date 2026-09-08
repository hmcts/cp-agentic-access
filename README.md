# cp-agentic-access

Design and decisions for AI-agent access to the Common Platform: WebMCP on the Advocate
Portal, remote MCP through the API Marketplace, and the identity, audit and classification
work each route needs.

**This repository is public.** Everything here is written for a public reader. Measured
evidence about the platform's internals, with file paths, counts and commands, stays in the
internal [CP knowledge store](https://github.com/hmcts/cp-knowledge-store); documents here
point to it rather than repeat it. Before adding a document, ask whether each specific in it is
publicly discoverable already. Protocols, standards and design reasoning are; internal hosts,
per-repository state, quoted internal documents and control weaknesses are not.

## The question this repository exists to answer

*How do AI agents get access to the Common Platform: acting as whom, through which route, with
what accountability?* The prompt was a product question, "why wouldn't we let defence interact
over MCP?", and the honest answer turned out to depend on three things the platform does not
yet have. The work here is about those three things and the routes that need them.

## Read in this order

1. [Should defence interact with the Common Platform over MCP?](docs/findings/2026-09-07-common-platform-over-mcp.md)
   The executive report. Separates WebMCP from remote MCP, records what defence can already do,
   measures the identity, audit and classification gaps against the estate's code, and ends
   with decisions in date order. Section 5 holds the sequence diagrams for the WebMCP routes.
2. [Decisions](docs/decisions/). One file per decision, with the rationale and the options
   considered. Decisions are dated and never edited after the fact; a change is a new decision
   that supersedes the old one.

## Layout

| Path | Holds |
|---|---|
| `docs/findings/` | Reports and measurements. Each states its evidence and date, and what it cannot tell you |
| `docs/decisions/` | Architecture decision records, numbered, dated |
| `docs/superpowers/specs/` | Design specifications, once a piece of work is scoped |
| `docs/superpowers/plans/` | Implementation plans derived from an approved spec |

## Conventions

- **Facts carry their source and date.** Platform facts come from the
  [CP knowledge store](https://github.com/hmcts/cp-knowledge-store) corpus and say which
  snapshot. Standards are quoted, not paraphrased, where the wording matters.
- **Legal points are named for counsel, not asserted.**
- **No person is named in a document.** Reasons are stated; owners are roles.
- **Declared is not deployed.** Anything read from code is what the code says, not what runs.

## Related

- [cp-knowledge-store](https://github.com/hmcts/cp-knowledge-store), the corpus and graph the
  measurements come from. The first report also lives there as the snapshot version.
- The API Marketplace's authentication standard, an internal document, which defines the
  identity pattern the remote-MCP route depends on.
- [WebMCP specification](https://webmachinelearning.github.io/webmcp/), W3C Web Machine
  Learning Community Group, Draft Community Group Report.
- [MCP authorisation specification](https://modelcontextprotocol.io/specification/draft/basic/authorization).
