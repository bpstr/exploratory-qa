# Inspect the product as a user

Use this guide for the active investigation in [SKILL.md](../SKILL.md).
Choose probes that address an observed inconsistency or a relevant product risk; do not expand them into a compulsory matrix.

## Contents

- [Establish the expected experience](#establish-the-expected-experience)
- [Explore from a specific user's perspective](#explore-from-a-specific-users-perspective)
- [Read the interface carefully](#read-the-interface-carefully)
- [Compare small visual details](#compare-small-visual-details)
- [Follow routes and controls](#follow-routes-and-controls)
- [Inspect sequences, persistence, and recovery](#inspect-sequences-persistence-and-recovery)
- [Follow data through its lifetime](#follow-data-through-its-lifetime)
- [Check input and accessibility behavior](#check-input-and-accessibility-behavior)
- [Observe actual screen-reader journeys when available](#observe-actual-screen-reader-journeys-when-available)
- [Describe platform coverage honestly](#describe-platform-coverage-honestly)
- [Turn observations into justified findings](#turn-observations-into-justified-findings)

## Establish the expected experience

- Identify the user's goal, role, current state, and relevant product documentation before judging the screen.
- Consult [project-context.md](project-context.md) when terminology, supported behavior, or requirements are unclear.
- State the expectation before the probe: what should this action accomplish, and what evidence would demonstrate it?
- Use documented behavior, an approved design, or a comparable working flow as the basis; retain conflicting evidence.
- Preserve the initial screen and exact state before interacting with a suspected failure.
- Use only available tools and authorized accounts, data, and actions; record missing capabilities as coverage limits.

## Explore from a specific user's perspective

Choose a plausible user, goal, starting knowledge, and entry point when they expose a relevant risk. Ground these in the product's audience and documentation; invented personas are investigation aids, not evidence from user research.

- Compare what a novice must discover with what a returning user may reasonably remember. Does the interface expose the next action, explain its consequence, and make completion recognizable without unstated team knowledge?
- Derive a scenario from that person's goal and constraints: for example, a recipient follows an observed notification link without having seen the creator's setup. Use an available, authorized link rather than constructing a guessed route.
- Consider affected people who do not operate the current screen, such as an approver, report reader, or notification recipient. Follow their side of the handoff only with authorized access; otherwise record the untested perspective.
- Describe observed misleading cues, missing information, or extra work. A simulated novice perspective supports a usability hypothesis; it does not prove that real users are confused or establish a failure rate.

## Read the interface carefully

- Read the encountered interface in visual order; do not scan only headings and primary buttons.
- Read labels, body text, navigation, captions, badges, units, footnotes, and inline links.
- Reveal relevant tooltips, help text, menus, and expanded descriptions through their normal interactions.
- Inspect placeholders separately from persistent labels and entered values; check whether necessary instructions disappear during entry.
- Read validation errors, empty states, loading messages, success messages, and recovery instructions when those states occur.
- Compare each message with the current state: does it describe the right object, action, actor, and result?
- Compare action wording with its consequence: distinguish saving a draft, publishing, deleting, archiving, and leaving a view.
- Check whether instructions refer to controls, settings, or destinations that exist and are reachable for this role.
- Trace one concept through navigation, page title, dialog, button, and confirmation; investigate unexplained terminology changes.
- Check spelling, grammar, punctuation, capitalization, duplicated words, and leftover placeholder or debug text.
- Respect product vocabulary, proper names, and user-authored content; do not substitute stylistic preferences for errors.
- Record the locale and your language confidence; verify uncertain language judgments before proposing corrections.
- For Hungarian content, inspect relevant accents such as `ő` and `ű`; apply equivalent language-specific care only to supported locales.
- Check untranslated strings and language mixing against the documented localization policy, including intentional brand terms.
- Reconcile counts, totals, currencies, units, date formats, and time zones with the shown filters and documented meaning.
- Distinguish a page count, loaded subset, and overall total before reporting inconsistent numbers.
- Inspect truncation and wrapping for lost meaning, hidden distinctions, clipped accents, or an inaccessible complete value.
- Quote verified visible text exactly, preserving punctuation and accents; mark omitted or illegible portions explicitly.
- Label evidence as screenshot, visible text read through the browser, DOM extraction, accessibility text, or OCR transcription.
- Verify suspected OCR mistakes against the image; do not report the recognizer's guess as product copy.
- Do not claim DOM or accessibility text is visible unless the rendered interface confirms it; record discrepancies separately.

## Compare small visual details

- Compare paired examples of the same component, purpose, and state before calling a difference inconsistent.
- Align locale, role, theme, content length, loading state, zoom, and viewport when those factors affect the comparison.
- Inspect spacing, alignment, typography, icon meaning, border treatment, emphasis, and the placement of related actions.
- Inspect clipped text, overlapping elements, hidden controls, misplaced tooltips, broken images, and unintended scroll containers.
- Check whether selected, disabled, loading, hovered, and focused states remain distinguishable where relevant.
- Check whether the apparent hit area matches the usable control and whether neighboring controls invite accidental activation.
- Inspect long labels, realistic names, and populated content when the available fixtures support them.
- Follow a suspected wrapping or overflow problem across the nearest relevant width change; avoid exhaustive viewport sweeps.
- Inspect overlays against sticky headers, footers, dialogs, and scroll boundaries in the actual affected state.
- Observe changes during loading and interaction; a settled screenshot cannot establish whether content flickered or jumped.
- Capture a short sequence or recording when timing or movement is material and the tool supports it.
- Allow intentional platform conventions and responsive rearrangement; compare meaning and task completion, not identical pixels.
- Describe the contradiction and its consequence; exclude unsupported preferences about attractiveness or fashionable styling.
- Call a problem a regression only when a comparable prior version or approved baseline supports that claim.

## Follow routes and controls

- Discover controls through the rendered interface and follow actual destinations; do not invent routes from naming patterns.
- Inspect the visible label and surrounding explanation before activating a control.
- Verify the resulting page, state, download, dialog, or other promised outcome; a successful click is not completion.
- Check an apparent dead end for an unnoticed new tab, blocked popup, delayed response, permission explanation, or offscreen feedback.
- Observe enabled and disabled behavior through normal pointer, touch, or keyboard input supported by the environment.
- Do not use forced clicks, script-invoked handlers, removed overlays, or altered permissions to establish user accessibility.
- Preserve a failed normal interaction even if a diagnostic tool can subsequently reach the underlying element.
- Inspect Back, Cancel, close, and return navigation when they matter to the user's task.
- Check whether the return path preserves the expected selection, filters, scroll position, or draft according to product behavior.
- Exercise only authorized consequences; use appropriate test records for destructive or externally visible actions.

## Inspect sequences, persistence, and recovery

Use [workflows.md](workflows.md) to discover longer journeys, conditional actions, and settings whose effect appears in a later operation or another view.

- Follow the full relevant sequence: starting state, action, immediate feedback, settled result, and later retrieval.
- Compare the actual transition with the promised one: opening a menu, saving a draft, submitting for review, and publishing are different outcomes even if each produces visible activity.
- Verify a reported save by reopening or reloading the affected record when persistence is in scope.
- After a property persists, exercise the relevant workflow that consumes it. Check the effective scope and any override before judging whether the property changed the behavior correctly.
- Check that another relevant view agrees with the result; investigate stale labels, badges, totals, and selections.
- Explore interruption, repeated input, or changed action order only when it tests a plausible risk in this flow.
- After validation fails, correct the input and check that errors clear, retained data remains, and submission becomes possible.
- After a failed operation, inspect whether retry is discoverable and whether it duplicates or loses work.
- Where supported and authorized, inspect a relevant slow, interrupted, expired-session, or offline transition and recovery.
- Distinguish immediate feedback, asynchronous completion, and durable success; respect documented eventual consistency.
- Record timing and repeat conditions for intermittent failures; do not label an unrepeatable observation as disproved.
- Stop repeating a sequence once the evidence resolves the current question; broaden only to investigate a concrete remaining risk.

## Follow data through its lifetime

When a record's age or relationships could change its meaning, follow one identifiable test object across the relevant views and events. Preserve its identity, original values, linked objects, and observation times; a similar replacement is not the same history.

- Compare existing or historical records with newly created records only when the distinction matters. Record creation context and applicable rules instead of assuming current defaults apply retroactively.
- Inspect a relevant relationship after an authorized rename, reassignment, or deactivation, or use an existing fixture in that state. Check whether references still identify the intended object and whether historical views preserve the meaning promised by the product.
- Follow the same record into supported search results, reports, exports, or recipient views when those are in scope. Distinguish a historical snapshot from a live value before judging a difference.
- Inspect archive, restore, or deletion behavior only where supported and authorized. Check documented effects on references and history; do not assume restoration reverses every effect or recreate deleted data to make an observation look consistent.
- If the product does not specify whether a historical label should remain fixed or reflect a later rename, report that ambiguity with both observations rather than declaring either behavior correct.

## Check input and accessibility behavior

- Navigate the relevant flow by keyboard where supported; observe order, visible focus, activation, and escape paths.
- Inspect dialog entry, contained focus, background interaction, close behavior, and logical focus restoration.
- Use the [W3C modal dialog pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/) as applicable guidance, accounting for its workflow exceptions.
- Inspect whether sticky content or overlays hide the focused control; capture the actual focused state.
- Inspect zoom and narrow-layout behavior for lost information or function, not merely a changed arrangement.
- Apply [W3C reflow guidance](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html) with its exceptions for content needing two-dimensional layout.
- Distinguish browser zoom, text enlargement, viewport resizing, and screenshot scaling; report what was actually changed.
- Check whether instructions depend on hover, color, shape, or position alone when that dependency affects the task.
- Inspect reduced-motion behavior only when the environment exposes that preference and movement can be observed.
- Use accessibility-tree or DOM evidence to investigate semantics, but do not claim it demonstrates a screen reader's actual announcements.
- Name the specific observed barrier; do not turn a limited inspection into an accessibility conformance verdict.

## Observe actual screen-reader journeys when available

Use this optional probe when a compatible screen-reader, browser, and platform are available and the environment permits observing their actual output. Name the combination and relevant mode or settings; if access, compatibility, or output cannot be established, mark the journey untested.

- Choose a relevant user goal and follow the reader's normal navigation and activation methods. Compare the encountered names, roles, and states with the control's purpose and applicable expectations; allow reader-specific wording and verbosity.
- Observe whether validation, completion, and other important state changes become perceivable, and whether focus moves or returns meaningfully after dialogs and navigation. Use the product's timing promises where applicable; do not invent a universal announcement deadline.
- Record the action, expected semantic information, actual announcement or captured output, and its effect on task completion. Distinguish observed speech, an actual speech-output log, and underlying accessibility-tree text.
- Preserve unavailable or inconclusive steps as coverage gaps. A tree inspection, visible toast, or authored script does not demonstrate what a screen reader announced, and one journey does not establish accessibility conformance.

## Describe platform coverage honestly

- Record the actual OS, browser or engine, viewport, zoom, input method, locale, theme, and relevant product version when available.
- Label each environment as actual desktop, emulated mobile, simulator, or physical mobile device; state unknown details.
- Do not infer real-device behavior from a mobile viewport or infer branded Safari coverage from a WebKit run.
- Investigate software-keyboard occlusion, native dialogs, safe areas, rotation, and background/resume only where the environment exposes them.
- Compare the supported platform's expected conventions with its observed behavior; do not impose desktop interactions on touch interfaces.
- State unavailable platform checks explicitly instead of fabricating observations or silently marking them passed.

## Turn observations into justified findings

- Follow [findings.md](findings.md) to separate evidence, expectation, impact, confidence, and unresolved questions.
- Include exact copy and a comparable example when they explain the defect; retain enough screenshot context to locate it.
- Match each finding to the applicable documentation or other stated expectation; describe uncertainty when that basis is incomplete.
- Use [Nielsen's usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) to generate questions, not automatic defect verdicts.
- Report the inspected scope and remaining uncertainty; never convert an uneventful sample into a claim that the product has no defects.
