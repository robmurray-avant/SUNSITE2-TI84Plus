# SUNSITE2 validation

SUNSITE2 is checked at three levels:

1. complete historical sight reductions on physical TI-84 Plus hardware
2. a small modern comparison against displayed U.S. Naval Observatory data
3. a broad 1900-2049 numerical comparison against Swiss Ephemeris

The three tests answer different questions. The hardware cases test the complete program path. The USNO set gives an authoritative navigational cross-check but is limited by the public display precision. The Swiss test is used to characterize the ephemeris numerically over the full supported date interval.

## Historical Cases A-D — physical TI-84 Plus

These four cases originate in William S. Murdoch's 1996 TI-81 article and were also used during SUNSIGHT development.

| Case | Date / UTC | Position | Hs / limb | IE | Eye | P / T | SUNSITE2 result | Status |
|---|---|---|---|---|---:|---|---|---|
| A | 1950-04-08 18:43:28 | N 62°28.2′ E 000°18.8′ | 1°38.2′ lower | 10.2′ off | 2.2 m | 1050 mb / 2°C | **11.4 To, Zn 282.8°** | **PASS** |
| B | 1972-06-23 00:17:52 | S 16°23.0′ E 172°00.0′ | 50°01.2′ lower | 10.2′ off | 3.4 m | 1010 mb / 10°C | **24.0 To, Zn 5.8°** | **PASS** |
| C | 1992-03-18 22:00:00 | S 00°38.1′ W 162°18.9′ | 76°24.8′ upper | 8.2′ on | 6.2 m | 970 mb / 40°C | **13.0 To, Zn 89.8°** | **PASS** |
| D | 1994-11-28 01:10:14 | N 18°17.2′ W 148°58.8′ | 25°40.7′ lower | 2.5′ on | 4.35 m | 1030 mb / 34°C | **0.7 From, Zn 234.3°** | **PASS** |

Case A also gives the expected:

`LOW SUN / USE WITH CAUTION`

Representative current internal values:

| Case | GHA | Declination | Hc |
|---|---:|---:|---:|
| A | about 100°23.087′ | N 7°12.012′ | 1°29.456′ |
| B | about 183°57.211′ | N 23°26.035′ | 49°59.209′ |
| C | about 148°01.819′ | S 0°34.371′ | 75°42.959′ |
| D | about 200°37.025′ | S 21°13.881′ | 25°49.682′ |

The historical regression set therefore passes **4/4 on physical hardware**.

## Ten-case 2026-2036 USNO ephemeris comparison

These cases are ephemeris tests rather than normal sight-entry tests. The exact SUNSITE2 formulas are evaluated off-calculator and compared with the displayed GHA and declination from the U.S. Naval Observatory Celestial Navigation Data service.

USNO displays GHA and declination to **0.1′**. Differences of a few hundredths of an arcminute therefore sit at or below the resolution of the displayed reference and should not be over-interpreted.

USNO's service takes UT1. SUNSITE2 accepts UTC and deliberately treats it as the practical approximation to UT1. For this model comparison, the same numerical date and clock time are used on both sides.

| Case | Date / time | USNO GHA | SUNSITE2 GHA | abs diff | USNO Dec | SUNSITE2 Dec | abs diff |
|---|---|---:|---:|---:|---:|---:|---:|
| 1 | 2026-02-15 15:46:17 | 53°03.3′ | 53°03.300′ | 0.000′ | S 12°31.4′ | S 12°31.376′ | 0.024′ |
| 2 | 2027-06-21 02:32:42 | 217°45.3′ | 217°45.307′ | 0.007′ | N 23°26.2′ | N 23°26.201′ | 0.001′ |
| 3 | 2028-10-05 13:02:05 | 18°27.7′ | 18°27.721′ | 0.021′ | S 5°03.7′ | S 5°03.737′ | 0.037′ |
| 4 | 2029-12-21 16:05:33 | 61°49.0′ | 61°48.972′ | 0.028′ | S 23°26.1′ | S 23°26.110′ | 0.010′ |
| 5 | 2030-12-01 12:44:51 | 13°57.2′ | 13°57.245′ | 0.045′ | S 21°51.0′ | S 21°51.002′ | 0.002′ |
| 6 | 2031-07-10 23:02:09 | 164°10.4′ | 164°10.434′ | 0.034′ | N 22°09.4′ | N 22°09.358′ | 0.042′ |
| 7 | 2032-09-22 11:30:27 | 354°29.2′ | 354°29.157′ | 0.043′ | S 0°00.3′ | S 0°00.319′ | 0.019′ |
| 8 | 2033-01-15 05:29:44 | 260°05.1′ | 260°05.198′ | 0.098′ | S 21°03.5′ | S 21°03.462′ | 0.038′ |
| 9 | 2034-05-20 03:07:12 | 227°39.7′ | 227°39.748′ | 0.048′ | N 19°58.4′ | N 19°58.440′ | 0.040′ |
| 10 | 2036-11-05 12:34:36 | 12°45.1′ | 12°45.043′ | 0.057′ | S 15°56.4′ | S 15°56.406′ | 0.006′ |

Summary over the ten cases:

| Model | Mean abs GHA difference | Maximum abs GHA difference | Mean abs Dec difference | Maximum abs Dec difference |
|---|---:|---:|---:|---:|
| Murdoch article code | 0.046′ | 0.103′ | 0.022′ | 0.048′ |
| SUNSIGHT v1.1 | 0.044′ | 0.145′ | 0.032′ | 0.063′ |
| **SUNSITE2 v0.1** | **0.038′** | **0.098′** | **0.022′** | **0.042′** |

The three compact approaches are all operating near the resolution floor of the displayed USNO data in this small set. The table is useful as a consistency check, not as a fine ranking instrument.

## Broad 1900-2049 numerical stress test

To characterize the ephemeris more meaningfully, the exact calculator algorithms were compared with **Swiss Ephemeris apparent geocentric solar coordinates** every two days at 12:00 from 1900-01-01 through 2049-12-31.

Number of epochs: **27,394**.

Swiss Ephemeris is used as a high-precision numerical reference, **not as USNO**.

| Model | GHA RMS | GHA max | Declination RMS | Declination max |
|---|---:|---:|---:|---:|
| SUNSIGHT v1.0 | 0.201′ | 0.618′ | 0.059′ | 0.227′ |
| **SUNSIGHT v1.1** | **0.059′** | **0.196′** | **0.019′** | **0.073′** |
| **SUNSITE2 v0.1** | **0.030′** | **0.100′** | **0.013′** | **0.040′** |

Using the unrounded numerical results, SUNSITE2 v0.1 produced approximately:

- GHA RMS: **0.02955′**
- maximum absolute GHA error: **0.10003′**
- declination RMS: **0.01291′**
- maximum absolute declination error: **0.04034′**

The test was reproduced with Python and `pyswisseph` / Swiss Ephemeris 2.10.03.

Relative to SUNSIGHT v1.1, SUNSITE2 roughly halves the remaining GHA error while using only 219 additional calculator bytes in the current tested builds.

## What these tests do not establish

They do not prove that a real Sun sight will be accurate to 0.03 NM or 0.10 NM.

The ephemeris is only one contributor to the final line of position. Sextant reading, horizon quality, timing, vessel motion, dip, index correction and especially abnormal refraction can dominate the error budget.

The broad numerical test supports the astronomical model. Physical A-D tests support the complete program path. Neither replaces navigational judgment or independent means of position fixing.
