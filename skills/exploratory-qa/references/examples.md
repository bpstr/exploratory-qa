# Calibrate findings against evidence

These examples are fictional. Their paths, observations, and evidence labels illustrate reporting; they are not results from a real application. Never reuse them as actual findings.

## Contents

- [A documented action returns the wrong scope](#a-documented-action-returns-the-wrong-scope)
- [A small text error is still a finding](#a-small-text-error-is-still-a-finding)
- [A no-op control without a matching requirement](#a-no-op-control-without-a-matching-requirement)
- [A visual difference that should not become a defect](#a-visual-difference-that-should-not-become-a-defect)
- [Conflicting documents and incomplete evidence](#conflicting-documents-and-incomplete-evidence)
- [A persistence claim that screenshots cannot establish](#a-persistence-claim-that-screenshots-cannot-establish)
- [A saved property is ignored by the operation it governs](#a-saved-property-is-ignored-by-the-operation-it-governs)
- [A button performs a different valid transition](#a-button-performs-a-different-valid-transition)
- [An inherited setting legitimately does not change existing items](#an-inherited-setting-legitimately-does-not-change-existing-items)
- [An asynchronous action has not yet established an outcome](#an-asynchronous-action-has-not-yet-established-an-outcome)
- [A boundary depends on the documented unit](#a-boundary-depends-on-the-documented-unit)
- [A round trip exposes retained approval](#a-round-trip-exposes-retained-approval)
- [A historical label intentionally differs from a current name](#a-historical-label-intentionally-differs-from-a-current-name)
- [A user perspective raises a question without proving user behavior](#a-user-perspective-raises-a-question-without-proving-user-behavior)
- [A passing alternative does not verify the original fix](#a-passing-alternative-does-not-verify-the-original-fix)

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

## A saved property is ignored by the operation it governs

**Finding:** A contributor starts a task without an estimate despite the project's enabled estimate requirement.

Fictional `docs/task-workflow.md`, “Start prerequisites,” approved revision `r8`, requires an estimate before contributors start tasks in projects with this setting enabled. Confirm the project, task, contributor role, and absence of a documented override. Save the setting, reload it, then start an eligible task with no estimate. The task enters “In progress” and retains that state after reload: expected rejection (A), observed transition (B).

Use a controlled comparison with equivalent task prerequisites and the setting disabled, keeping role and project fixed. If both conditions permit starting, the setting persists but its documented effect is absent. **Document status: Applicable; assessment: Defect** when these conditions are established. If the active role or effective configuration cannot be verified, report a **Suspected defect**. Do not infer which service ignored the setting.

## A button performs a different valid transition

**Finding:** “Save draft” publishes the article instead of preserving its draft state.

In an authorized test workspace, inspect an unpublished article as an author. Fictional `docs/editorial-workflow.md`, “Draft actions,” revision `r16`, permits authors to save drafts but reserves publication for an explicit publish action. Change the title and activate “Save draft.” A “Saved” toast appears, but the article subsequently shows “Published” in its detail view and appears in the reader listing. Confirm the article identity and state after reload; do not rely on the toast alone.

**Document status: Applicable; assessment: Defect** if the observed publication came from this action. Saving and publishing may each be valid operations, but their permissions and consequences differ. Check whether scheduled publication or another authorized actor explains the transition before attributing it. Without that distinction, retain a **Suspected defect** and identify the missing evidence. Avoid publishing real content to reproduce it.

## An inherited setting legitimately does not change existing items

**Observation:** Changing the workspace's default notification channel leaves an existing project's channel unchanged.

Fictional `docs/notification-settings.md`, “Defaults and overrides,” approved revision `r4`, states that the workspace default initializes newly created projects; existing projects retain their own channel. Read the project's effective setting and any explicit override. Compare an existing project with a newly created test project under the same workspace: the former retains its saved channel, while the latter receives the new default. This matches the documented object scope and timing.

**Document status: Applicable; assessment: resolved observation, no defect.** Do not infer that a default is a live inheritance rule. If the interface instead promises “Apply to all existing projects,” investigate that separate contradiction between copy and behavior. Preserve both the documentation and wording; classify a **Product question** if the intended contract remains unresolved, rather than quietly choosing whichever source fits the implementation.

## An asynchronous action has not yet established an outcome

**Observation:** “Rebuild index” acknowledges a request, but search results remain unchanged during the recorded interval.

Fictional `docs/search-operations.md` describes queued processing but provides no completion deadline. Record the affected index, request time, visible job state, and observation interval. “Queued” establishes acceptance, not completion or failure. Check an available job-status view and, once completion is reported, repeat the relevant search with controlled inputs.

**Document status: Applicable for asynchronous behavior; timing expectation unresolved.** While work remains queued, record the operation as pending and the outcome as unverified. Do not label it a defect solely because the exploration budget ended. An applicable deadline that is exceeded, a completed job with demonstrably stale results, or missing promised progress feedback can support a separate finding. State which condition was actually observed.

## A boundary depends on the documented unit

Fictional `docs/invitations.md`, revision `r8`, allows at most 64 distinct recipients, consolidates duplicate addresses, and rejects an over-limit batch before creating invitations. Select 63, 64, and 65 distinct recipients through the normal interface and inspect the created set or rejection, using only authorized test recipients.

If 65 distinct recipients are accepted and invitations created, report the documented limit violation with the input and affected set. If 65 entered rows include a duplicate and produce 64 distinct invitations, that observation matches the rule. Counting input rows as distinct recipients would create a false finding. An input control that prevents a 65th distinct entry establishes that restriction; it does not prove the unobserved submission path also enforces the limit. Keep cases designed and cases executed separate.

## A round trip exposes retained approval

Fictional `docs/review.md`, revision `r16`, says withdrawing a submission invalidates its approval and resubmission requires a new review. An author submits a document, a reviewer approves it, and the author withdraws it. Follow that same document through an edit and resubmission. If it becomes published without the required new review, preserve the approval, withdrawal, effective permissions, resubmission, and published-state evidence.

This supports a workflow defect when the applicable rule and lack of a legitimate bypass are established. Checking Submit and Withdraw independently would not exercise this history. A different product whose rule explicitly preserves approval for unchanged content needs a different expectation; do not infer invalidation solely from a returned status label.

## A historical label intentionally differs from a current name

Fictional `docs/audit-history.md`, revision `r4`, requires completed approval records to preserve the approver's display name at the time of approval. After an authorized account rename, the profile shows the new name and an earlier approval shows the old name, tied to the same user identity.

That difference is intentional under the historical-snapshot rule. Do not file a stale-label defect or rewrite the historical value. A broken link to the wrong person or a missing promised identity remains a separate question. When the product does not define snapshot versus live labels, preserve both observations and report the unresolved intent.

## A user perspective raises a question without proving user behavior

An approver follows a supplied test notification link. The page's instruction says to select "Review," but the available controls say "Open details" and "More." Inspect whether the promised action is reachable for this role and state, and check the applicable terminology or workflow documentation.

The mismatch can justify a concrete copy finding or usability concern once its context is established. Imagining a first-time approver does not establish that real users abandon the task, how often they struggle, or which redesign would improve completion. If the link opens the wrong role's view or approval is legitimately unavailable, record that evidence before choosing the finding.

## A passing alternative does not verify the original fix

A defect report records that an existing project ignores a review requirement after a particular edit-and-resubmit sequence. On a preview build, a newly created project correctly enters review, but the original sequence and relevant historical conditions have not been exercised.

Record the new-project result as observed behavior and leave confirmation of the reported defect inconclusive. Replay the original route with comparable configuration and history, identify the tested build, and check the original expected effect. A missing source revision limits attribution to a specific fix; it does not prevent observing the available build. Conversely, a passing replay confirms only its tested conditions, especially if the original failure was intermittent. Preserve any adjacent regression results separately.
