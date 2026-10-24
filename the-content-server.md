# The Content Server

The content server is the library's front
door for the rest of the house: point a
browser, a tablet or a reader app at it
and the whole catalogue is browsable and
downloadable, no cable and no copying
files by hand. It is also the part of
calibre most at home on a machine with no
screen — a home server, a NAS, a spare
laptop in a cupboard — because the server
is a complete, standalone program.

## Running it

The lab ran it exactly like this
(transcript t08):

```bash
calibre-server --port 18099 /path/to/library
# calibre server listening on [::]:18099
```

No other setup. What answered:

- **`http://server:18099/`** — the web
  interface: the library's grid in the
  browser, searchable, with per-book
  pages and download links in every
  format the book holds.
- **`/opds`** — the same library as an
  OPDS feed. OPDS is the open catalogue
  protocol reader apps speak: add the
  address to the app once, and the
  library appears inside it as a bookshop
  of one, with search and categories.
- **`/ajax/books`** — the library as JSON,
  which is how you know the edited
  metadata had truly propagated: the feed
  carried the lab's cleaned-up tags and
  `"rating": 4.0` — chapter 5's rating, in
  stars, shown by a third piece of
  calibre.

Inside the GUI the same server is one
menu away (**Connect/share → Start
Content server**), and everything in this
chapter applies to that one too.

## The password warning

Out of the box the server asks for **no
credentials**: anyone who can reach the
port can browse and download the library.
On a home network that may be exactly
what you want. It is not what you want if
the port is reachable from further away —
and "further away" includes a router
with the port forwarded, a VPN that
isn't only yours, and a campus or office
network full of strangers' laptops.

The fix is user accounts:

```bash
calibre-server --enable-auth \
  --manage-users /path/to/library
# create at least one user, then run the
# server with --enable-auth
```

Accounts can be limited per library and
made read-only. Treat the content server
like any other thing you publish: a
password before exposure, always. A
related switch, `--enable-local-write`,
lets programs on the same machine (which
includes `calibredb`, and also anything
else that can reach the port locally —
some browsers' idea of "local" is loose)
change the library through the server;
leave it off unless a workflow in the
next section is the reason you came.

## Working on a library through the server

Because the server speaks for the
library, `calibredb` can address the
server instead of the folder:

```bash
calibredb list \
  --with-library http://server:8080/#library
```

with `--username` and `--password` when
authentication is on. This is the
supported way to script against a library
that is in use — the server is the one
writer (chapter 2's rule), and the
clients queue at its door instead of
fighting over the database file. It is
documented behaviour from the manual; the
lab's client and server were the same
machine and it used the folder directly.

## Serving more than books

The server also offers the library's
**catalogues**: browse by author, tag or
series (OPDS clients show these as
shelves), a "recently added" feed, and
full-text search if you have enabled
calibre's full-text indexing in the GUI.
What it never serves is the library
folder's structure — readers see books,
not paths — which is as it should be:
the folder is the database's territory
(chapter 2), and the house's readers
are not the database.
