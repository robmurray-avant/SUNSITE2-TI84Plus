# SUNSITE2 for the TI-84 Plus

SUNSITE2 is a Sun-sight reduction program for the **plain monochrome Texas Instruments TI-84 Plus**.

It is an experimental successor to [SUNSIGHT](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus). It retains SUNSIGHT's practical marine sight-reduction workflow, refined Bennett refraction, safeguards, warnings and simple interface, but replaces the earlier compact solar ephemeris with a **heavily truncated VSOP87D-based Earth model** optimized specifically for Sun sights.

**Development release: v0.1.0 — 2026-09-17**

The current program occupies **7,216 bytes on the calculator**. On a physical plain TI-84 Plus, execution time is not perceptibly different from SUNSIGHT.

SUNSITE2 is deliberately Sun-only.

## Lineage

SUNSITE2 did not appear in isolation.

William S. **Murdoch's** 1996 *Cruising World* article, “Create Your Own Sun-Sight Reduction Program,” demonstrated that a complete Sun ephemeris and sight-reduction system could be fitted into a TI-81. Murdoch's remarkable program occupied only 2,259 bytes and used the Van Flandern–Pulkkinen / Emerson low-precision solar formulation.

[SUNSIGHT](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus) was an independent modern rewrite of that idea for the plain TI-84 Plus. It added a Meeus-style solar ephemeris, ΔT, refined Bennett refraction, clearer input handling, validation and numerical safeguards.

SUNSITE2 is a further experiment: keep the successful SUNSIGHT sight-reduction framework, but replace the solar ephemeris with a compact subset of **VSOP87D**.

Murdoch's original program and article are not included in, or licensed under, this repository's MIT License. Copyright in those materials remains with their respective rights holders.

## Why VSOP87D?

Full VSOP87D is far too large for a TI-84 Plus. SUNSITE2 therefore uses a small, navigation-specific subset of the Earth heliocentric series.

The current model uses:

- a heavily truncated Earth heliocentric longitude series
- only the dominant longitude terms needed for Sun-sight accuracy
- no useful Earth-latitude series, because its contribution is negligible at marine-navigation precision
- a minimal Earth–Sun distance model for semidiameter and parallax
- shortened coefficients selected and tested for calculator use

This is **not full VSOP87D**. It is a purpose-built approximation derived from VSOP87D for Sun-only celestial navigation.

The resulting astronomical precision appears substantially better than is practically necessary for sextant navigation. That is intentional: the extra precision costs little in execution time on the TI-84 Plus.

## Current supported range

The program currently accepts **1900 through 2049**.

That limit is presently imposed mainly by the ΔT implementation and validation range, not by VSOP87D itself. A wider supported date range is planned for testing.

## Inputs

SUNSITE2 asks for:

- date and UTC
- assumed latitude and longitude
- sextant altitude Hs
- lower or upper limb
- index error, on or off the arc
- height of eye in metres
- atmospheric pressure in mb/hPa
- temperature in °C

It returns:

- intercept in nautical miles, To or From
- Zn to 0.1°

Warnings are displayed for:

- apparent altitude below 5°
- Sun near the zenith
- intercept greater than 25 NM

## Physical-calculator validation

The current source has been loaded and run on a **plain monochrome TI-84 Plus**.

Historical regression status:

- **Case A — PASS:** 11.4 NM To, Zn 282.8°, with expected LOW SUN warning
- **Case B — PASS:** 24.0 NM To, Zn 5.8°
- **Case C — awaiting physical recheck**
- **Case D — PASS:** 0.7 NM From, Zn 234.3°

See [docs/test-cases.md](docs/test-cases.md) for the full inputs and validation notes.

## Repository contents

- [SUNSITE2.txt](SUNSITE2.txt) — human-readable TI-BASIC source
- [docs/INSTALL.md](docs/INSTALL.md) — installation notes
- [docs/test-cases.md](docs/test-cases.md) — historical validation cases and current hardware status
- [docs/memory-map.md](docs/memory-map.md) — variable and list allocation
- [docs/sources.md](docs/sources.md) — astronomical and historical sources
- [docs/original-cruising-world-1996/README.md](docs/original-cruising-world-1996/README.md) — citation and authorized link to Murdoch's article
- [CHANGELOG.md](CHANGELOG.md) — development history
- [LICENSE](LICENSE) — MIT License for SUNSITE2 code
- [COPYRIGHT.md](COPYRIGHT.md) — repository copyright scope

An installable `.8xp` file will be added once the current development build is ready to publish as a downloadable calculator program.

## Status

SUNSITE2 is **work in progress**.

The solar model is intentionally more accurate than necessary for normal sextant work. The current priorities are:

1. complete physical-calculator regression testing
2. validate the truncated VSOP87D model over a wider range of dates
3. determine a defensible expanded year range
4. document numerical accuracy against a high-precision reference
5. publish the tested `.8xp` build

## Disclaimer

This software is an educational and backup navigation tool, not a substitute for experience, education, judgment or common sense. A correct calculation cannot compensate for a bad sight, incorrect UTC, a poor assumed position or incorrect input.

Low-altitude Sun sights are especially sensitive to real atmospheric refraction. SUNSITE2 warns the navigator when the apparent altitude is below 5°.

Test the program yourself and retain independent means of navigation.
