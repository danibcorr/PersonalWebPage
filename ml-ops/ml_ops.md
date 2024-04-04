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

   1. La **inferencia en lotes** permite hacer predicciones en lotes y almacenarlas para una inferencia de baja latencia. No requiere un servicio separado, pero las predicciones pueden volverse obsoletas si cambian los intereses del usuario.

   2. La **inferencia en línea** ofrece predicciones en tiempo real y puede proporcionar una experiencia de usuario más significativa. Sin embargo, requiere un servicio separado para manejar las solicitudes y un monitoreo en tiempo real para evitar predicciones erróneas debido a un espacio de entrada ilimitado.

8. **Retroalimentación**: Recibe retroalimentación sobre nuestro sistema e incorpórala en la siguiente iteración. Esto puede involucrar tanto retroalimentación humana en el ciclo como retroalimentación automática a través de la monitorización, etc.

9.  **Impacto real**: Asegúrate de que nuestros sistemas de ML estén teniendo un impacto real. Interactúa constantemente con nuestros usuarios para iterar sobre por qué existe nuestro sistema de ML y cómo puede mejorarse.

## 2.2. Datos
### 2.2.1. Preparación
### 2.2.2. Exploración
### 2.2.3. Preprocesamiento
### 2.2.4. Distribuido

## 2.3. Modelo
### 2.3.1. Formación
### 2.3.2. Seguimiento
### 2.3.3. Ajuste
### 2.3.4. Evaluación
### 2.3.5. Servicio

## 2.4. Desarrollar
### 2.4.1. Scripting
### 2.4.2. Línea de comandos

## 2.5. Utilidades
### 2.5.1. Registro
### 2.5.2. Documentación
### 2.5.3. Estilización
### 2.5.4. Pre-commit

## 2.6. Prueba
### 2.6.1. Código
### 2.6.2. Datos
### 2.6.3. Modelos

## 2.7. Reproducibilidad
### 2.7.1. Versionado

## 2.8. Producción
### 2.8.1. Trabajos y servicios
### 2.8.2. Flujos de trabajo CI/CD
### 2.8.3. Monitorización
### 2.8.4. Ingeniería de datos