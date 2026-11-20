# ADR-002: Preset-Based Creation and Provisional Complexity Levels

- **Status:** Initial product direction accepted; details remain under research
- **Date:** 2026-11-21
- **Owner:** Gradient Lab project owner

## Context

Gradient Lab needs to serve people who want an appealing result without learning graphics terminology, while also supporting users who want to build original compositions.

The product owner proposed two ways to begin creating:
- Browse visual gradient families and choose from multiple pre-built compositions.
- Start from scratch in a blank creative workspace.

The product owner also proposed organizing presets into Basic, Medium, and Advanced levels for different practical needs and degrees of composition complexity. The classification is an initial hypothesis based on product vision and experience; research may improve it.

## Accepted initial product direction

### 1. Two creation entry points

**Explore gradient presets**
- The initial visual families are Aura, Mesh, Nebula, Prism, Lattice, Grain, Glass, and Flux.
- Each family should offer multiple distinct pre-built gradient compositions.
- The exact preset count per family is not fixed yet.
- Users should be able to preview presets and inspect how they are constructed before opening one.

**Start from scratch**
- Users can enter a blank creative workspace.
- They can construct an original composition without choosing a family preset first.

### 2. Presets should reveal their construction

A preset should not be only a flattened visual example. Its construction should be represented in editable form so a user can understand which layers, techniques, and effects create the result.

The amount of construction detail and its placement in the browsing experience remain open UX research questions.

### 3. Provisional Basic / Medium / Advanced organization

The initial version will explore three labels:

- **Basic:** simpler compositions for straightforward visual needs.
- **Medium:** more involved compositions with additional combinations or effects.
- **Advanced:** more elaborate compositions for richer creative work.

These labels describe the starting composition's complexity and intended use. They do not describe the user's ability, and they must not restrict the user's editing capabilities.

The labels are provisional. During planning and research, the team may:
- define clear criteria for each level;
- refine or rename the levels;
- add or remove levels;
- use a different classification if real examples and user needs support it better.

Do not treat the three-level structure as a universal technical classification of all gradients.

### 4. One shared, unrestricted editor

A selected preset opens as a complete editable composition in the same editor used by Start from Scratch.

The original family is a description of the preset's starting inspiration, not a locked editing mode. Users can:
- add, remove, duplicate, and reorder layers;
- change properties and blend modes;
- add effects and techniques associated with other families;
- transform the composition into something that no longer resembles its original preset.

No fixed layer count or fixed control set is imposed across all families. Starting structures and relevant controls should be based on research into the composition.

### 5. Contextual controls

To prevent the editor from overwhelming users with every available property, controls should be relevant to the currently selected layer or element. The precise selection model, control groups, and advanced-control disclosure remain open UX decisions.

## Consequences

- Presets need to be stored as editable recipes, not only as preview images.
- The data model should separate a composition's contents from its original family and preset metadata.
- Mixed compositions should be supported by the project model.
- The same editor should accept both loaded presets and scratch-created compositions.
- Complexity labels should be metadata used for discovery, never feature restrictions.
- Research must define preset quality, family characteristics, complexity criteria, and how construction is explained to users.

## Open research questions

- What makes each of the eight families distinct and recognizable?
- What is a useful initial preset collection for each family?
- What constitutes Basic, Medium, and Advanced in practical composition terms?
- Are the three labels suitable across all eight families?
- Which construction details should be visible before opening a preset?
- How should contextual controls adapt to different layer and effect types?
- Which cross-family combinations should be supported by the underlying model?

## Review condition

Revisit this decision after researching real examples from all eight families and testing the preset discovery experience. The initial product direction is accepted, but the taxonomy, counts, complexity criteria, and detailed UX are intentionally open to improvement.
