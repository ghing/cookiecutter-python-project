# ETL pipeline for this project.

PROJECT_SLUG := {{ cookiecutter.project_slug }}

# Variables for source, processed and other data.

DATA_DIR := data
DATA_DIR_SRC := $(DATA_DIR)/source
DATA_DIR_MANUAL := $(DATA_DIR)/manual
DATA_DIR_PROCESSED := $(DATA_DIR)/processed
DATA_DIR_PUBLIC := $(DATA_DIR_PUBLIC)

# Directory containing data processing and analysis notebooks
ANALYSIS_DIR := analysis
NOTEBOOK_DIR := $(ANALYSIS_DIR)/notebooks

# Path, using rclone configuration syntax of the root of the project folder on
# Google Drive. Data files and other output can be uploaded here for sharing.
# You will need to configure this in your rclone configuration.
DRIVE_PROJECT_ROOT :=

# Location where rendered versions of notebooks will be uploaded for sharing
# using rclone.
RCLONE_S3_REMOTE :=

# Include Makefiles for data components
# These should be put in the `etl` directory, .e.g.
# include etl/acs_2018.mk

.PHONY: share_data share_notebooks

# Share notebooks
# Add paths to HTML versions of notebooks to upload them to S3 when you run
# `make share_notebooks`.
SHARED_NOTEBOOKS =

share_notebooks: $(SHARED_NOTEBOOKS) index.html
	for f in $^; \
	do \
	  rclone copy $$f $(RCLONE_S3_REMOTE)/$(PROJECT_SLUG)/$(NOTEBOOK_DIR); \
	done; \
	rclone copy index.html $(RCLONE_S3_REMOTE)/$(PROJECT_SLUG)

# Pattern rule for rendering Jupyter notebooks as HTML.
# See https://groups.google.com/forum/#!topic/jupyter/W2M_nLbboj4 for more on
# the technique I use to hide input/output of cells.
$(NOTEBOOKS_DIR)/%.nb.html: $(NOTEBOOKS_DIR)/%.ipynb
	PYTHONPATH=$$(pwd) pipenv run jupyter nbconvert \
	  --to html \
	  --output $(notdir $@) \
	  --TagRemovePreprocessor.remove_input_tags={\"echo_false\"} \
	  --TagRemovePreprocessor.remove_all_outputs_tags={\"results_hide\"} \
	  $^

# Create an HTML version of the README to view with the notebooks
index.html: README.md
	pandoc -o $@ $<

# Share data using Google Drive.
# Add paths to data files that you want to be shared to Google Drive.
SHARED_DATA =

share_data: $(SHARED_DATA)
	for f in $^; \
	do \
	  data_subdir=$$(dirname $$f); \
	  rclone copy $$f $(DRIVE_PROJECT_ROOT)/$$data_subdir; \
	done
