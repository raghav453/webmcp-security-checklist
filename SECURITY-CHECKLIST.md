# Security review release gates

Tool / owner / reviewed commit / environment / date / reviewer:

Mark each gate pass, fail, not tested or not applicable with a reason and evidence. A consequential tool is blocked while any access, consent, replay or recovery gate is unresolved.

## Trust and data

- [ ] List assets, principals, origins, windows, session context and server endpoints.
- [ ] Distinguish caller instructions from untrusted tool input and returned page/user content.
- [ ] Expose only intended tools and origins; evaluate cross-origin exposure deliberately.
- [ ] Return the minimum public/authorized fields; no tokens, secrets or hidden account metadata.
- [ ] Identify user-controlled content and truthful untrustedContentHint where applicable.
- [ ] Render responses as data with safe text APIs; do not execute result HTML or instructions.

## Authentication, authorization and session

- [ ] Authenticate protected operations using the existing application mechanism.
- [ ] Enforce authorization for principal, operation and resource on the server each time.
- [ ] Reject another user's resource ID and unauthorized field changes.
- [ ] Handle expiry, logout, revoked access and account switching without stale authorization.
- [ ] Apply normal CSRF/origin protections to cookie-authenticated mutation endpoints.
- [ ] Keep discovery restrictions separate from operation-level permission enforcement.

## Contracts and execution

- [ ] Reject wrong types, unknown properties, excessive sizes and out-of-range values.
- [ ] Validate output shapes and minimize sensitive error details.
- [ ] Use explicit empty, denied, canceled and failed outcomes; no false-success responses.
- [ ] Keep read-only tools actually read-only and test absence of domain mutations.
- [ ] Propagate AbortSignal to cancellable work; do not commit canceled proposals.
- [ ] Remove registration on teardown/logout; reject work from obsolete contexts.
- [ ] Enforce server rate limits, resource budgets and abuse monitoring for costly operations.

## Consent, replay and recovery

- [ ] Identify consequential effects and show the exact proposed change to the human.
- [ ] Bind confirmation to payload, principal, intended operation and freshness.
- [ ] Reject agent-supplied booleans as confirmation evidence.
- [ ] Cancel on timeout, navigation, session change or user refusal.
- [ ] Implement atomic idempotency and reject key reuse with a different payload.
- [ ] Revalidate authorization and authoritative state immediately before committing.
- [ ] Define how to recover partial failures and ambiguous network outcomes.
- [ ] Provide visible status, a cancellation path and appropriate rollback or remediation.

## Observability and release

- [ ] Log minimal operation IDs, result classes and timing without raw sensitive payloads.
- [ ] Define retention, access and redaction policy for review evidence and logs.
- [ ] Run prompt-injection, cross-account, replay, cancellation and lifecycle cases.
- [ ] Separate browser demo evidence from server security evidence.
- [ ] Name the incident/maintenance owner and feature-disable procedure.
- [ ] Document untested environments and residual risks before pilot approval.
