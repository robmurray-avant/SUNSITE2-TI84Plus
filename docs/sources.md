# Sources and calculation references

## Historical predecessor

William S. **Murdoch**, “Create Your Own Sun-Sight Reduction Program,” *Cruising World*, March 1996, pp. 47-50.

Authorized online copy:

https://books.google.ca/books?id=yJv58Lx1rhIC&pg=RA3-PA47

Murdoch's article cites:

- Van Flandern and Pulkkinen, “Low Precision Formulae for Planetary Positions,” *The Astrophysical Journal Supplement Series* 41 (1979)
- B. Emerson, N.A.O. Technical Note No. 47, *Approximate Solar Coordinates*, HM Nautical Almanac Office, 1978
- Montenbruck and Pfleger, *Astronomy on the Personal Computer*, Springer-Verlag, 1991

Murdoch's eight operational TI-81 programs total **2,259 bytes** in the published listing. His separate 128-byte `ALLOUT` diagnostic program brings all nine listings to 2,387 bytes.

## SUNSIGHT predecessor

SUNSITE2 follows the independently developed SUNSIGHT project:

https://github.com/robmurray-avant/SUNSIGHT-TI84Plus

SUNSIGHT established the TI-84 Plus interface, sight-correction chain, ΔT treatment, Bennett refraction, semidiameter, parallax, numerical protections and warning logic that SUNSITE2 retains.

The relevant comparison baseline is now **SUNSIGHT v1.1**, not the original v1.0 ephemeris.

SUNSIGHT v1.1 occupies **6,997 bytes on the calculator** and **7,056 bytes as an `.8xp` file**. It retains the compact Meeus-style architecture and adds eight small VSOP87D-derived periodic longitude terms.

In the 27,394-epoch 1900-2049 stress test, SUNSIGHT v1.1 gives approximately **0.059′ GHA RMS / 0.196′ maximum** and **0.019′ declination RMS / 0.073′ maximum**.

## VSOP87 / VSOP87D

P. Bretagnon and G. Francou, “Planetary theories in rectangular and spherical variables. VSOP87 solutions,” *Astronomy and Astrophysics* 202 (1988), 309-315.

ADS entry:

https://ui.adsabs.harvard.edu/abs/1988A&A...202..309B/abstract

SUNSITE2 uses a **heavily truncated subset** of the VSOP87D Earth heliocentric spherical solution.

Public coefficient implementation used during development:

https://github.com/ctdk/vsop87

VSOP87 terms take the form:

`A cos(B + C t)`

within polynomial series in powers of Julian millennia from J2000.0.

SUNSITE2's current time argument is:

`t = (JD_TT - 2451545) / 365250`

where the program forms approximate TT from its entered UTC clock plus ΔT under its deliberate UTC≈UT1 standalone assumption.

The Sun's geometric ecliptic longitude is obtained from Earth's heliocentric longitude plus 180°.

SUNSITE2 does **not** implement complete VSOP87D. It keeps only a small navigation-specific set of Earth-longitude terms, omits the Earth-latitude series at the required marine precision, and uses a compact distance approximation.

See [`vsop87-truncation.md`](vsop87-truncation.md) for the terms actually retained in the calculator source.

## ΔT and time scales

Fred Espenak and Jean Meeus, polynomial expressions for ΔT:

https://eclipse.gsfc.nasa.gov/SEcat5/deltatpoly.html

The current program retains the 1900-2049 piecewise ΔT treatment inherited from SUNSIGHT.

ΔT is formally **TT - UT1**. SUNSITE2 accepts a UTC clock and uses it as the practical approximation to UT1; it does not require a DUT1 input. That is a deliberate standalone-navigation design choice rather than a claim that UTC and UT1 are identical.

For the small USNO comparison, the same numerical date and clock time are used as USNO UT1 and SUNSITE2 UTC so the solar-model difference can be examined separately.

## Apparent solar coordinates and sidereal time

After forming the truncated geometric solar longitude, SUNSITE2 applies compact apparent-longitude, nutation, obliquity, right-ascension and declination steps consistent with the existing SUNSIGHT architecture.

Greenwich apparent sidereal time is formed from the program's UT/UTC Julian date plus the compact nutation correction, and Sun GHA follows from GAST minus apparent right ascension.

## Refraction

G. G. Bennett, “The Calculation of Astronomical Refraction in Marine Navigation,” *Journal of Navigation* 35 (1982).

SUNSITE2 retains SUNSIGHT's refined Bennett apparent-altitude correction with pressure/temperature scaling.

The current source computes the main Bennett term, applies Bennett's small refinement term, then scales for entered pressure and temperature.

## Semidiameter and parallax

The program scales mean solar semidiameter with the compact Earth-Sun distance estimate and applies solar horizontal parallax in altitude.

The current compact distance expression is less accurate than the solar longitude model, but its resulting semidiameter error is tiny compared with normal sextant uncertainty and does not materially limit the program.

## U.S. Naval Observatory validation

U.S. Naval Observatory, *Celestial Navigation Data for Assumed Position and Time*:

https://aa.usno.navy.mil/data/celnav

The service provides GHA, declination, Hc, Zn and standard altitude-correction data for a specified assumed position and time.

USNO's public display gives GHA and declination to **0.1′**, which limits the significance of comparisons at the hundredth-of-an-arcminute level.

SUNSITE2 uses the same ten 2026-2036 ephemeris cases documented for SUNSIGHT v1.1. Results are in [`test-cases.md`](test-cases.md).

## Swiss Ephemeris broad validation

Swiss Ephemeris:

https://www.astro.com/swisseph/

SUNSITE2 was compared with Swiss Ephemeris apparent geocentric solar coordinates every two days at 12:00 from 1900 through 2049: **27,394 epochs**.

The reproduced results for the current v0.1 source are approximately:

- GHA RMS **0.02955′**
- maximum GHA error **0.10003′**
- declination RMS **0.01291′**
- maximum declination error **0.04034′**

The comparison was reproduced with Swiss Ephemeris / `pyswisseph` 2.10.03.

Swiss Ephemeris is used as a high-precision numerical reference, **not as a substitute name for USNO or the Nautical Almanac**.

## Navigational context

National Geospatial-Intelligence Agency, *The American Practical Navigator (Bowditch)*, Pub. No. 9:

https://msi.nga.mil/Publications/APN

Bowditch is used for the practical treatment of astronomical refraction, high-altitude/near-zenith sights and line-of-position geometry.
