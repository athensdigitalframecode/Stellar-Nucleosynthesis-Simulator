# Nuclear Physics Software Projects

Two independent scientific-software project proposals:

1. **Stellar Nucleosynthesis Simulator** — an interactive tool for exploring how stars produce chemical elements through nuclear reactions.
2. **Nuclear Spectroscopy Analyzer** — a data-analysis tool for processing gamma-ray spectra, detecting peaks, and investigating possible radionuclide signatures.

Both projects are intended to combine sound scientific calculations with clear visual explanations. They can be developed independently or eventually connected through a shared nuclear-data and visualization library.

> **Project status:** Concept and initial scope. Technical choices and feature priorities below are proposals, not implementation commitments.

---

## 1. Stellar Nucleosynthesis Simulator

### 1.1 Overview

The **Stellar Nucleosynthesis Simulator** is an educational and exploratory application that demonstrates how nuclear reactions inside stars transform lighter nuclei into heavier elements and release energy.

Users should be able to select a stellar environment or reaction process, explore the relevant nuclear reaction sequence, adjust simplified physical parameters, and observe how isotope abundances change over time.

The application should make the connection between nuclear physics and astrophysics understandable without presenting a simplified classroom model as a complete stellar-evolution simulation.

### 1.2 Goals

- Visualize the main nuclear processes responsible for element formation in stars.
- Explain how reaction pathways transform one nuclide into another.
- Demonstrate how temperature, density, and reaction rates affect reaction networks in simplified models.
- Show abundance changes over time using plots and reaction-flow diagrams.
- Explain the energy released or absorbed by selected reactions.
- Help users connect nuclear properties—such as binding energy and reaction Q-values—to astrophysical processes.

### 1.3 Intended audience

- Students learning nuclear physics or astrophysics.
- University-level learners studying nuclear reaction networks.
- Educators preparing demonstrations and interactive exercises.
- Developers and science enthusiasts interested in scientific simulation software.

### 1.4 Core features

#### A. Process explorer

Provide guided modules for major nucleosynthesis processes:

- **Proton–proton (pp) chains:** hydrogen burning, including the main branches and production of helium-4.
- **CNO cycles:** catalytic hydrogen burning through carbon, nitrogen, and oxygen isotopes.
- **Triple-alpha process:** formation of carbon-12 from helium-4 nuclei.
- **Advanced stellar burning:** introductory pathways involving carbon, neon, oxygen, and silicon burning.
- **Neutron-capture processes:** conceptual introductions to the slow (s-process) and rapid (r-process) neutron-capture pathways.

Each module should contain a process overview, reaction sequence, relevant nuclides, required conditions, and a clear explanation of the model's limitations.

#### B. Interactive reaction network

Represent nuclides as nodes and nuclear reactions as directed connections. Users should be able to:

- Select a nuclide to inspect its properties.
- Follow incoming and outgoing reaction pathways.
- Highlight a selected reaction chain.
- View the reactants, products, and reaction type.
- See the mass-number and charge-number balance for each reaction.
- Open a reaction detail panel with its Q-value when the required mass data are available.

The network should be navigable and readable; avoid displaying every possible reaction at once.

#### C. Abundance evolution simulator

Allow users to run a simplified reaction-network calculation and inspect how abundances evolve.

Proposed controls:

- Select a predefined reaction network.
- Set or choose a model temperature and density within the supported range.
- Set initial isotope abundances.
- Set the simulation interval and numerical resolution.
- Start, pause, reset, and step through the simulation.

Proposed outputs:

- Abundance-versus-time plots.
- Initial and final abundance tables.
- Reaction-flow visualizations.
- A summary of the dominant reactions in the selected model.

**Scientific scope:** Begin with small, documented networks and simplified conditions. A realistic stellar model requires substantially more physics, including temperature and density histories, energy transport, mixing, and potentially hydrodynamics. The initial application must not imply that a fixed-condition reaction network predicts the full life cycle of a star.

#### D. Reaction calculator

For a selected nuclear reaction, display:

- Reactants and products.
- Mass numbers and proton numbers.
- Mass defect, where applicable.
- Reaction Q-value and its sign convention.
- Energy conversion in clearly labeled units.
- The nuclear-mass data source and data version.

The application should distinguish atomic masses from nuclear masses and handle electron masses and binding-energy conventions consistently.

#### E. Stellar environment explorer

Offer a set of illustrative, predefined environments such as a main-sequence hydrogen-burning core or a helium-burning environment. Each environment should explain the assumptions used by its simplified model.

