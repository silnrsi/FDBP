---
published: true
layout: bookpage
weight: 340
outlevel: 5.4
category: Composite Glyphs
title: Composite Glyphs
---

Composite glyphs are made by referencing one or more other glyphs in the font. For example, the glyph for "é" can be composed of the glyph for the letter "e" (as the base) and the glyph for the acute accent (as the diacritic, or mark).

Using composite glyphs saves design time by not requiring that each base and diacritic combination be drawn separately.

It can also improve consistency since, for example, there is only one copy of the acute accent which is referenced by every glyph that needs it.

One format for describing composites uses a single line in a text file to define the resulting glyph as a combination of other glyphs. The tool described in [Composite Tools](Composite_Tools.html) uses this format.
