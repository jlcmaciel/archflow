# ArchFlow — Product Specification

**Tagline:** The Figma for architecture. Design, collaborate, and present buildings in the browser.

---

## 1. Vision

SketchUp, Revit, ArchiCAD, and Vectorworks were built for a single user on a desktop. The web is collaborative, AI-native, and installation-free — and architecture software hasn't caught up. ArchFlow is a browser-based, real-time multiplayer 3D modeler for the **conceptual and schematic design phase** (first 2–8 weeks of a project), with a frictionless path to BIM handoff.

## 2. Competitive landscape (summary)

| Tool | Strength | Weakness we exploit |
|---|---|---|
| **SketchUp** | Easy conceptual modeling, huge library | Desktop-first, collab is file-sync, stagnant 10 yrs |
| **ArchiCAD** | Solo-architect friendly BIM | Desktop-only, $5k+, heavy for concept |
| **Revit** | Industry BIM standard | Brutal UX, $335/mo, useless for concept |
| **AutoCAD** | 2D lingua franca | Legacy, expensive, no 3D workflow |
| **Vectorworks** | Flexible 2D/3D | Crashes, dongle licensing, slow |
| **Rhino** | Freeform/parametric | No realtime collab, node graphs scare non-coders |
| **Snaptrude** | Closest to our vision, BIM-forward web tool | Heavy, opaque pricing, no community |
| **Forma** | AI site analysis | Siloed to urban/feasibility |
| **Arkio** | VR collab sketching | VR-first is still a niche |

**Gap:** No one has built a browser-native, multiplayer, concept-phase modeler with a direct line to BIM export.

## 3. Target user & JTBD

**Primary:** Architects in conceptual/schematic design at studios of 2–50 people, plus design-forward teams at larger firms.

**JTBD:** *"When I'm exploring form, massing, and program with my team and clients in the first weeks of a project, help me iterate and communicate faster than redlining PDFs or screensharing SketchUp — and don't make me rebuild in Revit later."*

**Wedges:** architecture students (bottoms-up viral), interior designers, developers doing feasibility.

## 4. Seven differentiation bets

1. **Multiplayer cursors in 3D space** — avatars in world coordinates, voice bubbles per viewport. No more "share your screen."
2. **Shareable live URLs** — clients open a link, see the model in their browser, comment without signing up.
3. **Comments pinned to faces/edges/cameras** — threaded, @mention, resolve. Replaces Bluebeam markup.
4. **Prompt-to-massing** — "3 variants of a 12,000 sqft library, 30% daylight" → editable meshes, not images.
5. **Semantic concept model** — walls/slabs/roofs carry intent metadata; one-click IFC export feeds Revit/ArchiCAD without rebuilding.
6. **Live environmental HUD** — sun path, shadows, GFA/FAR, embodied carbon updating as you drag.
7. **Remixable component library** — Figma Community + GitHub for families/blocks. Attribution, forks, stars.

## 5. MVP scope (first 90 days)

1. Browser 3D modeler: draw, push/pull, extrude, boolean, move, rotate, scale.
2. Realtime multiplayer (Yjs CRDT) — cursors, selection, presence.
3. Shareable view-only link, no account needed for viewers.
4. Pinned comments with threads.
5. Import: OBJ, GLB, DWG 2D underlay. Export: OBJ, GLB, IFC.
6. Sun & shadow toggle, live GFA counter.
7. Components with simple shared library.
8. Free tier (2 editors, 3 projects, unlimited viewers) + $18/editor/mo Pro.

**Explicitly deferred:** full BIM walls/families, construction docs, node-graph parametrics, VR, native mobile, plugin SDK, AI generation (v2).

## 6. Technical architecture

- **Rendering:** Three.js (WebGPU path, WebGL2 fallback) + `three-mesh-bvh` for picking.
- **Geometry kernel:** Manifold (WASM) for interactive booleans, OpenCascade.js in a worker for precision/STEP, `web-ifc` for IFC I/O.
- **Realtime:** Yjs over WebSockets (Hocuspocus server), awareness channel for cursors.
- **Frontend:** React + Zustand, Vite, Tailwind.
- **Backend:** Node/Fastify or Rust/Axum, Postgres, S3-compatible blob store, Redis for presence.
- **Infra:** Cloudflare edge + Fly.io workers.
- **AI (v2):** LLM function-calling into modeler primitives for prompt-to-massing.

## 7. Pricing & GTM

- **Free:** 2 editors, 3 projects, unlimited viewers, public sharing.
- **Pro:** $18/editor/mo — unlimited projects, version history, private libraries.
- **Studio:** $30/editor/mo — SSO, IFC/Revit export, admin.
- **Education:** free (Figma playbook).

**Acquisition:**
1. Student ambassadors at Harvard GSD, AA, SCI-Arc, Columbia GSAPP, TU Delft, ETH, USP, Mackenzie.
2. Short-form video of multiplayer sessions (SketchUp physically can't produce this content).
3. Public remixable project gallery (SEO + network effects).
4. Export plugins into Revit/Rhino — *feed* the incumbents, don't fight them.
5. Partner with Enscape/Lumion/D5 for rendering.

## 8. Why now

- WebGPU shipping in all browsers (2024–2025).
- CRDT stacks mature (Yjs proven at Linear, tldraw, scale).
- Autodesk price hikes (2023–2025) created user revolt.
- Architects trained on Figma/Notion find Revit insulting.
- Snaptrude proved browser BIM works, left concept/presentation niche open.

## 9. Roadmap

- **Q1:** MVP prototype, closed alpha with 20 studios.
- **Q2:** Public beta, student program, IFC export.
- **Q3:** Comments, components library, Pro pricing live.
- **Q4:** AI prompt-to-massing, Revit/Rhino plugins.
- **Y2:** Semantic BIM layer, mobile/iPad, VR review.
