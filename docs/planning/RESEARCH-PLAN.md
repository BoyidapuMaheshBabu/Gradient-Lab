# Gradient Lab — Planning & Research Plan

**Branch:** planning/research  
**Status:** Active research  
**Last updated:** 2026-11-21

## 1. Goal

Define a reliable product and technical foundation for Gradient Lab before implementation begins.

This phase is for product discovery, technical comparison, small isolated experiments, and documented decisions. It is not an implementation phase for the actual application.

## 2. Confirmed product constraints

- **Platform:** installable desktop application, Windows first.
- **Priority:** desktop-first; mobile is outside the initial scope.
- **Operation:** local-first; core editing must work offline.
- **Backend:** none. No hosted API, user accounts, authentication, cloud database, or cloud synchronization.
- **Ownership:** users save, open, back up, and transfer their own project files.
- **Development environment:** Visual Studio Code.
- **Research approach:** understand options and validate important assumptions with practical experiments before choosing a final stack.

## 3. Working technical direction

These are recommendations to validate, not all final decisions:

| Area | Current candidate | Status |
|---|---|---|
| Desktop shell | Tauri 2 | Leading candidate |
| Frontend | React + TypeScript | Leading candidate |
| Frontend tooling | Vite | Leading candidate |
| Editor styling | CSS | Candidate |
| Standard gradient renderer | CSS | Candidate |
| Vector renderer/effects | SVG | Candidate |
| Raster and pixel work | Canvas 2D | Candidate |
| Advanced GPU effects | WebGL2 | Experiment only |
| Project storage | Versioned local project files | Direction agreed |
| Project extension | .glab | Working name; format open |
| Local database | None initially | Avoid unless justified |
| Native file dialogs | Tauri dialog plugin | Candidate |

## 4. Research workstreams

### A — Desktop platform and development environment

**Questions**
- Is Tauri 2 the right desktop shell for a Windows-first gradient editor?
- Does "native desktop" mean an installable app with a WebView-rendered UI, or a UI built from native Windows controls?
- What are the trade-offs between Tauri, WinUI 3, and Electron?
- What does the development and packaging toolchain require?

**Experiments and evidence**
- Verify the Tauri + React + TypeScript + Vite workflow.
- Build a disposable proof of concept that opens a native app window.
- Test native open/save dialogs.
- Produce a local Windows development build.
- Record installer output, startup behavior, memory use, and compatibility issues.

**Exit condition:** the desktop shell works on the target Windows machine, its WebView/native distinction is understood and accepted, and limitations are recorded.

### B — Gradient rendering engine

**Questions**
- Which gradient types are well represented by CSS?
- Which effects are easier or more reliable in SVG?
- When is Canvas 2D necessary?
- Which effects justify WebGL2?
- How can multiple renderers share one editable project model?
- What happens when an effect cannot be exported to a particular format?

**Experiments**
1. Linear, radial, conic, and repeating gradients.
2. Multiple translucent gradient layers and blend modes.
3. Softness, blur, glow, and masks.
4. Grain, noise, and turbulence-based texture.
5. Mesh-style compositions and movable color points.
6. SVG and PNG output comparison.
7. Responsiveness at realistic editor-canvas sizes.

**Exit condition:** a capability matrix identifies the best renderer for each supported effect; representative experiments exist for every renderer retained; performance and fallback behavior are understood.

### C — Editable project model and local storage

**Questions**
- What data must be preserved to reopen and continue editing?
- Should a .glab file be plain JSON initially or an archive containing a manifest and assets?
- How should project schema versions and migrations work?
- Is a database necessary, or are project files and local application settings sufficient?
- How should autosave, recovery, and undo history work?

**Experiments and evidence**
- Draft a sample project document.
- Round-trip a project: create → save → close → reopen → edit → save.
- Test schema version identification and invalid-file handling.
- Test portable transfer to a different folder.
- Evaluate whether SQLite solves a demonstrated requirement.

**Exit condition:** the format and local persistence approach are documented; projects reopen without losing editable properties; backup and portability behavior is defined.

### D — Editor workflow and desktop UX

**Questions**
- What are the essential editor areas and their hierarchy?
- How should users select, move, and edit gradient points or layers?
- Which properties need direct manipulation and which need numeric controls?
- How should selection, undo/redo, keyboard shortcuts, and preview zoom work?
- How can beginner-friendly controls coexist with advanced capabilities?

**Evidence**
- User-flow diagrams.
- Low-fidelity desktop layout exploration.
- Interaction notes for canvas, layers, properties, and project management.
- Core tasks to test against the proposed design.

**Exit condition:** the main editor workflow is understandable without implementation-level detail; core interactions and layout responsibilities are documented.

### E — Export, performance, and quality

**Questions**
- Which effects can be represented as CSS, Tailwind CSS, SVG, or PNG?
- Which effects need a warning or fallback during export?
- What performance target is realistic for the target laptop?
- How should the app behave when a GPU feature is unavailable?
- What tests protect rendering correctness and project compatibility?

**Evidence**
- Export compatibility matrix.
- Repeatable performance test cases.
- Visual comparison samples.
- Basic test strategy for serialization, rendering, and export.

**Exit condition:** output limitations are transparent; performance expectations and fallbacks are documented; a validation strategy exists.

## 5. Suggested research order

1. **Platform validation** — settle the desktop shell and confirm the native/WebView distinction.
2. **Rendering experiments** — test CSS, SVG, Canvas 2D, and WebGL2 against real Gradient Lab styles.
3. **Project model** — define editable data and a portable local file.
4. **Editor UX** — define the desktop workspace around the capabilities we proved.
5. **Export and performance** — validate outputs and realistic device performance.
6. **Implementation plan** — convert validated decisions into small, testable development phases.

The order can adapt when experiments reveal dependencies. Do not force a technology choice simply because it appears in this initial plan.

## 6. Research rules

- Prefer official documentation for platform capabilities and requirements.
- Record the source URL and date checked for material technical claims.
- Distinguish verified facts, recommendations, assumptions, and open questions.
- Use small experiments to validate risky assumptions.
- Do not introduce a dependency without identifying the problem it solves.
- Keep the core workflow offline and local.
- Do not add cloud services, authentication, analytics, or remote AI requirements.
- Do not create production application code in this branch during the planning phase.
- Keep the README aligned with decisions the owner has actually accepted.

## 7. Current open decisions

- Confirm that Tauri's WebView-rendered interface meets the owner's meaning of a desktop-native app.
- Validate graphics performance on the target Windows laptop.
- Decide the .glab container format.
- Decide whether project history and autosave require a database.
- Decide the minimum useful first set of gradient styles and export targets.

## 8. Definition of research completion

Research is ready to become an implementation plan when:
- The desktop framework and frontend stack are justified.
- The rendering capability matrix is backed by working experiments.
- The project format and local storage model are defined.
- The initial editor workflow is documented.
- Export limits, performance targets, and fallback behavior are understood.
- The owner reviews and accepts the proposed implementation phases.
