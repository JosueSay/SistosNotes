# THREADS - Apuntes Completos

## ¿Qué es un hilo?

Un **hilo (thread)** es una secuencia de ejecución dentro de un proceso.  
Es parecido a un proceso, pero comparte el mismo espacio de memoria y recursos del sistema.

### Diferencias clave

- **Proceso:** espacio de memoria separado.
- **Hilo:** comparte memoria con otros hilos del mismo proceso.

## Beneficios de los threads

- **Responsividad:** siguen funcionando aunque haya operaciones bloqueantes.
- **Recursos compartidos:** no se necesita paso de mensajes entre hilos.
- **Escalabilidad:** mayor número de operaciones por unidad de tiempo.
- **Modularidad:** más fácil dividir tareas.
- **Eficiencia:** crear/matar threads es más rápido que con procesos.

## Estados de un hilo

- **Creado**
- **Desbloqueado**
- **Bloqueado**
- **Terminado**

> ⚠️ Si un hilo se bloquea, puede bloquear al resto del proceso.

## Threads de Kernel vs. Usuario

| Característica      | Kernel                            | Usuario                          |
|---------------------|-----------------------------------|----------------------------------|
| Gestión             | Sistema Operativo                 | Aplicación                       |
| Paralelismo         | Sí                                | No necesariamente                |
| Cambio de contexto  | Costoso                           | Ligero                           |
| Control             | OS controla planificación         | Aplicación controla              |

## Terminología: LWP vs procesos

- **LWP (Lightweight Process):** otro nombre para los hilos del kernel.
- **Heavyweight Process:** proceso tradicional.

## Modelos de Multithreading

### 1. Uno a Muchos (1:N)

- Varios hilos de usuario sobre un solo hilo de kernel.
- No hay paralelismo real.
- Ejemplo: GNU Portable Threads.

### 2. Uno a Uno (1:1)

- Cada hilo de usuario tiene su hilo de kernel.
- Mayor concurrencia.
- Ejemplo: Pthreads en Linux, MFC en Windows.

### 3. Muchos a Muchos (M:N)

- Varios hilos de usuario mapeados a varios hilos de kernel.
- Teóricamente ideal, pero con overhead considerable.
- Ejemplo: Windows UMS.

## Scheduler Activations

Mecanismo de planificación eficiente para sistemas multiprocesador.

**Fases:**

1. **Inicialización:** se asignan hilos a núcleos.
2. **Asociación:** cada hilo se vincula con un planificador.
3. **Planificación local:** cada núcleo decide sobre sus propios hilos.
4. **Planificación cooperativa:** núcleos se ayudan entre sí.
5. **Minimización de sincronización:** menos cuellos de botella.
6. **Adaptación dinámica:** decisiones según carga.

## Multithreading en sistemas multinúcleo

### Problemas a resolver

- **Repartir tareas:** identificar subtareas paralelizables.
- **Balanceo de carga:** uso eficiente de los núcleos.
- **Separación de datos:** evitar conflictos.
- **Dependencias:** sincronización adecuada.
- **Testing/debugging:** más complejo por la concurrencia.

## Tipos de paralelismo

- **Paralelismo de datos:** mismas operaciones en datos diferentes.
- **Paralelismo de tareas:** distintas operaciones en los mismos datos.

**Ejemplo:**  
Intel Hyper-Threading permite que un núcleo maneje múltiples hilos.

## Ley de Amdahl

**Fórmula:**  
La aceleración máxima depende de qué porcentaje del código es paralelizable.

- Si el 90% es paralelizable, el 10% limita la ganancia.
- Incluso con 100 procesadores, el 10% secuencial limita el speedup.

## Thread-Local Storage (TLS)

Cada hilo puede tener su propia área privada de datos.  
**Ejemplo:** `__thread int var;` en Pthreads.

## Librerías de Threads

- **Windows:** nivel kernel.
- **Pthreads:** estándar POSIX (puede ser user/kernel).
- **Java Threads:** dependen del sistema operativo.

## Estrategias de creación de hilos

- **Asincrónica:** el proceso sigue su ejecución después de lanzar hilos.
- **Sincrónica:** el proceso espera a que terminen los hilos.

## Threads en Linux

- Linux usa `tasks`, representadas por estructuras `task_struct`.
- **`fork()`**: copia el proceso.
- **`clone()`**: permite compartir recursos, se usa para threads.
- Cada thread tiene:
  - ID, registros, pila de usuario y kernel, TLS.

## Threads en Windows

Similares a los de Linux, con su propio contexto, ID y pilas.

## Threads en Python

Uso de la clase `Thread` con una función y argumentos.  
Ejemplo básico de concurrencia, pero sin paralelismo real por el GIL.

## Threading Implícito

Hilos gestionados automáticamente por compiladores/librerías.

### Ejemplos

- **Thread Pools:** conjunto de hilos pre-creados.
- **OpenMP:** directivas para dividir loops (`#pragma omp parallel`).
- **Grand Central Dispatch (GCD):** gestión automática de tareas (Apple).

## Thread Pool

- Hilos se reutilizan desde un “banco” de threads.
- **Ventajas:**
  - Menor overhead.
  - Control de cantidad de hilos.
  - Mejor separación de lógica y ejecución.

## OpenMP

Directivas para paralelizar código en C/C++/Fortran.  
**Ejemplo:**

```c
#pragma omp parallel for
for (int i = 0; i < N; i++) {
  c[i] = a[i] + b[i];
}
```

## Grand Central Dispatch (GCD)

API de Apple para ejecutar tareas concurrentes fácilmente.  
Asigna tareas a hilos de forma automática y eficiente.

## Precauciones en multithreading

### fork() y exec()

- `exec()` reemplaza todos los hilos.
- `fork()` solo copia el hilo que lo ejecuta (en POSIX).

### Señales (signals)

- **Sincrónicas:** regresan al hilo que las provoca.
- **Asincrónicas:** pueden llegar a varios hilos.

### Cancelación de threads

- **Asincrónica:** el hilo muere inmediatamente.
- **Diferida:** el hilo verifica si debe terminar.

Funciones:

```c
pthread_setcancelstate()
pthread_cancel()
pthread_testcancel()
pthread_cleanup_push()
pthread_cleanup_pop()
```
