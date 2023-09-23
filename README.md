
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



------------

#### 3.CONCLUSIONES

------------
#### 4.BIBLIOGRAFIA

Antonio,N.,deAlmeida,A.,&Nunes,L. (2019).Hotelbookingdemanddatasets.Datainbrief,22,41-49.Recuperadode:
https://doi.org/10.1016/j.dib.2018.11.126 [Consulta:03de mayodel2023]
