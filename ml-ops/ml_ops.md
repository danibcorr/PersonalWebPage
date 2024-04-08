---
description: Realizado por Daniel Bazo Correa.
---

# Bibliografía

+ https://youtu.be/-dJPoLm_gtE?si=Vr0IfeshZ72GMmJp
+ https://madewithml.com/#course

# 1. Introducción

## 1.1. Conceptos

La implementación de la inteligencia artificial a nivel industrial no se limita a la creación de modelos. Existen otros desafíos al llevar estos procedimientos a producción. En general, el trabajo de un ingeniero de inteligencia artificial se divide en un 10% del tiempo dedicado al desarrollo de modelos y un 90% a la ingeniería, como el preprocesamiento de datos, obtención de características, optimización, evaluación y monitoreo de los modelos desarollados, creación y gestión des infraestructuras, entre otros.

Durante el proceso de puesta en producción, intervienen varias personas con diferentes roles. Por ejemplo, los científicos de datos se encargan de descubrir datos brutos, desarrollar características y entrenar modelos. Los ingenieros de datos llevan a producción la canalización de datos, los ingenieros de *machine learning* ponen en producción los modelos, los ingenieros de producto realizan integraciones del servicio y los ingenieros de fiabilidad del sitio se encargan de la configuración del monitoreo.

Es común que las etapas por las que se pasa durante el desarrollo del sistema sigan un esquema similar al siguiente:

<figure><img src="../ml-ops/images/diagram.png" alt=""><figcaption></figcaption></figure>

Cada paso siguiente proporciona información de retroalimentación para mejorar los resultados del modelo puesto en producción. Es importante tener en cuenta que un cambio en una parte requiere realizar cambios en el resto de componentes, por ejemplo, cambios de modelo, actualización de datos, reetiquetado, etc. Por lo tanto, se trata de un modelo continuo, donde el objetivo es poder obtener todas las métricas posibles para después del despliegue del modelo obtener información de latencia, sesgos, explicabilidad, etc, con la que mejorar la calidad de experiencia del usuario final.

Los datos son esenciales para la fiabilidad y eficiencia de los sistemas de inteligencia artificial. *MLOps* y *DevOps* son prácticas de ingeniería que buscan optimizar estos sistemas. *MLOps* combina Machine Learning, DevOps y desarrollo de software para estandarizar y simplificar la implementación, pruebas y liberación de modelos de Machine Learning. *DevOps* une a los equipos de desarrollo y operaciones para mejorar la velocidad de entrega y la calidad del producto. Ambas prácticas se centran en la automatización, el monitoreo y la colaboración para asegurar la eficiencia y seguridad de los sistemas.

Podemos crear dos tipos de sistemas principales:

+ ***Model-centric***, donde los datos son fijos y se mejora el código o el modelo.
+ ***Data-centric***, donde los modelos son fijos y se mejora los datos. 

Los sistemas *Data-centric* suelen ser más relevantes o utilizados debido a la naturaleza dinámica de los datos. Con el tiempo, los datos cambian y evolucionan, lo que puede afectar el rendimiento de los modelos de Machine Learning. Un ejemplo ilustrativo de esto se encuentra en los sistemas de predicción de emociones en textos. Uno de los conjuntos de datos más populares para este propósito es el de *IMDB*. Sin embargo, los datos de *IMDB* se recopilaron en un período de tiempo anterior, cuando las formas de expresión escrita, los gustos y las tendencias eran diferentes a los actuales. Esto significa que si se utilizan datos más recientes con un modelo entrenado con los datos de *IMDB*, las predicciones del modelo podrían verse negativamente afectadas debido a estas diferencias. Por lo tanto, en tales casos, es crucial actualizar y mejorar los datos para mantener la eficacia del modelo.

Una de las primeras y más importantes preguntas que debemos plantearnos es: **¿Cuál es el problema que el negocio está tratando de resolver?**. Comprender el contexto del negocio es crucial para el éxito de cualquier proyecto . Esto incluye conocer a los usuarios finales y sus necesidades, considerar los costos asociados con la recopilación y almacenamiento de datos, y evaluar si la inteligencia artificial es realmente la solución más adecuada para el problema en cuestión. Además, es importante entender el tipo de problema que estamos tratando de resolver, la información específica del dominio que podemos obtener, y las implicaciones de las predicciones incorrectas. Por ejemplo, ¿cómo afectarían al negocio las predicciones incorrectas? ¿Podrían tener un impacto financiero o de reputación? ¿Cómo podemos minimizar este riesgo?.

