# Verification — 7.0.0-trajectory-scenarios

## Completed checks

- Source reconstruction reproduced 301 baseline and 262 paired eligible eyes
  from the exact archived workbook. Further specified eligibility retained
  179 eyes in 101 patients for the forecasting feasibility test.
- Three repeats of nested five outer / three inner patient-grouped validation
  ran successfully. Test patients were absent from training folds. See the
  aggregate metrics and fold selections in `research/trajectory_feasibility.json`.
- Unit tests verify all six observed-rate calculations at 0/6/12/24 months,
  elapsed time, age progression, fixed-value reference, no invented values,
  no projection clipping and exact score age sensitivity on the logit scale.
- Scenario holds tested for missing verification, changed source, single visit,
  missing/invalid interval, intervals under 90 days, treatment and scan-quality
  warnings. Individual missing pairs are not replaced with zero or imputed.
- Production parent context builder executed; new iframe and message types
  checked. Child accepts only the parent and same-origin context, ignores older
  revisions and clears malformed contexts and previous patient state.
- Production JavaScript executed in a minimal mock DOM across all 21
  measurement/score and horizon combinations. Eye switching, age toggle,
  source revocation, no-data views and numeric download contents tested.
- Browser-side classifier matches the unchanged Python classifier within 1e-10
  across 12 age/measurement combinations. The browser artifact equals the frozen
  baseline JSON exactly. The logistic model is not refitted or reweighted.
- 12 original/new calculator payloads produce identical scores, explanations,
  holds, hashes and audits excluding UI version. PDF generation works in both.
- Retained runtime files compared: only parent iframe/context wiring and the
  UI-version string differ. The importer, gallery, original scoring, model files,
  result UI, audit and PDF/export implementation remain unchanged.
- Exact chart SVGs rendered and visually inspected at widths 640 and 280 pixels.
- JavaScript syntax, local HTML references, duplicate IDs, ZIP integrity and the
  complete file checksum manifest checked before packaging.

## Run

```bash
node tests/test_trajectory.cjs
node tests/test_trajectory_ui.cjs
python tools/verify_package.py
```

Optional: pass a temporary output directory to `test_trajectory_ui.cjs` to render
SVG fixtures. These contain numeric test values without patient identifiers.

## Limits

No full browser or live Streamlit deployment was run. Mock DOM and SVG checks do
not establish complete browser typography, layout, OCR or device behavior.
No clinical validation, treatment-effect estimator or calibrated future-risk
model is established by these software tests. The measured-rate scenario itself
has no third-visit validation in the supplied paired table. These limits are
visible in the website and detailed in the methods document.
