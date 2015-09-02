##Academic writing: Scrivener, Zotero, Pandoc, Marked 2

The following is a very robust and well tested setup for using Scrivener and Zotero, since it's something that took me a while to work out, and it might save people the hassle! This is a very detailed description of how to set it up, so don't be put off by the length. It should take no more than 15-20 minutes, less for someone familiar with the tools used. *There is another way of doing this documented [here](https://zotplus.github.io/better-bibtex/cayw.html), but I think that the method outlined below is less likely to break on updates and ultimately simpler.*

**0.** This setup assumes that you will write in [Pandoc flavoured markdown](http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown) - this is by far the best markdown for academic writing, mainly because of its excellent citation support. This is for OSX or Linux, but I'm sure somebody could contribute a windows version if so minded.

**0b.** I like to set up Scrivener to look more like a plain text editor, to remind me that I'm writing in plain text. It's also sensible to set up a compile preset. I have attached my own presets for people to use as they wish, but I've made no effort to check that they work on anybody else's computer (and they definitely won't work on Windows), so buyer beware!

[Pandoc Preset.plist](https://github.com/davepwsmith/academic-scrivener-howto/tree/master/Pandoc%20Preset.plist)
[Plain Text.prefs](https://github.com/davepwsmith/academic-scrivener-howto/tree/master/Plain%20Text.prefs)

**1.** Set up zotero with the [Better BibTex plugin](https://zotplus.github.io/better-bibtex/). This is a plugin which a) makes your bibtex keys saner; and b) can auto-export to a bibtex file every time you update the database. Export a collection or the whole database in 'Better Biblatex' style to somewhere sensible (e.g. `~/.zotero/YOUR_BIBLIOGRAPHY.bib`) and make sure you tick the 'Keep Updated' box. 

It also includes a Pandoc citation style so that you can quick cite directly from Zotero by dragging and dropping into Scrivener.

**2.** Install [Pandoc](http://pandoc.org/) and [download the appropriate csl file](http://citationstyles.org/) for your preferred style to somewhere sensible. Pandoc will check `~/.csl/` by default.

**3.** Write your work in (http://pandoc.org/README.html#pandocs-markdown]pandoc-flavoured markdown[/url]. For citations, you can either:
    a. Copy and paste from Zotero using quick cite and the pandoc citation style.
    b. Use my [zotpick-pandoc applet](https://github.com/davepwsmith/zotpick-applescript). For installation and usage instructions follow the link.
**4.a** (optional, OSX only) It's possible (quite easy) to set up the excellent  [Marked 2 app](http://marked2app.com) with pandoc as a processor (you can choose the processor in Marked's preferences). You need to put the path to your pandoc installation in the 'Path:' box  -- probably:

```bash
/usr/local/bin/pandoc[/code] and any arguments you need in the 'Args:' box -- probably [code]-r markdown -w html -s -S --normalize --bibliography ~/.pandoc/YOUR_BIBLIOGRAPHY.bib --csl ~/.csl/YOUR_CITATION_STYLE.csl
```

This, along with marked's ability to watch a scrivener file, gives you a live preview of your document. I have created a clear, academic-ish style for marked (called, unimaginatively, `Academia.css`) which you can download from the [Marked Custom Styles Repository](https://github.com/ttscoff/MarkedCustomStyles)

**4.** Export your scrivener document as plain text markdown (MYPROJECT.txt) –- i.e. not using any of the markdown conversion options etc. since we're already writing everything in markdown anyway (you can use my preset to do this if you can make it work) -– and use a pandoc command to convert it into a filetype of your choice, eg.

```
pandoc -s -S --normalize --bibliography ~/.pandoc/YOUR_BIBLIOGRAPHY.bib --csl ~/.csl/YOUR_CITATION_STYLE.csl -f markdown -t docx -o MYPROJECT.docx MYPROJECT.txt
```

This command would create a full document including any headers, footers or markup needed (`-s`), apply smart typography such as curly quotes (`-S`), conflate any consecutive formatting elements etc. to provide neater output (`--normalize`), use the bibliography (`--bibliography`) and citation style (`--csl`) specified, and convert from (`-f`) markdown to (`-t`) docx, with the output as a file (`-o`) called `MYPROJECT.docx`
 
It's worth noting that if you want to use pandoc's PDF output, you need to install LaTeX --- the [BasicTex package](http://mirror.ctan.org/systems/mac/mactex/mactex-basic.pkg) will do just fine. There are loads of options for pandoc output, which you can read about in the [extremely thorough documentation](http://pandoc.org/README.html).