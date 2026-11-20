# Gradient Lab — Technology Research

**Branch:** planning/research  
**Research snapshot:** 2026-11-21  
**Status:** Preliminary; recommendations require practical validation

## 1. Constraints

Gradient Lab is planned as a Windows-first installable desktop application. It must work locally, must not require a hosted backend, and should allow users to keep projects as files on their own computers.

The central engineering challenge is a visual editor and rendering engine—not accounts, APIs, or cloud infrastructure.

## 2. Desktop application options

### Tauri 2

**What it is:** a desktop application toolkit that combines a Rust application layer with a frontend rendered in the operating system's WebView. On Windows, that WebView is Microsoft Edge WebView2.

**Advantages**
- Provides an installable desktop application and access to native operating-system capabilities.
- Works with frontend frameworks including React.
- Lets the editor use CSS, SVG, Canvas, and WebGL web graphics APIs.
- Has native dialog support for opening and saving files.
- Allows most product UI and editor logic to remain in TypeScript.

**Trade-offs**
- The interface is rendered by WebView2, not by WinUI native controls.
- WebView2 and graphics-driver behavior must be tested on the target machine.
- Native features require a Rust layer and carefully scoped Tauri permissions.
- Developers need Rust and Windows C++ build tooling.

**Assessment:** leading candidate. It offers a good fit for a custom graphics editor while allowing the project to use the owner's JavaScript/React experience.

Official sources:
- https://v2.tauri.app/concept/architecture/
- https://v2.tauri.app/start/create-project/
- https://v2.tauri.app/start/frontend/
- https://v2.tauri.app/plugin/dialog/

### WinUI 3

**What it is:** Microsoft's recommended native UI framework for new Windows desktop applications, using C# or C++ with XAML and the Windows App SDK.

**Advantages**
- Native Windows UI controls and Fluent design integration.
- Direct alignment with Windows application conventions.
- Strong option when Windows-native controls and platform integration are the priority.

**Trade-offs**
- Moves the frontend implementation to C#/XAML or C++/XAML.
- The gradient engine would still need its own graphics implementation and experimentation.
- The owner's React/npm knowledge would be less directly reusable.

**Assessment:** the strongest alternative if "desktop-native" means a UI built from native Windows controls rather than a WebView-based desktop app.

Official sources:
- https://learn.microsoft.com/en-us/windows/apps/winui/winui3/
- https://learn.microsoft.com/en-us/windows/apps/desktop/

### Electron

**What it is:** a desktop application framework built around JavaScript, HTML, and CSS. It bundles Chromium and Node.js with the application.

**Advantages**
- Familiar web technologies.
- Mature desktop ecosystem and extensive examples.
- Consistent Chromium rendering across supported desktop platforms.

**Trade-offs**
- Bundles its own Chromium and Node.js runtime.
- Duplicates capabilities Windows supplies through WebView2.
- Not needed unless a specific Electron capability or compatibility requirement appears.

**Assessment:** viable, but not the first choice for this Windows-first project.

Official source:
- https://www.electronjs.org/docs/latest/

### Current recommendation

Proceed with a **Tauri 2 proof of concept**, with React + TypeScript + Vite as the frontend candidate. Keep WinUI 3 as the fallback if the owner decides native Windows controls are a hard requirement or if the Tauri/WebView model fails validation.

This is a recommendation, not an irreversible framework decision.

## 3. Frontend and development tooling

### React + TypeScript

React is a practical choice for a complex editor composed of separate panels, controls, layer lists, dialogs, and selection state. TypeScript can help keep the editor's project model and renderer interfaces consistent.

This also reuses the owner's existing frontend experience. It should still be validated with a small editor prototype; React should not own high-frequency pixel rendering.

### Vite

Tauri's documentation recommends Vite for single-page application frontends and provides a React project template. During development, Vite serves the frontend while Tauri opens the application window.

References:
- https://v2.tauri.app/start/create-project/
- https://v2.tauri.app/start/frontend/

### VS Code

VS Code is the selected editor. The installed extensions are:
- Tauri
- rust-analyzer
- ESLint
- Prettier
- Even Better TOML

Extensions improve editing support; they do not install the underlying compilers or runtimes.

## 4. Gradient rendering options

A hybrid rendering design is preferable to forcing every visual effect through a single technology.

| Capability | Best initial use | Strengths | Limitations to test |
|---|---|---|---|
| CSS gradients | Standard gradient layers | Native gradient functions; easy CSS export | Not a general arbitrary mesh-gradient model |
| SVG | Vector composition and filters | Paths, masks, filter chains, scalable output | Complex filter chains can be costly; output fidelity needs testing |
| Canvas 2D | Raster effects and pixel processing | Direct pixel/drawing operations; PNG-oriented workflows | Drawn objects are not inherently editable or accessibility-aware |
| WebGL2 | Advanced shader effects | GPU-oriented rendering pipeline | More implementation complexity; GPU and driver capabilities vary |

