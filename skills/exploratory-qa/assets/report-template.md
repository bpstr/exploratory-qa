# Exploratory QA findings — [product and tested scope]

<!-- Replace placeholders with observed facts. Omit irrelevant fields and empty sections. Never invent screenshots, document matches, environments, reproduction attempts, or test results. Keep concise findings concise while retaining their evidential basis. -->

[Lead with the most consequential justified findings and the main remaining uncertainty. If none were established, state that result and the limited scope.]

## Findings

<!-- For simple findings, use a compact entry: title; category, severity and confidence with reasons; exact observation and evidence; expected result and documentary status/basis; impact and uncertainty. Refer to shared context. Use the expanded structure below when a sequence or conflicting evidence needs explanation. -->

### [ID] — [Specific observable problem]

**Category:** [Defect / Suspected defect / Usability concern / Product question]

**Severity:** [Project level, or Critical / High / Medium / Low] — [impact-based reason]

**Confidence:** [High / Medium / Low] — [evidence and unresolved alternatives]

**Regression status:** [Confirmed against identified comparable baseline / Unknown / Other supported conclusion]

**Affected goal and context**

[The user's task. Route or screen, relevant build, role, data/state, actual platform, viewport, input method, and locale. Include conditions needed to reproduce or interpret the finding; mark important unknowns.]

**Steps and actual result**

1. [Initial state and normal user action.]
2. [Next essential action and actual outcome; preserve relevant waits, retries, reloads, or navigation.]

[Exact observed UI copy, preserving punctuation and locale. Identify whether it came from a screenshot, visible browser text, DOM, accessibility text, OCR, or a supplied transcript.]

[For a workflow or property failure, retain the chain: initial object/state and prerequisites; effective property value, scope, and overrides; normal action; immediate feedback; later state or dependent operation. Identify the first observable divergence. Distinguish a saved value from evidence that its intended effect occurred. Omit this paragraph for simple findings.]

**Expected result and justification**

[What should happen and why: applicable requirement, explicit UI promise, established equivalent behavior, task outcome, or applicable standard. Explain the correspondence, not just the source title.]

[For conditional behavior, state: under these conditions, this action or setting should cause A; the evidence shows B. Include relevant timing and expected non-effects. Mark inferred expectations or unknown completion timing explicitly.]

- **Document status:** [Applicable / No match / Unavailable / Apparently stale / Conflicting]
- **Source:** [Path or canonical URI, section, available revision/date; or scoped search locations and meaningful terms if no match]
- **Relevant passage:** [Short excerpt or faithful paraphrase, retaining conditions]
- **Applicability or conflict:** [How it applies to this role, state, platform, feature, and build; include competing sources]

**Evidence and reproduction**

| Evidence | What it establishes | Action and state |
| --- | --- | --- |
| [Actual screenshot, recording, trace, or supplied evidence reference] | [Observable fact, with limits] | [Before/after which action, relevant state/build, time if known] |

[Observed attempts and outcomes, if repeated. Explain what was not reproduced or could not be checked; do not infer a rate from an unknown denominator.]

**User impact and uncertainty**

[Separate observed consequence from inferred risk. Identify a workaround, if demonstrated. Record competing explanations and remaining questions. State a root cause only when evidence supports it.]

**Suggested next step** — [Optional: the smallest clarification, investigation, or correction supported by the finding. Do not prescribe an unverified implementation fix.]

**Manual retest, when requested** — [Original finding and failing conditions; candidate build/environment and known fix provenance; any material differences; replayed route and evidence; confirmed for the tested scenario / failure still observed / inconclusive, with reasons. Keep any adjacent regression observations separate. Do not infer that one passing attempt resolves an intermittent failure.]

<!-- Repeat only for independently actionable findings. Group evidenced repeated instances and list their locations. Do not duplicate product questions already captured in a finding. -->

## Coverage and limitations

- **Examined:** [Goals, flows, states, documentation, and material probes actually reviewed.]
- **Workflow coverage, when relevant:** [Entry points and branches discovered, transitions or setting effects examined, and handoffs or dependencies left unexamined.]
- **Case selection, when relevant:** [Input classes, boundaries and units, business rules, transition pairs, or configuration combinations chosen and why; significant unexamined cases. Claim pairwise or other model coverage only when it was checked against the stated model.]
- **Platforms:** [Actual browser/OS/device or emulation; viewport, input, locale, theme, zoom where relevant.]
- **Evidence mode:** [Live exploration / supplied evidence review / a clearly described combination.]
- **Blocked or unexamined:** [Unsupported tools, missing access, unvisited flows, and platform gaps. Keep tool errors separate from product findings.]
- **Remaining risks and questions:** [What further evidence would resolve them.]
- **Investigated observations not filed:** [Optional useful examples of intended behavior or disproved suspicions, with reasons.]

## Session learning and next investigation

<!-- Include only material learning; omit this section if it would repeat findings or coverage. No required time ratios, attention scores, or invented personal feelings. -->

- **What changed our understanding:** [Newly established behavior, a revised expectation, or a resolved suspicion, with its basis.]
- **Useful next investigation:** [A bounded user goal and remaining question, the evidence that would resolve it, and any obstacle. Mark this as proposed; do not imply it was executed or automatically start a new campaign.]

[A bounded exploration does not establish defect absence, full accessibility conformance, or complete platform coverage. State only conclusions supported by this session.]