Do not present arbitrary user-entered temperature or density values as physically representative unless the model's supported domain and assumptions are documented.

#### F. Learning mode

Include guided explanations, glossary entries, worked examples, and short challenges. An optional AI tutor could explain a selected reaction or plot, but scientific results must come from the simulation and verified data—not from generated AI calculations.

### 1.5 Scientific model and calculations

The initial model should be deliberately limited and transparent.

A possible foundation is a coupled reaction network in which the abundance of each nuclide changes according to the rates of reactions that produce or consume it. The model may be expressed as a system of ordinary differential equations:

\[
\frac{dY_i}{dt} = \sum_r N_{i,r}\,R_r(Y,T,\rho)
\]

where:

- \(Y_i\) is the abundance of nuclide \(i\),
- \(N_{i,r}\) is the net number of nuclei \(i\) produced by reaction \(r\),
- \(R_r\) is the rate of reaction \(r\),
- \(T\) and \(\rho\) are the model temperature and density.

This is a conceptual formulation; the implementation must define its abundance convention, units, reaction-rate conventions, and network equations precisely. Numerical integration should use a method appropriate to the stiffness and time scales of the selected network.

**Required scientific safeguards:**

- Validate conservation of baryon number and electric charge for every reaction.
- Track units explicitly and test conversions.
- Document reaction-rate sources, valid temperature ranges, and uncertainty where available.
- Check abundance normalization and numerical stability where the selected model requires them.
- Compare benchmark cases with published reference results before presenting them as validated.
- Label illustrative assumptions and approximations in the interface.

### 1.6 Suggested application structure

- **Dashboard:** project introduction, featured processes, and recent simulations.
- **Process library:** guided modules for each nucleosynthesis pathway.
- **Reaction explorer:** interactive nuclide-and-reaction network.
- **Simulator:** parameter controls, run controls, abundance plots, and result tables.
- **Reaction calculator:** Q-value and conservation calculations.
- **Theory and data:** equations, glossary, sources, model assumptions, and data versions.

### 1.7 Suggested technology

A practical initial stack could be:

- **Frontend:** React + TypeScript.
- **UI styling:** a consistent component system, with Tailwind CSS as one option.
- **Scientific plotting:** Plotly.js or another plotting library that supports zooming and multiple series.
- **Backend:** Python + FastAPI for reaction-network calculations and data services.
- **Scientific computation:** NumPy and SciPy, with explicit tests around numerical methods.
- **Data storage:** versioned JSON or CSV files initially; PostgreSQL only if the project later needs a database for users, saved runs, or larger datasets.

Keep the scientific calculation layer independent from the user interface so it can be tested and reused.

### 1.8 Development roadmap

| Phase | Deliverable | Completion criteria |
|---|---|---|
| 1. Foundation | Project structure, units, nuclide and reaction data models | Models are documented and covered by tests. |
| 2. Reaction explorer | Small curated network with interactive nodes and reaction details | Users can inspect pathways and verify reaction balance. |
| 3. Reaction calculator | Mass defect and Q-value calculations | Results match independently checked test cases within defined tolerances. |
| 4. First simulator | One small, documented reaction network | Abundance evolution is reproducible and numerically tested. |
| 5. Process library | pp-chain, CNO, and triple-alpha learning modules | Each module has reviewed explanations and clearly stated assumptions. |
| 6. Advanced processes | Additional burning stages and neutron-capture introductions | Each addition has suitable data, validation, and scope notes. |
| 7. Learning experience | Guided activities, glossary, optional AI tutor | AI explanations do not override or fabricate computed results. |

### 1.9 Initial MVP recommendation

The first release should focus on:

1. A curated pp-chain and triple-alpha reaction explorer.
2. Reaction balancing and Q-value calculations.
3. One small abundance-evolution simulation with fixed, documented conditions.
4. A few high-quality explanatory modules.

This is a more achievable and scientifically testable starting point than attempting to simulate an entire star from the beginning.

---

## 2. Nuclear Spectroscopy Analyzer

### 2.1 Overview

The **Nuclear Spectroscopy Analyzer** is a scientific data-analysis application for importing and examining gamma-ray energy spectra. It should help users visualize measured or sample data, calibrate channels to energy, estimate background, locate spectral peaks, and compare candidate peak energies with a reference nuclide library.

The application is intended for spectroscopy data analysis and education. It should not control radiation sources, detector hardware, or exposure systems.

### 2.2 Goals

