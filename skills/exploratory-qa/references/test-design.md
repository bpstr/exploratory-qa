# Choose revealing manual test cases

Use this guide when the active charter needs a better choice of inputs, rules, or combinations. Derive a few useful probes from the product's expectations, then execute them through its normal interface. Keep the authorized scope, available environments, and evidence rules in [SKILL.md](../SKILL.md).

## Choose a technique for the question

| Question or risk | Useful technique | Start with |
| --- | --- | --- |
| Different kinds of input should receive different treatment | Equivalence partitioning | A representative of each relevant valid or invalid class |
| Behavior changes at a documented limit | Boundary value analysis | Values immediately around that limit in the product's actual units |
| Several conditions jointly determine an outcome | Decision table | The distinct rules, their expected outcomes, and uncertain combinations |
| Several configurations may interact | Combination selection | Known risky combinations, then uncovered pairs where useful |
| The same action may behave differently after earlier actions | State and sequence probes | Relevant allowed, forbidden, and consecutive transitions from [workflows.md](workflows.md) |

Combine techniques when the question warrants it: a decision-table rule involving a quantity can also need a boundary probe. Do not run every technique for every charter. These adaptations draw on [ISTQB CTFL v4.0.1, §4.2](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf) and [CTAL-TA v4.0, §3.1.2](https://astqb.org/assets/documents/ISTQB-CTAL-TA-Syllabus-v4.0-EN-4.pdf).

## Partition inputs by expected behavior

Identify the input and the rule that determines its treatment. Separate classes only where a meaningful difference is expected: accepted, rejected, normalized, restricted to a role, or interpreted as an omitted value. Do not assume that empty, whitespace-only, missing, and a displayed default mean the same thing.

- Choose a concrete representative for each relevant class and state its expected outcome and basis.
- Keep other required inputs valid when testing a rejection, so an unrelated error does not conceal the behavior under investigation.
- Include realistic content where its shape matters: accented names, multiline text, duplicate names, or a referenced object that is no longer available. Explain why that case belongs to the mission.
- Treat the grouping as a model. If two supposedly equivalent inputs behave differently, investigate whether the rule, partition, or product is wrong.

Equivalence partitions group values by expected processing; they do not establish that one successful example proves every value works. See [ISTQB CTFL, §4.2.1](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf).

## Probe boundaries in the product's units

Establish the limit, whether it is inclusive, and the smallest meaningful change. For a fictional maximum of **64 selected records**, compare **63, 64, and 65** when those selections can be created through the authorized interface. Inspect the selection, explanation, attempted action, and affected records; acceptance alone does not establish the correct scope.

For other domains, determine the relevant unit before choosing neighbors: characters or bytes, accepted monetary increments, calendar dates or instants, and displayed precision or stored precision. Do not apply a universal increment or arbitrary floating-point epsilon. If the boundary or its unit is unknown, record that uncertainty instead of inventing a validation rule.

Check available lower bounds and distinct empty or missing cases when they address a real risk. Content-length and collection-size limits can matter even when text is free-form. If the interface prevents entering the next value, record that restriction and what it demonstrates. Distinguish prevention at input from rejection after submission; do not bypass the normal route or infer validation at later steps.

Boundary analysis applies to ordered partitions; adjacent values must reflect that domain. See [ISTQB CTFL, §4.2.2](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf).

## Make interacting rules explicit

List the conditions that affect the outcome, the resulting actions, and the source supporting each rule. Start with a small table for the relevant decision. Split a compound condition when its parts could change the expected result independently. Preserve an unknown outcome as a product question; current behavior cannot supply its own independent expectation.

Distinguish three cases before reducing the table:

- **Irrelevant:** changing this condition does not change the expected outcome under the stated rule. Mark it with a dash and retain the justification.
- **Impossible:** the conditions cannot coexist in the modeled domain. Record the constraint and check its applicability; verify the relevant restriction through the UI when useful and possible.
- **Expected rejection:** the conditions can occur, but the attempted operation should be refused. Keep this as a negative case, including the expected unchanged state.

Merge cases only where the justified outcomes are equivalent. Select by risk when the table becomes large, and record what remains unexamined. A full Cartesian expansion is not a prerequisite for useful exploration. See [ISTQB CTFL, §4.2.3](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf).

### Fictional example: starting a task

Assume an applicable requirement states that only a permitted actor can start a task in **Ready**. If the project's effective **Require estimate** setting is enabled, that actor must provide an estimate before starting. A rejected start leaves the task in Ready and explains the missing prerequisite; an accepted start changes it to In progress. These are invented rules for this example, not findings or default requirements for other products.

| Actor permitted to start | Estimate required | Estimate present | Expected result |
| --- | --- | --- | --- |
| No | — | — | Start is unavailable or rejected under the documented permission behavior; task stays Ready |
| Yes | Yes | No | Start is rejected with an estimate explanation; task stays Ready |
| Yes | Yes | Yes | Task enters In progress |
| Yes | No | — | Task enters In progress |

For each selected case, verify the actor, same object's starting state, and effective setting before acting; inspect the resulting state after ordinary retrieval. Choose concrete values for dash entries and record which were exercised. Do not claim that one representative exercised every underlying combination. Keep the rejection rows: they are meaningful cases, not impossible configurations. If Start is unavailable to the role, record that UI behavior without forcing the action.

**Counterexample:** the requirement governs starting a Ready task. An already active task that remains In progress after the setting is enabled does not contradict this rule. A retroactive requirement would need its own evidence. Do not broaden the expectation merely because the setting's name sounds general.

## Select combinations without inventing coverage

List the relevant factors and feasible values, such as role, object state, effective configuration, locale, or input method. Use only environments and accounts actually available. Start with a representative working configuration, known problematic combinations, and the interactions suggested by the requirements or observed failure.

Where many combinations remain, choose cases that cover new pairs of factor values. Keep important combinations involving more factors explicitly: a rule depending on role, state, and setting requires those conditions together even if every pair appeared elsewhere. Pairwise selection is a sampling technique, not a guarantee of defect detection. Do not wait for an escaped defect before investigating a known interaction risk. The primary treatment is [ISTQB CTAL-TA, §3.1.2](https://astqb.org/assets/documents/ISTQB-CTAL-TA-Syllabus-v4.0-EN-4.pdf).

Exclude only genuinely infeasible combinations. A restricted feature attempted by an ineligible role can be a valuable rejection case. Do not label a manually chosen sample “complete pairwise coverage” unless the defined factors, values, constraints, and all required pairs were actually checked. Report the combinations exercised and the gaps when that accounting would add unnecessary work.

## Preserve evidence and stop when the question is resolved

For each useful probe, retain the condition or value, expectation and basis, starting state, normal action, and observed result. Link the evidence to the case actually exercised. Distinguish cases planned, examined, blocked, and left untested; a completed design table is not an execution record.

Use [findings.md](findings.md) to investigate a discrepancy and report its impact. Expand the sample only to resolve a material uncertainty, isolate a relevant condition, or assess an evidenced risk. Stop once the finding or uncertainty is actionable, or the mission budget is reached. Carry remaining cases into the coverage limits rather than turning them into an automatic rerun. See [sources.md](sources.md) for the broader methodological and evidence boundaries.
