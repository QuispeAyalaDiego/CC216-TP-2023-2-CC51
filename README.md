
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


##### 1.2. Casos de uso aplicables:
a. ¿Cuántas reservas se realizan por tipo de hotel? o  ¿Qué tipo de hotel prefiere la gente? 
```
> sum(missing_data_rows$hotel=="Resort Hotel"&missing_data_rows$is_canceled==0)
[1] 28938
> sum(missing_data_rows$hotel=="City Hotel"&missing_data_rows$is_canceled==0)
[1] 46228
> sum(missing_data_rows$is_canceled==0)
[1] 75166

```
- Acorde a los datos obtenidos, las personas que realizaron la reserva de cada hotel y no la cancelaron fueron las siguientes:


| NOMBRE DEL HOTEL         | RESERVAS REALIZADAS SIN CANCELACIÓN |
| ------------------------ | ---------------------------------- |
| CITY HOTEL               | 46,228                             |
| RESORT HOTEL             | 28,938                             |





- A partir de estos datos se puede corroborar que el hotel que las personas prefieren es el City Hotel, con una diferencia de 17290 reservas



b. ¿Está aumentando la demanda con el tiempo? 




```
# Crear un gráfico de barras apiladas
ggplot(missing_data_rows_seasons, aes(x = factor(arrival_date_year), y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity") +
    labs(x = "Año", y = "Número de Reservas", title = "Número de Reservas por Estación y Año") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "orange", "Otoño" = "red")) +
    theme_minimal()

```
En la siguiente gráfica y tabla hemos agrupado la cantidad de reservas realizadas, por estación y por año, para una mejor visualización de las temporadas altas y bajas.

![imagen1 PNG](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/83883211/46d2619a-ee23-4afa-8250-b6082cc9da8d)
![imagen2](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/1a051b69-d088-4d82-ba28-e3873311f8e6)
Figura 2.

A partir de las tablas y el gráfico de barras podemos concluir que la demanda “no” está aumentando a lo largo del tiempo, en el año 2015,2016,2016 hubieron 21996,56707,40687 reservas respectivamente.


c. ¿Cuándo se producen las temporadas de reservas: alta, media y baja? 





```
 # ggplot(missing_data_rows_seasons, aes(x = factor(arrival_date_year), y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity", position = "stack") +
    labs(x = "Año", y = "Número de Reservas", title = "Resumen de Reservas por Estación y Año") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "yellow", "Otoño" = "red")) +
    theme_minimal() +
    facet_wrap(~estacion, ncol = 4) # Facetado por estación

```
![imagen3](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/0556e48c-33d8-4e92-8a02-d026aaa3adbf)
Con el gráfico y los datos obtenidos podemos concluir que las temporadas más bajas son las que están en invierno, las medias son las que están en primavera y finalmente las de verano son las temporadas más altas en cuanto al número de reservas.

d. ¿Cuándo es menor la demanda de reservas? 

```
# Crear un gráfico de barras de la cantidad total de reservas por estación
ggplot(missing_data_rows_seasons, aes(x = estacion, y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity") +
    labs(x = "Estación", y = "Número de Reservas", title = "Resumen de Reservas por Estación") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "yellow", "Otoño" = "red")) +
    theme_minimal()

```
![imagen4](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/f1d73d30-075e-4ea6-a778-df6c4be8addd)

En este gráfico se puede observar que las estaciones con la peor demanda en el Hotel es la estación de invierno.

e. ¿Cuántas reservas incluyen niños y/o bebes? 

```
pie(conteo_bebes, labels = c("No tiene niño o bebe", "Tiene niño o bebe"), col = c("chartreuse1", "darkturquoise")	


```
![imagennn55](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/83883211/9eb84a51-ea91-45d6-9be0-f763b930c238)
Verificando la cantidad de reservas que tuvieron un niño o bebé como huésped, se puede visualizar que fueron 9332

f. ¿Es importante contar con espacios de estacionamiento?