- Import common spectrum data formats or a clearly documented CSV format.
- Display a spectrum with interactive zooming and region selection.
- Convert channel numbers to energy using calibration information.
- Estimate and subtract background using selectable, documented methods.
- Detect candidate peaks and calculate peak properties.
- Compare peak energies with reference gamma lines and present possible matches with uncertainty.
- Export analysis results in reusable formats.
- Preserve the original input data and a record of analysis settings.

### 2.3 Intended audience

- Students learning radiation detection and gamma spectroscopy.
- Researchers and laboratory users working with spectroscopy data.
- Educators demonstrating spectral analysis.
- Developers building tools for scientific measurement data.

### 2.4 Core features

#### A. Spectrum import and data management

Support a small number of formats first, then expand based on real user requirements.

Initial options:

- CSV with channel/count columns and optional metadata.
- A documented plain-text format for sample spectra.
- Additional instrument-specific formats only when their specifications are available and tested.

On import, validate the file and report missing, malformed, or inconsistent values. Preserve the original data unchanged and create a separate working analysis state.

Suggested metadata:

- Sample or dataset label.
- Acquisition duration and live time, if supplied.
- Real time, if supplied.
- Detector description, if supplied.
- Energy calibration coefficients and calibration date, if supplied.
- Data format and import timestamp.

Never invent missing acquisition or detector metadata.

#### B. Interactive spectrum viewer

Display counts versus channel or energy, with:

- Zoom and pan.
- Linear and logarithmic vertical scales.
- Selectable regions of interest (ROIs).
- Cursor readouts for channel, energy, and count.
- Original-spectrum and processed-spectrum overlays.
- Optional background and fitted-peak overlays.
- Clear axis labels and units.

Users should be able to switch between channel space and calibrated energy space.

#### C. Energy calibration

Support calibration using known reference peaks and a configurable calibration model.

Initial approach:

- Linear calibration: \(E = a + bC\), where \(C\) is channel and \(E\) is energy.
- Optional higher-order calibration only when justified by the instrument and calibration data.
- Display calibration points, fitted curve, residuals, and uncertainty.
- Warn when a calibration is extrapolated beyond the calibration-point range.

Do not silently apply a calibration when required coefficients or units are missing. Keep the raw channel axis available at all times.

#### D. Background estimation and subtraction

Offer a small set of documented methods, for example:

- User-selected background spectrum, where available.
- Local baseline estimation around a selected region.
- A configurable smoothing or baseline-estimation method for exploratory use.

Show both the original and background-corrected spectrum. Explain that background subtraction changes the statistical uncertainty and should not be treated as exact removal of all background contributions.

The initial release should avoid presenting one background method as universally correct. Method choice and limitations must be visible in the analysis record.

#### E. Peak detection and fitting

Identify candidate peaks and estimate properties such as:

- Peak channel and calibrated energy.
- Peak height.
- Net area or integrated counts under a stated model.
- Full width at half maximum (FWHM), where the fit supports it.
- Fit quality and uncertainty estimates.

Users should be able to inspect and adjust the region of interest and fitting assumptions. Provide an overlay of the fitted peak model and residuals.

A detected peak is a candidate feature, not automatically proof of a particular isotope.

#### F. Nuclide reference matching

Compare measured peak energies with a maintained reference library of gamma emissions.

For each candidate match, show:

- Nuclide name and reference-line energy.
- Observed energy and energy difference.
- Matching tolerance or uncertainty basis.
- Reference intensity or emission probability, when reliably available.
- Data source and library version.

Matching should account for energy-calibration uncertainty and detector resolution. Present ranked candidates rather than a definitive isotope identification. A robust identification may require multiple lines, relative intensities, decay information, geometry, detector efficiency, and other experimental context.

#### G. Analysis report and export

Export:

- Original spectrum data.
- Calibrated spectrum data.
- Detected peak table.
- Fit parameters and uncertainties.
- Calibration parameters and residuals.
- Background method and settings.
- Candidate nuclide matches and reference-data version.
- A concise, reproducible analysis summary.

Proposed export formats: CSV for tables, JSON for machine-readable analysis records, and PDF for a human-readable report.

### 2.5 Scientific model and calculations

The application should treat the spectrum as count data indexed by detector channel. A calibration function maps channels to energy. Peak analysis then estimates signal features against a background model.

For a Gaussian peak model, a first approximation is:

\[
f(x) = A\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) + B(x)
\]

where \(A\) is the peak amplitude, \(\mu\) is the peak centroid, \(\sigma\) is the standard deviation, and \(B(x)\) represents the modeled background. For a Gaussian, the full width at half maximum is:

