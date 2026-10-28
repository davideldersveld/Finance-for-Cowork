# Executive commentary rules

## Number rules

1. **Closed set.** Build the figure register from the supplied analysis before writing. Every number in the commentary must appear in the register. This includes amounts, percentages, basis points, ratios, counts, days and dates.
2. **Permitted re-expression.** A register figure may be re-expressed only by:
   - changing units (12,412 USD thousands to $12.4m);
   - rounding to fewer decimals, half away from zero;
   - changing sign presentation to a direction word ("(2,400)" to "down $2.4m").
   Re-expression is recorded in the number trace. Everything else is a new number.
3. **Not permitted.** Computing a difference, percentage, margin, growth rate, share, average, annualization, run-rate or sum that the analysis does not already show. Combining two drivers into one figure. Converting currency. Restating at a different period. If the user wants such a figure, it must first be added to the analysis by the owning analysis skill.
4. **Magnitude words.** "Doubled", "halved", "a third", "most", "majority", "record" are numbers in disguise. Use them only when the register holds the ratio or comparison that supports them; otherwise use a plain direction word ("higher", "lower") or the register figure itself.
5. **Direction words.** Up/down, ahead/behind, favorable/unfavorable must match the sign and polarity in the analysis. For cost lines, an increase is unfavorable unless the analysis states otherwise. Never write "favorable" or "unfavorable" when the analysis does not state the comparator.
6. **Consistency.** The same figure is expressed the same way every time it appears (same units and decimals).
7. **Rounding visible in drivers.** If rounded driver figures do not add to the rounded total, do not add a balancing figure; say "other items" without a number unless the analysis shows the residual.
8. **Comparator always stated.** Every figure names its comparator where it is a variance: versus budget, forecast, prior year or prior quarter.

## Figure register columns

Register ID, Figure as in source, Units and currency, Period, Entity or scope, Basis (Actual, Budget, Forecast, Prior year, Pro forma), Comparator, Source (file + sheet + cell or range, or document + page/section), Evidence label in analysis (Evidenced / Hypothesis / not labelled), Verification status (Tied out / Reviewed by user / Unverified).

## Number trace columns

Trace ID, Commentary section, Sentence (short), Figure as written, Register ID, Source value, Re-expression applied (units, rounding, direction word), Check (Matches register / Not in register).

## Driver ranking

- Rank drivers by the absolute value of their quantified effect in the analysis, largest first.
- Include three to five. Fewer only if the analysis has fewer quantified drivers; more are grouped under "other items".
- Each driver sentence: what moved, by how much (register figure), why (cause from the analysis, with its evidence label), and whether it is expected to recur if the analysis says so.

## Evidence language

| Analysis label | Commentary phrasing |
|---|---|
| Evidenced | State as fact — "Volume was 6% below budget, reducing EBITDA by $2.4m." |
| Hypothesis | Hedge and attribute — "We believe higher freight rates drove most of the $0.9m logistics overrun; confirmation with the carrier is pending." |
| Not labelled | Treat as Hypothesis unless the user confirms it is evidenced |

## Length and register

| Medium | Target |
|---|---|
| In chat | 150 to 300 words plus the number trace |
| Word document | One page body; number trace as an appendix |
| Speaker notes | 130 to 150 words per minute of speaking time requested, default 90 seconds; short sentences; no tables |

Style — lead with the answer; one idea per sentence; no adjectives that the figures do not support ("strong", "disappointing") unless the analysis or the user states the judgement; no jargon the audience would not use; plain verbs.

## Readiness labels

- **Ready for review** — every figure Matches register, every register figure used is Tied out or Reviewed by user, and Hypothesis drivers are hedged.
- **Ready with caveats** — all figures match the register but one or more used figures are Unverified; the caveats are listed above the draft.
- **Blocked** — the headline figure is Unverified or contradicted by a tie-out Difference, or the user asked for a figure not in the analysis and declined to remove it.
