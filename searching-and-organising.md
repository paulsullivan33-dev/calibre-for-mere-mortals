# Searching and Organising

A library of two books needs no
organising; a library of two thousand
needs nothing else. Calibre's search is
not a box that finds words in titles —
it is a small query language over the
metadata, with named and savable pieces.
Learn it once and it becomes how you
browse, how you build shelves-within-the
library, and how you feed every batch
command in this guide.

## The language

The rule is `field:value`. `author:carroll`
finds Lewis Carroll; `tags:Horror` finds
the one book tagged Horror (transcript
t04). Bare words match against title,
authors, tags and description all at once.
Expressions compose the way you'd expect:

```bash
# either title match or author match
calibredb search --with-library ~/library \
  'title:prometheus or author:shelley'

# both conditions must hold
calibredb list --with-library ~/library \
  --search 'tags:"Classic fiction" and not author:carroll'
```

Quote anything containing a space;
`and`, `or` and `not` group with
parentheses; comparisons work on dates
(`pubdate:>2000`) and numbers
(`rating:>3` — in stars, per chapter 5).
The full field list is chapter 5's
`--list-fields` plus the fields
`show_metadata` prints, and the manual's
*Searching* reference covers the corners
(date prefixes, format: queries, the
`~` "contains" operator).

## From the shell: searches return ids

The useful difference between calibredb's
two commands: `search` returns just the
book ids, and id lists are what the other
commands take — so a search becomes a
batch operation:

```bash
# every book on the "to read" tag, exported
calibredb search --with-library ~/library tags:wishlist
# -> 3,7,12
calibredb export --with-library ~/library 3,7,12 --to-dir outgoing
```

`list` with `--search` is the readable
version of the same query — the lab used
it in t04, and it is what you reach for
when the ids are for your eyes rather
than a pipe.

## Saving a search

A query you run often can be named, kept
with the library, and called back by name
(transcript t11):

```bash
calibredb saved_searches --with-library ~/library \
  add gothic 'tags:Gothic'
calibredb saved_searches --with-library ~/library list
# Name: gothic
# Search string: tags:Gothic

calibredb list --with-library ~/library \
  --search search:gothic --fields title,authors
```

The prefix is `search:` followed by the
saved name. The GUI's search box knows
the same names, so a saved search is
written once and browsed everywhere.

## Virtual libraries

A saved search picks books out of the
library. A **virtual library** goes one
step further: it *is* the library for a
while — the book grid, the server and the
device sync all see only the books the
search matches. The canonical uses are
per-reader shelves ("everything for the
kids' tablet") and per-purpose views
("the unread research pile"). They are
defined in the GUI from a saved search —
this guide's lab had no GUI, so the
feature is documented-only — and they are
why a family can share one library
without sharing one reading list.

## The tag browser, on paper

The GUI's tag browser — every author,
tag, series, publisher and date as a
collapsible tree with counts — has a
command-line equivalent for reports
(transcript t11):

```bash
calibredb list_categories --with-library ~/library \
  --categories tags --item_count
# tags     CATEGORY ITEMS  4
```

`--details` expands it to per-item
counts. For a headless server it is the
fast way to audit a library's vocabulary:
if the tag report shows forty spellings
of one idea, chapter 5's editing chapter
shows how that happened and how to fix
it.

## Organising principles that survive

Two habits, learned from watching real
libraries rot:

1. **Tags are a vocabulary, not a
   dumping ground.** Chapter 5 replaced
   eight inherited Library of Congress
   headings with three chosen words per
   book. Choose a dozen tags for your
   household, write them down, and treat
   anything else as a suggestion to
   normalise. Series, by contrast, are
   exact data: name and number, always,
   because "book 4 of the series" is the
   query you'll run most.
2. **Searches are for the moment,
   virtual libraries for the ongoing.**
   A one-off "show me the unread Gothic"
   is a search. "Maya's tablet" is a
   virtual library. Naming the difference
   keeps saved searches from multiplying
   into a second, unmaintained catalogue.
