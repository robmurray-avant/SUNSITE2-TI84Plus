# Sources and calculation references

## Historical predecessor

William S. **Murdoch**, “Create Your Own Sun-Sight Reduction Program,” *Cruising World*, March 1996, pp. 47–50.

Authorized copy:

https://books.google.ca/books?id=yJv58Lx1rhIC&pg=RA3-PA47

Murdoch's article cites Van Flandern and Pulkkinen, “Low Precision Formulae for Planetary Positions,” *Astrophysical Journal Supplement Series* 41 (1979), and B. Emerson's N.A.O. Technical Note No. 47, *Approximate Solar Coordinates*.

## SUNSIGHT predecessor

SUNSITE2 directly follows the independently developed SUNSIGHT project:

https://github.com/robmurray-avant/SUNSIGHT-TI84Plus

SUNSIGHT established the TI-84 Plus user interface, validation structure, sight-correction chain, ΔT handling, refined Bennett refraction, semidiameter, parallax, numerical protections and warning logic that SUNSITE2 retains.

## VSOP87D

The solar ephemeris in SUNSITE2 is based on a heavily truncated subset of the **VSOP87D Earth heliocentric spherical solution**.

Public coefficient source used during development:

https://github.com/ctdk/vsop87

VSOP87 terms have the form:

`A cos(B + C t)`

with polynomial series in powers of Julian millennia from J2000.0.

SUNSITE2 uses only a very small subset of the complete Earth solution. Terms were selected for Sun-sight accuracy and compact TI-BASIC execution, not astronomical completeness.

The current time argument is:

`t = (JD_TT - 2451545) / 365250`

The Sun's geometric ecliptic longitude is obtained from Earth's heliocentric longitude plus 180°.

## ΔT

Fred Espenak and Jean Meeus, polynomial expressions for ΔT:

https://eclipse.gsfc.nasa.gov/SEcat5/deltatpoly.html

The current program retains the 1900–2049 piecewise ΔT treatment inherited from SUNSIGHT.

## Refraction

G. G. Bennett, “The Calculation of Astronomical Refraction in Marine Navigation,” *Journal of Navigation* 35 (1982).

SUNSITE2 retains SUNSIGHT's refined Bennett apparent-altitude correction with pressure/temperature scaling.

## Independent validation

U.S. Naval Observatory, *Celestial Navigation Data for Assumed Position and Time*:

https://aa.usno.navy.mil/data/celnav

High-precision numerical comparisons during development have also been made against modern astronomical software. Formal validation tables will be added as the wider-range test programme is completed.
