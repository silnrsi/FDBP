---
published: true
layout: bookpage
weight: 348
category: Composite Glyphs
title: Composite Tools
---

This subsection describes tools for creating composite glyphs.

One tool is the python script UFObuildComp.py found in pysilfont. It accepts a list of composite definitions and constructs a composite glyph for each definition line. For example,

```python UFObuildComp.py -i composites.txt -r V CharisSIL-Regular.ufo ```

* reads the file ```composites.txt```
* adds composite glyphs to the CharisSIL-Regular font
* writes results to a log file CharisSIL-Regular.log (default name based on font name)
* uses "verbose" (-r V) option for recording the log file

The format of the composite definition is:

```# everything after # is a comment
result = base1 & base2         # two bases
result = base + diacritic@AP   # base plus diacritic (at attachment point)
result = base + diac1@AP + diac2@AP # diac2 attaches to diac1
result = base + diac1@AP +diac2@base:AP # diac2 attaches to base
result = base + diac@AP | USV  # USV is 4 to 6 hex digits
result = base + diac@AP ^50,100 # add 50 to left and 100 to right sidebearings```

An SIL extension to the syntax allows properties to be listed as

```[prop1=value1;prop2=value2]```

If applied to a glyph, the property list appears after the glyph.
If applied to the result, the property list must follow a vertical bar and the USV (if it is present).
