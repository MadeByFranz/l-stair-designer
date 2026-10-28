# L-Stair Designer

Quarter-turn stair with a square landing, in the browser. Type in the opening and step counts, get plan and elevation drawings, a 3D model, a Finnish rules check and a cut list. One HTML file, no build, no server.

## Inputs

| Code | Field | Meaning |
|---|---|---|
| Y | Opening height | Floor to upper floor (finished levels) |
| X | Opening length | Slab edge to the far side of the landing, along the upper flight |
| E | Width of staircase | Both flights; the landing is E × E |
| Z | Stair thickness | Treads and landing deck |
| F | Stair nosing | Tread overhang past the riser line |
| C | Stairs in total | Landing counts as one stair |
| P | Lower steps | Up to and including the landing |
| H | Show risers | Closed risers (drawings, 3D, cut list) |
| SP | Top stair below the floor | On: one more rise up to the floor. Off: top stair is level with the floor |
| LR | Change staircase direction | Left / right turn |

How it is calculated:

- rises N = C + 1 (SP on) or C; rise R = Y / N
- going G = (X − E) / (C − P); same going in both flights
- lower flight run = (P − 1) × G, landing top at P × R

Structure settings (riser and stringer sizes, landing frame and posts, guard, slab), rule limits and the title block are in the collapsed groups.

## Outputs

- **Plan** and **Elevation** – hidden edges dashed, dimensions like a drawing office sheet, walking line, minimum floor opening for headroom
- **3D** – treads, risers, cut stringers, landing frame and posts, guard with balusters, walls and slab for context
- **A3 sheet** – both views at 1:20 / 1:25, key figures, title block
- **Steps & cut list** – heights, riser set-out, part sizes
- **Rules** – YMa 1007/2017: rise and going (§4), width (§3), guard (§7–8), handrails (§9), headroom (§14); step formula 2R + G as a comfort check. Pick “dwelling” (190 / 250) or “loft / storage” (220 / 220), or set your own limits. When rise or going fails, it suggests a C and P that pass for the same opening.

Export menu: PDF (A3), DXF (plan + elevation, layered, R12), SVG, PNG, OBJ (3D, mm, Y up), CSV cut list, JSON parameters. “Open…” loads a saved JSON.

There is also an inch ⇄ mm converter in the sidebar. The last design, open tab and display options are kept in the browser (localStorage).

## Put it on GitHub Pages

1. Create a repository, e.g. `stair-designer`.
2. Upload `index.html` (and this README) to the root.
3. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
4. Open `https://<username>.github.io/stair-designer/`.

It also runs by double-clicking `index.html`. The 3D viewer (three.js) and the PDF writer (jsPDF) load from jsDelivr the first time they are used, so those two need a connection.

## Notes

- Units are millimetres throughout.
- The rules check is a design aid, not an approval. Confirm the interpretation with the local building control (rakennusvalvonta).
- `window.LStair` in the browser console exposes `compute(params)` and the drawing functions for scripting.