\[
\mathrm{FWHM} = 2\sqrt{2\ln 2}\,\sigma
\]

This model is a starting point, not a universal description of detector peaks. Real spectra may require more appropriate response functions, low-energy tailing, escape peaks, overlapping-peak models, and detector-specific corrections.

**Required scientific safeguards:**

- Treat counts as statistical observations; avoid implying that background-corrected values have zero uncertainty.
- Propagate relevant uncertainties from calibration, background estimation, and peak fitting.
- Record the fitting range, fit model, and analysis settings.
- Detect and report overlapping peaks or poorly constrained fits where possible.
- Distinguish peak detection from nuclide identification.
- Do not infer activity from peak area unless efficiency, geometry, live time, emission probability, and required corrections are available and documented.
- Do not claim a real-world measurement is valid without appropriate instrument calibration and experimental metadata.

### 2.6 Suggested application structure

- **Dashboard:** recent datasets, sample spectra, and project overview.
- **Spectrum workspace:** import, plot, zoom, and select regions of interest.
- **Calibration panel:** calibration points, fit, residuals, and uncertainty.
- **Processing panel:** background estimation and processing history.
- **Peak analysis:** detection, fitting, and peak-property table.
- **Nuclide matching:** candidate lines, matching tolerances, and reference details.
- **Reports:** export, reproducibility record, and data provenance.
- **Documentation:** supported formats, methods, limitations, and scientific references.

### 2.7 Suggested technology

A practical stack could be:

- **Frontend:** React + TypeScript.
- **Plotting:** Plotly.js for interactive spectrum exploration.
- **Backend:** Python + FastAPI for import, processing, and analysis endpoints.
- **Scientific computation:** NumPy, SciPy, and pandas.
- **Data storage:** local files and JSON analysis records for the MVP; a database can be introduced if multi-user dataset management becomes necessary.
- **Testing:** synthetic spectra with known peak positions, areas, backgrounds, and calibration parameters.

Keep spectrum processing functions separate from API routes and UI components. This makes algorithms easier to validate and reuse from scripts or notebooks.

### 2.8 Development roadmap

| Phase | Deliverable | Completion criteria |
|---|---|---|
| 1. Foundation | Data model and documented CSV importer | Valid files import correctly; malformed files produce useful errors. |
| 2. Spectrum viewer | Interactive channel/count plot | Users can zoom, inspect values, and select ROIs. |
| 3. Calibration | Linear energy calibration and residual plot | Known synthetic calibration points are recovered within defined tolerances. |
| 4. Peak analysis | Candidate peak detection and basic fitting | Synthetic single-peak cases recover known parameters within tested uncertainty. |
| 5. Background tools | At least one documented background workflow | Original and processed data remain distinguishable and reproducible. |
| 6. Nuclide matching | Versioned reference-line library and candidate ranking | Matches show energy differences, uncertainty basis, and sources. |
| 7. Reporting | Exportable tables and analysis report | An exported report can be traced to its input and settings. |
| 8. Advanced analysis | Overlapping peaks, improved response models, additional formats | Each method is independently benchmarked and documented. |

### 2.9 Initial MVP recommendation

The first release should include:

1. CSV spectrum import with validation.
2. Interactive counts-versus-channel viewer.
3. Linear energy calibration.
4. ROI selection and basic peak detection/fitting.
5. A peak table with uncertainty and fit information.
6. Export of the spectrum and analysis results.

Add nuclide matching after calibration and peak fitting are reliable. That order reduces the risk of displaying confident-looking but scientifically misleading isotope suggestions.

---

## 3. Shared engineering principles

Although the applications solve different problems, they can share a few engineering principles and possibly reusable components.

### 3.1 Scientific data provenance

Every scientific result should be traceable to:

- Input data or selected model.
- Data source and version.
- Units and conventions.
- Calculation or processing method.
- User-adjustable parameters.
- Software version.

### 3.2 Separate science from presentation

Keep domain models and scientific calculations in testable modules. The frontend should present results and collect user inputs; it should not become the only place where scientific equations are implemented.

### 3.3 Units and uncertainty

Use explicit units in data models and interfaces. Avoid passing unexplained raw numbers between modules. Show uncertainty whenever it materially affects interpretation, and distinguish measured, calculated, estimated, and assumed values.

### 3.4 Reproducibility

A saved simulation or analysis should be reproducible from its input data, model version, calculation settings, and reference-data version. Prefer structured JSON records for this purpose.

