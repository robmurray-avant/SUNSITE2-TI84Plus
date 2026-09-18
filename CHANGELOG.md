# Changelog

## v0.1.0 — 2026-09-17

Initial development repository for SUNSITE2.

- Program name: `SUNSITE2`.
- Target: plain monochrome TI-84 Plus.
- Calculator size: **7,216 bytes**.
- Installable TI file: **`SUNSITE2.8xp`**, 7,275 bytes including file-format overhead.
- Current supported range: **1900–2049**.
- Replaces SUNSIGHT's compact solar ephemeris with a heavily truncated VSOP87D-based Earth model.
- Retains SUNSIGHT's sight-reduction sequence, refined Bennett refraction, semidiameter, parallax, warnings and user interface.
- Physical-calculator execution time is not perceptibly different from SUNSIGHT.
- Physical TI-84 Plus testing:
  - Case A passes: **11.4 To, Zn 282.8°**, with expected LOW SUN warning.
  - Case B passes: **24.0 To, Zn 5.8°**.
  - Case C passes: **13.0 To, Zn 89.8°**.
  - Case D passes: **0.7 From, Zn 234.3°**.
  - Historical hardware regression: **4/4 cases pass**.
- Wider date-range testing is planned before the year limits are expanded.
