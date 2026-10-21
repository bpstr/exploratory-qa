# Exploratory QA

**Find subtle product problems, read the interface carefully, and justify findings with evidence and relevant project documentation.**

Investigate whether the product behaves coherently for its intended users. When something is surprising, preserve the evidence, identify the expectation it contradicts, and investigate before declaring a defect.

An Agent Skill for exploratory product QA: workflow discovery, close reading, visual inspection, interaction testing, and evidence-based judgment. It helps an agent notice confusing copy, subtle inconsistencies, broken journeys, and unexpected behavior, then establish whether each observation warrants a finding. It also traces complex sequences and checks whether actions and settings produce their intended effects.

The skill uses the agent's existing browser or computer-use tools. It includes a workflow, reference material, and reporting templates; it does not bundle an application controller, test runner, browser, or model.

## What it inspects

| Area | Questions to investigate |
| --- | --- |
| Text and meaning | Do headings, labels, descriptions, placeholders, validation messages, and confirmations agree? Are names, units, dates, counts, and terminology consistent? |
| Visual details | Is text clipped or obscured? Do spacing, alignment, icons, contrast, and component states make sense in context? |
| Actions and destinations | Does a button or link deliver what its wording promises? Is the result visible, useful, and reachable through the normal interface? |
| Complex workflows | Which prerequisites, states, branches, and role handoffs lead to the user's goal? Does each action make the intended transition? |
| Properties and dependent behavior | Does a saved setting affect the operation that uses it? Are scope, inherited defaults, overrides, and activation conditions respected? |
| Interaction and recovery | What happens after cancellation, repeated activation, invalid input, interrupted work, or navigation back? Can the user recover? |
| State and persistence | Does a successful change survive reload or a return visit? Do related views and accounts reflect the same underlying result? |
| Platforms and input | Does the journey remain coherent across available viewport sizes, themes, locales, zoom levels, and keyboard or pointer input? |
| Product expectations | Does the observed behavior agree with applicable project documentation, workspace decisions, supported features, and user-facing promises? |

Every encountered screen deserves attention, including menus, dialogs, empty states, errors, and confirmations. The agent should read their visible copy and inspect their layout, rather than only locating the next control. Screenshots and interaction history supply evidence; DOM, accessibility, network, API, or data inspection can strengthen a finding when those tools are available and authorized.

## How an investigation works

1. **Establish scope.** Identify the product, intended users, meaningful journeys, available environments, and exploration budget. Respect the user's existing authorization and project instructions.
2. **Understand the product.** Read relevant project and workspace material, record important expectations, and identify risks and unresolved questions.
3. **Explore deliberately.** Follow realistic journeys, vary relevant conditions, and inspect each resulting state. Record a surprising outcome before trying a workaround.
4. **Investigate the surprise.** Preserve observations, identify the expectation involved, and distinguish product behavior from tool limitations or environmental failures.
5. **Confirm and classify.** Reproduce where practical, check relevant documentation, remove duplicates, and separate demonstrated defects from uncertainty or usability concerns.
6. **Report the evidence.** Explain the user impact, what was inspected, what remains untested, and the next useful action. A completed journey alone does not establish that every step was healthy.

Exploration is bounded by risk and available evidence. Additional checks should answer a concrete question; repeated clicks and a large volume of reports are not measures of quality.

## Discover workflows and check their meaning

The agent should discover relevant journeys through the interface and project documentation, including contextual actions, conditional branches, and steps revealed only after an earlier choice. It keeps a small map of the user's goal, actors, objects, states, prerequisites, and expected outcomes, updating it as new behavior becomes visible.

Before a meaningful action, it establishes what that action should do. Clicking **Save draft**, **Submit for review**, and **Publish** may all produce a confirmation, but they promise different states and consequences. The agent checks the resulting object and relevant downstream view, then explains any difference between the promised and observed outcome.

For properties, the investigation follows the full chain:

1. Establish the original state and the applicable requirement or UI promise.
2. Change the property through the normal interface and verify its effective saved value.
3. Check its scope, inherited defaults, overrides, and whether it applies to existing or newly created objects.
4. Exercise the workflow that should use the property and observe its actual effect.
5. Report the first observable divergence: **under these conditions, the setting or action should cause A, but the evidence shows B**.

