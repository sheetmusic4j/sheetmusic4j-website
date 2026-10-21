+++
title = "Sheetmusic4J Releases"
description = "Release notes and changelog for the Sheetmusic4J Java library, including new features, rendering fixes, and version history."
weight = 10
+++

## 2026-10-21, 0.0.5

LilyPond import and export, plus engraving improvements for tuplets and clefs. More info and details in [this blog post](/status/2026/20261021-release-0.0.5/).

* **Core**
  * **LilyPond (new)**: `LilyPondReader` and `LilyPondWriter` read and write `.ly` files, registered as a `ScoreFormat` service so `ScoreFile` handles the `.ly` extension. Supports `\relative`/`\fixed`/`\transpose`, all note-name languages, chords, ties, slurs, beams, tuplets, grace notes, repeats, `\partial`, multiple staves and voices, piano staves and staff groups, lyrics, chord names, dynamics, tempo and rehearsal marks, `\tag` and `\include`. Engraving tweaks and Scheme code are skipped. See [Inspired By: LilyPond](/inspired-by/lilypond/).
  * `LilyPondException` extends `ScoreFormatException`.
  * `Clef` gained `octaveChange` (treble clef with an 8 below or above).
  * `Tuplet` gained `actualNotes`, `normalNotes` and `placement`; the MusicXML reader and writer handle the tuplet `placement` attribute.
  * `Fraction` is now shared by the ABC reader/writer, with `Fraction.times`. New `KeySignature.alter(Step)` and `NoteType.quarters(dots)`.
* **Engraving and render**
  * Tuplet brackets and numbers go on the stem side (or the requested placement), clear beams, and support nested tuplets. `TupletPlacement` has a new `above` flag.
  * New glyphs for the octave clefs (G/F/C with 8 below, G with 8 above) and the percussion clef.
  * Note spacing uses `StrictMath` so layouts are identical on every CPU architecture.
* **FX Demo**
  * Opens `.ly` files, with a set of LilyPond sample scores and reference images.

