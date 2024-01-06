# MIMIC-IV
**MIMIC-IV data pipeline** is an end-to-end pipeline that offers a configurable framework to prepare MIMIC-IV data for the downstream tasks. 
The pipeline cleans the raw data by removing outliers and allowing users to impute missing entries. 
It also provides options for the clinical grouping of medical features using standard coding systems for dimensionality reduction.  
All of these options are customizable for the users, allowing them to generate a personalized  patient cohort. 
The customization steps can be recorded for the reproducibility of the overall framework. 
The pipeline produces a smooth time-series dataset by binning the sequential data into equal-length time intervals and allowing for filtering of the time-series length according to the user's preferences.
Besides the data processing modules, our pipeline also includes two additional modules for modeling and evaluation. 
For modeling, the pipeline includes several commonly used sequential models for performing prediction tasks. 
The evaluation module offers a series of standard methods for evaluating the performance of the created models. 
This module also includes options for reporting individual and group fairness measures.

##### Citing MIMIC-IV Data Pipeline:
MIMIC-IV Data Pipeline is available on [ML4H](https://proceedings.mlr.press/v193/gupta22a/gupta22a.pdf).
If you use MIMIC-IV Data Pipeline, we would appreciate citations to the following paper.

```
@InProceedings{gupta2022extensive,
  title = 	 {{An Extensive Data Processing Pipeline for MIMIC-IV}},
  author =       {Gupta, Mehak and Gallamoza, Brennan and Cutrona, Nicolas and Dhakal, Pranjal and Poulain, Raphael and Beheshti, Rahmatollah},
  booktitle = 	 {Proceedings of the 2nd Machine Learning for Health symposium},
  pages = 	 {311--325},
  year = 	 {2022},
  volume = 	 {193},
  series = 	 {Proceedings of Machine Learning Research},
  month = 	 {28 Nov},
  publisher =    {PMLR},
  url = 	 {https://proceedings.mlr.press/v193/gupta22a.html}
}
```

## Table of Contents:
- [Steps to download MIMIC-IV dataset for the pipeline](#Steps-to-download-MIMIC-IV-dataset-for-the-pipeline)
- [Repository Structure](#Repository-Structure)
- [How to use the pipeline?](#How-to-use-the-pipeline)

### Steps to download MIMIC-IV dataset for the pipeline

Go to https://physionet.org/content/mimiciv/1.0/

Follow instructions to get access to MIMIC-IV dataset.

Download the files using your terminal: wget -r -N -c -np --user mehakg --ask-password https://physionet.org/files/mimiciv/1.0/

### Repository Structure

- **mainPipeline.ipynb**
	is the main file to interact with the pipeline. It provides step-step by options to extract and pre-process cohorts.
- **./data**
	consists of all data files stored during pre-processing
	- **./cohort**
		consists of files saved during cohort extraction
	- **./features**
		consist of files containing features data for all selected features.
	- **./summary**
		consists of summary files for all features.
	 	It also consists of file with list of variables in all features and can be used for feature selection.
	- **./dict**
		consists of dictionary structured files for all features obtained after time-series representation
	- **./output**
		consists output files saved after training and testing of model. These files are used during evaluation.
- **./mimic-iv-1.0**
	consist of files downloaded from MIMIC-IV website.
- **./saved_models**
	consists of models saved during training.
- **./preprocessing**
	- **./day_intervals_preproc**
		- **day_intervals_cohort.py** file is used to extract samples, labels and demographic data for cohorts.
		- **disease_cohort.py** is used to filter samples based on diagnoses codes at time of admission
	- **./hosp_module_preproc**
		- **feature_selection_hosp.py** is used to extract, clean and summarize selected features for non-ICU data.
		- **feature_selection_icu.py** is used to extract, clean and summarize selected features for ICU data.
- **./model**
	- **train.py**
		consists of code to create batches of data according to batch_size and create, train and test different models.
	- **Mimic_model.py**
		consist of different model architectures.
	- **evaluation.py**
		consists of class to perform evaluation of results obtained from models.
		This class can be instantiated separated for use as standalone module.
	- **fairness.py**
		consists of code to perform fairness evaluation.
		It can also be used as standalone module.
	- **parameters.py**
		consists of list of hyperparameters to be defined for model training.
	- **callibrate_output**
		consists of code to calibrate model output.
		It can also be used as standalone module.

### How to use the pipeline?
- After downloading the repo, open **mainPipeline.ipynb**.
- **mainPipeline.ipynb**, contains sequential code blocks to extract, preprocess, model and train MIMIC-IV EHR data.
- Follow each code block and read intructions given just before each code block to run code block.
- Follow the exact file paths and filenames given in instructions for each code block to run the pipeline.
- For evaluation module, clear instructions are provided on how to use it as a standalone module.
