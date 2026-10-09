# RFC 0000: Title of the proposal

- **Status:** Draft
- **Author:** @username
- **Date:** YYYY-MM-DD
- **Affects:** milestone or repository list

## Abstract

Two or three sentences. What is being proposed, in terms a user of the
distribution would understand. No jargon that the project has not defined.

## Motivation

What problem exists today. Be concrete about who is affected and what it costs
them. "The current approach does not scale" is not concrete; "adding a
dependency takes three weeks of work in two repositories" is.

If this solves a problem someone reported, link the issue.

## Proposal

What should change. The level of detail should be enough that a reader could
estimate the work, and no more.

Describe the shape of the solution, not its implementation.

## Detailed design

Only if the proposal needs it. Cover:

- The interfaces involved: what other components call, and what they must
  provide.
- Data formats, with an example.
- Failure modes: what happens when something goes wrong.
- Migration: what happens to existing installations and packages.

This section is the one reviewers will scrutinise most.

## Alternatives considered

What else could be done, including **doing nothing**. For each, say why it was
rejected. "Doing nothing" is a real option and deserves a real argument.

## Drawbacks

Every design has costs. Be specific about them.

This is the section most often left out, and it is the one that makes an RFC
worth reading. If you cannot find a drawback, the proposal is probably too
narrow or the thinking is not finished.

## Unresolved questions

What still needs deciding. This is a normal section; an RFC with none is
usually overconfident.

## Implementation

Filled in **after** acceptance, linking the pull requests that implement it.

## Changelog

- YYYY-MM-DD: Draft created.