```
# Filtrar los datos para obtener personas que no han cancelado (0)
personas_no_canceladas <- missing_data_rows[missing_data_rows$is_canceled == 0, ]
# Crear un dataframe para el gráfico
df_grafico <- data.frame(
Grupo = c("Necesitaron Estacionamiento", "No Necesitaron Estacionamiento"),
Suma_Estacionamiento = c(sum(personas_no_canceladas$required_car_parking_spaces > 0),
sum(personas_no_canceladas$required_car_parking_spaces == 0))
)
# Crear el gráfico de barras
ggplot(df_grafico, aes(x = Grupo, y = Suma_Estacionamiento, fill = Grupo)) +
geom_bar(stat = "identity") +
labs(x = "Grupo", y = "Suma de Estacionamiento", title = "Comparación de Espacios de Estacionamiento Solicitados") +
scale_fill_manual(values = c("Necesitaron Estacionamiento" = "blue", "No Necesitaron Estacionamiento" = "red")) +
theme_minimal()
```
![imagen6](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/7e77dcad-953a-4cf6-a118-95908f2bb283)
Según lo visto en la anterior gráfica podemos observar que no es necesario contar con espacios de estacionamiento. De las 75166 reservas, solo 7416 pidieron que esta disponga de al menos un estacionamiento.

g. ¿En qué meses del año se producen más cancelaciones de reservas?

```
# Convertir la columna 'reservation_status_date' a formato de fecha 
missing_data_rows$reservation_status_date <-as.Date(missing_data_rows$reservation_status_date)

# Crear una nueva columna 'Mes' para extraer el mes de la fecha de 'reservation_status_date'
missing_data_rows <- missing_data_rows %>%
    mutate(Mes = format(reservation_status_date, "%Y-%m"))

# Filtrar los datos para obtener solo las cancelaciones (is_canceled == 1)
cancelaciones <- missing_data_rows %>%
    filter(is_canceled == 1)

# Contar la cantidad de cancelaciones por mes
conteo_cancelaciones <- cancelaciones %>%
    group_by(Mes) %>%
    summarize(Cantidad = n())

# Crear el gráfico de barras
ggplot(conteo_cancelaciones, aes(x = Mes, y = Cantidad)) +
    geom_bar(stat = "identity", fill = "blue") +
    labs(x = "Mes", y = "Cantidad de Cancelaciones", title = "Cancelaciones por Mes") +
    theme_minimal() +
    theme(axis.text.x = element_text(angle = 90, hjust = 1))


```
![imagen7](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/03287359-fdf7-42a8-8c95-319e540ac3fc)
Figura 7.
En el siguiente gráfico se puede apreciar que durante el mes de enero del año 2017 se concentró la mayor cantidad de cancelaciones, con un valor de 2616.




------------
#### 2. Data base

Descripción de la estructura de los datos (tabla conteniendo la estructura y descripción de cada uno de los datos).

En la siguiente tabla se muestra el nombre de cada una de las 32 columnas que conforman el dataset, así como el tipo de dato y una breve descripción de su contenido:



| Nº          | Tipo de Datos  | Descripción                                            |
| ---------------------------- | ---------------| ------------------------------------------------------ |
| 1                            | hotel          | Carácter (string) | Tipo de hotel (urbano o resort).   |
| 2                            | is_canceled    | Entero (int) | Indica si la reserva fue cancelada (1) o no (0). |
| 3                            | lead_time      | Entero (int) | Tiempo en días entre la reserva y la llegada. |
| 4                            | arrival_date_year | Entero (int) | Año de llegada.                       |
| 5                            | arrival_date_month | Carácter (string) | Mes de llegada.                |
| 6                            | arrival_date_week_number | Entero (int) | Número de semana del año de llegada. |
| 7                            | arrival_date_day_of_month | Entero (int) | Día del mes de llegada.          |
| 8                            | stays_in_weekend_nights | Entero (int) | Número de noches de fin de semana. |
| 9                            | stays_in_week_nights | Entero (int) | Número de noches de la semana.     |
| 10                           | adults         | Entero (int) | Cantidad de adultos.                   |
| 11                           | children       | Entero (int) | Cantidad de niños.                     |
| 12                           | babies         | Entero (int) | Cantidad de bebés.                     |
| 13                           | meal           | Carácter (string) | Tipo de comida reservada.         |
| 14                           | country        | Carácter (string) | País de origen del huésped.        |
| 15                           | market_segment | Carácter (string) | Segmento de mercado de la reserva. |
| 16                           | distribution_channel | Carácter (string) | Canal de distribución de la reserva. |
| 17                           | is_repeated_guest | Entero (int) | Indica si el huésped es repetitivo (1) o no (0). |
| 18                           | previous_cancellations | Entero (int) | Número de reservas canceladas previamente por el cliente. |
| 19                           | previous_bookings_not_canceled | Entero (int) | Número de reservas previas no canceladas por el cliente. |
| 20                           | reserved_room_type | Carácter (string) | Tipo de habitación reservada.       |
| 21                           | assigned_room_type | Carácter (string) | Tipo de habitación asignada.        |
| 22                           | booking_changes | Entero (int) | Número de cambios realizados en la reserva. |
| 23                           | deposit_type   | Carácter (string) | Tipo de depósito utilizado en la reserva. |
| 24                           | agent          | Entero (int) | Agente que realizó la reserva.          |
| 25                           | company        | Entero (int) | Empresa asociada a la reserva.           |
| 26                           | days_in_waiting_list | Entero (int) | Número de días en lista de espera.  |
| 27                           | customer_type  | Carácter (string) | Tipo de cliente (por ejemplo, Transitorios, Grupos, etc.). |
| 28                           | adr            | Numérico (float) | Tasa diaria promedio (Average Daily Rate). |
| 29                           | required_car_parking_spaces | Entero (int) | Cantidad de espacios de estacionamiento requeridos. |
| 30                           | total_of_special_requests | Entero (int) | Número total de solicitudes especiales. |
| 31                           | reservation_status | Carácter (string) | Estado de la reserva.                |
| 32                           | reservation_status_date | Fecha (date) | Fecha del estado de la reserva.       |


