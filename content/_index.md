+++
title = "Sheetmusic4J :: A Java(FX) library for rendering and interacting with sheet music."
description = "Sheetmusic4J is an open-source Java library to parse MusicXML files into Java objects and generate music sheet JavaFX visualizations."
type = "home"
+++

<div class="sm4j-hero">
  <img class="sm4j-hero-logo" src="/favicon/android-chrome-512x512.png" alt="Sheetmusic4J logo" width="120" height="120" loading="eager">
  <h1 class="sm4j-hero-title">Sheetmusic4J for Java &amp; JavaFX</h1>
  <p class="sm4j-hero-sub">
    Parse and render sheet music in Java(FX).
    <br/>
    <strong>No WebView required.</strong>
  </p>
  <p class="sm4j-hero-release"><span class="sm4j-hero-dot"></span> No release yet...</p>
  <p class="sm4j-hero-cta">
    <a class="sm4j-btn sm4j-btn-primary" href="#quick-start"><i class="fas fa-rocket"></i> Get Started</a>
    <a class="sm4j-btn sm4j-btn-ghost" href="https://github.com/sheetmusic4j/sheetmusic4j" target="_blank"><i class="fab fa-github"></i> View on GitHub</a>
  </p>
</div>

**Sheetmusic4J is an open-source Java library that parses MusicXML into Java objects and renders them as native JavaFX music sheet views — no WebView, no browser engine, no JavaScript bridge.**

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
TODO
```

## Why Sheetmusic4J

{{< cards >}}
  {{% card title="Native JavaFX rendering" icon="fas fa-bolt" %}}
Drawn straight to a JavaFX `Canvas`. No browser, no JS bridge. It's just a `Node`.
  {{% /card %}}
  {{% card title="Parse &amp; generate" icon="fas fa-code" %}}
Read MusicXML into typed Java objects, and write valid files back out.
  {{% /card %}}
  {{% card title="Modern, minimal Java" icon="fab fa-java" %}}
Built on Java 21 LTS with Records — a small, maintainable codebase.
  {{% /card %}}
  {{% card title="Lightweight &amp; offline-first" icon="fas fa-feather" %}}
Needs only `javafx.graphics`. Fast startup, tiny jlink footprint, no network.
  {{% /card %}}
{{< /cards >}}

The sources of this project are available on [github.com/sheetmusic4j/sheetmusic4j](https://github.com/lottie4j/lottie4j).

