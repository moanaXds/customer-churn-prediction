# Quick Start Guide

Get this project up and running in minutes!

## 📋 Prerequisites
- Python 3.8 or higher
- pip or conda package manager
- Git (for version control)

## 🚀 5-Minute Setup

### 1. Clone or Download
```bash
# If using git
git clone https://github.com/yourusername/customer-churn-prediction.git
cd customer-churn-prediction

# Or download as ZIP and extract
```

### 2. Create Virtual Environment
```bash
# On macOS/Linux
python3 -m venv venv
source venv/bin/activate

# On Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebooks
```bash
jupyter notebook
```

### 5. Run the Project
Open and execute notebooks in order:
- **notebooks/step 1.ipynb** (EDA & Exploration)
- **notebooks/step 2.ipynb** (Feature Engineering)
- **notebooks/step 3.ipynb** (Model Training)

---

## 📂 Project Structure

```
customer-churn-prediction/
├── README.md                     # Main project documentation
├── requirements.txt              # Python dependencies
├── .gitignore                    # Git ignore rules
├── LICENSE                       # MIT License
│
├── notebooks/
│   ├── step 1.ipynb             # EDA & Data Exploration
│   ├── step 2.ipynb             # Feature Engineering
│   └── step 3.ipynb             # Model Training & Evaluation
│
├── data/
│   ├── client_data.csv          # Raw customer data
│   ├── price_data.csv           # Raw pricing data
│   ├── clean_data_after_eda.csv # Step 1 output
│   └── data_for_predictions.csv # Step 2 output
│
├── models/
│   └── churn_model.pkl          # Trained model (Step 3 output)
│
└── docs/
    └── METHODOLOGY.md           # Technical documentation
```

---

## 🎯 What Each Notebook Does

### Step 1: Exploratory Data Analysis (EDA)
**Input**: Raw CSV files  
**Output**: `clean_data_after_eda.csv`  
**Tasks**:
- Load and inspect raw data
- Check data quality and missing values
- Generate summary statistics
- Visualize churn distribution
- Document findings

**Expected time**: 5-10 minutes

### Step 2: Feature Engineering
**Input**: Output from Step 1  
**Output**: `data_for_predictions.csv`  
**Tasks**:
- Convert datetime columns
- Merge datasets
- Create derived features from pricing data
- Engineer temporal features (price changes)
- Calculate price differentials

**Expected time**: 10-15 minutes

### Step 3: Model Training & Evaluation
**Input**: Output from Step 2  
**Output**: `churn_model.pkl` + Performance metrics  
**Tasks**:
- Split data into train/test sets
- Train Random Forest classifier
- Generate predictions
- Evaluate performance (accuracy, precision, recall)
- Analyze feature importances
- Export trained model

**Expected time**: 10-15 minutes

---

## 🔍 Using the Trained Model

```python
import pandas as pd
import joblib

# Load the trained model
model = joblib.load('models/churn_model.pkl')

# Prepare your data (must have same features as training)
new_data = pd.read_csv('your_customer_data.csv')
X_new = new_data.drop(columns=['id', 'churn'])

# Make predictions
predictions = model.predict(X_new)
probabilities = model.predict_proba(X_new)[:, 1]

# Get results
results = pd.DataFrame({
    'customer_id': new_data['id'],
    'predicted_churn': predictions,
    'churn_probability': probabilities
})

# Flag high-risk customers (>70% churn probability)
high_risk = results[results['churn_probability'] > 0.7]
print(f"Found {len(high_risk)} high-risk customers")
```

---

## 📊 Expected Results

After running all steps, you should see:
- **Accuracy**: ~89%
- **Precision**: ~88%
- **Recall**: ~91%
- **Model File**: `models/churn_model.pkl` (~10-50 MB)

---

## ⚠️ Troubleshooting

### Virtual environment not activating?
```bash
# Try this for zsh (newer Macs)
source venv/bin/activate

# Or for bash
source venv/bin/activate
```

### Import errors?
```bash
# Ensure you're in the virtual environment
which python  # Should show path to venv

# Reinstall requirements
pip install --upgrade -r requirements.txt
```

### Jupyter not found?
```bash
# Make sure you installed jupyter in venv
pip install jupyter notebook
```

---

## 🎓 Learning Resources

- **Pandas Documentation**: https://pandas.pydata.org/
- **Scikit-learn**: https://scikit-learn.org/
- **Jupyter Notebooks**: https://jupyter.org/
- **BCG X Forage**: https://www.forage.com/

---

## 📧 Need Help?

Check the [README.md](README.md) for more details or review the [METHODOLOGY.md](docs/METHODOLOGY.md) for technical documentation.

---

**Last Updated**: May 2024  
**Project Status**: ✅ Ready to Use
