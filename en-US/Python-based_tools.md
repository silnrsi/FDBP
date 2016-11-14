---
published: true
layout: bookpage
weight: 950
outlevel: 11.5
category: Tools
title: Python-based Tools
---

In addition to the various font editors already listed, it is often useful to use scripts to modify fonts, either changing source files (eg UFO) or the actual fonts (eg .ttf).

This could apply during the design process (for example, automatically creating composite glyphs) or during the build process (for example, automatically updating glyph names from design names to production names).

Python has become the de facto standard for such scripting, and there are several python-based collections of fonts tools available. These include both pre-written scripts to perform specific tasks as well as python libraries which can be used when writing new scripts or when modifying existing scripts to meet specific needs.

Those available include:

[Fonttools](https://github.com/behdad/fonttools) - a library for manipulating fonts, written in Python. See the section below for more information.

[Pysilfont](https://github.com/silnrsi/pysilfont) - a growing collection of tools for font development and building. See the section below for more information.

[Robofab](https://github.com/robofab-developers/robofab) - a Python library with objects that deal with data usually associated with fonts and type design. RoboFab supports the UFO font format and also FontLab.

[Fontforge](https://fontforge.github.io/en-US) - as well as being a font editor, FontForge comes with a python object library that can work with FontForge’s own format (.sfd), as well as with UFOs and ttf files.

All of the above are open-source projects.

Many font editors also support python scripting within their GUI.

## Fonttools

Fonttools - a library for manipulating fonts, written in Python. The project includes the TTX tool, which can convert TrueType and OpenType fonts to and from an XML text format (also called TTX). It supports TrueType, OpenType, AFM and, to an extent, Type 1 and some Mac-specific formats.

(More details to be added)

## Pysilfont

This a growing collection of tools, initially  written by members of SIL International’s Non-Roman Script Initiative team, with a broader set of contributors welcome.
Included are a UFO object library, support for testing fonts and scripts for specific tasks.
These tools are designed with a UFO-based workflow in mind, though many would also be useful in other workflows.

Most scripts are written to use a standard framework (which is included in the libraries). This framework provides for help text, parameter handling, file opening and error reporting, thereby simplifying script writing and giving users a standard interface.

### UFO support in Pysilfont
With some limitations, all UFO scripts in Pysilfont should work with UFO2 or UFO3 source files - and can convert from one format to the other.

In addition all scripts will output in a normalized form, designed to work with source control systems.  Most aspects of the normalization can be set by parameters, so projects are not forced to use Pysilfont’s default normalization.

The simplest script is UFOconvert, which will convert between UFO 2 and UFO3 (if -v is used to specify the alternative version) or otherwise simply normalize the UFO by ‘converting’ to the existing version.  Note that this same functionality is in most other scripts, so UFOconvert is normally only needed after fonts have been processed by external font tools.

The following are known limitations that are due to be addressed in the future:

* UFO 3 specific folders (data and images) are not copied
* Converting from UFO 3 to UFO 2 only handles data that has a place in UFO 2, but does include converting UFO 3 anchors to the standard way of handling them in UFO 2

There is further [documentation in github](https://github.com/silnrsi/pysilfont/blob/master/PysilfontUserDocs.pdf), although this is in need of updating and extending.
