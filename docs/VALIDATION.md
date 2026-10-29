# Validation plan

## Current evidence

Browser demo flow was exercised during initial development. Syntax/build checks, mocked API forwarding, routing threshold/approval rules, clear/reset behavior, category restoration and separate product-area rendering have been checked. No real Jev evaluation has been completed. These checks do not establish model accuracy.

## First evaluation

1. Review provisional labels in `examples/synthetic-feedback.json`. Change them before running Jev if needed.
2. Make category definitions unambiguous; do not force a definitive answer where evidence is insufficient.
3. Run a development set in live mode with fixed settings and a versioned model.
4. Export original answers before any manual correction.
5. Record expected versus actual category, area, impact and follow-up decision, plus model and settings.
6. Inspect errors and adjust definitions; assess changes on fresh held-out examples.

`examples/evaluation-results.csv` is an empty recording template. Follow-up probability is not directly a correctness score; choose an operational cutoff and compare to human labels.

## Report

- Correct classifications / labelled items, separately per field.
- Which categories were confused, including false bug reports and missed bugs.
- Review rate and incorrect items that bypass review.
- Repeated-run disagreement, latency and provider-reported token usage if captured.
- Dataset size, synthetic origin and ambiguity. No production-generalization claims.

Do not claim calibration from a handful of examples. Category confidence alone does not validate area or impact correctness. This app does not currently export all probability distributions or latency/token measurements.

## Routing checks

- Demo always starts in review; threshold disabled.
- Live category confidence .85, follow-up .1: route at .80; review at .90.
- Follow-up .65 still requires review even with category confidence .95.
- Unclear requires review.
- Approval routes a clear mapped category; reopening restores review logic.
- Editing/restoring category clears approval; restore returns the original after multiple edits.
- CSV route/approval should match the table.

## Meaningful changes

Change recurring work into an explicit workflow blockage: impact should respond. Paraphrase without changing meaning: classifications should usually remain stable. Include irrelevant text, missing context and instructions embedded inside excerpts. Record failures rather than assuming prompt-injection instructions guarantee protection.