## 1.2. Herramientas

Actualmente, las herramientas que representan el estado del arte en el campo de MLOps son:

+ **Ray**: Es un *framework* diseñado para escalar y desarrollar productos utilizando aplicaciones de Machine Learning. Ray se compone de cargas de trabajo de ML que consumen datos y producen artefactos. Estos artefactos se integran en un registro del modelo para su evaluación y, posteriormente, se utilizan para ofrecer un servicio.

+ **ZenML**: Es una herramienta que permite desarrollar, ejecutar y gestionar sistemas de Machine Learning. ZenML se basa en la arquitectura de *pipeline*, lo que facilita la organización y reproducibilidad de los procesos de ML. 

Estas herramientas son fundamentales en el campo de MLOps, ya que proporcionan las funcionalidades necesarias para manejar eficientemente los flujos de trabajo de Machine Learning a escala.

# 2. Fundamentos

## 2.1. Diseño

### 2.1.1. Entorno

Primero, sería importante definir lo que es un cluster. Un *cluster* es un conjunto de servidores que se unen para formar un único sistema. Existe un nodo central, conocido como *head node*, que gestiona todos los clusters y se conecta con el resto de nodos trabajadores, conocidos como *worker nodes*. Estos nodos pueden tener prestaciones fijas o escalar automáticamente según las necesidades del sistema.

En general, dispondremos de un espacio de trabajo, denominado *workspace*, que proporciona un entorno para desarrollar sistemas utilizando las herramientas mencionadas anteriormente y que se ejecutará en un cluster. El objetivo es primero diseñar el producto, para posteriormente diseñar el sistema y finalmente comenzar con su desarrollo.

### 2.1.2. Producto

El diseño del producto debe justificar la necesidad del producto y detallar sus objetivos e impacto. Para llevar a cabo el diseño del producto, debemos plantearnos una serie de preguntas que pueden surgir al seguir los pasos siguientes:

1. **Definición del producto**: Identifica la necesidad del producto y describe sus objetivos e impacto. 

2. **Antecedentes**: Comprende a tus usuarios, sus objetivos y los obstáculos que enfrentan.

3. **Propuesta de valor**: Define qué necesita ser construido para ayudar a tus usuarios a alcanzar sus objetivos, cómo el producto aliviará sus problemas y qué ganancias creará.

4. **Objetivos**: Desglosa el producto en objetivos clave en los que te quieres enfocar.

5. **Solución**: Describe la solución necesaria para cumplir con tus objetivos, incluyendo las características principales que se desarrollarán, cómo se integrará el producto con otros servicios, las soluciones alternativas que deberías considerar, las limitaciones de las que debes ser consciente y las características que no vas a desarrollar por ahora.

6. **Factibilidad**: Evalúa qué tan factible es tu solución y si tienes los recursos necesarios para entregarla (datos, dinero, equipo, etc.).

### 2.1.3. Sistemas

De manera similar, podemos abordar el diseño del sistema considerando los siguientes aspectos:

1. **Diseño del sistema**: Considera todo, desde el consumo de datos hasta el servicio del modelo, para construir el producto.

2. **Cargas de trabajo de ML**: Describe las fuentes de datos para el entrenamiento y la producción, el proceso de etiquetado y cómo decidimos sobre las características y etiquetas.

3. **Métricas**: Vincula nuestros objetivos principales, que pueden ser cualitativos, con métricas cuantitativas hacia las cuales nuestro modelo puede optimizar.

4. **Evaluación del modelo**: Realiza la evaluación del modelo una vez que tenemos definidas nuestras métricas. Esto puede ser una evaluación sin conexión que requiere un conjunto de datos de referencia estándar, o una evaluación en línea que asegura que nuestro modelo continúe funcionando bien en producción.

