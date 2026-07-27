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

La solución a implementar es el método de proyeccion de tendencias ya que se ajusta a lo que busca  la empresa que es: proyectar el comportamiento esperado de los costos de cada equipo para los meses requeridos por el proyecto hacia el futuro. Utilizando el modelo forecasting multivariable porque este  modelo utiliza otras variables además del historial de la variable objetivo para realizar la predicción. En este caso de negocio las otra variables son Price_X, Price_Y, Price_Z, Date y las variables objetivos  Price_Equipo1 y Price_Equipo2.

