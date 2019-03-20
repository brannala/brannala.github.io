---
inmenu: 0
layout: page
title: Emacs
permalink: /emacs/
---


**Configuration**

Emacs is all about configuration and configuration is all about
lisp. I try to keep configurations to a minimum and avoid putting things into
.emacs.d/init.el that I don't fully understand. 
[Learning emacs lisp](http://emacslife.com/emacs-lisp-tutorial.html) provides a
unified tutorial on lisp programming with an emphasis on emacs configuration
that is also available as an org file. 

**Setting up emacs for coding in React JSX and javascript**

I wanted to set up syntax highlighting, automated indenting and syntax
error checking (linting) etc when editing
javascript containing JSX (React) extensions. [Emacs-flycheck-eslint](http://codewinds.com/blog/2015-04-02-emacs-flycheck-eslint-jsx.html)
covers this but is a bit out of date. I used that page as a rough
guide and came up with the installation procedure that follows. I started by installing eslint
and plug-ins with npm
```
sudo npm install -g eslint babel-eslint eslint-plugin-react
```
and created a file `~/.eslintrc` with contents
```
{
  "parser": "babel-eslint",
  "plugins": [ "react" ],
  "env": {
    "browser": true,
    "es6": true,
    "node": true
  },
  "ecmaFeatures": {
    "arrowFunctions": true,
    "blockBindings": true,
    "classes": true,
    "defaultParams": true,
    "destructuring": true,
    "forOf": true,
    "generators": true,
    "modules": true,
    "spread": true,
    "templateStrings": true,
    "jsx": true
  },
  "rules": {
    "consistent-return": [0],
    "key-spacing": [0],
    "quotes": [0],
    "new-cap": [0],
    "no-multi-spaces": [0],
    "no-shadow": [0],
    "no-unused-vars": [1],
    "no-use-before-define": [2, "nofunc"],
    "react/jsx-no-undef": 1,
    "react/jsx-uses-react": 1,
    "react/jsx-uses-vars": 1
  }
}
```
I then installed the `rjsx-mode` and `flymake` packages in emacs and added the following lines to
`~/.emacs.d/init.el`
```
;; setting for programming
(add-to-list 'auto-mode-alist '("\\.js\\'" . rjsx-mode)) ;; use react jsx extension mode for javascript files

;; http://www.flycheck.org/manual/latest/index.html
(require 'flycheck)

;; turn on flychecking globally
(add-hook 'after-init-hook #'global-flycheck-mode)

;; disable jshint since we prefer eslint checking
(setq-default flycheck-disabled-checkers
  (append flycheck-disabled-checkers
    '(javascript-jshint)))

;; use eslint with rjsx-mode for js files
(flycheck-add-mode 'javascript-eslint 'rjsx-mode)

;; customize flycheck temp file prefix
(setq-default flycheck-temp-prefix ".flycheck")

;; disable json-jsonlist checking for json files
(setq-default flycheck-disabled-checkers
  (append flycheck-disabled-checkers
    '(json-jsonlist)))
```
When editing a js file in rjsx-mode using `C-c ! <char>` executes a
flycheck command in the buffer. For example `C-c ! l` give a full list
of syntax errors in the buffer. The full list of commands are
available at [flycheck quickstart](https://www.flycheck.org/en/latest/user/quickstart.html).

**Org mode**
A really useful package for creating project notebooks with
checklists, timestamps, executable code and so on. [What is Org mode
about?](https://mickael.kerjean.me/2017/03/20/emacs-tutorial-series-episode-2/)
provides an org mode tutorial that you can follow using the org file 
[org-mode-tutorial.org](http://mickael.kerjean.me/assets/files/org-mode-tutorial.org)

***Embedding plantuml figures in org***
The [plantuml](http://plantuml.com/) software is a java library for displaying uml diagrams. The
diagrams can be rendered in an emacs buffer as well and
in a code block in an org document. The language specification is
[here](http://plantuml.com/guide). On a mac you use `brew`
to first install plantuml
```
brew install plant uml
```
then install the two emacs packages `plantuml-mode` and
`flycheck-plantuml` (syntax checking). Then edit `~/.emacs.d/init.el`
and add the following lines
```
(add-to-list
  'org-src-lang-modes '("plantuml" . plantuml))
(setq plantuml-jar-path "/usr/local/Cellar/plantuml/1.2019.3/libexec/plantuml.jar")
```
The adding a code block like 
```
#+BEGIN_SRC plantuml
@startuml
Alice -> Bob: test
@enduml
#+END_SRC
```
and typing `C-c '` in the block will render a diagram in an emacs buffer. Cool.

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
