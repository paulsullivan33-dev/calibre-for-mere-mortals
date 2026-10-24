# Troubleshooting

Every entry here except the general
advice was hit for real by this guide's
lab, on the day, and fixed. The order is
roughly the order you'll meet them.

## PDF conversion dies with a Chromium complaint

**Symptoms:** `ebook-convert book.epub book.pdf`
fails on a server or in a container,
with errors about Vulkan, GPU vendors
and — the telling line — *"Running as
root without --no-sandbox is not
supported."* Other formats convert fine.

**Cause:** PDF output is rendered by an
embedded Chromium (via Qt WebEngine),
and Chromium refuses to run its sandbox
as root. On a normal desktop you're not
root and never see this; on a headless
box you often are.

**Fix:**

```bash
QTWEBENGINE_CHROMIUM_FLAGS=--no-sandbox \
  ebook-convert book.epub book.pdf
```

The lab's 93-page PDF appeared
immediately (transcripts t06 and t06b).
Know what you're trading: the flag turns
off a browser sandbox for the length of
one conversion of a book you supplied —
a reasonable trade at home, worth
thinking about before converting files
from strangers.

## The rating is not the number I typed

**Symptoms:** you set `rating:8` and the
book shows 5. Or `list --fields rating`
says 9 while `show_metadata` says 4.5.

**Cause:** three commands, two units.
`set_metadata` takes **stars, 0 to 5**,
and silently caps anything above 5. The
database stores the rating doubled
(0–10). `show_metadata` and the content
server print stars; `list` prints the
raw stored number.

**Fix:** none needed — type stars, and
read `list` output as double. Chapter 5
has the full set of receipts
(transcripts t05, t05b, t08).

## My library is empty — no, it's a different library

**Symptoms:** `calibredb list` shows no
books, but the library was full
yesterday.

**Cause:** almost always the path.
`calibredb` happily **creates a fresh,
empty library** at whatever
`--with-library` path you give it — that
is how new libraries are born — so a
typo, a moved folder, or a shell variable
that didn't get set gives you a pristine
empty library and a moment of horror.
Your real one is untouched at its old
address.

**Fix:** find the folder with
`metadata.db` in it and point at that:

```bash
find ~ -name metadata.db 2>/dev/null
```

Then set the path once, in a variable or
an alias, rather than retyping it (the
lab used `$LIB` throughout its
transcripts for exactly this reason).

## I tidied the library folder and now books are wrong

**Symptoms:** books missing files, covers
gone, entries pointing at nothing —
starting right after a session with a
file manager inside the library folder.

**Cause:** chapter 2's rule. The database
records where everything is; moving or
renaming files by hand teaches the
filesystem a truth the database doesn't
share.

**Fix:** first, measure the damage:

```bash
calibredb check_library --with-library ~/library
```

It lists the drift by category (missing
formats, extra files, unreadable
folders). Small drift: re-add the
strays properly (chapter 4), remove
broken entries, let calibre rename via
metadata edits. Big drift or a dead
`metadata.db`: the `.opf` safety net —
`calibredb restore_database` rebuilds
the catalogue from the per-book files
(chapter 10, with its list of what a
rebuild does *not* bring back). Then
back up the repaired library before
touching anything else.

## The installer, or a download, dies on a strange DNS error

**Symptoms:** the official Linux
installer fails early with an error
about an `idna` codec and a "label too
long" — a hostname that isn't one — on a
network behind a proxy. In calibre
itself, `fetch-ebook-metadata` fails
similarly while browsers work fine.

**Cause:** calibre's own small HTTPS
helper (used by the installer and by
live downloads) parses the proxy address
by hand and cannot cope when the address
contains **credentials** —
`user:password@proxy:port` becomes the
"hostname" it tries to resolve. Ordinary
programs using the system proxy settings
are unaffected.

**Fix:** give calibre a proxy address
without credentials for the duration of
the command — a local relay that adds
the credentials back is one way; a
network segment where the proxy needs
none is another. The lab's version of
this story, including fetching the
installer tarball by hand when the
signature host proved unreachable, is in
chapter 3 and transcript t10. Home
networks without proxies never meet it;
corporate ones do.

## The server answers, but shows the wrong books

**Symptoms:** the content server runs,
the page loads, and the library in it is
empty, stale, or somebody else's.

**Cause:** the server was pointed at a
different library path than the one you
edit (see the empty-library entry above
— the same trap, wearing a port), or a
second server is already holding the
port and you're talking to the old one.

**Fix:** check what is actually running
— `ps` for the `calibre-server` command
line shows its library path and port —
stop it, and start the server with the
full path to the library you mean:

```bash
calibre-server --port 8080 /full/path/to/library
```

## calibredb "changed nothing" while the GUI was open

**Symptoms:** a `set_metadata` or `add`
appears to succeed (or waits, or warns
about the database), but the GUI shows
the old state.

**Cause:** one library, one writer
(chapter 2). The GUI holds the database;
an outside writer is locked out or
working against a state the GUI will
overwrite from its own view.

**Fix:** pick a door. Either close the
GUI before shell work, or address
`calibredb` to the content server
(chapter 9) so the running program is
the one making your changes.
