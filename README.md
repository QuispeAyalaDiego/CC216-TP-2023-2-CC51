
#  TRABAJO PARCIAL
## Análisis Exploratorio de un conjunto de Datos
#####  Carrera: Ciencias de la Computación


|AUTORES    |
| ----------|
| Quispe Ayala Diego Juan Pablo  |
| Roque Ponce, Christian Alonso     |
| Retuerto Diaz, Pedro Alejandro   |
| Luis Lázaro, Daniel Orlando    |


------------



[INDICE](#título-principal)
1. [Objetivo del trabajo](#sección-1)
2. [Descripción del dataset](#sección-1)
3. [Conclusiones](#sección-1)
4. [Licencia](#sección-2)
------------
#### 1. OBJETIVO DEL TRABAJO

Como obejtivo del trabajo es realizar un análisis expliratorio de un  conjunto de datos (EDA), creando visualizaciones, 
preparando los datos y obteniendo inferencias básicas utilizando R/RStudio como herramienta de software. Dicho conjunto de datos que consta de dos partes, una correspondiente al hotel resort (H1) y la otra al hotel de ciudad (H2). Ambos conjuntos de datos tienen una estructura similar y comprenden un total de 40,060 observaciones para H1 y 79,330 observaciones para H2. Cada observación representa una reserva de hotel. Los datos cubren el período desde el 1 de julio de 2015 hasta el 31 de agosto de 2017 e incluyen tanto reservas que llegaron efectivamente como reservas que fueron canceladas. Se eliminaron todos los elementos de datos relacionados con la identificación de hoteles o clientes para preservar la privacidad.
Este conjunto de datos proviene del articulo titulado "Hotel booking demand datasets," se describe en un artículo de datos y es el resultado de la colaboración de Nuno Antonio, Ana de Almeida y Luis Nunes de diversas instituciones en Portugal, incluyendo el Instituto Universitário de Lisboa (ISCTE-IUL) y el Instituto de Telecomunicações. 
#### 2. DESCRIPCIÓN DEL DATA SET
En la siguiente tabla se muestra el nombre de cada una de las 32 columnas que conforman el dataset, así como el tipo de dato y una breve descripción de su contenido:

|nº | Nombre de la Columna | Tipo de Datos | Descripción |
| ------------ | ------------ | ------------ | ------------ |
| 1 | hotel | Carácter (string) | Tipo de hotel (urbano o resort)|
|2| is_canceled | Entero (int) | Indica si la reserva fue cancelada (1) o no (0). |
|  3 |lead_time | Entero (int) | Tiempo en días entre la reserva y la llegada. |
|  4| Fila 4, Col 2 | Entero (int)| Tiempo en días entre la reserva y la llegada. |
|5 | Fila 5, Col 2 | Fila 5, Col 3 | Fila 5, Col 4 |
|6 | Fila 6, Col 2 | Fila 6, Col 3 | Fila 6, Col 4 |
| Fila 7, Col 1 | Fila 7, Col 2 | Fila 7, Col 3 | Fila 7, Col 4 |
| Fila 8, Col 1 | Fila 8, Col 2 | Fila 8, Col 3 | Fila 8, Col 4 |
| Fila 9, Col 1 | Fila 9, Col 2 | Fila 9, Col 3 | Fila 9, Col 4 |
| Fila 10, Col 1 | Fila 10, Col 2 | Fila 10, Col 3 | Fila 10, Col 4 |
| Fila 11, Col 1 | Fila 11, Col 2 | Fila 11, Col 3 | Fila 11, Col 4 |
| Fila 12, Col 1 | Fila 12, Col 2 | Fila 12, Col 3 | Fila 12, Col 4 |
| Fila 13, Col 1 | Fila 13, Col 2 | Fila 13, Col 3 | Fila 13, Col 4 |
| Fila 14, Col 1 | Fila 14, Col 2 | Fila 14, Col 3 | Fila 14, Col 4 |
| Fila 15, Col 1 | Fila 15, Col 2 | Fila 15, Col 3 | Fila 15, Col 4 |
| Fila 16, Col 1 | Fila 16, Col 2 | Fila 16, Col 3 | Fila 16, Col 4 |
| Fila 17, Col 1 | Fila 17, Col 2 | Fila 17, Col 3 | Fila 17, Col 4 |
| Fila 18, Col 1 | Fila 18, Col 2 | Fila 18, Col 3 | Fila 18, Col 4 |
| Fila 19, Col 1 | Fila 19, Col 2 | Fila 19, Col 3 | Fila 19, Col 4 |
| Fila 20, Col 1 | Fila 20, Col 2 | Fila 20, Col 3 | Fila 20, Col 4 |
| Fila 21, Col 1 | Fila 21, Col 2 | Fila 21, Col 3 | Fila 21, Col 4 |
| Fila 22, Col 1 | Fila 22, Col 2 | Fila 22, Col 3 | Fila 22, Col 4 |
| Fila 23, Col 1 | Fila 23, Col 2 | Fila 23, Col 3 | Fila 23, Col 4 |
| Fila 24, Col 1 | Fila 24, Col 2 | Fila 24, Col 3 | Fila 24, Col 4 |
| Fila 25, Col 1 | Fila 25, Col 2 | Fila 25, Col 3 | Fila 25, Col 4 |
| Fila 26, Col 1 | Fila 26, Col 2 | Fila 26, Col 3 | Fila 26, Col 4 |
| Fila 27, Col 1 | Fila 27, Col 2 | Fila 27, Col 3 | Fila 27, Col 4 |
| Fila 28, Col 1 | Fila 28, Col 2 | Fila 28, Col 3 | Fila 28, Col 4 |
| Fila 29, Col 1 | Fila 29, Col 2 | Fila 29, Col 3 | Fila 29, Col 4 |
| Fila 30, Col 1 | Fila 30, Col 2 | Fila 30, Col 3 | Fila 30, Col 4 |
| Fila 31, Col 1 | Fila 31, Col 2 | Fila 31, Col 3 | Fila 31, Col 4 |
| Fila 32, Col 1 | Fila 32, Col 2 | Fila 32, Col 3 | Fila 32, Col 4 |






------------
BIBLIOGRAFIA

Antonio,N.,deAlmeida,A.,&Nunes,L. (2019).Hotelbookingdemanddatasets.Datainbrief,22,41-49.Recuperadode:
https://doi.org/10.1016/j.dib.2018.11.126 [Consulta:03de mayodel2023]
