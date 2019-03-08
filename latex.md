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