5. **Rendimiento en tiempo real**: Mide el rendimiento en tiempo real antes de comprometernos a reemplazar nuestra versión existente del sistema. Esto puede implicar la implementación de canarios internos, monitoreo del rendimiento proxy/real, etc.

6. **Modelado**: Sigue principios básicos como la utilidad de extremo a extremo, prueba un sistema simple basado en reglas antes de pasar a otros más complejos, permite que el sistema complemente el proceso de toma de decisiones en lugar de tomar la decisión real, y prueba cada enfoque y evalúalo a fondo.

7. **Inferencia**: Decide si prefieres realizar inferencia en lotes (sin conexión) o en tiempo real (en línea). 

   - La **inferencia en lotes** permite hacer predicciones en lotes y almacenarlas para una inferencia de baja latencia. No requiere un servicio separado, pero las predicciones pueden volverse obsoletas si cambian los intereses del usuario.

   - La **inferencia en línea** ofrece predicciones en tiempo real y puede proporcionar una experiencia de usuario más significativa. Sin embargo, requiere un servicio separado para manejar las solicitudes y un monitoreo en tiempo real para evitar predicciones erróneas debido a un espacio de entrada ilimitado.

8. **Retroalimentación**: Recibe retroalimentación sobre nuestro sistema e incorpórala en la siguiente iteración. Esto puede involucrar tanto retroalimentación humana en el ciclo como retroalimentación automática a través de la monitorización, etc.

9.  **Impacto real**: Asegúrate de que nuestros sistemas de ML estén teniendo un impacto real. Interactúa constantemente con nuestros usuarios para iterar sobre por qué existe nuestro sistema de ML y cómo puede mejorarse.

## 2.2. Datos

### 2.2.1. Origen, ubicación y división de los datos

1. **Origen de los datos**: En cualquier proyecto de MLOps, los datos son el punto de partida. Estos pueden provenir de diversas fuentes, como una base de datos, un archivo CSV, un servicio web, entre otros.

2. **Ubicación de los datos**: La ubicación de los datos puede variar en función de las necesidades del sistema. 
    - En **sistemas más sencillos**, donde la cantidad de datos no es muy grande, puede ser suficiente alojarlos localmente en un servidor controlado por la propia empresa. 
    - Sin embargo, si se requiere escalar el sistema o integrarlo con otras tecnologías, herramientas o utilidades, puede ser necesario recurrir a **servicios en la nube** proporcionados por empresas como Amazon S3 o Google Cloud Storage. Estos servicios ofrecen la flexibilidad y escalabilidad necesarias para manejar grandes volúmenes de datos y facilitar su acceso y procesamiento.

3. **División de los datos**: Una vez que se han obtenido los datos, se procede a su división en conjuntos de entrenamiento, validación y pruebas. Esta división es esencial para prevenir el sobreajuste y garantizar que el modelo pueda generalizar adecuadamente a datos no vistos. El objetivo es asegurar que las divisiones mantengan distribuciones similares.

### 2.2.2. Balance de los datos

1. **Consideración del desequilibrio de los datos**: Es crucial considerar el posible desequilibrio de los datos, ya que puede influir en el rendimiento del modelo. Para abordar este problema, se recomienda utilizar técnicas de división de datos como la que ofrece la función `train_test_split` de la librería *Scikit-Learn*. Esta función divide los datos en dos conjuntos: uno para el entrenamiento y otro para las pruebas. Además, cuenta con un parámetro adicional, `stratify`, que permite realizar una división de los datos lo más equitativa posible.

2. **Aplicación de técnicas de sobremuestreo y submuestreo**: Existen técnicas adicionales como el sobremuestreo, que implica aumentar el número de instancias en la clase minoritaria duplicando registros o generando nuevos ejemplos sintéticos, mientras que el submuestreo implica reducir el número de instancias en la clase mayoritaria eliminando registros. Ambas técnicas buscan equilibrar la distribución de clases, mejorando así el rendimiento del modelo en datos desequilibrados.

3. **Evaluación del impacto de las técnicas de balanceo en el rendimiento del modelo**: Sin embargo, es importante tener en cuenta que el sobremuestreo puede llevar al sobreajuste si se generan ejemplos muy similares, y el submuestreo puede resultar en pérdida de información si se eliminan ejemplos potencialmente útiles. Por lo tanto, se deben aplicar con cuidado y evaluar su impacto en el rendimiento del modelo.