Full differences are listed on [GitHub > compare/v0.0.4...v0.0.5](https://github.com/sheetmusic4j/sheetmusic4j/compare/v0.0.4...v0.0.5)

## 2026-10-16, 0.0.4

A big release with two new interactive views, a new module structure for rendering, and a thorough architectural cleanup. More info and details in [this blog post](/status/2026/20261016-release-0.0.4/).

* **New modules**
  * **`render`**: toolkit-neutral drawing of a `LayoutResult` through the `RenderSurface` abstraction. `ScorePainter`, `RenderSurface`, `RenderColor`, `NoteBackgroundStyle`, `SmuflGlyphs` and the Bravura font moved here from `fxviewer` (same `com.sheetmusic4j.render` package). `fxviewer` depends on it transitively, so existing `fxviewer` users don't need to change anything.
  * **`render-awt`**: headless rendering to images through AWT, with `AwtRenderSurface` and `HeadlessScoreImage.render(score, width)` returning a `BufferedImage`, no display or JavaFX needed.
  * All library modules are now proper JPMS modules with a `module-info.java`.
* **FX Viewer**
  * **`NodeSheetView` (new)**: a retained-mode view that builds a JavaFX scene graph with one `Group` per note, rest and chord, so each element can take mouse and keyboard events, effects and tooltips. Hover and selection are built in, with `setOnElementClicked`/`setOnElementHover` callbacks.
  * **`FlyOverSheetView` (new)**: a 3D variant of the strip view: the score lies on a sheet of paper, a perspective camera flies along it while it plays, a glowing ball per voice hops from note to note, and sounding noteheads light up.
  * `SheetView` gained play-along support: a `cursorTime` cursor on the playing system, `revealTime` to fill the page in note by note, and `pageColor`/`inkColor` properties.
  * `StripSheetView` gained `revealTime` and `pageColor`/`inkColor`, and barlines now line up across staves.
  * Performance and memory improvements: tiled layout drawing (only the visible region is painted) and a shared font cache.
* **Engraving**
  * The monolithic `Engraver` was split into focused packages (`analysis`, `page`, `spacing`, `staff`, `glyph`, `text`), guarded by new layout snapshot tests.
  * New `PlaybackTimeline` maps playback time to layout positions, used by the cursor and reveal features.
  * `LayoutResult.hitTest(x, y)` finds the note at a layout position, so canvas-based views can do picking too.
  * Fixed barline thickness.
* **Core**
  * New `ScoreFormat`, `ScoreReader` and `ScoreWriter` interfaces. All readers and writers implement them, `ScoreFile` dispatches through them, and additional formats can be plugged in as `ServiceLoader` services.
  * Format exceptions (`MusicXmlException`, `MidiException`, `AbcException`, `GuitarProException`) now share a common `ScoreFormatException` base class.
  * Exact rhythmic arithmetic with the new `Fraction` record and `MeasureTiming`.
  * Size limits on reading compressed files (`.mxl`, `.gp`) to guard against oversized archives.
* **FX Demo**
  * New `FlyOverDemoApp` and `NodeDemoApp` (drag notes to move them, Shift for sharp, Alt/Option for flat), available as the `-Pflyover` and `-Pnode` Maven profiles next to `-Pstrip`.
  * New "Report Visual Issue..." button that captures screenshots and a description to report rendering differences, see [CONTRIBUTING.md](https://github.com/sheetmusic4j/sheetmusic4j/blob/main/CONTRIBUTING.md).

Full differences are listed on [GitHub > compare/v0.0.3...v0.0.4](https://github.com/sheetmusic4j/sheetmusic4j/compare/v0.0.3...v0.0.4)

## 2026-07-30, 0.0.3

A small patch release that finishes wiring [ABC notation](/inspired-by/abc/) into the `ScoreFile` facade. More info and details in [this blog post](/status/2026/20260730-release-0.0.3/).

* **`ScoreFile`**
  * `ScoreFile.load()` and `ScoreFile.save()` now actually dispatch `.abc` files to `AbcReader` and `AbcWriter`. In 0.0.2 those classes existed, but the facade did not yet recognize the `.abc` extension, so loading or saving an ABC file through `ScoreFile` failed with an `Unsupported file extension` error. Direct use of `AbcReader`/`AbcWriter` was unaffected.
  * Added round-trip tests covering `.abc` load and save through the facade.

Full differences are listed on [GitHub > compare/v0.0.2...v0.0.3](https://github.com/sheetmusic4j/sheetmusic4j/compare/v0.0.2...v0.0.3)

## 2026-07-29, 0.0.2

The second release of Sheetmusic4J, focused on two new input formats and a broad round of rendering improvements. More info and details in [this blog post](/status/2026/20260729-release-0.0.2/).

* **ABC notation (new)**
  * Import **and** export of [ABC music notation](/inspired-by/abc/) files (`.abc`), via new `AbcReader` and `AbcWriter` classes in `core`.
  * Coverage includes keys and modes, unit note length, meter, tuplets, ties and slurs, grace notes, decorations (staccato/accent/roll/bow), barline styles, repeats and 1st/2nd endings, guitar chord symbols, lyrics, and multi-line `T:` titles/subtitles, with round-trip tests.
* **Guitar Pro (new, experimental)**
  * Basic import of [Guitar Pro](/inspired-by/guitarpro/) 7/8 files (`.gp`, load only), reading the GPIF XML payload with the JDK only (no third-party dependency). Guitar Pro is not an open format; this support is based on the community's documented reverse-engineering of it. Added to gauge how people want to use it, so feedback is very welcome. Older binary formats (`.gp3`/`.gp4`/`.gp5`/`.gpx`) are not supported.
* **`ScoreFile`**
  * The facade now dispatches on `.abc` (load/save) and `.gp` (load only) in addition to `.musicxml`, `.xml`, `.mxl`, `.mid`, and `.midi`.
* **Engraving**
  * Grace notes render as small flagged/beamed notes with a connecting curve, with the beam raked to follow the run's pitch contour and horizontal space reserved for the group.
  * Distinct flag glyphs for 32nd/64th/128th notes, and a dedicated double-whole (breve) notehead.
  * Ties and slurs default to the opposite side of the stem; the tuplet bracket is omitted when the run already beams cleanly.
  * Barline styles, repeat dots and voltas/endings; articulations hug the notehead; chord symbols sit closer to the staff; improved title/subtitle clearance and accidental spacing.
* **FX Viewer**
  * New `NoteBackgroundStyle` API to configure the rounded-rectangle highlight drawn behind a note (defaults/tight presets, measured in staff-line gaps).
  * Fixed a crash on large scores by rendering through a windowed single canvas instead of one oversized texture.
* **FX Demo**
  * Reorganized into focused packages, added a standalone `StripDemoApp` play-along demo, and added image-based side-by-side comparison alongside the PDF view.
* **Under the hood**
  * Introduced logging via SLF4J in the library (Log4j2 binding in the demo app).
  * MusicXML reader now merges multiple `<attributes>` blocks per part instead of overwriting, and MIDI import produces fewer spurious rests.

Full differences are listed on [GitHub > compare/v0.0.1...v0.0.2](https://github.com/sheetmusic4j/sheetmusic4j/compare/v0.0.1...v0.0.2)

## 2026-07-23, 0.0.1

The first release of Sheetmusic4J, published to gauge interest in a native Java(FX) sheet music library before investing further. More info and details in [this blog post](/status/2026/20260723-release-0.0.1/).

* **Core**
  * Domain model for `Score`, `Part`, `Measure`, `Note`, `Chord`, `Rest`, `Clef`, `KeySignature`, `TimeSignature`, `Harmony`, `Lyric`, and more.
  * Loading and saving of MusicXML 4.0 files.
  * Importing and exporting MIDI files (`javax.sound.midi`).
  * `ScoreFile` convenience facade that dispatches to the right reader/writer based on file extension (`.musicxml`, `.xml`, `.mxl`, `.mid`, `.midi`).
* **Engraving**
  * Framework-agnostic layout engine (no JavaFX dependency) that positions staves, measures, clefs, and notes from a `Score` into a `LayoutResult`.
  * Support for beams, ties and slurs, tuplets, dynamics hairpins, articulations, directions (words, tempo, dynamics), rehearsal marks, chord symbols, lyrics, and part groups (brackets/braces across parts).
* **FX Viewer**
  * `SheetView`, a JavaFX `Region` rendering a `Score` on a `Canvas`, with zoom and configurable system width.
  * `StripSheetView`, a one-line play-along view with a fixed cursor and live per-note highlighting, driven by `cursorTime`.
* **FX Demo**
  * Standalone JavaFX demo application to load MusicXML/MIDI files, inspect the score, and view debug information, with a companion PDF side-by-side view for checking rendering fidelity.

The full source is available on [github.com/sheetmusic4j/sheetmusic4j](https://github.com/sheetmusic4j/sheetmusic4j).