#### ANÁLISIS EXPLORATORIO DE DATOS
##### CARGAR DATOS  

``
url<-"C:/Users/Proyecto/Downloads/hotel_bookings.csv"
 datos<-read.csv(url,sep = ",",header = TRUE,stringsAsFactors = FALSE)
 View(datos) ``

![imagen8](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/35d3139c-e117-4b5f-b5b3-2450bff62de9)


##### INSPECCIONAR DATOS
![imagen9](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/f613d2a5-7e4c-4605-9a0c-3a5b75c901c0)

![imagen10](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/5a10328a-f458-4aca-8b90-bdc73e01661a)


##### PRE-PROCESAR DATOS 

- Identificar datos faltantes o NA:

Para identificar los datos faltantes, procedimos a realizar un proceso de filtrado en el conjunto de datos con el fin de detectar todas las observaciones que presentan valores nulos, representados como "NA" o "NULL" en sus respectivas características.


Adicionalmente, se observó que varias columnas presentan valores iguales a cero. En este sentido, se plantea la necesidad de considerar si es pertinente llevar a cabo una limpieza de datos en estas columnas o, en caso contrario, eliminarlas en caso de que no sean relevantes para las interrogantes planteadas en el análisis exploratorio de los datos.

A continuación, se presenta el fragmento de código y el gráfico correspondiente:


``
[
missing_data_rows <- hotel_data %>%
select(hotel,is_canceled,lead_time,arrival_date_year,arrival_date_month,arrival_date_week_number,arrival_date_day_of_month,stays_in_weekend_nights,stays_in_week_nights,adults,children,babies,meal,country,market_segment,distribution_channel,is_repeated_guest,previous_cancellations,previous_bookings_not_canceled,reserved_room_type,assigned_room_type,booking_changes,deposit_type,agent,company,days_in_waiting_list,customer_type,adr,required_car_parking_spaces,total_of_special_requests,reservation_status,reservation_status_date) %>%
  filter_all(any_vars(is.na(.) | . == "NULL"))
]
``
![imagen11](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/ae6f4125-75f1-4f20-aa70-12b425980530)

Con estos datos se procederá a elegir la información pertinente antes de ver que tipo de eliminación se debería realizar a los valores NA o NULL.


#### Explicación de las técnicas utilizadas para eliminar o completar los datos faltantes:

En cuanto a la selección de los datos, se nos plantea la tarea de responder un conjunto de preguntas para hacer un análisis exploratorio de los datos. Estas respuestas denotan la necesidad de que ciertas columnas estén pre procesadas de manera correcta y de igual manera sean pertinentes para este caso.
Es evidente que debemos reducir la cantidad de características (columnas) disponibles. Esto es debido a que algunas variables no contribuyen de manera significativa al análisis de los datos que estamos buscando obtener independientemente de si tienen valores NA o no.

Las columnas importantes para responder a las preguntas planteadas :


-`hotel`: Permite distinguir entre "Resort Hotel" y "City Hotel" para analizar el tipo de hotel y las preferencias de los clientes.

 -`is_canceled`: Necesaria para identificar las cancelaciones de reservas.

 -`arrival_date_year`, `arrival_date_month`, `arrival_date_day_of_month`: Estas columnas son esenciales para analizar la demanda a lo largo del tiempo y para identificar las temporadas de reservas.


