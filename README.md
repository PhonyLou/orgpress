#+TITLE: Dockerized Org Blog Generator
#+DATE: <2015-02-05 Thu>

# TLDR
fork this repo and clone

#+BEGIN_SRC sh
./compile
#+END_SRC

# Prerequisite
 - [Docker](https://www.docker.com/get-started)

# Configuration

## variables in =config.el=

- =config-blog-title=: you blog title
- =config-base-url=: base url
- =config-home-link=: about link
- =config-date-format=: date format using [[https://www.gnu.org/software/emacs/manual/html_node/elisp/Time-Parsing.html][elisp time parsing format]]
- =config-entry-format=: template for each blog item
#+BEGIN_SRC emacs-lisp
(format-spec fmt
               `((?t . ,(org-publish-find-title file t))
                 (?d . ,(format-time-string org-publish-sitemap-date-format
                                            (org-publish-find-date file)))
                 (?D . ,(format-time-string "<%Y-%m-%d %a>" (org-publish-find-date file)))
                 (?a . ,(or (plist-get project-plist :author) user-full-name))
                 (?c . ,(org-blog-find-content-lines
                         file (or (plist-get project-plist
                                             :blog-content-lines) 5)))
                 (?l . ,(concat "file:" link))
                 (?L . ,(replace-regexp-in-string "\.org" "\.html" link))
                 (?p . ,(org-blog-find-description file t))))
#+END_SRC

## header and footer html template
- =html/preamble.html=: header
- =html/postamble.html=: footer
- =html/header.html=: custom content inside =<head/>=

# Live Demo
[[https://blog.oyanglul.us]]
