# 0001. Treat the API Marketplace's audit logging as sufficient at application level

**Date:** 2026-09-07
**Status:** Accepted

## Context

The executive report measured the Common Platform's audit trail as uneven across service
generations, with the recorded actor asserted at the gateway rather than verified downstream
(detail in the CP knowledge store's internal finding). Any agent channel needs to say who did
what.

The API Marketplace's authentication standard has the gateway log every inbound request with the
calling application, the time, the endpoint and the outcome, and describes that log as its
primary forensic and detection record. The trail identifies the registered application.

## Decision

Treat the marketplace gateway's per-request logging as the audit trail for any agent traffic
that passes through it, at the level of the registered application. Do not build a separate
audit mechanism for that traffic.

## Consequences

- Attribution is to the application, not to a person. Per-person attribution follows only from
  a user-identity pattern the marketplace does not yet define (see decision 0002).
- Traffic that does not pass through the marketplace gateway, such as WebMCP tools calling the
  Advocate Portal's existing backend, is audited by the platform's existing mechanisms, which
  record the signed-in user. Tool-invoked calls should carry a marker so that an agent's
  involvement is visible in those records.
- What a receiving service does with a request is outside this decision; the gateway log covers
  the request, not the service's own record of it.

## Options considered

- **Build a dedicated audit path for agent calls.** Rejected: duplicates a control the
  marketplace already runs, and would still lack the person for the same reason.
- **Require per-person audit before any agent access.** Rejected as a blocker: the marketplace
  cannot supply the person today, and application-level attribution is enough for a read-only
  experiment acting as the firm.