-`adults`, `children` y `babies`: Permiten determinar cuántas reservas incluyen niños y/o bebés.

 -`required_car_parking_spaces`: Es relevante para evaluar la importancia de los espacios de estacionamiento.
-`reservation_status_date`: Nos permitirá evaluar las fechas en las cuales se realizaron las reservaciones.




Con eso dicho ahora nuestra tabla quedaría de la siguiente manera lo cual es mucho más factible de manejar y modificar.


`` [
missing_data_rows <- hotel_data %>%
  select(hotel, is_canceled, arrival_date_year, arrival_date_month, arrival_date_week_number, arrival_date_day_of_month, adults, children, babies, required_car_parking_spaces) %>%
  filter_all(any_vars(is.na(.) | . == "NULL"))
]
``

![imagen12](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/6e50ab85-f6f9-4fed-8fb9-1493e5c7aa38)


Este gráfico como se mencionó anteriormente nos mostrará las distintas columnas que contengan alumnos un valor NA o NULL, sin embargo debido a la eliminación de las columnas que contienen valores NULL, solo nos quedaron estas 3 filas en children las cuales cuentan con valores NA.

##### Análisis de las variables:

Children:


Lo primero que se pensaría en hacer sería utilizar eliminar las variables NA con na.omit(), sin embargo esto sería un error ya que estaríamos perdiendo información muy pertinente para responder otras preguntas, puesto que eliminamos la fila.

Ahora, si realizamos una imputación basada en la lógica, podemos llegar a la conclusión de que el valor faltante NA en la columna de bebés significa que no hay niños o bebes en ese reserva. Por lo que en este caso esos datos los podemos reemplazar por 0.

![imagen13](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/b332a56a-c1fd-443a-a0ac-15baf712aec6)

Después de ellos podemos crear una nueva variable la cual nos permite saber cuántas reservas incluyen niños o bebes.

![imagen14](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/42b7742c-f563-4f78-88f7-7483bb11abb8)

![imagen15](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/16a81a3c-83fe-457d-bee3-767316ba6641)

Arrival_date:

Debido a que en nuestro caso nos interesa saber si el valor es pequeño, mediano o grande con respecto a las temporadas de reservas, haremos uso de la categorización de datos numéricos.
En este caso se decidió utilizar las estaciones para clasificar la temporadas de la siguiente manera:


Baja temporada: Las estaciones con menor cantidad de reservaciones.
Media temporada: Las estaciones con una cantidad moderada de reservaciones.
Alta temporada: Las estaciones con la mayor cantidad de reservaciones.

Para realizar esto primero debemos agrupar los meses por estaciones para poder trabajar con esos datos así mismo siendo separados por años para un análisis más concreto de la siguiente manera:
Invierno(Diciembre, Enero, Febrero)
Primavera(Marzo, Abril, Mayo)
Verano(Junio, Julio, Agosto)
Otoño(Setiembre, Octubre, Noviembre)
Codigo en cuestion:

``#Convertir los nombres de los meses en minúscula en missing_data_rows
missing_data_rows <- missing_data_rows %>%
  mutate(arrival_date_month = tolower(arrival_date_month))
``
``#Asignar estaciones por cada mes en missing_data_rows
missing_data_rows <- missing_data_rows %>%
  left_join(meses_estaciones, by = c("arrival_date_month" = "mes"))
``

``# Calcular el número de reservas por estación y año en missing_data_rows
missing_data_rows_seasons <- missing_data_rows %>%
  group_by(estacion, arrival_date_year) %>%
  summarise(total_bookings = n())
``

``# Crear un dataframe con todas las combinaciones de estaciones y años
all_combinations <- expand.grid(estacion = estaciones, arrival_date_year = unique(missing_data_rows$arrival_date_year))
``

``# Combinar con los datos reales y rellenar valores faltantes con ceros
missing_data_rows_seasons <- all_combinations %>%
  left_join(missing_data_rows_seasons, by = c("estacion", "arrival_date_year")) %>%
  mutate(total_bookings = replace_na(total_bookings, 0))
``

``# Calcular estadísticas resumen (media) para cada estación
summary_stats <- missing_data_rows_seasons %>%
  group_by(estacion) %>%  summarise(avg_total_bookings = mean(total_bookings))
``




  ![imagen16](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/6a11e091-77fd-4504-9433-59e0dc56ca81)

  Asociación de Meses a Estaciones:
