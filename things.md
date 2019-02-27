---
inmenu: 1
layout: page
title: Things
permalink: /things/
---
## Programming
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

## Typesetting

**LaTeX**

This program (derived from Don Knuth’s TeX program) is ideal for
writing manuscripts that use a lot of equations. I wrote my PhD in
LaTeX and so have most of my graduate students. A tutorial, list of
symbols, etc, can be found
[here](http://www.artofproblemsolving.com/Wiki/index.php/LaTeX:Basics
"LaTeX").

## Emacs

**Configuration**

Emacs is all about configuration and configuration is all about
lisp. I try to keep configurations to a minimum and avoid putting things into
.emacs.d/init.el that I don't fully understand. 
[Learning emacs lisp](http://emacslife.com/emacs-lisp-tutorial.html) provides a
unified tutorial on lisp programming with an emphasis on emacs configuration
that is also available as an org file. 

**Org mode**
A really useful package for creating project notebooks with
checklists, timestamps, executable code and so on. [What is Org mode
about?](https://mickael.kerjean.me/2017/03/20/emacs-tutorial-series-episode-2/)
provides an org mode tutorial that you can follow using the org file 
[org-mode-tutorial.org](http://mickael.kerjean.me/assets/files/org-mode-tutorial.org)

**Gnus mail**
Reading gmail in emacs is a bit complicated. I thought about
Wanderlust but was disuaded by the lack of documentation. Finally
settled on the mu/[mu4e](http://www.djcbsoftware.nl/code/mu/mu4e/) and
[offlineimap](http://www.offlineimap.org/) combination.
[Emacs as email client with offlineimap and
mu4e](https://medium.com/@kirang89/emacs-as-email-client-with-offlineimap-and-mu4e-on-os-x-3ba55adc78b6)
provides a good tutorial on how to set these up in OS X. I provide a
quick summary here of what worked for me. First, install offlineimap
using brew
```
brew install offlineimap
```
Then create the configuration file `~/.offlineimaprc` with contents
```
[general]
ui=TTYUI
accounts = Gmail
autorefresh = 5

[Account Gmail]
localrepository = Gmail-Local
remoterepository = Gmail-Remote

[Repository Gmail-Local]
type = Maildir
localfolders = ~/.Mail/me@gmail.com

[Repository Gmail-Remote]
type = Gmail
remotehost = imap.gmail.com
remoteuser = me@gmail.com
remotepass = <password>
realdelete = no
ssl = yes
sslcacertfile = /usr/local/etc/openssl/cert.pem
maxconnections = 1
folderfilter = lambda folder: folder not in ['[Gmail]/Trash',
'[Gmail]/Spam',
'[Gmail]/All Mail',
'[Gmail]/Important',
'[Gmail]/Starred',
'Archive',
'Notes',
]
```
I filtered out most of the mailboxes as I only wanted to download
INBOX and Sent and Draft mail. Then type
```
offlineimap
```
and the mail will be downloaded. The mu/mu4e programs are then
installed
```
brew install mu
```
and the following command is run to index the mail files
```
mu index --maildir=~/.Mail
```
The init.el file is then edited to incorporate some mu4e
configurations
```
;; Settings for mu4e mail client
(require 'mu4e)
(setq mail-user-agent 'mu4e-user-agent)
(setq mu4e-maildir "~/.Mail")

(setq mu4e-drafts-folder "/me@gmail.com/[Gmail].Drafts")
(setq mu4e-sent-folder   "/me@gmail.com/[Gmail].Sent Mail")

;; don't save message to Sent Messages, Gmail/IMAP takes care of this
(setq mu4e-sent-messages-behavior 'delete)
;; allow for updating mail using 'U' in the main view:
(setq mu4e-get-mail-command "offlineimap")

;; shortcuts
(setq mu4e-maildir-shortcuts
    '( ("/me@gmail.com/INBOX"               . ?i)
       ("/me@gmail.com/[Gmail].Drafts"   . ?d)
       ("/me@gmail.com/[Gmail].Sent Mail"   . ?s)))

;; something about ourselves
(setq
   user-mail-address "lk@pepperspray.org"
   user-full-name  "Full Name"
   mu4e-compose-signature
   (concat
    "Me\n"
    "Organization\n"))

```
Mail will be sent using smtpmail so that is configured in init.el as
well
```
;; configuration for sending mail
(setq message-send-mail-function 'smtpmail-send-it
     smtpmail-stream-type 'starttls
     smtpmail-default-smtp-server "smtp.gmail.com"
     smtpmail-smtp-server "smtp.gmail.com"
     smtpmail-smtp-service 587)
```
If it is not already installed gnutls should be installed
```
brew gnutls
```
Finally, create an `~/.authinfo` file with the following contents:
```
machine smtp.gmail.com login <gmail username> password <gmail password>
```
and encrypt the above file by running:
```
gpg --output ~/.authinfo.gpg --symmetric ~/.authinfo
```
All done. Now in emacs type `M-x mu4e` to start using mu4e for email.

**Getting that ugly DOS ^M newline character out of your text files**

I collaborate with quite a few people who use Windows and seem to be
unaware that their Windows text editor is littering our shared text
files with ^M DOS style carriage returns. Here is a useful emacs
command to strip all the ^M characters out replacing them with a unix newline:
```
M-x replace-string RET C-q C-m RET C-q C-j RET
```

**Proggy fonts**

These are my favorite terminal fonts. Available
[here](https://github.com/bluescan/proggyfonts).



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
