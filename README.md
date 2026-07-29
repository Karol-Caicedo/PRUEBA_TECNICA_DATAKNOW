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

Preguntas realizadas al modelo de IA
1. ¿Cuál fue el pronostico para el dia 3 de septiembre?, ¿y para el dia 2? -> Equipo2
2. ¿Cuál fue el pronostico para el mes de septiembre? -> equipo2
3. ¿Cuál fue el pronostico para el dia 1 de octubre?, ¿y para el dia 2? -> Equipo2
4. ¿Cuál fue el pronostico para el mes de octubre? -> equipo2 ¿cómo se interpretan estos resultados?
5. ¿Cuál fue el pronostico para el dia 3 de septiembre?, ¿y para el dia 2? -> Equipo1
6. ¿Cuál fue el pronostico para el mes de septiembre? -> equipo1
7. ¿Cuál fue el pronostico para el dia 1 de octubre?, ¿y para el dia 2? -> Equipo1
8- ¿Cuál fue el pronostico para el mes de octubre? -> equipo1 ¿cómo se interpretan estos resultados?



Respuesta
1 - El pronóstico para el día 3 de septiembre fue de $1,076.63 con un rango de incertidumbre del 90% entre $1,049.83 y $1,100.85.
  - El pronóstico para el día 2 de septiembre fue de $1,076.19 con un rango de incertidumbre del 90% entre $1,050.11 y $1,099.30.

Esto quiere decir que el precio de aquisicion de los equipos para esas fechas indicadas oscila entre (90% entre $1,049.83 y $1,100.85) y (90% entre $1,050.11 y $1,099.30.)

2 - El pronóstico para el mes de septiembre incluyó los siguientes datos principales:

Fecha con costo más alto: 30 de septiembre con un costo de $1,078.71
Costo máximo del mes: $1,078.71
Costo mínimo: $1,065.13
Promedio mensual: $1,070.06
Rango de incertidumbre promedio: $51.23

Estos resultados indican que, según el pronóstico, el costo del Equipo 2 durante el mes de septiembre varió entre un mínimo de $1,065.13 y un máximo de $1,078.71, con un promedio de $1,070.06. La fecha con el costo más alto fue el 30 de septiembre, con un costo de $1,078.71.

El rango de incertidumbre promedio de $51.23 sugiere que hay una cierta variabilidad en los pronósticos, lo que significa que el costo real puede haber sido ligeramente diferente al pronosticado.

En general, estos resultados sugieren que el costo del Equipo 2 durante el mes de septiembre fue relativamente estable, con una tendencia a aumentar hacia el final del mes. Sin embargo, es importante tener en cuenta que estos son solo pronósticos y que los resultados reales pueden haber variado.

3. ¿Cuál fue el pronostico para el dia 1 de octubre?, ¿y para el dia 2? -> Equipo2

   
5. ¿Cuál fue el pronostico para el mes de octubre? -> equipo2 ¿cómo se interpretan estos resultados?

4. ¿Cuál fue el pronostico para el mes de octubre? -> equipo2 ¿cómo se interpretan estos resultados?
   
6. ¿Cuál fue el pronostico para el dia 3 de septiembre?, ¿y para el dia 2? -> Equipo1
   - El costo pronosticado para el dia 3 de septiembre fue $480.41 con un intervalo de confianza del 90% entre $466.50 y $493.35.
   - El costo pronosticado para el dia 2 de septiembre fue $480.49 con un intervalo de confianza del 90% entre $466.90 y $494.83.
  
Esto quiere decir que el precio de aquisicion de los equipos para esas fechas indicadas oscila entre (90% entre $466.90 y $494.83)
   
8. ¿Cuál fue el pronostico para el mes de septiembre? -> equipo1
   
10. ¿Cuál fue el pronostico para el dia 1 de octubre?, ¿y para el dia 2? -> Equipo1
    
8- ¿Cuál fue el pronostico para el mes de octubre? -> equipo1 ¿cómo se interpretan estos resultados?






# Demostracion Visual de que el agente de IA funciona


<img width="710" height="365" alt="Captura de pantalla 2026-07-29 045610" src="https://github.com/user-attachments/assets/03b21fe9-23dc-4084-b3e8-c81989693c30" />


# Futuros ajustes o mejoras

- Ajustar el modelo de pronostico Prophet ademas de dar como resultado el precio a futuro de las variables independientes tambien de el precio del equipo ya que solo muestra el nombre mas no el precio.
- Mejorar la configuracion de la inteligencia artificial para que en lugar de tener que hacerles preguntas muy puntuales porque la interfaz está hecha para seleccionar el mes y equipo a pronosticar, pueda         interpretar cualquier pregunta relacionada con cada tipo de equipo sin tener que haber seleccionado nada, sino que funcione como un cuadro de dialogo como chat gpt.
# Apreciaciones del caso o recomendaciones

- Por lo general los modelos para pronosticar necesitan un historico que tengan todas las fechas dia a dia para mas precision a la hora de pronosticar a futuro, se pudo evidenciar que el dataset tenia saltos de dias podian ser 1,3,4. por mes para algunos tenia registros de 20 dias otros 21, etc. Conservar un historicos completo del mes seria mi recomendacion para un pronostico mas acertado. Esto solucionaría posiblemente lo dicho como futura mejora.
  
- -Al comenzar la prueba durante los primeros 3 días investigué en sitios, PDF y videos de YouTube pero todas la soluciones recurrían a utilizar Azure machine Learning el módulo de designer donde todo el flujo se construía utilizando los componentes y el proceso de predicción se realizaba de forma interna pero en este entregable pedía código funcional así que como último recurso en los dos últimos días Lunes, recurrí a la Inteligencia artificial para poder brindar una solución al caso.

- Teniendo en cuenta de que la solucion es presentada por medio de la nube, siempre que vayan a correr los notebook ejecutarlos con ejecutar all. Claro, cuando primero ya haya prendido el computo y conectado a los notebook.