For example, if an applicable requirement says **Require approval** makes an author's submission enter review, an enabled and persisted toggle is only part of the evidence. The agent must follow a qualifying submission and inspect whether it enters review or becomes published. It should also check whether the account, content type, or an explicit override legitimately changes that expectation.

Relevant probes include alternative branches, action order, cancellation, retries, interrupted work, and authorized role handoffs. Controlled comparisons help isolate a change without assuming that correlation proves its implementation cause. Asynchronous work is assessed against applicable timing and completion signals; an unknown delay is reported as uncertainty. The [workflow guide](skills/exploratory-qa/references/workflows.md) provides the detailed method.

## Ground findings in project context

The skill checks relevant workspace and project documentation before drawing conclusions about product-specific behavior. Useful sources include requirements, acceptance criteria, design decisions, terminology guides, supported-platform policies, and documented exceptions.

A document title or search snippet is insufficient. Read the actual passage, retain its location and provenance, and check whether it applies to the observed feature, role, platform, version, and state. Current implementation and existing tests are evidence, but can preserve an error; neither automatically defines intended behavior.

For each finding, make the documentation status explicit:

| Status | Meaning |
| --- | --- |
| **Applicable** | A retrieved passage supports an expectation and applies to the observed conditions. |
| **No match** | The scoped search found no relevant passage; record what was searched. |
| **Unavailable** | A relevant source could not be accessed; explain the resulting uncertainty. |
| **Apparently stale** | Evidence suggests the passage may no longer describe the relevant product state. |
| **Conflicting** | Relevant sources disagree; preserve both positions and identify what needs resolution. |

Documentation is not required to establish every defect. A control labeled “Download CSV” that repeatedly downloads an unrelated image can contradict its own visible promise. Conversely, a feature the agent would prefer is not a defect merely because it is absent. Where expectations remain ambiguous, report the question or concern without inventing a requirement.

## Install

Use a skill-compatible agent and **Node.js 22.20 or later with npm/npx**. Browser or computer-use capabilities must already be available to the agent for live inspection. The Skills CLI installation command is `add`:

From the project you want to review:

```bash
npx skills add bpstr/exploratory-qa --skill exploratory-qa
```

The installer lets you choose an agent. To select one explicitly:

```bash
# Codex
npx skills add bpstr/exploratory-qa --skill exploratory-qa --agent codex

# Claude Code
npx skills add bpstr/exploratory-qa --skill exploratory-qa --agent claude-code
```

Installation is project-scoped by default. Add `--global` to make the skill available across projects:

```bash
npx skills add bpstr/exploratory-qa --skill exploratory-qa --agent codex --global
```

Inspect availability and maintain the installation:

```bash
# Discover this repository's skills without installing them.
npx skills add bpstr/exploratory-qa --list

# Inspect installed skills and available updates.
npx skills list
npx skills list --global
npx skills check

# Update only exploratory-qa in the chosen scope.
npx skills update exploratory-qa --project
npx skills update exploratory-qa --global
```

