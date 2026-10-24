# Installing Calibre

Calibre installs like any other program
on Windows and Mac, and in one specific
way on Linux, where the obvious route is
the wrong one. This chapter gives the
official paths first, then describes the
headless install this guide's lab
performed — including the two places it
had to step off the documented path, and
why.

## Windows and macOS

Download the installer from
[calibre-ebook.com](https://calibre-ebook.com/download)
and run it. That is the whole recipe; the
project publishes one build per platform
and updates it often (calibre releases
roughly weekly). There is also a portable
Windows build that runs from a folder or
USB stick without installing, useful for
trying calibre on a machine you don't
control.

## Linux: the project's installer, not your distro's

Most Linux distributions package calibre,
and the project asks you not to use those
packages: they lag versions behind and
are a recurring source of bugs the
upstream cannot reproduce. The documented
route is the project's own installer,
which needs no more than:

```bash
sudo -v
wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh \
  | sudo sh /dev/stdin
```

It installs a self-contained build into
`/opt/calibre` and links the commands
(`calibre`, `calibredb`, `ebook-convert`,
and the rest) into `/usr/bin`. On a
machine without a desktop — a home
server, say — a few system libraries are
needed even for the command-line tools,
because they load the same Qt libraries
the GUI uses. The installer names what is
missing; on Ubuntu the usual set is:

```bash
sudo apt install libegl1 libopengl0 libxcb-cursor0
```

Check: after installing, on any platform,

```bash
calibre --version
calibredb --version
ebook-convert --version
```

should each answer with the version —
`calibre (calibre 9.17)` in the lab.

## The lab's install, and its declared deviations

The lab machine was a headless Ubuntu
24.04 box with no display and an unusual
network: all web traffic left through a
proxy whose address contains credentials.
Two deviations resulted, neither hidden:

1. **The tarball was fetched by hand.**
   The installer's first step downloads a
   signature file from
   `code.calibre-ebook.com` using a small
   HTTPS helper of calibre's own. That
   helper parses proxy addresses by hand
   and cannot cope with one containing
   credentials — it failed with a DNS
   error about a name that was really the
   proxy string — and the signature host
   itself returned empty replies through
   the lab's network. So the lab did the
   installer's remaining steps manually:
   it downloaded the very file the
   installer fetches (the redirect from
   `calibre-ebook.com/dist/linux-x86_64`
   to the project's GitHub release of
   **v9.17.0**), unpacked it into
   `/opt/calibre`, and ran
   `calibre_postinstall`. The one step not
   reproduced is the installer's SHA-512
   signature check, which needs the
   unreachable host; the download itself
   came over HTTPS from the project's own
   release page. On a normal home network
   none of this applies — run the
   installer. (Chapter 14 keeps the proxy
   lesson, because corporate networks have
   credentialed proxies too.)
2. **Everything ran with
   `QT_QPA_PLATFORM=offscreen`.** With no
   display, Qt's tools need telling not to
   look for one. With that variable set,
   `calibredb`, `ebook-convert` and
   `calibre-server` all ran normally. The
   GUI itself was never started — there
   was nothing to start it on — so
   everything this guide says about the
   windows is documented-only, and the
   chapters say so where it matters.

Measured sizes, for planning: the 9.17.0
Linux tarball was 201.6 MB to download
and 654 MB unpacked in `/opt/calibre`.

## Keeping it current

Calibre updates itself in the GUI (it
tells you when a new version exists);
Linux installs repeat the installer
command, which replaces the build in
place and leaves every library exactly
where it was. Libraries are never stored
inside the program's folders — yours live
where you put them (chapter 4), which is
what makes upgrades boring, as they
should be.
