# Dodecahedron: The Excape — Prototype v1 engineering receipt

**Status:** Published browser prototype, not a finalized ruleset.  
**Implementation:** `dodecahedron-excape/index.html`; no external runtime dependencies.  
**Source requirements:** `Dodecahedron_The_Excape_Prototype_Spec_v1.md` supplied by the user.  
**Validation method:** JavaScript engine exercised with a simulated DOM, simulated animation frames, and in-memory localStorage. This is **not** a physical iPhone Safari playtest.

## Geometry

- [x] Original indexed icosahedron generates 12 vertices, 30 edges, 20 triangles.
- [x] Directed-edge truncation produces 60 indexed vertices, 12 pentagons, 20 hexagons, 32 faces, and 90 unique edges per shell.
- [x] Every edge is incident to exactly two faces and adjacency is reciprocal; face graph connected.
- [x] Three shells contain 96 rooms and 270 per-shell unique edge records.
- [x] Ten-room designated equator cycle has unique faces, closes through shared edges, and winds once around the sphere; winding = 1.
- [x] Stable room naming scheme `I/M/O-P00…P11` and `I/M/O-H00…H19`.

## Game rules

- [x] Four pawns begin together in I-P00; initial visits marked for both teams.
- [x] Build colors an edge once, with the same edge updating both incident rooms' tallies.
- [x] Building consumes that pawn's action; the two teammates can each act in one turn.
- [x] A pawn's second action in the same turn is denied; unused pawns may sit out.
- [x] Turns alternate Blue ↔ Orange.
- [x] Inner completed hex tie awards AB; middle completed hex tie awards none.
- [x] Outer margin 1 awards none; margin 2 awards leading team.
- [x] Defenders in either incident room block enemy recoloring but not neutral edge claims.
- [x] Cannot leave an unowned room; legal movement is to adjacent rooms.
- [x] Breadcrumbs are one boolean per team per room, not counters.
- [x] All designated equator rooms claimed opens the radial gate; revoking one relocks it.
- [x] Demo unlock bypasses equator gate but still requires current-room ownership.
- [x] Radial passage moves to corresponding face of next shell and consumes one action.

## View and interaction

- [x] Dragging rotates the camera and simple taps do not trigger pointer capture.
- [x] On-board current-room edge taps trigger paint actions.
- [x] Five edges of starting pentagon and five adjacent room choices are visible in the DOM.
- [x] Focus preserves zoom, yaw and pitch, smoothly panning the camera target.
- [x] Four pawns have distinct individual shades within two team colors.
- [x] State and visited rooms restore from saved localStorage; undo restores prior action.
- [x] Movement, edge paint and attitude changes have frame-driven visual animations and action locks.

## Known limits and intentionally provisional rules

- This prototype uses SVG-projected 3D polygons and shell transparency, not closed volumetric chambers or a full Three.js raycaster.
- In **All** view, only the currently selected pawn's shell is interactable; use Inner/Middle/Outer filters to inspect other shells.
- Room exit requires full perimeter ownership. The equator ring is the verified fixed 10-room cycle.
- The `Developer / Demo Unlock` switch lets reviewers exercise radial moves without completing the entire ring.
- Independent shell rotation, traps, monsters, portals, remote multiplayer, and final escape victory are not implemented.
- The animated SVG and mobile touch targets have **not** yet been visually qualified on a physical iPhone. Live GitHub Pages deployment timing also depends on GitHub Pages.
- Geometry and gameplay tests are engineering checks under a simulated DOM, not end-to-end browser certification.

## Manual acceptance walkthrough

1. Open the game. Verify all four player badges and the three shells.
2. Select A1, tap a numbered pentagon edge: it turns blue; tap A2 and color another edge.
3. End Turn. Select B1 and B2 to color or defend. The game allows both or neither to act.
4. Complete every edge of I-P00; room ownership appears. Move a pawn one adjacent room; observe the animation and breadcrumb.
5. Drag the structure, adjust zoom, click A1/B1 focus buttons, and switch shell views.
6. For radial travel, enable Developer / Demo Unlock, finish ownership of your current room, then choose Outward Passage.
7. Refresh: painted edges, players, turn, camera, and breadcrumbs should survive. Undo a recent action.

**Publication:** https://mrgarmise.github.io/fiber-hustle/dodecahedron-excape/