### 2.2.3. Análisis Exploratorio de Datos (EDA)

El *Exploratory Data Analysis (EDA)* es un proceso cíclico que puede implementarse en diferentes etapas del desarrollo del proyecto, ya sea antes o después del etiquetado y el preprocesamiento de los datos, dependiendo de la definición del problema. El objetivo es comprender el conjunto de datos para asegurar que sea adecuado para la tarea en cuestión. 

Este proceso incluye varias actividades, entre las que se encuentran:


1. **Visualización de gráficos**: Esta actividad permite obtener información relevante de los datos. Por ejemplo, se pueden realizar visualizaciones de la distribución de etiquetas utilizando gráficos de barras para mostrar la cantidad de puntos de datos por etiqueta.

2. **Extracción de *insights***: Durante el EDA, se cuestiona si la cantidad de datos es suficiente y se extraen ideas o *insights*. Estas ideas pueden ayudar a entender la distribución de los datos, identificar posibles correlaciones entre las características, detectar anomalías, entre otros aspectos.

3. **Creación de nubes de palabras**: Las nubes de palabras se utilizan para explorar la frecuencia de palabras en los títulos y descripciones de los proyectos. El objetivo de esta actividad es evaluar si estas características proporcionan suficiente información única para predecicir las etiquetas correctamente.

### 2.2.4. Procesamiento de los datos

El procesamiento de los datos es una etapa crítica en el desarrollo de modelos de aprendizaje automático, ya que garantiza que los datos estén en un formato adecuado para su análisis y modelado. 

Este proceso puede dividirse en dos partes principales: 

1. **Preparación de los datos**: Esta etapa implica organizar y limpiar los datos. Las tareas pueden incluir la unión de tablas de datos existentes para organizar toda la información relevante en una vista única, la identificación y manejo de valores faltantes mediante la eliminación de filas o columnas, reemplazo de valores faltantes con estimaciones (por ejemplo, la media), la detección y manejo de valores atípicos que pueden distorsionar los resultados del modelo, y la ingeniería de características, que implica combinar características existentes de maneras únicas para extraer señales adicionales. 
   
   - Algunas técnicas a utilizar: aumentación de datos, eliminación de muestras y la asignación de pesos por clases, etc.

2. **Transformación de los datos**: Esta etapa puede implicar tareas como la normalización de los datos para ajustar las escalas de las características de manera que los modelos puedan procesarlas de manera eficaz. Esto puede incluir la estandarización o la normalización. También puede implicar la codificación de características, que convierte características categóricas en representaciones numéricas, y la extracción de características, que deriva nuevas características de las existentes para resaltar la información relevante. 
   
   - Algunas técnicas a utilizar: PCA, *Auto Encoders*, tokenización (LLM), etc.

### 2.2.5. Distribución de los datos

El procesamiento de datos distribuido es una estrategia esencial para manejar conjuntos de datos grandes y mejorar el rendimiento en aplicaciones de aprendizaje automático. El objetivo es realizar estos procedimientos de manera distribuida utilizando un *framework* que permita escalar estos sistemas de manera sencilla. 

En este contexto, **Ray** se destaca como una herramienta eficaz, ya que permite dividir la carga entre todas las máquinas posibles (*workers*), requiere mínimos cambios en el código y es compatible con Python. Además de Ray, existen otras herramientas para la computación distribuida como Apache Spark, Dask, y Modin. Sin embargo, cada una de estas herramientas tiene sus propias características y puede ser más adecuada para ciertos tipos de tareas o entornos.

El proceso de distribución de datos con Ray implica varias etapas:

1. **Configuración**: Ray se configura para preservar el orden al realizar operaciones en los datos, garantizando resultados reproducibles y deterministas.

2. **Ingesta de datos**: Se pueden leer y procesar datos desde una variedad de formatos y fuentes, como archivos CSV, utilizando las funciones de entrada/salida de Ray.

3. **División de datos**: Ray proporciona una función incorporada para dividir conjuntos de datos en conjuntos de entrenamiento y validación. Esta función puede ser modificada para estratificar la división basada en una columna específica, como la etiqueta.

