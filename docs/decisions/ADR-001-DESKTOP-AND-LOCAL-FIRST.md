# ADR-001: Desktop Platform and Local-First Product Direction

- **Status:** Product constraints accepted; technical implementation candidate proposed
- **Date:** 2026-11-21
- **Owner:** Gradient Lab project owner

## Context

Gradient Lab is a visual gradient creation and editing tool. The project owner has confirmed:

- The application should be an installable desktop application.
- Windows is the first target.
- Development should prioritize desktop, not simultaneous mobile and desktop work.
- The application should not have a hosted backend.
- No user accounts, authentication, cloud database, or cloud synchronization are wanted.
- The core editing workflow should operate locally.
- The user should own and be able to transfer project files.
- Visual Studio Code is the selected development environment.

## Accepted product decisions

1. **Desktop-first:** the initial product is designed for Windows desktop usage.
2. **Local-first:** opening, editing, saving, and exporting projects must not depend on a remote service.
3. **No backend:** do not add a hosted application server, remote API, account system, or cloud database.
4. **File ownership:** projects are stored as files on the user's computer and can be manually backed up or transferred.
5. **No mobile-first scope:** mobile support is not part of the initial development plan.

## Terminology: what "desktop-native" means in this research

There are two different implementation models:

- **Native desktop app shell with a web-rendered interface:** the app installs and runs as a desktop window, but its UI is rendered by a system WebView. Tauri uses this model on Windows through WebView2.
- **Native Windows UI framework:** the UI is built with Windows-native controls, such as WinUI 3 using C# or C++ and XAML.

The current recommendation interprets the requirement as an installable Windows desktop app. It does not yet assume that the owner requires every UI control to be a WinUI-native control.

This distinction must be reviewed before implementation begins.

## Technical recommendation to validate

Proceed with a small proof of concept using:

- Tauri 2 as the desktop shell.
- React + TypeScript as the UI layer.
- Vite as the frontend tooling.
- CSS and SVG for standard gradient and vector rendering.
- Canvas 2D for raster/pixel effects.
- WebGL2 only for effects that need an advanced GPU renderer.
- Local project files as the initial persistence mechanism.

The stack remains a recommendation until the owner accepts the proof of concept and the rendering experiments.

## Alternatives considered

### Tauri 2

Pros:
- Installable desktop application.
- Rust native layer with a web-rendered frontend.
- Supports React and other frontend choices.
- Native system dialog plugin.
- Reuses web graphics technologies that suit a custom editor.

Cons:
- UI is rendered through WebView2 rather than WinUI controls.
- Requires Rust and Windows C++ build tooling for development.
- Must validate WebView2 rendering and GPU behavior on the target computer.

### WinUI 3

Pros:
- Microsoft's recommended native UI framework for new Windows applications.
- Native Windows controls and Fluent design support.

Cons:
- Requires C# or C++ with XAML.
- Less direct reuse of the owner's React/npm experience.
- A separate graphics approach still needs to be researched for gradient editing.

### Electron

Pros:
- Mature JavaScript desktop application framework.
- Familiar HTML/CSS/JavaScript frontend model.

Cons:
- Bundles Chromium and Node.js.
- Not the preferred first option for a Windows-only initial target when WebView2 is already available.

## Consequences

- No cloud architecture needs to be designed or implemented.
- Local save/reopen, file compatibility, backup, and recovery become important product responsibilities.
- The project format should be versioned.
- Tauri capabilities and filesystem access must follow least-privilege principles.
- WebGL2 must remain optional until tested.
- If the owner requires a fully native Windows UI, revisit WinUI 3 before building the full editor.

## References

- Tauri architecture: https://v2.tauri.app/concept/architecture/
- Tauri prerequisites: https://v2.tauri.app/start/prerequisites/
- Tauri native dialog plugin: https://v2.tauri.app/plugin/dialog/
- Microsoft WinUI 3: https://learn.microsoft.com/en-us/windows/apps/winui/winui3/
- Electron overview: https://www.electronjs.org/docs/latest/
