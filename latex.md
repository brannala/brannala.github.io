---
inmenu: 0
layout: page
title: LaTeX
permalink: /latex/
---

**Managing papers and bibliography databases at the command line**

My approach to managing papers and references is to have single folder
containing all my pdf reprints and a BibTeX format bibliography database file. I use
a python script called [papers](https://github.com/perrette/papers) to
manage my database and create BibTeX entries with cross referencing to the pdf files. The
papers program can extract the doi information from a pdf file, gather
information online to create a BibTeX entry and store a renamed copy
of the associated pdf in a folder; the new file name and location is
included as a 'file' field of the new bibtex item added to  the
database file. Papers can even do this recursively
for a folder full of pdf reprints. Very cool. Installation is
easy. First clone the git project:
```
git clone https://github.com/perrette/papers.git
```
then use the pip python installer to install python dependencies
```
pip install unidecode crossrefapi bibtexparser scholarly fuzzywuzzy six
```
and install the poppler pdf rendering library. On mac OSX this is done
using brew
```
brew install poppler
```
Then run the python installer in the cloned papers project directory
```
python setup.py install
```
To test whether the program is installed successfully type
```
papers -h
```
which should produce the output
```
Bruces-MBP-2:~ bruce$ papers -h
usage: papers [-h]
              {status,install,add,check,filecheck,list,doi,fetch,extract,undo,git}
              ...

library management tool

positional arguments:
  {status,install,add,check,filecheck,list,doi,fetch,extract,undo,git}

optional arguments:
  -h, --help            show this help message and exit

```

**Using ebib to manage citations within emacs**

I wanted a reference manager that I could use to embed citations in
org projects that would link out to the bibtex entry, a pdf reprint,
etc. Of course, I needed to embed citation in latex documents as
well. The emacs ebib-mode does all this and more. Install ebib mode from
the melpa archive using `list-packages` for example. The only hitch
was that some hooks for org were not installed properly. I found the
lisp file `org-ebib.el` at the authors github site and installed it manually. 

```
;; added directory for org-ebib.el loading
(add-to-list 'load-path "~/.emacs.d/lisp/")
(load "org-ebib")
```
Everything now worked. I set some options using `M-x customize-group
ebib` including the directory for my bib database. Also set it up to
open my main bibliography file by default when ebib is started. The next issue was
to get ebib to automatically open my local pdfs of entries that had
been archived using the papers script. By default ebib looks for a
file entry to specify the location of a reprint file. The problem is
that papers adds ':' at the start of the file path and appends ':pdf'
on the end. This confused ebib. The solution was to again use
customize to remove `file` as the default field for a file search and
leave the field blank which triggers a search in a default directory
using the bibtex entry key (+ .pdf). That is fine as papers also names the pdfs
it creates using the bibtex key. The next problem was that papers
automatically creates subfolders for years when organizing the
reprints but ebib does not search subdirectories so each directory has
to be explicitly specified. Ugh, no way I was going to do
that. Instead, I created a subfolder in my home directory and wrote a
bash script to create hard links to all the pdf reprints in that
single folder which then becomes the search target for ebib. The bash
script is
```
#!/bin/bash
rm -Rf ~/allreprints/*
for dir in $(ls -1FA | grep / | tr -d /); do ln $dir/* ~/allreprints; done
```
and is run after I add new entries to my database using papers. Works
like a charm so far. Ebib has some promising features like linking an
org note to an entry and creating reading lists (as org files). Also
nice search tools using regex are available in the main window.

**Preparing exams in latex**
I recently discovered a great package called ''exam'' that is part of the standard packages in texlive.
The package has commands for adding multiple choice questions and so on, and automatically tracks
the total points.

**Pedigrees in latex**
I often include pedigree questions on exams for my EVE 131 course (requiring calculation of kinship coefficients etc). Another exciting discovery I made recently was that a good latex package exists for drawing pedigrees. Just include the following packages ```\usepackage{pst-pdgr,pstricks,pst-pdf}``` and compile the file using xelatex. Information on the pst-pdgr package is [here](https://ctan.org/pkg/pst-pdgr?lang=en).
