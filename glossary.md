# Glossary

**add_format** — the calibredb command
that attaches another format's file to an
existing book record. Chapters 4 and 6.

**Author sort** — the filing form of an
author's name ("Shelley, Mary
Wollstonecraft") kept beside the display
form, so books shelve by surname.
Chapter 5.

**AZW3** — Amazon's current Kindle
format (also called KF8). What calibre
converts to for modern Kindles.
Chapters 6 and 8.

**calibre-server** — the standalone
content server program; serves a library
over HTTP and OPDS. Chapter 9.

**calibredb** — the command-line
interface to the library database: add,
list, search, metadata, export, checks.
Chapter 2.

**Content server** — calibre serving a
library to browsers and reader apps; see
calibre-server. Chapter 9.

**Conversion** — re-typesetting a book
from one format into another with
`ebook-convert`: structure survives,
exact layout does not. Chapter 6.

**DRM** — digital rights management, the
locking applied by ebook shops. Calibre
cannot open, convert or serve locked
books. Chapters 1 and 13.

**ebook-convert** — the conversion
command; works on loose files, no
library required. Chapter 6.

**EPUB** — the open ebook format most of
the industry outside Amazon uses, and
the recommended master format for a
library. Chapter 6.

**Format** — one flavour of a book:
a single book record can hold EPUB,
MOBI, PDF and more at once, one file
each. Chapters 2 and 6.

**Id** — the number calibre gives a book
record on arrival; most calibredb
commands address books by it.

**KEPUB** — Kobo's EPUB variant, with
faster page turns on Kobo devices;
reachable through the Kobo driver.
Chapter 8.

**Library** — a folder holding
`metadata.db`, one folder per author and
book, and the books' files. Calibre's
alone to arrange. Chapters 2 and 10.

**metadata.db** — the SQLite database at
a library's root: the catalogue itself.
Chapters 2 and 10.

**metadata.opf** — a per-book file
holding that book's metadata; the safety
net from which a damaged database can be
rebuilt. Chapters 2 and 10.

**MOBI** — the legacy Kindle format.
Still opens on Kindles; retired by
Amazon's Send to Kindle service in
favour of EPUB. Chapters 6 and 8.

**OPDS** — Open Publication Distribution
System, the catalogue protocol reader
apps use to browse and download from the
content server. Chapter 9.

**Output profile** — the device class a
conversion optimises for (screen size,
features). Chapter 6.

**Rating** — a book's stars, 0 to 5,
set in stars, stored doubled (0–10),
and printed differently by different
commands. Chapter 5.

**Saved search** — a named search
expression kept with the library,
reusable as `search:name`. Chapter 7.

**Series / series index** — the name and
position of a book within a sequence;
exact data, unlike tags. Chapter 7.

**Tags** — free-form labels on a book;
most useful as a small, chosen
vocabulary. Chapters 5 and 7.

**Virtual library** — a named subset of
the library, defined by a search, that
acts as the whole library for browsing,
sending and serving. Chapter 7.