Se creó un dataframe llamado `meses_estaciones` en el cual se relacionaron los nombres de los meses con sus respectivas estaciones. Esto permitió asignar una estación a cada mes del año.


![imagen17](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/4f260aee-1a8a-42cd-904a-fbf53ab24ba7)

Se convirtieron los nombres de los meses en minúscula en el conjunto de datos principal (`missing_data_rows`) para asegurar la coherencia en las asignaciones de estaciones.

Asignación de Estaciones a los Registros
Se asignaron estaciones a cada registro en el conjunto de datos principal mediante una operación de unión (join) con el dataframe `meses_estaciones`. Esto se logró utilizando los nombres de los meses como clave de unión.


![imagen18](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/25af898b-3bc3-41be-b297-52ef8a1895da)

Cálculo del Número de Reservas por Estación y Año
Los datos en `missing_data_rows` se agruparon por estación y año utilizando la función `group_by`. Luego, se calculó el número total de reservas (denominado `total_bookings`) en cada grupo mediante `summarise`. Los resultados se almacenaron en un nuevo dataframe llamado `missing_data_rows_seasons`.

Después generó un dataframe denominado `all_combinations` que contenía todas las combinaciones posibles de estaciones y años. Esto se logró tomando como base los valores únicos de años presentes en `missing_data_rows`. 

Finalmente se combinaron los datos de `all_combinations` con `missing_data_rows_seasons` mediante un "left_join," asegurando así que todas las combinaciones estuvieran presentes. Además, se rellenaron los valores faltantes de `total_bookings` con ceros.
![imagen19](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/b2083744-3de4-443c-9132-cdf28de0fcff)

Finalmente, se calculó la estadística resumen, que consistió en determinar el promedio (media) de `total_bookings` para cada estación en el dataframe `missing_data_rows_seasons`. Los resultados se recopilaron en un nuevo dataframe llamado `summary_stats`.
Este análisis proporciona una visión detallada de cómo se distribuyen las reservas de hotel a lo largo de las estaciones y los años, lo que puede ser valioso para la toma de decisiones y la planificación estratégica en la industria hotelera.
![imagen20](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/8b4a1291-b840-4f0d-99ba-cce5c660e74d)
Determinación de Umbrales:

Para la determinación de los umbrales en cuestión se decidió el uso de percentiles para definir la cantidad total de reservaciones de la siguiente manera.

`` # Definir umbrales para reservas bajas, medias y altas 
umbral_bajo <- quantile(summary_stats$avg_total_bookings, 0.33)
umbral_alto <- quantile(summary_stats$avg_total_bookings, 0.67)
``

`` # Clasificar las estaciones en categorías en summary_stats
summary_stats <- summary_stats %>%
  mutate(categoria = case_when(
    avg_total_bookings < umbral_bajo ~ "Bajas",
    avg_total_bookings >= umbral_bajo & avg_total_bookings < umbral_alto ~ "Medias",
    avg_total_bookings >= umbral_alto ~ "Altas"
  ))
``
Este código nos permitirá segmentar las estaciones en tres categorías distintas ("Bajas," "Medias" y "Altas") en función de su desempeño en términos de promedio de reservas de hotel, así mismo se tomó . Esto facilitará la interpretación y el análisis de cómo se distribuyen las estaciones en diferentes niveles de demanda, lo que puede ser útil para la toma de decisiones y la planificación en la industria hotelera.

El código que has proporcionado te permitirá realizar una clasificación de las estaciones en categorías en función del promedio de reservas de hotel por estación. A continuación, te explico en detalle lo que hace cada parte del código:

