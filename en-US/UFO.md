---
published: true
layout: bookpage
weight: 30
outlevel: 2.2
category: Source Formats
title: UFO
---

UFO (Unified Font Object) is our recommended format for new font projects, and can offer advantages for existing projects. The [UFO specification] calls it a "cross-platform, cross-application, human readable, future proof format for storing font data". It is a text-based format that draws on XML and plist structures. A UFO is a folder with a .ufo extension that contains files for font-wide metadata and a 'glyphs' folder that contains each glyph as a separate .glif file.

## UFO versions, or 'flavors'

UFO is actually not one single standard. There are multiple versions, or 'flavors' of UFO:

- *UFO 1* - The original from 2004. Rarely used now.
- *UFO 2* - The most common version (since 2009), with the broadest application support. Only slightly different from UFO 1. Still lacks some basic features, such as explicit glyph anchor elements.
- *UFO 3* - A much-improved and expanded spec from 2012. However adoption has been poor. Only FontForge offers UFO 3 support.

In practice, most foundries use UFO2, but may store application- or foundry-specific information in a `lib.plist` file. This can be a way of working around some of UFO2's deficiencies, and some applications even respect (don't touch) or read (use) `lib.plist` data added to a UFO by some other application. The [pysilfont] project includes a UFO normalizer and converter.

**We currently recommend storing UFO sources in UFO2 format, and relying on a UFO converter tool to move data between formats.**

There are various discussions going on towards future UFO versions beyond 3, by both the original UFO authors and others, but there is no clear successor at this point.

## Application support

Every major font design program supports UFO, but to varying degrees.

- [Robofont] provides the most seamless and native support.
- [Glyphs] can use UFO as a native format.
- [FontForge] can import and export UFOs, including the UFO3 format.

**We have used each of these successfully in UFO development, and can recommend their use. The key to successful use is to store UFOs in a normalized format then re-normalize them after editing them.**

- [Trufont] uses UFO as a native format, but is still early in development
- [Fontlab Studio 5][Fontlab] does not read or write UFO, but they provide a [vfb2ufo] converter that can be useful. It provides limited two-way conversion, but is mainly useful for one-time conversion into long-term UFO. They intend to support UFO more fully in version 6.

In addition to these visual design programs there are other applications and utilities that support UFO:

- [The Adobe Font Development Kit for OpenType][AFDKO]
- [Smith]
- [Tools from TypeSupply][TypeSupply]
- [pysilfont]

## Example projects

Adobe has a number of public projects that are based on UFO. [Source Sans Pro] is a good example.

SIL also has two example projects that we've used in testing UFO workflows: [Nokyung] and [Andika Mtihani].

## Why use UFO?

Our main motivation is that it is a well-supported, open, application-neutral format. We do not want to require that someone use a particular commercial program on a particular platform in order to access and use our font source. It also allows us to use common industry tools, and frees us from being locked into any one tool. It is handled well by version control systems, and has strong long-term readability.


[UFO specification]: http://unifiedfontobject.org/
[pysilfont]: https://github.com/silnrsi/pysilfont
[Robofont]: http://robofont.com/
[Glyphs]: https://glyphsapp.com/
[Trufont]: https://github.com/trufont/trufont
[FontForge]: https://fontforge.github.io
[FontLab]: http://old.fontlab.com/font-editor/fontlab-studio/
[vfb2ufo]: http://blog.fontlab.com/font-utility/vfb2ufo/
[Source Sans Pro]: https://github.com/adobe-fonts/source-sans-pro
[Nokyung]: https://github.com/silnrsi/font-nokyung
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani
[AFDKO]: https://github.com/adobe-type-tools/afdko
[TypeSupply]: https://github.com/typesupply
[Smith]: https://github.com/silnrsi/smith
