# PCB Drawing Generator

Built by [KD Circuits](https://www.kdcircuits.com) — full product development, from idea to production.

A single-file, offline web tool that turns an EAGLE / Fusion 360 Electronics board file (`.brd`) into the fabrication and assembly documentation a board house needs. Everything runs in your browser; nothing is uploaded.

**Try it:** open `PCB_Drawing_Generator.html` (or the GitHub Pages site). A demo board loads on first open so you can click around.

## What it produces

- **Fab drawing** – board top/bottom views with overall dimensions and hole callouts, a Milling & Cutouts view when the board has internal cutouts or slots, General PCB Information table, lettered stack-up table with cross-section, drill table (Sym / N° / Mils / MM / Qty / Plated) with a drill map, auto-generated fab notes, part-number box and title block.
- **Assembly drawing** – silkscreen views, assembly views with collision-free reference designators (sized to sit on their own part, turned 90° when the part is tall, halo instead of a box so pads stay visible; a leader only when there is no room), pin-1 dots, cathode (K) and polarity (+) marks read from the footprints, optional parts-list sheets, assembly notes. Dense boards automatically get one side per sheet.
- **Hand assembly mode** – a third view for building boards by hand: the board drawn large with one list row per value and package (one bag or reel). Click a row, or a part, and every part in that group lights up while the rest of the board fades; search by value, package, designator or part number; tick groups as placed (remembered per board); step through with the keyboard (arrows, Space, Enter, Z to zoom to the selection, / to search). Pin-1, cathode and polarity marks show on the highlighted parts.
- **Export** – one vector PDF containing both drawings (parts list included) at the exact sheet size: Letter by default, also Tabloid, A1–A4, ANSI B–D. A Fabmaster `.fab` (FATF REV 11.1) file equivalent to CadSoft's `fabmasterF360.ulp`. Settings can be saved to and loaded from a `.json`, and a `.pcbdg` **project file** bundles the board itself (compressed), all settings, the logo, the notes and the hand-assembly progress, so one file is enough to hand the whole thing to someone else.

## How to use it

1. In **Fusion 360 Electronics** open your PCB design and choose **File → Export → EAGLE 9.x**. Save the board as a `.brd`. (Files from EAGLE 6–9 work too.)
2. Open `PCB_Drawing_Generator.html` in a modern browser (Chrome, Edge, Firefox or Safari) and drop the `.brd` onto it.
3. Fill in the title block once (company, logo, name, SKU). The fab drawing uses `SKU-PCB` automatically.
4. Set the PCB specification. The panel mirrors the PCBWay order form (material, TG, thickness, finish, via process, special processes, etc.); the fab notes and the information table are generated from those choices. Standard PCBWay stack-ups are built in; the board's own design-rule stack-up or a custom one can be used instead.
5. Pick a drawing style (Classic, Blueprint, Colorful, Tactical, KD Circuits, Dark) from the dropdown above the sheet, and tick **Realistic board colors** in the Sheet panel to render the board with the ordered mask, surface finish and silkscreen colors.
6. Review the sheets. Drag any designator, callout or note to tidy the drawing; double-click a designator to turn it 90°, Alt+double-click to snap it back (callouts snap back on double-click). Use **+ Add note** to pin text to a spot on a view; drag the ring to move the spot. Every pinned note is listed in the **Drawing notes** panel, where its text can be edited or the note deleted; double-clicking a note on the sheet edits it in place.
7. **Download PDF** to get both drawings in one file.
8. When the boards arrive, switch to **Hand assembly** and work down the list. **Fabmaster .fab** writes the FATF file for the loaded board.

Settings, hand-placed labels and notes are remembered per board name in the browser and can be saved to a `.json` with **Save settings**, or together with the board as a `.pcbdg` with **Save project** (drop it on the page, or open `PCB_Drawing_Generator.html#project=<url of the .pcbdg>`). When you rev a board, load the new `.brd` and the old `.json`; the notes and labels come along.

## Notes on conventions

- Bottom views are true views from the bottom. The board can be flipped left-over-right (page turn) or top-over-bottom; **Auto** picks the flip in which the board's own bottom-side text reads upright, and the caption states which was used.
- Drill sizes are finished sizes. Layers in the drill table are physical (L1 = top).
- Reference designators shown on assembly views are placed by the tool; silkscreen on the fab views is drawn exactly as the board defines it.
- Orientation marks are derived from the footprints (pad names and artwork). Verify against the schematic when in doubt; the drawing says so in its notes.

## Deep links

`PCB_Drawing_Generator.html#load=<board.brd>&settings=<settings.json>&doc=asm&sheet=2&cfg.fabSize=A3` loads a board (and optional settings) from a URL next to the page, opens a document/sheet, and overrides any setting by path. `#project=<file.pcbdg>&doc=build` opens a project file the same way, straight into Hand assembly.

## Development

Everything lives in one HTML file with no build step. The version and changelog are at the top of the file. Three modules are inlined between the `MODULES` markers: a small XML parser, the label placement engine, and the Fabmaster FATF port.

## Feedback

Suggestions, bugs or feature ideas: [contact KD Circuits](https://www.kdcircuits.com/#contact) or open an issue on [GitHub](https://github.com/krdarrah/Fusion_Drawing_Generator/issues).

## License

MIT – see `LICENSE`. © 2026 KD Circuits LLC.
