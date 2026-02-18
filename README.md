# Räbeliechtli Simulator

An interactive 3D browser simulation of the Swiss [Räbeliechtli](https://en.wikipedia.org/wiki/R%C3%A4beliechtli) lantern tradition, where carved turnips with candles inside are carried in autumn processions.

## Features

- **Place turnips** on a canvas backdrop — up to 64 turnips
- **Realistic candle flickering** with multi-frequency sine-wave animation
- **Dynamic candlelight** — each turnip casts a warm cone of light on the canvas using a custom GLSL fragment shader
- **Paint the canvas** with a black brush before placing turnips to create lantern silhouettes
- **Candle intensity slider** — dim or brighten all candles simultaneously
- **Bloom post-processing** for glowing flames

## Usage

Open `index.html` in any modern browser — no build step, no server required.

| Mode | Action |
|------|--------|
| **Rotate** | Click + drag to orbit the scene |
| **Paint Black** | Click + drag on the canvas to paint |
| **Place Turnip** | Click on the canvas to place a turnip |
| **Clear Canvas** | Resets the canvas to white |

Use the **Brush Size** slider to adjust the paint brush and the **Candle Intensity** slider to control the brightness of all candles.

## Technical Details

- Single-file app (`index.html`) — pure HTML/CSS/JS, no build tooling
- [Three.js](https://threejs.org/) v0.169 (loaded via CDN) for 3D rendering
- Custom GLSL shader for cone-projected candlelight on the canvas plane
- Shared geometries and materials across all turnip instances for performance
- SpotLight pool (8 lights) for 3D scene illumination
- `UnrealBloomPass` post-processing for flame glow
