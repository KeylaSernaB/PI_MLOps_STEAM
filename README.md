# <h1 align=center> **PROYECTO INDIVIDUAL Nº1** </h1>

# <h1 align=center>**`Proyecto de Machine Learning Operations (MLOps): Sistema de Recomendación de Videojuegos para Usuarios de Steam`**</h1>

<p align="center">
<img src="https://user-images.githubusercontent.com/67664604/217914153-1eb00e25-ac08-4dfa-aaf8-53c09038f082.png"  height=300>
</p>

## Descripción del Proyecto
Este proyecto simula el rol como Data Scientist en Steam, una plataforma multinacional de videojuegos. Para su desarrollo, se entregan unos datos y se solicita un Producto Mínimo Viable que muestre una API deployada en un servicio en la nube y la aplicación de dos modelos de Machine Learning, por una lado, un análisis de sentimientos sobre los comentarios de los usuarios de los juegos y, por otro, la recomendación de juegos a partir de dar el nombre de un juego y/o a partir de los gustos de un usuario en particular.

## Datos

Para este proyecto se proporcionaron tres archivos JSON:

* **australian_user_reviews.json** es un dataset que contiene los comentarios que los usuarios realizaron sobre los juegos que consumen, además de datos adicionales como si recomiendan o no ese juego, emoticones de gracioso y estadísticas de si el comentario fue útil o no para otros usuarios. También presenta el id del usuario que comenta con su url del perfil y el id del juego que comenta.

* **australian_users_items.json** es un dataset que contiene información sobre los juegos que juegan todos los usuarios, así como el tiempo acumulado que cada usuario jugó a un determinado juego.

* **output_steam_games.json** es un dataset que contiene datos relacionados con los juegos en sí, como los título, el desarrollador, los precios, características técnicas, etiquetas, entre otros datos.

## **Fuente de datos**
+ [Dataset](https://drive.google.com/drive/folders/1HqBG2-sUkz_R3h1dZU5F2uAzpRn7BS) se encuetran el archivo que ha sido procesado.
+ [Diccionario de datos](https://docs.google.com/spreadsheets/d/1-t9HLzLHIGXvliq56UE_gMaWBVTPfrlTf2D9uAtLGrk/edit?usp=drive_link): Diccionario con algunas descripciones de las columnas disponibles en el dataset.<br/> 

## Tareas desarrolladas  <br />

### **ETL (Extracción, Transformación y Carga):** <br />
Esta primera etapa se centra en extraer los archivos JSON y convertirlos a archivos CSV. Se realiza la desanidación de las columnas, manteniendo solo aquellas necesarias para el sistema de recomendación y los endpoints propuestos. También se lleva a cabo el tratamiento de valores faltantes con el objetivo de dejar los datos limpios y preparados para su uso en los endpoints y el sistema de recomendación.
El proceso detallado se describe en el [Proceso de ETL](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/1.%20ETL.ipynb). 

### **Feature Engineering:** 
Se ha creado la columna 'sentiment_analysis' aplicando análisis de sentimiento a las reseñas de los usuarios mediante la librería NLTK. La asignación de valores es la siguiente: '0' si es una reseña negativa, '1' si es neutral y '2' si es positiva. Esta nueva columna se ha introducido para reemplazar la columna original 'user_reviews.review', facilitando así el trabajo de los modelos de machine learning y el análisis de datos.

Para obtener más detalles sobre este proceso se puede consultar la sección correspondiente en el [notebook de análisis de sentimiento](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/2.%20analisis_sentimientos.ipynb).

### **3.- Funciones de consultas** <br />

- **def PlayTimeGenre( genero : str ):** Debe devolver año con más horas jugadas para dicho género.[Notebook](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/3.PlayTimeGenre.ipynb)

Ejemplo de retorno: {"Año de lanzamiento con más horas jugadas para Género X" : 2013}. 

- **def UserForGenre( genero : str ):** Debe devolver el usuario que acumula más horas jugadas para el género dado y una lista de la acumulación de horas jugadas por año.[Notebook](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/4.user_for_genre.ipynb)

Ejemplo de retorno: {"Usuario con más horas jugadas para Género X" : us213ndjss09sdf, "Horas jugadas":[{Año: 2013, Horas: 203}, {Año: 2012, Horas: 100}, {Año: 2011, Horas: 23}]}.

- **def UsersRecommend( año : int ):** Devuelve el top 3 de juegos más recomendados por usuarios para el año dado. (reviews.recommend = True y comentarios positivos/neutrales)[Notebook](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/5.user_recommend.ipynb)

Ejemplo de retorno: [{"Puesto 1" : X}, {"Puesto 2" : Y},{"Puesto 3" : Z}].

- **def UsersWorstDeveloper( año : int ):** Devuelve el top 3 de desarrolladoras con juegos menos recomendados por usuarios para el año dado. (reviews.recommend = False y comentarios negativos)[Notebook](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/6.user_worst_developer.ipynb)

Ejemplo de retorno: [{"Puesto 1" : X}, {"Puesto 2" : Y},{"Puesto 3" : Z}].

- **def sentiment_analysis( empresa desarrolladora : str ):** Según la empresa desarrolladora, se devuelve un diccionario con el nombre de la desarrolladora como llave y una lista con la cantidad total de registros de reseñas de usuarios que se encuentren categorizados con un análisis de sentimiento como valor.[Notebook](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/7.sentiment_analysis.ipynb)

Ejemplo de retorno: {'Valve' : [Negative = 182, Neutral = 120, Positive = 278]}

### **Desarrollo de API**
Se implementó una API utilizando FastApi para exponer las funciones de consulta como endpoints y tambien se usó Render. El deploy de la API se encuentra en: https://ml-ksb.onrender.com/docs. El código para la API se encuentra en el archivo [main.py](https://github.com/KeylaSernaB/PI_MLOps_STEAM/blob/main/main.py).

### **Análisis Exploratorio de Datos (EDA)**
Realicé el análisis exploratorio de datos (EDA). Durante este proceso, se exploraron y examinaron  los conjuntos de datos. 
[Notebook del Análisis Exploratorio de Datos (EDA)]().

### **Video Explicativo**
Creé un video explicativo del proyecto y detallando el uso de los endpoints desplegados en la plataforma Render.
[Video]().




