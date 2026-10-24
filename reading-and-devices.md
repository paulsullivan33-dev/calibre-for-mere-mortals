# Reading and Devices

Most books in a library are going
somewhere: a Kindle in a bag, a Kobo by
the bed, a phone on a train. This is the
chapter of destinations. One honesty note
before it starts: this guide's lab ran on
a machine with no display and no devices
attached, so the viewer and the USB
workflows below are **documented** from
the project's manual — what the lab did
verify about devices is the part
underneath them all, that one book holds
several formats and calibre picks per
destination (chapter 6, transcript t06).

## Reading on the computer

`ebook-viewer` opens any book calibre
knows, and most loose ebook files beside:
full-text search, annotations and
highlights (which calibre stores with
the library, so they survive the book
moving), bookmarks, and a read-aloud
mode. It opens MOBI and AZW3 as happily
as EPUB, which makes it the quiet
household hero for reading the file a
friend sent that nothing else would
open. Double-clicking a book in the GUI
opens it here.

## Sending to an e-reader (USB)

Plug the reader in with USB and the GUI
gains a device view. **Send to device**
copies selected books across; calibre
knows each mainstream device's preferred
format — AZW3 for current Kindles, EPUB
for Kobo and Nook — and converts on the
fly when the book doesn't already have
it. Chapter 6's rule is what makes this
calm: the book keeps all its formats, so
sending is a choice per trip, not a
conversion project per device. Eject
from calibre, not mid-write.

Two provider facts that shape real
libraries:

- **Kindle over email is a different
  road.** Amazon's Send to Kindle service
  has retired MOBI — it accepts EPUB now
  and converts it itself. What calibre
  sends over USB is separate from that
  and still AZW3-first.
- **Kobo owners can go one better** with
  the KoboTouch driver's KEPUB output:
  Kobo's own variant of EPUB with faster
  page turns and chapter statistics.
  It is a plugin-level detail; the
  driver's preferences are where it
  lives, and the manual covers it.

## Getting books without a cable

Three wireless roads, in increasing
order of setup:

1. **The content server (chapter 9).**
   Any modern reader app or browser on
   your network can browse the library
   and download books. For many households
   this replaces USB entirely.
2. **Email delivery from calibre.** The
   GUI can send a book to an address —
   designed for Kindle's document
   address, gated by your mail settings
   and Amazon's allow-list for senders.
   Documented; needs working mail, which
   the lab had not configured.
3. **Reader apps with OPDS.** Phone and
   tablet reader apps that speak OPDS
   treat the content server as a built-in
   bookshop of one. Chapter 9 shows the
   feed the lab fetched.

## Where the books are, per device

Once sent, a book is a copy; the library
keeps the master. Deleting a book from a
device deletes the copy and nothing else
— and deleting it *in calibre's device
view* is the supported way, so the device
stays in step. Reading positions sync for
Kobo devices through the driver; Kindle
positions do not flow back into calibre.
Everyone's highlights in the *viewer*
live with the library (in its data
folder), not inside the book files,
unless you export them.
