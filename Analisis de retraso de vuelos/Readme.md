# 🚀 Análisis de Retrasos en Vuelos Comerciales (Airlines Dataset)

Un análisis exploratorio de datos (EDA) y modelado predictivo sobre más de **530,000 registros operativos** de vuelos comerciales en EE. UU., diseñado para identificar los principales patrones que provocan retrasos en las aerolíneas y estimar la probabilidad de demora pre-despegue.

---

## 📌 Descripción del Proyecto

El retraso en los vuelos comerciales representa uno de los mayores desafíos logísticos y financieros para la industria aeronáutica mundial. Este proyecto analiza un dataset operativo masivo de **539,383 instancias** y **8 características**, evaluando variables como la aerolínea, el horario de salida programado, el día de la semana, la duración estimada del vuelo y las rutas aéreas.

### 🎯 Objetivos Principales:
- Realizar un **Análisis Exploratorio de Datos (EDA)** para entender el comportamiento general del tráfico aéreo y los niveles de retraso (tasa global del **44.54%**).
- Identificar las **aerolíneas más y menos impuntuales** del mercado comercial.
- Evaluar la correlación entre variables numéricas (duración del vuelo, hora del día, número de vuelo y día de la semana) con respecto al estado de demora (`Delay`).
- Construir una base sólida para futuros modelos de Machine Learning de clasificación binaria.

---

## 📊 Estructura del Dataset

El dataset contiene **539,383 filas** y **8 columnas principales** (tras remover el identificador irrelevante `id`):

| Columna | Tipo de Dato | Descripción |
| :--- | :---: | :--- |
| **`Airline`** | Categorical (`object`) | Código IATA de la aerolínea (18 aerolíneas únicas). |
| **`Flight`** | Discrete (`int64`) | Número identificador del vuelo (Rango: 1 - 7814). |
| **`AirportFrom`** | Categorical (`object`) | Código IATA del aeropuerto de origen (293 aeropuertos únicos). |
| **`AirportTo`** | Categorical (`object`) | Código IATA del aeropuerto de destino (293 aeropuertos únicos). |
| **`DayOfWeek`** | Discrete (`int64`) | Día de la semana (1: Lunes a 7: Domingo). |
| **`Time`** | Continuous (`int64`) | Hora de salida programada expresada en minutos desde medianoche (Rango: 10 - 1439 min). |
| **`Length`** | Continuous (`int64`) | Duración programada del vuelo en minutos (Rango: 0 - 655 min, promedio ~132 min). |
| **`Delay`** | Binary (`int64`) | Variable objetivo (**1** = Retrasado, **0** = A tiempo). |

---

## 💡 Principales Hallazgos e Insights (EDA)

1. **Tasa Global de Retrasos**: El **44.54%** de todos los vuelos registrados sufren retrasos, mostrando un balance casi equitativo entre clases (0 y 1).
2. **Impuntualidad por Aerolínea**:
   - 🔴 **Top 5 Aerolíneas con Mayor Tasa de Retraso**:
     1. **WN** (Southwest Airlines): **69.78%** de vuelos retrasados.
     2. **CO** (Continental Airlines): **56.62%** de vuelos retrasados.
     3. **B6** (JetBlue Airways): **46.70%** de vuelos retrasados.
     4. **OO** (SkyWest Airlines): **45.29%** de vuelos retrasados.
     5. **DL** (Delta Air Lines): **45.05%** de vuelos retrasados.
   - 🟢 **Top 5 Aerolíneas Más Puntuales**:
     1. **YV** (Mesa Airlines): **24.29%** de retrasos.
     2. **OH** (PSA Airlines): **27.73%** de retrasos.
     3. **FL** (AirTran Airways): **30.13%** de retrasos.
     4. **HA** (Hawaiian Airlines): **32.02%** de retrasos.
     5. **UA** (United Airlines): **32.39%** de retrasos.
3. **Correlación de Variables**:
   - Existe una **correlación positiva significativa ($r = 0.15$)** entre la variable `Time` (hora del día en minutos) y `Delay`. A medida que avanza la jornada (tarde/noche), la probabilidad de retraso aumenta progresivamente debido al efecto dominó acumulado.
   - Existe una relación inversa negativa ($r = -0.34$) entre `Flight` (número de vuelo) y `Length` (duración del vuelo).

