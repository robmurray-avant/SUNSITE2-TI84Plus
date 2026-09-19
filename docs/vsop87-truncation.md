# SUNSITE2 VSOP87D truncation

SUNSITE2 does not implement full VSOP87D. It uses a deliberately severe navigation-specific truncation of the **Earth heliocentric longitude** series and then converts Earth longitude to geocentric solar longitude by adding 180°.

The purpose of this document is to record what the calculator actually evaluates and to make the truncation auditable.

## Time argument

The program uses:

`t = (JD_TT - 2451545) / 365250`

where `t` is Julian millennia from J2000.0.

The frequently reused annual argument is:

`6283.07585 t`

stored in `L₁(72)`.

## Retained L0 terms

The current source forms L0 as four partial sums in `L₁(73)` through `L₁(76)`.

The retained terms, in calculator form, are:

```text
1.7534705
+.0334166 cos(4.669257 + 6283.07585 t)
+.00034894 cos(4.6261 + 12566.1517 t)
+.0000342 cos(2.83 + 3.52 t)
+.000035 cos(2.744 + 5753.38 t)
+.00003136 cos(3.6277 + 77713.77 t)
+.00002676 cos(4.418 + 7860.42 t)
+.00002343 cos(6.135 + 3930.21 t)
+.000012732 cos(2.037 + 529.69 t)
+.000013243 cos(.7425 + 11506.77 t)
+.00000902 cos(2.045 + 26.3 t)
+.00001199 cos(1.11 + 1577.34 t)
+.00000857 cos(3.508 + 398.15 t)
+.0000078 cos(1.179 + 5223.69 t)
+.000009903 cos(5.233 + 5884.93 t)
+.00000753 cos(2.5334 + 5507.55 t)
+.000005053 cos(4.583 + 18849.23 t)
+.000003567 cos(2.92 + .07 t)
+.00000284 cos(1.9 + 796.3 t)
```

These are radians.

## Retained L1 and L2 treatment

The current compact L1 expression is:

```text
6283.3196675 + .0020606 cos(2.67823 + 6283.07585 t)
```

The retained L2 coefficient is:

```text
.0005292
```

Earth heliocentric longitude is then:

`L = L0 + L1 t + L2 t²`

and the Sun's geometric geocentric ecliptic longitude is:

`λ = degrees(L) + 180°`

normalized to 0-360°.

## What is omitted

The current calculator model deliberately omits:

- the overwhelming majority of smaller VSOP87D Earth-longitude terms
- the Earth heliocentric latitude series
- a full VSOP87D Earth-radius series
- planetary coordinates other than the Earth terms needed for the Sun

The program is therefore not intended for general planetary astronomy.

## Earth-Sun distance

The current distance approximation is:

```text
R = 1.00014 + .0167 cos(3.098 + 6283.07585 t)
```

in AU.

This is used only for solar semidiameter and parallax scaling.

The distance approximation is less accurate than the longitude model, but the resulting semidiameter effect is very small. Broad testing over 1900-2049 showed distance errors small enough to contribute only a few thousandths of an arcminute at worst to solar semidiameter, far below normal marine sight uncertainty.

## Apparent longitude

SUNSITE2 then applies the compact apparent-longitude correction already used in the SUNSIGHT architecture:

```text
Ω = 125.04 - 1934.136 T
λapp = λ - .00569 - .00478 sin Ω
```

with the program's compact nutation/obliquity treatment following afterward.

## Why this truncation is useful

The current v0.1 build occupies **7,216 bytes on the calculator**, only **219 bytes** more than SUNSIGHT v1.1.

In the same 27,394-epoch 1900-2049 stress test:

| Model | GHA RMS | GHA max | Dec RMS | Dec max |
|---|---:|---:|---:|---:|
| SUNSIGHT v1.1 | 0.059′ | 0.196′ | 0.019′ | 0.073′ |
| **SUNSITE2 v0.1** | **0.030′** | **0.100′** | **0.013′** | **0.040′** |

Thus the truncation roughly halves SUNSIGHT v1.1's remaining GHA error while retaining essentially the same calculator workflow and execution feel.

## Provenance work still worth adding

Before a stable SUNSITE2 v1.0, this document should ideally be extended with a term-by-term table tying each retained rounded calculator coefficient back to its exact coefficient/index in the public VSOP87D Earth data set.

That would record:

- source series and term index
- full source A, B and C values
- calculator-rounded A, B and C values
- contribution to error when included or removed
- reason for retention

The current numerical validation establishes that the chosen truncation performs well; a term-by-term provenance table would make the design easier to maintain and independently audit.