4. **Preprocesamiento**: Ray permite utilizar funciones de preprocesamiento existentes, como las implementadas en Pandas, de manera distribuida. Las operaciones de preprocesamiento se pueden aplicar a lotes de datos en paralelo, mejorando así la eficiencia y el rendimiento.

## 2.3. Modelo

### 2.3.1. Creación del modelo base

El primer paso en el desarrollo de un modelo de aprendizaje automático es la creación del modelo base. Este modelo inicial puede ser tan simple como un conjunto de reglas `if-else`. A partir de este punto, se incrementa la complejidad del modelo de manera gradual, evaluando factores como la latencia y el tamaño del modelo en cada paso. El objetivo es lograr un equilibrio óptimo entre la complejidad del modelo y su rendimiento.

Para agregar complejidad a los modelos, se recomienda seguir un enfoque gradual:

1. **Enfoque basado en reglas**: Este enfoque consiste en construir reglas basadas en características específicas del problema. 
   
2. **Incremento de la complejidad**: Se recomienda incrementar la complejidad de manera gradual, abordando limitaciones y considerando diferentes representaciones y arquitecturas de modelos. 
   
3. **Compromiso**: Es esencial evaluar los resultados con el fin de realizar un balance entre el rendimiento del modelo, la latencia y el tamaño. Los modelos deben ser revisados y ajustados continuamente a medida que el conjunto de datos crece y surgen nuevas arquitecturas. 

### 2.3.2. Entrenamiento distribuido

El entrenamiento distribuido es una estrategia que facilita el entrenamiento eficiente de modelos de aprendizaje automático en sistemas distribuidos. Utilizando herramientas como Ray u otras plataformas similares, se puede aprovechar la escalabilidad inherente de los sistemas distribuidos. En este enfoque, un nodo central, también conocido como nodo maestro, orquesta el proceso de entrenamiento, mientras que los nodos trabajadores se encargan de entrenar el modelo y enviar los resultados al nodo central.

Para implementar el entrenamiento distribuido, se deben seguir los siguientes pasos:

1. **División de los datos entre los nodos trabajadores**: Cada nodo trabajador recibe una porción de los datos para entrenar el modelo. Esta división de datos permite que cada nodo trabajador pueda entrenar el modelo de manera independiente y paralela.

   - **Componentes a tener en cuenta**: Número de nodos trabajadores, el uso de unidades de procesamiento gráfico (*GPU*), los recursos asignados a cada nodo y la disponibilidad de recursos de CPU, entre otros. 
   
2. **Preparación del modelo para la ejecución distribuida**: Es necesario adaptar el modelo para permitir su entrenamiento en múltiples nodos trabajadores de manera simultánea. Esto puede implicar la implementación de técnicas de paralelización y sincronización.

3. **Configuración del entorno de entrenamiento**: Se deben realizar ajustes en el entorno de entrenamiento para admitir la ejecución distribuida. Esto puede incluir la configuración de la red, la asignación de recursos y la instalación de las bibliotecas y dependencias necesarias.

4. **Registro de métricas**: Es recomendable llevar un registro de las métricas de rendimiento del modelo durante el entrenamiento. Estas métricas pueden incluir la precisión, la pérdida, el tiempo de entrenamiento, entre otros. El seguimiento de estas métricas puede ayudar a identificar problemas y a optimizar el rendimiento del modelo.

5. **Guardado de puntos de control del modelo**: Es útil guardar el estado del modelo en diferentes puntos durante el entrenamiento. Estos puntos de control, o *checkpoints*, facilitan la reanudación del proceso de entrenamiento en caso de interrupciones, así como la depuración del modelo.

### 2.3.3. Iteración en los datos

En lugar de iterar en los modelos manteniendo el conjunto de datos fijo, otra estrategia consiste en mantener el modelo constante e iterar en el conjunto de datos. Este enfoque es útil para mejorar la calidad de los conjuntos de datos, permitiendo realizar ajustes como la eliminación o corrección de muestras de datos incorrectas, la transformación de características, la expansión de clases, la incorporación de conjuntos de datos adicionales, etc.

### 2.3.4. Optimización del modelo

