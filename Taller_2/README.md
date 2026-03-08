# Predicción de Hipertensión Arterial

Modelo de clasificación para estimar el riesgo de hipertensión a partir de variables demográficas, hábitos de vida y antecedentes médicos.

## Contexto

La hipertensión arterial es uno de los principales factores de riesgo de enfermedades cardiovasculares. Su detección temprana es difícil porque los síntomas suelen pasar desapercibidos. Este proyecto desarrolla modelos predictivos que pueden servir como herramienta de apoyo para screening inicial.

## Estructura del repositorio

```
├── Datos_hipertension.csv       # Dataset (1990 registros, 13 variables)
├── Diccionario_Datos.xlsx       # Descripción de variables
├── Taller_2_Mondragon_Javier.ipynb   # Notebook con análisis completo
└── README.md
```

## Dataset

| Variable | Tipo | Descripción |
|----------|------|-------------|
| Edad | Numérica | Edad del paciente |
| Ingesta_Sal | Numérica | Nivel de consumo de sal |
| Nivel_Stres | Numérica | Nivel de estrés (1-10) |
| Colesterol | Numérica | Colesterol total (mg/dL) |
| Duración_Sueño | Numérica | Horas de sueño promedio |
| BMI | Numérica | Índice de masa corporal |
| Glucosa | Numérica | Glucosa en sangre (mg/dL) |
| Medicación | Categórica | Tipo de medicación actual |
| Historia_Familiar | Categórica | Antecedentes familiares (Sí/No) |
| Actividad_Fisica | Categórica | Nivel de actividad (Baja/Moderada/Alta) |
| Fumador | Categórica | Fumador activo (Sí/No) |
| Enfermedad_Corazon | Categórica | Enfermedad cardíaca previa (Sí/No) |
| **Hipertension** | Categórica | **Variable objetivo** (Sí/No) |

## Metodología

### Preprocesamiento
- Eliminación de 4 registros duplicados
- Corrección de 3 valores anómalos en Colesterol (errores de tipeo)
- División 80/20 estratificada (random_state=77)

### Modelos evaluados

**Pipeline 1: Regresión Logística / SVC**
- Escaladores: StandardScaler, MinMaxScaler
- Encoders: OneHotEncoder, OrdinalEncoder
- Hiperparámetro C: [0.01, 0.1, 1, 10, 100]
- Optimización por Recall mediante GridSearchCV (5-fold)

**Pipeline 2: Árbol de Decisión**
- max_depth: [3, 5, 7, 10, None]
- min_samples_split: [2, 5, 10, 20]
- min_samples_leaf: [1, 2, 5, 10]
- criterion: [gini, entropy]

## Resultados

### Comparación de modelos en test

| Métrica | SVC | Árbol de Decisión |
|---------|-----|-------------------|
| Accuracy | 62.6% | **87.7%** |
| Precision | 58.2% | **84.4%** |
| Recall | **99.5%** | 93.7% |
| F1-Score | 73.4% | **88.8%** |

El Árbol de Decisión fue seleccionado como mejor modelo al dominar en 3 de 4 métricas.

### Intervalos de confianza (Bootstrap, 1000 iteraciones)

| Métrica | IC 95% | Amplitud |
|---------|--------|----------|
| Recall | [0.90, 0.97] | 0.066 |
| Precision | [0.80, 0.89] | 0.094 |

Ambas métricas muestran estabilidad moderada.

### Variables más importantes

| Variable | Importancia |
|----------|-------------|
| Colesterol | 89.7% |
| Glucosa | 10.3% |

### Reglas de decisión (profundidad 3)

```
Si Colesterol > 204.05 → Hipertensión = Sí
Si Colesterol ≤ 204.05 y Glucosa ≤ 119.45 → Hipertensión = No
Si Colesterol ≤ 204.05 y Glucosa > 119.45 y Colesterol > 182.15 → Hipertensión = Sí
```

## Requisitos

```
pandas
numpy
matplotlib
seaborn
scikit-learn
```

## Ejecución

```bash
# Clonar repositorio
git clone https://github.com/[usuario]/hypertension-prediction.git
cd hypertension-prediction

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar notebook
jupyter notebook Taller_2_Mondragon_Javier.ipynb
```

## Limitaciones

- El modelo utiliza únicamente Colesterol y Glucosa como predictores
- No reemplaza el diagnóstico clínico ni la medición directa de presión arterial
- Diseñado como herramienta de screening, no de diagnóstico definitivo

## Autor

Javier Mondragón  
MINE 4206 - Aprendizaje de Máquina  
Universidad de los Andes, 2026
