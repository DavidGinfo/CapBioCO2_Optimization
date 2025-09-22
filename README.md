# Creation of a Data Model for Machine Learning using Sensor Data from a CO<sub>2</sub> Absorption Plant for Biogas

## Introduction

The data for this project comes from a facility belonging to the CapBioCO2 research project at Karlsruhe University of Applied Sciences. The aim of the facility is to absorb as much of the CO<sub>2</sub> contained in biogas as possible in order to increase the ecological sustainability of the biogas. In addition, the facility's process produces a salt solution as a by-product, which can be used for drinking water treatment from fermentation residues, for example.

The aim of this project is to first organize the collected data into a structure in which it can be further processed and evaluated. Since the underlying processes for the functioning of the plant are not so easy to simulate, the next step is to perform modeling based on the pre-processed data. Based on the models, optimization methods will then be applied to find the best possible combination of adjustable input parameters so that the average percentage of salt removal is highest. Another output variable is to maximize the percentage of treated water.

## Project Setup

In order to set up the project properly, a few programs are necessary/recommended.

### Prerequisites

Installation of the following programs:

- [Git](https://git-scm.com/downloads/win)
- [Visual Studio Code](https://code.visualstudio.com/Download)
- [Python](https://www.python.org/downloads/) (Version >=3.10)
- [Poetry](https://pypi.org/project/poetry/) (Version >=2.1.3)

### Initial Steps

To ensure that the notebooks function properly, the following steps are recommended to set up the project:

1. Clone Git Repository
    ```bash
    git clone https://github.com/DavidGinfo/CapBioCO2_Optimization
    ```
2. Create a virtualenv and activate it for current project
    ```bash
    poetry env use py
    ```
    If you do not want to use the standard Python installation, you must specify a path to the desired Python interpreter instead of *py*.

3. Install python packages and dependencies
    ```bash
    poetry install
    ```

4. Select Python Interpreter of created virtualenv as the Jupyter Notebooks Kernel. The Interpreter of the virtualenv should be suggested automatically.


## Project Structure

```
├── cached_objects
│   ├── model_gbrt
│   ├── model_lin_reg
│   ├── model_random_forest
│   └── prepared_data
├── data
│   ├── processed
│   └── raw
├── notebooks
│   ├── modelling
│   ├── optimization
│   ├── preparation
│   └── suggestion
├── .gitignore
├── poetry.lock
├── pyproject.toml
└── README.md
```

All cached objects and Numpy data structures are stored in the `cached_objects` directory and there in the respective model subfolder. The original data (Excel spreadsheet) is stored under the path `data/raw` and the preprocessed data is then stored as CSV files in the folder `data/processed`. The Jupyter notebooks are divided into four subfolders and organized according to *models*, *optimization methods*, *data preprocessing*, and *measurement prediction*.

## Manual

The project is generally divided into four sections, but their order is at least partially interdependent.

1. **Data Preprocessing**

    Here, the original data from the various test runs is processed into a format that can be reused in the next steps.

2. **Modeling**

    During modeling, the preprocessed data is used for a total of three different modeling approaches:
    - *Linear regression:* Represent features as quadratic terms and calculate the coefficients using linear regression
    - *Random forest regression*
    - *Gradient boosting regression (GBRT)*

3. **Optimization Methods**

    The primary optimization method used here is *extreme value search* for the quadratic model. Another optimization method used here in a simplified form is *Bayesian optimization*.

4. **Approach for Input Value Prediction**

    This section is independent of the previous two steps and is intended to use *Bayesian Optimization* to predict a measured value that can be used in the next experiment to better approximate the objective function.
