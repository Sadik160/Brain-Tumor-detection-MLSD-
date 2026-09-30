# MRI Tumor MLOps

A complete machine learning and MLOps workflow for detecting brain tumors from MRI scans using a deep learning model. This project demonstrates the end-to-end pipeline: data preparation, model training, experiment tracking, model registry, deployment-ready packaging, and reproducible automation.

## Project Overview

This repository is designed to train and manage a tumor classification model for MRI images. The workflow includes:

- MRI image preprocessing and labeling
- DVC-based data versioning
- Model training with PyTorch
- Experiment tracking using MLflow
- Configuration-driven pipeline structure
- CI/CD-friendly project organization
- Deployment-ready model packaging

## Project Structure

```text
mri_tumor_mlops/
├── .dvc/
├── .github/
├── .gitignore
├── README.md
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── model.py
│   ├── predict.py
│   └── utils.py
├── config/
│   ├── config.yaml
│   └── params.yaml
├── data/
│   ├── raw/
│   ├── processed/
│   └── labels/
├── model/
│   └── checkpoints/
├── notebooks/
│   └── exploration.ipynb
├── src/
│   ├── data/
│   │   ├── make_dataset.py
│   │   └── preprocess.py
│   ├── model/
│   │   ├── train.py
│   │   └── evaluate.py
│   └── pipeline/
│       └── train_pipeline.py
├── tests/
│   └── test_model.py
├── requirements.txt
├── setup.py
├── dvc.yaml
├── params.yaml
└── Makefile
```

## Features

- MRI classification pipeline for tumor detection
- Reproducible data and model versioning with DVC
- Modular project layout following MLOps best practices
- Model experiment tracking and comparison with MLflow
- Configurable hyperparameters and training settings
- Clean separation between source code, app code, and data assets
- Ready for extension to deployment via API or Docker

## Tech Stack

- Python 3.10+
- PyTorch
- OpenCV / PIL
- Scikit-learn
- MLflow
- DVC
- Hydra or YAML-based configuration
- FastAPI or Flask for inference service
- Docker (optional for deployment)

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/your-username/mri_tumor_mlops.git
cd mri_tumor_mlops
```

### 2. Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# or
.venv\Scripts\activate      # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

If the project uses editable installation:

```bash
pip install -e .
```

## Configuration

The project uses YAML config files to manage parameters for:

- model architecture
- training hyperparameters
- data paths
- preprocessing settings
- evaluation metrics

Typical config locations:

- `config/config.yaml`
- `config/params.yaml`
- `params.yaml`

Edit these files to tune training and pipeline behavior without changing source code.

## Data

This project expects MRI image datasets organized by class or folder structure, such as:

```text
data/
├── raw/
│   ├── yes/
│   └── no/
└── processed/
```

For DVC-managed data:

```bash
dvc pull
```

To track a new dataset:

```bash
dvc add data/raw
```

## Training

Train the model using your project pipeline:

```bash
python src/model/train.py
```

Or run the complete pipeline:

```bash
python src/pipeline/train_pipeline.py
```

If DVC is configured for pipeline reproducibility:

```bash
dvc repro
```

## Model Evaluation

Evaluation metrics can be computed with:

```bash
python src/model/evaluate.py
```

Typical metrics include:

- accuracy
- precision
- recall
- F1-score
- confusion matrix
- ROC-AUC

## Experiment Tracking

The project is structured for experiment logging with MLflow.

Start MLflow UI:

```bash
mlflow ui
```

Then open:

```text
http://localhost:5000
```

This helps compare runs, track hyperparameters, and store model artifacts.

## Inference

After training, the model can be used for inference through a Python script or app service.

Example:

```bash
python app/predict.py --image path/to/mri_scan.jpg
```

If an API is included:

```bash
uvicorn app.main:app --reload
```

## Testing

Run unit tests (if present):

```bash
pytest
```

## Deployment

This project is structured to be extended into deployment workflows such as:

- FastAPI prediction service
- Docker containerization
- Kubernetes deployment
- cloud deployment on AWS/GCP/Azure

Example packaging flow:

```bash
docker build -t mri-tumor-model .
docker run -p 8000:8000 mri-tumor-model
```

## DVC Workflow

This project uses DVC to version datasets and model artifacts.

Common commands:

```bash
dvc init
dvc add data/raw
dvc status
dvc repro
dvc push
```

## Git Workflow

```bash
git add .
git commit -m "Initial project setup"
git push origin main
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for details if included in the repository.

## Contributing

Contributions are welcome. Please open an issue or submit a pull request with a clear description of the proposed improvement.

## Contact

For questions or collaboration, contact the project owner or maintainer listed in the repository.

## Notes

This repository is intended as a practical MLOps example for brain MRI tumor classification. It can be used for learning, experimentation, and as a template for similar medical image classification projects.
