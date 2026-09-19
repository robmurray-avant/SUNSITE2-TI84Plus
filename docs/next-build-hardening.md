# Proposed SUNSITE2 next-build hardening

This document records code changes proposed after comparing SUNSITE2 v0.1 with the completed SUNSIGHT v1.1 review.

**These changes are not present in the current tested `SUNSITE2.8xp`.**

The current binary and `SUNSITE2.txt` should remain paired until a revised source is entered/tokenized, transferred to a plain TI-84 Plus, and re-tested. A documentation-only update must not imply that the existing `.8xp` contains these changes.

## 1. Exact discrete-choice validation

Current v0.1 range checks allow fractional values such as `1.5` for choices intended to be exactly 1 or 2.

The most important example is Sun limb selection. Later code assigns signed semidiameter only when `K=1` or `K=2`. If a fractional value passes the range check, neither assignment occurs and `L₁(62)` can retain a stale value.

The next build should accept only exact legal choices for:

- Sun limb
- latitude hemisphere
- longitude hemisphere
- index-error direction
- menu selections

This is a correctness fix, not merely cosmetic validation.

## 2. Calendar validation

The current master validation checks only:

- month 1-12
- day 1-31

It therefore allows dates such as February 31 or April 31. The Julian-date expression silently normalizes them into a later real date, producing a plausible but wrong result.

The next build should enforce:

- correct month length
- February 28/29
- Gregorian leap-year rules
- integer year/month/day

UTC seconds may remain fractional.

## 3. Position degrees/minutes validation

The current entry path uses absolute degrees plus absolute minutes/60. Minutes above 60 therefore normalize silently.

The next build should require:

- latitude minutes >=0 and <60
- longitude minutes >=0 and <60
- latitude <=90°, with zero minutes at exactly 90°
- longitude <=180°, with zero minutes at exactly 180°

Negative component entries should not be silently converted into positive values if doing so can mask a keying error; hemisphere should remain the only sign selection.

## 4. Sextant-altitude validation

The current source validates Hs degrees and minutes independently. It can therefore accept 90° plus non-zero minutes.

The next build should require:

- Hs minutes >=0 and <60
- combined Hs <=90°
- exact lower/upper limb selection

## 5. Broad correction-input plausibility checks

Current v0.1 requires only:

- eye height >=0
- pressure >=1

Temperature and index-error magnitude are effectively unconstrained.

A typo such as 105 hPa instead of 1050 hPa can produce a large refraction error while still yielding a plausible-looking answer.

The next build should use **broad typo-detection limits**, not narrow climatological assumptions. Candidate ranges should be selected conservatively and documented before coding.

Possible categories to bound:

- pressure
- temperature
- height of eye
- index-error magnitude

The purpose is to reject obviously mistyped data while still permitting unusual but physically possible conditions.

## 6. Result-screen cleanup / exit behaviour

The current result path enters `Fix 1`, displays the answer, pauses, then returns to `Float`.

If the user presses `ON` to interrupt while the result screen is paused, the program stops before `Float` and leaves the calculator in `Fix 1`.

The next build should either:

- provide an explicit Exit path that restores calculator formatting before `Stop`, or
- restore `Float` before the final pause if hardware testing confirms the displayed result remains satisfactory.

## 7. Workspace warning

SUNSITE2 overwrites variables A-Q and list L₁.

This is acceptable for a dedicated navigation calculator but should be stated prominently in installation documentation. It does not require a code change unless a future design chooses dedicated named lists or backup/restore logic.

## 8. Bennett scaling detail

The pressure/temperature factor currently uses the base Bennett refraction term `L₁(54)` inside its small temperature denominator rather than the refined `L₁(56)` value.

Testing during the SUNSIGHT review showed the numerical effect to be negligible for navigation. This should be treated as a low-priority fidelity cleanup, not a reason to disturb a tested correction chain without a complete regression test.

## 9. DUT1 / UTC

Do **not** add a mandatory DUT1 input merely for theoretical purity.

The standalone design intentionally accepts ordinary UTC and approximates UT1. That is practical for an offshore backup device. The limitation should be documented clearly and reconsidered only if future UTC policy makes the approximation operationally significant over the intended support period.

## 10. Required validation after any source change

A revised source should not replace the current tested build until all of the following are complete:

1. enter/tokenize the complete revised program on or for the TI-84 Plus
2. record on-calculator byte size
3. transfer the exact `.8xp` back from the calculator / TI Connect CE
4. verify TI container length and internal checksum
5. record SHA-256
6. run Cases A-D on physical hardware
7. repeat the ten-case USNO ephemeris check if the astronomy block changed
8. repeat the 27,394-epoch Swiss test if the astronomy block changed
9. verify `.txt` is a faithful human-readable rendering of the tested binary
10. only then update the documented build/version

## Suggested versioning

If the next build changes only validation/interface behaviour and leaves the VSOP ephemeris untouched, **v0.2.0** is a reasonable development version.

A stable v1.0 should wait until:

- input hardening is complete
- exact binary/source pairing is established
- physical regression passes
- broader validation is published
- the project's role relative to SUNSIGHT is settled
