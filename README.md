# Marketplace Data Analysis & Quality Audit (100k Listings)

## 📌 Descripción del Proyecto
Este proyecto simula una prueba técnica para un perfil de **Data Analyst / Data Engineer**. El objetivo es auditar la calidad de los datos, sanear inconsistencias y extraer hallazgos accionables de negocio a partir de una muestra de **100,000 publicaciones** (`MLA_100k.jsonlines`) de un marketplace de comercio electrónico en Argentina.

---

## 🛠️ Stack Tecnológico
* **Lenguaje:** Python 3.10+
* **Procesamiento de datos:** `pandas`, `numpy`
* **Visualización de datos:** `matplotlib`, `seaborn`
* **Entorno:** Jupyter Notebook

---

## 🔍 Enfoque Metodológico

### 1. Ingesta e Inspección Inicial
* Carga eficiente de datos en formato JSON Lines (`pd.read_json(..., lines=True)`).
* Verificación de dimensiones, tipos de datos (`dtypes`) y coherencia semántica de campos clave (`price`, `category_id`, `sold_quantity`, `shipping_type`, `condition`).

### 2. Diagnóstico y Limpieza de Calidad de Datos
* **Valores Nulos y Duplicados:** Detección de registros duplicados y porcentaje residual de nulos en variables operativas, aplicando eliminación controlada.
* **Reglas de Negocio:** Filtrado de registros inválidos con precios iguales a cero o negativos (`price <= 0`).
* **Tratamiento de Outliers:** 
  * Cálculo de medidas de tendencia central (media, mediana) y de dispersión (desvío estándar, percentiles).
  * Aplicación del criterio de Rango Intercuartílico ($IQR = Q_3 - Q_1$) con umbrales $1.5 \times IQR$ para clasificar valores extremos sin eliminar distorsiones legítimas de rubros de alto valor.

### 3. Análisis Exploratorio (EDA)
* Segmentación del precio por condición del ítem (`new` vs. `used`).
* Correlación entre métodos de envío (`me2`, `me1`, `custom`, `not_specified`) y unidades vendidas (`sold_quantity`).
* Identificación de las 5 categorías con mayor volumen acumulado de ventas.

---

## 📊 Principales Hallazgos (Insights de Negocio)

1. **Dispersión de Precios:**  
   La media de precios está fuertemente sesgada a la derecha por publicaciones de categorías premium (computación, electrónica y celulares). Para decisiones de *pricing*, la **mediana** resulta la medida de tendencia central más robusta.
2. **Impacto de la Logística en la Conversión:**  
   Las publicaciones que operan con la red logística estándar del marketplace (`me2`) concentran tanto el mayor volumen global como el promedio más alto de unidades vendidas por publicación frente a opciones personalizadas (`custom`).
3. **Condición del Ítem:**  
   Los productos clasificados como `new` representan la gran mayoría del inventario activo y del volumen transaccionado, mostrando una mayor rotación que los productos usados.

---

