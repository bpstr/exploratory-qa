# Produce justified, actionable findings

Use the [report template](../assets/report-template.md). Report what happened, why it matters, and what supports the expectation. Keep observation, interpretation, and suggested remedy separate.

Scale the report to the finding. A simple spelling error can be a compact entry with the exact copy, location and evidence, expected wording and basis, impact, and classification. Reference shared environment or provenance once instead of repeating it. Reserve a full sequence and detailed evidence table for problems that need them.

## Require the finding contract

Include the following for each finding; mark genuinely unavailable information instead of inventing it:

| Field | Required content |
| --- | --- |
| Title and observation | Describe the specific discrepancy. Include exact UI copy when relevant. |
| User goal and consequence | Explain the affected task and observed impact. Identify plausible risks as inferences. |
| Reproduction context | Record the route, build where known, role, relevant data/state, platform, viewport, input method, and locale. Include only conditions that affect understanding or reproduction. |
| Actions and outcome | Give minimal steps, actual behavior, and any relevant waits, retries, navigation, or refresh. |
| Expected behavior | State the expectation and its source: applicable document, UI promise, product consistency, task outcome, or standard. Explain why it applies. |
| Evidence | Link screenshots, recordings, or captured output to the relevant actions and states. |
| Assessment | Record finding category, severity, and confidence separately. State unresolved questions and competing evidence. |

Attach documentary provenance where available: path or canonical URI, section, relevant passage, and known revision. State when the scoped search found no applicable document or when a source was unavailable, stale, or conflicting.

## Preserve the evidence sequence

- Capture the failed route before trying a workaround. Do not replace its evidence with the eventual successful state.
- Associate observations with the relevant build, account, data, and action sequence. State when corroborating evidence was obtained after a retry, reload, navigation, or mutation.
- Preserve exact labels, messages, counts, and values. Use an annotated copy to highlight an issue while retaining the original evidence.
- Describe what screenshots show without claiming they prove timing, persistence, keyboard behavior, or server state that was not observed.
- Use optional API, database, or source inspection to investigate a specific question. Do not silently substitute these paths for the user operation being assessed.
- Call an issue a regression only when a valid earlier baseline demonstrates the behavior changed under sufficiently comparable conditions. Otherwise report the observed defect and unknown regression status.

## Classify before escalating

| Category | Use when |
| --- | --- |
| Defect | Evidence demonstrates a failed user operation or a contradiction of an applicable requirement, explicit promise, or defensible correctness condition. |
| Suspected defect | Evidence suggests a fault, but reproduction, applicability, or intended behavior remains materially uncertain. |
| Usability concern | A stated heuristic and concrete context support a plausible difficulty, without establishing a functional defect. |
| Product question | Ambiguous or conflicting intent prevents a responsible correctness judgment. |

Retain an independently demonstrated defect even when its surrounding requirements conflict. Report the documentation question alongside it. Do not downgrade verified data loss merely because wording elsewhere is ambiguous.

Do not treat difference alone as a defect. Compare purpose, state, hierarchy, role, and platform conventions before flagging inconsistent controls. Report a specific violated expectation or consequence, not a preference such as “this looks unprofessional.”

## Calibrate impact and certainty

Use the project's severity rubric when supplied; otherwise use these working labels and explain the impact:

| Severity | Meaning |
| --- | --- |
| Critical | Demonstrated loss or exposure of important data, or widespread inability to perform essential work. |
| High | A core task is blocked or materially wrong without a reasonable workaround. |
| Medium | A task is impaired, misleading, or difficult, but a workable recovery exists. |
| Low | A localized copy, visual, or consistency defect has limited impact. |

Record confidence separately as high, medium, or low, with a reason. Base it on evidence, applicability, reproduction, and unresolved alternatives. Do not manufacture probability percentages. Keep potential impact explicit when a serious outcome remains unconfirmed.

Do not equate severity with fix priority. Apply prioritization rules only when provided; otherwise leave scheduling and release decisions to the responsible stakeholder. Do not dismiss a verified small defect simply because it is low severity.

## Investigate efficiently and distinguish tool failures

- Check plausible alternatives: permissions, pending work, test data, configuration, environment, and misunderstood intent.
- If a tool reports success, inspect the product outcome. If it fails, establish whether the product action occurred before retrying a mutation.
- Record stale coordinates, unavailable tools, driver errors, and unsupported capabilities as investigation limitations unless product evidence independently establishes a defect.
- Repeat or vary an action only to answer a remaining question about validity, conditions, or scope. Stop once evidence is sufficient; retain intermittent behavior with observed frequency and context.
- Do not rerun unrelated journeys or the full platform matrix automatically. Do not repair code or update baselines during an investigation unless the user requested that work.
- Report root cause only with supporting evidence. Label an explanation such as “a missing flex rule” as a hypothesis until verified; a screenshot establishes the overlap, not its implementation cause.

## Consolidate and maintain findings

- Group repeated instances when they share an evidenced behavior and remediation scope; list affected locations. Do not assume identical symptoms have the same underlying cause.
- Keep independently actionable problems separate. Link related findings and previous reports instead of producing duplicate tickets.
- Track observable symptom, context, evidence, and status. Record why an issue was accepted, fixed, deferred, or judged intentional.
- Keep intentional exceptions scoped to their context. Do not learn a global suppression from one dismissal; reconsider when relevant requirements, behavior, or environment change.
- End the session report with examined scope, blockers, unexamined areas, and unresolved risks. Do not turn a bounded exploration into an unqualified “QA passed.”

## Check small details without inventing defects

- Report “1 items” as a concrete language defect, with the actual locale and low impact where appropriate. Do not rewrite otherwise correct copy merely to match personal taste.
- For clipped text, show which meaning or control is lost at the tested viewport; distinguish intentional truncation with an accessible full value from inaccessible content.
- For a button apparently leading nowhere, record the route, action, observation interval, and expected outcome. Check visible feedback and resulting state before claiming no action occurred.
- For “Saved” followed by missing edits, preserve both states and verify the same record and account. Describe the lost change without inventing a database cause.
