+++
title = "Engraved PDF"
description = "An engraved PDF holds its music as font glyphs and vector lines, not pixels. Sheetmusic4J is gaining an experimental reader that turns these PDFs into a Score without optical music recognition."
weight = 90
+++

{{% notice style="warning" title="Under development" %}}
Engraved PDF import is still being built and is not part of a release yet. Follow the progress in issue [#6](https://github.com/sheetmusic4j/sheetmusic4j/issues/6) and pull request [#9](https://github.com/sheetmusic4j/sheetmusic4j/pull/9). What is described below may still change.
{{% /notice %}}

## What Is an Engraved PDF?

Most PDFs of sheet music fall into one of two groups:

* **Scans and photos.** The page is an image. The notes are pixels, and turning them back into music takes [optical music recognition](/inspired-by/audiveris/) (OMR), which is hard.
* **Engraved PDFs.** Notation software such as Finale or [LilyPond](/inspired-by/lilypond/) exported the page with the music as **font glyphs and vector lines**. A notehead is a character in a music font, like a letter in a text. In a PDF viewer you can select individual notes with the mouse, the same way you select words.

That second group is what Sheetmusic4J can read, because the symbols are right there on the page and nothing needs to be recognized from pixels.

## Why Sheetmusic4J Supports It

The idea came from a [Reddit discussion](https://github.com/sheetmusic4j/sheetmusic4j/issues/6) about opening PDFs. Many freely shared scores, for example on [IMSLP](https://imslp.org/), are engraved PDFs, and there are few free tools that can read them. Reading them directly means:

* **No OMR needed.** The glyphs and their positions are exact, so there is no recognition guesswork.
* **The same pipeline as every other format.** The PDF becomes a `Score`, so engraving, JavaFX rendering and MIDI export work the same as for a MusicXML file.
* **A reference to compare against.** The demo app shows the loaded PDF next to the JavaFX rendering, so you can see how closely the engraving matches the original.

## What It Can Read

The `pdf` module registers as a `ScoreFormat` (load only), so `ScoreFile.load` handles `.pdf` files once the module is on the class or module path:

```java
// Build a Score from an engraved PDF
Score score = ScoreFile.load(Path.of("clarinet-part.pdf"));
```

Current coverage:

* **Music fonts:** Maestro (Finale) and Emmentaler (LilyPond). Other fonts need their own symbol table.
* **Read:** staves, clefs, key and time signatures, notes, chords, rests, dots, accidentals, stems, flags and beams for the durations, ties, slurs, tuplets, dynamics, hairpins, barlines and system breaks.
* **Not read yet:** text and tempo marks, articulations, lyrics, and a second voice on a staff unless its stems point the other way.

## Limitations

* **Scans are rejected.** A PDF without engraved staves fails with a `PdfException`. For those, use an OMR tool and load the MusicXML it produces.
* **Part matching is by position.** Staves are matched to parts by their position on the page, so orchestral scores that drop resting staves from some systems can end up with mixed-up parts.
* **It reads what the engraver drew.** The result is a reconstruction from the page layout, so it is less exact than the MusicXML the notation software could export. If you have the MusicXML, use that instead.

More info: [issue #6](https://github.com/sheetmusic4j/sheetmusic4j/issues/6) and [pull request #9](https://github.com/sheetmusic4j/sheetmusic4j/pull/9).
