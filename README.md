Proyecto n°4 Certificacion Data Science "Acamica"

Proyecto – Covid19.

Proyecto de ciencias de datos, centrado en el estudio de la pandemia, considerando diferentes curvas, indicadores y eficacia de políticas públicas de salud implementadas para luego modelar y ver si es posible predecir qué países utilizaron las distintas políticas, la cual una vez seleccionada será un problema binario.
Todo el desarrollo de proyecto esta basado en las consignas brindadas por la academia que nos capacita.

Desarrollo.
Los datos con los que se  trabajo los adquirimos del hub de” Our World in Data”.
https://github.com/owid/covid-19-data/tree/master/public/data
Aquí el desafío fue manejar una gran cantidad de instancias y features las cuales filtramos lo suficiente para quedarnos con las que necesitamos; el manejo de los faltantes no fue un desafío ya que los países que seleccionamos para el proyecto tenían datos suficientes, pero en si en general se veían muchísimos faltantes, cuestión que afectaría a un estudio mas global, esta faltante de datos puede tener muchos orígenes como por ejemplo la falta de voluntad de algún gobierno a brindar sus datos o a no brindarlos correctamente o quizás a que ciertos países no cuenta con instituciones seria que posean  sistemas de recopilación, guardado y análisis de datos y por últimos podría haber diferencias en la recopilación y tratamiento de los mismo.

Primera parte:

El primer parte del trabajo consiste en estudiar cómo se empieza a propagar la pandemia, luego analizaremos las medidas tomadas y su efectividad.
Al inicio de una pandemia, se estima que los contagios siguen una ley exponencial, esa es la fase de "crecimiento exponencial", luego hay un decaimiento dado por la inmunidad. 
Empezamos analizando la curva de contagios de 10 países del norte, en donde más temprano empezó la pandemia y con estos mismos 10 países se hizo todo el desarrollo del proyecto.
Los países son: 

El objetivo más allá de saber el K de los países y ver si la curva real de contagios se acomoda a una curva simulada tomando el K obtenido, es ver si el K de los 10 países seleccionados es representativo de la realidad mundial para el periodo de análisis.

Segunda parte:

Para esta segunda parte lo que hicimos fue seleccionar una Política Publica Sanitaria, la cual analizamos en base a los países seleccionados en el principio.
La política que analizamos fue la “cuarentena” para esto decidimos analizarlo de modo de llevarlo a un problema Binario, países que hicieron “Cuarentena Nacional Obligatoria” y países que “No hicieron Cuarentena o hicieron Cuarentena Regional”.

Los datos fueron obtenidos del siguiente link  https://es.wikipedia.org/wiki/Confinamiento_por_la_pandemia_de_COVID-19#Cuarentena_por_pa%C3%ADses

De aquí también obtuvimos las fechas de inicio de las diferentes cuarentenas. El rango fue determinado por la fecha de inicio de las cuarentenas y la fecha anterior al primer dato de vacunación, esto lo hicimos para aislar la política elegida. Creemos que hasta el momento hubo dos políticas principales en la lucha contra el Covid19 y estas son las cuarentenas y la vacunación, por eso la selección del rango de fechas hasta vacunación, para que no se interpongan las políticas.
Evaluamos la eficacia o no de las diferentes cuarentenas en virtud de 3 indicadores: 
•	“new_cases_per_100Thousand”
•	“reproduction_rate”
•	“new_deaths_per_100Thousand”

A su vez cada uno de estos indicadores fueron evaluados por determinados rangos los cuales fueron definidos por investigación de diferentes fuentes y criterio personal. 
En el caso de “new_cases_per_100Thousand” la fuente para determinar el rango de nuevos contagios a la luz de evaluar su eficacia fue el siguiente. https://www.cdc.gov/coronavirus/2019-ncov/travelers/how-level-is-determined.html

Menos de 50 casos cada 100 mil habitantes fue efectiva, mayor a este número empeoro la situación.
En el caso de “reproduction_rate” la fuente para determinar el rango fue: https://www.bbc.com/mundo/noticias-51469198.
En este articulo periodístico nos indica claramente que el reproduction rate si es menor a 1 es que se está logrando frenar el virus, si es mayor a uno este sigue reproduciéndose. El valor inicia de la pandemia fue de 2,5. Por lo que si la ratio es menor a 1 mejora la situación y si es mayor empeora.
Y por últimos. En el caso de “new_deaths_per_100Thousand” la fuente para determinar el rango de eficacia fue: https://www.bbc.com/mundo/noticias-51614537.
En este artículo periodístico nos indica que la tasa de mortalidad general que es de 2,3%. Aplicamos esta tasa al rango de nuevos casos para obtener de rango de muertes por cada 100 mil habitantes, y evaluar si mejoro o empeoro la pandemia según el estilo de cuarentena.

Conclusiones de esta Segunda parte:

En relación a los nuevos casos y las nuevas muertes tanto la cuarentena nacional obligatoria como la cuarentena regional o no cuarentena, fueron eficaces ya que lograron disminuir los casos y las muertes significativamente; caso contrario el del indicador Reproduction Rate que mostro que los dos tipos de cuarentena no fueron capaces de frenar los contagios en aproximadamente un 65% aun 70%.
Esto es lógico ya que si bien bajaron los casos y las muertes la pandemia siguió esparciéndose, además creemos que el indicador Reproduction Rate es un indicador más fuerte y más veraz y que puede ser aplicado a cualquier política y país por que indica si se esta frenando al virus o no, cosa que no pasa con nuevos casos por cuestiones de errores de carga, testeo falsos positivos o verdaderos negativos o casos asintomáticos que siguen contagiando.
Tampoco pasa con las nuevas muertes por cabe la posibilidad de errores en los registros de las causales de las nuevas muertes.

Tercera parte:

Aquí desarrollamos a través de regresiones logísticas de la librería Scikit-learn modelos que nos permitan predecir qué tipo de cuarentena hicieron los distintos países.

Conclusión Final:

Concluimos que el mejor modelo desarrollado fue la regresión logística que se basaba en la variable predictora "Reproduction Rate" este fue el que mayor accuracy arrojo y luego de optimizar sus hiperparametros llego a un 78% de accuracy.
También concluimos que el indicador más relevante y certero es el "Reproduction Rate" ya que es el único que nos dice con certeza si la expansión del virus se está frenando o no porque los nuevos casos tiene muchos baches en su determinación como por ejemplo la falta de testeos o los pocos testeos que hace cada país, asintomáticos, falsos positivo o verdaderos negativos; en relación a las nuevas muertes es posible errores de carga de datos y se podrían cargar muerte por covid19 y en realidad son muertes por otras causas, además de que no todos los contagiados son hospitalizado y no todos los hospitalizados mueren.
En relación a los modelos, concluimos que es posible hacer un clasificador a partir de una regresión logística, pero, aunque como pudimos ver en las pruebas con los tres países nunca visto por el modelo, no logra clasificar correctamente, creemos que, al agregar más países de distintas regiones del mundo, respetando la política seleccionada y agregando más variables predictoras se podría hacer un clasificador que nos diga que política implemento cada país con una altísima precisión.
Pero si lo que no podríamos hacer en predecir el futuro comportamiento del virus ni la efectividad anticipada de nuevas políticas públicas.


