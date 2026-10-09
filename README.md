# Griha AI – Personalised house design (mini project)

Enter plot, family, rooms, budget, location and style. The site generates 4 design alternatives
(space / budget / comfort / preference optimised), validates them, estimates cost, shows a 2D plan,
a report, and a 3D model (exterior, then floor-by-floor interiors with furniture).

## Publish on GitHub (free link for everyone)
1. Create a new **public** repository, e.g. `griha-ai`.
2. Upload `index.html` and this `README.md` (Add file → Upload files → Commit).
3. Repo **Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save**.
4. After ~1 minute your site is live at `https://<your-username>.github.io/griha-ai/`.

## What is real vs placeholder
| Part | Status |
|---|---|
| Input forms, budget, location rates, validation, analysis, 2D plan, report | Working (rule-based) |
| 3D exterior, roof by climate (flat / pitched), gate, parking, garden, interiors | Working |
| **Layout generation** (`gen()` in index.html) | **Procedural placeholder** – NOT a trained model yet |

## Adding the Deep Learning model (the core of the project)
GitHub Pages is static, so choose one:
- **Browser-only:** train in PyTorch (GNN + conditional layout generator on RPLAN, which needs a dataset access request),
  export to ONNX, and run it with `onnxruntime-web`. Replace `gen()` so it returns the same structure
  (`floors[].rooms[] = {t,x,y,w,h,f,b}` and `floors[].bands[]`). Validation, cost, 2D and 3D then work unchanged.
- **With backend:** FastAPI + PyTorch hosted on Render / Hugging Face Spaces; the page calls it with `fetch()`
  and the frontend stays on GitHub Pages (enable CORS).

## Known limitations of v1
Rectangular plots only; facing is displayed but does not rotate the plan; vastu is minimal; band-based
layouts can make rooms small on tight plots (the validator flags this); costs are approximate city rates.
No MongoDB / PDF export yet (the Report tab uses the browser's Print → Save as PDF).
