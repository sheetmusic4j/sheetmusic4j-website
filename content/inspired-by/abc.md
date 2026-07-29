+++
title = "ABC Notation"
description = "ABC is a compact, text-based music notation format widely used for folk and traditional tunes. Sheetmusic4J can import and export ABC files alongside MusicXML and MIDI."
weight = 70
+++

## What Is ABC Notation?

[ABC notation](https://abcnotation.com/) is a text-based format for writing down music. Instead of an XML tree or a binary blob, a tune is a short block of plain text: a header of information fields (`X:` tune number, `T:` title, `M:` meter, `L:` unit note length, `K:` key) followed by the notes themselves, written as letters with a handful of symbols for sharps, rests, bar lines, ties, slurs, and ornaments.

That compactness is why ABC became the de-facto standard for sharing folk and traditional tunes. A whole reel or jig fits in a few lines you can paste into an email, a forum post, or a tune database, and there are large public collections of ABC tunes that anyone can read with nothing more than a text editor.

Here's what a small tune looks like in ABC:

```abc
X:1
T:Speed the Plough
M:4/4
L:1/8
K:G
|:GABc dedB|dedB dedB|c2ec B2dB|c2A2 A2BA|
```

## Why Sheetmusic4J Supports It

ABC sits at the opposite end of the spectrum from MusicXML: where [MusicXML](/inspired-by/musicxml/) is verbose, tool-oriented, and exhaustive, ABC is terse, human-writable, and everywhere in the folk-music world. Supporting it means Sheetmusic4J can:

* **Read the huge body of existing ABC tunes** that people have collected and shared for decades.
* **Let users type music directly**, without a notation editor, and see it engraved.
* **Round-trip through a typed model.** ABC parses into the same `Score`/`Part`/`Measure`/`Note` model as everything else, so the engraving, JavaFX rendering, and MIDI export all work identically regardless of where the score came from.

## How Sheetmusic4J Uses ABC

The `core` module's `AbcReader` and `AbcWriter` parse and generate ABC files into and out of Sheetmusic4J's typed Java model. Coverage includes keys and modes, the unit note length, meter, tuplets, ties and slurs, grace notes, decorations (staccato, accent, roll, bow), barline styles, repeats and 1st/2nd endings, guitar chord symbols, lyrics, and multi-line `T:` titles/subtitles.

The `ScoreFile` facade dispatches automatically on the `.abc` extension, so most applications never touch the reader/writer classes directly:

```java
// Import: build a Score from an ABC tune
Score score = ScoreFile.load(Path.of("speed-the-plough.abc"));

// Export: write a Score back out as ABC
ScoreFile.save(score, Path.of("speed-the-plough-copy.abc"));
```

Because ABC is aimed at a specific slice of music (single-voice folk and traditional tunes, primarily), not every ABC feature maps cleanly onto a full engraving model, and not every MusicXML score can be expressed in ABC. It's a pragmatic, well-supported bridge into and out of the format rather than a lossless mirror of it.

More info: [abcnotation.com](https://abcnotation.com/).
