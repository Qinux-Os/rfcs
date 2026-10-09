# RFCs

Request for Comments. An RFC records a design decision **before** the code is
written, so that the reasoning survives and nobody has to reconstruct it from
a mailing list later.

## When an RFC is required

| Change | RFC? |
| --- | --- |
| Typo, comment, spelling fix | No |
| Bug fix with an obvious approach | No |
| New configuration option | Usually |
| New dependency | Yes |
| New architectural component | Yes |
| Changing the package format | Yes |
| Removing or renaming a repository | Yes |
| Anything that will be hard to reverse | Yes |

If you are unsure, write the RFC. It costs an afternoon; reversing a shipped
decision costs a release.

## Process

```text
  draft           proposed           accepted          superseded
    |                 |                  |                 |
    v                 v                  v                 v
proposed/      community call     implementation    a new RFC
                                + roadmap entry     replaces it
```

1. Copy [`0001-template/0001-template.md`](0001-template/0001-template.md).
2. Number it with the next free number and put it in [`proposed/`](proposed/).
3. Open a pull request and tag it `rfc`.
4. Discuss at a community call. Comments happen in the pull request, not in
   private messages.
5. On agreement, move the file to [`accepted/`](accepted/) and update the table
   below.

## RFCs

### Accepted

| Number | Title | Area | Decided |
| --- | --- | --- | --- |
| [0001](accepted/0001-package-format.md) | Package format | Packaging | 2026-01-05 |

### Proposed

| Number | Title | Author | Status |
| --- | --- | --- | --- |
| [0002](proposed/0002-repository-layout.md) | One repository per component | @q7xk | Open |

### Superseded

| Number | Title | Replaced by |
| --- | --- | --- |
| None yet | | |

## Numbering

Numbers are permanent and never reused, including for rejected proposals. A
number identifies a specific argument; if the argument is replaced, the
replacement gets a new number and the old one is marked superseded.

Naming: `NNNN-kebab-case-title.md`.

## Writing a good RFC

The parts reviewers care about most:

- **Motivation.** What problem exists today? Be specific about who has it.
- **Cost.** What does this cost in maintenance, not just in implementation?
- **Alternatives.** What else did you consider, including doing nothing?
- **Drawbacks.** Every design has them. An RFC with no drawbacks is unfinished.

Avoid:

- Explaining the implementation in detail. That is the pull request.
- Describing code that does not exist yet in the present tense.
- "This is obviously the right approach."

## Superseded RFCs

Never delete an accepted RFC. Move it to [`superseded/`](superseded/) and add a
header pointing at the RFC that replaced it. The record of a decision that was
later reversed is more valuable than a clean directory.
