# RAY // minimal vision

A standalone, touch-first raycasting experiment built from the minimal vision prototype in [BOIDS](https://github.com/gemquota/boids/blob/main/vision-minimal.html).

**Live app:** https://gemquota.github.io/ray/

Ray is deliberately small: one full-screen canvas, moving geometric entities, a field-of-view cone, and a configurable set of sensory rays. Gestures change the perception model directly; a compact translucent HUD briefly explains each change.

## Gesture controls

Tap the **?** in the upper-right corner to open the on-screen gesture guide.

| Fingers | Gesture | Action |
|---|---|---|
| 1 | Double-tap | Cycle ray distribution: uniform → clustered → progressive |
| 1 | Vertical drag | Change total ray positions |
| 1 | Horizontal drag | Change simultaneously active rays |
| 1 | Circular drag around the centre | Rotate the FOV cone |
| 2 | Single tap | Toggle contact-only reconstruction |
| 2 | Vertical drag | Adjust ray width and contact-pixel size together |
| 2 | Horizontal drag | Adjust FOV angular width |
| 3 | Vertical drag | Adjust ray-cycling frequency |

### Gesture recognition

- Drag direction locks after a short movement threshold, so diagonal motion does not keep switching controls mid-gesture.
- Two-finger drags also lock to one axis. A diagonal two-finger movement cannot accidentally adjust both FOV width and ray thickness.
- FOV rotation is recognised as tangential movement around the centre, within a ring around the centre dot. Dragging directly across the dot is not treated as rotation.
- Small movements are not interpreted as taps; this prevents a slight finger slip from toggling contact-only mode or triggering a double-tap.
- The guide is available on demand and does not occupy the artwork permanently.

### Ray distributions

- **Uniform:** evenly spaced ray positions across the FOV.
- **Clustered:** positions concentrated around the centre.
- **Progressive:** a central cluster combined with positions spreading towards the FOV edges.

Total ray positions define the sampling locations. Active rays define how many positions are sampled at once. Cycling frequency controls how quickly the active window advances.

### Contact-only reconstruction

Two-finger tap hides entity bodies and ray shafts, leaving only the ray-hit contact points. This exposes the sampled reconstruction rather than the underlying scene.

### Gesture feedback

Parameter changes produce a small translucent HUD near the bottom of the display. It updates during interaction, shows the current value and a proportional indicator, and fades shortly after the gesture ends. Coupled changes (ray width and contact-pixel size) appear together.

## Run locally

No build step or dependencies are required. Open `index.html` in a modern browser, or serve the repository root with any static HTTP server.

## Deployment

GitHub Pages is deployed from the `main` branch by `.github/workflows/pages.yml`.
