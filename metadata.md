# Metadata

Metadata is the information *about* the
book: title, author, tags, series,
publisher, date, identifiers, the cover,
and the short description readers actually
browse by. It is the difference between a
library and a pile, and it is the part of
calibre where a little regular care pays
for itself every time you search. This
chapter shows what a book arrives with,
how to inspect and change it from the
command line, and the two traps the lab
measured — one in the sources books come
from, one in calibre itself.

## What a book arrives with

Whatever the file claims. For the lab's
two Gutenberg books, that was generous
and noisy at once (transcript t03):

```text
$ calibredb show_metadata --with-library ~/library 2
Title               : Frankenstein; or, The modern Prometheus
Author(s)           : Mary Wollstonecraft Shelley [Shelley, Mary Wollstonecraft]
Tags                : Science fiction, Horror tales, Gothic fiction,
                      Scientists -- Fiction, Monsters -- Fiction,
                      Frankenstein, Victor (Fictitious character) -- Fiction,
                      Frankenstein's monster (Fictitious character) -- Fiction
Identifiers         : uri:http://www.gutenberg.org/84
```

Those tags are Library of Congress
subject headings — accurate, and useless
as shelving in a home library: eight tags
for one book, in a vocabulary nobody
browsing at midnight would guess. Books
from other sources arrive with the
opposite problem: no tags, the author's
name three ways across three books, a
title carrying the series name, the
publisher's marketing paragraph as the
description. Both kinds are normal. The
metadata is raw material, not gospel, and
calibre's tools exist because fixing it
is routine work, not an edge case.

Also in the output: the **author sort**
in brackets — `Shelley, Mary Wollstonecraft`
— which is how the library shelves her
under S while displaying her name
properly. Calibre maintains sort forms
for titles and authors alongside the
display forms, and most "why is this
filed there?" questions are answered by
looking at them.

## Changing it

`set_metadata` takes fields one by one:

```bash
calibredb set_metadata --with-library ~/library 2 \
  --field "tags:Classic fiction, Gothic, Horror"
```

(Quote values: they contain spaces and
commas, and your shell will otherwise
have opinions.) `--list-fields` names
every settable field. The lab used the
command to replace both books' inherited
tag sprawl with a small household
vocabulary — and this is the habit that
scales: five tags you chose beat fifty
you inherited, because chapter 7's
browsing is only as good as the words it
has to work with.

In the GUI the same work happens in the
**Edit metadata** dialog — individually,
or in bulk across a selection, which is
how a shelf of one author's books gets
its name spelled one way on all of them.
The dialog also holds the **Download
metadata** button described below. This
guide's lab had no GUI; the dialog
follows the manual.

## The rating trap, measured

Ratings are where the lab caught calibre
being genuinely confusing, so here are
the receipts (transcripts t05 and t05b):

- `set_metadata --field rating:8` was
  **accepted silently** — and the book
  then showed `Rating: 5`.
- `set_metadata --field rating:4.5` on
  the other book showed `Rating: 5` too.
- Setting `rating:4` and `rating:4.5`
  instead, then listing with
  `--fields rating`, showed **8 and 9**.

The explanation, once all three outputs
are on the table: `set_metadata` takes a
rating in **stars, 0 to 5**, halves
allowed, and anything above 5 is quietly
capped at 5. Inside the database the
rating is stored doubled, on a 0–10
scale. And the commands disagree about
which scale they speak: `show_metadata`
prints stars, `list` prints the raw
stored number, and the content server's
JSON prints stars again as a decimal
(`"rating": 4.0` in transcript t08).
Nothing is broken; three honest answers
are given in two different units, and
only the receipts show it. Rule of thumb:
type stars, expect stars back from
anything except `list`, where you will
see double.

## Downloading metadata — and the lab's ceiling

The designed way to enrich a book is to
fetch metadata for it: `fetch-ebook-metadata`
(or the GUI's Download metadata button)
takes a title, author or ISBN and queries
online sources for a better record —
cleaner title and author, a real cover,
a description, identifiers, sometimes a
publisher and date worth having.

**The lab could not verify this.** On
calibre 9.17 the command first downloads
a helper module from
`code.calibre-ebook.com` before it
queries anything, and the lab's network
answered that host with empty replies on
every attempt (transcript t10 has both
failures, including the one through a
proxy workaround). This is a property of
the lab's sandbox, not of your home
connection — but the guide reports what
it ran, so: metadata *download* is
documented-only here, on the manual's
word, while everything else in this
chapter was run.

Two cautions that hold wherever it runs.
Downloaded metadata is a **suggestion
with confidence**, not a correction: the
top match for a common title is often a
different edition, occasionally a
different book, so review before applying
— the GUI shows the candidates side by
side for exactly this reason. And it
needs an ISBN or a distinctive title to
do its best work; `Identifiers` like the
Gutenberg `uri:` above are how calibre
keeps track of which outside record a
book came from.

## Which copy is true

Edits change the **database**. The book
files still carry their old embedded
metadata until something updates them —
which happens automatically when a book
is exported or sent to a device
(chapters 8 and 10), or on demand:

```bash
calibredb embed_metadata --with-library ~/library all
```

The per-book `metadata.opf` (chapter 2)
is updated on every edit regardless,
which is what makes it a trustworthy
safety net. So the order of truth is:
database first, `.opf` in step, files
when they leave.
