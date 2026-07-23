+++
title = "Bravura"
description = "Bravura is the reference SMuFL music font Sheetmusic4J uses to draw clefs, noteheads, rests, and every other engraved symbol."
weight = 50
+++

## What Is Bravura?

[Bravura](https://github.com/steinbergmedia/bravura) is Steinberg's reference font implementation of [SMuFL](/inspired-by/smufl/) (Standard Music Font Layout), the open specification that maps musical symbols (clefs, noteheads, accidentals, rests, dynamics, articulations, and hundreds more) to consistent code points in a font. Any SMuFL-compliant font can be swapped in for another without an application needing to change how it looks up glyphs.

Bravura is released under the [SIL Open Font License, Version 1.1](https://github.com/steinbergmedia/bravura/blob/master/redist/OFL.txt), so it's free to redistribute alongside an application.

## Why Sheetmusic4J Uses It

Drawing correct-looking sheet music means drawing the *actual* engraving glyphs, not approximations built out of lines and circles. Rather than designing a custom glyph set, Sheetmusic4J's `fxviewer` module bundles Bravura and looks up every glyph it draws (clefs, noteheads, rests, time-signature digits, accidentals, articulations, dynamics, and more) by its standard SMuFL code point.

Because SMuFL is a standard, this also means Sheetmusic4J's rendering vocabulary lines up with other SMuFL-aware tools: the same code point that draws a treble clef in Bravura draws a treble clef in every other SMuFL font, and in every other SMuFL-compliant renderer.

## How Sheetmusic4J Uses It

`fxviewer`'s render surfaces (`FxRenderSurface` for on-screen JavaFX, `AwtRenderSurface` for headless test/demo rendering) detect `Bravura.otf` on the classpath and draw glyphs using the font's SMuFL glyph names and code points. If the font is unavailable, the renderer falls back to simplified primitive/text shapes rather than failing, so a build without the font still produces a legible (if plainer) result.

More info: [Bravura on GitHub](https://github.com/steinbergmedia/bravura) and the [SMuFL specification](/inspired-by/smufl/).
