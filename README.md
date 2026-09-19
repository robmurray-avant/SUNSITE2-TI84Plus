# SUNSITE2 for the TI-84 Plus

SUNSITE2 is an experimental Sun-sight reduction program for the **plain monochrome Texas Instruments TI-84 Plus**.

It is a successor to [SUNSIGHT](https://github.com/robmurray-avant/SUNSIGHT-TI84Plus). It keeps the same practical marine sight-reduction approach but replaces SUNSIGHT's compact solar ephemeris with a **heavily truncated VSOP87D-based Earth model** optimized for Sun sights on a small calculator.

> **DO NOT USE SUNSITE2 FOR NAVIGATION YET.**
>
> The current calculator build passes the historical A-D regression cases on a physical TI-84 Plus and its ephemeris has now been tested numerically across 1900-2049. However, the program still carries several input-validation limitations inherited from the earlier development shell. Those should be corrected and the resulting build re-tested on hardware before SUNSITE2 is treated as an operational navigation program.

**Development build: v0.1.0**

Current tested calculator program:

- on-calculator size: **7,216 bytes**
- `SUNSITE2.8xp` file size: **7,275 bytes**
- SHA-256: **`daad8997b61b4161bc5d6986ece2da19c7bd47b84fc79982fc522673767bdaea`**
- internal calculator program name: **`SUNSITE2`**

The installable `.8xp` file is the physical-calculator-tested build. `SUNSITE2.txt` is a human-readable rendering of that build and is supplied for inspection and documentation, not as the preferred installation method.

SUNSITE2 is deliberately Sun-only.

## Where SUNSITE2 fits after SUNSIGHT v1.1

SUNSITE2 was started before the final SUNSIGHT v1.1 ephemeris work was complete. That matters when comparing the two programs.

SUNSIGHT v1.1 kept its compact Meeus-style architecture and added eight small VSOP87D-derived periodic longitude terms. That reduced the broad 1900-2049 GHA RMS error to about **0.059′**, with a maximum of about **0.196′**.

SUNSITE2 goes farther and replaces the compact solar longitude model with a severe truncation of the VSOP87D Earth series. In the same 27,394-epoch numerical test used for SUNSIGHT v1.1, SUNSITE2 gives about:

| Model | GHA RMS | GHA max | Dec RMS | Dec max |
|---|---:|---:|---:|---:|
| SUNSIGHT v1.0 | 0.201′ | 0.618′ | 0.059′ | 0.227′ |
| **SUNSIGHT v1.1** | **0.059′** | **0.196′** | **0.019′** | **0.073′** |
| **SUNSITE2 v0.1** | **0.030′** | **0.100′** | **0.013′** | **0.040′** |

The broad test evaluates apparent geocentric solar coordinates every two days at 12:00 from 1900-01-01 through 2049-12-31 against Swiss Ephemeris: **27,394 epochs**.

Relative to SUNSIGHT v1.1, the current SUNSITE2 ephemeris reduces:

- GHA RMS error by about **50%**
- maximum GHA error by about **49%**
- declination RMS error by about **34%**
- maximum declination error by about **45%**

The cost is modest. The tested SUNSITE2 build occupies **7,216 bytes** on the calculator versus **6,997 bytes** for SUNSIGHT v1.1: an increase of **219 bytes**, about **3.1%**.

That is a technically interesting result. It is not evidence that a real marine sextant sight will improve by the same amount.

## Accuracy in context

There are two different questions:

1. How accurately does the program calculate the Sun's position?
2. How accurately does a real sight establish a line of position?

Once the ephemeris error is below a few tenths of an arcminute, the observation normally dominates: sextant reading, horizon quality, vessel motion, timing, dip, index error and atmospheric refraction.

A ten-case 2026-2036 comparison against the displayed USNO Celestial Navigation Data gives:

| Model | Mean abs GHA diff | Max abs GHA diff | Mean abs Dec diff | Max abs Dec diff |
|---|---:|---:|---:|---:|
| Murdoch article code | 0.046′ | 0.103′ | 0.022′ | 0.048′ |
| SUNSIGHT v1.1 | 0.044′ | 0.145′ | 0.032′ | 0.063′ |
| **SUNSITE2 v0.1** | **0.038′** | **0.098′** | **0.022′** | **0.042′** |

USNO displays GHA and declination to **0.1′**, so differences of only a few hundredths of an arcminute are at or below the display-resolution floor. The small ten-case set should not be used to claim meaningful superiority between compact algorithms. The broader Swiss Ephemeris test is more useful for distinguishing the models.

The practical conclusion is straightforward: **SUNSIGHT v1.1 is already more than accurate enough for ordinary marine Sun sights. SUNSITE2 makes the ephemeris still better, but most navigators will not be able to exploit that additional precision through a sextant on a moving boat.**

## Why VSOP87D?

VSOP87 is an analytical theory of planetary motion developed by P. Bretagnon and G. Francou. VSOP87D expresses planetary positions in heliocentric spherical coordinates of date.

For a Sun sight, SUNSITE2 calculates a truncated heliocentric longitude of the Earth, adds 180° to obtain the Sun's geocentric ecliptic longitude, and then applies the same compact apparent-longitude, obliquity, right-ascension, declination and sidereal-time framework used by the program.

Full VSOP87D is far too large for this job. SUNSITE2 retains only a small set of dominant Earth-longitude terms, a highly compressed L1/L2 treatment, no Earth-latitude series, and a simple Earth-Sun distance approximation.

This is therefore **not full VSOP87D**. It is a navigation-specific approximation derived from VSOP87D and judged by its measured solar-coordinate performance, not by astronomical completeness.

See [docs/vsop87-truncation.md](docs/vsop87-truncation.md).

## Historical line

### Murdoch, 1996

William S. Murdoch's 1996 *Cruising World* article, “Create Your Own Sun-Sight Reduction Program,” showed that a complete Sun ephemeris and sight-reduction system could be fitted into a TI-81. His eight operational programs occupied **2,259 bytes**, with a separate 128-byte diagnostic program.

Murdoch used compact low-precision planetary formulae derived from Van Flandern and Pulkkinen and arranged for practical solar-coordinate calculation by B. Emerson of HM Nautical Almanac Office.

The result remains impressive. When the reconstructed article code is run against the same modern ten-case USNO set used for SUNSIGHT, its displayed-value differences are in roughly the same small fraction-of-an-arcminute class as the later compact methods.

### SUNSIGHT

SUNSIGHT rebuilt the concept for the plain TI-84 Plus with:

- a modern compact solar ephemeris
- ΔT treatment
- refined Bennett refraction with entered pressure and temperature
- semidiameter and parallax
- clearer data entry
- numerical safeguards
- practical warnings
- hardware and off-calculator validation

Version 1.1 occupies **6,997 bytes** on the calculator and adds eight small longitude terms that materially improve the original v1.0 ephemeris without abandoning its simple structure.

### SUNSITE2

SUNSITE2 asks how far the ephemeris can be pushed while keeping the same sort of plain-calculator program.

The answer so far is: surprisingly far. The current truncated VSOP87D model roughly halves SUNSIGHT v1.1's remaining GHA RMS error for only about 219 additional calculator bytes.

Whether that justifies maintaining a separate operational program is still an open design question.

## Current supported range

The current build accepts **1900 through 2049**.

This is a tested support range, not a claim that the truncated VSOP terms suddenly fail outside it. The range is limited by the current ΔT branches, the validation programme, and the program's deliberate UTC≈UT1 standalone design.

SUNSITE2 accepts UTC and treats it as the practical approximation to UT1. It does **not** require DUT1 as an input. The astronomical comparison tables use the same numerical clock time for SUNSITE2 and the reference calculation so that solar-model differences can be examined separately.

The range should not be widened merely because the calculator can evaluate the formulae.

## Inputs and outputs

SUNSITE2 asks for:

- date and UTC
- assumed latitude and longitude
- sextant altitude Hs
- lower or upper Sun limb
- index error, on or off the arc
- height of eye in metres
- atmospheric pressure in mb/hPa
- temperature in °C

It returns:

- intercept in nautical miles, To or From
- Zn to 0.1°

It also warns for:

- apparent altitude below 5° — `LOW SUN`
- corrected altitude above 87° — `SUN NEAR ZENITH`
- intercept above 25 NM — `REPLOT BETTER DR`

## Current development limitations

The current v0.1 calculator build predates the final SUNSIGHT v1.1 review. Several input-validation issues identified during that review also exist in SUNSITE2 and are planned for the next build.

In particular, the current source should be hardened so that it:

- accepts only exact discrete choices for limb and hemisphere selections
- rejects impossible calendar dates rather than allowing the Julian-date formula to normalize them silently
- validates degrees/minutes components independently
- rejects a combined Hs above 90°
- catches obvious pressure, temperature, eye-height and index-error keying mistakes with broad plausibility checks
- exits without leaving the calculator in `Fix 1`

These are mostly **human-input safeguards**, not ephemeris defects. They are nevertheless important in a program intended for backup navigation.

See [docs/next-build-hardening.md](docs/next-build-hardening.md).

## Physical-calculator validation

The current source and the complete 7,275-byte `.8xp` build have been run on a **plain monochrome TI-84 Plus**.

Historical regression results:

- **Case A — PASS:** 11.4 NM To, Zn 282.8°, with expected LOW SUN warning
- **Case B — PASS:** 24.0 NM To, Zn 5.8°
- **Case C — PASS:** 13.0 NM To, Zn 89.8°
- **Case D — PASS:** 0.7 NM From, Zn 234.3°

See [docs/test-cases.md](docs/test-cases.md).

## Download and install

Use **[SUNSITE2.8xp](SUNSITE2.8xp)** with TI Connect CE.

Before transfer, the file should be:

- **7,275 bytes**
- SHA-256 **`daad8997b61b4161bc5d6986ece2da19c7bd47b84fc79982fc522673767bdaea`**

See [docs/INSTALL.md](docs/INSTALL.md).

## Calculator workspace warning

SUNSITE2 uses calculator letter variables **A-Q** and list **L₁** as working storage. Running the program can overwrite values already stored there.

Back up anything important before using SUNSITE2. A dedicated backup-navigation calculator avoids most of this concern.

The program also sets Degree mode while running.

## Repository contents

- `SUNSITE2.8xp` — physical-calculator-tested TI program
- `SUNSITE2.txt` — human-readable rendering of the tested program
- `SHA256SUMS` — checksum for the installable binary
- `docs/INSTALL.md` — installation and integrity checks
- `docs/test-cases.md` — hardware and numerical validation
- `docs/memory-map.md` — variables and `L₁` allocation
- `docs/sources.md` — calculation references and validation sources
- `docs/vsop87-truncation.md` — retained VSOP terms and model scope
- `docs/next-build-hardening.md` — proposed code changes before an operational release
- `docs/original-cruising-world-1996/` — citation and authorized link for Murdoch's article
- `CHANGELOG.md` — development history
- `LICENSE` — MIT License for SUNSITE2 code
- `COPYRIGHT.md` — repository copyright scope

## Development direction

The next useful milestone is not another ephemeris term. The current astronomical model is already comfortably beyond ordinary sextant requirements.

The priorities are:

1. harden the input shell using lessons from the SUNSIGHT v1.1 review
2. generate a new `.8xp` from that source and test the exact binary on hardware
3. repeat historical A-D and numerical validation
4. decide whether SUNSITE2 remains an experimental research branch or becomes the ephemeris basis for a future SUNSIGHT v2

Until that work is complete, **SUNSIGHT v1.1 remains the mature program and SUNSITE2 remains experimental**.

## Disclaimer

This software is an educational and experimental navigation project, not a substitute for experience, education, judgment or independent means of navigation.

A correct ephemeris cannot compensate for a bad sight, incorrect time, a poor assumed position or incorrect input. Test the software yourself and maintain other independent ways of determining position.
