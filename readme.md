# AP Python Cookiecutter

This is a project template powered by [Cookiecutter](https://github.com/cookiecutter/cookiecutter) for use with [datakit-project](https://github.com/associatedpress/datakit-project/).

It is a fork of [associatedpress/cookiecutter-python-project](https://github.com/associatedpress/cookiecutter-python-project) with these differences:

- Subdirectory for Jupyter notebooks, similar to how [associatedpress/cookiecutter-r-project](https://github.com/associatedpress/cookiecutter-r-project) has an `analysis/markdown` directory. This acknowledges that there are both scripts to prepare or analyze data as well as notebooks.
- Makefile for running ETL pipeline steps. Inspired by [Making Data, the DataMade Way](https://github.com/datamade/data-making-guidelines).
- Placeholder for "What's in here?", "Methods and techniques" and "Data diary" sections in the README.md template.
- Use make rules and rclone to upload HTML versions of notebooks to S3 and data to Google Drive.
  - TODO: Consider writing a DataKit plugin to share the notebooks.
  - TODO: Consider using [quickhand/datakit-data-gdrive](https://bitbucket.org/quickhand/datakit-data-gdrive/src/master/) for data sharing.
- `settings.py` file similar to Django's, mostly for handling path resolution.

**Structure**

```
.
├── README.md
├── analysis
│   └── archive
├── data
│   ├── documentation
│   ├── html_reports
│   ├── manual
│   ├── processed
│   ├── public
│   └── source
├── etl
├── publish
└── scratch
```

- `README.md`
  - Project-specific readme with boilerplate for data projects.
- `analysis`
  - This is where we keep all of our jupyter ipython notebooks that contain analysis for the project.
    - Notebooks in this folder can ingest data from either `data/source` (if that data comes from the source in a workable format) or `data/processed` (if the data required some prep).
    - Dataframes from analysis notebooks should be written out to `data/processed`
  - `analysis/archive`: Notebooks that leave the scope of the project but should also remain in the project history will be placed here.
- `data`
  - This is the directory used with our `datakit-data` plugin.
  - `data/documentation`
    - Documentation on data files should go here - data dictionaries, manuals, interview notes.
  - `data/html_reports`
    - Contains rendered html of our analysis notebooks, the results of calling `jupyter nbconvert` on a notebook.
  - `data/manual`
    - Contains data that has been manually altered (e.g. excel workbooks with inconsistent string errors requiring eyes on every row).
  - `data/processed`
    - Contains data that has either been transformed from an `etl` script or output from an `analysis` jupyter notebook.
    - Data that has been transformed from an `etl` script will follow a naming convention: `etl_{file_name}.[csv,json...]`
  - `data/public`
    - Public-facing data files go here - data files which are 'live'.
  - `data/source`: contains raw, untouched data.
- `etl`
  - This is where we keep python scripts involved with collecting data and prepping it for analysis.
  - These files should be scripts, they should not be jupyter notebooks.
- `publish`
  - This directory holds all the documents in the project that will be public facing (e.g. data.world documents).
- `scratch`
  - This directory contains output that will not be used in the project in its final form.
  - Common cases are filtered tables or quick visualizations for reporters
  - This directory is not git tracked.

**Our `.gitignore`**

```
.DS_Store

.ipynb_checkpoints

data/
!data/source/.gitkeep
!data/manual/.gitkeep
!data/processed/.gitkeep
!data/html_reports/.gitkeep
!data/public/.gitkeep
!data/documentation/.gitkeep

scratch/
!scratch/.gitkeep
```

## Usage

These steps assume configuration for [datakit-project](https://github.com/associatedpress/datakit-project) are complete.

- If you'd like to keep a local version of this template on your computer, git clone this repository to where your cookiecutters live:

```
cd path/to/.cookiecutters
git clone git@github.com/associatedpress/cookiecutter-python-project
```

- Now, when starting a new project with `datakit-project`, reference the cookiecutter in your filesystem

```
datakit project create --template path/to/.cookiecutters/cookiecutter-python-project`
```

If you'd like to avoid specifying the template each time, you can edit `~/.datakit/plugins/datakit-project/config.json` to use this template by default:

```
 {"default_template": "/path/to/.cookiecutters/cookiecutter-python-project"}
```

## Configuration

You can set the default name, email, etc. for a project in the `cookiecutter.json` file.
