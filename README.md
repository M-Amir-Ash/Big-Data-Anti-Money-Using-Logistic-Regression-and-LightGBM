# SAML-D AML Big Data Fraud Detection

Big Data Anti-Money Laundering Detection Using Graph-Based Feature Engineering, Imbalanced Learning, and Explainable Machine Learning.

## MAIN WORKFLOW

Run only this notebook:

```text
notebooks/AML_BigData_Final_Project.ipynb
```

This is the single main Jupyter notebook for the final project. It contains the complete end-to-end workflow: project introduction, dataset loading, Big Data justification, PySpark setup, EDA, preprocessing, feature engineering, graph-based feature engineering, sampling, model training, evaluation, visualization, interpretation, and report-ready conclusion.

The notebook is also the main report and presentation material. It displays the important outputs directly inside the notebook:

- dataset summary tables
- EDA tables and interpretations
- preprocessing summary
- feature engineering summary
- sampling summary
- model configuration and comparison tables
- threshold tuning table
- matplotlib figures
- report-ready result interpretation and final conclusion

Old split notebooks have been removed. The only notebook workflow is `notebooks/AML_BigData_Final_Project.ipynb`.

## Dataset Download

Kaggle dataset:

```bash
kaggle datasets download -d berkanoztas/synthetic-transaction-monitoring-dataset-aml
```

Extract the archive and put the CSV file into:

```text
data/raw/
```

The notebook searches for CSV files inside `data/raw/`.

For the provided `SAML-D.csv`, the actual target column is:

```text
Is_laundering
```

The notebook normalizes this into the binary model label `label`, where `1` means laundering/suspicious and `0` means normal. The typology column `Laundering_type` is kept for analysis and excluded from model training to avoid leakage.

## Installation

Install requirements:

```bash
pip install -r requirements.txt
```

PySpark requires Java to be installed and available on your `PATH`.

## Run Jupyter

Start Jupyter from the project root:

```bash
jupyter notebook
```

Then open:

```text
notebooks/AML_BigData_Final_Project.ipynb
```

## Big Data Design

PySpark is used for Big Data processing: CSV loading, schema inspection, EDA aggregation, preprocessing, feature engineering, graph-based aggregation, and Parquet output.

The full dataset is never converted to Pandas. Only aggregated outputs or the controlled model-training sample are converted to Pandas.

## Model Training Scope

Model training uses a controlled sample for laptop feasibility:

- All suspicious transactions are kept.
- Normal transactions are sampled.
- The Pandas training sample is capped at 500,000 rows by default.

## Outputs

The `outputs/` folder contains backup exported files. The primary deliverable remains the notebook with visible inline report outputs.

- `data/processed/`: preprocessed and feature-engineered Parquet datasets.
- `data/sample/`: controlled training sample and train/validation/test splits.
- `outputs/figures/`: matplotlib visualizations.
- `outputs/metrics/`: class distribution, sampling summary, model metrics, threshold tuning, and confusion matrices.
- `outputs/models/`: trained Logistic Regression and LightGBM models.
- `outputs/reports/`: EDA summary, feature list, evaluation summary, and report-ready markdown files.

## Recommended Run

Run all cells from top to bottom:

```text
notebooks/AML_BigData_Final_Project.ipynb
```

Do not run only the model-training or visualization cells first, because those sections depend on outputs created by earlier cells.
