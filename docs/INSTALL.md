# Installing SUNSITE2 on a plain TI-84 Plus

SUNSITE2 is currently a **development build** for the plain monochrome Texas Instruments TI-84 Plus.

The tested calculator program occupies **7,216 bytes** and runs under the program name `SUNSITE2`.

An installable `.8xp` file has not yet been added to this repository. The current repository therefore provides the human-readable source for inspection and development.

## Important TI-BASIC tokenization note

TI-BASIC source is tokenized, not stored as ordinary text. Pasting source through editors can alter inverse-trigonometric tokens, `π`, `√`, list tokens and whitespace.

In particular, this source intentionally uses a trailing space after every `Pause ` token in the human-readable representation because this avoided tokenization errors during development.

Once a tested `SUNSITE2.8xp` file is published, that file should be the normal installation method.

## Acceptance tests

Before relying on the program, run the historical regression tests in [test-cases.md](test-cases.md).

The current development build has passed Cases A and B on a physical plain TI-84 Plus.
