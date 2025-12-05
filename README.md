# Algoritmo-Financiero-Simulaciones-Monte-Carlo

El presente algoritmo realiza una simulación Monte Carlo para estimar pérdidas asociadas a aviones no registrados, considerando costos base, inflación, costo de oportunidad y factores estacionales mensuales. Genera un conjunto de resultados, estadísticas descriptivas (media, desviación, CV) y visualización mediante boxplot.

## Simulación de Pérdidas: Modelo Monte Carlo

Este proyecto implementa un modelo de simulación Monte Carlo para estimar pérdidas económicas derivadas de aviones no registrados. Considera costos base, tasas financieras diarias (inflación y costo de oportunidad) y factores estacionales mensuales, ofreciendo análisis estadístico y visualización clara.

## Key Features

* Simulación Estocástica: 1000 iteraciones por mes para estimar pérdidas bajo incertidumbre.

* Factores Financieros: Ajuste por inflación y costo de oportunidad calculados a nivel diario.

* Estacionalidad Mensual: Índices que reflejan variaciones en la demanda y riesgo por mes.

* Análisis Estadístico: Media, desviación estándar, mínimo, máximo y coeficiente de variación (CV).

* Visualización: Boxplot comparativo de pérdidas por mes para identificar dispersión y riesgo.

## Recursos Utilizados

* Lenguaje: Python

* Librerías: NumPy, Pandas, Matplotlib, Seaborn

## Estructura
El proyecto sigue una estructura simple y clara:
.
├── README.md
├── simulacion_perdidas.py
├── requirements.txt
└── /figuras
    └── boxplot_perdidas.png

