+++
title = "OpenSheetMusicDisplay"
description = "OpenSheetMusicDisplay (OSMD) renders MusicXML sheet music in the browser and headless with Node.js. It's the JavaScript-world sibling Sheetmusic4J looked to for JavaFX."
weight = 30
+++

## What Is OpenSheetMusicDisplay?

[OpenSheetMusicDisplay](https://github.com/opensheetmusicdisplay/opensheetmusicdisplay) (OSMD) is an open-source JavaScript library that renders sheet music in MusicXML format: in browsers, and headless with Node.js. It builds on top of [VexFlow](https://github.com/0xfe/vexflow) for the actual music-symbol drawing, and adds MusicXML parsing plus the layout logic needed to turn a full score into readable, correctly engraved pages.

OSMD is widely used across web-based music applications: notation viewers, practice tools, music education apps, and anything else that needs to show real sheet music in a browser rather than a static image.

## Why It Inspired Sheetmusic4J

Sheetmusic4J exists because there wasn't a comparable option for **Java(FX)**. If you wanted to show MusicXML-based sheet music in a JavaFX application, the pragmatic answer was usually "embed a `WebView` and run OSMD (or a similar JS renderer) inside it." That works, but it drags a browser engine, a JavaScript bridge, and all the packaging/startup overhead that comes with it into an otherwise native desktop app.

OSMD demonstrated that the concept (parse MusicXML, run it through a layout engine, render it with a 2D drawing API) is entirely practical as a standalone library, without depending on a full notation editor. Sheetmusic4J follows the same shape, aimed at the JavaFX and `Canvas` world instead of the DOM/SVG world:

| | OpenSheetMusicDisplay | Sheetmusic4J |
|---|---|---|
| Input format | MusicXML | MusicXML |
| Runtime | Browser / Node.js | Java(FX) |
| Drawing target | SVG / Canvas (via VexFlow) | JavaFX `Canvas` |
| Language | TypeScript | Java 21 |

## No WebView Required

Because Sheetmusic4J parses and engraves MusicXML natively in Java and draws straight to a JavaFX `Canvas`, a JavaFX application can render sheet music as a plain `Node` in its scene graph: no `WebView`, no bundled browser engine, no JS bridge to marshal data across.

More info: [opensheetmusicdisplay on GitHub](https://github.com/opensheetmusicdisplay/opensheetmusicdisplay).
