+++
title = "Sheetmusic4J Releases"
description = "Release notes and changelog for the Sheetmusic4J Java library, including new features, rendering fixes, and version history."
weight = 10
+++

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