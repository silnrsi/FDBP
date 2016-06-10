# FDBP
Font Development Best Practice documentation

General Info
- Each page is written in GitHub Flavored Markdown (GFM) and begins with Jekyll front matter which specifies the title, category, weight (page sort order), published status, and layout (page template - bookpage is currently used by all pages).
- The GFM pages are in the en-US folder.
- The current pages are all placeholders which need to be filled out.

## Contributing

To contribute, edit the GitHub Flavored Markdown pages in the en-US folder.
This can be done several ways:
- Clone the repo, then edit the files with a text editor and push them. (See [Previewing your changes locally] (https://github.com/silnrsi/FDBP#previewing-your-changes-locally) for previewing the site or consider a markdown editor such as [Geany] for previewing content)
- Use the GitHub web editor.
- Use [prose.io/#silnrsi/FDBP](http://prose.io/#silnrsi/FDBP), which provides a GUI-like interface for GFM.
You will need to use the prose.io interface to add that service as an authorized app on your GitHub account.

A page can be added by adding a file to the en-US directory.
- Do not use spaces in the file name.
- Copy the front matter (between the triple hyphens) from another file and update the
weight, title, and possibly category.
- New pages will generally use a category that’s already in use.
- Add the page title and weight to en-US-weightlist.md.

If you contribute, add your name to AUTHORS.txt. The structure Victor indicated can be found
at the bottom of this Google [Doc](https://docs.google.com/document/d/1F0K-oYRw6ZqHvM1TT2k0_CkQuv-pJqvRQgQXNUb02IA/edit#heading=h.zhldii2y6sjb). New pages probably aren’t needed for topics below the top level -- at least not until a placeholder page gets too full.

## Previewing your changes locally
To see your working copy of the site served locally in your browser, start a command window, change to the directory containing the repository (using the `cd` command) and start the jekyll server. For example:
```
cd /home/hyde/FDBP
jekyll serve
```
then point your browser at the URL which jekyll prints out (something like http://127.0.0.1:4000/FDBP/, for example).
You may be able to substitute 'localhost' for '127.0.0.1' in the URL.

This assumes you have jekyll installed already.

### Installing jekyll

**Windows:** This guide explains how to [Easily install Jekyll on Windows]  
**Linux:** Install the jekyll package using your package manager, for example on Debian based operating systems

`sudo apt-get install jekyll`

Ensure that you have jekyll version 2 or later.

## Acknowledgements
We gratefully acknowledge this site is modeled on [Design With FontForge] on [GitHub].

[Design With FontForge]: http://designwithfontforge.com
[GitHub]: https://github.com/fontforge/designwithfontforge.com
[Easily install Jekyll on Windows]: https://davidburela.wordpress.com/2015/11/28/easily-install-jekyll-on-windows-with-3-command-prompt-entries-and-chocolatey/
[Geany]: https://www.geany.org/
