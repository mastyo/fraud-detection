# 🔍 Detector de Fraude en Tarjetas de Crédito

Modelo de Machine Learning para detectar transacciones fraudulentas en tiempo real.

## 📋 Problema de Negocio

Las empresas financieras pierden miles de millones anuales por fraude con tarjetas de crédito. Este proyecto desarrolla un clasificador que identifica transacciones sospechosas, permitiendo bloquearlas antes de que se concreten.

**Desafío principal**: El dataset tiene un desbalance extremo (99.83% transacciones legítimas vs 0.17% fraudes), lo que requiere técnicas especiales de manejo de clases desbalanceadas.

## 📊 Dataset

- **Fuente**: [Kaggle - Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Transacciones**: 284,807
- **Fraudes**: 492 (0.17%)
- **Features**: 28 componentes PCA (anonimizados) + Amount + Time

## 🔬 Metodología

1. **EDA**: Análisis de distribuciones, correlaciones y patrones de fraude
2. **Preprocessing**: Escalado de Amount, ingeniería de feature Hour
3. **Modelado**: Comparación de 4 modelos (LogReg, RF, XGBoost, XGBoost balanceado)
4. **Tuning**: RandomizedSearchCV para optimización de hiperparámetros

## 📈 Resultados

| Modelo | Precision | Recall | F1 | AUC-ROC |
|--------|-----------|--------|-----|---------|
| Logistic Regression | 0.83 | 0.65 | 0.73 | 0.9559 |
| Random Forest | 0.94 | 0.81 | 0.87 | 0.9528 |
| XGBoost | 0.89 | 0.79 | 0.83 | 0.9319 |
| **XGBoost Balanceado** | **0.88** | **0.85** | **0.86** | **0.9726** |

**Mejor modelo**: XGBoost con `scale_pos_weight=577`
- Detecta **85%** de los fraudes
- Solo **12%** de falsos positivos
- AUC-ROC de **0.9726**

## 🔑 Features más importantes

1. **V14** (58% importancia)
2. **V4** (7%)
3. **V12** (4%)

## 💡 Insights

- Los fraudes tienen mediana de $9 (testeo de tarjeta) pero media de $122 (golpes grandes)
- El balanceo de clases fue crítico para mejorar el Recall de 65% a 85%
- El tuning de hiperparámetros no mejoró vs el modelo balanceado simple

## 🚀 Cómo ejecutar
```bash
# Clonar repositorio
git clone https://github.com/mastyo/fraud-detection.git
cd fraud-detection

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar notebook
jupyter notebook notebooks/fraud_detection.ipynb
```

## 📁 Estructura
fraud-detection/
├── README.md
├── requirements.txt
├── notebooks/
│   └── fraud_detection.ipynb
├── models/
│   ├── fraud_detector_model.pkl
│   └── amount_scaler.pkl
└── data/
└── (descargar de Kaggle)

## 🔮 Mejoras futuras

- [ ] Implementar SMOTE para oversampling
- [ ] Probar LightGBM y CatBoost
- [ ] Crear API REST con FastAPI para predicciones en tiempo real
- [ ] Agregar monitoreo de drift del modelo

## 🛠️ Tech Stack

- Python 3.10+
- pandas, numpy
- scikit-learn
- XGBoost
- matplotlib, seaborn

## 📝 Autor

Marco Andrés Sánchez Tejeda - [[LinkedIn](https://www.linkedin.com/in/mastpp/)]
