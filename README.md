# SUNSITE2 for the TI-84 Plus

SUNSITE2 is a Sun-sight reduction program for the **plain monochrome Texas Instruments TI-84 Plus**.

It is an experimental successor to [SUNSIGHT](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus). It retains SUNSIGHT's practical marine sight-reduction workflow, refined Bennett refraction, safeguards and simple interface, but replaces the earlier compact solar ephemeris with a **heavily truncated VSOP87D-based Earth model** optimized specifically for Sun sights.

> **DO NOT USE SUNSITE2 FOR NAVIGATION YET.**
>
> The program is still under development. The historical A–D regression cases pass on a physical TI-84 Plus, but the wider date-range and independent validation work is not complete. Until that testing is finished, use this repository for evaluation and development only.

**Development release: v0.1.0 — 2026-09-17**

The current program occupies **7,216 bytes on the calculator**. The downloadable `SUNSITE2.8xp` file is **7,275 bytes** including TI file-format overhead. On a physical plain TI-84 Plus, execution time is not perceptibly different from SUNSIGHT.

SUNSITE2 is deliberately Sun-only.

## Where SUNSITE2 came from

SUNSITE2 is the third step in a line of small-calculator Sun-sight programs.

### 1. Murdoch's 1996 TI-81 program

William S. **Murdoch's** 1996 *Cruising World* article, “Create Your Own Sun-Sight Reduction Program,” demonstrated that a complete Sun ephemeris and sight-reduction system could be fitted into a TI-81.

Murdoch used low-precision solar formulae derived from the work of **Van Flandern and Pulkkinen**, arranged for practical solar-coordinate calculation by **B. Emerson** of HM Nautical Almanac Office.

His complete program occupied only **2,259 bytes**.

For its size and the calculator available in 1996, it was an extraordinary achievement. The resulting solar positions are much better than the phrase “low precision” might suggest. In the historical test cases the astronomical solution is already quite close to modern reference values.

Its principal merit is elegant economy: a useful self-contained Sun ephemeris and sight reducer in an extraordinarily small program.

### 2. SUNSIGHT

[SUNSIGHT](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus) was an independent modern implementation of the same practical idea for the plain TI-84 Plus.

It replaced Murdoch's older solar model with a compact **Meeus-style** ephemeris and added:

- ΔT handling
- refined Bennett refraction with entered pressure and temperature
- modern semidiameter and parallax treatment
- clearer data entry
- numerical safeguards
- input validation
- warning messages
- extensive comparison with historical cases and USNO data

SUNSIGHT occupies about **6.8 kB** on the calculator.

Its astronomical accuracy is already substantially better than is required for ordinary marine sextant work. In its documented modern USNO validation suite, the largest displayed difference in calculated altitude Hc was about **0.5 minute of arc**, with historical A–D results closer still.

For practical celestial navigation, **SUNSIGHT is already good enough**. A half-minute of arc corresponds to about half a nautical mile in an altitude intercept, and normal real-world errors from the sight itself, the horizon, vessel motion, timing and atmospheric refraction can readily be as large or larger.

### 3. SUNSITE2

SUNSITE2 keeps the successful SUNSIGHT sight-reduction framework but replaces its solar ephemeris with a compact subset of **VSOP87D**.

Full VSOP87D is far too large for a TI-84 Plus, so SUNSITE2 uses a deliberately severe truncation of the Earth heliocentric series:

- a small set of dominant Earth-longitude terms
- no Earth-latitude series at marine-navigation precision
- a minimal Earth–Sun distance model
- shortened coefficients tested for calculator use

This is **not full VSOP87D**. It is a navigation-specific approximation derived from it.

Development testing indicates that the truncated VSOP87D model reduces solar-position error to roughly the **one-tenth-of-an-arcminute class or better** over the present 1900–2049 test interval. That is considerably more accurate than SUNSIGHT's already adequate Meeus implementation.

The important question is therefore not whether SUNSITE2 can calculate the Sun more accurately. It can.

The question is whether that extra accuracy matters aboard a boat.

For most practical sextant work, **probably not**.

The additional astronomical precision is smaller than many ordinary observational and atmospheric errors. SUNSITE2 is therefore best regarded as an experiment in how much accurate modern ephemeris can be fitted into a plain TI-84 Plus without making the program noticeably slower or much larger.

If you want the fuller history, design decisions, validation work and practical reasoning behind this project, read the [SUNSIGHT repository](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus) in detail first. SUNSITE2 deliberately builds on that work rather than repeating all of it here.

## Why VSOP87D?

VSOP stands for **Variations Séculaires des Orbites Planétaires** — literally, *Secular Variations of the Planetary Orbits*. VSOP87 is a modern analytical theory of planetary motion developed by P. Bretagnon and G. Francou. VSOP87D is the version that expresses planetary positions in heliocentric spherical coordinates of date.

For the Sun, SUNSITE2 calculates a truncated heliocentric position of the Earth and then obtains the Sun's geocentric ecliptic longitude by adding 180°.

The full Earth series contains far more terms than a marine navigator needs. SUNSITE2 deliberately keeps only enough to drive navigational error well below practical sextant accuracy.

The result is mathematically excessive for the job, but computationally inexpensive on the TI-84 Plus.

## Current supported range

The program currently accepts **1900 through 2049**.

That range is presently limited more by the ΔT implementation and completed validation than by VSOP87D itself. One purpose of this project is to determine how much farther the existing truncated model can be trusted before additional terms or ΔT branches are required.

