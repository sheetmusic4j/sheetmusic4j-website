+++
title = "LilyPond"
description = "LilyPond is a free, text-based music engraving program known for its beautiful output. Sheetmusic4J can import and export LilyPond .ly files alongside MusicXML, MIDI and ABC."
weight = 75
+++

## What Is LilyPond?

[LilyPond](https://lilypond.org/) is a free, open-source music engraving program, part of the GNU project. You don't drag notes onto a staff: you write the music as plain text in a `.ly` file, and LilyPond compiles it into a PDF (or PNG, SVG, MIDI). Its stated goal is engraving quality on par with traditionally hand-engraved scores, and many musicians, publishers and projects like the [Mutopia Project](https://www.mutopiaproject.org/) use it for exactly that reason.

The input language is more of a programming language than a data format. Notes are written as Dutch (or English, German, Italian...) note names with octave marks and durations, music is grouped into staves, voices and staff groups with `\new` and `<< >>`, and you can define variables, include other files, and even run Scheme code. Here's a short melody:

```lilypond
\version "2.24.0"
\header {
  title = "C Major Scale"
}

\relative c' {
  \clef treble
  \key c \major
  \time 4/4
  c4 d e f | g a b c | c b a g | f e d c |
}
```

## Why Sheetmusic4J Supports It

Where [ABC](/inspired-by/abc/) covers folk tunes and [MusicXML](/inspired-by/musicxml/) is the exchange format between notation editors, LilyPond is the format of choice for people who care about engraving and like to work in a text editor and under version control. A large body of classical repertoire, from Bach chorales to full orchestral scores, is available as `.ly` source. Supporting it means Sheetmusic4J can:

* **Open existing LilyPond scores** and show them natively in JavaFX, without running LilyPond itself.
* **Export any score to LilyPond**, so a file loaded from MusicXML, MIDI or ABC can be handed to LilyPond for high-quality PDF output.
* **Learn from the best.** LilyPond's engraving and its extensive documentation are a constant reference for how Sheetmusic4J's own engraving should look.

## How Sheetmusic4J Uses LilyPond

The `core` module's `LilyPondReader` reads a `.ly` file the way LilyPond itself does, in three steps: a parser builds a music tree (resolving the note-name language, default durations and variables), an interpreter runs it through time into contexts (staff groups, staves, voices, lyrics, chord names), and an assembler cuts the result into measures and derives what LilyPond leaves implicit, such as ties across bar lines, accidentals, beams and gap rests. The result is the same typed `Score` model as every other format, so engraving, JavaFX rendering and the other exporters work identically.

The reader understands a large part of the language:

* `\relative`, `\fixed` and `\transpose`, and all note-name languages
* chords (including `q`), ties, slurs, explicit and automatic beams, tuplets and grace notes
* `\repeat` (volta with alternatives, unfold, percent, tremolo), `\partial` and `\cadenzaOn`
* multiple staves and voices (`<< \\ >>`, `\new Voice`, `\change Staff`), piano staves, staff groups and instrument names
* lyrics (`\addlyrics`, `\lyricsto`), chord names, dynamics, hairpins, text scripts, tempo and rehearsal marks
* `\tag` filtering and `\include` of files next to the score
* the `\header` fields title, subtitle/piece, composer, arranger, poet and lyricist

Engraving tweaks (`\override`, `\tweak`) and Scheme code are skipped: Sheetmusic4J does its own layout. Only the first `\score` of a file is read.

The `LilyPondWriter` writes each part as a `\score` with a `\new Staff`, in absolute pitch mode, using the same subset the reader understands, so a read/write/read round-trip stays structurally stable.

The `ScoreFile` facade dispatches automatically on the `.ly` extension:

```java
// Import: build a Score from a LilyPond file
Score score = ScoreFile.load(Path.of("bach-bwv610.ly"));

// Export: convert any score, e.g. a MusicXML file, to LilyPond
ScoreFile.save(ScoreFile.load(Path.of("song.musicxml")), Path.of("song.ly"));
```

LilyPond's input language is huge and programmable, so Sheetmusic4J will never read every `.ly` file the way LilyPond does. The goal is to correctly read the music itself in real-world scores. If you find a file that doesn't load or look right, [an issue with the file attached](https://github.com/sheetmusic4j/sheetmusic4j/issues) is the best way to get it fixed.

More info: [lilypond.org](https://lilypond.org/).
