# Gradient Lab

**A visual-first workspace for discovering, creating, and customizing gradients — without needing to write code.**

Gradient Lab is a project to make sophisticated gradient creation accessible to people who may not know CSS, Tailwind CSS, or the technical details behind visual effects. Users should be able to focus on the appearance they want while the Lab handles the underlying implementation.

## Why Gradient Lab?

Creating a particular gradient can be difficult when you do not know which gradient techniques, layers, blend effects, textures, or tools are needed to achieve it.

Gradient Lab aims to bring those capabilities into one understandable creative workspace. Instead of depending on prompts or manually writing styling code for every design, users can explore visual templates, adjust clear controls, experiment with combinations, and create their own compositions.

The goal is not to hide creative control. It is to make that control approachable.

## The Vision

Gradient Lab is intended to provide three ways to create:

- **Start with a template** — choose a visual style and customize its colors, layers, effects, and composition.
- **Create from scratch** — begin with a blank canvas and build a gradient using visual tools.
- **Experiment and explore** — compare settings, try variations, and discover new combinations.

The result should be a live visual preview that users can refine, save, and export.

## What Users Should Be Able to Do

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

The experience should follow a few principles:

1. **Visual-first** — let people work with what they see.
2. **Understandable controls** — use clear names, short explanations, and sensible defaults.
3. **Beginner-friendly** — make common adjustments easy to find and use.
4. **Room for depth** — offer more detailed controls when someone wants them.
5. **Immediate feedback** — show the effect of an adjustment in the preview.
6. **Creative freedom** — templates are starting points, not restrictions.

Technical details such as CSS properties, rendering methods, and export syntax should be handled by the Lab rather than required knowledge for the user.

## Export Goals

A gradient should be useful beyond the editor. The planned export direction is:

1. **Tailwind CSS** — the first code-export target.
2. CSS
3. CSS Variables
4. CSS-in-JS
5. SVG
6. PNG

The same composition should be reusable across supported output formats wherever the underlying rendering technique allows it. Some effects may have format-specific limitations, which should be made clear when exporting.

## Research-Led Development

Gradient Lab will be developed through exploration and practical experiments.

We will investigate:

- How different gradient styles are constructed.
- Which visual effects can be combined.
- How layers, blending, blur, color, and texture affect a result.
- Which browser capabilities and rendering techniques are suitable.
- Which free and open-source libraries or resources are useful.
- How to turn technical capabilities into simple, meaningful user controls.

Examples and references will help us learn, but the goal is to develop our own understanding, workflows, templates, and original compositions.

AI tools may assist with research, explanation, coding, and experimentation. However, the core visual editing and rendering experience should not require an external AI generation service.

## Current Status

**Research and product definition.**

We are currently exploring gradient styles, studying how they are built, testing visual effects, and identifying the tools and capabilities the Lab should provide. The interface, rendering approach, technology choices, and feature set will be shaped by those findings.

## Guiding Idea

**Technical power behind the scenes. Creative control in the user's hands.**

Gradient Lab should make gradient creation understandable and approachable — so people can create the gradients they imagine, even without knowing how to code them.
