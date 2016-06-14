---
published: true
layout: bookpage
weight: 10
outlevel: 2
category: Source Formats
title: Source Formats
---

Installable, end-user fonts come in a variety of formats: OpenType (containing either Postscript/CFF or TrueType glyph data), TrueType, PS Type 1, SVG, WOFF, and others. The current standard for most uses is [OpenType].

Although many font tools can use these end-user formats as source for derivative fonts, it is more common to store master font data in formats specifically designed for that purpose. These are usually associated with a particular application, such as FontLab (.vfb), FontForge (.sfd), and Glyphs (.glyphs). They contain data such as guidelines and multiple layers that may be useful in the design process but are not present in the end-user font. The formats vary in their levels of openness and documentation.

**We recommend that new font projects avoid these proprietary formats and instead adopt an open, platform-neutral standard: [UFO (Unified Font Objects)][UFO].** UFO is a public, human-readable, text-based source format for storing font source data. It's now being used by many foundries, including Adobe, as their primary source format. [Read more about using UFO](UFO.html).

This book will also cover relevant issues for other source formats.

[OpenType]: https://en.wikipedia.org/wiki/OpenType
[UFO]: http://unifiedfontobject.org/
