+++
title = "SMuFL"
description = "SMuFL is the open specification that maps music notation symbols to standard code points in a font, the standard Sheetmusic4J's Bravura-based glyph rendering is built on."
weight = 4
+++

## What Is SMuFL?

[SMuFL](https://www.smufl.org/) (Standard Music Font Layout) is an open specification that defines a standard way to map the thousands of symbols used in music notation, such as clefs, noteheads, accidentals, rests, articulations, and dynamics, to consistent code points in the Private Use Area of a font. It's maintained under the [W3C Music Notation Community Group](https://www.w3.org/community/music-notation/), the same community group that stewards MusicXML.

Before SMuFL, every music font used its own arbitrary glyph mapping, so a document referencing "code point U+E050" in one font meant something completely different in another. SMuFL fixes that by giving every notation symbol a stable, documented code point that any compliant font can implement.

## Why It Matters to Sheetmusic4J

Sheetmusic4J's `fxviewer` module draws every engraved symbol, clefs, noteheads, rests, accidentals, articulations, dynamics, and more, by looking it up as a named SMuFL glyph rather than hand-drawing shapes. That has two practical benefits:

* **The glyph font is swappable.** Because the lookup is by standard SMuFL name/code point rather than a font-specific glyph index, any SMuFL-compliant font could in principle replace [Bravura](/inspired-by/bravura/) (the font Sheetmusic4J currently bundles) without changing how the renderer looks things up.
* **The symbol vocabulary is shared** with every other SMuFL-aware notation tool, including [OpenSheetMusicDisplay](/inspired-by/opensheetmusicdisplay/) and the desktop notation editors that can import/export the MusicXML files Sheetmusic4J reads and writes.

## How Sheetmusic4J Uses It

The `engraving` module's `Glyph` enum names every symbol Sheetmusic4J can place (`CLEF_G`, `NOTEHEAD_BLACK`, `ACCIDENTAL_SHARP`, `REST_QUARTER`, and so on), and `fxviewer`'s render surfaces resolve each one to its SMuFL code point when drawing with the bundled Bravura font. See the [Sheetmusic Terminology](/notation-terminology/) glossary for how each rendered element maps from MusicXML, through the core model and layout, to the glyph that gets drawn.

More info: [smufl.org](https://www.smufl.org/) and the [W3C Music Notation Community Group](https://www.w3.org/community/music-notation/).
