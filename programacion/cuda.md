---
description: Realizado por Daniel Bazo Correa.
---

# CUDA

## Bibliografía

* [https://www.nvidia.com/](https://www.nvidia.com/)
* [El DLI (Deep Learning Institute) (uma.es)](http://nvidiadli.uma.es/index.php/es/certificaciones-nvidia)
* [CuPy: NumPy & SciPy for GPU](https://cupy.dev/)
* [Numba: A High Performance Python Compiler (pydata.org)](https://numba.pydata.org/)

## Tema 1: Acelerar aplicaciones con CUDA, C y C++

### 1.1. Introducción

Existen diferentes gamas de GPU para NVidia:

* **GeForce**: enfocadas al mercado doméstico (consumidor general).
* **Quadro**: enfocadas al sector profesional. Sobre todo en el uso de renderización o aplicaciones similares.
* **Tegra**: utilizado en sistemas de bajo consumo como móviles o sistemas empotrados.
* **Tesla**: llevado a nivel industrial/empresa. Por ejemplo, este tipo de gráficas son las que suele dar Google en Google Colab.

CUDA cuenta con un amplio ecosistema aunque nosotros nos centraremos en C/C++.

<figure><img src="../.gitbook/assets/B0FF9827-9E32-46F2-8365-FA0E686C649D.jpeg" alt=""><figcaption></figcaption></figure>

Existen 3 cualidades principales que han hecho que la GPU sea un elemento único y fundamental en CUDA:

* **Simplicidad**: el control de un hilo se amortiza en otros 31. Esto se conoce como warp size, cuyo valor es de 32.
* **Escalabilidad**: gracias a la gran cantidad de datos existentes en la actualidad se consiguen sistemas/modelos de paralelización sostenible. La paralelización sólo sería necesario implementar en aplicaciones a gran escala permitiendo crear el paralelismo de datos (SIMT).
* **Productividad**: cuando un hilo pasa a realizar operaciones que no permitan su ejecución veloz, otro hilo oculta su latencia tomando el procesador de forma inmediata (conmutan de forma inmediata). Decir que lo hilos no tienen dependencia.

Algunos conceptos a conocer son:

*   **Warp**: visto desde el hardware, un bloque de hilos se compone de "warps". Un warp es un conjunto de 32 hilos (32 es la resolución del planificador para emitir hilos por grupos a las unidades de ejecución) dentro de un bloque de hilos, de manera que todos los hilos de un warp ejecutan la misma instrucción. Una vez que se lanza un bloque de hilos en un multiprocesador, todos sus warps son residentes hasta que finaliza su ejecución. Así, un nuevo bloque no se lanza en un multiprocesador hasta que haya un número suficiente de registros libres para todos los warps del nuevo bloque, y hasta que haya suficiente memoria compartida libre para el nuevo bloque.

    Estos hilos, se caracterizan por conmutar entre ellos de forma inmediata.

    A modo de resumen, vemos que los hilos se agrupan en warps, los warps en bloques y los bloques en mallas.
* **SIMT**: Single Instruction, Multiple Thread.

CUDA (Compute Unified Device Architecture) es una plataforma diseñada a partir de la unión de software, firmware y hardware:

* **Software**: permite programar la GPU con extensiones SIMD (agrupaciones de multiprocesadores que comparten una misma unidad de control, _Single Instruction Multiple Data_) permitiendo ejecuciones eficientes y escalables.
* **Firmware**: ofrece drivers para la programación GPGPU compatible con trabajos de renderizar, manejo de APIs, manejo de memoria, etc.
* **Hardware**: habilita el paralelismo de la GPU para propósito general.

A pesar de que CUDA introduzca ventajas favorables para la computación tenemos que mantener un equilibrio entre lo que se procesa en la GPU y la CPU. Este tipo de computación se conoce como computación heterogénea (comutación compuesta por la GPU y la CPU donde: GPU → Intensiva en datos, paralelismo fino, CPU → Saltos y bifurcaciones, paralelismo grueso) . Esta consiste en identificar las partes del código de una aplicación que se pueden paralelizar en la GPU pero también identificar aquellas partes que se pueden procesar directamente de manera secuencial en la CPU.

<figure><img src="../.gitbook/assets/EEA7EE5C-1D79-4B88-8DF7-37E17BF0D2FF.jpeg" alt=""><figcaption></figcaption></figure>

Por tanto, vemos que el pararelismo por el que CUDA destaca es en el parelilismo de datos (**data parallelism**).

### 1.2. Hardware de CUDA

Una GPU cuenta con:

* _N_ multiprocesadores, cada uno dotado de _M_ cores.

Algunas de las familias de GPU de la familia Tesla de NVidia son:

<figure><img src="../.gitbook/assets/Untitled (1).png" alt=""><figcaption></figcaption></figure>

Cada multiprocesador cuenta con su banco de registros, memoria compartida y una caché de constantes y otra de texturas (ambas de sólo lectura y uso marginal). También, se cuenta con una memoria global de la memoria de vídeo de tipo GDDR la cual es 3 veces más rápida que la memoria principal de la CPU pero mucho más lenta que la memoria compartida de tipo SRAM. Un bloque de hilos en CUDA se puede asignar a cualquier multriprocesador de la CPU para su ejecución. Si lanzamos un Kernel que tiene un solo bloque, sólo aprovecharemos uno de los multiprocesadores de la GPU.

<figure><img src="../.gitbook/assets/Untitled 1 (1).png" alt=""><figcaption></figcaption></figure>

A modo de ejemplo, cogeremos la generación Volta para estudiar su interior. En concreto, veremos la GPU GV100 que cuenta con 84 SMs y 8 controladores de memoria de 512 bits.

El multiprocesador de Volta cuenta con 64 cores de tipo int32, 64 cores de tipo float32, 32 cores de tipo float64 y 8 unidades tensor.

<figure><img src="../.gitbook/assets/Untitled 2.png" alt=""><figcaption></figcaption></figure>

De la imagen anterior vemos que se realiza el diseño de un solo bloque para posteriormente ir copiando creando un diseño más complejo.

<figure><img src="../.gitbook/assets/Untitled 3.png" alt=""><figcaption></figcaption></figure>

La estructura del core tensor permite realizar operaciones matriciales a mayor velocidad (entrenar modelos de Deep Learning con mayor eficiencia). La imagen siguiente muestra el proceso:

<figure><img src="../.gitbook/assets/Untitled 4 (2).png" alt=""><figcaption></figcaption></figure>

Cambiar el valor de la precisión de los datos, por ejemplo pasar de un valor entero de 32 bits a un entero de 16 bits, repercute en la tasa de transferencia (_Throughput_) que fluye por un sistema. Por tanto se consigue realizar un mayor número de operaciones pero con menor precisión en los datos aunque dependiendo de la aplicación esta precisión no sería relevante. A continuación se muestra el formato del Throughput para distintas precisiones de datos en arquitecturas de GPU más modernas:

<figure><img src="../.gitbook/assets/Untitled 5 (2).png" alt=""><figcaption></figcaption></figure>

### 1.3. Programación en CUDA

#### 1.3.1. Conceptos básicos de la programación con CUDA

**Toda función que cuenta con paralelización escrita en CUDA recibe el nombre de Kernel.**

Si queremos conocer la GPU, junto con sus características, que nos ha tocado en alguna de las plataformas online como AWS o Google Colab podemos utilizar el siguiente código en una celda de un cuaderno Jupyter:

```c
!nvidia-smi
```

Durante la programación con CUDA tanto la CPU como la GPU se encuentran realizando operaciones, por lo tanto existe la necesidad de tener que sincronizar los tiempos entre la ejecución de ambos componentes.

<figure><img src="../.gitbook/assets/Untitled 6 (2).png" alt=""><figcaption></figcaption></figure>

Debido a esa sincronización necesaria entre procesos que suceden en la GPU y la CPU e incluso entre diferentes hilos de la GPU, las sentencias condicionales como los `if` son muy desfavorables para su ejecución en la GPU. Por lo que, cuantos menos sentencias condicionales en un Kernel, mejor.

En este caso, toda la programación con CUDA se realizará utilizando C/C++ pero los ficheros acelerados por CUDA tendrán extensión `.cu`. La compilación del código de CUDA se realiza de la siguiente manera:

```c
!nvcc -arch=sm_70 -o resultado_nombre programa.cu -run
```

Del comando anterior, `-arch=sm_70` indica la arquitectura a la que debe ser compilador el fichero.

A continuación mostramos un ejemplo de código empleando CUDA:

```c
#include <iostream>

using namespace std;

void hola_cpu(void)
{
	printf("Esto es un saludo desde la CPU");
}

__global__ void ejemplo_kernel(void)
{
	printf("Hola, esto se está ejecutando de forma paralela en GPU");
}

int main(void)
{
	hola_cpu();
	ejemplo_kernel<<<1, 1>>>();
	
	cudaDeviceSynchronize();
	
	return 0;
}
```

Utilizamos la palabra `__global__` delante de la definición de una función para indicar que se ejecuta desde la GPU y que puede ser invocada de manera global, es decir, tanto en la GPU como en la CPU. En ocasiones, nos referiremos al código ejecutado en CPU como **host** y el código ejecutado en GPU como **device**. Además, el tipo de función de `__global__` ha de ser de tipo `void()` . Para llamar a la función que emplea CUDA utilizamos `nombre_funcion<<<x, y>>>` , dicha invocación a la función escrita en CUDA recibe el nombre de **configuración de ejecución**, en ella:

* `x`: hace referencia al número de bloques que se van a emplear. Ha de ser menor a 2048 (2 GigaBloques). A su vez, un conjunto de bloques forman una malla o _grid_.
* `y`: hace referencia al número de hilos por bloque. Ha de ser menor a 1024 (1 GigaHebras).

Por tanto, el número total de hebras será el resultado de multiplicar el valor de `x` por `y`. Por ejemplo, si tenemos 2 bloques (`x = 2`) y 4 hebras por bloque (`y = 4`), tendremos un total de 8 hebras. **Recalcar, que el número de bloques y hebras dependerá de las capacidades hardware que estemos utilizando, es decir, de la GPU que se esté empleando.**

El código del Kernel se ejecuta en cada hebra de cada bloque configurado cuando se lanza dicho Kernel.

Vemos en el código anterior una llamada a la función `cudaDeviceSynchronize()` . Esta función permite a la GPU finalizar su tarea antes de que la CPU finalice y acabe con el programa. Por lo tanto, se trata de una herramienta de sincronización entre la CPU y la GPU. Por lo que, si la GPU tiene que realizar una acción previa a la CPU, el orden de ejecución debería ser:

1. GPU.
2. Sincronización (`cudaDeviceSynchronize()`).
3. CPU.

Podemos utilizar CUDA para agilizar los bucles durante la programación. Por ejemplo, si queremos incrementar un valor `b` a los `N` elementos de un vector:

```c
void incremento_en_cpu(float *a, float b, int N)
{
	for (int idx = 0; idx<N; idx++)
	{
		a[idx] = a[idx] + b;
	}
}
void main()
{
	...
	incremento_en_cpu(a, b, N);
}
```

Analizaríamos el bucle, llegando a la conclusión de que se puede paralelizar ya que un índice es independiente del otro y tampoco requiere de un orden específico (recordar que las hebras de un _warp_ se ejecutan de manera desordenada).

Primero, saber que CUDA proporciona variables que describen a las hebras, bloques y mallas (_grid_):

| Función     | Definición                                                        |
| ----------- | ----------------------------------------------------------------- |
| gridDim.x   | Es el número de bloques en la malla.                              |
| blockIdx.x  | Es el índice del bloque actual de la malla.                       |
| blockDim.x  | Dentro de un Kernel describe el número de hebras en un bloque.    |
| threadIdx.x | Dentro de un kernel describe el índice de una hebra de un bloque. |

Decir que no podemos comunicar los bloques de un mismo kernel durante su ejecución ya que los bloques pueden ejecutarse en cualquier orden y de forma independiente.

Con ello, la única consideración a realizar es que hay que programar el Kernel para que realice el trabajo de una sola iteración del bucle. Por lo tanto, la configuración del Kernel (la llamada a la función) tiene que ejecutarse tantas veces como iteraciones del bucle (ajustar acorde a ello el número de bloques y de hebras por bloque). Tras esto, pasamos a paralelizar el bloque de código presentado anteriormente:

```c
__global__ void incremento_en_gpu(float *a, float b, int N)
{
	int idx = blockIdx.x * blockDim.x + threadIdx.x;

	if (idx < N)
	{
		a[idx] = a[idx] + b;
	}
}

void main()
{
	...
	dim3 dimBlock (blocksize);
	dim3 dimGrid (ceil(N/(float)blocksize));
	incremento_en_gpu<<<dimGrid, dimBlock>>>(a, b, N);
}
```

En la imagen anterior vemos que hay `N` hilos haciendo 1 iteración.

Con la fórmula siguiente podemos mapear cada hebra un elemento del bucle, es decir, un índice del bucle:

$$
i_{x}=(blockIdx.x \cdot blockDim.x)+threadIdx.x
$$

Por ejemplo:

<figure><img src="../.gitbook/assets/Untitled 7 (1).png" alt=""><figcaption></figcaption></figure>

Tener en cuenta que _blockDim.x_ debería ser ≥ 32 correspondiente al tamaño del Warp.

Con la imagen anterior, **tenemos que considerar casos en los que existe un mayor número de hebras que de tareas por realizar**, por ejemplo:

<figure><img src="../.gitbook/assets/Untitled 8 (1).png" alt=""><figcaption></figcaption></figure>

**En estos casos, habría que asegurarnos que el índice obtenido $i\_{x}$ es menor al número de datos.**

#### 1.3.2. Asignación de memoria

Veremos la forma en la que asignar memoria y liberarla tanto para CPU como para la GPU. Para ello, utilizaremos las funciones `cudaMallocManaged()` y `cudaFree()`.

Por ejemplo:

```c
// Sólo para CPU

// 2 ^ 21
int N = 2<<20;
size_t size = N * sizeof(int);

int *a;
a = (int *)malloc(size);

// Liberar memoria
free(a);

// Acelerado con GPU y CUDA

int N = 2<<20;
size_t size = N * sizeof(int);

int *a;

cudaMallocManaged(&a, size);

cudaFree(a);
```

Gracias al avance en Hardware se han conseguido mayores tasas de transferencia entre la GPU y la CPU así como también mejoras en la fabricación de memorias de ambos componentes. Con ello, junto a las versiones actualizadas de CUDA, podemos compartir datos entre la GPU y CPU utilizando la **memoria unificada**.

<figure><img src="../.gitbook/assets/Untitled 9.png" alt=""><figcaption></figcaption></figure>

La memoria unificada ofrece una serie de ventajas:

* En la parte de programación, otorga un único puntero a los datos para acceder desde la CPU y GPU.
* No requiere utilizar `cudaMemcpy()`.
* Facilita la portabilidad del código.
* Consigue un mayor rendimiento en la migración de datos a la memoria de la CPU o GPU garantizando la coherencia global (el formato de datos y el valor que tienen) además de permitir la optimización manual con `cudaMemcpyAsync()`.

Los tipos de memoria en CUDA son:

<figure><img src="../.gitbook/assets/Untitled 10 (1).png" alt=""><figcaption></figcaption></figure>

Algunas de las consideraciones a tener en cuenta son:

* La máxima cantidad de memoria unificada que puede alojarse es la menor de las memorias que tienen las GPUs.
* La memoria unificada tocada por la CPU debe migrar de vuelta a la GPU antes de lanzar el Kernel.
* La CPU no puede acceder a la memoria unificada mientras la GPU esté ejecutando por lo que debemos llamas a la función `cudaDeviceSynchronize()` antes de permitir a la CPU acceder a la memoria unificada.
* La GPU tiene acceso exclusivo a la memoria unificada mientras se esté ejecutando un Kernel, aunque éste no toque la memoria unificada.

Podemos resumir el proceso de la memoria unificada con la siguiente imagen:

<figure><img src="../.gitbook/assets/AB407146-6A59-4476-A97F-B0D7BF2AA8CC.jpeg" alt=""><figcaption></figcaption></figure>

A continuación, veremos un ejemplo de acceso a memoria donde existen restricciones de uso de la memoria.

Este no funciona:

```c
__device__ __managed__ int x, y = 2; // Memoria unificada

__global__ void mykernel() // Territorio GPU
{
	x = 10;
}

int main() // Territorio CPU
{
	mykernel <<<1,1>>> ();
	y = 20; // ERROR: Acceso desde CPU concurrente con GPU

	return 0;
}
```

Este sí funciona. Existe una sincronización entre la GPU y la CPU donde los datos migran un procesador a otro:

```c
__device__ __managed__ int x, y = 2; // Memoria unificada

__global__ void mykernel() // Territorio GPU
{
	x = 10;
}

int main() // Territorio CPU
{
	mykernel <<<1,1>>> ();
	cudaDeviceSynchronize();
	y = 20; 

	return 0;
}
```

Tener en cuenta que podemos clonar estructuras sin memoria unificada pero habría que crear copias sucesivas entre la CPU y la GPU. También se puede hacer con memoria unificada pero se ha de usar C++.

#### 1.3.3. Manejo de desajustes en la configuración del Kernel

Puede existir el caso de que no se pueda expresar una configuración de ejecución de un Kernel con el número exacto de hilos necesarios para paralelizar un bucle.

Un caso muy común viene con el deseo de elegir tamaños de bloque óptimos. Por ejemplo, debido a las características del hardware de la GPU, los bloques que contienen un número de hilos que es un múltiplo de 32 otorgan aplicaciones con mejor rendimiento.

Por ejemplo, si queremos lanzar bloques de 256 hilos (múltiplo de 32), y necesitamos ejecutar 1000 tareas paralelas, entonces no hay ningún número de bloques que produzca un total exacto de 1000 hilos en la malla, ya que no hay ningún valor entero por el que se pueda multiplicar 32 y que sea exactamente 1000.

Estos casos se pueden abordar de diferentes maneras:

1. Crear más hilos de los necesarios.
2.  Pasar un parámetro como argumento del Kernel a utilizar con el fin de indicar el tamaño total del conjunto de datos o el total de hilos necesarios que van a realizar la tarea.

    ```c
    // Si conocemos N
    int N = 100000;

    // Dejamos un valor fijo de hebras por bloque múltiplo de 32
    size_t num_hebras_bloque = 256;

    size_t num_bloques = (N + num_hebras_bloque - 1) / num_hebras_bloque ;

    some_kernel<<<num_bloques, num_hebras_bloque>>>(N);
    ```
3.  Después de calcular el índice las hebras con la función $i\_{x}=(blockIdx.x \cdot blockDim.x)+threadIdx.x$ indicar con un `if()` que el índice no supere el número total de datos.

    ```c
    __global__ some_kernel(int N)
    {
    	int i = (blockIdx.x * blockDim.x) + threadIdx.x;
    	
    	if (i < N)
    	{
    		// Solo hace el trabajo necesario
    	}
    }
    ```

#### 1.3.4. Kernels con gran tamaño de datos

En el caso de que nos encontremos con una gran cantidad de datos que supere al número máximo de hebras, realizaríamos divisiones de los datos para ajustar al número de hebras disponibles. Tras finalizar sus tareas, realizaríamos un salto a la siguiente división de los datos con la expresión:

$$
blockDim.x \cdot gridDim.x
$$

Para ello, programaremos el siguiente bucle:

```c
__global__ void kernel(int *a, int N)
{
    int indexWithinTheGrid = (blockIdx.x * blockDim.x) + threadIdx.x;
    int gridStride = gridDim.x * blockDim.x;
    
    for (int i = indexWithinTheGrid; i < N; i += gridStride)
    {
    
    }
}
```

#### 1.3.4. Manejo de errores con CUDA

Muchas de las funciones de CUDA devuelven un valor que permite indicar si se ha producido o no un error siendo muy útil para el manejo de errores.

A continuación, veremos un ejemplo gestionando errores a la hora de reservar memoria:

```c
cudaError_t err;
err = cudaMallocManaged(&a, N)              

// cudaSuccess, es proporcionado por CUDA
// cudaGetErrorString(), también es proporcionado por CUDA
if (err != cudaSuccess)  
{
    printf("Error: %s\n", cudaGetErrorString(err)); 
}
```

Para el caso del lanzamiento de Kernel donde el tipo de función es `void()` usaremos `cudaGetLastError()` que devuelve un valor de tipo `cudaError_t`. Por ejemplo:

```c
// -1, no es un valor válido para el número de hebras por bloque
someKernel<<<1, -1>>>();
cudaError_t err;

err = cudaGetLastError(); 

if (err != cudaSuccess)
{
    printf("Error: %s\n", cudaGetErrorString(err));
}
```

O podemos utilizar una función similar a la siguiente:

```c
#include <stdio.h>
#include <assert.h>

inline cudaError_t checkCuda(cudaError_t result)
{
	if (result != cudaSuccess) 
	{
		fprintf(stderr, "CUDA Runtime Error: %s\n", cudaGetErrorString(result));
		assert(result == cudaSuccess);
	}

	return result;
}

int main()
{
	checkCuda(todas_las_funciones_a_gestionar_errores);
}
```

### 1.4. Kernels característicos

Previamente a ver los operadores tenemos que _definir un bucle forall:_

> Un bucle _forall_ es un bucle for que no cuenta con independencias. Independientemente del índice por lo que empieza el resultado no se ve alterado.

Tenemos diferentes tipos de operadores:

*   Operadores streaming: constituyen la expresión más simple de un bucle _forall._ CUDA aprovecha todo el paralelismo utilizando tantos hilos como sean necesarios.

    En el ejemplo siguiente podríamos crear tantos hilos como píxeles para que cada uno se encargue de una sola iteración (paralelismo de grano fino):

    ```c
    #define N 1920 * 1080

    float r[N], g[N], b[N], lumincancia[N];

    for(int i = 0; i < N; i++)
    {
    	luminancia[i] = 255 * (0.2999 * r[i] + 0.587 * g[i] + 0.114 + b[i])
    }
    ```
*   Operadores sobre vectores: ora expresión típica de un bucle _forall._ Aquí, declararíamos un hilo CUDA por cada iteración del bucle para aprovechar al máximo paralelismo y escalabilidad.

    Por ejemplo:

    ```c
    #define N (1 << 30)

    float a[N], b[N], c[N];

    for(int i = 0;i < N; i++)
    {
    	c[i] = a[i] + b[i];
    }
    ```
*   Operadores patrón (stencil operators): las iteraciones del bucle externo deben serializarse debido a la presencia de dependencias pero podemos explotar todo el paralelismo para cada partícula. La carga computacional depende del número de iteraciones.

    Todos los hilos deben sincronizarse entre asignaciones.

    ```c
    int i, j, iter, N, Niters;	

    float in[N][N], out[N][N];	

    for (iter = 0; iter < Niters; iter++)	
    {	
    	for (i = 1; i< N-1; i++)
    	{
    		for (j = 1; j < N - 1; j++)
    		{
    			out[i][j] = 0.2	* (in[i][j] + in[i-1][j] + in[i+1][j] + in[i][j-1] + in[i][j+1]);	
    		}
    	}	
    			
    	for (i = 1; i < N - 1; i++)
    	{
    		for (j = 1; j < N - 1; j++)
    		{
    			in[i][j] = out[i][j];
    		}	
    	}	
    }
    ```

    Del ejemplo anterior, el paralelismo depende del tamaño de la matriz 2D ($N^2$).
*   Operadores de reducción: el código tiene dependencias entre las iteraciones, pero el paralelismo puede explotar la asociativadad del operador para desplegar paralelismo en forma de árbol binario, resultando en $log(N)$ pasos que van reduciendo el grado de paralelismo a la mitad hasta concluir con un solo hilo. El reto está en utilizar el patrón de acceso a memoria que explota mejor la jerarquía de memoria de la GPU.

    ```c
    float sum, x[N];	

    sum = 0;	

    for (i = 0; i < N; i++)
    {
        sum += x[i];
    }
    ```

<figure><img src="../.gitbook/assets/Untitled 11 (1).png" alt=""><figcaption></figcaption></figure>

*   Histogramas: veremos un ejemplo:

    ```c
    int histo[Nbins], image[N][N];	

    sum = 0;	

    for (i = 0; i < Nbins; i++)
    {
    	histo[Nbins] = 0;	
    }

    for (i = 0; i < N; i++)
    {
    	for (j = 0; j < N; j++)
    	{
    		histo[image[i][j]]++;
    	}
    }
    ```

    El primer bucle _for_ apenas tiene carga computacional. Los dos bucles siguientes tienen dependencias, pero los valores de `image[][]` se pueden leer en paralelo si los asignamos a hilos CUDA. A partir de ahí, CUDA proporciona operaciones atómicas (`atomicInc(histo[image[i][j]])`) para serializar accesos concurrentes al vector `histo[]` y que usaremos aquí para prevenir condiciones de carrera.

Como análisis final tenemos:

<figure><img src="../.gitbook/assets/Untitled 12.png" alt=""><figcaption></figcaption></figure>

* El operador streaming es el que más acelera en GPU.
* El operador patrón es el que mejor aprovecha la memoria compartida.
* El operador de reducción depende más del programador.
* El histograma supone el mayor reto para el programador.

## Tema 2: Acelerar aplicaciones con CUDA, Python, Numba y CuPy

### 2.1. Numba

#### 2.1.1. Introducción

Numba es un compilador para Python que permite ejecutar en la GPU o CPU código de NumPy, funciones y bucles haciendo una conversión a código máquina sin utilizar el interprete de Python, mejorando así los tiempos de ejecución de un programa. La manera más sencilla de usar Numba es mediante sus decoradores que se aplican en el código directamente para que Numba los compile. Dicha compilación se hace en tiempo de ejecución.

> **IMPORTANTE:** actualmente Numba **NO ES COMPATIBLE** con Pandas → Opciones:
>
> * Convertir DataFrames de Pandas en matrices de NumPy o CuPy.

#### 2.1.2. Decoradores

| Decoradores                   | Definición                                                                                                                                                                                                                                               |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| @jit                          | Compilación en modo objeto. Numba reconoce los bucles que pueden ser compilados en código máquina y compilará el resto de la función con el interprete de Python.                                                                                        |
| @njit = @jit(nopython = True) | Se obtiene el mejor rendimiento ya que se compila la función sin utilizar el interprete de Python, aunque dependiendo de los parámetros a procesar dará fallos en la compilación. En caso de fallo, utilizar @jit. Esta es la primera opción a utilizar. |
| @njit(parallel = True)        | Si el código realiza operaciones que se pueden paralelizar y son soportadas, Numba realizará una compilación para ejecutar el código en múltiples hilos de la GPU.                                                                                       |
| @njit(fastmath = True)        | Permite reducir la precisión de los datos realizando cálculos más rápidos.                                                                                                                                                                               |

Tener en cuenta que los decoradores anteriores se pueden combinar entre sí, por ejemplo:

```python
@njit(parallel = True, fastmath = True)
```

Con el decorador anterior, estaríamos utilizando la compilación directa de `njit` evitando utilizar el interprete de Python además de estar paralelizando el código (`parallel = True`) y reduciendo la precisión numérica (`fastmath = True`) para reducir aún más el coste en tiempo.

#### 2.1.3. Ejemplos de código

```python
from numba import jit
import numpy as np

# Cambiar por cualquier otro decorador dependiendo de lo necesitado
@jit(nopython = True)
def bucle(lista1, lista2, num_filas):
	
	lista3 = []

	for fila in num_filas:
		
		if (lista1[fila] >= 1) && (lista2[fila] <= 5):
			
			lista3.append(np.mean(lista[fila], lista2[fila])) 
```

### 2.2. Cupy
