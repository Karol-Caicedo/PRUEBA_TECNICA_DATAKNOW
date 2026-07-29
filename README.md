# Caso de Negocio: Gestión de Costos Operativos en un Proyecto de Construcción

Una empresa del sector constructor se encuentra en la fase de planificación de un 
proyecto con una ventana de ejecución definida. Durante este período, la empresa deberá
gestionar el suministro continuo de dos tipos de equipos críticos para las operaciones en
campo. Históricamente, el costo de adquisición de estos equipos ha mostrado
comportamientos variables que la empresa no ha logrado anticipar con precisión, lo que
ha generado desviaciones presupuestales recurrentes.

La gerencia sospecha que los precios de los equipos guardan alguna relación con la
dinámica de ciertos insumos del mercado de materias primas, pero no cuenta con un
modelo formal que respalde esta hipótesis ni con claridad sobre cuáles insumos son
realmente determinantes para cada tipo de equipo. Se ha contratado a un consultor para
que, a partir del análisis de la información histórica disponible, proponga una metodología
que permita estimar el costo de los equipos de forma sistemática y sostenible en el tiempo,
y que adicionalmente sirva como insumo para la planeación financiera del proyecto en los
meses venideros.

# Beneficios esperados:
- Contar con un mecanismo reproducible para anticipar costos de equipos antes del
inicio de cada fase del proyecto.

- Reducir las desviaciones presupuestales asociadas a la volatilidad en los precios de
insumos.

- Establecer una base analítica para comprender el comportamiento histórico de los costos de adquisición de los equipos.

# Objetivos

- Proyectar los costos de los equipos mediante modelos de pronóstico que estimen los precios futuros a partir de la relación entre las materias primas y los equipos, considerando la incertidumbre de las predicciones.
- Presentar los resultados mediante un agente de IA que permita interactuar con el análisis, responder preguntas del usuario e integrar información externa del mercado para enriquecer las proyecciones, explicando además las diferencias entre un modelo de IA y un agente de IA.
- Diseñar una arquitectura en la nube (AWS, Azure o GCP) que soporte el flujo completo de la solución, desde la ingesta y procesamiento de datos hasta la ejecución del modelo y la visualización de los resultados.

# Supuestos

Un supuesto de proyecto se utiliza en la planificación de proyectos para definir un factor que se considera verdadero, real o seguro, incluso si no existe evidencia que lo demuestre. Es necesario asumir ciertas verdades para poder avanzar con la planificación del proyecto.

**Supuestos del análisis de este caso de negocio:**

- Los precios de los equipos guardan alguna relación con la dinámica de ciertos insumos del mercado de materias primas. Si el precio de los insumos aumenta es posible que el de los equipos también y si el precio disminuye ocurre lo mismo  para el precio de los equipos.
- Se asume que los datos históricos representan el comportamiento del precio de la adquisicion de los equipos con respecto a los insumos.
- El cambio de precio de los insumos a lo largo del tiempo puede estar determinado por la inflaccion, tipo de cambio, costos de produccion, etc.
- La relación de los datos históricos continuará en el horizonte de predicción de 1 año.
- Se asume que los costos de adquisición de los equipos varían en el tiempo y que es posible modelar o predecir dichas variaciones para mejorar la planeación financiera de la empresa.

# Formas para resolver el caso

Los métodos cuantitativos facilitan el análisis de datos numéricos y estadísticos. Para interpretar el comportamiento de datos históricos de un negocio para hacer pronósticos y proyecciones al futuro, los métodos  de pronosticos con series de tiempo más utilizados en la práctica son (Regresiones simples, promedios móviles simples y ponderados, método de descomposición estacional, SARIMA y suavización exponencial).

**Métodos de pronósticos cuantitativos:**

