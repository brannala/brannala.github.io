---
inmenu: 1
layout: page
title: Things
permalink: /things/
---
## Core Tools

**LaTeX**

[LaTeX](https://www.latex-project.org/) is a program (derived from Don Knuth’s TeX program) that is ideal for
writing manuscripts that use a lot of equations. I wrote my PhD in
LaTeX and so have most of my graduate students. A LaTeX cheat sheet
(list of symbols, etc) can be found
[here](https://wch.github.io/latexsheet/latexsheet.pdf). 

[LaTeX stuff](/latex/): provides a description of the
programs that I use for managing pdf reprints, BibTeX databases and
other activities related to writing manuscripts in LaTeX.

**Emacs**

[GNU Emacs](https://www.gnu.org/software/emacs/) is "an extensible, customizable, free/libre text editor —
and more." An Emacs cheat sheet can be found [here](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf).

[Emacs stuff](/emacs/): provides a description of my emacs configuration and
packages that I have found useful.

[Sequed](https://github.com/brannala/sequed) is an emacs package I wrote for viewing alignments and manipulating DNA sequence
data in fasta format.

**Proggy fonts**

These are my favorite terminal fonts. Available
[here](https://github.com/bluescan/proggyfonts).

## Programming Tools
**Lex and Yacc**

Lex and yacc (now flex and bison) can be used to write a lexer and
parser for such things as configuration files, trees in newick format,
and so on. A basic tutorial is available
[here](http://ds9a.nl/lex-yacc/cvs/output/lexyacc.html#toc2.1 "Lex and
YACC primer"). There are also detailed manuals for
[flex](ftp://ftp.gnu.org/old-gnu/Manuals/flex-2.5.4/html_mono/flex.html
"flex manual") and
[bison](http://www.gnu.org/s/bison/manual/bison.html "bison manual").

**Javascript Resources**

***React stuff*** React is an open source project that has developed a
pretty nice language extension to Javascript. The basic idea is to
have components that include both logic and presentation (rather than
having logic in a javascript file, presentation in an html file, and
styles in a css file). A simplified language for writing React called
JSX can be used to write the code which is then transpiled into
javascript using [Babel](https://babeljs.io/). Straight javascript and
JSX can be mixed together in a source file as needed. Pretty cool.
React can also use a component based approach to styling that is
described in detail at
[styled-components.com](https://www.styled-components.com/). I have
been experimenting with React and will collect some useful sites
together here eventually.

**Autotools**

This is a suite of gnu tools for creating portable source code
distributions. A great tutorial can be found [here](
http://fsmsh.com/2753 "Autotools tutorial"). The definitive “goat”
book on autotools and libtools can be found online
[here](http://sourceware.org/autobook/autobook/autobook.html#SEC_Top
""Goat" book").

**getopt**

This is a gnu standard library that is incredibly useful for parsing
command line options. It is best used with the gcc/c++ compiler. A
brief description is found
[here](https://www.gnu.org/software/libc/manual/html_node/Getopt.html#Getopt
"getopt").

**Git**

Git (git) is a great tool for maintaining prior versions of your
source code (or manuscripts) in an organized hierarchy. A free book on
git is [here](https://git-scm.com/book/en/v2). A quick reference is
[here](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf). Open
source projects can be hosted for free on
[github](https://github.com/) and private repositories for academic
research (with some limitations) can be hosted on
[bitbucket](https://bitbucket.org/). I use both. Projects on github
can have web pages (gitpages) hosted as well. This website is hosted
on github


## Bioinformatics
**NGS data file formats**

The FASTQ format appears to be emerging as a standard for
next-generation sequencing data (particularly Illumina GAII
reads). The Wikipedia description of the format is
[here](http://en.wikipedia.org/wiki/FASTQ_format "FASTQ").

**NCI wiki**

This
[wiki](https://wiki.nci.nih.gov/display/TCGA/TCGA+barcode#TCGAbarcode-types
"NCI barcodes") explains barcoding scheme and other features of cancer
genome databases such as [GCAT](http://cancergenome.nih.gov/ "Cancer
Genome Atlas").
