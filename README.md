# Heart Disease Prediction Model ❤️

A machine learning project that predicts cardiovascular disease risk using K-Nearest Neighbors (KNN) classification. This model analyzes clinical and demographic factors to identify patients at risk of heart disease, potentially helping prevent premature deaths through early detection.

## 📊 Project Overview

According to the WHO, 17.9 million people die from cardiovascular diseases (CVDs) every year. This project aims to identify risk factors early using anonymized hospital data from multiple medical facilities.

**Key Results:**
- 🎯 **82% accuracy** on test data
- 🔍 **6 key features** selected through correlation analysis
- ⚡ **Optimized hyperparameters** using GridSearchCV
- 📈 **Comprehensive EDA** with data visualization

## 🗂️ Dataset Information

The dataset contains **918 patient records** with the following features:

| Feature | Description | Type |
|---------|-------------|------|
| Age | Patient age (28-77 years) | Numerical |
| Sex | Patient gender (M/F) | Categorical |
| ChestPainType | Type of chest pain (TA, ATA, NAP, ASY) | Categorical |
| RestingBP | Resting blood pressure (mm Hg) | Numerical |
| Cholesterol | Serum cholesterol (mm/dl) | Numerical |
| FastingBS | Fasting blood sugar (>120 mg/dl) | Binary |
| RestingECG | Resting ECG results (Normal, ST, LVH) | Categorical |
| MaxHR | Maximum heart rate (60-202) | Numerical |
| ExerciseAngina | Exercise-induced angina (Y/N) | Binary |
| Oldpeak | ST depression value | Numerical |
| ST_Slope | Peak exercise ST segment slope | Categorical |
| HeartDisease | Target variable (1: disease, 0: normal) | Binary |


## 📈 Model Development Process

### 1. Exploratory Data Analysis (EDA)
- **Age distribution**: Patients aged 28-77 years
- **Gender split**: ~80% male patients
- **Heart disease prevalence**: 55% of observations have heart disease
- **Data quality issues**: Identified zero values in RestingBP and Cholesterol

### 2. Data Cleaning
- Removed 1 row with RestingBP = 0
- Imputed 172 zero Cholesterol values with mean (199)
- No missing values detected

### 3. Feature Engineering
- Applied one-hot encoding to categorical variables
- Calculated correlation with target variable
- Selected top 6 features based on correlation strength:
  1. **ST_Slope_Up** (0.62 correlation)
  2. **ST_Slope_Flat** (0.55 correlation)
  3. **ChestPainType_ASY** (0.52 correlation)
  4. **ExerciseAngina_Y** (0.50 correlation)
  5. **ExerciseAngina_N** (0.50 correlation)
  6. **Oldpeak** (0.40 correlation)

### 4. Model Training & Evaluation

#### Single Feature Performance
- **Best single feature**: ST_Slope_Up (78.80% accuracy)
- **Worst single feature**: Oldpeak (62.50% accuracy)

#### Multi-Feature Model
- **All 6 features**: 81.52% validation accuracy
- **Scaling**: Applied MinMaxScaler for optimal performance

#### Hyperparameter Optimization
Used GridSearchCV with the following parameters:
- `n_neighbors`: [5, 10, 50, 100]
- `weights`: ['uniform', 'distance']
- `algorithm`: ['ball_tree', 'brute']
- `leaf_size`: [30, 40, 50]

**Best Parameters:**
- `algorithm`: 'brute'
- `leaf_size`: 30
- `n_neighbors`: 10
- `weights`: 'uniform'

## 📊 Results

| Metric | Score |
|--------|-------|
| Cross-validation Accuracy | 85.53% |
| Test Accuracy | 82.07% |
| Data Split | 60% Train / 20% Validation / 20% Test |

## 🔍 Key Insights

1. **ST Slope features** are the strongest predictors of heart disease
2. **Asymptomatic chest pain** is highly correlated with heart disease risk
3. **Exercise-induced angina** is a significant risk factor
4. **Cholesterol levels** showed surprisingly low correlation (0.01)
5. **Age and gender** have moderate predictive power

## ⚠️ Limitations & Considerations

- **Sample size**: Only ~1,000 observations may limit generalization
- **Medical context**: Should be used as a screening tool, not diagnostic
- **Data bias**: 80% male patients may affect female prediction accuracy
- **Feature selection**: Additional features might improve performance

## 🔮 Future Improvements

1. **Increase dataset size** for better generalization
2. **Explore additional features** with high correlation
3. **Try ensemble methods** (Random Forest, Gradient Boosting)
4. **Implement cross-validation** strategies
5. **Add feature importance analysis**
6. **Deploy as web application** for clinical use
