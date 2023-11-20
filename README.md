![barbell](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/a22db238-528c-4cc2-8cb2-2295f1e0d992)

# Fitness Tracker

Python scripts to process, visualize, and model accelerometer and gyroscope data to create a machine learning model that can classify barbell exercises and count repetitions. The project was created based on a course featured on YouTube by Dave Ebbelaar.

## Project Organization

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io

## Dataset

The dataset was collected using a Meta Motion sensor placed in a wristband worn by various individuals during the performance of five types of exercises: bench press, deadlift, overhead press, rowing, and squats. The sets were divided into medium (10 repetitions) and heavy (5 repetitions). All series data were recorded on a Bluetooth-connected phone and exported in .csv format.

 
## Processing Raw Data

All .csv files were readed, creating two separate DataFrames: one with accelerometer data and the other with gyroscope data. Next, both DataFrames were merged into one and a frequency conversion was performed:

![dataset](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/141f281e-57d4-463f-b9da-8d0ccf81f5df)
 

## Data Visualization

Various types of visualizations have been created to better understand the accelerometer and gyroscope data.

1.Compare medium vs. heavy sets

2.Compare participants

3.Compare exercises

 

## Detecting Outliers in Sensor Data

Checking whether there are any outliers (extreme values) in our data that we want to remove using various methods(IQR, Chauvenet’s Criterion, Local Outlier Factor (LOF))

The Chauvenet’s Criterion method was chosen, and the outliers detected using this method were replaced with NaN:

![output2](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/d3d00980-0b3f-4de1-8f7e-6292e31f67bd)


## Feature Engineering

Applying interpolation to fill rows with NaN values. Filter subtle noise (not outliers) and identify parts of the data that explain most of the variance. Then add numerical, temporal, frequency, and cluster features.

1. Butterworth lowpass filter

![output3](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/31e731f6-1cff-4d7c-afd5-aff12886a827)

2. Principal component analysis (PCA)

3. Sum of squares attributes

4. Discrete Fourier Transformation (DFT)

5. K-means Clustering

![output4](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/a09926b5-e112-4942-a2a5-2ce2f56151f2)

 

## Predictive Modelling

Experiment with feature selection, model selection and hyperparameter tuning with grid search to find the combination that results in the highest classification accuracy.

1. Generated separate sets for training and testing.

2. Divided the features into subsets.

3. Conducted forward feature selection employing a simple decision tree.

4. Executed a grid search to identify optimal hyperparameters and select the model.

5. Illustrated a grouped bar plot to compare the outcomes.

6. Identified the superior model and assessed its performance.

7. Segregated training and testing data based on individual participants.

8. Employed the best model again and assessed its performance.

![output5](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/c988cfdb-0525-4684-a638-08cf7bf6e348) 

## Counting Repetitions

Visualizing the data to spot patterns, configuring the LowPassFilter, applying and fine-tuning the LowPassFilter settings, developing a function to count repetitions, establishing a benchmark dataframe

![output](https://github.com/kacperpodgorski00/tracking_barbell_exercises/assets/73601611/3bc121ae-0f88-4f9c-905f-1f3476f13b4e)

