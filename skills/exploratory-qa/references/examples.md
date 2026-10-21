# Calibrate findings against evidence

These examples are fictional. Their paths, observations, and evidence labels illustrate reporting; they are not results from a real application. Never reuse them as actual findings.

## A documented action returns the wrong scope

**Finding:** Export includes 42 records while the active filter shows 7 matching records.

- **Observed:** As an editor, apply the “Open” filter. The table reports “7 results.” Activate “Export filtered results.” The downloaded file contains 42 data rows, including closed records. Record the filter, exact control label, file contents, build, and action sequence.
- **Expectation:** The action should export the filtered set. Fictional `docs/reporting.md`, “Export,” revision `r12`, says exports use the active filters and all matching pages. The role and filter in the captured session match that scope. The explicit button label also supports the expectation.
- **Document status:** Applicable.
- **Assessment:** Defect; medium severity because the user receives a misleading data set and must filter it again; high confidence if the captured file is tied to that action. Regression status unknown without a comparable earlier build.
- **Limits:** Do not infer an authorization leak, incorrect SQL, or all-platform failure from this evidence. Record one attempt if only one was observed.

The useful justification connects the actual passage to the current action. Merely linking a general reporting document would not establish the expected scope.

## A small text error is still a finding

**Finding:** The selection toolbar displays “1 items selected” for one selected item in the English interface.

- **Observed:** One row is selected; the visible toolbar reads exactly “1 items selected.” Preserve a screenshot showing the locale and relevant selection context.
- **Expectation:** The singular count should use “item.” A scoped search of the selection and terminology documentation found no corresponding copy rule. Ordinary English number agreement supports the correction without inventing a product requirement.
- **Document status:** No match; record searched locations and terms.
- **Assessment:** Defect; low severity because meaning remains understandable; high confidence after checking the rendered text. Regression status unknown.
- **Limits:** Do not escalate this to task failure or rewrite unrelated sentences to match a preferred tone.

If the phrase came only from OCR and the image was unreadable, verify it before making the same claim.

## A no-op control without a matching requirement

**Finding:** “Open invoice” provides no invoice, navigation, or explanation in the observed session.

- **Observed:** On an accessible invoice record, activate the enabled control through normal pointer input. During the recorded observation interval, the route and visible state remain unchanged; no new tab, download, dialog, or message appears. A second ordinary activation under the same conditions behaves the same way.
- **Expectation:** “Open invoice” promises access to the invoice or an explanation of why it cannot open. Relevant invoice and navigation documentation contained no applicable description after a bounded search.
- **Document status:** No match.
- **Assessment:** Defect when the evidence establishes the failed operation and rules out the relevant alternative destinations; otherwise suspected defect. A blocked core task with no workaround may justify high severity under the project's rubric; do not infer that severity from the label alone.
- **Limits:** State the measured interval rather than “never responds.” A timeout from the click tool alone establishes an execution problem, not this product finding. Do not claim the backend is broken without separate evidence.

Missing documentation does not erase a demonstrated failure of an explicit UI promise.

## A visual difference that should not become a defect

**Observation:** “Delete workspace” is red; “Leave workspace” is neutral.

An applicable design decision says irreversible workspace deletion uses a destructive treatment, while leaving preserves the workspace for other members. The controls have different consequences, and the observed styling matches that distinction. Record the resolved observation if useful; do not file “inconsistent button colors.”

If a separate captured state shows the delete label clipped so its object cannot be read, investigate that specific loss of meaning independently. An intentional color difference does not excuse a different defect.

## Conflicting documents and incomplete evidence

An accepted release requirement says editors can rename an item; a later draft proposes restricting renaming to administrators. A screenshot shows a disabled editor control, but the tested build and applicable release are unknown.

Retain both sources, their status and scope, and the observed disabled state. Report a product question or suspected defect according to what remains uncertain. Do not silently treat the newest date as final authority. If a separate normal interaction demonstrably loses saved user data, report that failure on its own evidence even while the permission decision remains unresolved.

## A persistence claim that screenshots cannot establish

A supplied image shows a “Saved” toast. A later image shows different text, but the record identifiers are missing. The images do not establish that the same record lost its changes.

Request or collect the minimum missing evidence if possible: identity of the record, the save sequence, later retrieval, and applicable asynchronous behavior. Until then, retain the uncertainty. Do not claim data loss, reproduction frequency, or a storage root cause.