Installation syntax and runtime requirements follow the [official Skills CLI reference](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) and [CLI README](https://github.com/vercel-labs/skills#readme), checked against version 1.7.4. Agent installation locations and optional feature support vary; consult the [supported agents documentation](https://github.com/vercel-labs/skills/blob/main/docs/agents.md). Installing instructions does not grant additional tool capabilities or access.

## Use

Ask your agent to use `exploratory-qa`, supplying the application or environment and the area to investigate. In agents that support explicit skill invocation, use `$exploratory-qa`:

```text
Use $exploratory-qa to explore the account settings flow in our staging app.
Read the encountered UI text and match findings to relevant project docs.
Report evidence, expected behavior, user impact, and remaining uncertainty.
```

Include documentation locations or a baseline when available. The [product context template](skills/exploratory-qa/assets/product-context-template.md) can help, but is not a prerequisite for starting useful work.

**Explore a feature:**

> Use exploratory-qa to investigate project settings in the running staging app. Read the relevant requirements and workspace decisions first. Inspect all encountered text, dialogs, empty states, and interactions. Investigate surprising results and report justified findings with evidence, documentation status, and remaining gaps.

**Compare a change:**

> Use exploratory-qa to compare the supplied baseline and current build for the document editor. Focus on layout, wording, keyboard behavior, and persistence across reloads. Distinguish confirmed regressions from existing defects and intentional changes. Record exactly which environments were exercised.

**Investigate a subtle inconsistency:**

> Use exploratory-qa to inspect the inconsistent archive behavior I observed. Compare the list, detail view, and confirmation copy against the project documentation. Determine what is observed, what is promised, and what still needs a product decision. Do not expand into unrelated testing.

**Discover a workflow and check a setting's effect:**

> Use exploratory-qa to discover the content approval workflow in our test workspace. Identify the relevant roles, states, prerequisites, and branches from the UI and project docs. Investigate whether Require approval actually changes what happens after submission. Trace the same content item through the dependent views, and report where the expected transition differs from the observed result.

The skill can still review supplied screenshots or recordings when live interaction is unavailable, but should identify that reduced scope and avoid claiming behavior it could not observe.

## Findings contract

Each finding should let another person understand and investigate the problem without reconstructing the session:

- **Observation:** the exact wording, visible state, or behavior that raised concern.
- **Context and reproduction:** environment, prerequisites, relevant inputs, and a concise sequence of actions.
- **Expectation and basis:** the promise, applicable requirement, consistency relationship, or other reason the outcome is questionable.
- **Workflow divergence, when relevant:** the prerequisites, effective property and scope, action sequence, expected effect, actual effect, and first observable mismatch.
- **Documentation reconciliation:** status, source location, relevant passage, applicability, and unresolved conflicts.
- **Impact and evidence:** who is affected, what becomes difficult or impossible, and linked captures or other recorded observations.
- **Classification and uncertainty:** finding category, severity, confidence, reproduction result, and a useful next step.

| Category | Use when |
| --- | --- |
| **Defect** | Observed behavior demonstrably contradicts a supported expectation. |
| **Suspected defect** | Evidence suggests a defect, but confirmation or an important condition is missing. |
| **Usability concern** | The observed experience creates a concrete difficulty without establishing a broken requirement. |
| **Product question** | Intent or conflicting expectations require clarification. |

Severity describes user impact. Confidence describes the strength of evidence. Priority reflects the product's decision about what to address first. Keep these separate; apply a supplied priority policy or leave scheduling to the responsible stakeholder. A suspected root cause must remain a hypothesis unless verified. Small verified copy or layout defects remain valid findings with proportionate severity.

## Package contents

| File | Purpose |
| --- | --- |
| [SKILL.md](skills/exploratory-qa/SKILL.md) | Activation guidance and investigation workflow |
| [Agent metadata](skills/exploratory-qa/agents/openai.yaml) | Codex interface metadata |
| [Inspection guide](skills/exploratory-qa/references/inspection.md) | Text, visual, interaction, state, and platform inspection |
| [Workflow guide](skills/exploratory-qa/references/workflows.md) | Journey discovery, expected actions, property effects, branches, and dependencies |
| [Project context guide](skills/exploratory-qa/references/project-context.md) | Documentation discovery, applicability, and reconciliation |
| [Findings guide](skills/exploratory-qa/references/findings.md) | Evidence, classification, and reporting rules |
| [Examples](skills/exploratory-qa/references/examples.md) | Worked examples and calibrated judgments |
| [Sources](skills/exploratory-qa/references/sources.md) | Research and methodological references |
| [Report template](skills/exploratory-qa/assets/report-template.md) | Session summary and individual findings |
| [Product context template](skills/exploratory-qa/assets/product-context-template.md) | Optional product-specific investigation context |

## Scope and contributions

This skill complements automated tests and specialist reviews. It does not establish exhaustive coverage, accessibility conformance, security assurance, or physical-device coverage from browser emulation. A visual difference requires a valid comparison before it can be called a regression. Report unavailable capabilities and untested conditions explicitly.

Detection effectiveness has not yet been established by a live-application benchmark. Contributions should improve observable judgment: provide a reproducible example, explain the expectation and user impact, and include a counterexample where similar behavior is intentional. Changes to guidance should preserve uncertainty, avoid turning preferences into requirements, and keep runtime references inside the installable skill directory. Evaluation contributions should measure confirmed findings and false positives, including missed defects and duplicate reports.

## License

[MIT](LICENSE).
