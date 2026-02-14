# Análisis Integral de Indicadores Urbanos en la Ciudad de Nueva York

**Consultor:** Julián Camilo Ramos Granada  
**Entrega para:** Gobierno de la Ciudad de Nueva York  
**Curso:** Procesamiento de Datos a Gran Escala – Pontificia Universidad Javeriana  
**Fecha:** Noviembre de 2025  

---

## Contexto del Proyecto

Este proyecto simula el trabajo de un equipo consultor contratado por el gobierno de la ciudad de Nueva York con el propósito de analizar, a partir de datos públicos, las causas y posibles soluciones frente a dos problemáticas urbanas de alto impacto: la inseguridad y la ocurrencia de accidentes viales.  

El objetivo central fue desarrollar un análisis integral que permitiera identificar patrones sociales, territoriales y económicos asociados a estos fenómenos, y a partir de ello proponer acciones orientadas a mejorar la seguridad ciudadana y la movilidad urbana.  

Para lograrlo, se aplicó la metodología **CRISP-DM (Cross Industry Standard Process for Data Mining)**, que estructuró el proceso desde la comprensión del contexto y los datos hasta la obtención de resultados e interpretación de hallazgos.  

El trabajo se desarrolló en dos fases complementarias:  
- **Fase 1:** centrada en el entendimiento del negocio, la exploración de los conjuntos de datos y la formulación de preguntas de análisis. Esta etapa permitió establecer las bases técnicas y conceptuales del estudio.  
- **Fase 2:** orientada a la preparación final de los datos, el modelado con técnicas de aprendizaje automático y la generación de respuestas, hallazgos y recomendaciones aplicables al contexto urbano.  

Durante ambas fases se utilizaron fuentes oficiales del portal **NYC Open Data** y herramientas de **Apache Spark** para el procesamiento distribuido, la limpieza, la exploración visual y el análisis predictivo de grandes volúmenes de información.  

El enfoque integró métodos estadísticos, visualización y aprendizaje automático para comprender cómo se relacionan variables como la pobreza, el nivel educativo, la seguridad y la movilidad dentro del territorio neoyorquino.


---

## Actividades Realizadas

### **1. Entendimiento del negocio**
Se analizó el contexto urbano y social de Nueva York, resaltando los desafíos relacionados con la desigualdad económica, la educación y la seguridad ciudadana. El objetivo del proyecto se definió como la generación de hallazgos basados en datos que orienten decisiones informadas en materia de movilidad y bienestar social.  

A partir de este planteamiento se formularon **ocho preguntas de negocio** centradas en las relaciones entre variables como ingreso, desempeño académico, número de arrestos y frecuencia de accidentes. Estas preguntas se usaron como base para la exploración, el análisis y el modelado de las etapas posteriores.

---

### **2. Selección de datos**
Se seleccionaron cuatro conjuntos de datos principales:  
- Arrestos policiales (**NYPD Arrest Data**)  
- Colisiones vehiculares (**Motor Vehicle Collisions**)  
- Medición de pobreza (**NYCgov Poverty Measure**)  
- Desempeño educativo (**SAT NYC**)  

Cada conjunto fue analizado para identificar su estructura, variables disponibles y posibles limitaciones. Se incorporaron además campos derivados que facilitaron la integración entre los conjuntos, como identificadores de distrito, rangos de fecha y categorías estandarizadas.

---

### **3. Configuración del entorno distribuido y carga de datos**
El procesamiento se realizó sobre un clúster propio de **Apache Spark** configurado manualmente en tres máquinas virtuales con sistema operativo **Rocky Linux**:

- **1 nodo master** (que también cumple función de worker)
- **2 nodos worker**

Cada nodo posee una dirección IP específica, comunicados mediante red interna y autenticación SSH. Desde **JupyterLab**, se ejecutaron las tareas de carga, exploración, transformación y modelado en el entorno distribuido, lo que permitió trabajar con los distintos conjuntos de datos en paralelo y optimizar la ejecución de los análisis.

---

### **4. Análisis exploratorio y visualizaciones**
Se aplicaron métodos de estadística descriptiva y visualización para comprender la distribución y comportamiento de las variables. Se generaron tablas agregadas, histogramas, boxplots, mapas de calor y gráficos comparativos que permitieron observar las diferencias entre distritos.

---

### **5. Revisión y tratamiento de la calidad de los datos**
Se identificaron columnas incompletas, valores atípicos y registros con errores de formato. Se aplicaron técnicas de limpieza y estandarización, incluyendo la eliminación de duplicados, conversión de tipos de dato, normalización de variables numéricas mediante *min–max* y homogenización de nombres de columnas.  

Los conjuntos fueron revisados para garantizar la consistencia entre fuentes y permitir su integración en un posterior análisis.

---

### **6. Transformaciones de datos**
Se realizaron transformaciones adicionales que facilitaron la modelación y el análisis conjunto. Entre ellas:  
- Creación de variables derivadas (día, mes y año de eventos).  
- Categorización de distritos según nivel de ingreso.  
- Generación de indicadores normalizados de desempeño educativo y pobreza.  
- Eliminación de variables redundantes tras el análisis de correlación.  

Estas transformaciones permitieron relacionar de forma más precisa las distintas dimensiones sociales y urbanas consideradas en el estudio.


#### Normalización de datos

- Se creó una variable binaria `label` a partir de `NYCgov_Income_Norm`:
  - **1 (alta pobreza):** ≤ 0.2586 (percentil 25)
  - **0 (baja pobreza):** > 0.2586
- Se aplicó **StandardScaler** (media=0, desviación estándar=1) a los features seleccionados.

---

### **7. Modelado y técnicas de aprendizaje automático**
Para ampliar el alcance del análisis se aplicaron modelos de **aprendizaje supervisado y no supervisado** mediante la biblioteca **MLlib** de Spark:  

#### Modelo supervisado: Regresión Logística

- Se entrenó un modelo de **Logistic Regression** con los datos normalizados.
- División de datos: **75% entrenamiento** / **25% prueba**.
- **Resultados del modelo base:**

| Métrica | Valor |
|---|---|
| AUC ROC | 1.0000 |
| Accuracy | 0.9999 |
| F1-score | 0.9999 |



#### Modelo supervisado: Red Neuronal Perceptrón Multicapa (MLP)

- Empleada para capturar relaciones no lineales entre las variables socioeconómicas y educativas.
- Los resultados confirmaron métricas altas de precisión y *AUC ROC*, comparables con la Regresión Logística.

#### Modelo no supervisado: K-Means Clustering

- Se entrenaron modelos K-Means con K = 2, 3, 4 y 5.
- Se evaluaron con **Silhouette Score**:

| K | Silhouette Score |
|---|---|
| 2 | ~0.46 |
| 3 | ~0.42 |
| 4 | ~0.41 |
| 5 | ~0.41 |

- Se seleccionó **K=5** como valor óptimo, equilibrando silhouette score e interpretabilidad.
- Se identificaron y analizaron los centroides de cada clúster en el espacio de features normalizados.

---

### **8. Principales hallazgos**
El análisis integrado mostró una relación clara entre las condiciones económicas, educativas y de seguridad. Los distritos con menor ingreso registraron mayores tasas de arrestos y menor desempeño académico, lo que evidencia un patrón territorial de desigualdad.  

En cuanto a la movilidad, se determinó que la mayoría de los accidentes se debe a factores humanos como distracción, exceso de confianza o incumplimiento de normas, con mayor incidencia en días laborales.  

Estos hallazgos sirvieron como base para formular recomendaciones orientadas a la prevención vial, la reducción de brechas territoriales y la mejora de la calidad educativa en zonas vulnerables.

---

### **9. Recomendaciones**
A partir de los resultados se plantean líneas de acción orientadas a la mejora del entorno urbano:  
- Implementar programas de **educación vial y control normativo** para reducir los accidentes provocados por errores humanos.  
- Fortalecer la **infraestructura educativa y social** en los distritos con mayores niveles de pobreza.  
- Promover políticas públicas que integren **movilidad, seguridad y educación** dentro de un mismo enfoque territorial.  
- Mejorar la **calidad y cobertura de los datos públicos**, incluyendo el registro geográfico de incidentes y la reducción de valores nulos.  

---


## Herramientas Utilizadas

| Herramienta | Uso |
|---|---|
| Apache Spark (PySpark, MLlib) | Procesamiento distribuido, StandardScaler, LogisticRegression, KMeans |
| JupyterLab | Entorno de desarrollo en clúster HPC |
| Pandas | Manipulación de DataFrames para visualización |
| Matplotlib / Seaborn | Visualización de datos (heatmaps, histogramas, boxplots) |
| APIs públicas | OpenWeatherMap para datos climáticos |
| LaTeX | Documentación formal |

---
