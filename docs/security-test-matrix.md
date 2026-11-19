# Security test matrix and required evidence

Use fictional accounts A/B and bounded sample payloads. Run against an isolated test service; never probe unrelated websites. Store test fixture IDs rather than private payloads.

| ID | Setup and request | Required result | Evidence owner |
| --- | --- | --- | --- |
| AUTH-1 | A requests B's protected object ID | Denied; no private fields | Server integration test |
| AUTH-2 | Expire A's session after discovery | Execution denied | Browser plus server |
| AUTH-3 | Revoke permission while review is open | Commit denied; no mutation | Server commit test |
| INPUT-1 | Wrong type, unknown field, oversized text | Rejected before operation | Handler/server tests |
| OUTPUT-1 | Seed backing object with secret marker | Marker absent from result/error/log | Response/log review |
| INJECT-1 | Include hostile instructions in returned user content | Content treated as data; scope unchanged | Caller task test |
| DOM-1 | Return HTML/script-shaped text | Displayed safely; no script execution | Browser test |
| REVIEW-1 | Invoke preparation, then refuse | No committed state | Browser plus operation log |
| REVIEW-2 | Let review expire or abort it | Promise resolves/rejects as documented; no mutation | Browser test |
| REVIEW-3 | Change payload after review | New approval required | Server test |
| REPLAY-1 | Concurrent same-key identical requests | Exactly one committed operation | Atomic server test |
| REPLAY-2 | Same key with changed payload | Conflict/denial, no second mutation | Server test |
| RECOVER-1 | Lose response after commit | Status lookup returns durable result | Fault injection test |
| LIFE-1 | Logout/teardown during in-flight request | Old tool removed; stale context cannot commit | Browser plus server |
| ABUSE-1 | Oversized or excessive requests | Bounded work and rate-limit behavior | Service test |

## Record outcomes, not just assertions

For each ID retain commit, environment, fixture, expected/actual result, operation count and sanitized evidence path. An unimplemented server test is **not tested**, even if a local demonstration passes. For read-only examples, justify not-applicable mutation tests rather than silently skipping them.

Review the test's independence: measure the actual state/operation count, not just a success message. Check server refusal and absence of protected output. For prompt injection, evaluate the caller's actions as well as the content annotation.

## Release decision

Resolve failed authentication, authorization, confirmation, replay and recovery tests before a consequential pilot. Document remaining environment coverage and review date. No universal “secure” label follows from this matrix.
