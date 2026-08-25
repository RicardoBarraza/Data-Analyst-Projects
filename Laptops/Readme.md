# Análisis de Precios de Laptops y Factores de Mercado

## 1. Problema de Negocio
En el mercado actual de tecnología y comercio electrónico, la determinación de precios de las computadoras portátiles (laptops) varía considerablemente en función de las especificaciones técnicas (procesador, memoria RAM, almacenamiento, tarjeta gráfica, pantalla táctil) y el posicionamiento de la marca. 

Este proyecto fue iniciado con el objetivo de comprender la estructura de precios de las laptops en el mercado, identificar la distribución del costo del equipo, detectar valores atípicos (*outliers*) y analizar cómo influyen los componentes de hardware y la reputación/calificaciones de los usuarios en el precio final. Este análisis permite a distribuidores, compradores y analistas de producto tomar decisiones fundamentadas sobre fijación de precios y relación costo-beneficio.

---

## 2. Los Datos y Metodología
### Descripción de los Datos
El conjunto de datos utilizado (`laptopPrice.csv`) contiene **823 registros** y **19 variables** que caracterizan las laptops disponibles en el mercado:

- **Variables de Marca y Procesador:** `brand` (marca de la laptop), `processor_brand` (Intel, AMD), `processor_name` (Core i3, Core i5, Celeron, etc.), `processor_gnrtn` (generación del procesador).
- **Especificaciones de Hardware:** `ram_gb` (cantidad de memoria RAM), `ram_type` (DDR4, etc.), `ssd` (capacidad de disco sólido), `hdd` (capacidad de disco duro), `graphic_card_gb` (memoria de tarjeta gráfica dedicada).
- **Sistema Operativo y Estructura:** `os` (Windows, Mac, etc.), `os_bit` (64-bit, 32-bit), `weight` (categoría de peso/uso: Casual, Gaming, etc.).
- **Características Adicionales:** `warranty` (garantía), `Touchscreen` (pantalla táctil: Yes/No), `msoffice` (incluye Microsoft Office: Yes/No).
- **Variables Métricas y Valoraciones:** 
  - `Price`: Precio del equipo (variable objetivo).
  - `rating`: Calificación asignada por usuarios.
  - `Number of Ratings`: Cantidad total de calificaciones acumuladas.
  - `Number of Reviews`: Cantidad total de reseñas escritas.

### Metodología de Análisis
1. **Carga y Exploración Inicial:** Uso de `pandas.read_csv()` y `datos.head()` para verificar la integridad del DataFrame y la estructura de tipos de datos.
2. **Estadística Descriptiva:** Análisis de medidas de tendencia central y dispersión mediante `datos.describe()` para identificar el rango de precios, la media, mediana y percentiles.
3. **Análisis Exploratorio Visual:** Generación de gráficos con `matplotlib.pyplot` y `seaborn` (diagramas de cajas y bigotes / *boxplots*) para identificar dispersión, simetría y detectar valores extremadamente altos en el precio.

---

## 3. Resultados y Conclusiones
### Métricas Clave (Resumen Estadístico del Precio)
- **Tamaño de la Muestra:** 823 laptops evaluadas.
- **Precio Promedio (Media):** $76,745.18
- **Precio Mediano (Mediana - 50%):** $64,990.00
- **Desviación Estándar:** $45,101.79 (indica alta variabilidad en los precios según la gama del equipo).
- **Rango de Precios:**
  - **Mínimo:** $16,990.00 (gama de entrada / económica).
  - **Percentil 25% (Q1):** $46,095.00
  - **Percentil 75% (Q3):** $89,636.00
  - **Máximo:** $441,990.00 (equipos de gama alta / *workstations* / gaming especializado).

### Principales Conclusiones
1. **Asimetría Positiva en los Precios:** La diferencia significativa entre la mediana ($64,990.00) y la media ($76,745.18) refleja una distribución sesgada a la derecha. La mayoría de los equipos se concentran en rangos de precio accesibles y de gama media (entre $46,000 y $90,000).
2. **Presencia de Valores Atípicos (*Outliers*):** El diagrama de caja y bigotes (`boxplot`) evidencia la presencia de equipos con precios superiores a los $200,000 e incluso alcanzando los $441,990. Estos valores corresponden a especificaciones extremas (tarjetas gráficas avanzadas, procesadores de última generación y gran almacenamiento SSD).
3. **Volumen de Opiniones:** El número de evaluaciones (`Number of Ratings`) promedia 315.3 valoraciones por producto, registrando un máximo de 15,279, lo que sugiere alta concentración de ventas en modelos populares de gama media.

---

## 4. Limitaciones y Pasos Siguientes
### Limitaciones Identificadas
- **Formato de Variables Categóricas:** Variables como `ram_gb`, `ssd`, `hdd`, `graphic_card_gb` y `rating` incluyen texto acompañando a los valores numéricos (ej. `"4 GB"`, `"1024 GB"`, `"2 stars"`), requiriendo limpieza de datos para convertirlas a tipo numérico (`int`/`float`).
- **Valores Faltantes o No Disponibles:** Existencia de valores como `"Not Available"` en columnas categóricas (`processor_gnrtn`), lo cual afecta el análisis de series de generaciones.
- **Moneda y Contexto Geográfico:** No se especifica explícitamente la divisa en la columna `Price` (ej. INR/Rupias indias o pesos), por lo que las métricas deben interpretarse en el contexto de escala relativa del dataset.

### Pasos Siguientes y Futuras Mejoras
1. **Preprocesamiento y Limpieza Fina:** Extracción de valores numéricos de las columnas de memoria/almacenamiento mediante expresiones regulares en Pandas.
2. **Modelado Predictivo:** Desarrollo de modelos de regresión (Regresión Lineal, Random Forest, XGBoost) para predecir el precio de una laptop en función de sus características técnicas.
3. **Análisis Multivariado:** Evaluación de la correlación entre marcas (`brand`), tipo de tarjeta gráfica y precio para identificar qué componente aporta mayor valor agregado al producto final.

---

## 5. Comparativa de Herramientas Utilizadas

| Herramienta | Función en el Proyecto | Ventajas / Fortalezas | Limitaciones Observadas |
| :--- | :--- | :--- | :--- |
| **Python** | Lenguaje principal de programación y ejecución del entorno de análisis. | Flexible, multiplataforma y con un ecosistema robusto de librerías para ciencia de datos. | Requiere configuración de entorno de ejecución (Jupyter Notebook / Anaconda). |
| **Pandas** | Carga del dataset (`read_csv`), exploración estructural (`head`) y resumen estadístico (`describe`). | Manipulación eficiente de datos tabulares y cálculo rápido de métricas agregadas. | Puede consumir mucha memoria RAM con datasets masivos sin optimización de tipos. |
| **NumPy** | Soporte de cálculo numérico vectorizado y estructuras matriciales subyacentes. | Operaciones matemáticas y estadísticas de alto rendimiento a nivel de código C. | Menos intuitivo para manejo directo de tablas con encabezados y columnas texto. |
| **Matplotlib** | Creación y personalización de gráficos base (diagrama de caja y bigotes con `plt.boxplot`). | Control total sobre la estética del gráfico, títulos, ejes y renderizado de imágenes. | Sintaxis más imperativa y verbosa para lograr diseños complejos. |
| **Seaborn** | Librería de visualización estadística complementaria construida sobre Matplotlib. | Estilos visuales atractivos por defecto y facilidad para gráficos estadísticos complejos. | Depende de Matplotlib para personalización avanzada de capas. |
