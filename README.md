
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
b. ¿Está aumentando la demanda con el tiempo? 
```
# Crear un gráfico de barras apiladas
ggplot(missing_data_rows_seasons, aes(x = factor(arrival_date_year), y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity") +
    labs(x = "Año", y = "Número de Reservas", title = "Número de Reservas por Estación y Año") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "orange", "Otoño" = "red")) +
    theme_minimal()

```

c. ¿Cuándo se producen las temporadas de reservas: alta, media y baja? 

```
 # Crear un gráfico de barras facetado por estación
ggplot(missing_data_rows_seasons, aes(x = factor(arrival_date_year), y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity", position = "stack") +
    labs(x = "Año", y = "Número de Reservas", title = "Resumen de Reservas por Estación y Año") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "yellow", "Otoño" = "red")) +
    theme_minimal() +
    facet_wrap(~estacion, ncol = 4) # Facetado por estación


```
d. ¿Cuándo es menor la demanda de reservas? 
```
# Crear un gráfico de barras de la cantidad total de reservas por estación
ggplot(missing_data_rows_seasons, aes(x = estacion, y = total_bookings, fill = estacion)) +
    geom_bar(stat = "identity") +
    labs(x = "Estación", y = "Número de Reservas", title = "Resumen de Reservas por Estación") +
    scale_fill_manual(values = c("Invierno" = "blue", "Primavera" = "green", "Verano" = "yellow", "Otoño" = "red")) +
    theme_minimal()

```

e. ¿Cuántas reservas incluyen niños y/o bebes? 

```
pie(conteo_bebes, labels = c("No tiene niño o bebe", "Tiene niño o bebe"), col = c("chartreuse1", "darkturquoise")	


```

```
f. ¿Es importante contar con espacios de estacionamiento? 
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

------------
#### 2. Data base



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



#### PRE-PROCESAR DATOS 

- Identificar datos faltantes o NA:

Para identificar los datos faltantes, procedimos a realizar un proceso de filtrado en el conjunto de datos con el fin de detectar todas las observaciones que presentan valores nulos, representados como "NA" o "NULL" en sus respectivas características.


Adicionalmente, se observó que varias columnas presentan valores iguales a cero. En este sentido, se plantea la necesidad de considerar si es pertinente llevar a cabo una limpieza de datos en estas columnas o, en caso contrario, eliminarlas en caso de que no sean relevantes para las interrogantes planteadas en el análisis exploratorio de los datos.

A continuación, se presenta el fragmento de código y el gráfico correspondiente




```
[
missing_data_rows <- hotel_data %>%
select(hotel,is_canceled,lead_time,arrival_date_year,arrival_date_month,arrival_date_week_number,arrival_date_day_of_month,stays_in_weekend_nights,stays_in_week_nights,adults,children,babies,meal,country,market_segment,distribution_channel,is_repeated_guest,previous_cancellations,previous_bookings_not_canceled,reserved_room_type,assigned_room_type,booking_changes,deposit_type,agent,company,days_in_waiting_list,customer_type,adr,required_car_parking_spaces,total_of_special_requests,reservation_status,reservation_status_date) %>%
  filter_all(any_vars(is.na(.) | . == "NULL"))
]

```

Con estos datos se procederá a elegir la información pertinente antes de ver que tipo de eliminación se debería realizar a los valores NA o NULL.


### Explicación de las técnicas utilizadas para eliminar o completar los datos faltantes:

En cuanto a la selección de los datos, se nos plantea la tarea de responder un conjunto de preguntas para hacer un análisis exploratorio de los datos. Estas respuestas denotan la necesidad de que ciertas columnas estén pre procesadas de manera correcta y de igual manera sean pertinentes para este caso.
Es evidente que debemos reducir la cantidad de características (columnas) disponibles. Esto es debido a que algunas variables no contribuyen de manera significativa al análisis de los datos que estamos buscando obtener independientemente de si tienen valores NA o no.


Las columnas importantes para responder a las preguntas planteadas :


  -`hotel`: Permite distinguir entre "Resort Hotel" y "City Hotel" para analizar el tipo de hotel y las preferencias de los clientes.

   -`is_canceled`: Necesaria para identificar las cancelaciones de reservas.

 -`arrival_date_year`, `arrival_date_month`, `arrival_date_day_of_month`: Estas columnas son esenciales para analizar la demanda a lo largo del tiempo y para identificar las temporadas de reservas.


-`adults`, `children` y `babies`: Permiten determinar cuántas reservas incluyen niños y/o bebés.

 -`required_car_parking_spaces`: Es relevante para evaluar la importancia de los espacios de estacionamiento.




Con eso dicho ahora nuestra tabla quedaría de la siguiente manera lo cual es mucho más factible de manejar y modificar.


```

