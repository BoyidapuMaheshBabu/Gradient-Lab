# Gradient Lab

**A visual-first Windows desktop workspace for discovering, creating, and customizing gradients — without needing to write code.**

Gradient Lab aims to make sophisticated gradient creation approachable. Users should be able to focus on the appearance they want while the Lab handles the underlying rendering and export details.

## Why Gradient Lab?

Creating a particular gradient can be difficult when you do not know which techniques, layers, blend effects, textures, or tools are needed to achieve it.

Gradient Lab brings those capabilities into an understandable creative workspace. Users can explore visual templates, adjust clear controls, experiment with combinations, and create original compositions.

The goal is not to hide creative control. It is to make that control approachable.

## Product Vision

Gradient Lab is intended to provide three ways to create:

- **Start with a template** — choose a visual style and customize its colors, layers, effects, and composition.
- **Create from scratch** — begin with a blank canvas and build a gradient using visual tools.
- **Experiment and explore** — compare settings, try variations, and discover new combinations.

The result should be a live visual preview that users can refine, save, and export.

## Gradient Creation

The capabilities below describe the product direction. They are goals for the Lab, not a claim that every feature is already implemented.

### Explore gradient styles and templates

The initial exploration includes visual families such as:

- Aura
- Mesh
- Nebula
- Prism
- Lattice
- Grain
- Glass
- Flux

These are starting points for research and template discovery, not a fixed or final classification. Gradient Lab may develop its own categories as we learn how different visual styles are constructed.

Templates should be editable starting points, not locked designs. Users should be able to change their colors, composition, layers, and effects, then save their own versions.

### Customize visually

Potential controls include:

- **Colors** — choose, replace, and combine colors.
- **Color placement** — move and resize color fields or points.
- **Layers** — add, remove, duplicate, reorder, and adjust layers.
- **Blending** — explore blend modes and understand their visual impact.
- **Appearance** — adjust blur, softness, opacity, glow, and intensity.
- **Texture and patterns** — explore grain, noise, repeating patterns, and geometric details.
- **Composition** — combine techniques to create an original result.

The preview should respond immediately to changes so users can learn by experimenting.

## Desktop-First Experience

Gradient Lab is planned as an installable Windows desktop application. The first serious editor experience will be designed for desktop screens, mouse and keyboard input, and detailed creative controls.

Mobile support is not part of the initial development scope. The project format should remain portable so users can move their work between computers using ordinary file transfer.

## Local-First and No Backend

Gradient Lab is intended to work locally without a hosted backend.

- No user accounts or sign-in are required.
- No cloud database or cloud synchronization is planned.
- Projects are saved and opened from the user's computer.
- Core editing and export workflows should not require an internet connection.
- Users should be able to back up and move projects using ordinary files.

The working project-file extension is **.glab**. Its versioned structure and whether it should be a JSON document or an archive containing JSON and assets will be decided during research.

Local persistence technology is still under evaluation. A database is not assumed to be necessary; the simplest reliable file-based approach should be preferred unless real requirements justify more.

## Rendering and Export Research

The rendering approach will be selected through practical experiments. Candidate browser-based graphics capabilities include CSS gradients, SVG filters, Canvas 2D, and WebGL2 inside the desktop application's WebView.

No single rendering technology is assumed to handle every effect. The same editable project model should be able to produce supported output formats, while documenting effects that cannot be represented faithfully in a particular format.

Planned export targets include:

1. Tailwind CSS
2. CSS
3. CSS Variables
4. CSS-in-JS
5. SVG
6. PNG

The exact export order and compatibility rules will be refined during research.

## Research-Led Development

Gradient Lab will be developed through exploration and practical experiments.

We will investigate:

- Which desktop application framework best fits a Windows-first creative tool.
- How different gradient styles are constructed.
- Which rendering capabilities are suitable for each effect.
- How layers, blending, blur, color, and texture affect a result.
- How to represent an editable gradient independently of its renderer.
- How to save, reopen, version, and export projects reliably.
- How to keep the editor responsive on the target hardware.
- Which free and open-source libraries or resources are genuinely useful.

Examples and references will help us learn, but the goal is to develop our own understanding, workflows, templates, and original compositions.

AI tools may assist with research, explanation, coding, and experimentation. However, the core visual editing and rendering experience should not require an external AI generation service.

## Current Status

**Planning and research.**

The agreed product constraints are:

- Windows desktop first.
- Installable desktop application.
- Local-first operation.
- No hosted backend, accounts, or cloud synchronization.
- No implementation work until the technical and product research is sufficiently validated.

Tauri 2 with a React and TypeScript frontend is the leading technology candidate, not yet a final implementation commitment. The rendering engine, project format, local persistence details, and final editor experience remain under research.

See the [research plan](docs/planning/RESEARCH-PLAN.md), [technology research](docs/research/TECHNOLOGY-RESEARCH.md), and [platform decision record](docs/decisions/ADR-001-DESKTOP-AND-LOCAL-FIRST.md).

## Guiding Idea

**Technical power behind the scenes. Creative control in the user's hands.**

Gradient Lab should make gradient creation understandable and approachable — so people can create the gradients they imagine and keep control of their creative projects.
