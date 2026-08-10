# MoTrPAC_x_MetabolomicsWorkbench

# Integrative Metabolomics: An NIH Common Fund Data Ecosystem Workflow for Exploring MoTrPAC and Metabolomics Workbench Data

## Overview

In this notebook, you will use the **Metabolomics Workbench REST API** to identify, retrieve, and compare metabolomics studies related to exercise training. The workflow focuses on publicly available **MoTrPAC** rat heart metabolomics studies and an independent exercise-training study from the **Metabolomics Workbench** as a cross-study comparator.

This workflow identifies and downloads candidate Metabolomics Workbench studies, reviews study metadata and data structure, and identifies metabolites shared across datasets. It then characterizes shared metabolites based on their RefMet IDs, and then performs within-study as well as integrative analyses.

Because metabolomics studies can differ in experimental design, analytical platform, metabolite naming, data scale, and sample annotation, the workflow also emphasizes the importance of reviewing study metadata and data characteristics before making cross-study comparisons.

## Learning Objectives

1. **Use the Metabolomics Workbench REST API** to identify MoTrPAC studies and candidate comparator studies for cross-study metabolomics analysis.
2. **Extract and evaluate study data and metadata** to determine whether selected studies are suitable for comparison.
3. **Analyze shared metabolites across studies** using statistical, effect-size, metabolite classification, and directional-concordance approaches.

## Notebook Outline

- **Setup and environment checks:** confirm Python 3.12, install/import required packages, and configure data/output directories.
- **API connectivity:** confirm access to the Metabolomics Workbench REST API and introduce reusable API helper functions.
- **MoTrPAC study search:** search Metabolomics Workbench for candidate MoTrPAC studies using study metadata and keyword queries.
- **Comparator search:** identify independent rat exercise-training metabolomics studies that may be suitable for cross-study comparison.
- **Study comparison and data retrieval:** review study metadata, sample/group annotations, metabolomics type, and analysis accessions; download selected datatables locally.
- **Data-scale diagnostics:** inspect metabolite value distributions and generate study-specific transformation recommendations.
- **Shared-metabolite analysis:** identify metabolites shared between the comparator study and targeted MoTrPAC studies.
- **RefMet characterization:** annotate shared metabolite names using RefMet and examine chemical super-class, main-class, and sub-class composition.
- **Statistical analysis:** calculate within-study mean differences, Welch's t-tests, Cohen's *d*, combined p-values, and Benjamini-Hochberg false discovery rate-adjusted q-values.
- **Directional concordance:** classify shared metabolites as having same- or opposite-direction responses across datasets.
- **Visualization:** generate static heatmaps, concordance plots, and interactive Plotly visualizations with study-group and statistical details.

## Data Sources Used

### Metabolomics Workbench / NMDR Projects

