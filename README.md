# Latex-imitatie

This repository contains a LaTeX template for dissertations suitable for Dutch universities. It was specifically designed for the University of Amsterdam, but it should be (more-or-less) compatible with most other Dutch universities.

See [HERE](main.pdf) for an example of what the thesis will look like.

This template is build on the excellent [`latex-mimosis`](https://github.com/Pseudomanifold/latex-mimosis) template. Under the hood, `latex-mimosis` uses [`KOMA-script`](https://ctan.org/pkg/koma-script) which is a *huge* package that provides alternatives to the standard classes (`book`, `article`, etc.) with many options.

# How to use

Download or clone this repository, paste in your text in each chapter, run LaTeX in the way you usually run it, and a nice thesis should come out!

However, this template is made for tinkering. I would strongly advise you to go through the explanation below and go through the settings files to set up everything to your liking, etc.

# What your thesis should look like (and when)
## Section to include
Although we typically think of a thesis only in its completed form as a printed booklet, there are actually 2 different versions. This is explained in the thesis regulations of your university, for the University of Amsterdam, you can find that [here](https://www.uva.nl/en/research/phd/documents-and-forms/documents-and-forms.html).

 1. A first 'reading' version of the thesis. This needs to be turned in with your PhD committee, several weeks before the planned date of your defence (at UvA, its 14 weeks, so a long time!). This version MUST contain all scientific content (so your chapters, bibliography, etc.). No one will ever see this version, except for your (co-)promotors and the committee. It is only digital. Apart from the scientific content, the reading version *must* contain the following:
    -  All figures, tables, etc.
    -  Table of contents.
    -  Acknowledgement of financial support of research.
    -  If the thesis consists of an article or articles in the name of several authors: a page with a complete reference list with a list of authors for each article and an explanation of the relative importance of the co-authors.
    -  A summary.
    -  A bibliography.
 2. A 'final' version. After the committee approves the 'reading' version of your thesis, you prepare this version. The scientific content of the final version is identical to the reading version (no changes! Even grammatical corrections are banned, only spelling errors can be fixed). Apart from the contents of the reading version of the thesis, the following are added:
    -  A nice cover. This is not actually relevant for the pdf you will generate.
    -  A title page, as given by the office of the beadle ('pedel') (this is mandatory).
    -  Colophon (a page with the ISBN, credits for the design of the cover, etc.).
    -  Layout changes.
    -  A summary in your own language, typically aimed at laymen (i.e., your parents).
    -  An acknowledgement section.

In this template you can just turn sections you don't need on and off, meaning that you can prepare the reading and final version of your thesis at the same time.

## Digital vs printed versions
Dutch PhD theses are always printed as a 17x24cm booklet. Since this is a weird size, it may be tempting to just submit your reading version to the committee in A4 size. This is a mistake! Figures and tables will shrink significantly when changing over to the smaller paper size of the final version, meaning you may not be able to read them in the final version of your thesis. Since you cannot change Figures after submitting the reading version, this means you are stuck with too small graphics.

However, you should also not send the reading version in exactly the same formatting as the final version: since the final version of your thesis will be a printed booklet, you need to adjust page margins and the like (this template can do this for you). This template makes it easy to switch between generating `pdf`s suitable for reading on a PC and `pdf`s suitable for the printing press.

# How this template works

## The setting files
First, go over the setting files:
### `mimosis.cls`
Contains the `mimosis` class. It does quite a few things, like loading certain packages and changing default settings here and there. It also sets up a font, so change that if you don't like the one currently setup. For more information, see the [`latex-mimosis`](https://github.com/Pseudomanifold/latex-mimosis) repository. In general it is better to not change this complicated file too much and use other setting files to get the desired results. However, don't be afraid to change things and break stuff if you feel like it, you can always return to the original state. 

### `packages.tex`
Load all packages. Note that quite a lot of packages are already loaded inside `mimosis`, so what you see here is not all the packages we use. For the packages' `mimosis` uses, open `mimosis.cls`, and look for `\RequirePackage` commands. I tried to keep the settings of the imported packages separated from the file, but that is not always possible. It should be pretty well documented what each package does. Add stuff from yourself if you want to.

### `bibliography.tex`
Handle how you want to show your bibliography. This can get surprisingly complicated, so this dedicated file will contain all settings. I put my personal preferences there, feel free to change what you want. This template uses `biblatex`, which is just a way of handling citations most standard latex installations will support.

### `mimosis-personal.tex`
Here you can change all settings of the document. A lot of things are set up by default, go over them and decide if you agree.

### `personalcommands.tex`
Small definitions, like `\com`, which just colours text red, good for making comments. Also used to set hyphenation: especially personal names in the bibliography will stick out into the margin sometimes, using these settings you can break the names and make things look better.

## Chapters
Each chapter gets their own folder, containing `chapterX.tex` and a dedicated `Figures` folder where you can put figures belonging to the chapter. Each `chapterX.tex` file starts with some commands which make sure the chapter starts on the right page (left or right in the booklet), then has room to include a quote (optional), and an abstract (not optional), before the actual chapter starts. Just look at the examples, replace with your own text.

There is also a folder called `preface`, which contains `.tex` files which are part of the preface: the official title and committee pages (received from the beadle), the colophon and anything else you want to put before the thesis *really* starts. I include a template for the pages the beadle gives you, where you can just replace your own name etc.

The `postface` folder similarly contains the texfiles related to the postface: acknowledgements, the list of publications, whatever else you want to put there.

## Colours
In this template, each chapter gets its own theme colour (setup in `mimosis-personal.tex`). In the first bit of `chapterX.tex` files, I set up things such that the colour is used for all highlighted text. You can use the command `\textcolor{\chapclr}{Your text here.}` to set any of your text to the current theme colour.

## Actually loading everything and outputting a document

The `main.tex` file is the main LaTeX file. Instead of putting text here directly, like you would in a 'regular' LaTeX document, this file is used to load settings and the individual chapters of your thesis. If you open up `main.tex`, you see it first loads the `mimosis` class. After that, it uses `\input` commands to load all settings and chapters. There are also some weird settings that change over the course of the booklet, hopefully the remainder of this readme make clear why.

# Boring details about page ordering and typography

This may explain some seemingly odd choices of commands

## Coverpages and titlepages
In printed books, it is normal to include a cover page before the 'real' titlepage, so we do that as well in the thesis! If you open your booklet, on the left side, you have the inside of your cover, on the right side the cover page, just containing a title and your name. On the next page, there is an empty page on the left, and on the right, the thesis *really* starts with the official tile page. To make this work you have to be careful that page numbering starts at the right place, this template currently does that correctly.

## Empty pages and where they live
By default, each chapter *always* starts on a right-hand page. This is pretty normal in printed books. If a previous page ends on a left-hand page, the chapter starts immediately next to that. We control this behaviour with `\KOMAoptions{open=right}`.

However, I don't like this title page on the right, with the previous chapter on the left: in my own thesis, I wanted to put a picture at the left-hand side, relevant to the chapter starting on the right. So, in this template at every chapter I insert `\cleardoubleevenemptypage` to skip to the first right-handed page before inserting the chapter heading, leading to the desired behaviour. This behaviour is explained in the KOMA-script docs, section 3.13.

Please note that changes in the `\cleardoubleevenemptypage` and `\KOMAoptions{open=right}` commands can have pretty weird effects that are not always easy to sort out, so be a bit careful if you want to change those things.

If you (like me) want to add a picture on the left empty page, which might be nice, insert before the beginning of the rest of the chapter the following:
```latex
\cleardoubleevenemptypage
\thispagestyle{empty}
\includegraphics[
  width=\textwidth,%
  height=\textheight,%
  keepaspectratio,%
]{picture}
\chapter{Chapter Heading}
```
And tada, a picture will show left, the chapter begins on the right.