The year limits will not be widened merely because the calculator accepts the mathematics. They will be widened only after testing establishes a defensible accuracy range.

## Download and install

Use **[SUNSITE2.8xp](SUNSITE2.8xp)** for installation with TI Connect CE.

The human-readable [SUNSITE2.txt](SUNSITE2.txt) is provided for inspection and documentation, not as the preferred installation method.

See [docs/INSTALL.md](docs/INSTALL.md) for details.

Again: **do not use this development build for navigation until the validation programme is complete.**

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

## Warnings and why they are there

SUNSITE2 retains SUNSIGHT's three practical warnings.

### LOW SUN — apparent altitude below 5°

Refraction becomes rapidly larger and less predictable as altitude falls. The program can calculate a standard correction from the entered pressure and temperature, but the real atmosphere may not behave like the model.

*The American Practical Navigator* (Bowditch) puts the problem plainly:

> “The atmosphere contains many irregularities which are erratic in their influence upon refraction.”

Bowditch notes that temperature inversions, fronts, squalls, differences between sea and air temperature and layered air can all produce abnormal refraction. Near the horizon, even a mathematically excellent ephemeris cannot remove that uncertainty.

**Human-readable citation:** National Geospatial-Intelligence Agency, *The American Practical Navigator (Bowditch)*, Pub. No. 9, 2024 edition, Vol. II, §605, “Astronomical Refraction,” p. 250. Official publication page: https://msi.nga.mil/Publications/APN

The LOW SUN warning therefore means exactly what it says: the result may still be useful, but it deserves less confidence than a sight taken at a healthier altitude.

### SUN NEAR ZENITH — corrected altitude above 87°

As the Sun approaches the zenith, azimuth changes very rapidly with small changes in position and time. The altitude can remain useful, but Zn becomes increasingly sensitive and should be treated cautiously.

The near-zenith warning is a geometric caution rather than a refraction warning. As altitude approaches 90°, azimuth becomes increasingly sensitive to small changes in time, position and measured altitude. This is also reflected in NGA sight-reduction guidance, which requires special interpolation procedures close to the zenith.

### INT >25 NM — large intercept

A large intercept does not necessarily mean the celestial calculation is wrong. It usually means the assumed or DR position is a poor centre from which to plot the line of position, or that an input deserves checking.

SUNSITE2 therefore advises:

`REPLOT BETTER DR`

The purpose is practical: use a more suitable assumed position and check the sight data rather than blindly plotting a very large intercept.

These are **navigation cautions, not calculation-error messages**.

### Bowditch citation — machine-readable form

For citation managers and automated tools, the Bowditch source used above can be represented as BibTeX:

```bibtex
@book{NGA_Bowditch_2024,
  author    = {{National Geospatial-Intelligence Agency}},
  title     = {The American Practical Navigator (Bowditch)},
  year      = {2024},
  volume    = {2},
  number    = {9},
  publisher = {National Geospatial-Intelligence Agency},
  note      = {Section 605, Astronomical Refraction, p. 250},
  url       = {https://msi.nga.mil/Publications/APN}
}
```

The official NGA publication page is preferable to a copied third-party PDF because NGA maintains the digital edition continuously.

## Physical-calculator validation

The current source and `.8xp` build have been run on a **plain monochrome TI-84 Plus**.

Historical regression status:

- **Case A — PASS:** 11.4 NM To, Zn 282.8°, with expected LOW SUN warning
- **Case B — PASS:** 24.0 NM To, Zn 5.8°
- **Case C — PASS:** 13.0 NM To, Zn 89.8°
- **Case D — PASS:** 0.7 NM From, Zn 234.3°

The historical hardware regression set therefore passes **4/4**.

That is encouraging, but four historical cases are not enough to establish a new ephemeris over an extended date range. Wider numerical testing against high-precision reference data is still in progress.

See [docs/test-cases.md](docs/test-cases.md) for the full inputs and validation notes.

## Repository contents

- [SUNSITE2.8xp](SUNSITE2.8xp) — tested TI-84 Plus calculator program for transfer with TI Connect CE
- [SUNSITE2.txt](SUNSITE2.txt) — human-readable TI-BASIC source
- [docs/INSTALL.md](docs/INSTALL.md) — installation notes
- [docs/test-cases.md](docs/test-cases.md) — historical validation cases and current hardware status
- [docs/memory-map.md](docs/memory-map.md) — variable and list allocation
- [docs/sources.md](docs/sources.md) — astronomical and historical sources
- [docs/original-cruising-world-1996/README.md](docs/original-cruising-world-1996/README.md) — citation and authorized link to Murdoch's article
- [CHANGELOG.md](CHANGELOG.md) — development history
- [LICENSE](LICENSE) — MIT License for SUNSITE2 code
- [COPYRIGHT.md](COPYRIGHT.md) — repository copyright scope

## Status

SUNSITE2 is **work in progress**.

Current priorities are:

1. complete a much wider numerical validation of the truncated VSOP87D model
2. test progressively wider historical and future date ranges
3. determine a defensible expanded year range
4. document accuracy against a high-precision reference
5. decide whether the extra precision offers enough practical benefit to justify maintaining SUNSITE2 separately from SUNSIGHT

## Disclaimer

This software is an educational and experimental navigation project, not a substitute for experience, education, judgment or independent means of navigation.

A correct calculation cannot compensate for a bad sight, incorrect UTC, a poor assumed position or incorrect input.

Until the wider validation programme is complete, **SUNSITE2 should not be relied upon for navigation**.
