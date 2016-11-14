---
published: true
layout: bookpage
weight: 210
outlevel: 4.1
category: Glyph Metadata
title: Characters and Glyphs
---

It may seem obvious that a font must contain symbols for each _letter_ or _character_ of the writing system in focus. However, each of those _characters_ may be visually represented by one or more _glyphs_ - the individual graphic shapes defined in the font. At this point it's really important to have a clear understanding of the differences and interrelationships between characters, keystrokes, codepoints and glyphs. Chapter 2 of the online book [Implementing Writing Systems][IWSc2] is an excellent and thorough way to deepen that understanding.

**When choosing which characters to support we recommend that you consider the full range of uses for the font, both linguistic and typographic.** In addition to the basic letters, numerals, and punctuation, you may need to consider:

- letters and diacritics used for loan words, foreign terms, or names
- punctuation used in publishing applications, such as formal quote marks, text markers, footnote symbols, and special-width spaces

You may also need to consider alternate glyphs for special purposes, and create smart font rules for them:

- different numeral forms (old-style and tabular in Latin, for example)
- contextual alternates and ligatures

**Non-Latin fonts should also contain a basic set of Latin glyphs.** For technical reasons, the font is less likely to cause problems in certain OSes and environments if a basic Latin set is present. Our recommendation is that you support the following list: [Basic Set of characters needed in a Non-Roman font][basicLatin].

If you don't want to draw all of these Latin glyphs yourself, and are making a font that will be released freely under the [SIL Open Font License](Copyright_and_Licensing.html), you can get the glyphs from some other OFL font as long as you acknowledge the source and follow the conditions of the OFL.

[IWSc2]: http://scripts.sil.org/IWS-Chapter02
[basicLatin]: http://scripts.sil.org/BasicCharSet