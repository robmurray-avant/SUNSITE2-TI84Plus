# Installing SUNSITE2 on a plain TI-84 Plus

SUNSITE2 is currently a **development build** for the plain monochrome Texas Instruments TI-84 Plus.

The tested calculator program occupies **7,216 bytes** on the calculator and runs under the program name `SUNSITE2`.

The repository includes the tested installable file:

**[SUNSITE2.8xp](../SUNSITE2.8xp)**

The `.8xp` file itself is 7,275 bytes because the TI file format adds a small header and wrapper around the 7,216-byte calculator program.

## Installation

1. Install Texas Instruments **TI Connect CE**.
2. Connect the plain TI-84 Plus by USB.
3. Download `SUNSITE2.8xp` from this repository.
4. Transfer the file to the calculator with TI Connect CE.
5. Press `PRGM`, select `SUNSITE2`, and run it.

## Important TI-BASIC tokenization note

TI-BASIC source is tokenized, not stored as ordinary text. Pasting source through editors can alter inverse-trigonometric tokens, `π`, `√`, list tokens and whitespace.

In particular, the human-readable source intentionally shows a trailing space after every `Pause ` because that was required to avoid tokenization problems during development.

For normal installation, use the tested `.8xp` file rather than pasting `SUNSITE2.txt`.

## Acceptance tests

Before relying on the program, run the historical regression tests in [test-cases.md](test-cases.md).

Current physical plain-TI-84-Plus status:

- Case A — PASS
- Case B — PASS
- Case C — awaiting physical recheck
- Case D — PASS
