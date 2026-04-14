# ArchFlow — Figma for Architecture

Browser-based, real-time multiplayer 3D modeler for the conceptual design phase.

## Files

- `index.html` — Marketing landing page (the entry point at `/`).
- `app.html` — The actual app: multiplayer 3D modeler, AI massing, IFC export, site upload (served at `/app`).
- `SPEC.md` — Product strategy, competitor analysis, MVP scope, architecture, GTM.
- `_headers` — Cloudflare Pages header config (security + caching).
- `.gitignore` — standard ignores.

## What the prototype does

- **Realtime multiplayer** — Yjs + public WebSocket, cursors in 3D world-space, synced geometry + comments.
- **Sketch-style modeling** — Rectangle (R), Push/Pull (P), Move (M), Wall (W), Slab (S), Delete.
- **AI Massing** — plain-language brief → 5 parametric archetypes (bar, L, courtyard, stepped, tower) as editable geometry.
- **Site context** — drag-and-drop aerial image, scale/rotate/opacity, synced across collaborators.
- **Live HUD** — GFA, volume, embodied carbon, object count.
- **Sun + shadows** — slider for time of day.
- **Export** — GLB (for Enscape/Lumion/Blender), OBJ, IFC 2x3 (for Revit/ArchiCAD).
- **Share link** — URL-based room ID, open in another tab = live collab.

## Run locally

Just open `index.html` in any modern browser. No build step, no dependencies install.

## Test multiplayer

1. Open `app.html` — the URL gains `#room=archflow-xxxx`.
2. Copy that URL into another browser/tab.
3. Both tabs sync in real time (geometry, cursors, comments).

## Deploy (Cloudflare Pages)

This repo is ready for one-click deploy. See the deploy guide in the project chat
— the short version is: push to GitHub, connect the repo in Cloudflare Pages,
no build command needed (it's a static site), output directory is `/`.

## Roadmap

1. ✅ Multiplayer realtime (Yjs WebSocket)
2. ✅ AI massing generator (rule-based, LLM swap-ready)
3. ✅ IFC 2x3 export
4. ✅ Site context upload
5. ✅ Waitlist form (Web3Forms)
6. ⏭ Deploy to Cloudflare Pages
7. ⏭ Self-hosted Hocuspocus sync server
8. ⏭ Auth + project persistence (Postgres + S3)
9. ⏭ Real geometry kernel (Manifold + OpenCascade.js)
10. ⏭ Revit / Rhino plugins
