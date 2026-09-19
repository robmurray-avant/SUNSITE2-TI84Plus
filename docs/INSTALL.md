# Installing SUNSITE2 on a plain TI-84 Plus

SUNSITE2 is currently a **development build** for the plain monochrome Texas Instruments TI-84 Plus.

The physical-calculator-tested program occupies **7,216 bytes** on the calculator and runs under the program name `SUNSITE2`.

The installable repository file is:

**[SUNSITE2.8xp](../SUNSITE2.8xp)**

Expected file properties:

- file size: **7,275 bytes**
- SHA-256: **`daad8997b61b4161bc5d6986ece2da19c7bd47b84fc79982fc522673767bdaea`**
- internal program name: **`SUNSITE2`**

## Before installation

SUNSITE2 uses calculator variables **A-Q** and list **L₁** as working storage. Running the program can overwrite values already stored there.

Back up anything important first.

The program also places the calculator in Degree mode while running.

## Installation

1. Install Texas Instruments **TI Connect CE**.
2. Connect the plain TI-84 Plus by USB.
3. Download `SUNSITE2.8xp` from this repository.
4. Confirm that the downloaded file is **7,275 bytes**. If you use a checksum tool, confirm the SHA-256 above.
5. Transfer the file to the calculator with TI Connect CE.
6. Press `PRGM`, select `SUNSITE2`, and run it.

If TI Connect CE reports that the file is corrupt, do not rename, re-save or reconstruct the binary. Download the repository copy again and check its size/checksum.

## Human-readable source

`SUNSITE2.txt` is supplied for inspection and documentation. TI-BASIC is tokenized, so ordinary text editors are not a reliable way to reconstruct an installable `.8xp` file.

In particular, inverse trigonometric functions, `π`, `√`, list tokens and whitespace can be altered by text handling.

For normal installation, use the tested `.8xp` file.

## Acceptance tests

After installation, run the historical regression cases in [test-cases.md](test-cases.md).

Current physical plain-TI-84-Plus results:

- Case A — **PASS:** 11.4 To, Zn 282.8°, LOW SUN warning
- Case B — **PASS:** 24.0 To, Zn 5.8°
- Case C — **PASS:** 13.0 To, Zn 89.8°
- Case D — **PASS:** 0.7 From, Zn 234.3°

All four have been confirmed on hardware with the current development build.

## Development warning

SUNSITE2 is still experimental. Its ephemeris has been validated broadly, but the current v0.1 input shell still has several validation weaknesses documented in [next-build-hardening.md](next-build-hardening.md).

For the mature operational version of this project, use the released SUNSIGHT v1.1 program until SUNSITE2's next build has completed the same hardware and validation cycle.
