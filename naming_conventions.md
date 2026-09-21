# Naming Conventions

This document defines the naming conventions used throughout this
Project. consistent naming helps keep project files organized and makes
The data easier to find, understand, analyze, and reuse.

## 1. General Rules

-   use lowercase letters for file and folder names.
-   use underscores (`_`) instead of spaces.
-   avoid special characters when possible.
-   use short but descriptive names.
-   include dates using the `YYYY-MM-DD` format when relevant.
-   avoid unclear names such as `final`, `new`, `test2`, or
    `final_final`.
-   use Git for version control instead of creating many manually
    numbered copies of the same file.

**Preferred:** `cow_milking_data_2026-09-21.csv`

**Avoid:** `cow_data_final_new.csv`

## 2. Folder Names

Folder names should be lowercase and descriptive.

``` text
Project/
├── readme.md
├── naming_conventions.md
├── data/
│   ├── raw/
│   ├── processed/
│   └── output/
├── notebooks/
├── scripts/
└── docs/
```

-   `data/raw/` --- original data received from the farm. raw data
    should not be modified or overwritten.
-   `data/processed/` --- cleaned, standardized, or imputed datasets.
-   `data/output/` --- final datasets or results produced by the
    project.
-   `notebooks/` --- Jupyter notebooks used for exploration, analysis,
    and modeling.
-   `scripts/` --- reusable Python scripts.
-   `docs/` --- project documentation, data dictionaries, agreements,
    and related materials.

## 3. Data File Names

Use:

`<data_type>_<processing_stage>_<date>.<extension>`

Examples:

-   `cow_milking_raw_2026-09-21.csv`
-   `cow_milking_cleaned_2026-09-21.csv`
-   `cow_milking_imputed_2026-09-21.csv`
-   `cow_milking_output_2026-09-21.csv`

Raw data should never be overwritten. cleaned, modified, or imputed
Datasets should be saved as separate files.

## 4. Jupyter Notebook Names

Number notebooks in the order they are intended to be used:

`<number>_<description>.ipynb`

Examples:

-   `01_data_exploration.ipynb`
-   `02_missing_data_analysis.ipynb`
-   `03_data_imputation.ipynb`
-   `04_model_evaluation.ipynb`

## 5. Python Script Names

Python scripts should use lowercase `snake_case`.

Examples:

-   `clean_data.py`
-   `identify_missing_data.py`
-   `assign_missing_cows.py`
-   `impute_missing_values.py`
-   `evaluate_model.py`

## 6. Variable and Column Names

Variables created during analysis should use lowercase `snake_case`.

Examples:

-   `animal_number`
-   `lactation_number`
-   `days_in_milk`
-   `reproduction_status`
-   `avg_milk_flow`
-   `flow_30_60`
-   `session_yield`
-   `yield_first_2_min`
-   `session_duration`
-   `session_sec_milking`

Existing variables from the original farm dataset should not be renamed
Without documenting the change. if a variable is renamed, both the
Original and standardized names should be recorded in the data
Dictionary.

## 7. Missing Data

Use a consistent representation for missing values. the preferred
Representation is `NA`.

Avoid using `0`, `-1`, `999`, or `unknown` for missing data unless
Explicitly defined and documented.

Values assigned, reconstructed, or imputed during the project should be
Distinguishable from values in the original farm data.

Examples:

-   `animal_number_was_imputed`
-   `session_yield_was_imputed`

Suggested indicator values:

-   `TRUE` --- value was assigned or imputed by the project.
-   `FALSE` --- value was present in the original data.

The original raw data should always be preserved.

## 8. Versioning

Use Git to track changes to code and documentation.

Avoid names such as:

-   `analysis_final.py`
-   `analysis_final2.py`
-   `analysis_really_final.py`

For datasets that need separate versions, use the processing stage and
Date, such as `cow_milking_cleaned_2026-09-21.csv`.

## 9. Data Lineage

Document changes made to the original farm data so researchers can
Determine where each value came from.

Whenever possible, preserve whether a value was:

-   present in the original dataset.
-   cleaned or standardized.
-   assigned to a cow during processing.
-   imputed because the original value was missing.
-   removed or excluded from analysis.

This prevents the final dataset from hiding which values were directly
Observed and which were generated or modified during the research
Process.

## 10. FAIR Principles

These naming conventions support the FAIR data principles.

### Findable

Descriptive and predictable file names, folder structures, and metadata
Make datasets easier to locate.

### Accessible

Consistent organization allows authorized researchers to identify and
Access the files needed for the project.

### Interoperable

Standardized file formats, variable names, units, and missing-value
Conventions make the data easier to use across different programs and
Analyses.

### Reusable

Clear naming, documentation, versioning, and data-lineage practices
Allow future researchers to understand how the data were collected and
Modified.

Any deviation from these naming conventions should be documented in the
Project's `readme.md` or data dictionary.
