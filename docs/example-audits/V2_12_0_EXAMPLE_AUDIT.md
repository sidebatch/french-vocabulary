# TEF Vocab Loop v2.12.0 — Example Sentence Audit

## Scope
- Baseline: v2.11.4
- Total vocabulary cards audited: 2,866
- High-confidence example sentences changed: 583
- French (`exFr`), Korean (`exKo`), and English sidecar (`e`) updated together for all 583 cards.
- Card IDs, original Korean meanings, English meanings, cross-reference IDs, and learner-state structure were not changed.

## Main cleanup areas
- Repetitive home-object templates (`Je cherche ... dans la maison.`)
- Generic place/study `On parle de ...` templates
- Generic object templates (`Je regarde ... de plus près.`, `J'utilise souvent ...`)
- Generic food templates (`On trouve ... dans la cuisine.`)
- Generic personality templates (`Cet homme est ...`)
- Travel/transport boilerplate
- Country/nationality boilerplate
- Animal boilerplate
- Profession boilerplate
- High-confidence target-word sense mismatches

## Sense mismatches corrected
Examples include:
- `arrêter` (막다, 체포하다): bus stopping sense -> police arrest sense
- `vers` (~을 향하여): approximate-time sense -> direction sense
- `responsable` (책임이 있는): noun “person in charge” -> adjective construction
- `tendre` (부드러운, 상냥한): verb “extend” -> adjective “tender/gentle”

## Patterns verified as removed
- `Je cherche ... dans la maison.`: 0
- generic `On parle de/du/...`: 0
- `Je regarde ... de plus près.`: 0
- `J'utilise souvent ...`: 0
- `On trouve ... dans la cuisine.`: 0
- `Cet homme est ...`: 0
- `Je vérifie ... avant le départ.`: 0
- generic transport `J'ai vu ... ce matin.`: 0
- generic animal `J'ai vu un/une ... hier.`: 0

## Intentionally retained simple/template examples
A simple sentence was not changed merely because it was tagged `template`. Remaining template-tagged items are mainly:
- 58 number cards (`Ce nombre s'écrit en lettres : ...`)
- 28 ordinal cards (`C'est le premier/deuxième/... exemple.`)
- 22 month/date cards (`Nous sommes en janvier/...` etc.)
- topic examples in history, environment, current affairs, religion, and health that already carry useful context

## Structural QA
- Cards: 2,866 -> 2,866
- English sidecar entries: 2,866 -> 2,866
- Unique IDs: 2,866
- Broken `cf` references: 0
- Empty FR/KO/EN example fields: 0
- Original Korean meaning changes: 0
- English meaning changes: 0
- Non-example card-field changes: 0
- Changed FR example IDs == changed KO example IDs == changed EN example IDs: yes (583)
- JavaScript syntax check: passed
- HTML major opening/closing tag counts: balanced

## Notes
This was a full-corpus audit, not a forced rewrite of every sentence. Existing examples that were already useful were deliberately preserved. Ten exact duplicate example groups remain; they are ordinary, semantically appropriate sentences attached to closely related/duplicate concepts and were not changed only for the sake of uniqueness.
