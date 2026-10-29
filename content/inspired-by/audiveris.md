+++
title = "Audiveris"
description = "Audiveris is an open-source optical music recognition (OMR) application that turns scans of sheet music into MusicXML. It complements Sheetmusic4J, which renders and plays that MusicXML but does no OMR."
weight = 85
+++

## What Is Audiveris?

[Audiveris](https://github.com/Audiveris/audiveris) is an open-source Java application for **optical music recognition** (OMR). You give it an image of a page of sheet music, such as a scan, a photo or an image-based PDF, and it recognizes the staves, notes and other symbols, and exports the result as MusicXML.

OMR is a hard problem, because the notation has to be rebuilt from pixels. That makes it a project of its own, and Audiveris is one of the few free options.

## How It Relates to Sheetmusic4J

The two projects solve different problems and don't depend on each other:

| | Audiveris | Sheetmusic4J |
|---|---|---|
| Input | Images: scans, photos, image-based PDFs | Structured scores: MusicXML, MIDI, ABC, LilyPond, Guitar Pro, engraved PDF |
| Job | Recognize the notation in the image | Parse, lay out, render and play a score |
| Output | MusicXML | A `Score` model, JavaFX or image rendering, MIDI |
| Does OMR | Yes | No |

They fit together as a pipeline. Audiveris can turn a scan into MusicXML, and Sheetmusic4J can then load, render and play that file like any other:

```java
// MusicXML exported by Audiveris from a scanned page
Score score = ScoreFile.load(Path.of("scanned-page.mxl"));
```

## Which Route for Which PDF?

| What you have | What to use |
|---|---|
| Scanned or photographed page, image-based PDF | An OMR tool such as Audiveris, then load the MusicXML in Sheetmusic4J |
| Engraved (vector) PDF, where the notes are font glyphs | Sheetmusic4J can read it directly, see [Engraved PDF](/inspired-by/engraved-pdf/) (under development) |
| MusicXML, MIDI, ABC, LilyPond, Guitar Pro | Sheetmusic4J reads these directly |

If you can't tell which kind of PDF you have, try selecting a single note with the mouse in a PDF viewer. If you can, it's engraved. If the whole page is selected as one image, it's a scan.

More info: [Audiveris on GitHub](https://github.com/Audiveris/audiveris).
