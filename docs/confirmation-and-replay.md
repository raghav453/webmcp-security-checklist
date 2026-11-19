# Confirmation, idempotency and ambiguous outcomes

## Separate a proposal from its effect

For a support request, prepare a bounded draft and display the exact text and recipient. A preparation tool can return requires_user_action. Sending is a separate operation controlled by a human decision and application policy. Never accept a caller-provided approval flag as proof that the human reviewed the proposal.

For a production mutation, bind review to the authenticated principal, operation, canonical payload, relevant state version and expiry. Store or validate that binding through a trusted application mechanism. Revalidate authorization at commit time; a previously valid session or price may have changed. If the payload changes, require a new review. Do not let an agent choose arbitrary recipients or URLs outside the intended task.

## A review state machine

```text
validated input → immutable proposal → awaiting human review
  cancel / timeout / abort / context change → discarded
  approve exact proposal → revalidate access and state → commit
    rejected/stale → no mutation; fresh review required
    committed → durable operation result
    ambiguous network response → query operation status before retry
```

The demo implementation in the companion examples uses a dialog and local fictional state. It demonstrates review, cancellation and timeout; it has no real server authority, payment operation or customer data. Same-origin application code can control its local state. Do not reuse that UI mechanism as a secure approval token for a real service.

## Make idempotency atomic

A durable server operation should enforce a unique key scoped to the principal and operation, and bind it to a canonical payload hash. Acquire/create the operation and apply the mutation in the appropriate transaction or atomic mechanism. Return the stored outcome for a repeated identical key. Reject the same key with a different payload. A JavaScript Map checked before an asynchronous network call is not durable or atomic across workers.

Use an idempotency key only when the endpoint defines that policy. It does not make every GET or POST safe to retry. For a timeout after a possible commit, ask the server for operation status before issuing a new key. Define retention and recovery for pending/failed states.

## Session and cancellation races

Abort cancels work only where the operation honors it. It cannot undo a server commit already completed. Recheck authorization immediately before mutation and provide a recoverable result if the client disappears. Abort pending dialogs, fetches and registrations on logout or teardown; do not let a stale approval complete a new session's task.

Required tests: refusal, timeout, changed payload, expired session, replay, concurrent identical requests, key/payload mismatch, lost response after commit, and status recovery. See [security-test-matrix.md](security-test-matrix.md).
