# Sources and design rationale

Reviewed: 2026-10-21.

Use these primary sources to understand or maintain the method. Routine execution is defined by [SKILL.md](../SKILL.md) and the bundled references; do not fetch this entire bibliography for each investigation. The procedures in this repository are an adaptation, not a claim of endorsement by these authors or organizations.

## Testing judgment and communication

### ISTQB: Foundation Level syllabus v4.0.1

[Official syllabus](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf), especially sections 1.5.1, 2.2.3, 4.2, 4.4.2, 5.1.3, 5.2, and 5.5.

Use its treatment of tester skills, exploratory testing, risk, completion criteria, and defect management as the broad methodological foundation. Translate curiosity and critical thinking into observable investigation steps. Prioritize user consequences, adapt exploration as evidence changes, and communicate unresolved risks. Do not measure the quality of this work by the number of generated tests.

Use section 4.2 for input partitions, domain-appropriate boundaries, decision tables, and state transitions in [test-design.md](test-design.md) and [workflows.md](workflows.md). Use section 2.2.3 to separate confirmation of an original failure from regression checks of other behavior. Select the relevant techniques and cases; a model's coverage criterion is not a universal completion requirement for every exploratory charter.

### ISTQB: Advanced Test Analyst syllabus v4.0

[Official syllabus hosted by ASTQB](https://astqb.org/assets/documents/ISTQB-CTAL-TA-Syllabus-v4.0-EN-4.pdf), especially sections 3.1.2, 3.2.2, and 3.5.1.

Use its treatment of combinatorial selection, consecutive transition sequences, round trips, and risk-sensitive technique choice. Preserve known interactions involving several conditions even when a smaller sample covers their pairs. Derive the relevant model from product evidence and report sampled and untested cases honestly.

### James Bach: Heuristic Test Strategy Model

[HTSM v6.3](https://www.satisfice.com/download/heuristic-test-strategy-model).

Use the model's context-sensitive guidewords to broaden investigation across product factors, quality criteria, project conditions, and techniques. Select relevant lenses rather than executing every possible check. Its emphasis on states and boundaries informs exploration of loading, empty, populated, failed, interrupted, and recovered states around a user's task.

### Michael Bolton: FEW HICCUPPS

[Original explanation](https://developsense.com/blog/2012/07/few-hiccupps).

Use this account of testing oracles to explain where an expectation comes from: product claims, purpose, history, internal consistency, and other relevant comparisons. Its central limitation matters: such expectations are fallible and contextual. Require a justified expectation, investigate legitimate differences, and retain uncertainty when sources disagree. An inconsistency alone does not establish a defect.

### Jonathan and James Bach: Session-Based Test Management

[Original article and download](https://www.satisfice.com/download/session-based-test-management).

Use the reviewable-session and debrief concepts to retain learning and direct the next useful investigation. Adapt the report to observations, revised understanding, obstacles, and unresolved questions. Do not turn time accounting into a universal quality threshold or require an agent to invent personal feelings or attention scores.

### Jakob Nielsen: Usability heuristics

[Ten usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) and [NN/g's evaluation procedure](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/).

Use these principles to investigate status feedback, terminology, consistency, user control, error prevention, and recovery. Apply them to actual tasks and interface content. Treat a heuristic concern as an argued assessment, not proof of how every user will behave. Independent review can challenge a judgment; it does not replace research with actual users.

### Mozilla: Bug writing guidelines

[Official guidelines](https://bugzilla.mozilla.org/page.cgi?id=bug-writing.html).

Use the distinction between observations and speculation, together with precise reproduction steps and expected-versus-actual outcomes, to shape reports. Explain the problem before suggesting a remedy. Preserve environment and reproduction conditions. Do not infer an implementation cause from a visible symptom or combine unrelated problems into one vague ticket.

## Visual observation, accessibility, and platform fidelity

### Playwright: Visual comparisons

[Screenshot comparison documentation](https://playwright.dev/docs/test-snapshots).

Playwright supports authored visual regression checks against reference screenshots. This skill complements those checks by investigating expectations, uncovered states, and unexpected behavior. Preserve comparable environments and application states when judging a change against a baseline. A newly observed visual defect is not necessarily a regression, and a screenshot difference is not automatically an error.

### W3C WAI: Reflow, dialogs, and evaluation limits

[Reflow explanation](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html), [modal dialog pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/), [evaluation tools overview](https://www.w3.org/WAI/test-evaluate/tools/), and [WCAG 2.2 status messages](https://www.w3.org/TR/WCAG22/#status-messages).

Use reflow guidance to examine lost content or functionality under enlargement, preserving its scope and exceptions. Use the dialog pattern to investigate focus movement, keyboard operation, dismissal, and return paths. Distinguish supporting explanations and design patterns from normative requirements. Automated checks and structural inspection have limits; do not turn a limited review into an accessibility conformance claim or imply screen-reader testing that did not occur.

For actual screen-reader journeys, inspect meaningful names, roles, states, and status information in the tested reader/browser context. Preserve the actual announcement evidence and relevant vendor variation. The status-message criterion does not impose a universal one- or two-second announcement deadline.

### Chrome and Playwright: Emulation boundaries

[Chrome Device Mode](https://developer.chrome.com/docs/devtools/device-mode/) and [Playwright browser documentation](https://playwright.dev/docs/browsers).

Device emulation approximates conditions; it does not establish that an actual mobile device was tested. Playwright's WebKit build is not branded Safari. Record the real browser, operating system, input mode, and emulation settings. Keep actual-device evidence and simulated conditions distinguishable in findings and coverage reports.

## Manual QA material considered from Testland

The comparison with [Testland's manual-testing material](https://github.com/testland/qa/tree/main/plugins/qa-manual-testing) informed the selection of additions. Relevant source guides are [decision tables](https://github.com/testland/qa/blob/main/plugins/qa-manual-testing/skills/decision-table-test-design/SKILL.md), [state transitions](https://github.com/testland/qa/blob/main/plugins/qa-manual-testing/skills/state-transition-test-design/SKILL.md), [user/scenario/data tours](https://github.com/testland/qa/blob/main/plugins/qa-manual-testing/skills/exploratory-testing/references/fcc-cuts-vids.md), [session debriefs](https://github.com/testland/qa/blob/main/plugins/qa-manual-testing/skills/exploratory-testing/references/debrief.md), [confirmation testing](https://github.com/testland/qa/blob/main/plugins/qa-defect-management/skills/confirmation-testing-workflow/SKILL.md), and [screen-reader journeys](https://github.com/testland/qa/blob/main/plugins/qa-accessibility/skills/screen-reader-test-author/SKILL.md). Testland attributes the touring heuristic to [Michael Kelly's original post](https://michaeldkelly.com/blog/2005/9/20/touring-heuristic.html); its worked elaborations are distinct from that original description.

Use these as methodological context for the original, scoped procedures in this skill. The adaptation retains manual reasoning and checks primary technique definitions above; it does not import Testland's skills, code generators, mandatory matrices, fixed time-ratio gates, or announcement deadlines. Tours generate questions, while findings still require an applicable expectation and evidence. A perspective imagined by an agent is not a study of real users.

## Packaging and installation

[Agent Skills specification](https://agentskills.io/specification) defines the skill directory, metadata, and optional resources. [Vercel's CLI commands](https://github.com/vercel-labs/skills/blob/main/docs/commands.md), [repository](https://github.com/vercel-labs/skills), and [package metadata](https://github.com/vercel-labs/skills/blob/main/package.json) document installation and runtime requirements. Verify commands and requirements against the CLI version being used. Installing instructions does not install or validate a browser-control capability.

## Evidence boundary

These references support the method; they do not prove this skill's GUI defect-detection efficacy. Package validation, an installation smoke check, and review of supplied evidence establish different things from a live exploration benchmark. Evaluate live behavior using unseen cases, intentional differences, reproducible evidence, and fixed budgets. Report detection, false positives, replayability, coverage, and cost with their tested scope. Do not transfer another system's benchmark performance to this skill.
