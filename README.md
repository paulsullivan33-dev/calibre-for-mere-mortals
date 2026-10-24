# Calibre for Mere Mortals

Sooner or later, anyone who reads ebooks
ends up with the same quiet mess: books
scattered across a downloads folder, a
phone, a tablet and an e-reader, in
formats half the devices can't open, with
titles like `final_v2_REAL.epub` and no
memory of what half of them are.
**Calibre** is the open-source answer
built for exactly that: one library on
one computer, where every book is
catalogued once, converted to whatever
format each device wants, and served to
the rest of the house. This guide explains
how it works, how to install it, and how
to run a library without fooling yourself
about the parts that matter: the library
folder is the database's territory, not
yours, and a conversion is a re-typeset,
not a photocopy.

The lab behind this guide ran the real
thing: **calibre 9.17.0**, the project's
current release on build day, installed on
a headless Ubuntu 24.04 machine and driven
entirely from the command line — this
guide's lab had no screen, which turns out
to be a fair way to learn where calibre's
centre of gravity really sits. Into a
fresh library went two public-domain
books from Project Gutenberg — *Alice's
Adventures in Wonderland* and
*Frankenstein* — and the system was
exercised end to end: the books added and
listed, their metadata inspected and
edited, one searched for three ways,
Alice converted to MOBI and to a 93-page
PDF, the converted file added back as a
second format, the whole library exported,
its structure checked, and the content
server run and queried over HTTP. What
the lab could not do, it did not fake:
the graphical interface never ran (there
was no display), so the GUI is taught
from the project's own manual, and
calibre's online metadata lookup could
not be reached from the lab's network at
all — chapter 5 and `criteria.md` say
exactly why, and keep the ledger of what
was run and what was only read.

## What this guide covers

- [**What Calibre is**](what-calibre-is.md) —
  the mental model: a librarian, a
  converter and a server in one program;
  what it is not (a bookshop, a reading
  app first, a cloud)
- [**The moving parts**](the-moving-parts.md) —
  the library folder and its database, the
  command-line tools, the viewer and
  editor, and the content server: what
  each holds, and the one rule that keeps
  a library healthy
- [**Installing Calibre**](installing-calibre.md) —
  the official routes on Windows, Mac and
  Linux, the headless install the lab
  performed, and its declared deviations,
  told in full
- [**Adding Books**](adding-books.md) —
  adding from the command line and the
  GUI, where the files land, duplicates,
  and why you never tidy the library
  folder by hand
- [**Metadata**](metadata.md) — titles,
  authors, tags, covers and ratings: what
  a book arrives with, how to fix it, and
  the star-rating trap the lab measured
- [**Converting Between Formats**](converting-formats.md) —
  how `ebook-convert` works, EPUB to MOBI
  and PDF for real, and what conversion
  can and cannot rescue
- [**Searching and Organising**](searching-and-organising.md) —
  the search language, tags and series,
  saved searches and virtual libraries
- [**Reading and Devices**](reading-and-devices.md) —
  the built-in viewer, sending books to an
  e-reader, and which format each device
  actually wants
- [**The Content Server**](the-content-server.md) —
  your library in a browser and in reader
  apps over OPDS, run for real in the lab,
  with the password warning that matters
- [**Backup and Moving a Library**](backup-and-moving.md) —
  the folder copy that is a complete
  backup, the export, the per-book safety
  net files, and checking a library's
  structure
- [**Recipes**](recipes.md) — a
  public-domain classics shelf, a family
  library on a home server, and a scripted
  intake for a folder of mixed files
- [**The Neighbours**](the-neighbours.md) —
  the Kindle and Kobo shops, Apple Books,
  calibre-web, Kavita and friends: what
  each one trades
- [**Limits**](limits.md) — the DRM wall,
  one writer at a time, conversion quality,
  and the other ceilings, stated plainly
- [**Troubleshooting**](troubleshooting.md) —
  the PDF conversion that refuses to run
  as root, the rating that is not the
  number you typed, the "empty" library
  that is a wrong path, and the other
  traps this guide's lab fell into so you
  don't have to
- [**Glossary**](glossary.md) — the terms,
  collected in one place

## What it doesn't cover

Removing DRM from books you bought — it
is the one job readers most often expect
calibre to do, it cannot do it out of the
box, and chapter 13 explains the wall
plainly rather than pointing at the
grey-market tools around it. Writing and
typesetting your own ebook from scratch
is pointed at (calibre's editor exists;
a full tutorial is another guide), and
running a public bookshop for strangers
is out of scope: the content server
chapter is about your household, behind
your passwords.

## How to use this guide

Read chapter 1 for the model and chapter
2 before adding a single book — knowing
which part holds what, and why the
library folder is hands-off, prevents the
one mistake that actually damages
libraries. Chapter 3 gets calibre
installed; chapter 4 starts the library.
If your real interest is a Kindle full of
books it can't open, chapters 6 and 8 are
the pair you want. Chapter 10 is not the
optional ending: take your first backup
while the library is two books and a
restore rehearsal costs minutes. The
lab's transcripts live in
`calibre-lab/transcripts/`; its notes are
`examples/lab-notes.txt`.
