# {{ cookiecutter.project_name }}

{{ cookiecutter.project_short_description }}

*Created by {{ cookiecutter.full_name }} (<{{ cookiecutter.email }}>)*

*Reporter: {{ cookiecutter.full_name }} (<{{ cookiecutter.email }}>)*

## Project goal

*TK: Briefly describe this project*

## Project notes

### Staff involved

*TK: List people & contact info for people involved in the project*

[Responsibility matrix](url-to-responsibility matrix)

[HIRUFF Q&A](url-to-hiruff)

### Data sources

*TK: List access info & contact info for data sources used in the project*

## Technical

*TK: Instructions on how to bootstrap project, run ETL processes, etc.*

### Assumptions

- Python 3.7+
- Pipenv
- GNU Make
- Jupyter Lab
- Rclone (for uploading data to Google Drive and shared notebooks to S3)

### What's in here?

*TK: Document important files in this project.*

- `Makefile`: Defines rules for running the ETL pipeline to process source data.
- `analysis`: Scripts and notebooks for analyzing data.
  - `analysis/notebooks`: Jupyter notebooks for analysis should go in this directory.
  - `analysis/archive`:  Notebooks that leave the scope of the project but should also remain in the project history will be placed here.
- `settings.py`: Project-wide settings for use in Python scripts or Jupyter notebooks. Good to help with path resolution to data files or defining connection strings to databases.
- `data`
  - `data/documentation`: Documentation on data files should go here - data dictionaries, manuals, interview notes.
  - `data/manual`: Contains data that has been manually altered (e.g. excel workbooks with inconsistent string errors requiring eyes on every row).
  - `data/processed`: Contains data that has either been transformed from an `etl` script or output from an `analysis` jupyter notebook.
  - `data/public`: Public-facing data files go here - data files which are 'live'.
  - `data/source`: contains raw, untouched data.
- `etl`: This is where we keep scripts involved with collecting data and prepping it for analysis. Try to use scripts here, insead of Jupyter notebooks.
- `publish`: This directory holds all the documents in the project that will be public facing (e.g. data.world documents).
- `scratch`: This directory contains output that will not be used in the project in its final form. Common cases are filtered tables or quick visualizations for reporters. This directory is not git tracked.

### Project setup instructions

After cloning the git repo:

Install Python dependencies:

```
pipenv install
```

*TK: For more complex or unusual projects additional directions follow*

### Methods and techniques

*TK: Make note of things in this project that are new, unique or clever that you might want to reuse in future projects.*

## Data notes

*Add important caveats, limitations, and source contact info here.*

## Data diary

*TK: Document the steps you take as you explore the data. This is particularly important for manual steps.*
