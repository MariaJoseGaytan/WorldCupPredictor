# WorldCupPredictor 

Proyecto de Machine Learning enfocado en la predicción de resultados de partidos de la Copa Mundial de la FIFA utilizando estadísticas históricas y features generadas a partir del desempeño acumulado de las selecciones.

---

# Objetivo del Proyecto

El objetivo principal de este proyecto es desarrollar un modelo de Machine Learning capaz de predecir el resultado de partidos de la Copa Mundial utilizando información histórica y desempeño previo de las selecciones.

El modelo busca identificar patrones históricos dentro de los Mundiales para intentar estimar si un equipo ganará, empatará o perderá un partido.

---

# Cambio de enfoque del proyecto

Inicialmente consideré utilizar datasets de fútbol internacional que incluían amistosos, eliminatorias y distintos torneos alrededor del mundo. La idea era utilizar una mayor cantidad de partidos para entrenar el modelo.

Sin embargo, después de analizar mejor el problema y el alcance real del proyecto, me di cuenta de que utilizar partidos internacionales generales añadía mucho ruido al modelo y no necesariamente aportaba valor para predecir encuentros mundialistas.

Esto se debe a varios factores:

- Los equipos que juegan Mundiales cambian dependiendo de la edición.
- Los amistosos y eliminatorias tienen contextos competitivos muy distintos.
- Un partido amistoso no representa la presión ni comportamiento de un partido de Copa Mundial.
- Algunos equipos juegan muchísimos partidos internacionales pero rara vez participan en Mundiales.

Debido a esto, decidí utilizar exclusivamente un dataset enfocado en partidos de la Copa Mundial de la FIFA, priorizando la relevancia del contexto competitivo sobre la cantidad total de datos.

Esta decisión me permitió construir un dataset más coherente con el objetivo real del proyecto.

---

# Dataset Utilizado

Dataset principal utilizado:

- [FIFA Football World Cup](https://www.kaggle.com/datasets/piterfm/fifa-football-world-cup)

Dataset internacional considerado inicialmente:

- [International Football Results From 1872 to 2026](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017)

---

# Limpieza y Preparación de Datos

El notebook encargado de la limpieza y generación de features se encuentra en:

```text
notebooks/preprocessingData/cleanData_newFeatures.ipynb
```

Durante el proceso de limpieza realicé las siguientes tareas:

- Limpieza y normalización de nombres de columnas.
- Conversión de fechas a formato datetime.
- Eliminación de espacios innecesarios.
- Ordenamiento cronológico de partidos.
- Creación de variables auxiliares.
- Creación de la variable objetivo del modelo.

Resultados obtenidos después de la limpieza:

```text
Dataset limpio: (964, 38)
```

---

# Variables Agregadas

Además de las columnas originales, agregué nuevas variables para aportar más contexto al modelo.

## Variables básicas

| Columna | Descripción |
|---|---|
| goal_difference | Diferencia de goles |
| total_goals | Total de goles en el partido |
| result_label | Resultado codificado |
| result_name | Resultado textual |
| world_cup_year | Año del Mundial |

---

# Feature Engineering

Una de las partes más importantes del proyecto fue la generación de features históricas para cada selección.

La idea fue que el modelo no solamente viera nombres de países, sino también estadísticas acumuladas y rendimiento previo antes de cada partido.

Todas las features fueron calculadas utilizando únicamente información anterior al partido correspondiente para evitar data leakage.

El notebook utilizado fue:

```text
notebooks/preprocessingData/cleanData_newFeatures.ipynb
```

---

# Features Históricas Agregadas

## Estadísticas históricas

- Partidos jugados.
- Victorias acumuladas.
- Empates acumulados.
- Derrotas acumuladas.
- Goles anotados.
- Goles recibidos.
- Diferencia histórica de goles.
- Puntos acumulados.
- Participaciones en Mundiales anteriores.

## Estadísticas promedio

- Win rate histórico.
- Draw rate histórico.
- Loss rate histórico.
- Promedio de goles anotados.
- Promedio de goles recibidos.
- Puntos promedio por partido.

## Rendimiento reciente

Tomando los últimos 5 partidos:

- Promedio reciente de goles anotados.
- Promedio reciente de goles recibidos.
- Win rate reciente.

## Historial entre selecciones 

- Partidos históricos entre ambos equipos.
- Victorias históricas del local.
- Victorias históricas del visitante.
- Empates históricos.

Resultados después del feature engineering:

```text
Dataset con features: (964, 78)
```

---

# Variable Objetivo

La variable objetivo del modelo quedó definida de la siguiente manera:

| Valor | Significado |
|---|---|
| 2 | Victoria del equipo local |
| 1 | Empate |
| 0 | Victoria del equipo visitante |

---

# División del Dataset

La división del dataset se realizó por edición de Copa Mundial.

Tomé esta decisión para evitar fuga de información entre partidos del mismo torneo y simular un escenario más realista de predicción futura.

El notebook encargado del split fue:

```text
notebooks/preprocessingData/splitData.ipynb
```

La división quedó de la siguiente manera:

| Dataset | Mundiales |
|---|---|
| Train | 1930 - 2010 |
| Validation | 2014 |
| Test | 2018 y 2022 |

Resultados finales:

```text
Train: (772, 78)
Validation: (64, 78)
Test: (128, 78)
```

Porcentajes obtenidos:

```text
Train: 80.08 %
Validation: 6.64 %
Test: 13.28 %
```

---

# Archivos Generados

Los archivos generados después del procesamiento fueron:

```text
data/processedData/cleanedData.csv
data/processedData/featuredData.csv
data/processedData/train.csv
data/processedData/validation.csv
data/processedData/test.csv
```

---

# Autor

María José Gaytán Gil - A01706616

