# Match observations to project context

Ground expectations in the product being tested. Use the [product context template](../assets/product-context-template.md) to retain the relevant context without loading every document into the session.

## Establish the scope

- Identify the application, repository, project, workspace, and tested build where available. Distinguish the deployed build from the local checkout.
- Read applicable repository instructions and documentation indexes. Locate requirements, acceptance criteria, designs, terminology guides, and decisions relevant to the current mission.
- Search the corresponding project before expanding to workspace guidance. Expand when behavior is shared, a project document points elsewhere, or a targeted search leaves a material question unanswered.
- Use available authorized document connectors for workspace sources. Record unavailable sources; do not infer that inaccessible documentation does not exist.
- Follow relevant links selectively. Do not search unrelated projects merely to find language supporting a suspected defect.

## Search from the observation

Start with exact visible text, then search the feature and domain concepts. Preserve spelling, punctuation, and locale in the evidence even when using broader search terms.

Adapt these examples to existing documentation paths in the relevant repository:

```sh
rg --files -g '*.md' -g '*.mdx' -g '*.rst' -g '*.adoc'
rg -n -F 'Delete all' docs/
rg -n -i 'bulk (delete|remove)|pagination|selected items' docs/
```

- Prefer literal search for a distinctive label or error. Expand to synonyms when labels have changed or requirements use business terminology.
- Retrieve the actual matching passage and enough surrounding context to understand its conditions. Do not base a finding on search snippets alone.
- Inspect linked acceptance criteria or decisions when they can resolve the expectation. Avoid reading whole document collections without a specific question.
- Bound discovery to the mission budget. Record searched locations and meaningful terms when no applicable source is found; continue investigating observable behavior.

## Check applicability and provenance

For every documentary expectation, record:

| Field | Record |
| --- | --- |
| Source | Repository path or canonical workspace URI, plus heading or section. |
| Passage | A short relevant excerpt or faithful paraphrase; preserve qualifications. |
| Revision | Available commit, document revision, or update date. Mark unknown values explicitly. |
| Applicability | Feature, role, lifecycle state, platform, locale, configuration, and version conditions that matter. |
| Relationship | Explain how the passage supports, contradicts, or leaves open the expected behavior. |

Check that a similarly named feature actually refers to the tested behavior. Do not apply administrator requirements to a viewer or a future roadmap to the current release. Treat age as a reason to check applicability, not proof that a document is stale.

## Handle the documentary result

| Status | Required response |
| --- | --- |
| Applicable | Explain the specific mismatch between the passage and the observation. |
| No match | State that the scoped search found no applicable documentation. Do not claim that none exists. |
| Unavailable | Identify the missing access or source and the resulting uncertainty. Keep this distinct from no match. |
| Apparently stale | Explain the version or decision mismatch; do not silently choose the source that supports the finding. |
| Conflicting | Retain both passages and their scopes. Explain whether the conflict can be resolved; otherwise record a product question. |

Do not require a document before reporting a demonstrated failure. A control's explicit promise, a failed user operation, established equivalent behavior, or an applicable standard can justify an expectation. Name that basis and its limits.

Treat source code, existing tests, and current implementation as diagnostic evidence. They can show what was implemented or checked; they do not independently prove what users should receive. A test accepting a misleading success message does not settle whether that message is correct.

Resolve expectations against explicit current user instructions and applicable product decisions. When intent remains uncertain, retain the uncertainty instead of inventing precedence. A documentation conflict can coexist with an independently demonstrated defect.

## Read the interface as product content

- Read headings, labels, helper text, placeholders, empty states, validation errors, notifications, and confirmation dialogs during their actual use.
- Compare terminology across related screens and corresponding documentation. Check entity names, counts, units, dates, selection scope, and instructions for recovery.
- Evaluate wording together with its effect: what does the button promise, what does the action affect, and does the feedback describe the result accurately?
- Record concrete language defects even when their impact is minor. Use the applicable locale and terminology guide; do not invent a preferred writing style.
- Distinguish a verified mismatch from optional editorial taste. Explain the ambiguity or consequence when calling wording confusing.

For example, investigate whether “Delete all” means all selected records, all visible records, or all matching records. Compare the actual affected set with the relevant requirement and confirmation text. If the sources disagree, record the conflict while still reporting any independently observed loss or misleading feedback.