[
missing_data_rows <- hotel_data %>%
  select(hotel, is_canceled, arrival_date_year, arrival_date_month, arrival_date_week_number, arrival_date_day_of_month, adults, children, babies, required_car_parking_spaces) %>%
  filter_all(any_vars(is.na(.) | . == "NULL"))
]

```

------------

#### 3.CONCLUSIONES
En conclusión los beneficiarios de este análisis llegan a ser diversas entidades, logrando abarcar desde el equipo de gestión del hotel hasta especialistas en marketing y planificadores de recursos. El equipo de gestión del hotel puede utilizar los resultados para tomar decisiones informadas sobre la ocupación y mejorar la satisfacción del cliente. Los especialistas en marketing pueden ajustar sus estrategias para atraer a diferentes segmentos de mercado, mientras que los planificadores de recursos podrían optimizar la gestión de habitaciones y servicios en función de la demanda histórica y las preferencias de los huéspedes. En resumen, estos datos ofrecen una base sólida para la toma de decisiones en la industria hotelera y áreas relacionadas.

a) Respecto a la primera pregunta se logra concluir que las personas prefieren realizar una reserva en el hotel City Hotel, este análisis nos sirve a futuro para poder saber qué hotel es el más valorado por los visitantes.
b) En la segunda pregunta se puede observar que durante el primer y segundo año, hubo un incremento considerado de las reservas; pero, tras el segundo y tercer año, hubo un declive considerado, por lo que se puede concluir que las cantidades de reservas a futuro llegarán a disminuir, pero aún habrá reservas considerables.
c) Se llega a concluir en la tercera pregunta que los meses posteriores al invierno generan una mayor demanda de reservas.
d) Lo concluido en la cuarta pregunta, es que durante los meses que contempla el invierno las reservas decaen considerablemente para ambos hoteles, por lo que se recomienda que en las temporadas altas el costo de reserva incremente, gracias a la alta demanda.
e) En la quinta pregunta se logra evidenciar que las personas que realizan reservas en los distintos hoteles no acuden a este con algún niño. En conclusión es mejor destinar los recursos de los hoteles a un mejor entretenimiento para el público mayor.
f) De la sexta pregunta se logra concluir que las personas no requieren un espacio de estacionamiento, por lo que se recomienda no invertir en una gran cantidad de estas zonas.
g) Se llega a concluir de la última pregunta que en los meses de enero se genera una mayor cantidad de cancelaciones de hotel, mostrando un pico de 2616 cancelaciones en el año de 2017.

------------
#### 4.BIBLIOGRAFIA

Antonio,N.,deAlmeida,A.,&Nunes,L.(2019).Hotelbookingdemanddatasets.Datainbrief,22,41-49.Recuperado de:https://doi.org/10.1016/j.dib.2018.11.126  (Consulta:03 de septiembre del 2023)

Follow, S. (2021, julio 27). Filter data by multiple conditions in R using Dplyr. GeeksforGeeks. Recuperado de: Filter data by multiple conditions in R using Dplyr - GeeksforGeeks

Data visualization with ggplot2. (s/f). Datacarpentry.org. Recuperado el 24 de septiembre de 2023. Recuperado de: https://datacarpentry.org/R-ecology-lesson/04-visualization-ggplot2.html

Dplyr. (s/f). Rdocumentation.org. Recuperado el 24 de septiembre de 2023. Recuperado de:https://www.rdocumentation.org/packages/dplyr/versions/0.7.8

hotel_bookings.csv. (s/f). Google Docs. Recuperado el 24 de septiembre de 2023. Ruperador de: https://drive.google.com/file/d/1G0-AKU6Lx5i23a1o62wCPSwBQHg1wls1/view
