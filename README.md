# Automotive Intrusion Detection System (CAN & Telematics)

## Overview
This project implements a multi-layer Intrusion Detection System (IDS) for modern connected vehicles. It combines an in-vehicle CAN bus anomaly detection model (analyzing raw network traffic at the edge) with a cloud-based Telematics behavioral monitoring baseline. The system correlates alerts from both layers to generate high-confidence Vehicle Security Operations Center (vSOC) alerts.

## Project Structure
```text
automotive_ids_project/
├── data/                  # Raw CAN datasets (Ignored by Git)
├── models/                # Serialized model artifacts (.pkl, .keras)
├── notebooks/
│   ├── 01_can_exploration.ipynb        # CAN IDS feature engineering & model training
│   ├── 02_telematics_behavior.ipynb    # Telematics autoencoder baseline
│   └── 03_integration_deployment.ipynb # vSOC correlation logic & resource profiling
├── README.md              
└── requirements.txt       # Python environment dependencies

Setup Instructions
Clone the repository and navigate to the project root:

Bash
git clone <your-github-repo-url>
cd automotive_ids_project
Create and activate a virtual environment:
This project was developed using Windows. Run the following in your terminal:

Bash
python -m venv venv
.\venv\Scripts\activate
Install the required dependencies:

Bash
pip install -r requirements.txt
Set up the Jupyter kernel:
Open the notebooks in your IDE (e.g., VS Code) and ensure the venv Python interpreter is selected as your kernel.

Data Download Steps
Due to their massive size (~4M messages per scenario), the raw datasets are not included in this repository.

To run the notebooks, you must download the Car Hacking Dataset (HCRL).

Download the dataset files from the official HCRL repository (or provided academic link).

Create a folder named data/ in the root of this project.

Place the following extracted CSV files directly into the data/ folder:

DoS_dataset.csv

Fuzzy_dataset.csv

gear_dataset.csv

RPM_dataset.csv

Note: The notebooks use pandas chunking/sampling to manage memory, so loading these large files on a standard machine is safe.

Execution Pipeline
To reproduce the findings and regenerate the serialized models, execute the notebooks in the following order:

01_can_exploration.ipynb: Trains the XGBoost and Isolation Forest models for edge detection and calculates per-attack metrics.

02_telematics_behavior.ipynb: Extracts RPM/Speed proxies to simulate fleet-wide behavioral data and trains the cloud-based Autoencoder.

03_integration_deployment.ipynb: Runs the vSOC alert correlation engine and profiles the inference speed/memory footprint for automotive ECUs.