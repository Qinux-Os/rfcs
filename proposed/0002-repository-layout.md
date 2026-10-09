# RFC 0002: One repository per component

- **Status:** Proposed
- **Author:** @q7xk
- **Date:** 2026-01-12
- **Affects:** the whole organization

## Abstract

Each component of Qinux lives in its own repository under the `Qinux-Os`
organization, rather than a single monorepo or a handful of large trees.

## Motivation

There are around fifty components. Grouping them is possible; separating them
lets each be licensed appropriately.

That last point matters more than it first appears. A distribution that ships
GPL-3.0 kernel sources, MIT build tooling, CC0 mirror lists and CC BY wallpapers
cannot express all of that in one repository without choosing a single
license that fits none of them properly.

Separate repositories also mean:

- A user who wants only the CLI tools does not have to reason about the
  installer.
- Permissions and branch protection can differ per component.
- A component can be mirrored or vendored on its own.
- Upstream contributions are a clean single-purpose repository.

## Proposal

The organization holds one repository per component, grouped into eight
areas: base system, packaging, ISO and installer, desktop, visual design,
Qinux tools, infrastructure, and community.

Each repository declares its own license in a `LICENSE` file and a summary in
its description.

## Detailed design

Licensing is assigned per component rather than per project:

| Content | License |
| --- | --- |
| System configuration, installer, desktop integration, Qinux tools | GPL-3.0-only |
| Kernel | GPL-2.0-only, matching upstream |
| Build scripts, CI, release tooling, the website | MIT |
| Package definitions, PKGBUILDs | MIT |
| Mirror lists, release metadata, package indexes, community files | CC0-1.0 |
| Documentation | CC BY 4.0 |
| Wallpapers and brand assets | CC BY 4.0 |
| Fonts | OFL-1.1 |

Infrastructure is permissive because downstream distributors embed it. Data is
CC0 because there is nothing creative about a list of mirrors to protect.
Documentation and artwork need attribution; code that ships inside the system
should stay GPL.

## Alternatives considered

**A monorepo.** Fewer repositories to manage, atomic changes across
components, and one place to search. Rejected because it forces one license on
everything, and because a contributor who wants to fix one thing must clone the
whole distribution.

**A few large repositories** grouped by area, for example one `desktop`
repository instead of six. Rejected as a middle ground that keeps the licensing
problem without keeping the separation benefit.

**One repository with a `LICENSE` per directory.** Attractive, but most tools,
including GitHub's licence detection, do not understand it.

## Drawbacks

- **Cross-component changes need several pull requests.** A change touching
  `desktop` and `kde` cannot merge atomically. Mitigated by keeping such
  changes rare and documenting the order to merge them.
- **Fifty-three repositories is a lot to administer.** Topics, descriptions,
  branch protection and `CODEOWNERS` all need maintaining.
- **Search is fragmented.** Searching the organization returns partial results;
  searching code does not cross repositories.
- **Release coordination is harder.** A change to versioning touches
  `metadata`, `repo` and `release` at once.

## Unresolved questions

- Should the eight groups be reflected in GitHub topics, or in an additional
  set of umbrella repositories?
- Does anything in the packaging area need to be CC0 rather than MIT, for
  consistency with `metadata` and `mirrors`?

## Discussion

Open for comment at the next community call.
