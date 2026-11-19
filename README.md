# WebMCP security checklist

This WebMCP security checklist turns browser-agent risks into reviewable application controls and negative tests. Use it as a developer or security reviewer before exposing protected data or consequential website operations. It provides a trust-boundary model, threat scenarios, an actionable release checklist, a confirmation design and a test matrix with required evidence. It is a review aid, not a security certification.

Treat tool inputs, website content and agent-generated requests as untrusted. Reuse your application's authentication and enforce authorization at the server operation. Browser availability, schema declarations and tool annotations do not replace those controls.

## Review a tool

1. Map assets and boundaries in [docs/threat-model.md](docs/threat-model.md).
2. Complete [SECURITY-CHECKLIST.md](SECURITY-CHECKLIST.md) with an owner and evidence for every gate.
3. Apply [docs/confirmation-and-replay.md](docs/confirmation-and-replay.md) to consequential changes.
4. Run the negative cases in [docs/security-test-matrix.md](docs/security-test-matrix.md).
5. Preserve a sanitized [review record](examples/security-review.example.json).

## Current technical scope

Reviewed 19 November 2026 against the [13 November WebMCP draft](https://webmachinelearning.github.io/webmcp/). This community-group draft is experimental and is not a W3C Standard. Its JavaScript surface is `document.modelContext`, asynchronous `registerTool`, and registration cleanup through an AbortSignal. Chrome implementations and older examples may use another API revision. Record the actual browser, flags or trial, and observed API before assessing compatibility. A polyfill test does not prove browser-agent interoperability.

The guide covers application behavior around structured website tools. It does not promise that WebMCP prevents prompt injection, guarantees consent, or authorizes tool callers. Cross-origin exposure and discovery options should be constrained deliberately, and browser controls still need their own compatibility evidence.

## A practical first boundary

A search tool over public fictional products is different from updating a customer's delivery address. Both can accept structured inputs; only the latter needs account/resource authorization, exact-payload review, replay protection and durable recovery. A hidden button or confirmed: true parameter does not satisfy those requirements.

## Related implementation guidance

- [Readiness checklist](https://github.com/raghav453/webmcp-readiness-checklist) for release evidence and lifecycle verification.
- [Action examples](https://github.com/raghav453/webmcp-action-examples) for validated handlers and local confirmation/cancellation behavior.

[WebMCPly's AI action testing preview](https://webmcply.com/product/ai-testing) illustrates a proposed review workflow. It is a pre-launch, illustrative product preview, not an available security scanner or proof of verified integrations.

## Sources, disclosure and maintenance

- [Current WebMCP draft](https://webmachinelearning.github.io/webmcp/) — normative proposal text, interfaces, lifecycle, and security considerations.
- [Chrome WebMCP guide](https://developer.chrome.com/docs/ai/webmcp) — browser implementation, origin trial, local testing, and declarative forms; check its revision independently of the draft.
- [Chrome best practices](https://developer.chrome.com/docs/ai/webmcp/best-practices) — tool design and implementation guidance.
- [Agent security guidance](https://developer.chrome.com/docs/agents/security) — threats and boundaries when agents act on web content.

Use [SECURITY.md](SECURITY.md) for reporting guidance. Follow [CONTRIBUTING.md](CONTRIBUTING.md) and the dated review procedure in [MAINTENANCE.md](MAINTENANCE.md). Original material is MIT licensed.

Maintained by WebMCPly contributors. [WebMCPly information and early access](https://webmcply.com/). This independent educational resource carries no standards-body or browser-vendor endorsement.
