+++
title = "Sheetmusic4J :: A Java(FX) library for rendering and interacting with sheet music."
description = "Sheetmusic4J is an open-source Java library to parse MusicXML files into Java objects and generate music sheet JavaFX visualizations."
type = "home"
+++

<div class="sm4j-hero">
  <img class="sm4j-hero-logo" src="/img/logo/sheetmusic4j.png" alt="Sheetmusic4J logo" loading="eager">
  <h1 class="sm4j-hero-title">Sheetmusic4J for Java &amp; JavaFX</h1>
  <p class="sm4j-hero-sub">
    Parse and render sheet music in Java(FX).
    <br/>
    <strong>No WebView required.</strong>
  </p>
  <p class="sm4j-hero-release"><span class="sm4j-hero-dot"></span> Latest release: <a href="/releases/">v0.0.3 · 2026-07-30</a></p>
  <p class="sm4j-hero-cta">
    <a class="sm4j-btn sm4j-btn-primary" href="#quick-start"><i class="fas fa-rocket"></i> Get Started</a>
    <a class="sm4j-btn sm4j-btn-ghost" href="https://github.com/sheetmusic4j/sheetmusic4j" target="_blank"><i class="fab fa-github"></i> View on GitHub</a>
  </p>
</div>

**Sheetmusic4J is an open-source Java library that parses MusicXML into Java objects and renders them as native JavaFX music sheet views: no WebView, no browser engine, no JavaScript bridge.**

## Quick start

Sheetmusic4J requires **Java 21 or higher** and is available from Maven Central. Add the `fxviewer` dependency (it includes the `core` library):

{{< tabs >}}
{{% tab title="Maven" %}}
```xml
<dependency>
    <groupId>com.sheetmusic4j</groupId>
    <artifactId>fxviewer</artifactId>
    <version>${sheetmusic4j.version}</version>
</dependency>
```
{{% /tab %}}
{{% tab title="Gradle (Kotlin)" %}}
```kotlin
implementation("com.sheetmusic4j:fxviewer:$sheetmusic4jVersion")
```
{{% /tab %}}
{{% tab title="Gradle (Groovy)" %}}
```groovy
implementation "com.sheetmusic4j:fxviewer:${sheetmusic4jVersion}"
```
{{% /tab %}}
{{< /tabs >}}

Then load a file and drop the view into your scene:

```java
Score score = ScoreFile.load(Path.of("song.musicxml"));

SheetView sheetView = new SheetView();
sheetView.setScore(score);

stage.setScene(new Scene(new ScrollPane(sheetView), 900, 600));
stage.show();
```

See the [code examples](/code-examples/) for the full, runnable application, core-only (parse/generate) usage, and play-along cursor/highlighting.

**Watch:** an introduction to Sheetmusic4J — Render Interactive Sheet Music in JavaFX (MusicXML Library).

{{< youtube D2uaHpvC9ao >}}

## Why Sheetmusic4J

{{< cards >}}
  {{% card title="Native JavaFX rendering" icon="fas fa-bolt" %}}
Drawn straight to a JavaFX `Canvas`. No browser, no JS bridge. It's just a `Node`.
  {{% /card %}}
  {{% card title="Parse &amp; generate" icon="fas fa-code" %}}
Read MusicXML into typed Java objects, and write valid files back out.
  {{% /card %}}
  {{% card title="Modern, minimal Java" icon="fab fa-java" %}}
Built on Java 21 LTS with Records, a small, maintainable codebase.
  {{% /card %}}
  {{% card title="Lightweight &amp; offline-first" icon="fas fa-feather" %}}
Needs only `javafx.graphics`. Fast startup, tiny jlink footprint, no network.
  {{% /card %}}
{{< /cards >}}

Wondering about the standards behind it? Read what [inspired Sheetmusic4J](/inspired-by/): MusicXML, OpenSheetMusicDisplay, MIDI, ABC notation, Guitar Pro, SMuFL, the Bravura music font, and the MusicXML.com test files. And check the [sheetmusic terminology](/notation-terminology/) glossary to see which class/method draws which notation element.

The sources of this project are available on [github.com/sheetmusic4j/sheetmusic4j](https://github.com/sheetmusic4j/sheetmusic4j).

## Used By

**[MelodyMatrix](https://melodymatrix.rocks/)** is a cross-platform MIDI recording and visualization app (Java, Kotlin, JavaFX) that turns live keyboard performances into real-time visual displays, including piano roll, staff notation, guitar fretboard, and chord diagrams. It uses Sheetmusic4J for its staff notation view.

![MelodyMatrix staff notation view, rendered with Sheetmusic4J](/img/melodymatrix/screenshot.png)

Building something with Sheetmusic4J? [Let us know](https://github.com/sheetmusic4j/sheetmusic4j/issues) and we'll add it here.

## Current status

Sheetmusic4J is at release **0.0.3**, still early and published to gauge interest in a native Java(FX) sheet music library before investing further. The module structure, domain model, layout engine, JavaFX rendering (including a play-along strip view with a moving cursor and per-note highlighting), and the demo app are all in place. On top of MusicXML and MIDI, it supports [ABC notation](/inspired-by/abc/) import/export (now fully wired into the `ScoreFile` facade) and basic, experimental [Guitar Pro](/inspired-by/guitarpro/) 7/8 import; rendering fidelity and format coverage are still being expanded.

Latest updates:

{{< latest-status 4 >}}

Follow the progress in the [status posts](/status/) and check the [release notes](/releases/) for the latest changes.

## Related projects

Sheetmusic4J follows the same approach as [Lottie4J](https://lottie4j.com/): parse a standard file format into typed Java objects and render it natively in JavaFX, without a WebView. Lottie4J does it for Lottie animations, Sheetmusic4J for MusicXML scores, and both are built on Java 21 with the same minimal, `javafx.graphics`-only footprint. See also [MelodyMatrix](https://melodymatrix.rocks/), the MIDI recording and visualization app that uses Sheetmusic4J for its staff notation view.