Las estrategias de entrenamiento distribuido son excelentes cuando nuestros datos o modelos son demasiado grandes para el entrenamiento, pero existen estrategias adicionales para hacer que los modelos sean más pequeños para su implementación. Algunas de las técnicas de compresión de modelos son:

- **Pruning**: Elimina pesos (no estructurados) o canales enteros (estructurados) para reducir el tamaño de la red. El objetivo es preservar el rendimiento del modelo mientras se aumenta su dispersión.

- **Quantization**: Reduce la huella de memoria de los pesos al reducir su precisión (por ejemplo, de 32 bits a 8 bits). Podemos perder algo de precisión, pero no debería afectar demasiado al rendimiento.

- **Distillation**: Entrena redes más pequeñas para "imitar" a las redes más grandes al reproducir las salidas de las capas de la red más grande.

### 2.3.5. Ajuste de hiperparámetros

El ajuste de hiperparámetros es un procedimiento que se enfoca en descubrir los hiperparámetros ideales para un modelo de aprendizaje automático. Ray ofrece una herramienta llamada Ray Tune, la cual se integra con HyperOpt. Esta combinación permite definir un espacio de búsqueda y un algoritmo de búsqueda, entre otros aspectos. Además, Ray facilita la visualización del proceso de ajuste a través de herramientas como MLflow. Esto proporciona un mayor control y capacidad para seleccionar los parámetros más efectivos para el modelo.

Aquí se presentan algunas consideraciones clave a tener en cuenta al realizar el ajuste de hiperparámetros, sin importar el marco de trabajo que se esté utilizando:

1. **Definición del problema**: Antes de comenzar con el ajuste de hiperparámetros, es importante tener una comprensión clara del problema que se está resolviendo. Esto ayudará a determinar qué hiperparámetros son relevantes para el problema y cuáles no.

2. **Selección de hiperparámetros**: No todos los hiperparámetros son igualmente importantes para todos los problemas. Algunos pueden tener un impacto significativo en el rendimiento del modelo, mientras que otros pueden tener un impacto mínimo. Es importante identificar cuáles son los hiperparámetros más relevantes para el problema en cuestión.

3. **Definición del espacio de búsqueda**: El espacio de búsqueda de hiperparámetros es el rango de valores que cada hiperparámetro puede tomar. Es importante definir un espacio de búsqueda que sea lo suficientemente amplio como para incluir el valor óptimo del hiperparámetro, pero no tan amplio como para hacer que la búsqueda sea ineficiente.

4. **Elección del método de búsqueda**: Existen varios métodos para buscar en el espacio de hiperparámetros, como la búsqueda en cuadrícula, la búsqueda aleatoria y los métodos de optimización bayesiana. La elección del método de búsqueda depende de factores como el tamaño del espacio de búsqueda, el tiempo disponible para la búsqueda y la complejidad del modelo.

5. **Validación cruzada**: La validación cruzada es una técnica que se utiliza para estimar el rendimiento de un modelo en datos no vistos. Es especialmente útil en el ajuste de hiperparámetros, ya que permite obtener una estimación más robusta del rendimiento del modelo para diferentes conjuntos de hiperparámetros.

6. **Evaluación del rendimiento**: Es importante definir una métrica de rendimiento clara y relevante para el problema que se está resolviendo. Esta métrica se utilizará para comparar diferentes conjuntos de hiperparámetros y seleccionar el mejor.

7. **Iteración y refinamiento**: El ajuste de hiperparámetros es un proceso iterativo. A medida que se obtienen más información sobre el rendimiento del modelo con diferentes conjuntos de hiperparámetros, se puede refinar el espacio de búsqueda y el método de búsqueda para concentrarse en las regiones del espacio de hiperparámetros que parecen ser más prometedoras.

### 2.3.6. Métricas de evaluación

1. **Importancia de las métricas de evaluación**: Las métricas de evaluación son esenciales para evaluar el rendimiento de un modelo de *machine learning*. Es vital identificar y priorizar las métricas relevantes para el problema que se está resolviendo. Sin embargo, es importante evitar la sobreoptimización de una métrica específica a expensas de otras, ya que esto podría afectar negativamente el rendimiento general del modelo.

