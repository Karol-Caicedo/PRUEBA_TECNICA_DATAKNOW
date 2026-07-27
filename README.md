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



