# CFDE-Course-Module-MoTrPAC-x-Metabolomics-Workbench

# Integrative Metabolomics: A NIH Common Fund Data Ecosystem workflow to extract and analyze metabolomics data sets from The MoTrPAC Study and the Metabolomics Workbench

## Overview
In this notebook, you will extract and analyze metabolomics data sets from two **NIH Common Fund Data Ecosystem** programs: **MoTrPAC** and the **Metabolomics Workbench**. This workflow provides an example to extract heart tissue data from rat exercise training studies and to analyze overlapping metabolites.

### Learning Objectives
1. Leverage Metabolomics Workbench API queries to find **MoTrPAC** and **Metabolomics Workbench** studies for analyses.
2. Extract and compare data/metadata from candidate studies.
3. Analyze overlapping metabolites and compare the directionality of abundance by study groups.

## Notebook Outline
- **Setup:** install/import Python packages and set global parameters.
- **API connectivity:** confirm Metabolomics Workbench REST API access.
- **Study search:** identify MoTrPAC studies and candidate comparable rat exercise studies by keyword search.
- **Compare/contrast studies:** select MoTrPAC heart studies and one comparator study; review metadata and grouping structures; download and preview datatables; diagnose normalization/scale.
- **Harmonization & analysis:** identify overlapping metabolites; annotate with RefMet; compute within-study statistics and effect sizes; compare directional concordance; generate interactive comparisons.

## Data Sources Used
### Metabolomics Workbench / NMDR Projects
| Data source | Studies used | Project ID | Project DOI | DOI Link |
|---|---:|---|---|---|
| Metabolomics Workbench / NMDR (MoTrPAC heart studies) | 13 | PR001020 | 10.21228/M8V97D | https://doi.org/10.21228/M8V97D |
| Metabolomics Workbench / NMDR (non-MoTrPAC comparator study) | 1 | PR000623 | 10.21228/M84T25 | https://doi.org/10.21228/M84T25 |

## Citation (Data & Resource)
### How to cite NMDR data used in this workflow
**MoTrPAC heart studies (Project PR001020):**  
This data is available at the NIH Common Fund's National Metabolomics Data Repository (NMDR) website, the Metabolomics Workbench, https://www.metabolomicsworkbench.org where it has been assigned Project ID **PR001020**. The data can be accessed directly via its Project DOI: **10.21228/M8V97D** (https://doi.org/10.21228/M8V97D). This work is supported by NIH grant **U2C-DK119886**.

**Non-MoTrPAC comparator study (Project PR000623):**  
This data is available at the NIH Common Fund's National Metabolomics Data Repository (NMDR) website, the Metabolomics Workbench, https://www.metabolomicsworkbench.org where it has been assigned Project ID **PR000623**. The data can be accessed directly via its Project DOI: **10.21228/M84T25** (https://doi.org/10.21228/M84T25). This work is supported by NIH grant **U2C-DK119886**.

### How to cite Metabolomics Workbench as a general resource
"The Metabolomics Workbench, https://www.metabolomicsworkbench.org/"

## Requirements
### Recommended runtime
- Google Colab (Python 3)

### Python packages used (installed in-notebook)
- pandas, numpy, requests, scipy, statsmodels, seaborn
- matplotlib, matplotlib-venn (for overlap visualization)
- plotly (for interactive charts)

## Reproducibility Notes
- Metabolomics Workbench API responses can change over time as studies are updated; re-running the notebook in the future may yield different search results.
- Datatables can include QC/blank/standard rows; filtering logic in the notebook controls whether these are retained for analysis.
- Metabolite overlap based on datatable column names may require harmonization (e.g., RefMet matching) to improve comparability.

## Outputs
The notebook writes intermediate and result files under directories like:
- `./data/` (downloaded MW datatables and caches)
- `./outputs/` (analysis outputs and figures, if configured)

## Contact / Attribution
If you reuse or adapt this workflow, please cite the data sources above and acknowledge Metabolomics Workbench / NMDR.
