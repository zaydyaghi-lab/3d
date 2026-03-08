# 3D Model Viewer

A **zero-build-step** web page that loads a `.glb` 3D model from GitHub and displays it interactively in the browser using [Three.js](https://threejs.org/).

Features:
- Rotate, zoom, and pan with the mouse (OrbitControls)
- Automatic centering and scaling of any model
- Loading progress indicator
- Friendly error messages
- Draco-compressed mesh support

---

## Step 1 – Create a GitHub repository

> If you already have a repository, skip to Step 2.

1. Go to [github.com](https://github.com) and sign in (create a free account if needed).
2. Click the **+** button in the top-right corner → **New repository**.
3. Give it a name (e.g. `my-3d-model`), set it to **Public**, tick **Add a README file**, then click **Create repository**.

---

## Step 2 – Upload your `.glb` file

### ➡️ [Click here to upload your .glb file now](https://github.com/zaydyaghi-lab/3d/upload/main)

That link takes you straight to the upload page for this repository. Just:

1. Drag your `.glb` file onto the upload area (or click **choose your files**).
2. Scroll down and click **Commit changes**.

> **Not working?** Make sure you are signed into GitHub first, then try the link again.

---

## Step 3 – Get the raw GitHub URL

1. After uploading, click on the `.glb` file in [this repository](https://github.com/zaydyaghi-lab/3d).
2. Click the **Raw** button in the top-right of the file view.
3. Copy the URL from your browser's address bar.  
   For this repository it will look like:
   ```
   https://raw.githubusercontent.com/zaydyaghi-lab/3d/main/YOUR-FILE-NAME.glb
   ```
   (just replace `YOUR-FILE-NAME` with the actual name of your file)
4. Keep this URL handy – you will paste it into `index.html` next.

---

## Step 4 – Paste your URL into `index.html`

Open `index.html` in any text editor and find this line near the top of the `<script>` block:

```js
const MODEL_URL =
  'https://raw.githubusercontent.com/zaydyaghi-lab/3d/main/YOUR-FILE-NAME.glb';
```

Replace `YOUR-FILE-NAME` with the actual name of your uploaded file, for example:

```js
const MODEL_URL =
  'https://raw.githubusercontent.com/zaydyaghi-lab/3d/main/robot.glb';
```

Save the file.

---

## Step 5 – Test locally

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

## Step 6 – Deploy to GitHub Pages (free hosting)

1. Upload `index.html` to your GitHub repository (same steps as uploading the `.glb`).
2. Go to your repository → **Settings** → **Pages** (left sidebar).
3. Under **Source**, choose **Deploy from a branch**.
4. Select **main** branch and **/ (root)** folder, then click **Save**.
5. After about 60 seconds, your site will be live at:
   ```
   https://YOUR-USERNAME.github.io/YOUR-REPO/
   ```

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
