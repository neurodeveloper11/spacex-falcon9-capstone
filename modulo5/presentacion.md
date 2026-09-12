# 🚀 Predicción de Aterrizaje del Falcon 9 (SpaceX)
## Presentación Ejecutiva y Técnica — IBM Applied Data Science Capstone

**Autor:** Fabio Ignacio Torres Benitez  
**Rol:** Lead Data Scientist  
**Repositorio GitHub:** [SpaceX Falcon 9 Landing Prediction](https://github.com/neurodeveloper11/spacex-falcon9-capstone)  
**Fecha:** Septiembre 2026  

---

## 📑 Diapositiva 1: Portada y Metadatos
* **Título del Proyecto:** SpaceX Falcon 9 First Stage Landing Prediction
* **Organización:** IBM Data Science Professional Certificate
* **Autor:** Fabio Ignacio Torres Benitez
* **Enlace al Repositorio de GitHub:** `https://github.com/neurodeveloper11/spacex-falcon9-capstone`

---

## 🎯 Diapositiva 2: Resumen Ejecutivo (Executive Summary)
* **El Reto:** SpaceX reduce los costos de lanzamiento a ~$62M USD frente a los ~$165M USD de los competidores gracias a la reutilización de la primera etapa del cohete Falcon 9.
* **Objetivo de Negocio:** Predecir si la primera etapa aterrizará con éxito para estimar costos de lanzamiento y formular ofertas competitivas en licitaciones aeroespaciales.
* **Metodología End-to-End:**
  1. Extracción de datos vía SpaceX REST API y Web Scraping de Wikipedia.
  2. Limpieza de datos (Wrangling) y creación de la variable binaria `Class` (60 éxitos, 30 fallos).
  3. EDA con SQL (SQLite) y visualización exploratoria con Seaborn y Matplotlib.
  4. Análisis geoespacial con mapas Folium y cálculo de distancias Haversine a infraestructuras.
  5. Dashboard analítico en tiempo real construido con Plotly Dash.
  6. Modelado de Machine Learning supervisado (Logistic Regression, SVM, Decision Tree, KNN) con optimización mediante `GridSearchCV` (10-fold CV).
* **Resultado Clave:** Todos los modelos alcanzaron un **83.33% de precisión (Accuracy)** en el conjunto de prueba independiente, destacando el **Árbol de Decisión** con el mejor puntaje en validación cruzada (**87.68%**).

---

## 🌌 Diapositiva 3: Introducción y Planteamiento del Problema
* **Contexto Aeroespacial:** Los cohetes tradicionales se descartan tras el despegue, hundiéndose en el océano. SpaceX revolucionó la industria aeroespacial logrando aterrizajes controlados en tierra (RTLS) y en barcazas autónomas en el océano (ASDS).
* **Pregunta de Negocio:** ¿Bajo qué condiciones de carga útil, tipo de órbita y sitio de lanzamiento es más probable que el cohete aterrice exitosamente?
* **Impacto Comercial:** Permite a una empresa aeroespacial rival cotizar licitaciones agresivas cuando SpaceX no tenga certeza de recuperar su propulsor.

---

## 📡 Diapositiva 4: Metodología — Recolección y Manipulación de Datos
1. **API REST de SpaceX:** Consumo del endpoint `/v4/launches/past` y extracción de 90 vuelos históricos de Falcon 9.
2. **Web Scraping:** Extracción de tablas HTML de lanzamientos históricos desde Wikipedia mediante `BeautifulSoup4`.
3. **Data Wrangling:**
   - Tratamiento de valores faltantes en `PayloadMass` imputando la media del dataset (6,123.5 kg).
   - Conversión de fechas a formato estándar ISO y extracción de año.
   - Creación de la etiqueta binaria `Class`:
     * `Class = 1`: Aterrizajes exitosos (`True ASDS`, `True RTLS`, `True Ocean`) -> 60 vuelos (66.7%).
     * `Class = 0`: Aterrizajes fallidos o no recuperados (`False ASDS`, `False RTLS`, `False Ocean`, `None None`, `None ASDS`) -> 30 vuelos (33.3%).

---

## 🔍 Diapositiva 5: Metodología — EDA y Analítica Visual Interactiva
* **EDA con SQL:** Ingesta del dataset en base de datos relacional local `my_data1.db` (SQLite) y ejecución de 10 consultas analíticas.
* **EDA Visual:** Gráficos de dispersión y de barras con `seaborn.catplot` y `matplotlib.pyplot` para correlacionar masa de carga útil, órbitas, sitios de lanzamiento y número de vuelo.
* **Inteligencia Geoespacial:** Mapas interactivos en `folium` con clústeres de éxito/fallo y trazado de distancias ortodrómicas a costas y vías férreas.
* **Aplicación Web:** Dashboard interactivo en `Plotly Dash` con selector de sitios y deslizador dinámico de rango de carga útil.

---

## 🤖 Diapositiva 6: Metodología — Modelado Predictivo de Machine Learning
1. **Feature Engineering:** One-Hot Encoding (`pd.get_dummies`) sobre variables categóricas (`Orbit`, `LaunchSite`, `LandingPad`, `Serial`), expandiendo el dataset a 83 características numéricas normalizadas a `float64`.
2. **Estandarización:** Aplicación de `StandardScaler` de Scikit-Learn sobre la matriz de características `X`.
3. **Partición de Datos:** División estratificada con `train_test_split`:
   - Conjunto de Entrenamiento: 72 registros (80%).
   - Conjunto de Prueba: 18 registros (20%), con semilla aleatoria fija `random_state=2`.
4. **Optimización de Hiperparámetros:** Búsqueda sistemática con `GridSearchCV` y 10 particiones de validación cruzada (`cv=10`) para prevenir sobreajuste (*overfitting*).

---

## 📊 Diapositiva 7: Resultados — EDA con Visualizaciones (Seaborn/Matplotlib)
* **Vuelo vs Sitio de Lanzamiento:** A medida que aumentó el número de vuelos (experiencia acumulada), la tasa de éxito creció exponencialmente en todos los complejos.
* **Carga Útil vs Sitio:** El complejo **KSC LC-39A** se reserva para cargas útiles muy pesadas (>10,000 kg) y misiones tripuladas, mostrando una tasa de éxito muy alta.
* **Tasa de Éxito por Órbita:**
  - Órbitas con **100% de éxito**: `ES-L1`, `GEO`, `HEO`, `SSO`.
  - Órbita `VLEO` (Starlink): ~85% de éxito.
  - Órbita `GTO` (geoestacionaria): ~52% de éxito (mayor desgaste y velocidad de reentrada).
  - Órbita `SO`: 0% de éxito.
* **Tendencia Temporal Anual:** La tasa de éxito pasó de un 0% en 2010 a más del 85% a partir de 2017 y superó el 90% en 2020.

---

## 🗄️ Diapositiva 8: Resultados — Consultas SQL con SQLite
1. **Sitios de Lanzamiento:** 4 complejos únicos: `CCAFS LC-40`, `CCAFS SLC-40`, `KSC LC-39A`, `VAFB SLC-4E`.
2. **Carga Total de NASA (CRS):** 45,596 kg transportados en misiones de reabastecimiento a la ISS.
3. **Masa Promedio de F9 v1.1:** 2,534.67 kg.
4. **Primer Aterrizaje Exitoso en Tierra:** 22 de diciembre de 2015 (`2015-12-22`), propulsor `F9 FT B1019`.
5. **Aterrizajes en Barcaza con Carga entre 4,000 y 6,000 kg:** Propulsores `F9 FT B1022`, `F9 FT B1026`, `F9 FT B1021.2`, `F9 FT B1031.2`.
6. **Propulsores con Carga Máxima (15,600 kg):** Versiones Falcon 9 Block 5 (misiones Starlink): `B1048.4`, `B1049.4`, `B1051.3`, `B1056.4`, etc.

---

## 🗺️ Diapositiva 9: Resultados — Análisis Geoespacial con Folium
* **Patrones Geográficos Hallados:**
  1. **Proximidad Inmediata a la Costa (< 1 km):** CCAFS SLC-40 está a sólo **0.90 km** de la línea de costa para garantizar que los despegues y posibles anomalías ocurran sobre aguas abiertas.
  2. **Proximidad a Infraestructura de Transporte:** A **0.59 km** de autopistas principales y a **1.29 km** de vías férreas para el traslado seguro de los propulsores.
  3. **Distancia Segura a Zonas Urbanas:** A más de **23 km** de la ciudad más cercana (Titusville, FL), reduciendo ruidos e impacto de ondas de choque.
* **Visualización de Éxitos:** La mayoría de los fracasos iniciales se concentraron en Cabo Cañaveral durante la fase experimental (2010-2015).

---

## 🖥️ Diapositiva 10: Resultados — Dashboard Interactivo con Plotly Dash
* **Componentes Reactivos:**
  - Selector desplegable (`site-dropdown`): Permite alternar entre la visión global (*All Sites*) y el análisis individual por complejo.
  - Control deslizante de carga (`payload-slider`): Filtra misiones entre 0 y 10,000 kg.
* **Hallazgos del Dashboard:**
  - El sitio con mayor número absoluto de lanzamientos exitosos es **KSC LC-39A** (tasa de éxito del 76.2%), seguido de **CCAFS SLC-40**.
  - En el rango de carga útil de **2,000 a 4,000 kg**, la tasa de éxito supera el 70%.
  - Las cargas útiles superiores a **8,000 kg** muestran una tasa de aterrizaje casi perfecta cuando se utilizan propulsores de la serie **FT** y **B5**.

---

## 📈 Diapositiva 11: Resultados — Modelado Predictivo y Clasificación ML
Se evaluaron 4 familias de algoritmos supervisados optimizados con 10-fold Cross-Validation:

| Modelo Evaluado | Mejores Hiperparámetros | Accuracy en Validación (CV) | Accuracy en Conjunto de Prueba |
| :--- | :--- | :---: | :---: |
| **Árbol de Decisión** | `criterion='gini', max_depth=8, max_features='sqrt', min_samples_leaf=2` | **87.68%** | **83.33%** |
| **Máquinas de Vectores de Soporte (SVM)** | `C=1.0, gamma=0.0316, kernel='sigmoid'` | 84.82% | **83.33%** |
| **K-Nearest Neighbors (KNN)** | `n_neighbors=10, p=1 (Manhattan), algorithm='auto'` | 84.82% | **83.33%** |
| **Regresión Logística** | `C=0.01, penalty='l2', solver='lbfgs'` | 84.64% | **83.33%** |

* **Diagnóstico de las Matrices de Confusión (Conjunto de Prueba - 18 muestras):**
  - **Verdaderos Positivos:** 12 aterrizajes exitosos predichos con exactitud.
  - **Verdaderos Negativos:** 3 fallos predichos con exactitud.
  - **Falsos Positivos:** 3 muestras (el modelo predijo éxito pero el aterrizaje falló).
  - **Falsos Negativos:** 0 muestras (ningún aterrizaje exitoso fue catalogado erróneamente como fallo).

---

## 🏆 Diapositiva 12: Selección del Modelo Ganador y Diagnóstico
* **Modelo Ganador:** **Decision Tree Classifier (Árbol de Decisión)**.
* **Justificación Técnica:**
  1. Obtuvo la mayor precisión en el conjunto de entrenamiento/validación cruzada (**87.68%**).
  2. Mantiene una alta interpretabilidad de las reglas de decisión para los ingenieros de vuelo.
  3. No hace suposiciones lineales sobre el espacio de características, capturando relaciones complejas no lineales entre la masa de carga útil, el tipo de órbita y la versión del propulsor.

---

## 💡 Diapositiva 13: Estrategia de Negocio y Licitación (Bidding Strategy)
* **Estructura de Costes de la Industria:**
  - Costo de lanzamiento competidor tradicional (un solo uso): **$165 Millones USD**.
  - Costo de lanzamiento SpaceX Falcon 9 (primera etapa reutilizada): **$62 Millones USD**.
  - Costo de fabricación de la primera etapa: ~$40 Millones USD (~65% del costo total).
* **Estrategia Comercial de Licitación:**
  1. **Misiones a Órbitas de Alto Riesgo / Cargas Extremas (GTO, >7,000 kg):** Nuestro modelo predice menor probabilidad de recuperación de la primera etapa de SpaceX. Aquí podemos licitar con precios agresivos en el rango de **$80M - $95M USD**, donde el margen de SpaceX se estrecha debido al riesgo de pérdida del booster.
  2. **Misiones a Órbitas SSO, LEO o Starlink:** La probabilidad de reutilización de SpaceX roza el 100%. No es rentable competir por precio directo; la estrategia debe basarse en disponibilidad de calendario o servicios de inserción orbital dedicada.

---

## 🎨 Diapositiva 14: Creatividad y Valor Agregado más allá de la Plantilla
* **Infraestructura Local Automatizada:** Despliegue de scripts locales reproducibles en Python 3.13 con base de datos SQLite integrada y verificación automática de 0 nulos.
* **Dashboard Reactivo Local:** Servidor interactivo Plotly Dash con soporte de filtrado multidimensional en tiempo real.
* **Mapeo de Distancias de Seguridad:** Integración de la fórmula trigonométrica de Haversine para modelar los protocolos de escape y seguridad costera.
* **Auditoría de Invariantes:** Cero *Data Leakage* al aislar estrictamente el conjunto de prueba (`test_set = 18`) durante el preprocesamiento y escalado.

---

## 🏁 Diapositiva 15: Conclusiones y Próximos Pasos
1. **La reutilización del cohete es el factor determinante en el costo espacial:** La capacidad de predecir el aterrizaje con más del 83% de precisión transforma la incertidumbre técnica en ventaja financiera.
2. **Recomendación para la Dirección:** Continuar nutriendo la base de datos con los lanzamientos recientes de Falcon Heavy y Starship para entrenar modelos de ensamble (*Random Forest*, *XGBoost*) que reduzcan a cero los falsos positivos.
3. **Estado del Proyecto:** Repositorio en GitHub listo con 100% de los notebooks resueltos, código fuente y documentación ejecutiva para entrega y certificación inmediata.