### CSS

CSS provides linear, radial, conic, and repeating gradient functions. These are a natural foundation for standard gradients and directly map to useful code exports.

Reference:
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Images/Using_gradients

### SVG

SVG supports vector paths, masks, and filter pipelines. Relevant filter primitives include Gaussian blur and turbulence generation, which can help with softness, noise, and organic textures.

References:
- https://developer.mozilla.org/en-US/docs/Web/SVG/Guides/Filters
- https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/feTurbulence
- https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/feGaussianBlur

### Canvas 2D

Canvas is suitable for direct drawing, image manipulation, and pixel-level effects. It is a candidate for grain/noise and raster exports.

Reference:
- https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API

### WebGL2

WebGL2 exposes an OpenGL ES 3.0 graphics context through a canvas. It is a candidate for advanced shader-driven gradients and complex real-time effects.

It should not be the starting renderer. First prove that CSS, SVG, or Canvas cannot meet a specific visual or performance requirement. Check context availability and provide a fallback.

Reference:
- https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext

## 5. Local project storage — no backend

### Agreed direction

The project must not depend on a hosted service. Files should be stored and managed on the user's computer.

### Options to investigate

**Versioned JSON project file**
- Simple and inspectable.
- Easy to export, back up, and transfer.
- Good starting point if projects contain structured parameters and few assets.

**Packaged project file**
- Could contain a JSON manifest plus images or other required assets.
- More suitable if projects eventually include imported resources.
- Requires archive validation, path safety, and version handling.

**SQLite**
- A local database, not a hosted backend.
- Could help if the app later needs a searchable library, substantial metadata, or durable history.
- Adds schema and migration responsibilities.

**Recommendation:** do not add SQLite at the beginning. First test a versioned project-file approach. Decide on a database only after an actual requirement emerges.

The working extension is **.glab**, but the internal format remains open.

### Native file operations

Tauri's dialog plugin provides native open/save dialogs. File access should be limited to paths a user selects or to the app's own data directory. Do not grant broad filesystem permissions without a requirement.

References:
- https://v2.tauri.app/plugin/dialog/
- https://v2.tauri.app/plugin/file-system/

## 6. Windows development prerequisites

According to the Tauri v2 Windows prerequisites, development requires:
- Microsoft C++ Build Tools with the **Desktop development with C++** workload.
- Microsoft Edge WebView2.
- Rust installed through rustup.

Node.js is required for the JavaScript frontend and package tooling.

Windows 11 normally includes WebView2, but the development environment should still be checked rather than assumed.

Official source:
- https://v2.tauri.app/start/prerequisites/

The full Visual Studio IDE is not required solely for a Tauri project; the standalone C++ Build Tools package is the relevant compiler/toolchain dependency.

## 7. Proposed technical direction

| Area | Proposal | Confidence |
|---|---|---|
| Desktop shell | Tauri 2 | Medium-high; validate locally |
| UI | React + TypeScript | High; fits editor structure and existing skills |
| Frontend build | Vite | High; documented Tauri path |
| Standard rendering | CSS | High |
| Vector effects | SVG | High |
| Raster effects | Canvas 2D | High |
| Advanced effects | WebGL2 | Conditional |
| Project storage | Local versioned files | High as direction; format open |
| Database | None initially | High |
| Cloud/backend | None | Confirmed constraint |

## 8. Validation still required

1. Run a minimal Tauri + React + TypeScript app on the target Windows laptop.
2. Confirm native open/save dialogs can read and write a chosen project file.
3. Test representative CSS, SVG, and Canvas effects in the actual Tauri WebView.
4. Probe WebGL2 support and measure a small shader experiment.
5. Compare rendering responsiveness at realistic canvas sizes.
6. Test project serialization and reopening after closing the application.
7. Build and install a local Windows package.
8. Reassess whether the WebView-based UI meets the owner's intended meaning of "desktop-native".

## 9. References and research date

Primary references checked on **2026-11-21**:

- Tauri architecture: https://v2.tauri.app/concept/architecture/
- Tauri prerequisites: https://v2.tauri.app/start/prerequisites/
- Tauri project creation: https://v2.tauri.app/start/create-project/
- Tauri frontend configuration: https://v2.tauri.app/start/frontend/
- Tauri dialog plugin: https://v2.tauri.app/plugin/dialog/
- Tauri filesystem plugin: https://v2.tauri.app/plugin/file-system/
- Microsoft WinUI 3: https://learn.microsoft.com/en-us/windows/apps/winui/winui3/
- Electron overview: https://www.electronjs.org/docs/latest/
- MDN CSS gradients: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Images/Using_gradients
- MDN SVG filters: https://developer.mozilla.org/en-US/docs/Web/SVG/Guides/Filters
- MDN SVG turbulence: https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/feTurbulence
- MDN Canvas API: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API
- MDN WebGL2: https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext
