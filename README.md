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
El procesamiento se realizó sobre un clúster propio de **Apache Spark** configurado manualmente en tres máquinas virtuales con sistema operativo **Rocky Linux**. Una de las máquinas actuó como nodo master y las otras dos como nodos worker, comunicadas mediante red interna y autenticación SSH.  

Desde **JupyterLab**, se ejecutaron las tareas de carga, exploración, transformación y modelado en el entorno distribuido, lo que permitió trabajar con los distintos conjuntos de datos en paralelo y optimizar la ejecución de los análisis.

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

---

### **7. Modelado y técnicas de aprendizaje automático**
Para ampliar el alcance del análisis se aplicaron modelos de **aprendizaje supervisado y no supervisado** mediante la biblioteca **MLlib** de Spark:  

- **Regresión Logística:** utilizada para estimar la probabilidad de pobreza a partir de variables socioeconómicas y educativas.  
- **Red Neuronal Perceptrón Multicapa (MLP):** empleada para capturar relaciones no lineales entre las mismas variables.  
- **K-Means (K=5):** aplicado para agrupar distritos según características sociales y económicas compartidas.  

Los modelos supervisados alcanzaron métricas altas de precisión y *AUC ROC*, mientras que el modelo no supervisado permitió identificar agrupaciones territoriales con patrones sociales diferenciados.

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

## Bonos Académicos Implementados
- Extracción y análisis de datos demográficos mediante **web scraping** desde el portal del Departamento de Salud de Nueva York.  
- Integración de datos climáticos mediante la **API de OpenWeatherMap**.  
- Implementación de un **modelo adicional de aprendizaje profundo (MLP)** y comparación de su desempeño con la regresión logística.  

---

## Herramientas Utilizadas
- Apache Spark (PySpark, MLlib)  
- JupyterLab en entorno HPC  
- Pandas, Matplotlib, Seaborn  
- APIs públicas 
- LaTeX para documentación  

---

## Nota Final
El proyecto culmina con un análisis integral de las dinámicas sociales y urbanas que caracterizan a la ciudad de Nueva York. A través del procesamiento de datos a gran escala, fue posible vincular indicadores de pobreza, educación, seguridad y movilidad, revelando cómo estos factores interactúan dentro del territorio y condicionan la calidad de vida de sus habitantes.  

La aplicación de técnicas de Big Data  permitió  cumplir con los objetivos de comprender los patrones existentes y generar recomendaciones para la planificación y la toma de decisiones públicas. Así mismo, el trabajo plantea la importancia de fortalecer el análisis de datos como una práctica continua, orientada a mejorar la calidad y estructura de la información disponible. Mantener procesos de registro más completos y consistentes permitirá en el futuro contar con datos cada vez más precisos, facilitando decisiones urbanas más acertadas y sostenibles.


