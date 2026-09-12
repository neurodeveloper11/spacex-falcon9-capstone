# 🚀 SpaceX Falcon 9 First Stage Landing Prediction
### IBM Applied Data Science Capstone Project
**Autor:** Fabio Ignacio Torres Benitez  
**Certificación:** IBM Data Science Professional Certificate (Coursera)

---

## 📌 Descripción General del Proyecto
SpaceX es el líder mundial en la industria aeroespacial gracias a su capacidad de reutilizar la primera etapa (*booster*) de sus cohetes Falcon 9. Mientras que un lanzamiento espacial tradicional cuesta más de 165 millones de dólares, SpaceX ofrece lanzamientos a aproximadamente 62 millones de dólares debido a la recuperación exitosa de la primera etapa.

En este proyecto asumimos el rol de **Científicos de Datos** para una compañía emergente que compite en el sector aeroespacial. El objetivo central es **predecir si la primera etapa del Falcon 9 aterrizará con éxito** para determinar costos de lanzamiento y formular estrategias de licitación comercialmente viables frente a SpaceX.

---

## 📂 Estructura del Repositorio

```text
├── modulo1/                          # Ingesta, Web Scraping y Wrangling de Datos
│   ├── jupyter-labs-spacex-data-collection-api-v2.ipynb
│   ├── jupyter-labs-webscraping.ipynb
│   └── labs-jupyter-spacex-Data wrangling-v2.ipynb
│
├── modulo2/                          # Análisis Exploratorio de Datos (EDA)
│   ├── jupyter-labs-eda-dataviz-v2.ipynb
│   └── jupyter-labs-eda-sql-coursera_sqllite.ipynb
│
├── modulo3/                          # Visualización Geoespacial y Dashboards
│   ├── lab-jupyter-launch-site-location-v2.ipynb
│   ├── Build_a_Dashboard_Application_with_Plotly_Dash.pdf
│   └── spacex_dash_app.py
│
├── modulo4/                          # Modelado Predictivo de Machine Learning
│   └── SpaceX-Machine-Learning-Prediction-Part-5-v1.ipynb
│
├── modulo5/                          # Presentación y Entrega Final para Stakeholders
│   ├── presentacion.md
│   └── SpaceX_Falcon9_Executive_Presentation.pdf
│
├── .gitignore
└── README.md
```

---

## 🛠️ Stack Tecnológico y Metodología
* **Lenguaje:** Python 3.10+
* **Ingesta y Extracción:** REST APIs (`requests`), Web Scraping (`BeautifulSoup4`).
* **Tratamiento y Wrangling:** `pandas`, `numpy`.
* **Bases de Datos & EDA:** SQL (`sqlite3`), `seaborn`, `matplotlib`.
* **Analítica Espacial & UI:** Mapas interactivos con `folium`, aplicaciones analíticas web con `Plotly Dash`.
* **Machine Learning:** `scikit-learn` (Regresión Logística, SVM, Árboles de Decisión, KNN, `StandardScaler`, `GridSearchCV`, `ConfusionMatrixDisplay`).

---

## 📊 Fases del Proyecto
1. **Recolección de Datos:** Consumo de la API REST de SpaceX v4 y extracción de tablas de lanzamientos de Falcon 9 desde Wikipedia.
2. **Data Wrangling:** Creación de la variable objetivo binaria `Class` (1 = Aterrizaje exitoso, 0 = Fallo o no recuperado) y tratamiento de valores nulos en `PayloadMass`.
3. **Análisis Exploratorio (EDA) con SQL y Python:** Determinación de relaciones entre masa de carga útil, órbitas, sitios de lanzamiento y tasa de éxito acumulada.
4. **Análisis Geoespacial:** Mapeo de complejos de lanzamiento (CCAFS SLC-40, KSC LC-39A, VAFB SLC-4E) y cálculo de distancias con la fórmula de Haversine a costas, vías de tren y centros urbanos con Folium.
5. **Dashboard Interactivo:** Construcción de una app reactiva en Plotly Dash con selector de sitios y deslizador de carga útil para visualización de métricas en tiempo real.
6. **Modelado Predictivo:** Ajuste de hiperparámetros con 10-fold cross validation (`GridSearchCV`) sobre 4 familias de clasificadores, evaluación con matriz de confusión y diagnóstico del mejor modelo.
7. **Estrategia Comercial (Bidding Strategy):** Formulación de recomendaciones de costos para licitar contratos de lanzamiento frente a SpaceX.

---

## 🚀 Cómo Reproducir este Proyecto
1. Clonar el repositorio:
   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd "Ciencia de datos aplicada"
   ```
2. Instalar dependencias requeridas:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn folium plotly dash requests beautifulsoup4 sqlalchemy
   ```
3. Ejecutar los notebooks en orden cronológico (`modulo1` a `modulo4`).
4. Para levantar el Dashboard interactivo:
   ```bash
   python modulo3/spacex_dash_app.py
   ```
   Abrir en el navegador: `http://127.0.0.1:8050/`
