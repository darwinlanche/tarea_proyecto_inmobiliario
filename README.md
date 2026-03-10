# Análisis Predictivo y Exploratorio del Mercado Inmobiliario en Quito

## 1. Propósito del Dataset y Enfoque Investigativo
El presente proyecto utiliza un dataset extraído de Kaggle filtrado exclusivamente para la ciudad de Quito, el archivo descargado se llama ec_properties.cvs. 

*Enfoque Investigativo:* El objetivo central de este análisis es evaluar la factibilidad de adquirir una vivienda en Quito con un presupuesto accesible orientado a la clase media, específicamente quwe iscile entre los *50,000 USD*. Este valor es estratégico, ya que se ajusta a las opciones de financiamiento local preferencial (como los créditos hipotecarios del BIESS con tasas de interés del 2.99%). A través del Análisis Exploratorio de Datos y Machine Learning, buscamos identificar si existe oferta real en este segmento y en qué sectores se concentra.

---

## 2. Flujo de Trabajo Colaborativo
Para garantizar las mejores prácticas de desarrollo y control de versiones, este proyecto fue coordinado centralizando el código en GitHub. 
* Se implementó el uso de ramas secundarias (branches) para separar el flujo de trabajo.
* La integración del código final se realizó mediante Pull Requests

---

## 3. Pasos de Limpieza y Transformación
El dataset original de toda Sudamérica contenía ruido y datos inconsistentes, por lo que se aplicó un pipeline de limpieza riguroso utilizando pandas:

1. *Filtrado Geográfico y de Operación:* Se aisló el dataset (l1 = Ecuador, l3 = Quito) y se descartaron propiedades en Alquiler, oficinas y lotes, manteniendo estrictamente ventas de *Casas* y *Departamentos*.
2. *Manejo de Valores Nulos:*
   * Se eliminó por completo la columna surface_covered debido a que presentaba un 99.42% de datos faltantes.
   * *Imputación:* La columna bathrooms (2.27% de nulos) fue rellenada utilizando la mediana estadística según su property_type.
   * Se descartaron las filas sin precio (price) o sin área total (surface_total), variables críticas para el modelo.
3. *Limpieza de Anomalías:* Se filtraron errores de tipeo evidentes (inmuebles menores a 20 m2 o precios irreales inferiores a 10,000 USD), resultando en un dataset final pulcro de *11,746 propiedades*.

---

## 4. Principales Hallazgos del Análisis (EDA)
Mediante el uso de matplotlib y seaborn, el análisis visual arrojó los siguientes descubrimientos clave sobre el mercado quiteño:

* *Concentración del Mercado:* El histograma de distribución de precios demuestra que la mayor concentración de la oferta inmobiliaria se sitúa entre los *70,000 USD y 150,000 USD*. 
* *Viabilidad del Presupuesto Objetivo:* Al trazar la línea de nuestro presupuesto objetivo (50,000 USD), evidenciamos que sí existe oferta en este rango inferior, demostrando que la adquisición mediante créditos preferenciales es factible, aunque requiere una búsqueda focalizada.
* *Departamentos vs. Casas:* El gráfico de cajas revela que la mediana de precios de los departamentos (120,000 USD) es considerablemente menor a la de las casas (140,000 USD). Para un presupuesto ajustado, el comprador debe priorizar la búsqueda de departamentos.

(Nota: En el repositorio se incluye el archivo mapa_oportunidades_quito.html generado con folium, el cual permite visualizar de forma interactiva las propiedades exactas que se ajustan al rango de 40,000 a 60,000 USD).

---

## 5. Machine Learning y Generación de Insights
Para aportar valor agregado, se implementó un modelo predictivo utilizando scikit-learn con el fin de estimar el precio de las viviendas basándose en su latitud, longitud, baños, área total y tipo de propiedad.

*Resultados y Evaluación:*
* *Precisión (R2):* 0.25
* *Margen de Error Absoluto (MAE):* 52,500 USD

*Insights y Conclusiones del Modelo:*
A primera vista, un R2 de 0.25 indica un rendimiento bajo del modelo; sin embargo, este resultado es interesante. Nos demuestra empíricamente que, en el mercado inmobiliario de Quito, el precio no está dictado únicamente por los metros cuadrados o los baños. Existen variables latentes u ocultas (no incluidas en este dataset) que dictan el valor real, tales como:
* Antigüedad de la construcción.
* Nivel de seguridad del sector o urbanización.
* Calidad de los acabados.

*Detección de Anomalías:*
Al utilizar el modelo para encontrar discrepancias entre el Precio Real y el Precio estimado, la Inteligencia Artificial fue capaz de identificar listados atípicos (por ejemplo, propiedades catalogadas con 950 m2 a solo 52,000 USD). Esto demuestra que el Machine Learning no solo sirve para predecir precios, sino que es una herramienta excepcional para realizar *control de calidad de datos* y auditar bases de datos inmobiliarias masivas en busca de errores humanos de digitación.