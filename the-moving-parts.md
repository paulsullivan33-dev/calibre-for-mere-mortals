# The Moving Parts

Calibre looks like one program in the
applications menu, but it is a family of
tools sharing one library. Knowing which
piece holds what will save you real time
the first time something misbehaves —
and, in this guide's lab, it was the
difference between "the GUI won't run
here" and "everything that matters runs
fine": the lab machine had no screen, so
the lab exercised every part except the
windows.

## 1. The library: a folder and a database

A calibre library is a folder. Inside it,
after the lab added two books, it looked
like this (transcript t01):

```text
library/
  metadata.db
  Lewis Carroll/
    Alice's Adventures in Wonderland (1)/
      Alice's Adventures in Wonderland - Lewis Carroll.epub
      cover.jpg
      metadata.opf
  Mary Wollstonecraft Shelley/
    Frankenstein; or, The modern Prometheus (2)/
      Frankenstein; or, The modern Prometheus - Mary Wollstonecraft Shelley.epub
      cover.jpg
      metadata.opf
```

Three kinds of thing live here:

- **`metadata.db`** — a SQLite database
  holding the whole catalogue: every
  book's title, authors, tags, series,
  ratings, and where its files are. This
  file *is* the library, in the way a
  card catalogue is a library.
- **One folder per author, one per book,**
  named from the metadata, with the
  book's number in brackets. Inside: the
  book's files (one per format), its
  `cover.jpg`, and a `metadata.opf`.
- **`metadata.opf`** — the book's metadata
  written out as a file, one per book.
  It is the safety net: if `metadata.db`
  is ever lost or corrupted, calibre can
  rebuild the catalogue from these
  (chapter 10).

Everything in this folder is calibre's
working area. The rule, stated once here
and enforced everywhere: **never add,
rename, move or delete files inside a
library folder yourself.** The database
wouldn't know, and a database that
disagrees with its files is how libraries
get damaged. Chapter 4 returns to this;
chapter 14 has the check that tells you
whether a library still agrees with
itself.

## 2. The graphical program: the front desk

`calibre` itself is the windowed
application most people use: the book
grid, the tag browser down the side, the
edit dialogs, the viewer. It is the
comfortable way to do everything in this
guide — and it is the one part the lab
could not run, having no display. Where a
chapter describes the GUI, it follows the
project's manual and says so.

## 3. calibredb: the same desk, from the shell

`calibredb` is the command-line interface
to the same database: add, list, search,
show and set metadata, export, check the
library. It is not a lesser subset — the
lab ran the whole library lifecycle
through it — and it is what makes a
library scriptable: nightly imports,
batch conversions, reports. It takes the
library's location as `--with-library`,
and nearly every chapter leans on it:

```bash
calibredb list --with-library /path/to/library
```

One warning that matters: calibredb works
on a library **on disk**, and a library
should have only one writer at a time.
Running calibredb against a library the
GUI currently has open is asking two
desks to file into one cabinet — close
one first. (Pointing calibredb at a
running content server instead is the
supported way to work remotely; chapter 9
mentions it and the authentication it
needs.)

## 4. ebook-convert: the print shop out back

`ebook-convert` turns a file in one
format into another:

```bash
ebook-convert alice.epub alice.mobi
```

It does not need the library at all — it
works on loose files — which makes it the
tool for one-off jobs. Chapter 6 covers
what the conversion actually does to a
book, and why "convert" means re-typeset,
not copy.

Around these two sit smaller tools the
guide uses where they fit:
`ebook-meta` reads and writes a single
file's embedded metadata, `fetch-ebook-metadata`
downloads metadata from online sources
(chapter 5), `ebook-edit` is the built-in
editor, and `ebook-viewer` the reader.

## 5. The content server: the reading room

`calibre-server` serves a library over
HTTP: a web interface for browsers, and
OPDS feeds — the open catalogue protocol
reader apps speak — for phones, tablets
and e-readers. It can run from inside the
GUI or standalone on a machine with no
screen at all, which is how the lab ran
it (chapter 9). It reads the same
`metadata.db`; it changes nothing about
the layout in part 1.

## How the parts fit

One library folder, one database as the
single source of truth; the GUI and
calibredb as two doors into it, never
both at once; the converter as a workshop
that takes books in and hands new formats
back; the server as a window the rest of
the house looks through. Every workflow
in this guide is some combination of
those moves.
