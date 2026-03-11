# Scope and Handoff Rules

This file defines the boundary and handoff between three related skills.

## Role Split

- `find-skills`: discovery only. It finds candidate skills and installation options.
- `skill-fit`: decision only. It judges whether a candidate skill is worth installing for a specific user profile and task context.
- `skill-creator`: creation and iteration only. It creates or improves a skill after a decision is made.

## Hard Boundaries

1. Do not let `find-skills` produce "install / don't install" judgments.
2. Do not let `skill-fit` run broad ecosystem search as its default behavior.
3. Do not let `skill-creator` act as a selector when multiple candidate skills are still unresolved.

## Handoff Contract

### `find-skills` -> `skill-fit`

Pass:
- candidate skill name(s)
- short capability summary per candidate
- install source (skills.sh URL or package id)

When no candidate is found, stop and return "no candidate".

### `skill-fit` -> user

Return:
- one of: `RECOMMEND_INSTALL`, `OPTIONAL_INSTALL`, `DO_NOT_INSTALL`
- usage-scene tags
- value tags
- suitable-user tags
- unsuitable-user tags
- installation threshold and non-install fallback

### `skill-fit` -> `skill-creator`

If user still needs this capability but none of the candidates fit:
- recommend creating a custom skill
- provide why existing candidates fail for this profile or scene

## Conflict Resolution

If a user request mixes "find" and "judge":
1. run discovery first
2. ask if they want decision analysis
3. run decision analysis on top candidate(s)