### 3.5 Testing strategy

Each project should include:

- Unit tests for equations and conversions.
- Validation tests for input data.
- Regression tests using fixed reference cases.
- Boundary and error-condition tests.
- Integration tests for the main user workflow.
- Documentation explaining the expected precision and limitations of benchmark results.

### 3.6 AI use

AI features may explain concepts, summarize results, or help users navigate the software. They must not silently generate scientific input data, replace numerical calculations, or make unsupported claims of isotope identification or model validity. Any AI-generated explanation should be grounded in the application's computed outputs and source material.

---

## 4. Repository organization options

The projects can begin as two independent repositories:

- `stellar-nucleosynthesis-simulator`
- `nuclear-spectroscopy-analyzer`

This is the simplest option if they will have different release cycles, datasets, and user communities.

Alternatively, a monorepo could be used if shared infrastructure becomes valuable:

```text
nuclear-physics-lab/
├── apps/
│   ├── stellar-nucleosynthesis-simulator/
│   │   ├── frontend/
│   │   └── backend/
│   └── nuclear-spectroscopy-analyzer/
│       ├── frontend/
│       └── backend/
├── packages/
│   ├── nuclear-data/          # Only if genuinely shared and consistently modeled
│   ├── scientific-units/       # Shared unit helpers and conventions
│   └── ui-components/         # Optional shared interface components
├── docs/
├── README.md
└── LICENSE
```

Do not create shared packages prematurely. A shared package is worthwhile only when both projects need the same functionality and can agree on its scientific meaning and data conventions.

---

## 5. Suggested authoritative data references

Select and document data sources before implementing scientific calculations. Check licensing, citation requirements, data formats, update policies, and versioning before redistributing any dataset.

Potential starting points include:

- **IAEA LiveChart of Nuclides:** nuclear structure and decay information.
- **NNDC NuDat / ENSDF resources:** evaluated nuclear structure and decay data.
- **Atomic Mass Evaluation (AME):** evaluated atomic-mass data for mass-related calculations.
- **Nuclear reaction-rate compilations and peer-reviewed astrophysics literature:** reaction rates and their valid domains for nucleosynthesis models.
- **Evaluated gamma-ray emission data:** reference energies and emission probabilities for spectroscopy matching; select a specific maintained source and record its version before implementation.

These sources serve different purposes. Do not assume that one database provides every quantity required by either application. Store source attribution and version information alongside imported data.

---

## 6. Recommended order of development

If building both projects, develop them as separate applications and validate each scientific core before investing heavily in interface polish.

**Recommended first project: Nuclear Spectroscopy Analyzer MVP.** Its initial workflow—import a spectrum, calibrate it, inspect peaks, and export results—can be scoped into a compact and testable first release using synthetic datasets.

**Recommended second project: Stellar Nucleosynthesis Simulator MVP.** Start with a small reaction network and verified reaction data, then expand gradually into more processes and more sophisticated numerical models.

This is a project-planning recommendation, not a statement that spectroscopy is scientifically simpler in every respect. Both projects require careful domain validation.

---

## 7. Definition of done for an initial public release

A project is ready for an initial public release when:

- Its README explains the purpose, supported features, setup, and limitations.
- Installation and local execution are documented and reproducible.
- Scientific calculations have automated tests and documented reference cases.
- Units, assumptions, uncertainties, and data sources are visible.
- Example datasets or example simulations are included where licensing permits.
- The application distinguishes demonstration data from real experimental data.
- Known limitations and unsupported use cases are documented.
- No feature presents an unvalidated estimate as a definitive scientific result.

---

## 8. Open decisions before implementation

The following decisions should be made during project planning rather than assumed:

1. Will each application have its own repository, or will both live in a monorepo?
2. Is the primary audience educational, university-level, or research-oriented?
3. Should the first release be a browser application, a desktop application, or a Python-first scientific tool?
4. Which exact data sources and versions will be used, and what are their redistribution terms?
5. Which supported input formats are required for the spectroscopy analyzer?
6. Which reaction networks and temperature-density regimes are in scope for the first stellar simulator?
7. What numerical accuracy and validation benchmarks are required for each release?

Until these decisions are confirmed, treat the technology stack and roadmap in this document as a proposed starting point.

---

## 9. Guiding principle

**Scientific reliability comes before feature count.** A smaller application with traceable data, tested calculations, clear uncertainties, and honest limitations is more valuable than a large collection of impressive-looking but unverified simulations.
