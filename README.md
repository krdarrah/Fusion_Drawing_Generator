# PCB Drawing Generator

Built by [KD Circuits](https://www.kdcircuits.com) — full product development, from idea to production.

A single-file, offline web tool that turns an EAGLE / Fusion 360 Electronics board file (`.brd`) into the fabrication and assembly documentation a board house needs. Everything runs in your browser; nothing is uploaded.

**Try it:** open `PCB_Drawing_Generator.html` (or the GitHub Pages site). A demo board loads on first open so you can click around.

## What it produces

- **Fab drawing** – board top/bottom views with overall dimensions and hole callouts, a Milling & Cutouts view when the board has internal cutouts or slots, General PCB Information table, lettered stack-up table with cross-section, drill table (Sym / N° / Mils / MM / Qty / Plated) with a drill map, auto-generated fab notes, part-number box and title block.
- **Assembly drawing** – silkscreen views, assembly views with collision-free reference designators, pin-1 dots, cathode (K) and polarity (+) marks read from the footprints, optional parts-list sheets, assembly notes.
- **Export** – one vector PDF containing both drawings (parts list included) at the exact sheet size: Letter by default, also Tabloid, A1–A4, ANSI B–D. Settings can be saved to and loaded from a `.json`.

## How to use it

1. In **Fusion 360 Electronics** open your PCB design and choose **File → Export → EAGLE 9.x**. Save the board as a `.brd`. (Files from EAGLE 6–9 work too.)
2. Open `PCB_Drawing_Generator.html` in a modern browser (Chrome, Edge, Firefox or Safari) and drop the `.brd` onto it.
3. Fill in the title block once (company, logo, name, SKU). The fab drawing uses `SKU-PCB` automatically.
4. Set the PCB specification. The panel mirrors the PCBWay order form (material, TG, thickness, finish, via process, special processes, etc.); the fab notes and the information table are generated from those choices. Standard PCBWay stack-ups are built in; the board's own design-rule stack-up or a custom one can be used instead.
5. Review the sheets. Drag any designator, callout or note to tidy the drawing (double-click to snap back). Use **+ Add note** to pin text to a spot on a view; drag the ring to move the spot.
6. **Download PDF** to get both drawings in one file.

Settings, hand-placed labels and notes are remembered per board name in the browser and can be saved to a `.json` with **Save settings**. When you rev a board, load the new `.brd` and the old `.json`; the notes and labels come along.

## Notes on conventions

- Bottom views are true views from the bottom. The board can be flipped left-over-right (page turn) or top-over-bottom; **Auto** picks the flip in which the board's own bottom-side text reads upright, and the caption states which was used.
- Drill sizes are finished sizes. Layers in the drill table are physical (L1 = top).
- Reference designators shown on assembly views are placed by the tool; silkscreen on the fab views is drawn exactly as the board defines it.
- Orientation marks are derived from the footprints (pad names and artwork). Verify against the schematic when in doubt; the drawing says so in its notes.

## Deep links

`PCB_Drawing_Generator.html#load=<board.brd>&settings=<settings.json>&doc=asm&sheet=2&cfg.fabSize=A3` loads a board (and optional settings) from a URL next to the page, opens a document/sheet, and overrides any setting by path.

## Development

Everything lives in one HTML file with no build step. The version and changelog are at the top of the file. One module is inlined between the `MODULES` markers: the label placement engine.

## License

MIT – see `LICENSE`. © 2026 KD Circuits LLC.
