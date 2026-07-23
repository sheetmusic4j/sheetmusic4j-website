+++
title = "MusicXML"
description = "MusicXML is the open, standard format for exchanging digital sheet music between notation software. It's the file format Sheetmusic4J reads and writes."
weight = 10
+++

## What Is MusicXML?

[MusicXML](https://www.musicxml.com/) is the standard open format for exchanging digital sheet music. It's a universal, XML-based way to represent Western music notation: notes, rests, chords, clefs, key and time signatures, dynamics, lyrics, and much more, so that scores can move between different notation programs without losing information.

Before MusicXML, every notation application (Finale, Sibelius, MuseScore, ...) used its own proprietary file format. Sharing a score between two programs usually meant exporting to MIDI, which loses all the notation-specific information: beaming, slurs, articulations, dynamics, lyrics, part names, and so on. MusicXML solves that by giving every notation program a common, lossless(ish) interchange format.

## Why Sheetmusic4J Uses It

MusicXML is exactly the kind of open, well-documented standard that a library like Sheetmusic4J needs to build on:

* **It's an open standard**, maintained by the W3C Music Notation Community Group, with a public specification and versioned schema.
* **It's widely supported.** Finale, Sibelius, MuseScore, Dorico, and most other notation software can import and export it, so a `.musicxml` file is a realistic, general-purpose interchange point rather than a niche format.
* **It captures notation, not just sound.** Unlike MIDI, MusicXML models the actual engraving semantics (beams, ties vs. slurs, voice/staff assignment, part groups, chord symbols, ...) that a renderer needs to draw correct-looking sheet music.
* **Real-world example files are freely available**, which makes it possible to test a renderer against a broad set of real scores. Sheetmusic4J's test suite uses the [MusicXML example set](https://www.musicxml.com/music-in-musicxml/example-set/) for exactly this reason.

## How Sheetmusic4J Uses MusicXML

The `core` module's `MusicXmlReader` and `MusicXmlWriter` parse and generate MusicXML 4.0 files into and out of Sheetmusic4J's own typed Java model (`Score`, `Part`, `Measure`, `Note`, `Chord`, `Rest`, `Clef`, `KeySignature`, `TimeSignature`, ...). The `ScoreFile` facade dispatches automatically based on file extension (`.musicxml`, `.xml`, `.mxl`), so most applications never need to touch the reader/writer classes directly:

```java
Score score = ScoreFile.load(Path.of("song.musicxml"));
ScoreFile.save(score, Path.of("song-copy.musicxml"));
```

See the [code examples](/code-examples/) for more on loading and inspecting a `Score`.

More info: [musicxml.com](https://www.musicxml.com/).
