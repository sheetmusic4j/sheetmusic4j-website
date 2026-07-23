+++
title = "MIDI"
description = "The Standard MIDI File format that Sheetmusic4J can import and export alongside MusicXML, using Java's built-in javax.sound.midi API."
weight = 3
+++

## What Is MIDI?

[MIDI](https://midi.org/) (Musical Instrument Digital Interface) is a decades-old standard for representing musical performance data: which note starts and stops, when, at what velocity, and on which channel/instrument. A Standard MIDI File (`.mid`/`.midi`) stores that same event data as one or more tracks of timestamped messages.

Unlike MusicXML, MIDI has no concept of notation. It doesn't know about beams, slurs, key signatures as engraving choices, part names, or lyrics; it only knows about sounding events on a timeline. That makes it a great interchange format for playback and DAWs, but a lossy one for anything that needs to be engraved back onto a staff.

## Why Sheetmusic4J Supports It

Sheetmusic4J's `core` module can both import a Standard MIDI File into a `Score` and export a `Score` back to MIDI, via `javax.sound.midi`, the MIDI API that has shipped with the JDK since Java 1.3. No external dependency is needed for MIDI support.

Importing MIDI is inherently lossy: only PPQ-based sequences are supported (the tick resolution becomes the MusicXML `divisions`), a default 4/4 time signature is assumed for barring, each track containing notes becomes one `Part`, and notes are laid out monophonically per measure with gaps becoming rests. It's a pragmatic bridge for getting *something* on the page from a MIDI file, not a substitute for a properly engraved MusicXML source.

## How Sheetmusic4J Uses MIDI

The `ScoreFile` facade dispatches to MIDI import/export automatically based on file extension, exactly like it does for MusicXML:

```java
// Import: build a Score from a Standard MIDI File
Score score = ScoreFile.load(Path.of("song.mid"));

// Export: write a Score back out as a Standard MIDI File
ScoreFile.save(score, Path.of("song.mid"));
```

Combined with `StripSheetView`'s `cursorTime` and per-note highlighting (see the [code examples](/code-examples/)), this is what makes it practical to drive a sheet music view directly from MIDI playback or an incoming MIDI clock, exactly the use case behind [MelodyMatrix](https://melodymatrix.rocks/).
