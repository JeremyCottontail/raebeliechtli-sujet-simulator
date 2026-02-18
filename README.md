# Räbeliechtli Simulator

An interactive 3D browser simulation of the Swiss [Räbeliechtli](https://en.wikipedia.org/wiki/R%C3%A4beliechtli) lantern tradition, where carved turnips with candles inside are carried in autumn processions.

## Features

- **Place & remove turnips** on a canvas backdrop — up to 900 turnips, click an existing one to remove it
- **Turnip grid generator** — define columns and rows (1–30 each) to place a perfectly spaced grid in one click
- **Painting templates** — one-click Cat, Tiger, or Spongebob designs painted in black on the canvas, with turnips auto-placed on all white areas (15×15 candidate grid)
- **Canvas size sliders** — independently adjust canvas width (0.5–6 m) and height (0.5–8 m) for any aspect ratio
- **Realistic candle flickering** with multi-frequency sine-wave animation
- **Dynamic candlelight** — each turnip casts a tight warm cone of light on the canvas using a custom GLSL fragment shader; light fades to zero within ~3× turnip height
- **Paint the canvas** with a black brush to create lantern silhouettes; black paint retains 10% reflectivity so candlelight still shows through
- **Candle intensity slider** — dim or brighten all candles simultaneously (affects flame glow, inner cavity, canvas lighting)
- **Bloom post-processing** for glowing flames

## Usage

Open `index.html` in any modern browser — no build step, no server required.

### Toolbar

| Button | Action |
|--------|--------|
| **Rotate** | Click + drag to orbit the scene |
| **Paint Black** | Click + drag on the canvas to paint |
| **Place/Remove Turnip** | Click empty canvas to place a turnip; click an existing turnip to remove it |
| **Clear Canvas/Painting** | Resets the canvas paint to white |
| **Clear Turnips** | Removes all placed turnips |
| **Clear All** | Removes all turnips and resets the canvas |

### Controls

| Control | Description |
|---------|-------------|
| **Brush Size** slider | Adjusts the paint brush diameter (4–150 px) |
| **Candle Intensity** slider | Dims or brightens all candles (0–100%) |
| **Canvas Size** sliders | Sets canvas width (0.5–6 m) and height (0.5–8 m) independently |
| **Grid Generator** | Set columns and rows (1–30 each), then click **Place Grid** to fill the canvas with an evenly spaced turnip grid |
| **Templates** | Click **Cat**, **Tiger**, or **Spongebob** to paint a template and auto-place turnips on white areas |

## Technical Details

- Single-file app (`index.html`) — pure HTML/CSS/JS, no build tooling
- [Three.js](https://threejs.org/) v0.169 (loaded via CDN) for 3D rendering
- Custom GLSL fragment shader for cone-projected candlelight on the canvas plane
  - Tight quadratic falloff (range 0.45 m) for a localised glow
  - Black paint floor of 10% ensures candlelight is never fully absorbed
  - Turnip position/intensity passed via a `DataTexture` (RGBA float, `MAX_TURNIPS × 1`) instead of uniform arrays — removes WebGL uniform-count limits and supports up to 900 turnips
- Shared geometries and materials across all turnip instances for performance
- `UnrealBloomPass` post-processing for flame glow
