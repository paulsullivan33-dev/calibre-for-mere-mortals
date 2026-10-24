# Limits

What calibre doesn't do, stated plainly
enough to plan around.

## The DRM wall

Books bought from the big shops arrive
locked with digital rights management.
Calibre can catalogue the files it can
read, but a locked book it cannot open,
convert, or serve — the converter refuses
it outright. Plugins that strip DRM
exist in the world; they are not part of
calibre, this guide does not cover them,
and their legality varies by country.
Practical consequence: the value of a
calibre library is greatest for books
that arrive unlocked — public domain,
publisher-direct, shops that sell
DRM-free — and a library strategy that
ignores the wall will keep walking into
it.

## One library, one writer

The database is single-writer. The GUI,
`calibredb` and the server cooperate only
in the arrangements chapter 2 and
chapter 9 describe; two programs writing
at once, or a sync tool rewriting files
underneath, are how databases corrupt.
For a household this is fine — the server
is the shared door. For an organisation
wanting twenty simultaneous librarians,
calibre is the wrong shape entirely.

## Conversion is re-typesetting, not rescue

Chapter 6's list bears repeating as a
limit: PDF in is guesswork, scans need
OCR calibre doesn't do, fixed-layout
books lose their composition, and a
badly-made source converts into a
faithfully badly-made result. The
converter is excellent at its real job —
flowing prose between formats — and no
setting enlarges that job.

## The GUI is the main road

The command line in this guide is real
and complete for the library's lifecycle,
but calibre is designed GUI-first: some
things live only in the windows (virtual
library editing, the metadata download
review screen, the device drivers'
preferences, the editor). A headless
calibre, like the lab's, is a supported
and useful creature — and it is not the
whole animal. The chapters flag each
documented-only feature where it stands.

## It is a desktop program wearing a server's coat

The content server serves a household
well. It is not a hardened public
service: no rate limiting, no elaborate
account system, and a password model
meant for families (chapter 9). Putting
it on the open internet without a
reverse proxy and care is asking a
reading room to be a bank vault.

## Metadata is only as good as its sources

Chapter 5's Frankenstein arrived wearing
eight subject headings and no
description; other books arrive with the
wrong author entirely. Calibre's tools
for fixing this are good, its automatic
sources are fallible, and there is no
setting that makes inherited metadata
true. The care is manual, at the door,
forever.

## The reader is not the ecosystem

Calibre manages books; it does not sync
reading positions across a Kindle, a
phone and its own viewer (Kobo positions
are the partial exception, chapter 8),
sell you anything, or know what a shop
knows about your purchases. People who
want one account silently following them
from screen to screen want a shop's
walled garden — with the walls that come
with it.
