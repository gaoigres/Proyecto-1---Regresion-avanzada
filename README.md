# Predicción de Precios de Bienes Raíces en Australia - Regresión Avanzada

## Índice

- [Índice](#índice)
- [Introducción](#introducción)
  - [Métodos Utilizados](#métodos-utilizados)
  - [Tecnologías](#tecnologías)
- [Descarga y Configuración](#descarga-y-configuración)
  - [Requisitos Previos](#requisitos-previos)
  - [Cómo Ejecutar](#cómo-ejecutar)
- [Declaración del Problema](#declaración-del-problema)
  - [Objetivo Comercial](#objetivo-comercial)
  - [Preparación de Datos](#preparación-de-datos)
  - [Construcción y Evaluación del Modelo](#construcción-y-evaluación-del-modelo)
  - [Conclusiones](#conclusiones)
    - [Regresión Ridge](#regresión-ridge)
    - [Regresión Lasso](#regresión-lasso)
    - [Regresión ElasticNet](#regresión-elasticnet)
    - [Las Variables Más Significativas Son](#las-variables-más-significativas-son)

## Introducción

El presente proyecto tiene como propósito aplicar técnicas de **regresión avanzada** para predecir el precio de viviendas en Australia, utilizando un conjunto de datos con más de 80 variables entre numéricas y categóricas. Se emplean modelos de **regresión lineal regularizada** (Ridge, Lasso y ElasticNet) para mejorar la estabilidad del modelo y evitar el sobreajuste.

### Métodos Utilizados
* Limpieza y preparación de datos con imputación por mediana y moda.
* Codificación de variables categóricas mediante `OneHotEncoder(handle_unknown='infrequent_if_exist')`.
* Escalado estandarizado con `StandardScaler`.
* Validación cruzada con `GridSearchCV` para optimizar hiperparámetros.
* Evaluación mediante R² y RMSE.

### Tecnologías
* Python 3.12
* Pandas, NumPy, Matplotlib, Seaborn
* Scikit-learn
* Jupyter Notebook

## Descarga y Configuración

### Requisitos Previos

Este proyecto requiere tener **Anaconda** instalado en el sistema.  
Para más detalles sobre la instalación, visite:  
[Documentación oficial de Anaconda](https://docs.anaconda.com/anaconda/install/index.html)

### Cómo Ejecutar

1. Clonar o descargar este repositorio.  
2. Abrir el archivo `.ipynb` en Jupyter Notebook o JupyterLab.  
3. Ejecutar todas las celdas secuencialmente.  

---

## Declaración del Problema

### Objetivo Comercial

El objetivo principal es construir un modelo predictivo capaz de **estimar el precio de venta de una vivienda (SalePrice)** a partir de sus características físicas, estructurales y de ubicación.  
El modelo debe balancear precisión, interpretabilidad y estabilidad estadística.

### Preparación de Datos

Se aplicó una limpieza integral del dataset:  
- Eliminación de duplicados.  
- Imputación de valores faltantes:  
  - Mediana para variables numéricas.  
  - Moda para variables categóricas.  
- Escalado de variables y codificación con manejo robusto de categorías infrecuentes.

El dataset final tiene **1460 observaciones y 81 columnas**.

### Construcción y Evaluación del Modelo

Los modelos fueron entrenados usando validación cruzada de 5 pliegues.  
Se optimizó el hiperparámetro `alpha` (y `l1_ratio` en ElasticNet) para minimizar el RMSE.

| Modelo | R² (Train) | R² (Test) | RMSE (Test) | α óptimo |
|---------|------------|------------|--------------|-----------|
| Ridge | 0.897 | 0.878 | 30,535 | 5.62 |
| Lasso | 0.882 | 0.861 | 31,214 | 0.001 |
| ElasticNet | 0.887 | 0.868 | 30,981 | 0.004 |

---

## Conclusiones

### Regresión Ridge

El modelo **Ridge** demostró el mejor equilibrio entre sesgo y varianza, manteniendo un desempeño alto y estable. La regularización L2 evitó la sobreajuste y permitió conservar todas las variables significativas.  
- R² de prueba: **0.878**  
- RMSE: **30,535**  
- Excelente generalización y bajo error residual.

### Regresión Lasso

La **Regresión Lasso**, con penalización L1, logró simplificar el modelo al reducir coeficientes de variables poco influyentes.  
- R² de prueba: **0.861**  
- RMSE: **31,214**  
- Ventaja principal: **selección automática de variables**, aunque con leve pérdida de precisión frente a Ridge.

### Regresión ElasticNet

El modelo **ElasticNet** combinó las ventajas de Lasso y Ridge mediante un balance entre L1 y L2.  
- R² de prueba: **0.868**  
- RMSE: **30,981**  
- Desempeño intermedio, estable y adecuado para escenarios con correlación entre variables.

### Las Variables Más Significativas Son

Las variables con mayor correlación con el precio de venta fueron:  
- `OverallQual` (calidad general de la vivienda)  
- `GrLivArea` (área habitable sobre el suelo)  
- `GarageCars` (capacidad del garaje)  
- `TotalBsmtSF` (superficie total del sótano)  

Estas variables explican la mayor parte de la variabilidad en los precios, confirmando la influencia de la **calidad, tamaño y equipamiento estructural**.

---

**Conclusión General:**  
El modelo **Ridge Regression** se recomienda como el más robusto para este problema, alcanzando un rendimiento estable (R² ≈ 0.88) y un RMSE competitivo. Los modelos regularizados demostraron que es posible lograr alta precisión sin recurrir a modelos no lineales más complejos, manteniendo la interpretabilidad del modelo lineal.

---
