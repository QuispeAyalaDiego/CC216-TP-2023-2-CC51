
#  TRABAJO PARCIAL
##Análisis Exploratorio de un conjunto de Datos
#####  Carrera: Ciencias de la Computación


|  AUTORES                 |                      
|----------------|-------------------------------
|Quispe Ayala Diego Juan Pablo|
|Roque Ponce, Christian Alonso          |
|Retuerto Diaz, Pedro Alejandro      |
|Luis Lázaro, Daniel Orlando


------------


------------
#### 1. CASO DE ANÁLISIS 
##### 1.1. Explicación sobre el origen de los datos:

El conjunto de datos, titulado "Hotel booking demand datasets," se describe en un artículo de datos y es el resultado de la colaboración de Nuno Antonio, Ana de Almeida y Luis Nunes de diversas instituciones en Portugal, incluyendo el Instituto Universitário de Lisboa (ISCTE-IUL) y el Instituto de Telecomunicações. A continuación, se proporciona una breve descripción del conjunto de datos:

- Origen y Autoría: Los datos se originan en la industria hotelera y fueron recopilados de dos hoteles en Portugal. Uno de los hoteles es un hotel resort (H1), mientras que el otro es un hotel de ciudad (H2). Los datos fueron proporcionados por Nuno Antonio, Ana de Almeida y Luis Nunes, quienes representan varias instituciones en Portugal.

- Fecha de Recepción y Aceptación: El artículo describe que los datos fueron recibidos el 5 de octubre de 2018 y aceptados para su uso el 26 de noviembre de 2018. Los datos están disponibles en línea desde el 29 de noviembre de 2018.

- Resumen General: El conjunto de datos consta de dos partes, una correspondiente al hotel resort (H1) y la otra al hotel de ciudad (H2). Ambos conjuntos de datos tienen una estructura similar y comprenden un total de 40,060 observaciones para H1 y 79,330 observaciones para H2. Cada observación representa una reserva de hotel. Los datos cubren el período desde el 1 de julio de 2015 hasta el 31 de agosto de 2017 e incluyen tanto reservas que llegaron efectivamente como reservas que fueron canceladas. Se eliminaron todos los elementos de datos relacionados con la identificación de hoteles o clientes para preservar la privacidad.

- Utilidad de los Datos: El artículo señala que estos conjuntos de datos tienen un valor significativo para la investigación y la educación en áreas como la gestión de ingresos, el aprendizaje automático y la minería de datos en la industria hotelera y otros campos relacionados. Debido a la escasez de datos empresariales reales disponibles con fines científicos y educativos, estos conjuntos de datos pueden desempeñar un papel importante en la investigación y la educación.

- Área Temática y Accesibilidad de los Datos: Los datos están relacionados con la gestión de la hospitalidad y específicamente en la gestión de ingresos. Se obtuvieron mediante extracción de sistemas de gestión de propiedades (PMS) de hoteles mediante consultas SQL. Los datos están en formato mixto, incluyendo datos crudos y preprocesados. El tiempo para cada observación se definió como el día previo a la llegada de cada reserva.

- Ubicación de los Hoteles: Ambos hoteles están ubicados en Portugal, con H1 en la región de Algarve y H2 en la ciudad de Lisboa.

- Accesibilidad de los Datos: Los datos se proporcionan junto con el artículo, lo que significa que están disponibles para su uso en investigaciones y análisis.

##### 1.2. Casos de uso aplicables:

El análisis de estos datos es fundamental para varios propósitos, entre ellos:

** a. Evaluación de la Demanda Hotelera:** Estos datos son esenciales para comprender la cantidad de reservas realizadas en cualquiera de los dos hoteles en consideración. Esto proporciona una base sólida para determinar cuál de los dos hoteles es más solicitado por los clientes, lo que es vital para la gestión y la estrategia de marketing.

**b. Beneficios para Inversores y Clientes: **Los beneficiarios de este análisis incluyen tanto inversores como clientes. Los clientes pueden utilizar esta información para evaluar la disponibilidad de habitaciones y planificar futuras reservas en función de la demanda histórica. Por otro lado, los inversores pueden aprovechar estos datos para tomar decisiones informadas sobre en qué hotel invertir, basándose en la concurrencia de huéspedes. En resumen, estos datos son valiosos para la toma de decisiones tanto a nivel de clientes como de inversores en la industria hotelera.
**c. Optimización de Recursos:** Además de los inversores y clientes, los equipos de gestión de los hoteles pueden beneficiarse enormemente de este análisis. Les permite optimizar la asignación de recursos, como personal y servicios, en función de las tendencias de reserva históricas. Esto puede conducir a una gestión más eficiente y a una mejor experiencia del cliente.

**d. Estrategias de Precios:** Los datos de demanda hotelera son esenciales para desarrollar estrategias de precios efectivas. Los equipos de precios pueden ajustar las tarifas en función de la temporada alta o baja, la ocupación histórica y otros factores identificados en el análisis. Esto maximiza los ingresos y la competitividad en el mercado.

**e. Evaluación de Éxito de Campañas: **Los especialistas en marketing pueden utilizar estos datos para evaluar el éxito de sus campañas promocionales y estrategias de adquisición de clientes. Pueden identificar cuándo las promociones han atraído más reservas y cuándo se necesitan ajustes en las estrategias publicitarias.

**f. Planificación Estratégica a Largo Plazo: **Los datos históricos de demanda también son valiosos para la planificación estratégica a largo plazo. Los equipos directivos pueden utilizar estos datos para tomar decisiones sobre la expansión de la capacidad hotelera, la inversión en instalaciones adicionales o la introducción de nuevos servicios.

**g. Investigación Académica: **Además de su utilidad práctica, estos datos también pueden ser valiosos para la investigación académica en áreas como la gestión hotelera, la ciencia de datos y la toma de decisiones. Los académicos pueden utilizar estos conjuntos de datos para desarrollar y probar modelos y teorías en el campo de la hospitalidad.
