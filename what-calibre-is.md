# What Calibre Is

Calibre is a program for managing a
collection of ebooks: cataloguing them,
fixing their descriptions, converting
them between formats, and getting them
onto the devices you read on. It is free,
open-source software that runs on
Windows, macOS and Linux, and it has been
in continuous development by Kovid Goyal
and contributors since 2006 — older than
the Kindle, and shaped by every format
war since.

## Three jobs in one program

Most people meet calibre through one job
and discover the others later. It helps
to hold all three from the start:

| Job | What it does | The piece that does it |
|---|---|---|
| **Librarian** | Keeps one catalogue of every book, with title, author, tags, covers and ratings | The library and its database (chapter 2) |
| **Converter** | Re-typesets a book from one format into another — EPUB to Kindle format, PDF to EPUB, and dozens more pairings | `ebook-convert` (chapter 6) |
| **Server** | Puts the library on your home network, in a browser or a reader app | The content server (chapter 9) |

The librarian is the centre. The converter
works on books in the library (or on loose
files), and the server serves the
library — so the quality of everything
downstream depends on the catalogue being
right, which is why chapter 5 spends so
long on metadata.

## A library, not a folder of files

The idea to take away from this chapter
is that calibre is a **database with
books attached**, not a file manager with
extras. When a book is added, calibre
copies the file into its own library
folder, files it under the author's name,
and records everything about it in the
database. From then on, the database is
the truth: you search it, sort it, edit
it, and calibre keeps the files in step.
Chapter 2 shows the layout and states the
rule that follows from it — you never
rename or rearrange the library folder
yourself, for the same reason you don't
rearrange a card catalogue's drawers with
a broom.

This design is why calibre suits the
mess described in the introduction. A
downloads folder answers "where is the
file?". A calibre library also answers
"what is it, who wrote it, have I read
it, what else is in the series, and can
my e-reader open it?" — and it can act on
the answers: convert this, send that,
serve the other.

## Who it is for

Anyone whose books live on more than one
device or in more than one format, which
in practice means anyone with an e-reader
that isn't fed by exactly one shop. The
project's own summary calls calibre "a
powerful and easy to use e-book manager",
and the audience it suits best is a
reader with a growing pile: the
public-domain collector, the household
sharing one library between a Kindle, a
Kobo and two phones, the researcher with
four hundred PDFs, the small organisation
with manuals nobody can find. The common
thread is that the books came from
several places and are read in several
places, and one catalogue has to cover
all of it.

## What it is not

- **Not a bookshop.** Calibre has no store
  and sells nothing. It manages books you
  already have; where they come from —
  Project Gutenberg, a publisher, a shop
  that lets you download your purchases —
  is your business.
- **Not primarily a reading app.** It
  includes a perfectly good viewer
  (chapter 8), but its centre of gravity
  is managing the collection, not the
  armchair.
- **Not a DRM remover.** Books locked by a
  shop's digital rights management stay
  locked. Calibre cannot open them, let
  alone convert them, without third-party
  plugins this guide does not cover —
  chapter 13 is plain about the wall.
- **Not a cloud.** The library lives on
  one computer's disk. The content server
  can share it across your network and,
  carefully, beyond — but there is no
  account syncing your library into
  someone else's data centre unless you
  build that yourself.
- **Not maintenance-free.** A library is a
  database and a folder of files, and it
  deserves the backup in chapter 10.

## The one-sentence version

If your ebooks currently live in a
downloads folder, on three devices, and
in formats half of them can't open,
calibre gives them one catalogue, one
converter, and one front door — at the
price of letting it own the folder they
live in.
