# NKPI 7.0 — Conditional longitudinal scenarios

This complete Streamlit / GitHub release replaces the v6 simulated treatment
curves with a **working calculation from the entered visit pair**. The original
NKPI calculator, frozen model artifacts, ZIP/DICOM importer, source gallery,
audit panels and PDF/numeric result exports remain unchanged.

## What it calculates

- Observed change and annualized rate for A, B, thickness, Kmax, BAD-D and ARTmax.
- Conditional 6-, 12- and 24-month measurement values if each observed rate
  continues; a second line holds measurements constant as a reference.
- Optional NKPI score scenarios obtained by evaluating those projected inputs
  using the existing cohort-trained **single-visit** classifier.
- Actual future age and a separate, opt-in age-association sensitivity. Age is
  held at the latest-visit age in the score scenario by default, isolating changes
  in the measurements. Advancing age never changes the physical measurement rates.
- Descriptive cohort rate context calculated from 179 eligible Northwestern eyes
  in 101 patients. The original 426-eye workbook was source-reconstructed before
  this subset was selected; no patient records are included in this ZIP.
- Numeric scenario export, kept separate from audited original NKPI results.

**These are conditional scenarios, not validated forecasts, future progression
probabilities or treatment-effect estimates.** The dashed future points are
calculated from actual inputs and explicit assumptions, not handcrafted example
risk percentages. The same calculations work for different entered patients.

## Why the lines are not labelled CXL versus no CXL

The available selected scans do not provide the post-CXL outcomes or complete
therapy timelines needed for that comparison. The unchanged-measurement line is
not a CXL prediction, and the continuation line is not an identified untreated
counterfactual. A two-visit slope cannot establish that its rate will persist.

We tested cohort-based first-to-second-visit prediction with nested,
patient-grouped validation. It did not consistently outperform carrying the
last measurement forward. The candidate forecast is therefore **not promoted**
into the website. See [evidence and methods](docs/TRAJECTORY_METHODS.md).

## Install

1. Extract `NKPI_Longitudinal_Scenarios_v7_0_GitHub.zip`.
2. Upload the extracted contents to the repository root, replacing matching
   files and preserving the folder structure.
3. Keep `kcn_dual_calculator_app.py` as the Streamlit main file. Python deployment
   requirements are unchanged.
4. Reboot Streamlit, reload the browser, and confirm the footer version
   **7.0.0-trajectory-scenarios**.
5. Import and verify two visits as before. Open **Longitudinal projections** at
   the former 3D/model location. Choose the eye, variable and horizon.
6. To examine the score, select **NKPI score scenario**. To see the mathematical
   age effect, explicitly enable the age-association option.

The engine requires a verified pair at least 90 days apart. This interval rule
is an operational safeguard, not an evidence-based progression threshold. A
recorded scan-quality warning or prior treatment blocks scenarios. Unknown
quality/treatment history remains explicitly disclosed, never marked normal.

Missing values remain unavailable. Future values outside the calculator's
input bounds, and future scores outside its development ranges, are withheld
rather than clipped. The current NKPI score and its interpretation above remain
those of the original model.

## Checks

```bash
python tools/verify_package.py
node tests/test_trajectory.cjs
node tests/test_trajectory_ui.cjs
```

The chart/UI test uses a mock DOM; a full browser or live Streamlit run was not
available in the build environment. See [test report](docs/TEST_REPORT.md).
The `research` folder contains reproducible analysis code and aggregate results,
not patient data. It is not used by the deployed app. Older documents are retained
as historical background, not the description of this release's model.
