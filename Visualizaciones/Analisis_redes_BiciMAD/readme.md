# Análisis de redes sobre los viajes en bicicletas de BICIMAD

## 1. Introducción

Las visualizaciones son representaciones gráficas de datos que permiten comunicar de manera sencilla y efectiva la información ligada a los mismos. Las posibilidades de visualización son muy amplias, desde representaciones básicas, como puede ser un gráfico de líneas, barras o sectores, hasta visualizaciones configuradas sobre cuadros de mando o dashboards interactivos. Las visualizaciones juegan un papel fundamental en la extracción de conclusiones utilizando el lenguaje visual, permitiendo además detectar patrones, tendencias, datos anómalos o proyectar predicciones, entre otras muchas funciones.  

En esta sección de [“Visualizaciones paso a paso”](https://datos.gob.es/es/documentacion/tipo/visualizaciones-paso-paso-3923) estamos presentando periódicamente ejercicios prácticos de visualizaciones de datos abiertos disponibles en  datos.gob.es u otros catálogos similares. En ellos se abordan y describen de manera sencilla las etapas necesarias para obtener los datos, realizar las transformaciones y análisis que resulten pertinentes para, finalmente, la creación de visualizaciones interactivas, de las que podemos extraer información resumida en unas conclusiones finales. En cada uno de estos ejercicios prácticos, se utilizan sencillos desarrollos de código convenientemente documentados, así como herramientas de uso gratuito. Todo el material generado está disponible para su reutilización en el repositorio del laboratorio de datos de Github perteneciente a datos.gob.es.

En este ejercicio práctico, hemos realizado un sencillo desarrollo de código que está convenientemente documentado apoyandonos en herramientas de uso gratuito. 

[Accede al repositorio del laboratorio de datos en Github.](https://github.com/datosgobes/Laboratorio-de-Datos/tree/main/Visualizaciones/Analisis_redes_BiciMAD)

[Ejecuta el código de pre-procesamiento de datos sobre Google Colab.](https://colab.research.google.com/drive/1gb0hoL04K45BwObukLVburW0pfLtn70h?usp=sharing)

## 2. Objetivo
El objetivo principal de este ejercicio es mostrar cómo realizar un análisis de redes o de grafos partiendo de datos abiertos sobre viajes en bicicleta de alquiler en la ciudad de Madrid. Para ello, realizaremos un preprocesamiento de los datos con la finalidad de obtener las tablas que utilizaremos a continuación en la herramienta generadora de la visualización, con la que crearemos las visualizaciones del grafo. 

Los análisis de redes son métodos y herramientas para el estudio y la interpretación de las relaciones y conexiones entre entidades o nodos interconectados de una red, pudiendo ser estas entidades personas, sitios, productos, u organizaciones, entre otros. Los análisis de redes buscan descubrir patrones, identificar comunidades, analizar la influencia y determinar la importancia de los nodos dentro de la red. Esto se logra mediante el uso de algoritmos y técnicas específicas para extraer información significativa de los datos de red. 

Una vez analizados los datos mediante esta visualización, podremos contestar a preguntas como las que se plantean a continuación:  
- ¿Cuál es la estación de la red con mayor tráfico de entrada y de salida? 
- ¿Cuáles son las rutas entre estaciones más frecuentes? 
- ¿Cuál es el número medio de conexiones entre estaciones para cada una de ellas? 
- ¿Cuáles son las estaciones más interconectadas dentro de la red?

## 3. Recursos
### 3.1 Conjuntos de datos
Los conjuntos de datos abiertos utilizados contienen información sobre los viajes en bicicleta de préstamo realizados en la ciudad de Madrid. La información que aportan se trata de la estación de origen y de destino, el tiempo del trayecto, la hora del trayecto, el identificador de la bicicleta, …
Estos conjuntos de datos abiertos son publicados por el Ayuntamiento de Madrid, mediante ficheros que recogen los registros de forma mensual.

[Series mensuales datos estáticos BICIMAD](https://datos.gob.es/es/catalogo/l01280796-bicimad-datos-de-los-itinerarios-de-las-bicicletas-electricas1)

### 3.1 Herramientas
Para la realización de las tareas de preprocesado de los datos se ha utilizado el lenguaje de programación Python escrito sobre un Notebook de Jupyter alojado en el servicio en la nube de [Google Colab](https://colab.research.google.com/?hl=es). "Google Colab" o, también llamado Google Colaboratory, es un servicio en la nube de Google Research que permite programar, ejecutar y compartir código escrito en Python o R sobre un Jupyter Notebook desde tu navegador, por lo que no requiere configuración. Este servicio es gratuito.

Para la creación de la visualización interactiva se ha usado la herramienta [Gephi](https://gephi.org/) "Gephi" es una herramienta de visualización y análisis de redes. Permite representar y explorar relaciones entre elementos, como nodos y enlaces, con el fin de entender la estructura y patrones de la red. El programa precisa descarga y es gratuito.

Si quieres conocer más sobre herramientas que puedan ayudarte en el tratamiento y la visualización de datos, puedes recurrir al informe ["Herramientas de procesado y visualización de datos"](https://datos.gob.es/es/documentacion/herramientas-de-procesado-y-visualizacion-de-datos).

## 4. Tratamiento o preparación de datos
Los procesos que te describimos a continuación los encontrarás comentados en el [Notebook](https://colab.research.google.com/drive/1gb0hoL04K45BwObukLVburW0pfLtn70h) que también podrás ejecutar desde Google Colab. Debido al alto volumen de viajes registrados en los conjuntos de datos, definimos los siguientes puntos de partida a la hora de analizarlos:
- Analizaremos la hora del día con mayor tráfico de viajes
- Analizaremos las estaciones con un mayor volumen de viajes
  
Antes de lanzarnos a analizar y construir una visualización efectiva, debemos realizar un tratamiento previo de los datos, prestando especial atención a su obtención y a la validación de su contenido, asegurándonos que se encuentran en el formato adecuado y consistente para su procesamiento y que no contienen errores.

Como primer paso del proceso, es necesario realizar un análisis exploratorio de los datos (EDA), con el fin de interpretar adecuadamente los datos de partida, detectar anomalías, datos ausentes o errores que pudieran afectar a la calidad de los procesos posteriores y resultados. Si quieres conocer más sobre este proceso puedes recurrir a la [Guía Práctica de Introducción al Análisis Exploratorio de Datos](https://datos.gob.es/es/documentacion/guia-practica-de-introduccion-al-analisis-exploratorio-de-datos).

El siguiente paso es generar la tabla de datos preprocesada que usaremos para alimentar la herramienta de análisis de redes (Gephi) que de forma visual nos ayudará a comprender la información. Para ello modificaremos, filtraremos y uniremos los datos según nuestras necesidades.

Los pasos que se siguen en este preprocesamiento de los datos, explicados en este Notebook de Google Colab, son los siguientes:
1. Instalación de librerías y carga de los conjuntos de datos
2. Análisis exploratorio de los datos (EDA)
3. Generación de tablas preprocesadas
4. 
Podrás reproducir este análisis con el código fuente que está disponible en nuestra cuenta de GitHub. La forma de proporcionar el código es a través de un documento realizado sobre un Jupyter Notebook que, una vez cargado en el entorno de desarrollo, podrás ejecutar o modificar de manera sencilla.

Debido al carácter divulgativo de este post y para favorecer el entendimiento de los lectores no especializados, el código no pretende ser el más eficiente sino facilitar su comprensión, por lo que posiblemente se te ocurrirán muchas formas de optimizar el código propuesto para lograr fines similares. ¡Te animamos a que lo hagas!

## 5. Análisis de la red

### 5.1 Definición de la red
La red analizada se encuentra formada por los viajes entre distintas estaciones de bicicletas en la ciudad de Madrid, teniendo como principal información de cada uno de los viajes registrados la estación de origen (denominada como “source”) y la estación de destino (denominada como “target”). 

La red está formada por 253 nodos (estaciones) y 3012 aristas (interacciones entre las estaciones). Se trata de un grafo dirigido, debido a que las interacciones son bidireccionales y ponderado, debido a que cada arista entre los nodos tiene asociado un valor numérico denominado "peso" que en este caso corresponde al número de viajes realizados entre ambas estaciones.

### 5.2 Carga de la tabla preprocesada en Gephi
Mediante la opción “importar hoja de cálculo” de la pestaña archivo, importamos en formato CSV la tabla de datos previamente preprocesada. Gephi detectará que tipo de datos se están cargando, por lo que utilizaremos los parámetros predefinidos por defecto.

![Imagen 1](https://github.com/datosgobes/Laboratorio-de-Datos/assets/13691480/0e998eea-3090-4354-9865-37c037da59bd)




