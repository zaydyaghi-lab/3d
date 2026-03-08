# 3D Model Viewer

A **zero-build-step** web page that loads a `.glb` 3D model from GitHub and displays it interactively in the browser using [Three.js](https://threejs.org/).

Features:
- Rotate, zoom, and pan with the mouse (OrbitControls)
- Automatic centering and scaling of any model
- Loading progress indicator
- Friendly error messages
- Draco-compressed mesh support

---

## 🌐 View your 3D model online

**➡️ [https://zaydyaghi-lab.github.io/3d/](https://zaydyaghi-lab.github.io/3d/)**

The site deploys automatically via GitHub Actions whenever you push to `main`.  
If GitHub Pages isn't enabled yet, do it once:

1. Go to **Settings** → **Pages** (left sidebar of this repo).
2. Under **Source**, choose **GitHub Actions**.
3. Click **Save** — then push any commit (or re-run the *Deploy to GitHub Pages* workflow).

---

## Test locally

Browsers block file-to-file requests for security reasons, so you need a simple local server.  
Pick **one** of the methods below:

### Option A – Python (usually pre-installed)

```bash
# Python 3
python -m http.server 8080

# Python 2
python -m SimpleHTTPServer 8080
```

Then open <http://localhost:8080> in your browser.

### Option B – Node.js

```bash
npx serve .
```

Then open the URL it prints (usually <http://localhost:3000>).

### Option C – VS Code

Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension, right-click `index.html` → **Open with Live Server**.

---

## Mouse controls

| Action | Control |
|---|---|
| Rotate | Left-click and drag |
| Zoom | Scroll wheel |
| Pan | Right-click and drag |

---

## How the code works

```
index.html
├── Imports Three.js r169 (ES module) from jsDelivr CDN
├── Imports GLTFLoader  – parses .glb / .gltf files
├── Imports OrbitControls – mouse rotate / zoom / pan
├── Imports DRACOLoader – decodes Draco-compressed meshes (optional)
├── Creates a Scene, Camera, and WebGL Renderer
├── Adds ambient + directional lighting
├── Loads the model, auto-centers and auto-scales it
└── Runs an animation loop (requestAnimationFrame)
```

No `npm install`, no bundler, no build step required.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| White screen / error message | Check that `MODEL_URL` contains your real GitHub raw URL |
| "CORS" error in the console | Open the page via a local server (Step 5), not by double-clicking the file |
| Model looks too dark | Increase `toneMappingExposure` in `index.html` (default: `1.2`) |
| Model is invisible | The model may be too small or too large – the viewer auto-scales, but very unusual models may need manual tweaking of `camera.position` |
| Slow load on mobile | Compress your GLB with [gltf-transform](https://gltf-transform.donmccurdy.com/) or [Blender](https://www.blender.org/) before uploading |
