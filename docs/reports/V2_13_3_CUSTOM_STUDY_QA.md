# v2.13.3 Custom Study QA

## Scope
Full Custom Study QA across:
- Level: ALL / A1-A2 / B1-B2
- Topic
- Size: 10 / 20 / 30 / 50
- Focus: Auto mix / Meaning / Listening / Reverse / Spelling
- New mix: Auto / min 25% New / Review only
- session persistence / resume
- New introduction chains
- delayed tests / retries

A synthetic QA pass exercised **5,700 combinations**.

## Correct behavior confirmed
- Review only excludes truly New cards.
- Seen cards remain eligible for Review only because they have already been introduced.
- New25 is a minimum composition rule, not “every fourth screen”.
- Auto may contain zero New when Weak/Seen/Due backlog fills the target.
- New cards in Listening/Reverse/Spelling focus first receive introduction/basic meaning foundation.
- focus mode and new-policy survive saved-session resume.
- selected target IDs remain stable through resume.

## Finding 1 — Spelling focus could fall through
v2.13.3 allowed cards that were not eligible for spelling to enter a Spelling-focused session.
Those cards could then fall away from spelling inside review-skill selection.

Estimated spelling eligible:
- 2,167 / 2,866 eligible
- 699 ineligible

High-ineligible groups included:
- A1-A2 ADJECTIFS
- B1-B2 La profession
- B1-B2 L’adjectif
- A1-A2 TEMPS ET DATES
- A1-A2 LES PAYS

**Fixed in v2.13.4** by filtering the candidate pool in Spelling focus.

## Finding 2 — finite-session delayed spacing can collapse
A future retry/follow-up may be scheduled several logical turns later, but if there is no currently available task the finite selector can jump directly to the earliest future task.

Result:
“3–5 turns later” can become effectively immediate in real learner interactions, especially:
- narrow scopes,
- many New cards,
- New25,
- end-of-session retry tails.

**Still open in v2.13.4.**

## Finding 3 — duplicate semantic topics under Level = All
Raw source categories differ by level, for example:
- `LES VERBES` vs `Les verbes`
- `ADJECTIFS` vs `L’adjectif`
- `PRÉPOSITIONS` vs `Les prépositions`
- `L’ENDROIT` vs `L’endroit`
- `LA PROFESSION` vs `La profession`
- `OBJETS` vs `L’objet`

In English UI, some map to the same visible label while exact filtering still selects only one raw category.

Preferred fix:
canonical topic grouping layer, without rewriting source category strings.

**Still open.**

## Finding 4 — Meaning focus used an adaptive secondary skill
In v2.13.3, New/Seen chains could move from Meaning into Listening/Reverse/Spelling because Meaning had no forced secondary mapping.

Expected semantics were clarified:
- Meaning → intro → meaning → delayed meaning reconfirmation
- Listening → intro → meaning → listening
- Reverse → intro → meaning → reverse
- Spelling → intro → meaning → spelling
- Auto mix → adaptive secondary

**Fixed in v2.13.4.**

## Finding 5 — requested size may exceed available scope
Some exact level/topic pools contain fewer than 20/30/50 eligible cards.

Observed:
- all topic groups have at least 10
- 7 groups have fewer than 20
- 10 groups have fewer than 30
- 25 groups have fewer than 50

Example:
A1-A2 `LES INSTRUMENTS DE MUSIQUE` contains only 10 cards, so choosing 50 silently yields a smaller session.

Preferred UX:
available-count hint and/or disable impossible sizes.

**Still open.**

## Finding 6 — Review-only empty state is generic
If the selected scope has no introduced cards, the app currently gives a generic “no words” message.

Preferred wording:
“이 범위에는 복습할 단어가 없습니다.”

**Still open.**
