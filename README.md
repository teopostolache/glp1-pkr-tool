# GLP-1 PKR Clinical Decision Tool

> Interactive clinical decision support tool implementing the **GLP-1 PKR framework** — GLP-1 receptor agonist–induced pharmacokinetic recalibration of lipophilic psychotropic medications. Companion to the Translational Psychiatry manuscript (2026).

**[▶ Launch the tool](https://teopostolache.github.io/glp1-pkr-tool/)** · No installation required · Works offline after first load · Compatible with all modern browsers

---

## What this tool does

When a patient loses significant body weight on a GLP-1 receptor agonist (tirzepatide, semaglutide, liraglutide), the adipose and lean-tissue compartments that normally sequester lipophilic psychotropic medications contract. This raises plasma concentrations at unchanged prescribed dose — a silent, unintended dose escalation. We call this phenomenon **GLP-1–induced Pharmacokinetic Recalibration (GLP-1 PKR)**.

This tool estimates the expected percentage change in steady-state plasma concentration (%ΔCss) for:

- **31 psychotropic medications** across three redistribution risk tiers
- **8 GLP-1 receptor agonist regimens** with DEXA-anchored body composition parameters
- **0–35% cumulative body weight loss**

It also displays:

- **Per-drug QTc risk** (high / moderate / low, from CredibleMeds)
- **D3-preferential status** (yes / no)
- **TDM actionability** (five levels from AGNP 2017: strongly recommended / recommended / limited / provisional / not useful)
- **Proactive TDM alerts** for high-risk drug + weight-loss combinations
- Optional target dose in mg when the current daily dose is specified

## How to use it

1. **Select a psychotropic medication** — Tier 1, 2, or 3
2. **Select the GLP-1 receptor agonist** and dose
3. **Enter cumulative body weight loss.** Two input paths are supported:
   - **Direct entry** — enter the percentage via slider or number field (0–35%)
   - **Compute from absolute weights** — enter baseline and current weight in kg or lb; the tool computes the percentage automatically
4. *(Optional)* Specify the current daily dose to receive a target dose estimate in mg

The tool instantly displays:

- **Total %ΔCss** (full-compartment model incorporating fat and lean mass correction)
- **Fat-only %ΔCss** for comparison
- **Lean correction** (difference between full and fat-only models)
- **Drug property chips** — QTc risk, D3 status, TDM actionability
- **Proactive TDM alert** when the drug + weight-loss combination warrants anticipatory concentration measurement
- **TDM actionability banner** explaining what TDM can and cannot tell you for this specific drug
- **Colour-coded action recommendation** with language calibrated to the drug's TDM category
- **Target dose** when a current dose is entered, with nearest commercial strength

## Scientific basis

### The full-compartment pharmacokinetic model

```
%ΔCss = (1 / (1 − f_fat · %Δfat/100 − f_lean · %Δlean/100) − 1) × 100
```

where `f_fat` = adipose fraction of Vd, `f_lean` = 1 − f_fat, `%Δfat` = fat mass lost, `%Δlean` = lean mass lost (as % of lean body mass). LBM fraction = 0.50 (average of SURMOUNT-1 and STEP 1 DXA baselines).

### DEXA-anchored body composition parameters

| Agent | Fat factor | Lean fraction of WL | Source |
|---|---|---|---|
| Tirzepatide (all doses) | 1.59 | 25% | [Look et al. *Diabetes Obes Metab* 2025](https://doi.org/10.1111/dom.16275) |
| Semaglutide 2.4 mg SC | 1.29 | ~38% | [Wilding/King et al. *J Endocr Soc* 2021;5(Suppl 1):A16–A17](https://doi.org/10.1210/jendso/bvab048.030) |
| Liraglutide, oral semaglutide | 0.62–0.95 | ~38% | Estimated (no dedicated DEXA substudy) |

### TDM actionability categories (AGNP 2017)

| Category | Tool language | Drugs |
|---|---|---|
| **Strongly recommended** | "TDM is the definitive guide for dose adjustment; obtain serum concentration before changing dose where possible." | Clozapine, olanzapine, haloperidol, fluphenazine, chlorpromazine, amitriptyline, nortriptyline, lithium, valproate, carbamazepine, lamotrigine |
| **Recommended** | "TDM is recommended to guide dose adjustment where available." | Aripiprazole, brexpiprazole, quetiapine, risperidone, paliperidone, ziprasidone, lurasidone, citalopram, escitalopram, paroxetine, venlafaxine |
| **Limited** | "Clinical assessment should guide dose change — TDM is of limited value for this drug (broad orientation range only)." | Sertraline, fluoxetine, duloxetine |
| **Provisional** | "Clinical assessment should guide dose change — no validated AGNP concentration target exists for this drug." | Cariprazine |
| **Not useful** | "Clinical assessment (sedation, gait, cognition, dependence) guides dose change — TDM is not routinely useful for this drug." | Diazepam, clonazepam, alprazolam, lorazepam |

### Proactive TDM alerts

The tool fires a **"⚑ Proactive TDM recommended"** banner — independent of the severity-driven action card — when anticipatory concentration measurement is clinically more informative than waiting for symptoms. Two layers:

- **Drug-specific rationales** (always fire, regardless of AGNP category):
  - **Cariprazine** — DCAR active metabolite accumulates over weeks; track parent + DCAR from the patient's own baseline even without a validated AGNP target
  - **Clozapine** — narrow therapeutic index + seizure risk above 600 ng/mL; add a visit-anchored measurement at ≥10% BW loss to the standard REMS monthly protocol
  - **Lithium** — narrow TI with GLP-1 RA–related fluid/sodium balance changes that can independently alter lithium
  - **Haloperidol** — established concentration–akathisia relationship plus TdP risk make proactive measurement more informative than reactive confirmation

- **Generic high-risk combinations** (fire only when TDM is actionable enough to inform dose):
  - Tier 1 drug + ≥10% body weight loss
  - Predicted %ΔCss ≥15%

## Clinical caveat

This tool is a **clinical decision support aid**, not a replacement for clinical judgement. All estimates are model-derived and hypothesis-generating. No prospective pharmacokinetic validation data exist yet for GLP-1 RA–treated populations. This is an emerging area; guidelines are likely to evolve. See the companion manuscript for full limitations.

## Citation

If you use this tool in research, teaching, or clinical decision support, please cite the accompanying manuscript:

> [Author names]. GLP-1 Receptor Agonist–Induced Pharmacokinetic Recalibration of Lipophilic Psychotropic Medications: Framework, Algorithm, and Clinical Tool. *Translational Psychiatry* (in submission, 2026).

Once the Zenodo DOI is minted, add:

> [Author]. (2026). *GLP-1 PKR Clinical Decision Tool* (Version 2.9) [Software]. Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX

## Files

| File | Purpose |
|---|---|
| `index.html` | The interactive tool itself (single-file, no dependencies) |
| `README.md` | This file |
| `LICENSE` | MIT License |
| `CITATION.cff` | Machine-readable citation metadata |

## Version history

- **v2.9** (April 2026) — Graded TDM recommendations calibrated to the five AGNP categories; drug-specific proactive TDM alerts for cariprazine, clozapine, lithium, haloperidol; generic proactive alerts for Tier 1 + ≥10% BW and predicted %ΔCss ≥15%. Replaces binary "TDM must confirm" language.
- **v2.8** — Fixed hidden bug: agent `<option>` values carried old pre-DEXA parameters (tirzepatide 1.622 → corrected 1.592; semaglutide 1.644 → corrected 1.287; lean fractions 0.13/0.27 → corrected 0.25/0.38). All calculations from v2.2 onward were affected by this bug.
- **v2.7** — Unified fat/lean display below both inputs; visible "% BW" label; slider thumb sync on programmatic value change
- **v2.6** — Optional weight-loss calculator: enter baseline and current weight in kg or lb, tool computes percentage
- **v2.5** — TDM-aware dose confirmation logic; removed residual "If QTc drug…" conditional language
- **v2.4** — TDM actionability per drug (AGNP 2017)
- **v2.3** — Drug-specific QTc / D3 properties as chips; optional dose target calculation in mg
- **v2.2** — DEXA-anchored fat conversion factors and lean fractions
- **v2.1** — Lean fraction correction
- **v2.0** — Added GLP-1 RA agent selector; full two-compartment formula with lean correction
- **v1.0** — Fat-only model; single drug selector

## Development

Single-file HTML application. No build step, no dependencies, no server requirement. Open `index.html` in any modern browser. All logic is plain JavaScript in the `<script>` block; CSS is embedded in the `<style>` block. To modify: edit `index.html` and commit.

## License

[MIT License](LICENSE) — you may use, copy, modify, and distribute this tool freely with attribution.

## Author and contact

Teodor T. Postolache, MD
University of Maryland School of Medicine; Department of Psychiatry; Division of Biological Psychiatry; Mood and Anxiety Program

## Acknowledgements

 The DEXA substudy data used to anchor body composition parameters are drawn from the SURMOUNT-1 (tirzepatide; Look et al. 2025) and STEP 1 (semaglutide; Wilding/King et al. 2021) trials. The AGNP 2017 Consensus Guidelines (Hiemke et al. *Pharmacopsychiatry* 2018) informed the TDM actionability categorisation. The CredibleMeds registry (crediblemeds.org) informed the QTc risk classification. All clinical observations reported in the companion manuscript are de-identified.
