# Recipes

Four working arrangements, each built
from chapters you've already read. None
needs anything beyond the tools this
guide has run or documented.

## 1. The public-domain classics shelf

**The shape.** Project Gutenberg and its
kin hold tens of thousands of books whose
copyright has expired, free in EPUB. The
risk isn't scarcity, it's sprawl: a
hundred classics grabbed in an evening,
catalogued in nobody's vocabulary.

**The habit.** Add in small batches and
fix metadata on arrival, while the batch
is still on screen:

```bash
calibredb add --with-library ~/library ~/incoming/*.epub
# then, per book, the chapter 5 tidy:
calibredb set_metadata --with-library ~/library 12 \
  --field "tags:Classic fiction"
```

The lab's entire run is this recipe at
two books: inherited subject headings
replaced with household tags, ratings
set, one book converted for a Kindle.
The two minutes per book at the door is
what keeps a thousand-book shelf
browsable in chapter 7's terms.

## 2. A family library on a home server

**The shape.** One always-on machine
(an old laptop, a small server) holds the
library; the house reads from it.

**The pieces.** Calibre installed
headless (chapter 3); the server run as a
service with accounts on (chapter 9):

```bash
calibre-server --port 8080 --enable-auth ~/library
```

Each reader gets the web address or adds
the OPDS feed to their app. Parents'
books and children's books share one
library, separated by chapter 7's virtual
libraries — one per reader, defined from
a tag — so the kids' tablet sees the
kids' shelf. New books land by whichever
chapter 4 route the household prefers;
the backup is chapter 10's folder copy,
swept up by whatever already backs up
the server.

## 3. A scripted intake folder

**The shape.** A folder everyone drops
ebooks into, emptied into the library
nightly, no human at the desk.

**The script**, built only from commands
this guide ran for real:

```bash
#!/bin/sh
# intake.sh — run from cron, library not in use
LIB=$HOME/library
QT_QPA_PLATFORM=offscreen calibredb add \
  --with-library "$LIB" --automerge \
  "$HOME/incoming" --recurse
QT_QPA_PLATFORM=offscreen calibredb check_library \
  --with-library "$LIB"
```

`--automerge` (chapter 4) files repeat
formats onto the records they belong to.
Run it when the GUI is closed and the
server elsewhere — one writer (chapter
2). The honest limit: the script files
books; it does not *review* them, so tags
arrive as inherited as chapter 5 found
them. A weekly human pass with the tag
report (`list_categories`, chapter 7)
keeps the vocabulary clean.

## 4. The manuals and documents shelf

**The shape.** Appliance manuals,
datasheets, the PDF the council sent —
documents, not literature, that everyone
loses.

**The arrangement.** They go in as books
like any other (chapter 4); PDF is a fine
format to *store and serve*, whatever
chapter 6 said about converting *from*
it. Tag them by room or device model, and
the content server (chapter 9) becomes
the household's answer to "where's the
washing machine manual": searchable from
the phone standing in front of the
machine. What this shelf does not get
from calibre is full-text search of the
PDFs' insides unless the GUI's full-text
indexing is switched on (documented) —
the catalogue is metadata-deep, so honest
titles and tags do the finding.
