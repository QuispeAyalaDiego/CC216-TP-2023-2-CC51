
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
![imagen5](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/42ee296f-a05d-4bac-a155-6eacd60b4945)
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



`` # Convertir los nombres de los meses en minúscula en missing_data_rows
missing_data_rows <- missing_data_rows %>%
  mutate(arrival_date_month = tolower(arrival_date_month))

# Asignar estaciones por cada mes en missing_data_rows
missing_data_rows <- missing_data_rows %>%
  left_join(meses_estaciones, by = c("arrival_date_month" = "mes"))

# Calcular el número de reservas por estación y año en missing_data_rows
missing_data_rows_seasons <- missing_data_rows %>%
  group_by(estacion, arrival_date_year) %>%
  summarise(total_bookings = n())

# Crear un dataframe con todas las combinaciones de estaciones y años
all_combinations <- expand.grid(estacion = estaciones, arrival_date_year = unique(missing_data_rows$arrival_date_year))

# Combinar con los datos reales y rellenar valores faltantes con ceros
missing_data_rows_seasons <- all_combinations %>%
  left_join(missing_data_rows_seasons, by = c("estacion", "arrival_date_year")) %>%
  mutate(total_bookings = replace_na(total_bookings, 0))

# Calcular estadísticas resumen (media) para cada estación
summary_stats <- missing_data_rows_seasons %>%
  group_by(estacion) %>%
  summarise(avg_total_bookings = mean(total_bookings))``

  ![imagen16](https://github.com/QuispeAyalaDiego/CC216-TP-2023-2-CC51/assets/103915075/6a11e091-77fd-4504-9433-59e0dc56ca81)



