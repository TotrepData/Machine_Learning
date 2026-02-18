# Machine Learning - Universidad de los Andes

Repositorio del curso **MINE 4206 - Analisis con Machine Learning**  
Maestría en Ingenieria de la Información | 2026-10

---

## Taller 1 - Predicción de Demanda de Bicicletas

Desarrollo de un modelo predictivo para estimar la demanda de bicicletas en sistemas de alquiler urbano, aplicando el ciclo completo de Machine Learning.

### Modelos implementados
- Regresión Polinomial (grado 3) con regularización Ridge
- Regresión Lasso con regularización L1 (α=1)

### Resultados en conjunto de prueba

| Modelo | R² | RMSE | MAE |
|--------|:--:|:----:|:---:|
| Polinomial (grado=3) | 0.507 | 128.6 | 93.5 |
| Lasso (α=1) | 0.423 | 139.1 | 102.6 |

### Variables más influyentes (Modelo Lasso)
- Temperatura (+61.6)
- Parte del día - Noche (-48.3)
- Parte del día - Tarde (+39.7)
- Humedad (-27.7)

### Archivos
- `taller_1_{Mondragon_Javier}.ipynb` - Notebook con análisis completo
- `Datos_Bicicletas.csv` - Dataset
- `DiccionarioDatos_Bicicletas.xlsx` - Diccionario de variables

---

**Autor:** Javier Mondragón
