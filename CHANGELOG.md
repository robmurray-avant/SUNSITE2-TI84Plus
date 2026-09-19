# Changelog

## Unreleased — documentation and validation refresh

This proposed update does **not** change the v0.1 calculator algorithm.

- Restores and identifies the complete physical-calculator-tested `SUNSITE2.8xp`:
  - calculator size: **7,216 bytes**
  - `.8xp` file size: **7,275 bytes**
  - SHA-256: **`daad8997b61b4161bc5d6986ece2da19c7bd47b84fc79982fc522673767bdaea`**
- Updates SUNSITE2's comparison baseline from the earlier SUNSIGHT build to **SUNSIGHT v1.1**.
- Adds the same ten-case 2026-2036 USNO ephemeris comparison used in SUNSIGHT v1.1 documentation.
- Records SUNSITE2 ten-case displayed-USNO differences:
  - GHA mean absolute difference **0.038′**, maximum **0.098′**
  - declination mean absolute difference **0.022′**, maximum **0.042′**
- Adds a broad 1900-2049 stress test against Swiss Ephemeris at 27,394 epochs:
  - GHA RMS **0.02955′**, maximum **0.10003′**
  - declination RMS **0.01291′**, maximum **0.04034′**
- Documents the direct broad-test comparison with SUNSIGHT v1.1:
  - SUNSIGHT v1.1 GHA RMS **0.059′**, maximum **0.196′**
  - SUNSITE2 v0.1 GHA RMS **0.030′**, maximum **0.100′**
- Clarifies that the current SUNSITE2 build uses only **219 more calculator bytes** than SUNSIGHT v1.1.
- Corrects installation documentation so Case C is recorded as a physical hardware PASS; all historical cases are **4/4 PASS**.
- Adds binary checksum and calculator-workspace warnings to installation documentation.
- Adds explicit UTC≈UT1 wording consistent with SUNSIGHT v1.1 documentation.
- Adds `docs/vsop87-truncation.md` to document the retained compact coefficient set and model scope.
- Adds `docs/next-build-hardening.md` to separate proposed input-validation/interface work, from the current tested binary.
- Documents known v0.1 validation weaknesses rather than implying the current input shell is release-ready.

## v0.1.0 — 2026-09-17

Initial SUNSITE2 development build.

- Program name: `SUNSITE2`.
- Target: plain monochrome TI-84 Plus.
- Calculator size: **7,216 bytes**.
- Installable TI file: **`SUNSITE2.8xp`**, 7,275 bytes including file-format overhead.
- Supported/tested date interval: **1900-2049**.
- Replaces the earlier SUNSIGHT compact solar ephemeris with a heavily truncated VSOP87D-based Earth model.
- Retains the SUNSIGHT sight-reduction sequence, Bennett refraction, semidiameter, parallax, warnings and user-interface structure.
- Physical TI-84 Plus historical testing:
  - Case A: **11.4 To, Zn 282.8°**, expected LOW SUN warning
  - Case B: **24.0 To, Zn 5.8°**
  - Case C: **13.0 To, Zn 89.8°**
  - Case D: **0.7 From, Zn 234.3°**
  - hardware regression: **4/4 PASS**
