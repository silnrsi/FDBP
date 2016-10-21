---
published: true
layout: bookpage
weight: 348
outlevel: 5.4.8
category: Composite Glyphs
title: Composite Tools
---

This subsection describes one tool for creating composite glyphs.

# Composite building tool

There is a python script named ```UFObuildComp.py``` found in ```pysilfont```. It accepts a list of composite definitions and constructs a composite glyph for each definition line. For example,

```python UFObuildComp.py -i composites.txt -r V CharisSIL-Regular.ufo ```

* reads composite definitions from the input (```-i```) file named ```composites.txt```
* uses "verbose" (```-r V```) option for recording progress in the log file
* adds composite glyphs to the CharisSIL-Regular font
* writes results to a log file CharisSIL-Regular.log (default name based on font name)

# Basic syntax of input file

The format used for composite definitions is a subset of that used by RoboFont. It allows:

```
# everything after # is a comment
result = base1 & base2         # two bases
result = base + diacritic@AP   # base plus diacritic (at attachment point)
result = base + diac1@AP + diac2@AP # diac2 attaches to diac1
result = base + diac1@AP +diac2@base:AP # diac2 attaches to base
result = base + diac@AP | USV  # USV is 4 to 6 hex digits
result = base + diac@AP ^50,100 # add 50 to left and 100 to right sidebearings
```

Example (1):

```LtnCapDSmZCaron = LtnCapD & LtnSmZ + CombCaron@U |01C5```

defines the glyph ```LtnCapDSmZCaron``` (Latin capital letter D with small letter z with caron) as being composed of the glyph ```LtnCapD``` (Latin capital letter D) followed by the glyph ```LtnSmZ``` (Latin small letter z) with the glyph ```CombCaron``` (Combining caron) placed over the ```LtnSmZ``` glyph at the attachment point (or anchor) labeled ```U``` (which, by default, is matched to the attachment point ```_U``` on the attaching glyph). The resulting glyph is assigned the Unicode value U+01C5.

Example (2):

```LtnSmECircumDotBlw = LtnSmE + CombDotBlw@L + CombCircum@LtnSmE:U |1EC7```

defines the glyph ```LtnSmECircumDotBlw``` (Latin small letter e with circumflex and dot below) as being composed of the glyph ```LtnSmE``` (Latin small letter e) with the glyph ```CombDotBlw``` (Combining dot below) placed below the ```LtnSmE``` glyph at attachment point ```L``` (matched to attachment point ```_L``` on the attaching glyph) as well as the glyph ```CombCircum``` (Combining circumflex) placed above the ```LtnSmE``` glyph at attachment point ```U```. The ```LtnSmE:``` after the ```@``` is needed to override the default of attaching a diacritic to the immediately preceding glyph. The resulting glyph is assigned the Unicode value U+1EC7.

Example (3):

```LtnCapACircumGrave = LtnCapA + CombCircum@U + CombGrave@U |1EA6```

```LtnCapACircumGrave.VN = LtnCapA + CombCircumGrave.VN@U```

The first line defines the glyph ```LtnCapACircumGrave``` (Latin capital letter A with circumflex and grave) as being composed of the glyph ```LtnCapA``` (Latin capital letter A) with the glyph ```CombCircum``` (Combining circumflex) placed over the ```LtnCapA``` glyph at attachment point ```U``` and with the glyph ```CombGrave``` (Combining grave) placed over the preceding glyph ```CombCircum``` (since the default action is to attach to the immediately preceding glyph) and using the attachment point of that glyph. So, in addition to having an attachment point ```_U``` which is used to attach to the base glyph, the Combining circumflex also has a ```U``` attachment point to which the Combining grave glyph attaches. The resulting glyph is assigned the Unicode value U+1EA6.

The second line in the above example defines another composite glyph for this same Unicode character to be used when the Vietnamese writing system is active, since in Vietnamese these diacritics appear next to each other rather than one atop the other.

# Extension to basic syntax

SIL added an extension to the RoboFont syntax in order to allow additional properties to be added with minimal conflict with the original syntax. The list of properties is enclosed in square brackets, entries are separated by semicolons and each entry consists of a property name, an equals sign and a value.

```[prop1=value1;prop2=value2] ```

If applied to a glyph that is being used to build the composite glyph, then the property list appears after the glyph to which it applies.
If applied to the resulting composite glyph, the property list must follow a vertical bar and the USV (if it is present).

Example (4):

```InvisibleTimes.ShowInv = BoxDotted + LtnCapX.Sophia@C11 [with=_C]```

defines a glyph composed of the ```BoxDotted``` glyph (a box made with a dotted line) with a glyph containing a sans-serif "X". The attachment point on the dotted box is ```C11```, so by default the corresponding attachment point on the ```LtnCapX.Sophia``` glyph would be ```_C11```. Using ```[with=_C]``` overrides that with the ```_C``` attachment point.
