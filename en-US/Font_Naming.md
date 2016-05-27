---
published: true
layout: bookpage
weight: 110
category: Font Metadata
title: Font Naming
---

Fonts typically have two names by which they're identified: the internal font name that appears in application menus and the font filename. **These two names should be synchronized in a particular way.**

## Internal font names

The most effective font names (those seen in application menus, etc.) have a few characteristics:

- They are unique to the particular font family.
- They do not include "Unicode", as most fonts are Unicode-encoded. If the font is _not_ Unicode-encoded, then an indication of that may be added to the name, as in "Anaconda L" (for legacy).
- They do not include specific script or language names. If a font family has multiple language-specific versions, then some indication of the language (such as an [Ethnologue] code), may be added, as in "Anaconda GDX".
- They may include spaces, but not numerals or any punctuation. There are some rare situations in which numbers can cause technical problems.

## Font filenames

An individual font file is typically no different from other files in an operating system, and is (for the most part) only bound by the limitations on legal names in that operating system. **However there is a pattern of font file naming that has become reasonably common, and that we recommend:**

> _FontFamilyName_-_StyleName_.otf

Here the spaces are removed in the family and style names. The Bold Italic weight of "Source Sans Pro" would be named:

> SourceSansPro-BoldItalic.otf

## Font families

Some applications and operating systems can handle complex font families with many weights, however many still do not, and trying to coordinate a well-functioning family across multiple platforms is a technical nightmare. **Best practice is that font families should normally be grouped in sets of four that correspond to Regular, Italic, Bold, and Bold Italic weights. If a design has more than four weights/styles, it is best to split them into separate groups of two or four and change the main font name for each group.**

For example, say the "Anaconda Pro" font family has four upright weights (Light, Regular, Semibold, Bold) and four corresponding italic faces. The most trouble-free way to deliver these would be as two separate font families, Anaconda Pro Light:

- Anaconda Pro Light - Regular  _(designed as Anaconda Pro - Light)_
- Anaconda Pro Light - Italic  _(designed as Anaconda Pro - Light Italic)_
- Anaconda Pro Light - Bold  _(designed as Anaconda Pro - Semibold)_
- Anaconda Pro Light - Bold Italic  _(designed as Anaconda Pro - Semibold Italic)_

and Anaconda Pro:

- Anaconda Pro - Regular  _(designed as Anaconda Pro - Regular)_
- Anaconda Pro - Italic  _(designed as Anaconda Pro - Italic)_
- Anaconda Pro - Bold  _(designed as Anaconda Pro - Bold)_
- Anaconda Pro - Bold Italic  _(designed as Anaconda Pro - Bold Italic)_

## References

[ScriptSource blog post regarding font naming recommendations]

[Ethnologue]: http://www.ethnologue.com/
[ScriptSource blog post regarding font naming recommendations]: http://scriptsource.org/cms/scripts/page.php?item_id=entry_detail&uid=k7dwx5fhnz
