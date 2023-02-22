# Visualización paso a paso: Generación de mapa turístico personalizado

## 1. Introducción
Las visualizaciones son representaciones gráficas de datos que permiten comunicar de manera sencilla y efectiva la información ligada a los mismos. Las posibilidades de visualización son muy amplias, desde representaciones básicas, como puede ser un gráfico de líneas, barras o sectores, hasta visualizaciones configuradas sobre cuadros de mando o dashboards interactivos.  

En esta sección de “Visualizaciones paso a paso” estamos presentando periódicamente ejercicios prácticos de visualizaciones de datos abiertos disponibles en  datos.gob.es u otros catálogos similares. En ellos se abordan y describen de manera sencilla las etapas necesarias para obtener los datos, realizar las transformaciones y análisis que resulten pertinentes para, finalmente, la creación de visualizaciones interactivas, de las que podemos extraer información resumida en unas conclusiones finales. En cada uno de estos ejercicios prácticos, se utilizan sencillos desarrollos de código convenientemente documentados, así como herramientas de uso gratuito. Todo el material generado está disponible para su reutilización en el repositorio de GitHub.

En este ejercicio práctico, hemos realizado un sencillo desarrollo de código que está convenientemente documentado apoyandonos en herramientas de uso gratuito. 

[Accede al repositorio del laboratorio de datos en Github.](https://github.com/datosgobes/Laboratorio-de-Datos/tree/main/Visualizaciones/Generacion_mapa_personalizado)

[Ejecuta el código de pre-procesamiento de datos sobre Google Colab.](https://colab.research.google.com/drive/1MUpic-GtjNsyg-RnpJtM1eWfuhT82DAi?usp=sharing)


## 2. Objetivo
El objetivo principal de este post es mostrar cómo generar un mapa personalizado de Google Maps mediante la herramienta ["My Maps"](https://www.google.com/intl/es_ES/maps/about/mymaps/) partiendo de datos abiertos. Este tipo de mapas son altamente populares en páginas, blogs y aplicaciones del sector turístico, no obstante, la información útil proporcionada al usuario suele ser escasa.

En este ejercicio, utilizaremos el potencial de los datos abiertos para ampliar la información a mostrar en nuestro mapa y hacerlo de una forma automática. También mostraremos como realizar un enriquecimiento de los datos abiertos para añadir información de contexto que mejore significativamente la experiencia de usuario. 

Desde un punto de vista funcional, el objetivo del ejercicio es la creación de un mapa personalizado para planificar rutas turísticas por los espacios naturales de la Comunidad Autónoma de Castilla y León. Para ello se han utilizado conjuntos de datos abiertos publicados por la Junta de Castilla y León, que hemos preprocesado y adaptado a nuestras necesidades de cara a generar el mapa personalizado. 


## 3. Recursos
### 3.1 Conjuntos de datos
Los conjuntos de datos contienen distinta información turística de interés geolocalizada. Dentro del catálogo de datos abiertos de la Junta de Castilla y León, encontramos el [“diccionario de entidades”](https://datosabiertos.jcyl.es/web/jcyl/set/es/medio-ambiente/refugios/1284378322579) (sección información adicional), documento de vital importancia, ya que nos define la terminología utilizada en los distintos conjuntos de datos. 

[Miradores en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-miradores-en-espacios-naturales1)
      
[Observatorios en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-observatorios-en-espacios-naturales1)
      
[Refugios en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-refugios-en-espacios-naturales1)
      
[Árboles en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-arboles-singulares-en-espacios-naturales1)
      
[Casas del parque en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-casas-del-parque-en-espacios-naturales1)
      
[Zonas recreativas en espacios naturales](https://datos.gob.es/es/catalogo/a07002862-zonas-recreativas-en-espacios-naturales1)
      
[Registro de establecimientos hoteleros](https://datosabiertos.jcyl.es/web/jcyl/set/es/turismo/alojamientos_hoteleros/1284211831639)

Estos conjuntos de datos también se encuentran disponibles en el [repositorio de Github](https://github.com/datosgobes/Laboratorio-de-Datos/tree/main/Visualizaciones/Generacion_mapa_personalizado/Conjunto_datos_origen)


### 3.2 Herramientas
Para la realización de las tareas de preprocesado de los datos se ha utilizado el lenguaje de programación Python escrito sobre un Notebook de Jupyter alojado en el servicio en la nube de Google Colab.

[Google Colab](https://colab.research.google.com/?hl=es) o también llamado Google Colaboratory, es un servicio gratuito en la nube de Google Research que permite programar, ejecutar y compartir código escrito en Python o R desde tu navegador, por lo que no requiere la instalación de ninguna herramienta o configuración.

Para la creación de la visualización interactiva se ha usado la herramienta Google My Maps.

[Google My Maps](https://www.google.com/intl/es_ES/maps/about/mymaps/) es una herramienta online que permite crear mapas interactivos que pueden ser incrustados en sitios web o exportarse como archivos. Esta herramienta es gratuita, sencilla de usar y permite múltiples opciones de personalización.  

Si quieres conocer más sobre herramientas que puedan ayudarte en el tratamiento y la visualización de datos, puedes recurrir al informe ["Herramientas de procesado y visualización de datos".](https://datos.gob.es/es/documentacion/herramientas-de-procesado-y-visualizacion-de-datos)


## 4. Tratamiento o preparación de los datos
Los procesos que te describimos a continuación los encontrarás comentados en el [Notebook](https://colab.research.google.com/drive/1MUpic-GtjNsyg-RnpJtM1eWfuhT82DAi?usp=sharing)  que podrás ejecutar desde Google Colab.

Antes de lanzarnos a construir una visualización efectiva, debemos realizar un tratamiento previo de los datos, prestando especial atención a la obtención de los mismos y validando su contenido, asegurando que se encuentran en el formato adecuado y consistente para su procesamiento y que no contienen errores.  

Como primer paso del proceso es necesario realizar un análisis exploratorio de los datos (EDA) con el fin de interpretar adecuadamente los datos de partida, detectar anomalías, datos ausentes o errores que pudieran afectar a la calidad de los procesos posteriores y resultados. Si quieres conocer más sobre este proceso puedes recurrir a la Guía Práctica de Introducción al Análisis Exploratorio de Datos.  

El siguiente paso a dar es generar las tablas de datos preprocesados que usaremos para alimentar el mapa. Para ello, transformaremos los sistemas de coordenadas, modificaremos y filtraremos la información según nuestras necesidades. 

Los pasos que se siguen en este preprocesamiento de los datos, explicados en el [Notebook](https://colab.research.google.com/drive/1MUpic-GtjNsyg-RnpJtM1eWfuhT82DAi?usp=sharing), son los siguientes: 