| Data source | Studies used | Project ID | Project DOI | DOI Link |
| --- | ---: | --- | --- | --- |
| Metabolomics Workbench / NMDR (MoTrPAC heart studies) | 13 | PR001020 | 10.21228/M8V97D | [https://doi.org/10.21228/M8V97D](https://doi.org/10.21228/M8V97D) |
| Metabolomics Workbench / NMDR (non-MoTrPAC comparator study) | 1 | PR000623 | 10.21228/M84T25 | [https://doi.org/10.21228/M84T25](https://doi.org/10.21228/M84T25) |

## Citation (Data & Resource)

### How to cite NMDR data used in this workflow

**MoTrPAC heart studies (Project PR001020):**  
This data is available at the NIH Common Fund's National Metabolomics Data Repository (NMDR) website, the Metabolomics Workbench, [https://www.metabolomicsworkbench.org](https://www.metabolomicsworkbench.org), where it has been assigned Project ID **PR001020**. The data can be accessed directly via its Project DOI: **10.21228/M8V97D** ([https://doi.org/10.21228/M8V97D](https://doi.org/10.21228/M8V97D)). This work is supported by NIH grant **U2C-DK119886**.

**Non-MoTrPAC comparator study (Project PR000623):**  
This data is available at the NIH Common Fund's National Metabolomics Data Repository (NMDR) website, the Metabolomics Workbench, [https://www.metabolomicsworkbench.org](https://www.metabolomicsworkbench.org), where it has been assigned Project ID **PR000623**. The data can be accessed directly via its Project DOI: **10.21228/M84T25** ([https://doi.org/10.21228/M84T25](https://doi.org/10.21228/M84T25)). This work is supported by NIH grant **U2C-DK119886**.

### How to cite Metabolomics Workbench as a general resource

> The Metabolomics Workbench, [https://www.metabolomicsworkbench.org/](https://www.metabolomicsworkbench.org/)

## Requirements

### Recommended runtime

This notebook is designed for a **Python 3.12 Jupyter environment**. An internet connection is also required to query the Metabolomics Workbench REST API and RefMet service.

It can be run in environments such as:

- Google Colab
- Jupyter Notebook or JupyterLab
- Visual Studio Code with the Jupyter extension

### Python packages used

The notebook installs pinned package versions for reproducibility, including:

- `pandas`
- `numpy`
- `requests`
- `scipy`
- `statsmodels`
- `seaborn`
- `matplotlib`
- `matplotlib-venn`
- `plotly`
- `nbformat`

## Reproducibility Notes

- Metabolomics Workbench API responses and study metadata may change over time as repository records are updated. Re-running the notebook in the future may therefore produce different search results or metadata.
- The workflow downloads selected study datatables locally so that later analyses use a consistent local copy rather than repeatedly querying the API.
- Datatables may contain biological samples as well as QC, blank, standard, or other technical rows. The notebook includes filtering logic for relevant analyses.
- Study group information is encoded in the Metabolomics Workbench `Class` field and may include variables such as group, sex, tissue, and timepoint.
- Metabolite overlap is initially based on exact datatable column-name matching. Matching names do not by themselves guarantee identical chemical identity or comparable measurement across studies.
- RefMet annotation is used to support standardized metabolite identification and chemical classification.
- Transformation decisions are based on study-level value-distribution diagnostics and should be interpreted as practical workflow recommendations rather than definitive evidence of or the need for normalization.
- Welch's t-tests are used for within-study group comparisons, and Cohen's *d* is used to summarize standardized effect size.
- When corresponding MoTrPAC comparisons occur across studies, p-values are combined using Fisher's method and multiple-testing correction is performed using the Benjamini-Hochberg procedure.
- Directional concordance is based on whether summarized metabolite responses have the same or opposite direction of metabolite abundance across the MoTrPAC and comparator datasets; it does not imply statistical equivalence between studies.

## Outputs

The notebook writes downloaded data, cached annotations, and analysis results to project directories including:

- `./data/` — downloaded Metabolomics Workbench datatables and RefMet cache files
- `./outputs/` — heatmap matrices and other exported analysis results

Example output files include:

- MoTrPAC targeted mean-difference matrices
- comparator mean-difference matrices
- Cohen's *d* matrices
- p-value or q-value matrices
- cached RefMet annotations

Static figures are displayed within the notebook, while interactive Plotly figures allow users to hover over individual comparisons to inspect study-group and statistical details.

## Learning Assessments

Short multiple-choice assessments with answer keys are included throughout the notebook.

## Recommended Next Steps

1. **Apply the workflow to additional Metabolomics Workbench studies.**  
   Before comparing studies, review the study design, metadata, sample annotations, metabolite naming, analytical platform, and data scale to determine whether the datasets are suitable for cross-study analysis.

2. **Explore MoTrPAC data with the official R packages.**  
   Publicly released MoTrPAC data are available through official R packages that include functions for accessing, organizing, and analyzing MoTrPAC datasets. Visit the [MoTrPAC Data Hub](https://motrpac-data.org/code-repositories) for package documentation and code resources.

## Contact / Attribution

If you reuse or adapt this workflow, please cite the data sources above and acknowledge **Metabolomics Workbench / NMDR** and **MoTrPAC** as appropriate.