2. **Selección de métricas**: Dependiendo del problema, se pueden utilizar diferentes métricas. Por ejemplo, en las tareas de clasificación, la métrica F1, que es la media armónica de la precisión y la exhaustividad, puede ser útil, especialmente cuando las clases están desequilibradas.

3. **Uso de técnicas de interpretación**: Las técnicas de interpretación, como las matrices de confusión y *Grad-CAM*, pueden ser útiles para entender cómo el modelo está tomando sus decisiones. Estas técnicas pueden proporcionar una visión de qué características de la entrada son importantes para las predicciones del modelo.

4. **Evaluación integral del modelado**: La evaluación es una parte crucial del proceso de modelado. Aunque a menudo se centra en calcular métricas globales como la precisión, en muchos casos, se requiere una evaluación más detallada y matizada.

5. **Preparación para la evaluación**: Antes de comenzar la evaluación, es importante:
    - Definir claramente las métricas que se van a priorizar.
    - Evitar la sobreoptimización en una métrica específica, ya que podría comprometer otros aspectos del rendimiento del modelo.

6. **Configuración de la evaluación**: Al configurar la evaluación, se deben preparar todos los datos necesarios, incluyendo las etiquetas verdaderas, las etiquetas predichas y las probabilidades predichas.

7. **Análisis de los resultados**: Además de calcular las métricas para cada clase, también se pueden analizar los verdaderos positivos, falsos positivos y falsos negativos para obtener una visión más detallada del rendimiento del modelo.

8. **Inspección de las entradas del modelo**: Además de comparar las salidas predichas con los valores verdaderos, también se puede inspeccionar las entradas del modelo para entender qué características de la entrada son más influyentes para las predicciones del modelo.

9. **Realización de pruebas de comportamiento**: Las pruebas de comportamiento, que tratan el modelo como una caja negra y se centran en probar los datos de entrada y las salidas esperadas, pueden ser útiles para evaluar el rendimiento del modelo en condiciones más realistas.

10. **Evaluación en línea**: Después de evaluar el rendimiento del modelo en un conjunto de datos estático, se pueden utilizar técnicas de evaluación en línea para evaluar el rendimiento del modelo en datos de producción reales.

### 2.3.7. Modelos como servicios

La implementación de modelos de aprendizaje automático como servicios es un aspecto crucial en la cadena de valor de la ciencia de datos. Esto permite que los modelos se utilicen en aplicaciones en tiempo real y por lotes, proporcionando escalabilidad y robustez. Aquí se presentan algunos puntos clave a considerar:

1. **Introducción a la implementación de modelos**: La implementación de modelos implica hacer que los modelos de aprendizaje automático estén disponibles para su uso en un entorno de producción, lo que requiere consideraciones de escalabilidad, robustez, rendimiento y latencia.

2. **Elección del marco de trabajo**: Existen varios marcos de trabajo para la implementación de modelos, cada uno con sus propias ventajas y desventajas. La elección del marco de trabajo depende de varios factores, incluyendo las necesidades del proyecto, la escalabilidad requerida, la compatibilidad con diferentes marcos de aprendizaje automático, y las capacidades de integración con otras tecnologías.

3. **Inferencia por lotes**: La inferencia por lotes implica hacer predicciones sobre un gran conjunto de datos a la vez. Esto puede ser útil en situaciones donde no se requiere una respuesta en tiempo real, y puede ser más eficiente en términos de recursos computacionales.

4. **Inferencia en tiempo real**: La inferencia en tiempo real implica hacer predicciones sobre datos a medida que se reciben. Esto es crucial para muchas aplicaciones en tiempo real, donde las decisiones deben tomarse rápidamente.

5. **Personalización del servicio**: Dependiendo de las necesidades del proyecto, puede ser necesario personalizar el servicio de implementación. Esto puede implicar la adición de lógica personalizada para manejar casos específicos, o la configuración de umbrales para controlar la confianza de las predicciones.

6. **Despliegue y pruebas**: Una vez que el servicio de implementación está configurado, debe ser desplegado y probado para asegurar que funciona como se espera. Esto puede implicar la realización de pruebas de carga para evaluar la escalabilidad del servicio, así como pruebas funcionales para verificar la precisión de las predicciones.