1. **Pronóstico ingenuo:** Utiliza el valor del período anterior como predicción para el siguiente. Es el método más simple y suele emplearse como referencia para comparar el desempeño de modelos de pronóstico más avanzados. Modelos que utiliza ( **Naïve Forecast**).
2. **Método de promedio móvil:** Calcula el promedio de varios períodos anteriores para estimar el valor futuro. Funciona bien cuando los datos son estables, aunque responde lentamente a cambios en la tendencia o la estacionalidad. Modelos que utiliza (**Promedio Móvil Simple**  y **Promedio Móvil Ponderado (WMA).**
3. **Método de suavizado exponencial:** Asigna mayor peso a los datos más recientes, permitiendo que el pronóstico se adapte más rápidamente a cambios en el comportamiento de la serie. Es adecuado para pronósticos de corto plazo y entornos dinámicos. Modelos que utiliza (**Suavizado Exponencial Simple, doble suavizado)** y **Holt-Winters (triple suavizado).**
4. **Proyección de tendencias:** Analiza el comportamiento histórico para identificar tendencias y proyectarlas hacia el futuro. Es útil cuando existen suficientes datos históricos y se espera que la tendencia continúe en el tiempo. Modelos que utiliza (**Regresión Lineal**, **Regresión Polinómica**, **Modelo de Tendencia Exponencial**, **Modelo Logarítmico).**

- La solución a implementar es el método de proyeccion de tendencias ya que se ajusta a lo que busca  la empresa que es: proyectar el comportamiento esperado de los costos de cada equipo para los meses requeridos por el proyecto hacia el futuro. Utilizando el modelo forecasting multivariable Prophet, este  modelo permtite predecir un valor futuro con base en el tiempo y  es un algoritmo especializado exclusivamente en series temporales con estacionalidad, perfecto para capturar los ciclos diarios y semanales de los precios.  Este modelo genera Prophet  intervalos de confianza (las bandas de límite superior e inferior).  Donde se puede decir que "el costo oscilará entre este máximo y este mínimo con un 90% de seguridad".

- Para determinar que variables constituyen ruido y cual no, se utilizó el modelo Random Forest Regressor de ya que parte del analisis consitía en no solo saber si  "sube o baja", sino cuánto influye cada insumo en el valor real del costo. Es un modelo adecuado para series en tiempo. Su objetivo principal Random Forest no es pronosticar el futuro, sino usar toda la historia para auditar los datos, encontrar relaciones no lineales y extraer matemáticamente la importancia de cada materia prima para poder  que variables son las determinantes en el precio de los equipos.

Para la proyeccion de los meses se utilizó El forecasting basado en IA que es el uso de la inteligencia artificial para producir pronósticos precisos mediante el aprendizaje de patrones a partir de datos históricos y la actualización continua de los modelos de forecasting a medida que llegan nuevos datos.

# Proyección de costos y horizonte de predicción
Teniendo en cuenta que la empresa quiere hacer el pronostico para los meses venideros y él último histórico es de agosto (2023-08-31), tomé la decisión de realizar el pronóstico con un horizonte de 4 meses 
(desde septiembre hasta diciembre 2023) ya que se ha realizado durante los 13 años (2010-2023) registros del costo de los equipos desde enero hasta diciembre.

# Resultados del análisis de los datos y los modelos

**Preguntas realizadas al modelo de IA**
1. ¿Cuál fue el pronostico para el dia 3 de septiembre?, ¿y para el dia 2? -> Equipo2
2. ¿Cuál fue el pronostico para el mes de septiembre? -> equipo2
3. ¿Cuál fue el pronostico para el dia 3 de septiembre?, ¿y para el dia 2? -> Equipo1
4. ¿Cuál fue el pronostico para el mes de septiembre? -> equipo1
5. ¿Cual es la importancia de usar modelos de machine learning para le gestion de costos operativos?


**Respuestas**

1. - El pronóstico para el día 3 de septiembre fue de $1,076.63 con un rango de incertidumbre del 90% entre $1,049.83 y $1,100.85.
   - El pronóstico para el día 2 de septiembre fue de $1,076.19 con un rango de incertidumbre del 90% entre $1,050.11 y $1,099.30.

Esto quiere decir que el precio de aquisicion de los equipos para esas fechas indicadas oscila entre (90% entre $1,049.83 y $1,100.85) y (90% entre $1,050.11 y $1,099.30.)

2. El pronóstico para el mes de septiembre incluyó los siguientes datos principales:

- Fecha con costo más alto: 30 de septiembre con un costo de $1,078.71
- Costo máximo del mes: $1,078.71
- Costo mínimo: $1,065.13
- Promedio mensual: $1,070.06
- Rango de incertidumbre promedio: $51.23

Estos resultados indican que, según el pronóstico, el costo del Equipo 2 durante el mes de septiembre varió entre un mínimo de $1,065.13 y un máximo de $1,078.71, con un promedio de $1,070.06. La fecha con el costo más alto fue el 30 de septiembre, con un costo de $1,078.71.

El rango de incertidumbre promedio de $51.23 sugiere que hay una cierta variabilidad en los pronósticos, lo que significa que el costo real puede haber sido ligeramente diferente al pronosticado.

En general, estos resultados sugieren que el costo del Equipo 2 durante el mes de septiembre fue relativamente estable, con una tendencia a aumentar hacia el final del mes. Sin embargo, es importante tener en cuenta que estos son solo pronósticos y que los resultados reales pueden haber variado.



3. - El costo pronosticado para el dia 3 de septiembre fue $480.41 con un intervalo de confianza del 90% entre $466.50 y $493.35.
   - El costo pronosticado para el dia 2 de septiembre fue $480.49 con un intervalo de confianza del 90% entre $466.90 y $494.83.
     
  
Esto quiere decir que el precio de aquisicion de los equipos para esas fechas indicadas oscila entre (90% entre $466.90 y $494.83)
   
   
4. El pronóstico para el mes de septiembre incluyó los siguientes datos principales:

  - Fecha con costo más alto: 2023-09-04 con un costo de $490.67
  - Costo máximo del mes: $490.67
  - Costo mínimo: $468.92
  - Promedio mensual: $483.40
  - Rango de incertidumbre promedio: $27.11
  
  En resumen, septiembre tuvo un promedio de costo de $483.40, con un máximo de $490.67 y un mínimo de $468.92.

**Estos son algunos de los muchos resultado que hay expuestos por medio de la IA, sin embargo, por cuestiones de que son modelo gratuitos está la limitacion de token por dias**



5. La importancia de usar modelos de machine learning en la gestión de costos operativos radica en su capacidad para analizar grandes cantidades de datos, identificar patrones y tendencias, y hacer predicciones     precisas sobre los costos futuros. Esto permite a las empresas tomar decisiones informadas y optimizar sus procesos para reducir costos y mejorar la eficiencia.

   Algunos de los beneficios del uso de modelos de machine learning en la gestión de costos operativos incluyen:

   - Mejora en la precisión de las predicciones de costos
   - Identificación de patrones y tendencias en los datos que pueden ayudar a reducir costos
   - Optimización de procesos y recursos
   - Reducción de costos y mejora de la eficiencia
   - Mejora en la toma de decisiones informadas
   - En el contexto de la logística y el transporte, el uso de modelos de machine learning puede ayudar a optimizar rutas, reducir costos de combustible y mejorar la eficiencia en la gestión de la cadena de           suministro. Además, la IA puede ayudar a anticipar escenarios operativos y mejorar la toma de decisiones basadas en datos.
  

**Otros hallazgos como resultado de la consola**


<img width="527" height="402" alt="image" src="https://github.com/user-attachments/assets/314dafbc-2236-44a0-8b39-fc8a66832333" />




Porcentaje de variacion por cada insumo: Variables determinantes

- En modelo Random Forest: el 99.16% de los cambios en el costo del Equipo 1 se explican exclusivamente por la materia prima Y. Las demás variables (X, Z ) son prácticamente ruido estadístico para este equipo.
  Para el equipo 2, El 95.75% del costo es determinado por la materia prima Z. La materia prima Y tiene un impacto marginal (2.4%), y el x es ruido estadístico para este equipo."
- Bajo la metrica de confianza  R2 que indica qué tan bueno fue el modelo explicándolo con datos que nunca había visto. Para este caso el resultado es que nuestro modelo logra explicar el 68.2% de la realidad      del Equipo 1 y el 59.5% del Equipo 2 utilizando únicamente estas materias primas.
  


**Otros Hallazgos Visuales**



<img width="533" height="521" alt="image" src="https://github.com/user-attachments/assets/3d3fdfb8-a47c-422d-9946-c3231e0d932a" />



Esta matriz de correlacion mide qué tan relacionados están los insumos entre sí. Va de -1 (inverso) a 1 (idénticos). 0 significa sin relación.
- El cuadro rojo oscuro entre Price_Y y Price_Z indica una relación fuerte (0.84). Cuando el precio de Y sube, el de Z casi siempre sube también en el mercado.
 

- Los valores absolutos representan el impacto estimado: por cada dólar que sube el insumo, cuánto sube (o baja) el precio del equipo. Al ver el valor absoluto, evaluamos la "fuerza" del impacto, ignorando si es   positivo o negativo.
- El insumo Price_Y (0.80) tiene el mayor impacto absoluto por una gran diferencia. Price_X tiene un impacto menor (0.20), y Price_Z es prácticamente cero (0.0005). Esto confirma que Price_Y es el verdadero        determinante para el equipo1.
- El insumo Price_X (0.36) tiene un impacto ligeramente mayor, pero Price_Y (0.34) y Price_Z (0.33) le siguen muy de cerca con valores casi idénticos. A diferencia del Equipo 1, no hay un factor dominante, lo      que confirma que el costo del Equipo 2 se ve afectado de forma combinada por las tres materias primas


# Demostracion Visual de que el agente de IA funciona


<img width="1228" height="247" alt="image" src="https://github.com/user-attachments/assets/8212e28f-cff8-43f0-92e3-9242deaaaee4" />


# Futuros ajustes o mejoras

- Mejorar la configuracion de la inteligencia artificial para que en lugar de tener que hacerles preguntas muy puntuales porque la interfaz está hecha para seleccionar el mes y equipo a pronosticar, pueda          interpretar cualquier pregunta relacionada con cada tipo de equipo sin tener que haber seleccionado nada, sino que funcione como un cuadro de dialogo como chat gpt.
  
- Para el agente utilizar alguna API que sea de pago por el tema de la limitacion de consultas por dias, en mi caso como he estado realizando muchas pruebas, he consumido mi limite de token por dia. Mas que una    mejora puede ser una recomendacion si lo que se busca es haceer muchas consultas usar servicios gratuitos tiene limites de token. se reinicia cada dia u otra opcion es cambiar el modelo llama para seguir         haciendo preguntas. Tener en cuenta que no todos tienen la opcion de hacer busquedas externas.
  
# Apreciaciones del caso o recomendaciones

- Por lo general los modelos para pronosticar necesitan un historico que tengan todas las fechas dia a dia para mas precision a la hora de pronosticar a futuro, se pudo evidenciar que el dataset tenia saltos de dias podian ser 1,3,4. por mes para algunos tenia registros de 20 dias otros 21, etc. Conservar un historicos completo del mes seria mi recomendacion para un pronostico mas acertado. Esto solucionaría posiblemente lo dicho como futura mejora.
  
- -Al comenzar la prueba durante los primeros 3 días investigué en sitios, PDF y videos de YouTube pero todas la soluciones recurrían a utilizar Azure machine Learning el módulo de designer donde todo el flujo se construía utilizando los componentes y el proceso de predicción se realizaba de forma interna pero en este entregable pedía código funcional así que como último recurso en los dos últimos días Lunes, recurrí a la Inteligencia artificial para poder brindar una solución al caso.

- Teniendo en cuenta de que la solucion es presentada por medio de la nube, siempre que vayan a correr los notebooke en orden ejecutarlos con ejecutar all. Claro, cuando primero ya haya prendido el computo y conectado a los notebook.
  
-  Para el agente utilizar alguna API que sea de pago por el tema de la limitacion de consultas por dias, en mi caso como he estado realizando muchas pruebas, he consumido mi limite de token por dia. Mas que una    mejora puede ser una recomendacion si lo que se busca es hacer muchas consultas usar servicios gratuitos tiene limites de token, entonces podriar cambiar el modelo que se usa en mi caso (llama-3.3-70b-versatile)  Tener en cuenta que no todos tienen la opcion de hacer busquedas externas. Otra opcion es una API de pago con buena capacidad de token.



