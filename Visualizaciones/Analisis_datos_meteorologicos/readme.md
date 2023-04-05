# Análisis de datos meteorológicos registrados en los últimos años

## 1. Introducción
Las visualizaciones son representaciones gráficas de datos que permiten comunicar de manera sencilla y efectiva la información ligada a los mismos. Las posibilidades de visualización son muy amplias, desde representaciones básicas, como puede ser un gráfico de líneas, barras o sectores, hasta visualizaciones configuradas sobre cuadros de mando o dashboards interactivos. Las visualizaciones juegan un papel fundamental en la extracción de conclusiones utilizando el lenguaje visual, permitiendo además detectar patrones, tendencias, datos anómalos o proyectar predicciones, entre otras muchas funciones.  

En esta sección de [“Visualizaciones paso a paso”](https://datos.gob.es/es/documentacion/tipo/visualizaciones-paso-paso-3923) estamos presentando periódicamente ejercicios prácticos de visualizaciones de datos abiertos disponibles en  datos.gob.es u otros catálogos similares. En ellos se abordan y describen de manera sencilla las etapas necesarias para obtener los datos, realizar las transformaciones y análisis que resulten pertinentes para, finalmente, la creación de visualizaciones interactivas, de las que podemos extraer información resumida en unas conclusiones finales. En cada uno de estos ejercicios prácticos, se utilizan sencillos desarrollos de código convenientemente documentados, así como herramientas de uso gratuito. Todo el material generado está disponible para su reutilización en el repositorio del [laboratorio de datos de Github](https://github.com/datosgobes/Laboratorio-de-Datos/tree/main/Visualizaciones/Analisis_datos_meteorologicos) perteneciente a datos.gob.es.

## 2. Objetivo
El objetivo principal de este ejercicio es hacer un análisis de los datos meteorológicos recogidos en varias estaciones durante los últimos años. Para realizar este análisis utilizaremos distintas visualizaciones generadas mediante la librería “ggplot2” del lenguaje de programación “R” 

De todas las estaciones meteorológicas españolas, hemos decidido analizar dos de ellas, una en la provincia más fría del país (Burgos) y otra en la provincia más cálida del país (Córdoba), según los datos de la AEMET. Se buscarán patrones y tendencias en los distintos registros entre los años 1990 y 2020 con la finalizad de entender la evolución meteorológica sufrida en este periodo de tiempo. 

Una vez analizados los datos, podremos contestar a preguntas como las que se muestran a continuación: 
¿Cuál es la tendencia en la evolución de las temperaturas en los últimos años? 
¿Cuál es la tendencia en la evolución de las precipitaciones en los últimos años? 
¿Qué estación meteorológica (Burgos o Córdoba) presenta una mayor variación de los datos climatológicos en estos últimos años? 
¿Qué grado de correlación hay entre las distintas variables climatológicas registradas? 

Estas, y muchas otras preguntas pueden ser resueltas mediante el uso de herramientas como ggplot2 que facilitan la interpretación de los datos mediante visualizaciones interactivas.

## 3. Recursos
### 3.1 Conjunto de datos
Los conjuntos de datos contienen distinta información meteorológica de interés para las dos estaciones en cuestión desglosados por año. Dentro del centro de descargas de la AEMET, podremos descárgalos, previa solicitud de la clave API, en el apartado “climatologías mensuales/anuales”. De las estaciones meteorológicas existentes, hemos seleccionado dos de las que obtendremos los datos: Burgos aeropuerto (2331) y Córdoba aeropuerto (5402) 

Cabe destacar, que, junto a los conjuntos de datos, también podremos descargar sus metadatos, los cuales son de especial importancia a la hora de identificar las distintas variables registradas en los conjuntos de datos. Estos conjuntos de datos también se encuentran disponibles en el repositorio [laboratorio de datos de Github](https://github.com/datosgobes/Laboratorio-de-Datos/tree/main/Visualizaciones/Analisis_datos_meteorologicos)

### 3.2 Herramientas
Para la realización de las tareas de preprocesado de los datos se ha utilizado el lenguaje de programación R escrito sobre un Notebook de Jupyter alojado en el servicio en la nube de [Google Colab](https://colab.research.google.com/?hl=es).

"Google Colab" o, también llamado Google Colaboratory, es un servicio en la nube de Google Research que permite programar, ejecutar y compartir código escrito en Python o R sobre un Jupyter Notebook desde tu navegador, por lo que no requiere configuración. Este servicio es gratuito.

Para la creación de las visualizaciones se ha usado la librería [ggplot2](https://ggplot2.tidyverse.org/).

"ggplot2" es un paquete de visualización de datos para el lenguaje de programación R. Se centra en la construcción de gráficos a partir de capas de elementos estéticos, geométricos y estadísticos. ggplot2 ofrece una amplia gama de gráficos estadísticos de alta calidad, incluyendo gráficos de barras, gráficos de líneas, diagramas de dispersión, gráficos de caja y bigotes, y muchos otros  

Si quieres conocer más sobre herramientas que puedan ayudarte en el tratamiento y la visualización de datos, puedes recurrir al informe "Herramientas de procesado y visualización de datos".

## 4. Tratamiento o preparación de los datos
Los procesos que te describimos a continuación los encontrarás comentados en el [Notebook](https://colab.research.google.com/drive/1YQurWKgZXEj8uj69YHtDOa1Vv7KpAAKy) que también podrás ejecutar desde Google Colab. 

Antes de lanzarnos a construir una visualización efectiva, debemos realizar un tratamiento previo de los datos, prestando especial atención a la obtención de los mismos y validando su contenido, asegurando que se encuentran en el formato adecuado y consistente para su procesamiento y que no contienen errores.  

Como primer paso del proceso, una vez importadas las librerías necesarias y cargados los conjuntos de datos, es necesario realizar un análisis exploratorio de los datos (EDA) con el fin de interpretar adecuadamente los datos de partida, detectar anomalías, datos ausentes o errores que pudieran afectar a la calidad de los procesos posteriores y resultados. Si quieres conocer más sobre este proceso puedes recurrir a la Guía Práctica de Introducción al Análisis Exploratorio de Datos.  

El siguiente paso a dar es generar las tablas de datos preprocesadas que usaremos en las visualizaciones. Para ello, filtraremos los conjuntos de datos iniciales y calcularemos los valores que sean necesarios y de interés para el análisis realizado en este ejercicio. 

Una vez terminado el preprocesamiento, obtendremos las tablas de datos “datos_graficas_C” y “datos_graficas_B” las cuales utilizaremos en el siguiente apartado del Notebook para generar las visualizaciones.  

La estructura del Notebook en la que se realizan los pasos previamente descritos junto a comentarios explicativos de cada uno de ellos, es la siguiente: 

1. Instalación y carga de librerías
2. Carga de los conjuntos de datos
3. Análisis exploratorio de datos (EDA)
4. Preparación de las tablas de datos
5. Visualizaciones
6. Guardado de gráficos

Podrás reproducir este análisis, ya que el código fuente está disponible en nuestra cuenta de GitHub. La forma de proporcionar el código es a través de un documento realizado sobre un Jupyter Notebook que una vez cargado en el entorno de desarrollo podrás ejecutar o modificar de manera sencilla. Debido al carácter divulgativo de este post y de cara a favorecer el entendimiento de los lectores no especializados, el código no pretende ser el más eficiente, sino facilitar su comprensión por lo que posiblemente se te ocurrirán muchas formas de optimizar el código propuesto para lograr fines similares. ¡Te animamos a que lo hagas! 

## 5. Visualizaciones
Diversos tipos de visualizaciones y gráficos se han realizado con la finalidad de extraer información sobre las tablas de datos preprocesadas y responder a las preguntas iniciales planteadas en este ejercicio. Como se ha mencionado previamente, se ha utilizado el paquete “ggplot2” de R para realizar las visualizaciones.  

El paquete "ggplot2" es una biblioteca de visualización de datos en el lenguaje de programación R. Fue desarrollado por Hadley Wickham y es parte del conjunto de herramientas del paquete "tidyverse". El paquete "ggplot2" está construido en torno al concepto de "gramática de gráficos", que es un marco teórico para construir gráficos mediante la combinación de elementos básicos de la visualización de datos como capas, escalas, leyendas, anotaciones y temas. Esto permite crear visualizaciones de datos complejas y personalizadas, con un código más limpio y estructurado. 

Si quieres tener una visión a modo resumen de las posibilidades de visualizaciones con ggplot2, consulta la siguiente [“cheatsheet”](https://github.com/rstudio/cheatsheets/blob/main/data-visualization.pdf). También puedes obtener información más en detalle en el siguiente ["manual de uso"](https://ggplot2-book.org/).






