# Gradient Lab

**A visual-first workspace for discovering, creating, and customizing gradients — without needing to write code.**

Gradient Lab aims to make sophisticated gradient creation accessible to people who may not know CSS, Tailwind CSS, or the technical details behind visual effects. Users should be able to focus on the appearance they want while the Lab handles the underlying implementation.

## Why Gradient Lab?

Creating a particular gradient can be difficult when you do not know which gradient techniques, layers, blend effects, textures, or tools are needed to achieve it.

Gradient Lab brings those capabilities into an understandable creative workspace. Users can explore visual templates, adjust clear controls, experiment with combinations, and create original compositions instead of having to write styling code for every design.

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

Users should be able to work with understandable controls for:

- **Colors** — choose, replace, and combine colors.
- **Color placement** — move and resize color fields or points.
- **Layers** — add, remove, duplicate, reorder, and adjust layers.
- **Blending** — try effects such as Normal, Soft Light, Hard Light, Multiply, Screen, Overlay, and Color Dodge, with a clear explanation of each.
- **Appearance** — adjust blur, softness, opacity, glow, and intensity.
- **Texture and patterns** — explore grain, noise, repeating patterns, and geometric details.
- **Composition** — combine techniques to create an original result.

The preview should respond immediately to changes so users can learn by experimenting.

## Easy to Use, With Room to Explore

Gradient Lab is for people who want creative control without first learning the technical language behind it.

The experience should follow these principles:

1. **Visual-first** — let people work with what they see.
2. **Understandable controls** — use clear names, short explanations, and sensible defaults.
3. **Beginner-friendly** — make common adjustments easy to find and use.
4. **Room for depth** — offer more detailed controls when someone wants them.
5. **Immediate feedback** — show the effect of an adjustment in the preview.
6. **Creative freedom** — templates are starting points, not restrictions.

Technical details such as CSS properties, rendering methods, and export syntax should be handled by the Lab rather than required knowledge for the user.

## Cross-Device Experience

Gradient Lab is planned as a responsive web application that can be used on both laptops and mobile phones. The experience should adapt to the device instead of simply shrinking the desktop editor to fit a phone.

### Desktop workspace

The desktop experience is the full creative workspace. It should provide the complete editor, detailed layer management, advanced customization controls, experimentation tools, and export options.

### Mobile workspace

The mobile experience is a convenient creation and prototyping workspace. Users should be able to explore templates, create gradient prototypes, adjust essential visual properties, and save their work while away from their laptop.

The mobile editor does not need to expose every advanced desktop control. Both experiences should work with the same underlying gradient project format so a mobile creation can be continued on desktop.

The web application should be designed to be installable as a Progressive Web App (PWA), subject to the capabilities and limitations of supported browsers.

## Data, Accounts, and Synchronization

**Selected backend direction: Firebase.**

Gradient Lab is planned to use:

- **Firebase Authentication** for user accounts and sign-in.
- **Cloud Firestore** for users' saved gradient projects, templates, experiments, and related structured data.
- **Local persistence** so users can continue working with locally available projects when offline.
- **Synchronization** to make saved work available across a user's signed-in devices when connectivity is available.

The goal is for a user to start a gradient on a phone and continue refining the same project on a laptop. Local editing should not depend on a live cloud connection.

Offline changes, simultaneous edits, and synchronization conflicts must be handled deliberately. The product should track project versions and provide appropriate recovery or conflict-handling behavior rather than silently losing a user's work.

### Portable projects and backups

Cloud synchronization should not be the only way users can move or protect their creations.

Gradient Lab should provide a versioned, portable project format (working extension: `.glab`) that preserves the editable gradient recipe and any assets required by the project. Users should be able to export a project on one device and import it on another, including through ordinary file transfer such as USB.

JSON backup and restore should also be supported. Exported PNG, SVG, and code files should be generated locally wherever practical.

## Infrastructure and Cost Direction

The initial infrastructure target is **Firebase's no-cost Spark plan**, staying within its published quotas and service restrictions.

The product should be designed to avoid unnecessary cloud usage:

- Render and customize gradients on the user's device.
- Store compact, structured gradient recipes rather than uploading every preview as an image.
- Keep temporary drafts and working data locally where appropriate.
- Synchronize user projects through Firestore when online.
- Allow portable project export and backup.

The Spark plan has usage limits and is not an unlimited or permanent free-service guarantee. Usage should be monitored, and the application must not assume paid services are available. Any future move to a paid plan must be evaluated against actual product needs and operating costs.

## Export Goals

A gradient should be useful beyond the editor. The planned export direction is:

1. **Tailwind CSS** — the first code-export target.
2. CSS
3. CSS Variables
4. CSS-in-JS
5. SVG
6. PNG

The same composition should be reusable across supported output formats wherever the underlying rendering technique allows it. Some effects may have format-specific limitations, which should be clearly communicated during export.

## Research-Led Development

Gradient Lab will be developed through exploration and practical experiments.

We will investigate:

- How different gradient styles are constructed.
- Which visual effects can be combined.
- How layers, blending, blur, color, and texture affect a result.
- Which browser capabilities and rendering techniques are suitable.
- Which free and open-source libraries or resources are useful.
- How to turn technical capabilities into simple, meaningful user controls.
- How to keep the editor responsive and reliable across desktop and mobile devices.

Examples and references will help us learn, but the goal is to develop our own understanding, workflows, templates, and original compositions.

AI tools may assist with research, explanation, coding, and experimentation. However, the core visual editing and rendering experience should not require an external AI generation service.

## Current Status

**Research and product definition.**

The product direction is established: a visual-first, cross-device web application with Firebase as the selected backend direction. We are currently exploring gradient styles, studying how they are built, testing visual effects, and identifying the tools and capabilities the Lab should provide.

The detailed interface, rendering approach, local data model, synchronization behavior, and final technology choices will be shaped and validated during development. Planned capabilities described in this README are not claims that those features have already been implemented.

## Guiding Idea

**Technical power behind the scenes. Creative control in the user's hands.**

Gradient Lab should make gradient creation understandable and approachable — so people can create the gradients they imagine, continue their work across devices, and keep control of their creative projects.
