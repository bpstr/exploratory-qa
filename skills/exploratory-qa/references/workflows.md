# Discover workflows and verify expected effects

Use this guide with [SKILL.md](../SKILL.md) when quality depends on a sequence, a state transition, or a property that changes later behavior. Discover what users can do and what those actions mean; do not limit exploration to predetermined steps or whether individual controls respond.

## Contents

- [Discover journeys from the product](#discover-journeys-from-the-product)
- [Build the map incrementally](#build-the-map-incrementally)
- [Define the action contract](#define-the-action-contract)
- [Follow properties into the behavior they govern](#follow-properties-into-the-behavior-they-govern)
- [Follow branches, order, and recovery](#follow-branches-order-and-recovery)
- [Probe transitions and their history](#probe-transitions-and-their-history)
- [Compare conditions without overstating causality](#compare-conditions-without-overstating-causality)
- [Respect asynchronous timing](#respect-asynchronous-timing)
- [Report the first divergence and stop responsibly](#report-the-first-divergence-and-stop-responsibly)

## Discover journeys from the product

Start with a user goal and the domain objects involved: a task, document, project, invitation, order, or account. Identify who creates, changes, consumes, reviews, and completes each object. Follow visible navigation, menus, contextual actions, status changes, helper text, and settings to discover possible paths.

Read corresponding requirements and decisions using [project-context.md](project-context.md). Connect documented behavior to actual controls and object states. Mark expectations as documented, explicitly promised by the UI, supported by equivalent behavior, or inferred. Preserve uncertain intent instead of treating a plausible workflow as a requirement.

Look for forgotten paths: an action available only after a status change, a setting consumed elsewhere, a secondary role's next step, an empty state's creation route, or recovery from partial completion. Revisit relevant menus and controls when the object's state changes. Follow leads that affect the mission; do not inventory every screen first.

## Build the map incrementally

Keep a small working map of the active journey. Add rows as a new branch or dependency becomes relevant; do not construct a mandatory cross-product of roles, states, and properties.

| Role, object, starting state | Action or condition | Expected next state and later effect | Expectation basis | Observed result or next probe |
| --- | --- | --- | --- | --- |
| `[role; object ID; state]` | `[control; target; value]` | `[immediate outcome; consuming step]` | `[source and conditions; or inference]` | `[evidence; uncertainty]` |

Track stable object identities, relevant configuration, and important checkpoints. Keep separate objects and sessions distinguishable. A changed label, duplicated record, filtered list, or switched account must not silently change what the journey is testing.

## Define the action contract

Before a meaningful action, state what would establish success:

- **Prerequisites and target:** Identify the actor, permissions, starting state, selected object or set, entered value, and applicable configuration.
- **Immediate feedback:** Identify the promised navigation, confirmation, progress, validation, or visible state change. Check whether feedback accurately describes the outcome.
- **Persisted state:** Identify what should survive reopening, navigation, or another relevant retrieval. Do not infer persistence from a toast.
- **Downstream effect:** Identify the later operation or actor that consumes the result and how its behavior should change.
- **Expected non-effects:** Identify relevant things that should remain unchanged, such as unrelated records, an explicit override, or a cancelled operation. Justify these expectations too.
- **Timing and scope:** Establish whether the effect is immediate, asynchronous, scheduled, or conditional, and whether it applies to one object, a selection, a project, or an account.

Use ordinary UI interactions to exercise this contract. Do not navigate directly to a later state, invoke handlers, or call an API as a substitute for the user route. Use optional read-only diagnostics to corroborate a specific observation, recording how that evidence was obtained.

## Follow properties into the behavior they govern

Treat a saved setting as the start of an investigation, not its conclusion. First verify the configured value through the normal UI; then perform the workflow that should consume it.

Determine where the effective value comes from: an object property, project default, account setting, inherited value, or explicit override. Check displayed inheritance indicators and relevant documentation. Do not assume a universal precedence rule or equate an unset value with false. Distinguish a stored local value from the effective value used by the operation.

Check when the property takes effect. A default may apply only to newly created objects; another setting may affect existing objects when they next run. Determine whether the value is copied at creation, resolved when an action occurs, or applied through a later process. When documentation does not settle this, record the question rather than assuming retroactive behavior.

For example, if project documentation says an inherited review requirement sends newly submitted tasks to review, save that requirement, create an eligible task, and submit it as the relevant role. Verify both the saved setting and the resulting task state. If it becomes completed instead, report that mismatch. Check an existing task or explicit override only when needed to establish applicability; do not assume every task shares the failure.

## Follow branches, order, and recovery

Choose branches by their consequences: valid versus invalid input, allowed versus unavailable action, acceptance versus cancellation, and successful versus interrupted completion. Check whether permissions differ for initiating an action, seeing its outcome, and performing the next step.

Investigate order when it could change meaning: setting a property before or after creation, changing a selection before confirmation, or editing while another step is pending. Follow Cancel, Back, correction, retry, and resume when relevant. Check whether partial work survives as promised and whether abandoned work causes unintended later effects.

For long journeys, preserve checkpoint evidence, object identities, actors, and outstanding operations. Resume from a known state rather than silently recreating a different object. When another role or device is unavailable, mark that handoff untested and continue useful reachable work.

Use authorized test records and actions. Repeat operations only when repetition is safe within the existing authorization. Establish whether a prior mutation occurred before retrying it; do not create duplicate sends, purchases, or destructive effects to improve reproduction statistics.

## Probe transitions and their history

When a lifecycle or workflow presents a concrete risk, extend the working map with the relevant starting state, event, guard or prerequisite, expected next state, and expected effects. Derive allowed and forbidden transitions from applicable evidence. An action missing from the current screen alone does not establish a universal business rule.

- **Forbidden transitions:** Select consequential attempts, such as editing a finalized record or resubmitting a cancelled request, only where the normal user route permits an attempt. Check rejection feedback, retained state, and relevant non-effects. Do not force disabled controls, bypass guards, or invent an API route to make a case reachable.
- **Isolate rejected attempts:** Start each selected invalid attempt from a known state. Verify its result before proceeding; separate attempts when an earlier failure could alter the prerequisites or hide another defect. If the attempt is unavailable, record the observed restriction and leave any unobserved enforcement unverified.
- **Transition pairs:** Exercise a meaningful pair consecutively when the second action could depend on how the first changed state. Testing both actions independently does not test their interaction. Look for retained approvals, counters, selections, or pending work that should change according to the contract.
- **Round trips:** Where supported and authorized, return through a reversible path such as submit → withdraw → submit. Check documented reset and retention behavior; do not assume the returned state must erase its history or exactly match a newly created object.

For example, if withdrawing a submission is documented to invalidate its approval, a later submission should require the appropriate review again. Observe each checkpoint and the consuming action; a return to the same status label does not establish that the old approval was cleared.

Record the states, individual transitions, selected pairs or round trips, and rejected attempts actually exercised. Keep blocked, unavailable, and untested cases distinct. Reaching every state does not establish coverage of every transition or sequence; choose further probes only to resolve a material risk or uncertainty.

## Compare conditions without overstating causality

When needed, compare two suitable cases while changing one relevant property or condition. Keep the role, object type, lifecycle state, build, relevant data, and timing comparable. Record unavoidable differences and configuration changes. Restore only test state you are authorized to change.

Start with the smallest comparison that can resolve the question. Expand only if the result leaves a material uncertainty. A different outcome after a setting change supports an association; it does not establish an implementation cause. Check plausible alternatives such as an override, cached state, different eligibility, concurrent activity, or a delayed process before attributing the discrepancy.

## Respect asynchronous timing

Read the product's timing promise, prerequisites, timezone, calendar, and business-hours rules where relevant. Record the trigger and observed times. Distinguish pending, queued, failed, and completed states using available evidence; a spinner or absent result alone may not settle which applies.

Use a documented deadline when one applies. If no delay or service target is specified, do not invent one. Observe within the mission budget, then report the elapsed observation window and unresolved outcome. If completion falls beyond the session, mark that step unverified. Do not claim failure solely because the session ended, or accelerate a process by changing time or system state without authorization.

## Report the first divergence and stop responsibly

Use [findings.md](findings.md) to report the earliest established mismatch: given these prerequisites and this action or value, the applicable expectation was A, but the observed result was B. Preserve the preceding successful checkpoints and the evidence for the divergence.

State which downstream consequences were observed and which remain inferred. Distinguish a wrong saved value, a correct value consumed incorrectly, misleading feedback, and unresolved intent. Avoid claiming every branch fails from one example. Stop when the evidence supports an actionable finding or a clear uncertainty; report the paths, roles, configurations, and handoffs examined, blocked, or left untested.
