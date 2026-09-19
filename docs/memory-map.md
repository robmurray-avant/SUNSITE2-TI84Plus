# SUNSITE2 memory map

SUNSITE2 preserves the user's sight inputs in letter variables and uses `L₁` for calculation storage. The current tested build ensures that `L₁` has at least **76 elements**.

Running SUNSITE2 can overwrite existing values in **A-Q** and **L₁**. Back up anything important before using the program on a general-purpose calculator.

## User-entered letter variables

| Variable | Contents | Units / coding |
|---|---|---|
| `A` | Year | 1900-2049 in current build |
| `B` | Month | 1-12 |
| `C` | Day | 1-31 in current build; full calendar validation planned |
| `D` | UTC hour | 0-23 |
| `E` | UTC minute | 0-59 |
| `F` | UTC second | seconds |
| `G` | Assumed latitude | decimal degrees; N +, S - |
| `H` | Assumed longitude | decimal degrees; E +, W - |
| `I` | Hs degrees | degrees |
| `J` | Hs minutes | arcminutes |
| `K` | Sun limb | 1 lower, 2 upper |
| `L` | Signed index correction | arcminutes; off +, on - |
| `M` | Height of eye | metres |
| `N` | Pressure | mb / hPa |
| `O` | Temperature | °C |
| `P` | Menu / temporary scratch | varies |
| `Q` | Position-display scratch | varies |

## List `L₁`

| Element | Contents | Units / notes |
|---:|---|---|
| 1 | Adjusted year for JD | year |
| 2 | Adjusted month for JD | month |
| 3 | Gregorian century term | integer |
| 4 | Gregorian calendar correction | days |
| 5 | Julian Date from entered UTC | JD; used as practical UT1 approximation |
| 6 | Decimal year | year |
| 7 | ΔT polynomial argument | years |
| 8 | ΔT | seconds; formally TT-UT1 |
| 9 | Approximate Julian Date TT | `JD_UTC + ΔT/86400` under UTC≈UT1 design |
| 10 | Julian centuries TT from J2000 | centuries |
| 11 | Julian centuries from entered UTC/UT approximation | centuries |
| 12 | VSOP87D time argument | Julian millennia from J2000 |
| 13 | Truncated VSOP L0 sum | radians |
| 14 | Truncated VSOP L1 coefficient | radians / millennia |
| 15 | Truncated VSOP L2 coefficient | radians / millennia² |
| 16 | Earth heliocentric longitude | radians |
| 17 | Geocentric solar longitude before normalization | degrees |
| 18 | Geometric solar longitude | degrees, 0-360 |
| 19 | Ω node-angle term | degrees |
| 20 | Apparent solar longitude | degrees |
| 21 | Mean solar longitude term for nutation | degrees |
| 22 | Normalized mean solar longitude | degrees |
| 23 | Mean obliquity | degrees |
| 24 | Corrected obliquity | degrees |
| 25 | RA numerator | dimensionless |
| 26 | RA denominator | dimensionless |
| 27 | Preliminary right ascension | degrees |
| 28 | Quadrant-corrected RA | degrees |
| 29 | Right ascension | degrees, 0-360 |
| 30 | Sun declination | degrees |
| 31 | Earth-Sun distance | AU |
| 32 | Approximate lunar mean longitude | degrees |
| 33 | Nutation in longitude | degrees |
| 34 | GMST raw | degrees |
| 35 | GMST normalized | degrees |
| 36 | GAST raw | degrees |
| 37 | GAST normalized | degrees |
| 38 | GHA raw | degrees |
| 39 | Sun GHA | degrees |
| 40 | LHA raw | degrees |
| 41 | LHA | degrees |
| 42 | Raw sin(Hc) | dimensionless |
| 43 | Calculated altitude Hc | degrees |
| 44 | Azimuth numerator | dimensionless |
| 45 | Azimuth denominator | dimensionless |
| 46 | Preliminary azimuth | degrees |
| 47 | Quadrant-corrected azimuth | degrees |
| 48 | Navigational azimuth raw | degrees |
| 49 | Zn | degrees |
| 50 | Hs | degrees |
| 51 | Index correction | degrees |
| 52 | Dip | degrees |
| 53 | Ha after index correction and dip | degrees |
| 54 | Bennett base refraction | arcminutes |
| 55 | Bennett refinement term | arcminutes |
| 56 | Refined standard refraction | arcminutes |
| 57 | Pressure / temperature factor | dimensionless |
| 58 | Actual refraction | arcminutes |
| 59 | Actual refraction | degrees |
| 60 | Altitude after refraction | degrees |
| 61 | Solar semidiameter | degrees |
| 62 | Signed semidiameter | degrees |
| 63 | Altitude after semidiameter | degrees |
| 64 | Parallax in altitude | degrees |
| 65 | Corrected observed altitude Ho | degrees |
| 66 | Signed intercept | NM; + To, - From |
| 67 | Intercept magnitude | NM |
| 68 | Unused | - |
| 69 | Unused | - |
| 70 | Unused | - |
| 71 | Protected sin(Hc) argument | clamped to -1…+1 |
| 72 | Reused annual VSOP argument `6283.07585 t` | radians |
| 73 | VSOP L0 partial sum 1 | radians |
| 74 | VSOP L0 partial sum 2 | radians |
| 75 | VSOP L0 partial sum 3 | radians |
| 76 | VSOP L0 partial sum 4 | radians |

## VSOP87D-specific allocation

The key SUNSITE2 change is the ephemeris block using `L₁(12)-L₁(18)` and `L₁(72)-L₁(76)`.

The four L0 partial sums are stored separately because a single expression is impractical to enter and maintain on the TI-84 Plus. Each list element has one intended calculation meaning and is not deliberately reused for unrelated data.

See [`vsop87-truncation.md`](vsop87-truncation.md) for the retained coefficient set.

## Sight-reduction chain

`Hs -> index correction -> dip -> refraction -> semidiameter -> parallax -> Ho`

Final plotting values:

- `L₁(49)` — Zn
- `L₁(66)` — signed intercept
- `L₁(67)` — displayed intercept magnitude

## Current-build note

This map describes the **7,216-byte v0.1 development build** whose installable `.8xp` is 7,275 bytes with SHA-256:

`daad8997b61b4161bc5d6986ece2da19c7bd47b84fc79982fc522673767bdaea`

Proposed validation/interface changes for the next build are documented separately so this memory map remains tied to the tested binary.
