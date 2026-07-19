# Divvy Trip Data Ingestion Pipeline

A reproducible Python pipeline for downloading, extracting, and organizing Divvy bike-share trip data for analytics and machine learning projects. The notebook is explicitly framed around the **CRISP-DM** methodology and focuses on the early lifecycle stages needed to build reliable downstream analysis workflows.

## Project Overview

This project automates the retrieval of monthly Divvy trip data from the public Divvy S3 bucket, filters files by a configurable start date, downloads ZIP archives, extracts them, and consolidates the resulting CSV files into a single master directory for later use in exploratory analysis, feature engineering, and modeling.

The uploaded notebook is designed as a reusable ingestion workflow rather than a modeling notebook. Its primary value is creating a consistent raw-data foundation that supports later notebooks in the project lifecycle.

## Business Understanding

Urban mobility and bike-share analytics often require large, continuously updated trip datasets before any meaningful analysis can begin. This project addresses that operational need by building a repeatable pipeline that reduces manual downloading and keeps source data organized for future analysis.

From a CRISP-DM perspective, the objective is to support future questions such as trip demand patterns, rider behavior, seasonality, station utilization, and predictive modeling by making historical trip files easy to collect and maintain.

## Data Understanding

The notebook connects to the public Divvy S3 bucket, reads the XML listing of available objects, and extracts file keys for available ZIP archives. In the recorded run, the notebook reported finding 94 ZIP files in the bucket before filtering them by the configured date range.

The configuration sets the download window to begin at January 2024 using `START_YEAR = 2024` and `START_MONTH = 1`. After applying the date filter and excluding future months, the notebook selected 30 files for download in that execution.

## Data Preparation

The preparation workflow creates three main folders: one for downloaded ZIP files, one for extracted contents, and one consolidated `csv_master` directory for final CSV storage. This structure helps separate raw compressed data, extracted intermediate files, and analysis-ready flat files.

The notebook then performs four preparation tasks in sequence:
- Creates required directories with `os.makedirs(..., exist_ok=True)`.
- Downloads monthly ZIP files from Divvy using streamed HTTP requests.
- Extracts each archive into its own subfolder with Python's `zipfile` module.
- Walks through extracted folders and copies all CSV files into a single master directory using `shutil.copy2`.

## Modeling Readiness

This notebook does not train machine learning models directly, but it prepares the data foundation needed for later modeling notebooks. The consolidated CSV repository can be used for exploratory data analysis, data quality checks, feature engineering, and supervised or unsupervised learning workflows.

Potential next modeling tasks include trip duration prediction, demand forecasting, rider segmentation, or station-level usage analysis, depending on how the consolidated CSV files are transformed in later project stages.

## Evaluation

The notebook includes practical indicators that the ingestion pipeline ran successfully, including status messages for connection, download counts, extraction progress, and final CSV collection. In the captured output, the workflow ended with a completion message and reported the destination path for the consolidated CSV files.

For a production-quality version, evaluation could be strengthened by adding automated checks for duplicate files, corrupted archives, row-count validation, schema consistency, and download retry logic.

## Deployment

The current implementation is notebook-based and suitable for local execution or scheduled runs in a managed environment. Because the workflow is parameterized through configuration variables such as base paths and start date, it can be adapted for local storage, cloud storage, or shared project directories.

A practical deployment path would be to refactor the notebook into a Python script or package, add logging, and schedule monthly refresh jobs with Task Scheduler, cron, GitHub Actions, or a cloud orchestration service.

## Repository Structure

```text
.
├── download_divvy_data.ipynb
├── README.md
└── data/
    ├── downloads/
    ├── extracted/
    └── csv_master/
```

> Note: The exact data folder location in the notebook is currently configured to a Google Drive path on Windows (`G:\My Drive\Divvy_TripData`). Update this path before running the project in another environment.

## Technologies Used

- Python
- Jupyter Notebook
- requests
- BeautifulSoup
- tqdm
- zipfile
- shutil
- os
- datetime

## How to Run

1. Open `download_divvy_data.ipynb` in Jupyter Notebook or JupyterLab.
2. Update `BASE_FOLDER` to a valid path on your local machine.
3. Adjust `START_YEAR` and `START_MONTH` if you want a different historical download window.
4. Run the notebook cells in sequence to create folders, discover available files, download ZIP archives, extract them, and consolidate CSVs.
5. Use the resulting `csv_master` folder as the input source for downstream EDA, dashboarding, or machine learning notebooks.

## Future Improvements

- Add exception-specific error handling instead of broad `except` blocks.
- Validate file integrity after download and extraction.
- Add deduplication and schema validation checks.
- Save execution logs for reproducibility and troubleshooting.
- Parameterize output paths with environment variables or a config file.
- Convert the notebook into a reusable Python module or CLI pipeline.

## Author

Seif H. Kungulio
