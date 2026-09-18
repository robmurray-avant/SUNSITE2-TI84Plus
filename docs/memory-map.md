# SUNSITE2 memory map

SUNSITE2 preserves user sight inputs in letter variables and uses `L₁` for calculation storage. The current build ensures `L₁` has at least **76 elements**.

## User-entered letter variables

| Variable | Contents | Units / coding |
|---|---|---|
| `A` | Year | 1900–2049 in current build |
| `B` | Month | 1–12 |
| `C` | Day | 1–31 |
| `D` | UTC hour | 0–23 |
| `E` | UTC minute | 0–59 |
| `F` | UTC second | seconds |
| `G` | Assumed latitude | decimal degrees; N +, S − |
| `H` | Assumed longitude | decimal degrees; E +, W − |
| `I` | Hs degrees | degrees |
| `J` | Hs minutes | arcminutes |
| `K` | Sun limb | 1 lower, 2 upper |
| `L` | Signed index correction | arcminutes; off +, on − |
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
| 5 | Julian Date UTC | JD |
| 6 | Decimal year | year |
| 7 | ΔT polynomial argument | years |
| 8 | ΔT | seconds |
| 9 | Julian Date TT | JD |
| 10 | Julian centuries TT from J2000 | centuries |
| 11 | Julian centuries UT from J2000 | centuries |
| 12 | VSOP87D time argument | Julian millennia from J2000 |
| 13 | Truncated VSOP L0 sum | radians |
| 14 | Truncated VSOP L1 coefficient | radians / millennia |
| 15 | Truncated VSOP L2 coefficient | radians / millennia² |
| 16 | Earth heliocentric longitude | radians |
| 17 | Geocentric solar longitude before normalization | degrees |
| 18 | Geometric solar longitude | degrees, 0–360 |
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
| 29 | Right ascension | degrees, 0–360 |
| 30 | Sun declination | degrees |
| 31 | Earth–Sun distance | AU |
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
| 66 | Signed intercept | NM; + To, − From |
| 67 | Intercept magnitude | NM |
| 68 | Unused | — |
| 69 | Unused in current source | — |
| 70 | Unused in current source | — |
| 71 | Protected sin(Hc) argument | clamped to −1…+1 |
| 72 | Reused annual VSOP argument `6283.07585 t` | radians |
| 73 | VSOP L0 partial sum 1 | radians |
| 74 | VSOP L0 partial sum 2 | radians |
| 75 | VSOP L0 partial sum 3 | radians |
| 76 | VSOP L0 partial sum 4 | radians |

## VSOP87D-specific allocation

The key change from SUNSIGHT is the block `L₁(12)–L₁(18)` plus `L₁(72)–L₁(76)`.

SUNSIGHT used those early list positions for a Meeus-style solar model. SUNSITE2 instead stores the VSOP87D Julian-millennia argument, four L0 partial sums, the retained L1/L2 terms, and the resulting Earth heliocentric longitude.

The four partial sums are stored separately because the full L0 expression is too long for a practical single TI-BASIC source statement. Each stored element has one calculation meaning and is not intentionally reused for unrelated values.

## Sight-reduction chain

`Hs → index correction → dip → refraction → semidiameter → parallax → Ho`

Final plotting values:

- `L₁(49)` — Zn
- `L₁(66)` — signed intercept
- `L₁(67)` — displayed intercept magnitude

This map documents the current 7,216-byte development build and may change as the supported year range is expanded.
