+++
title = "MusicXML Test Files"
description = "The MusicXML.com example set Sheetmusic4J uses as real-world test fixtures for its MusicXML reader, writer, and engraving layout."
weight = 6
+++

## What Is the MusicXML Example Set?

MusicXML.com publishes a [set of example MusicXML files](https://www.musicxml.com/music-in-musicxml/example-set/): real scores, from a single-staff melody up to a full orchestral score, released specifically so that developers of notation software can test their MusicXML support against realistic, varied input rather than hand-crafted toy files.

## Why Sheetmusic4J Uses Them

A MusicXML reader that only handles the elements a developer thought to write test cases for will break on the first real-world file a user throws at it. Real scores combine features in ways that are easy to miss when testing in isolation: multi-voice parts, part groups with braces and brackets, chord symbols alongside lyrics, tuplets nested inside beamed runs, and so on.

Testing against the MusicXML.com example set gives Sheetmusic4J's reader, writer, and engraving layout a broad, realistic baseline to develop and regress against, instead of only the specific fixtures a contributor happened to author.

## How Sheetmusic4J Uses Them

Files from the example set are used throughout the `core`, `engraving`, and `fxdemo` test suites, both for round-trip parsing/writing checks and for the headless rendering comparisons used to catch engraving regressions (see the [Sheetmusic Terminology](/notation-terminology/) page for how a rendered element maps back to the responsible code).

More info: [musicxml.com example set](https://www.musicxml.com/music-in-musicxml/example-set/).
