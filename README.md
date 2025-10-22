# Análisis Exploratorio de Indicadores Urbanos en la Ciudad de Nueva York

**Consultor:** Julián Camilo Ramos Granada  
**Entrega para:** Gobierno de la Ciudad de Nueva York 
**Curso:** Procesamiento de Datos a Gran Escala – Pontificia Universidad Javeriana  
**Fecha:** Octubre de 2025

## Contexto del Proyecto

Este repositorio documenta la primera entrega de un proyecto académico que simula una consultoría para el gobierno de la ciudad de Nueva York. El objetivo es contribuir, mediante análisis de datos, a la formulación de un plan de acción para mejorar dos indicadores críticos: la cantidad de arrestos y la frecuencia de accidentes viales. El trabajo se desarrolla siguiendo la metodología CRISP-DM, implementando procesos de análisis y visualización sobre un clúster de procesamiento de datos en Apache Spark.

El enfoque combina fundamentos estadísticos, exploración visual y limpieza de datos provenientes de fuentes oficiales del portal NYC Open Data, con el propósito de tener un entendimiento profundo de los fenómenos urbanos y sociales que afectan a la ciudad.


## Actividades Realizadas

**1. Entendimiento del negocio**  
Se contextualiza la situación actual de Nueva York, destacando los retos sociales y territoriales que motivan este estudio. Se establece el objetivo consultor: generar hallazgos basados en datos que orienten decisiones sobre seguridad y movilidad.

**2. Selección de datos**  
Se seleccionaron cuatro conjuntos de datos clave:  
- Arrestos policiales (NYPD Arrest Data)  
- Colisiones vehiculares (Motor Vehicle Collisions)  
- Medición de pobreza (NYCgov Poverty Measure)  
- Desempeño educativo (SAT NYC)

**3. Configuración del entorno distribuido y carga de datos**  
El entorno de procesamiento fue desplegado manualmente mediante la configuración de un clúster de Apache Spark sobre tres máquinas virtuales con sistema operativo Rocky Linux. Una de estas máquinas fue configurada como nodo master, mientras que las otras dos actúan como nodos worker. A pesar de esto, para mayor rendimiento el nodo master también cumple funciones de worker, permitiendo así una utilización eficiente de los recursos disponibles.

Cada nodo posee una dirección IP específica y está integrado mediante los archivos de configuración de Spark y SSH sin contraseña para la orquestación del clúster. Adicionalmente, se configuró un túnel para acceder a JupyterLab desde el nodo master.

La carga de datos en este entorno incluyó la validación de esquemas, revisión de tipos de datos y verificación de la integridad estructural de cada conjunto, permitiendo su exploración y transformación.


**4. Análisis exploratorio y visualizaciones**  
Se aplicaron técnicas de estadística descriptiva y análisis visual para detectar patrones en los datos. Se generaron tablas, histogramas, boxplots y gráficos de barras. 

**5. Revisión de calidad de datos**  
Se identificaron columnas incompletas, valores atípicos y registros vacíos. Se propusieron estrategias para la imputación o eliminación, según el tipo de variable y su importancia en el análisis posterior.

**6. Formulación de preguntas de negocio**  
Se plantearon ocho preguntas relevantes para el diagnóstico territorial. Estas buscan establecer relaciones entre variables como pobreza, nivel educativo, frecuencia de arrestos y accidentes. Las respuestas se desarrollarán en la segunda fase del proyecto.

**7. Transformaciones iniciales**  
Se ejecutaron limpiezas básicas, conversiones de tipos, estandarización de nombres, eliminación de columnas irrelevantes y transformación de variables interpretadas como texto a numéricas.

## Bonos Académicos Implementados

- Extracción y análisis de datos demográficos mediante web scraping desde el portal del Departamento de Salud de Nueva York.  
- Obtención de datos climáticos mediante integración con la API de OpenWeatherMap.

## Herramientas Utilizadas

- Apache Spark (PySpark)  
- JupyterLab en entorno HPC  
- Pandas, Matplotlib, Seaborn  
- APIs públicas (OpenWeatherMap)  
- LaTeX para documentación


## Nota Final

Este repositorio corresponde a la fase exploratoria del proyecto. En la segunda entrega se responderán las preguntas de negocio mediante análisis avanzado y modelado con técnicas de aprendizaje automático supervisado y no supervisado, mediante el uso de la biblioteca MLlib de Spark.

