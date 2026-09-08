# 0002. Put the user-identity use case to the API Marketplace formally

**Date:** 2026-09-07
**Status:** Accepted

## Context

An agent acting for a defence practitioner needs a token that names the person, the
organisation and the agent client. The platform's external APIs carry no user identity, and no
delegation flow exists anywhere on the estate (detail in the CP knowledge store's internal
finding).

The API Marketplace's authentication standard defines one pattern, application-to-API using
OAuth 2.0 client credentials with a signed JWT. The marketplace trusts the registered
application; end-user identity is out of scope, to be revisited when a confirmed use case for
individual user access emerges. The gateway mints a token for the platform carrying an
organisation identifier used for data-access scoping; it carries no user. The marketplace's
design notes anticipate tokens that carry user identity claims, and that such tokens would need
a separate DPIA, but no such pattern is designed.

## Decision

Treat an AI agent acting as a named practitioner as the confirmed use case the standard invites,
and put it to the marketplace team formally rather than designing around it in the Common
Platform. Until the marketplace carries a person, any agent route through the marketplace acts
as the firm, scoped by the organisation identifier.

## Consequences

- The remote-MCP route (the marketplace gateway exposing platform operations as MCP tools) can
  begin read-only with the agent registered as the firm's application. Acting as the named
  practitioner waits for the marketplace change.
- WebMCP tools on the Advocate Portal that call the portal's existing backend do not depend on
  this decision: the signed-in session already carries the person.
- The marketplace change, when designed, needs: a user-consent flow at the marketplace identity
  provider; a minted token carrying the user alongside the organisation; a mapping from that
  user to their own platform identity at the gateway; and the DPIA the standard already
  requires for user-claim tokens.

## Options considered

- **Design an on-behalf-of flow inside the Common Platform.** Rejected: it would create a
  second external identity boundary beside the marketplace, which the marketplace standard says
  clients calling platform APIs must eventually use.
- **Pass the user in a header from the agent client.** Rejected: the marketplace standard
  deprecates header-based identity, and a header carries no cryptographic proof of who set it.
- **Wait for the marketplace to reach it on its own roadmap.** Rejected: the standard revisits
  the position only when a confirmed use case emerges. This is that case, and it has to be
  stated to count.
