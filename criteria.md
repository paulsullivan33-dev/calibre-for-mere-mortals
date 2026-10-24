# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Built and verified 2026-10-24 against
**calibre 9.17.0** (the current release
on build day), on Ubuntu 24.04, on a
machine with no display: every calibre
command ran headless with
`QT_QPA_PLATFORM=offscreen`.

**Primary sources read, not remembered:**
the project's official manual — the
calibredb command reference in full
(every sub-command this guide uses is
described there), the installer's own
source when its failure needed
explaining (chapter 3), and the live
output of the installed tools
themselves.

**The install, with its declared
deviations** (transcript t00; chapter 3
tells it in full): the official
installer's signature step fetches from
`code.calibre-ebook.com` through a small
HTTPS helper that parses proxy addresses
by hand and cannot cope with a
credentialed one — the lab's egress
proxy — and that host returned empty
replies through the lab's network in any
case. The lab therefore fetched the
identical tarball the installer fetches
(the `calibre-ebook.com/dist/linux-x86_64`
redirect to the project's GitHub release
of v9.17.0, 201.6 MB), unpacked it into
`/opt/calibre` (654 MB) and ran
`calibre_postinstall`. The one step not
reproduced is the installer's SHA-512
signature check. System libraries
`libegl1`, `libopengl0` and
`libxcb-cursor0` were installed first, as
the installer itself directs.

**Ran for real** (transcripts in
`calibre-lab/transcripts/`), against a
fresh two-book library of public-domain
EPUBs from Project Gutenberg:

- t00 — `calibre`, `calibredb` and
  `ebook-convert` all report 9.17.
- t01 — `calibredb add` of Alice's
  Adventures in Wonderland (#11) and
  Frankenstein (#84): ids 1 and 2, the
  author/title folder layout, covers
  extracted, `metadata.opf` files and
  `metadata.db` created.
- t02 — `list`, plain and with a field
  set and author sort.
- t03 — `show_metadata` for both books:
  full inherited metadata, including
  Frankenstein's eight Library of
  Congress subject headings as tags.
- t04 — search three ways: `author:`,
  `tags:` through `list --search`, and a
  compound `title: ... or author: ...`
  query.
- t05 — `set_metadata`: both books' tags
  replaced with a household vocabulary;
  ratings set, exposing the scale trap —
  `rating:8` and `rating:9` silently
  capped to 5 stars.
- t05b — the rating resolution: set in
  stars (0–5, halves allowed), stored
  doubled; `rating:4` and `rating:4.5`
  read back as 8 and 9 through
  `list --fields rating`.
- t06 — `ebook-convert` EPUB → MOBI
  (189,810 bytes); `add_format` attached
  it, and `list --fields formats` shows
  Alice holding EPUB and MOBI. The same
  transcript holds the PDF failure:
  embedded Chromium refusing to run as
  root.
- t06b — EPUB → PDF with
  `QTWEBENGINE_CHROMIUM_FLAGS=--no-sandbox`:
  a 93-page, 477,513-byte PDF.
- t07 — `calibredb export --all`: both
  books written out with every format,
  cover and `.opf`.
- t08 — `calibre-server` run against the
  library and queried with curl: the web
  interface answers, the OPDS feed at
  `/opds` describes the library, and
  `/ajax/books` returns the edited
  metadata as JSON — the rating showing
  as `4.0`, the third confirmation of the
  chapter 5 scale story.
- t09 — `check_library` reports every
  category empty, exit 0;
  `backup_metadata --all` rewrote both
  books' `.opf` files.
- t11 — saved searches: `gothic` added
  and listed, then used as
  `search:gothic` in a query;
  `list_categories` counted the library's
  four tags.

**Attempted and not verified, stated
plainly:** `fetch-ebook-metadata`. On
9.17 the command first downloads a
helper module from
`code.calibre-ebook.com`; that host was
unreachable from the lab network (empty
replies on every attempt, including one
through a local proxy relay built to
work around the credentialed-proxy
parsing bug — transcript t10). Chapters
5 and 14 present metadata download as
documented-only for this reason. The
failure is a property of the lab's
sandboxed network; nothing in it
suggests the command misbehaves on an
ordinary connection.

**Documented only, and labelled as such
in the chapters:** the entire graphical
interface (no display existed) — the Add
books flow, the Edit metadata dialog and
its download review screen, the tag
browser, virtual library editing, the
viewer, the editor, and the device
drivers' preferences; sending books to a
physical e-reader over USB and by email
(no device, no mail setup in the lab);
`restore_database` (the lab's database
was never damaged; the rebuild's costs
are quoted from the manual); and remote
`calibredb` against a running content
server (the lab's server and client were
one machine using the folder directly).

**Fixtures:** both books are public
domain (Project Gutenberg #11 and #84);
the edited tags ("Classic fiction",
"Childrens fiction", "Gothic", "Horror")
and the ratings set on them are the
lab's own inventions for demonstration.
No credentials, accounts or personal
data appear in any transcript.
