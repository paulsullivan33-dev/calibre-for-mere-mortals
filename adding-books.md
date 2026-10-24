# Adding Books

Adding a book means handing calibre a
file and letting it catalogue the book:
copying the file into the library, reading
the metadata out of it, and filing
everything under the author. The original
file is never touched — calibre works on
its own copy from this moment on, which
is worth pausing on. Your downloads
folder stays exactly as messy as it was;
the library is the tidy copy.

## From the command line

The lab's whole library was built with
one command (transcript t01):

```bash
calibredb add --with-library ~/library \
  alice.epub frankenstein.epub
```

```text
Added book ids: 1, 2
```

Each book gets a number — its **id** —
which most other calibredb commands use
to name the book they mean. What landed
on disk is chapter 2's layout: an author
folder, a title folder with the id in
brackets, and inside, the book file
renamed to `Title - Author.epub`, its
cover pulled out as `cover.jpg`, and a
`metadata.opf` recording what calibre
learned.

Metadata can be set right at the door:

```bash
calibredb add --with-library ~/library \
  --tags "Classic fiction" \
  --series "Discworld" --series-index 4 \
  city-watch.epub
```

Whatever the file itself claims can be
overridden the same way (`--title`,
`--authors`, `--isbn`, `--languages`).

## Folders of books

Point `add` at a folder and it takes the
ebook files it finds there; two options
shape how:

```bash
# every ebook file under this folder, each
# treated as its own book
calibredb add --with-library ~/library \
  --recurse ~/Downloads/ebooks

# one folder per book, holding several
# formats of the same title
calibredb add --with-library ~/library \
  --recurse --one-book-per-directory ~/sorted-books
```

The second form matters more than it
looks. The same novel as EPUB, MOBI and
PDF is **one book with three formats** in
calibre, not three books — one catalogue
entry, one set of metadata, three files.
Adding formats to an existing book is
also a command of its own (the lab used
it in chapter 6):

```bash
calibredb add_format --with-library ~/library 1 alice.mobi
```

## Duplicates

Add the same book twice and calibredb
will, by default, add it twice: the check
it makes is deliberately light (title and
author), and it would rather duplicate
than guess wrongly about two editions.
Three tools keep a library honest:

- `--automerge` on `add` merges an
  incoming file into the existing record
  when title and authors match, instead
  of creating a twin.
- Sorting the library by title groups a
  book's accidental twins together where
  your eyes can settle them; the GUI can
  then merge records onto one.
- Chapter 10's `check_library` reports a
  library whose files and database have
  drifted apart — duplicates are a
  catalogue problem, not that kind of
  drift, but a periodic check keeps both
  in view.

Which behaviour you want depends on
whether your pile holds *editions* (keep
both, deliberately) or *accidents*
(merge). Calibre cannot know; that is
your call, made once, as a habit.

## In the GUI (documented)

The windows way is the **Add books**
button, or dragging files onto the book
list. It does the same work as the
command above, with dialogs for the
folder and duplicate choices. What it
adds over the shell is the review step:
calibre can show each incoming book's
metadata before committing it, which is
the cheapest moment to catch a file whose
innards claim the wrong title entirely.
This guide's lab had no GUI to try it
with; the manual's *Adding books* section
is the source.

## Books with no file

A library can hold a record with no
ebook at all:

```bash
calibredb add --with-library ~/library --empty \
  --title "The Paper Copy on the Shelf" --authors "A. Writer"
```

Paper books, borrowed books, the one you
lent out in 2019 — a catalogue that only
lists what is digital quietly teaches you
to forget the rest. Empty records keep
one list for everything, and a format can
be attached later if a digital copy ever
turns up.

## The rule, again

However a book got in, the folder it
landed in is calibre's. If a file in the
library looks wrongly named, the fix is
to fix its **metadata** (chapter 5) and
let calibre rename things — never a file
manager. People who tidy library folders
by hand meet chapter 14's repair tools
next.
