# AI-for-Forensics

## System Requirements

### Hardware
- **Processor:** Intel Core i5 or equivalent (4+ cores)
- **RAM:** 8GB minimum (16GB recommended)
- **Storage:** 20GB free disk space
- **GPU:** Optional (NVIDIA CUDA for faster training)

### Software
- **OS:** Windows 10/11, macOS 10.14+, or Linux (Ubuntu 20.04+)
- **Python:** 3.8 or higher
- **pip:** Python package manager

## Quick Start

### 1. Environment Setup

**Option A: Automated Setup on Kali Linux (RECOMMENDED)**
```bash
chmod +x scripts/setup_kali.sh
./scripts/setup_kali.sh
source AIfF_env/bin/activate
```

**Option B: Automated Setup (Linux/macOS)**
```bash
chmod +x scripts/setup.sh
./scripts/setup.sh
source AIfF_env/bin/activate
```

**Option B: Manual Setup**
```bash
# Create virtual environment
python3 -m venv AIfF_env
source AIfF_env/bin/activate  # On Windows: AIfF_env\Scripts\activate

# Upgrade pip
pip install --upgrade pip

# Install dependencies
pip install -r requirements.txt
```

### 2. Verify Installation
```bash
python3 -c "import numpy, pandas, sklearn, tensorflow; print('✓ All packages installed')"
```

### 3. Run Lab Exercises

**Part 1: Exploratory Data Analysis**
```bash
python code/01_exploratory_analysis.py
```
This generates visualizations:
- correlation_matrix.png
- feature_distributions.png
- benign_vs_malicious.png
- class_distribution.png

**Part 2: Model Training**
```bash
python code/02_model_training.py
```
This trains three models and generates:
- model_comparison.png
- Saved models in models/ directory

**Part 3: Forensic Analysis**
```bash
python code/03_forensic_analysis.py
```
This analyzes the dataset and generates:
- analysis_results.csv
- forensic_analysis_report.txt
- analysis_visualization.png

## Troubleshooting

### Issue: ImportError for sklearn
```bash
pip install scikit-learn
```

### Issue: TensorFlow not found
```bash
pip install tensorflow
```

### Issue: Model training is slow
- Reduce dataset size
- Use fewer features
- Enable GPU acceleration
- Reduce number of epochs

### Issue: Out of memory
- Reduce batch size
- Use fewer features
- Reduce dataset size
- Close other applications

### Issue: Models not saved
- Check models/ directory exists
- Verify write permissions
- Check disk space

## Advanced Usage

### Custom Dataset
To use your own forensic dataset:

1. Prepare CSV with same columns as forensic_dataset.csv
2. Update dataset path in scripts
3. Run analysis with your data

### Hyperparameter Tuning
Modify hyperparameters in 02_model_training.py:

```python
# Random Forest
RandomForestClassifier(
    n_estimators=200,  # Increase for better accuracy
    max_depth=10,      # Decrease to reduce overfitting
    min_samples_split=10
)
```

### Model Deployment
To use trained models in production:

```python
import joblib

# Load model
model = joblib.load('models/random_forest_model.pkl')
scaler = joblib.load('models/random_forest_scaler.pkl')

# Prepare features
features = scaler.transform(new_data)

# Make prediction
prediction = model.predict(features)
probability = model.predict_proba(features)
```
