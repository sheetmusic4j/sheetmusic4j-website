+++
title = "Guitar Pro"
description = "Guitar Pro is a popular tablature and notation editor. Sheetmusic4J has basic, experimental import of Guitar Pro 7/8 (.gp) files to gauge interest and gather feedback."
weight = 80
+++

## What Is Guitar Pro?

[Guitar Pro](https://www.guitar-pro.com/) is a widely used commercial application for writing, editing, and playing back tablature and standard notation, especially for guitar, bass, and other fretted instruments. Its files are a very large source of transcriptions shared by musicians, and the modern `.gp` format (Guitar Pro 7 and 8) stores a score as a **GPIF** XML document inside a ZIP archive.

## Why Support Is Experimental

Unlike [MusicXML](/inspired-by/musicxml/), [MIDI](/inspired-by/midi/), and [ABC](/inspired-by/abc/), Guitar Pro is **not an open format**. There is no published specification. The support in Sheetmusic4J is based on the music community's documented reverse-engineering of the GPIF format, so it is deliberately marked as basic and experimental.

The goal of this early support is to find out **how people actually want to use Guitar Pro files** with Sheetmusic4J before investing further:

* Is importing into the `Score` model and rendering it as standard notation enough?
* Is tablature-specific rendering needed?
* Which parts of the format matter most in practice?

If you have a use case, [feedback and sample files on GitHub](https://github.com/sheetmusic4j/sheetmusic4j/issues) are exactly what would help shape where this goes next.

## How Sheetmusic4J Uses Guitar Pro Files

The `core` module's `GuitarProImporter` reads a `.gp` file with the JDK only, no third-party dependency: it opens the ZIP archive, extracts the `score.gpif` payload, and parses that XML into Sheetmusic4J's typed `Score` model. From there the engraving, JavaFX rendering, and other exporters work exactly as they do for any other score.

Import is **load only**, and dispatched by the `ScoreFile` facade on the `.gp` extension:

```java
// Import a Guitar Pro 7/8 file (load only)
Score score = ScoreFile.load(Path.of("song.gp"));
```

Only the modern `.gp` format (Guitar Pro 7/8) is handled. The older binary formats (`.gp3`, `.gp4`, `.gp5`, `.gpx`) are intentionally not supported, and saving back to Guitar Pro is not supported.

More info: [guitar-pro.com](https://www.guitar-pro.com/).
