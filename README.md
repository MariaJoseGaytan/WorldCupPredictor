# WorldCupPredictor
# Contexto del Proyecto

Este proyecto tiene como objetivo desarrollar un modelo de Machine Learning capaz de predecir resultados de partidos de fútbol, enfocándose principalmente en partidos de la Copa Mundial de la FIFA. La idea principal es analizar datos históricos de selecciones nacionales para identificar patrones que permitan estimar el posible ganador de futuros encuentros.

---

# Dataset

Inicialmente investigué diferentes datasets relacionados con la Copa Mundial de la FIFA y encontré un dataset que contenía únicamente partidos mundialistas desde 1930 hasta 2022:

[FIFA World Cup 1930-2022 All Match Dataset](https://www.kaggle.com/datasets/jahaidulislam/fifa-world-cup-1930-2022-all-match-dataset/data)

Aunque este dataset estaba completamente enfocado en el objetivo del proyecto, solamente contaba con alrededor de 900 instancias. Después de analizarlo, consideré que esta cantidad de datos podía ser insuficiente para entrenar correctamente un modelo de Machine Learning, especialmente una red neuronal, ya que existía el riesgo de overfitting y de que el modelo únicamente memorizara patrones históricos del Mundial.

Debido a esto, continué investigando datasets más amplios relacionados con fútbol internacional y finalmente decidí utilizar el siguiente dataset:

[International Football Results From 1872 to 2017](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017?)

Este dataset incluye partidos internacionales de distintas competiciones, como:

- Mundial
- Partidos amistosos internacionales  
- Eliminatorias mundialistas  
- Torneos continentales  
- Otras competiciones oficiales internacionales  

La decisión de utilizar este dataset fue tomada porque permite trabajar con una cantidad mucho mayor y más variada de partidos, ayudando al modelo a aprender patrones generales del rendimiento de las selecciones nacionales y no únicamente información específica de los Mundiales.

Posteriormente, realicé un proceso de limpieza y normalización de los datos utilizando Python. Durante este proceso:

- Eliminé filas vacías o con información faltante importante.
- Normalicé nombres de equipos, torneos, ciudades y países utilizando `unicodedata` para eliminar acentos y caracteres especiales.
- Convertí todos los textos al formato CamelCase para mantener consistencia en nombres y evitar problemas relacionados con espacios o formatos diferentes.
- Transformé la columna `neutral` a valores numéricos (`1` y `0`) para facilitar el entrenamiento del modelo.
- Agregué una nueva columna llamada `winner` para identificar explícitamente al ganador de cada partido.
- Ordené cronológicamente el dataset para mantener coherencia temporal en el proyecto.

El notebook encargado de este proceso se encuentra en:

```text
notebooks/preprocessingData/cleanData.ipynb
```

El dataset limpio generado se almacena en:

```text
data/processedData/cleanedData.csv
```

---

# División del Dataset

Después del proceso de limpieza, dividí el dataset en entrenamiento, validación y prueba considerando los datos deportivos.

El notebook encargado de esta división se encuentra en:

```text
notebooks/preprocessingData/splitData.ipynb
```

Los archivos generados se almacenan en:

```text
data/processedData/
```

Archivos generados:

```text
train.csv
validation.csv
test.csv
```

La estrategia utilizada fue la siguiente:

- El dataset de entrenamiento contiene partidos internacionales de distintas competiciones anteriores al Mundial de 2014.
- Los partidos de la Copa Mundial de 2014 fueron reservados exclusivamente para validación.
- Los Mundiales de 2018 y 2022 fueron reservados únicamente para pruebas finales del modelo.

La razón de esta división es que el objetivo principal del proyecto es evaluar el desempeño del modelo específicamente en partidos mundialistas. Por ello, decidí utilizar los partidos de los Mundiales más recientes únicamente para validación y prueba, evitando asi que el modelo tenga acceso a ellos durante el entrenamiento.

Además, el shuffle fue aplicado únicamente al dataset de entrenamiento para mejorar la distribución de ejemplos durante el aprendizaje, manteniendo el orden cronológico en validación y prueba para poder simular escenarios reales de predicción.

---

# Autor

María José Gaytán Gil - A01706616