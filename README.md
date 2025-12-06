# Simulación Monte Carlo de Pérdidas por Aviones no Registrados

## Propósito

 Estimar pérdidas económicas de aviones no registrados, incorporando costos base, tasas financieras diarias (inflación y costo de oportunidad) y estacionalidad mensual, mediante simulación de Monte Carlo.

## Índice

* Key Features

* Fundamentos Matemáticos

* Parámetros del Modelo

* Pseudocódigo

* Suposiciones y Alcances

* Validación y Calidad de Resultados

* Reproducibilidad

* Extensiones Sugeridas


## Key Features

* Simulación Monte Carlo: 1000 iteraciones por mes para estimar pérdidas bajo incertidumbre.

* Factores Financieros: Ajuste por inflación y costo de oportunidad calculados a nivel diario.

* Estacionalidad Mensual: Índices que reflejan variaciones en la demanda y riesgo por mes.

* Análisis Estadístico: Media, desviación estándar, mínimo, máximo y coeficiente de variación (CV).

* Visualización: Boxplot comparativo de pérdidas por mes para identificar la dispersión y el riesgo.

## Fundamentos Matemáticos

* Conversión de tasas anuales a diarias

<img width="263" height="106" alt="image" src="https://github.com/user-attachments/assets/8e3243f3-3743-4af9-9524-a8ecddfd5d54" />

* Componentes financieros por simulacion

Ajuste por Inflacion: 

<img width="194" height="53" alt="image" src="https://github.com/user-attachments/assets/6e5b68f4-34d8-43b0-8592-e7b9744cdc66" />

Costo de oportunidad (rendimiento dejado de percibir): 

<img width="219" height="42" alt="image" src="https://github.com/user-attachments/assets/25af34f1-a688-469c-9534-ffd5baa6a7e3" />

* Pérdida por simulación
<img width="629" height="112" alt="image" src="https://github.com/user-attachments/assets/83e1b053-48cb-45aa-9a26-a72fca836355" />


## Parámetros del Modelo

* Costos base:

Cr (USD): costo de repuestos por avión.

Cm (USD): costo de mano de obra por avión.

N: número de aviones no registrados.

* Tasas anuales:

inflacion_anual (ej. 0.027 = 2.7%).

retorno_anual (ej. 0.053 = 5.3%).

* Estacionalidad:

iem_dict: diccionario {Mes: índice}.

* Simulación:

n_simulaciones: número de corridas por mes (ej. 1000).

días: valor entero sorteado en [5, 30].

## Pseudo-Codigo

```bash

INPUT: Cr, Cm, N, inflacion_anual, retorno_anual, iem_dict, n_simulaciones
CALC: rd = (1 + inflacion_anual)^(1/365) - 1
      id = (1 + retorno_anual)^(1/365) - 1
INIT: resultados = []

FOR each (mes, iem) in iem_dict:
    REPEAT n_simulaciones times:
        dias ← RandomInteger(5, 30)
        costo_total ← Cr + Cm
        A_infl ← (1 + rd)^dias
        A_oport ← (1 + id)^dias - 1
        factor_total ← A_infl + A_oport
        perdida ← N * costo_total * factor_total * iem
        resultados.APPEND({Mes: mes, Días: dias, Pérdida: perdida})

df_resultados ← DataFrame(resultados)
estadisticas ← GroupBy(df_resultados, Mes).Agg(mean, std, min, max)
estadisticas["CV (%)"] ← (std / mean) * 100
SORT estadisticas BY mean DESC
PLOT boxplot df_resultados (x=Mes, y=Pérdida)

```

## Suposiciones y Alcances

* Los días de atraso se modelan con distribución uniforme discreta en [5,30].
* El impacto financiero se asume aditivo entre ajuste por inflación y costo de oportunidad.
* La estacionalidad se aplica como un factor multiplicativo independiente del tiempo.
* El modelo no incorpora correlaciones entre meses ni cambios estructurales de mercado.

## Validación y Calidad de Resultados

* Reproducibilidad: fijar semilla np.random.seed(42) antes de sortear días.
* Estabilidad estadística: aumentar n_simulaciones hasta que la media y el CV converjan.
* Sanidad de estadísticas: evitar CV extremadamente altos sin justificación; revisar outliers por mes.
* Backtesting básico: comparar medias estimadas con pérdidas observadas históricas por mes (si están disponibles).

## Reproducibilidad 
* Utilizar los siguientes parámetros sugueridos: 

Cr: 20000

Cm: 800

N: 2

inflacion_anual: 0.027

retorno_anual: 0.053
n_simulaciones: 1000

dias_min: 5

dias_max: 30

seed: 42


