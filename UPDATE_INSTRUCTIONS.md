# Update to 7.0.0-trajectory-scenarios

Extract the release ZIP and upload its contents to the repository root. Replace
matching files and preserve the new `components/trajectory` folder. Keep
`kcn_dual_calculator_app.py` as the Streamlit main file; requirements are unchanged.
Reboot the app and reload the browser. Check **7.0.0-trajectory-scenarios** in the
calculator footer.

The previous model area now opens **Longitudinal projections**. The adjacent
original report-map tab remains available. Import/verify two visits, select OD
or OS, then choose a measurement and 6/12/24 months. Forecast columns are explicit
linear-continuation scenarios. They are not trained risk probabilities.

The age option appears under the graph. By default age is held at the latest
scan for future score comparisons; enable the option only to inspect how the
existing classifier's age association changes the hypothetical score. No age
change automatically improves the physical measurement projections.

Single visits, unverified sources, short intervals under 90 days and recorded
adverse treatment/quality information do not produce a future trajectory. For a
single visit, original calculator results above remain available as before.

The package stays below GitHub's 100-file upload batch limit. Old `benefit` files
may remain in the repository, but are no longer embedded or linked by the main
website. Upload the complete release rather than mixing files across versions.

No patient data should be uploaded from your local research workspace into the
public repository. This release contains only software, aggregate summaries and
model coefficients, with research reproduction instructions.
