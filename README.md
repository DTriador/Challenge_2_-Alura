# Sistema de Prediccion de Abandono de Clientes - TelecomX

## Descripcion del Proyecto
Este proyecto desarrolla un pipeline de Machine Learning para predecir la tasa de cancelacion (Churn) en una empresa de telecomunicaciones. El objetivo principal es identificar patrones de comportamiento en los usuarios para permitir la ejecucion de estrategias de retencion proactivas basadas en datos.

El analisis abarca desde la ingesta de datos en formato JSON anidado hasta el despliegue de modelos de clasificacion supervisada, evaluando el impacto de variables financieras y de permanencia en la lealtad del cliente.

## Estructura de Datos y Preprocesamiento
El conjunto de datos original de 7,267 registros fue sometido a un proceso de ETL (Extract, Transform, Load) que incluyo:
* **Normalizacion de Esquema:** Descomposicion de estructuras anidadas para su tratamiento tabular.
* **Gestion de Valores Nulos:** Identificacion y remocion de registros inconsistentes en la variable objetivo.
* **Ingenieria de Caracteristicas:** Codificacion de variables categoricas y estandarizacion de variables numericas (Tenure, MonthlyCharges, TotalCharges) mediante StandardScaler para eliminar sesgos de magnitud.
* **Tratamiento de Desbalanceo:** Aplicacion de SMOTE (Synthetic Minority Over-sampling Technique) sobre el conjunto de entrenamiento para equilibrar la representacion de la clase minoritaria (26.54%).



## Arquitectura de Modelado
Se implementaron y compararon dos enfoques algoritmos distintos:

1. **Regresion Logistica:** Modelo lineal basado en optimizacion, utilizado para establecer una linea base interpretable y evaluar la sensibilidad de las variables estandarizadas.
2. **Random Forest Classifier:** Modelo basado en ensamble de arboles de decision para capturar relaciones no lineales y jerarquicas entre las caracteristicas de consumo.

### Metricas de Evaluacion
La evaluacion se realizo mediante una particion estratificada (80% entrenamiento / 20% testeo), obteniendo los siguientes resultados:

| Modelo | Exactitud (Test) | Recall (Clase 1) | F1-Score | Observaciones |
| :--- | :--- | :--- | :--- | :--- |
| Regresion Logistica | 0.7275 | 0.7433 | 0.5915 | Modelo seleccionado por estabilidad |
| Random Forest | 0.7268 | 0.5882 | 0.5333 | Presento Overfitting severo (0.99 Train) |



## Hallazgos y Analisis de Relevancia
El analisis de coeficientes e importancia de variables determino que:
* La **antiguedad del cliente (Tenure)** es el factor mas determinante para la retencion; los primeros 12 meses representan el periodo de mayor criticidad operacional.
* Los **cargos mensuales elevados** actuan como un disparador directo de la cancelacion, indicando una elasticidad precio significativa en la base de usuarios.

## Propuestas de Implementacion (Business Intelligence)
Basado en el modelo de Regresion Logistica (Recall 74.33%), se recomiendan las siguientes acciones:
* Implementacion de un sistema de alertas tempranas para clientes en el primer quintil de antiguedad.
* Reestructuracion de contratos mensuales hacia modelos de permanencia anual mediante incentivos de valor agregado.
* Analisis de clusters para identificar segmentos con alta sensibilidad al precio y ofrecer planes de retencion personalizados.

## Tecnologias Utilizadas
* Python 3.x
* Pandas y NumPy (Manipulacion de datos)
* Scikit-Learn (Modelado y Preprocesamiento)
* Imbalanced-Learn (SMOTE)
* Matplotlib y Seaborn (Visualizacion de datos)

---
Proyecto desarrollado como parte del analisis de sistemas inteligentes para la toma de decisiones empresariales.
