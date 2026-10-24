# Converting Between Formats

Conversion is calibre's second job and
the reason many people install it: a book
exists in one format, a device wants
another, and something has to re-typeset
the book across the gap. That word is
chosen carefully. A conversion is **not**
a photocopy and not a file rename — the
converter takes the book apart into its
structure (chapters, headings, paragraphs,
images, a table of contents), then builds
a new book in the target format from that
structure. What survives is everything
structural. What does not survive is
exact appearance: fonts, page breaks and
fine layout belong to the old format's
world, and the new one makes its own.

## The one command

On loose files, conversion is a single
command (transcript t06):

```bash
ebook-convert alice.epub alice.mobi
ebook-convert alice.epub alice.pdf
```

The output format is read from the file
extension you ask for. The lab's runs:

| From | To | Result |
|---|---|---|
| alice.epub (136,756 bytes) | MOBI | 189,810 bytes, written in seconds |
| alice.epub | PDF | 477,513 bytes, **93 pages** |

A PDF is the odd one in the table: it is
the only common output with *pages* at
all, because PDF is a fixed-layout format
— the converter must choose a page size
and margins and pour the book into them
(`--paper-size`, `--margin-*` if the
defaults displease). Every other format
flows to fit the reader's screen and font
settings, which is what e-readers are
for. One honest line from the lab's PDF
run: it needed a workaround on a
screen-less machine run as root —
chapter 14 has it, because it will bite
anyone converting in a container or on a
server.

## Converting inside the library

A loose conversion makes a file. Usually
you want the new format *attached to the
book*, so the library offers it to devices
and the server alongside the original.
Two routes:

- **In the GUI** (documented): select
  books, **Convert books**, individually
  or in bulk. The original is kept; the
  new format joins the record.
- **From the shell**, the lab's route:
  convert the file, then attach it:

```bash
ebook-convert alice.epub alice.mobi
calibredb add_format --with-library ~/library 1 alice.mobi
```

after which `calibredb list --fields formats`
shows Alice holding EPUB and MOBI — one
book, one catalogue entry, two files
(transcript t06). Bulk conversion to a
device's format, on a schedule, is a
small script around exactly these two
commands.

Conversion settings — the output
**profile** (which device's screen to
optimise for), margins, how chapter
breaks and headings are detected, what to
do with the original's fonts — are a
per-conversion or per-book choice in the
GUI and `--output-profile` and friends on
the command line. The defaults are sane
for prose; the manual's conversion
chapter is the reference for the hundred
knobs, and chapter 13 explains why no
setting fixes the next section's cases.

## What converts well, and what doesn't

**Well:** ordinary books. Novels, essays,
manuals with simple structure, anything
that began life as flowing text in EPUB,
MOBI, AZW3, DOCX, HTML or plain text.
Chapters, headings, italics, images and
the contents page come through; the lab's
two conversions were this case, start to
finish in seconds.

**Badly, and no setting rescues it:**

- **PDF as input.** A PDF knows where ink
  sits on pages, not what the words'
  order or the paragraphs are. The
  converter guesses — columns interleaved,
  page headers repeated through the text,
  hyphenated line-breaks fossilised. Fine
  for ten pages, misery for a novel. If a
  book exists anywhere in a flowing
  format, convert *that*.
- **Scanned books.** A scan is a
  photograph of pages. There is no text
  to convert until OCR software reads the
  pictures, and calibre does not do OCR.
- **Fixed-layout and image-heavy books.**
  Cookbooks, comics, children's picture
  books and design-heavy nonfiction are
  composed, not flowed; conversion keeps
  the pictures and loses the composition.
- **DRM-locked books.** The converter
  refuses them outright — chapter 13.

## Which format for which device

The short table; chapter 8 gives the
devices' side of the story.

| Destination | Ask for |
|---|---|
| Modern Kindle | AZW3 |
| Very old Kindle, or Send to Kindle | MOBI (legacy) |
| Kobo, Nook, most other readers and apps | EPUB |
| Printing, or a screen that only takes documents | PDF |
| Reading in a terminal or plain-text tools | TXT |

Keep the EPUB as the library's master
where you can: it is the most open,
best-structured common format, and every
other format in the table converts from
it cleanly. Converting *from* a derived
format (a MOBI someone sent you) works,
but each generation of re-typesetting
loses a little, so the library's copy
should be the earliest generation you
have.
