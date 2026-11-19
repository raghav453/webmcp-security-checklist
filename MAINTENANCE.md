# Maintenance and compatibility record

Reviewed 19 November 2026 against the [13 November WebMCP draft](https://webmachinelearning.github.io/webmcp/). This community-group draft is experimental and is not a W3C Standard. Its JavaScript surface is `document.modelContext`, asynchronous `registerTool`, and registration cleanup through an AbortSignal. Chrome implementations and older examples may use another API revision. Record the actual browser, flags or trial, and observed API before assessing compatibility. A polyfill test does not prove browser-agent interoperability.

Review monthly, and whenever the draft IDL, Chrome release/trial guidance, or a linked tool changes. This is a maintainer process, not an automated schedule.

1. Compare the draft IDL with the recorded API above. Read changed registration, discovery, execution, cancellation and security sections.
2. Re-run applicable examples in a clean browser. Record browser version, operating system, secure origin, enabled feature, discovery evidence, execution result, and negative cases.
3. Check external links, redirects and destination content. Remove unavailable or misleading recommendations.
4. Update the reviewed date only after review; record behavior changes in CHANGELOG.md. Preserve migration notes for earlier revisions.
5. Confirm this project's purpose still differs from the companion repositories. Add detail to the owning guide instead of duplicating it.

Acceptance: source citations match claims, examples reflect the stated runtime, links work, no product preview is represented as a deployed integration, and each new section resolves a real developer question. A passing test is scoped to its tested environment.
