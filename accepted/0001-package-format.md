# RFC 0001: Use pacman's package format

- **Status:** Accepted
- **Author:** @q7xk
- **Date:** 2026-01-05
- **Affects:** packages, pkgbuilds, repo, package-manager, package-index
- **Decided at:** Community call, 2026-01-05

## Abstract

Qinux uses pacman's package format and its package database. Packages are built
with `makepkg` from PKGBUILD files and installed with `pacman` against a
pacman-style repository.

## Motivation

Building a package format from scratch is a large amount of work that adds
nothing to the distribution itself. Contributors already know PKGBUILD, and
Arch's tooling is mature, permissive and well documented.

The alternative distributions that start from scratch spend their first years
building tooling. Qinux would rather spend that time on the desktop.

## Proposal

Adopt pacman's format unmodified:

- Packages are `.pkg.tar.zst` archives with a `.PKGINFO` metadata file.
- The database is a set of SQLite files under `/var/lib/pacman/`.
- Repositories are served over HTTP as a directory of package files plus
  `repo.db.tar.zst`.
- `pacman -Syu` updates the whole system.

The database schema, archive layout and repository layout are Arch's, with no
Qinux-specific extensions.

## Detailed design

The package manager in [`package-manager`](https://github.com/Qinux-Os/package-manager)
is pacman plus Qinux defaults and hooks. It is not a fork.

Repository infrastructure lives in [`repo`](https://github.com/Qinux-Os/repo).
PKGBUILDs live in [`pkgbuilds`](https://github.com/Qinux-Os/pkgbuilds).

Signatures use pacman's standard detached GPG signatures, not an alternative
scheme.

## Alternatives considered

**Debian's `.deb`.** Mature, but the format and the toolchain are tightly
coupled, and adapting it to a modular distribution would mean forking
`dpkg`. Rejected: too much divergence for too little gain.

**A new format designed for modularity.** Tempting, because the format could
encode component dependencies natively. Rejected: it would have to be
maintained, documented and taught from scratch, and the one benefit does not
justify it. Component dependencies can be expressed with package groups
instead.

**Arch Linux packages unchanged.** Rejected: Qinux needs its own package set
and defaults. It is a distribution, not a rebuild of an existing one.

## Drawbacks

- **Ties Qinux to pacman's release cadence.** A pacman major version bump may
  require work in Qinux. Accepted, because the format is stable and Arch has
  kept it stable for years.
- **No native notion of a component.** A user cannot "remove the KDE
  component" as one operation; they remove a package group. Manageable, and
  the package manager can offer it as a convenience.
- **Inheriting Arch's packaging conventions.** Some conventions may not suit
  Qinux. They can be overridden in PKGBUILDs, at the cost of divergence from
  upstream documentation.

## Unresolved questions

- Does Qinux ship its own package groups, or reuse Arch's?
  Settled later: Qinux ships its own, defined in `packages`.
- Which mirrors are in the default configuration? See
  [`mirrors`](https://github.com/Qinux-Os/mirrors).

## Implementation

- [`pkgbuilds`](https://github.com/Qinux-Os/pkgbuilds) holds the PKGBUILDs.
- [`repo`](https://github.com/Qinux-Os/repo) holds the repository infrastructure.
- [`package-manager`](https://github.com/Qinux-Os/package-manager) configures
  pacman and adds hooks.
