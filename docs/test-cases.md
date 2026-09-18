# Validation test cases

## Historical Cases A–D

These four cases originate in William S. Murdoch's 1996 TI-81 article and were also used during SUNSIGHT development.

### Case A — physical TI-84 Plus PASS

- Date: 1950-04-08
- UTC: 18:43:28
- Position: N 62°28.2′, E 000°18.8′
- Hs: 1°38.2′
- Limb: lower
- Index error: 10.2′ off
- Eye height: 2.2 m
- Pressure: 1050 mb
- Temperature: 2 °C

SUNSITE2 result:

**11.4 NM To, Zn 282.8°**

Expected warning:

**LOW SUN / USE WITH CAUTION**

Representative internal values from the current calculation:

- GHA ≈ 100°23.087′
- Dec ≈ N 7°12.012′
- Hc ≈ 1°29.456′

### Case B — physical TI-84 Plus PASS

- Date: 1972-06-23
- UTC: 00:17:52
- Position: S 16°23.0′, E 172°00.0′
- Hs: 50°01.2′
- Limb: lower
- Index error: 10.2′ off
- Eye height: 3.4 m
- Pressure: 1010 mb
- Temperature: 10 °C

SUNSITE2 result:

**24.0 NM To, Zn 5.8°**

Representative internal values:

- GHA ≈ 183°57.211′
- Dec ≈ N 23°26.035′
- Hc ≈ 49°59.209′

### Case C — predicted current result

- Date: 1992-03-18
- UTC: 22:00:00
- Position: S 00°38.1′, W 162°18.9′
- Hs: 76°24.8′
- Limb: upper
- Index error: 8.2′ on
- Eye height: 6.2 m
- Pressure: 970 mb
- Temperature: 40 °C

Predicted SUNSITE2 result:

**13.0 NM To, Zn 89.8°**

### Case D — predicted current result

- Date: 1994-11-28
- UTC: 01:10:14
- Position: N 18°17.2′, W 148°58.8′
- Hs: 25°40.7′
- Limb: lower
- Index error: 2.5′ on
- Eye height: 4.35 m
- Pressure: 1030 mb
- Temperature: 34 °C

Predicted SUNSITE2 result:

**0.7 NM From, Zn 234.3°**

## Status

Cases A and B have been confirmed on a physical plain TI-84 Plus.

Cases C and D remain to be physically rechecked for this development repository.

A wider modern and historical numerical validation suite will be added as the VSOP87D date-range testing proceeds.