Definición de Umbrales:
 Umbral_bajo: se calcula como el percentil 33 (1/3) del promedio de reservas (`avg_total_bookings`) en `summary_stats`. Este valor representa el límite inferior para categorizar las estaciones como "Bajas".

  `Umbral_alto : se calcula como el percentil 67 (2/3) del promedio de reservas en `Summary_stats`. Este valor representa el límite superior para categorizar las estaciones como “Altas”


is_canceled:

En nuestro caso requerimos saber si la reserva ha sido cancelada o si ha sido reservada con éxito, al principio los valores contenidos se encontraban como tipo numérico, lo cual no es precisamente exacto cuando tratamos de hacer uso de valores de valores Booleanos como verdadero o falso. Por lo que se decidió transformarlo en un factor para poder analizarlo de una manera más adecuada.
![imagen21](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/bca99875-53ee-4171-bc0f-ff408aeca599)

Requiered_car_parking_spaces y Reservation_status_date:

Para los espacios de estacionamiento requerimos saber cuántas familias han pedido que la reserva venga con al menos un estacionamiento y las que no desean el estacionamiento, por lo que no es conveniente hacer uso de algún tipo de cambio para esta variable para responder la pregunta.
Lo mismo pasa con el estado de la fecha de estado de reserva, puesto que nos conviene que esté de esa manera, ya que nos conviene para responder la pregunta en el análisis respectivo.
		





Identificacion de Datos Atipicos:



Primero que todo debido a la cantidad reducida de datos con los cuales estamos trabajando y siendo esto en su mayoría de valores que no son muy cambiantes, así mismo contando con una columna con valores propiamente numéricos, es muy probable que no haya outliers en los actos con los cuales estamos trabajando.

Con esto en mente se decidió  la limpieza de  la variable total booking haciendo un box plot para identificar si hay algún outliers, a su vez verificando que los total_bookings sean atípicos. 

![imagen22](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/36b64d69-5178-4ead-8800-0fad6c61f529)

![imagen23](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/0924dc5f-cbcc-4f38-8487-b3310349c826)

Como se puede observar no se obtuvieron datos atípicos al momento de realizar el análisis de los datos por lo que se puede analizar estos valores sin esperar un problema de sesgo.




### VISUALIZAR DATOS 

- Los alumnos decidirán qué variables del dataset seleccionarán del conjunto de datos para demostrar las correlaciones existentes, y visualizarlas e inferir sus conclusiones.

Para el presente proyecto utilizaremos las siguientes variables:
``
"hotel"                       	        "is_canceled"                 "arrival_date_year"                   "babies"
"arrival_date_month"                  "arrival_date_week_number"    "arrival_date_day_of_month"           "estacion"  
"adults"                              "children"                                        
"required_car_parking_spaces"         "has_children_or_babies"                       
"Reservation_status_date"     
``
#### 3. CONCLUSIONES PRELIMINARES 

En conclusión los beneficiarios de este análisis llegan a ser diversas entidades, logrando abarcar desde el equipo de gestión del hotel hasta especialistas en marketing y planificadores de recursos. El equipo de gestión del hotel puede utilizar los resultados para tomar decisiones informadas sobre la ocupación y mejorar la satisfacción del cliente. Los especialistas en marketing pueden ajustar sus estrategias para atraer a diferentes segmentos de mercado, mientras que los planificadores de recursos podrían optimizar la gestión de habitaciones y servicios en función de la demanda histórica y las preferencias de los huéspedes. En resumen, estos datos ofrecen una base sólida para la toma de decisiones en la industria hotelera y áreas relacionadas.

- a) Respecto a la primera pregunta se logra concluir que las personas prefieren realizar una reserva en el hotel City Hotel, este análisis nos sirve a futuro para poder saber qué hotel es el más valorado por los visitantes.
- b) En la segunda pregunta se puede observar que durante el primer y segundo año, hubo un incremento considerado de las reservas; pero, tras el segundo y tercer año, hubo un declive considerado, por lo que se puede concluir que las cantidades de reservas a futuro llegarán a disminuir, pero aún habrá reservas considerables.
- c) Se llega a concluir en la tercera pregunta que los meses posteriores al invierno generan una mayor demanda de reservas.
- d) Lo concluido en la cuarta pregunta, es que durante los meses que contempla el invierno las reservas decaen considerablemente para ambos hoteles, por lo que se recomienda que en las temporadas altas el costo de reserva incremente, gracias a la alta demanda.
- e) En la quinta pregunta se logra evidenciar que las personas que realizan reservas en los distintos hoteles no acuden a este con algún niño. En conclusión es mejor destinar los recursos de los hoteles a un mejor entretenimiento para el público mayor.
- f) De la sexta pregunta se logra concluir que las personas no requieren un espacio de estacionamiento, por lo que se recomienda no invertir en una gran cantidad de estas zonas.
- g) Se llega a concluir de la última pregunta que en los meses de enero se genera una mayor cantidad de cancelaciones de hotel, mostrando un pico de 2616 cancelaciones en el año de 2017.

#### 4 Bibliografia

Antonio,N.,deAlmeida,A.,&Nunes,L.(2019).Hotelbookingdemanddatasets.Datainbrief,22,41-49.Recuperado de:https://doi.org/10.1016/j.dib.2018.11.126  (Consulta:03 de septiembre del 2023)
