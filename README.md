# Physics-Guided Data Augmentation for Friction Stir Welding (FSW)

## Overview

This project implements a **physics-guided data augmentation pipeline** for predicting yield strength in the Friction Stir Welding (FSW) process.

Due to the limited availability of experimental welding data, synthetic samples are generated using a combination of:

* Response Surface Methodology (RSM)
* Design of Experiments (DOE)
* Physics-based feature engineering
* Latin Hypercube Sampling (LHS)

The augmented dataset can be used for machine learning models to predict mechanical properties of welded joints.

---

## Dataset Parameters

The experimental dataset contains the following process parameters:

| Parameter | Description           | Unit   |
| --------- | --------------------- | ------ |
| D         | Shoulder Diameter     | mm     |
| V         | Welding Speed         | mm/min |
| N         | Tool Rotational Speed | RPM    |
| Yield     | Yield Strength        | MPa    |

---

## Augmentation Methodology

### 1. Data Cleaning

Invalid data rows with zero process parameters were removed to ensure physically meaningful samples.

### 2. Feature Engineering

Three physics-derived features were computed:

**Heat Input Index**

HI = (N × D³) / V

**Rotational Pitch**

Pitch = V / N

**Tool Peripheral Velocity**

U = πDN

These features represent the thermo-mechanical behavior of the FSW process.

---

### 3. Response Surface Modeling

A quadratic regression model was trained using polynomial features to approximate the relationship between process parameters and yield strength.

---

### 4. Design of Experiments Sampling

Latin Hypercube Sampling was used to generate new combinations of welding parameters within realistic operating ranges:

| Parameter | Min | Max  |
| --------- | --- | ---- |
| D         | 10  | 20   |
| V         | 100 | 200  |
| N         | 600 | 1000 |

---

### 5. Synthetic Data Generation

The trained regression model predicts yield strength for the sampled parameter combinations.

This produces synthetic welding experiments consistent with the learned process behavior.

---

### 6. Physics Consistency Filtering

Synthetic samples are filtered to ensure predicted yield strength remains within physically realistic bounds.

---

## Output

The final augmented dataset includes:

* Original experimental data
* Synthetic DOE-generated samples
* Physics-derived features

Final dataset columns:

D | V | N | Yield | HeatInput | Pitch | ToolVelocity

---

## Installation

Install required dependencies:

```bash
pip install numpy pandas scikit-learn scipy matplotlib
```

---

## Running the Code

Rull all the cell of the Python Notebook
data_augmentation.ipynb

This will:

1. Load the experimental dataset
2. Train the RSM model
3. Generate synthetic samples
4. Produce an augmented dataset

---

## Applications

This augmented dataset can be used for:

* Machine learning model training
* Welding process optimization
* Predictive modeling of mechanical properties
* Process parameter sensitivity analysis

---

## Research Context

This project demonstrates how **physics-guided machine learning techniques** can improve predictive modeling in manufacturing processes with limited experimental data.

---

## Author

Mechanical Engineering Research Project
Advanced Welding Course