---

## 🛫 Catálogo de Aerolíneas y Aeropuertos Principales

### Aerolíneas (Códigos IATA)
| Código | Aerolínea | Código | Aerolínea |
| :---: | :--- | :---: | :--- |
| **9E** | Endeavor Air | **HA** | Hawaiian Airlines |
| **AA** | American Airlines | **MQ** | Envoy Air |
| **AS** | Alaska Airlines | **OH** | PSA Airlines |
| **B6** | JetBlue Airways | **OO** | SkyWest Airlines |
| **CO** | Continental Airlines | **UA** | United Airlines |
| **DL** | Delta Air Lines | **US** | US Airways |
| **EV** | ExpressJet Airlines | **WN** | Southwest Airlines |
| **F9** | Frontier Airlines | **XE** | ExpressJet (JetLink) |
| **FL** | AirTran Airways | **YV** | Mesa Airlines |

---

## ⚠️ Limitaciones y Futuras Mejoras

### 📌 Limitaciones del Dataset Actual
- **Ausencia de Factores Exógenos Críticos**: El conjunto de datos no incluye variables meteorológicas (clima, viento, visibilidad), congestión en pista ni motivos específicos de retraso (mantenimiento, personal, seguridad).
- **Falta de Marcas Temporales Absolutas**: No se especifica la fecha exacta (año/mes), lo que limita la capacidad de capturar estacionalidad (temporadas altas, festivos) o tendencias multianuales.
- **Formato del Retraso**: La variable objetivo es binaria (`Delay`), por lo que no especifica la magnitud ni la duración exacta del retraso en minutos.

### 🔮 Futuras Mejoras y Plan de Implementación de ML
1. **Modelado de Machine Learning (Clasificación Binaria)**:
   - **Ingeniería de Características (*Feature Engineering*)**: Creación de métricas agregadas como la tasa histórica de retraso por ruta (`AirportFrom` ➡️ `AirportTo`), franjas horarias discretizadas (Mañana, Tarde, Noche) y frecuencias por aerolínea.
   - **Modelos a Evaluar**: Entrenar y comparar modelos baseline como *Regresión Logística*, *Random Forest*, *XGBoost* y *LightGBM*.
   - **Métricas de Evaluación**: Optimización basada en **ROC-AUC**, **PR-AUC**, **F1-Score** y **Matriz de Confusión** dada la distribución de clases (~44.5% positivos).
2. **Enriquecimiento de Datos (*Data Augmentation*)**:
   - Integrar variables meteorológicas históricas por aeropuerto y fecha.
   - Incluir datos de capacidad y tráfico aéreo simultáneo por aeropuerto de salida.
3. **Despliegue de API Predictiva**:
   - Empaquetar el modelo seleccionado mediante `FastAPI` / `Flask` e inferencia en tiempo real para estimar la probabilidad de retraso antes del despegue dado el horario y la aerolínea.

---

## 🛠️ Tecnologías Utilizadas

- **Lenguaje**: Python 3.x
- **Manipulación de Datos**: `pandas`, `numpy`
- **Visualización de Datos**: `matplotlib`, `seaborn`, `plotly.express`
- **Entorno de Desarrollo**: Jupyter Notebook / Google Colab

---

## ⚙️ Instalación y Requisitos

Para ejecutar el notebook localmente o explorar los resultados, me aseguro de tener instalado Python 3.8+ y las bibliotecas requeridas:

```bash
git clone https://github.com/tu-usuario/airlines-delay-analysis.git
cd airlines-delay-analysis
pip install pandas numpy matplotlib seaborn plotly
```

---

## 📁 Estructura del Repositorio

```text
├── Airlines.csv              # Dataset operativo (539k+ registros)
├── flight_delay_analysis.ipynb # Notebook Jupyter con el análisis exploratorio y gráficos
├── README.md                 # Documentación principal del proyecto
└── requirements.txt          # Dependencias del entorno Python
```

---
*Proyecto de Ciencia de Datos y Análisis Exploratorio de Datos Operativos.*
