---
published: false
layout: bookpage
weight: 430
category: OpenType
title: OpenType
---
On [ScriptSource][OTinfo on SS] there is information on where to find copies of the OpenType specification.

## Lookup Orders

## Language Tags

## Feature Tags

The OpenType specification provides for Layout Feature tables, each of which is identified by a 4-character tag.

## Stylistic Sets and Character Variants

Tags for Layout Feature tables which are in the range "ss01" to "ss20" are registered as Stylistic Set 1 through 20. Tags in the range "cv01" to "cv99" are registered as Character Variant 1 through 99.

When should one use [Stylistic Sets] and when should one use [Character Variants]?

According to the OT spec, Character Variants (cvxx tags) should be preferred when only a few similar characters are affected, for example, all characters based on the ‘a’ form, while Stylist Sets (ssxx tags) are preferred when systematically related changes affect a number of characters. Having said that, there are some technical and practical distinctions that may require violating these guidelines:

- The cvxx tags utilize GSUB “alternate” (type 3) lookups thus allowing a feature to have more than on/off values.
- There are only 20 registered ssxx features, but 99 cvxx features.
- Some apps (MS Word for example) assume that users would need to turn on only one ssxx feature at a time.
- Not as many apps support cvxx [yet].

[OTinfo on SS][http://scriptsource.org/cms/scripts/page.php?item_id=entry_detail&uid=kr5s6gwpdy]

[Stylistic Sets][http://www.microsoft.com/typography/otspec/features_pt.htm#ssxx]

[Character Variants][http://www.microsoft.com/typography/otspec/features_ae.htm#cv01-cv99]
