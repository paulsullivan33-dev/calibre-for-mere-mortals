# Backup and Moving a Library

A calibre library is unusually honest
about backup: there is no export wizard
standing between you and safety, because
the library *is* a folder. Everything —
the database, every book file, every
cover — lives in one tree (chapter 2).
This chapter is about copying that folder
properly, the finer-grained export for
when a copy is not what's wanted, and
the safety nets calibre keeps inside the
library for when things go wrong anyway.

## The backup: copy the folder

```bash
# with calibre and calibre-server stopped
cp -a ~/library ~/backups/library-2026-10-24
```

That, complete, is a backup. To restore,
copy it back, or point calibre at the
copy (the GUI switches libraries from its
library menu; `calibredb` takes the path
in `--with-library`) and the library is
exactly as it was: metadata, formats,
saved searches, all of it.

Three disciplines make the copy worth
trusting:

- **Copy it shut.** A running calibre (or
  server) may hold the database mid-write.
  One writer, one copy, no exceptions.
- **A backup on the same disk is a
  draft.** Fire, theft and a dying drive
  take the folder and its neighbour
  together. The copy that counts lives
  somewhere else — another machine, an
  external drive, your usual backup
  system sweeping the folder up.
- **Don't "sync" a live library.**
  File-sync tools that rewrite files
  underneath a running database are how
  libraries get quietly corrupted; the
  project advises against keeping the
  live library inside a Dropbox-style
  folder. Copy snapshots out, by all
  means — chapter 11 has a recipe-shaped
  version — but let the original be still
  when it's copied.

## The export: books without the library

Sometimes the destination shouldn't be
another calibre — a folder of books for
a relative's reader, an archive drive, a
subset leaving for good. `export` writes
books out as plain files (transcript t07):

```bash
calibredb export --with-library ~/library \
  --all --to-dir ~/export
```

```text
export/
  Carroll, Lewis/
    Alice's Adventures in Wonderland/
      Alice's Adventures in Wonderland - Lewis Carroll.epub
      Alice's Adventures in Wonderland - Lewis Carroll.mobi
      Alice's Adventures in Wonderland - Lewis Carroll.jpg
      Alice's Adventures in Wonderland - Lewis Carroll.opf
  ...
```

Every format, the cover, and an `.opf`
carrying the full metadata — the export
is deliberately calibre-readable, so the
same folder can be `add`ed into a fresh
library elsewhere and arrive with its
cataloguing intact (chapter 4 in
reverse). Exporting also **embeds the
database's metadata into the files** as
it writes them, which is why an export
makes a better "leave calibre" archive
than copying book files out of the
library tree by hand — the files that
leave carry the truth (chapter 5).

## The safety nets inside

Even without backups, a library carries
its own repair kit:

- **`metadata.opf` files.** One per book,
  refreshed on every metadata edit. If
  `metadata.db` is destroyed, calibre can
  rebuild the catalogue from them:
  `calibredb restore_database --really-do-it`
  (documented from the manual — the lab
  never damaged its database to try it,
  and neither should you on purpose).
  The manual's warning is worth
  repeating: the rebuild recovers books
  and their metadata, but **not** saved
  searches, virtual libraries,
  stored per-book conversion settings or
  custom recipes. A rebuilt library is a
  rescued library, not a restored one.
- **`backup_metadata --all`** forces every
  `.opf` to be rewritten from the
  database, so the safety net is current
  before you rely on it. The lab ran it
  as a rehearsal (transcript t09): both
  books rewritten, no errors.
- **`check_library`** compares the
  database against the files and reports
  drift — missing formats, extra files,
  folders it can't read, the fingerprints
  of someone tidying by hand (chapter 4's
  rule). The lab's two-book library came
  back with every category empty:

```bash
calibredb check_library --with-library ~/library
# Invalid titles / Extra titles / ... all empty, exit 0
```

Run it after any accident, import mishap
or disk problem, and before assuming a
larger library is healthy. It reports;
repairing is chapter 14.

## Moving house

Moving a library to a new computer is
the backup with a longer walk: copy the
folder, install calibre at the other end
(chapter 3), open the copied folder as
the library. Nothing else travels —
settings and plugins live with the
program, not the library, and the GUI
can export those separately (documented,
under *Export/import all calibre data*).
The books, happily, cannot tell the
difference.
