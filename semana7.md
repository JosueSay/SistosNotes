
# 🧠 Calendarización de Procesos

## ¿Qué es calendarización?

Es el proceso de decidir **a qué proceso se le asigna un recurso**, como la CPU, RAM o disco.  
Se puede aplicar **prioridad** basada en **la jerarquía de memoria**:

- Procesos más cercanos al CPU (RAM) → **más prioridad.**
- Procesos en disco (memoria secundaria) → **menos prioridad.**

## ⏳ Tipos de Calendarización

| Tipo        | Nivel          | Encargado                         | Ejemplo                        |
|-------------|----------------|-----------------------------------|--------------------------------|
| **Largo plazo (LP)** | Admisión | Job Scheduler                    | Sistemas batch (uso de disco)  |
| **Mediano plazo (MP)** | Memoria | Memory Scheduler                | Control del grado de multiprogramación |
| **Corto plazo (CP)** | CPU       | CPU Scheduler                    | Procesos en RAM listos para CPU |

## 📊 Ambientes de ejecución

- **Batch systems:** maximizar throughput y uso de CPU.
- **Sistemas interactivos:** minimizar tiempo de respuesta.
- **Tiempo real:** garantizar ejecución dentro de tiempos límite.

## 🔁 Comportamiento de procesos

Los procesos alternan entre:

- **CPU bursts** (ejecutan)
- **I/O bursts** (esperan)

Tipos:

- **CPU-bound:** hacen más trabajo en CPU.
- **I/O-bound:** esperan más por entradas/salidas.

> El scheduler intenta predecir el comportamiento usando bursts anteriores.

## 🧭 Decisiones de calendarización

- Al **terminar un proceso**.
- Al **bloquearse** por I/O.
- Al **crear un nuevo proceso**.
- Por **interrupciones** (reloj, I/O).

### Tipos

- **Preemptive:** permite interrupciones (interactivos).
- **Non-preemptive:** no interrumpe (batch).

## 🎯 Criterios de evaluación

| Criterio          | Qué mide                                     | Relevancia en…           |
|-------------------|-----------------------------------------------|---------------------------|
| **Tiempo de respuesta** | Desde solicitud hasta primera respuesta       | Interactivos              |
| **Tiempo de completación** | Desde solicitud hasta finalización           | Batch systems              |
| **Uso del CPU**     | % del tiempo en uso                        | Todos                     |
| **Throughput**      | Procesos completados por unidad de tiempo  | Todos                     |
| **Tiempo de espera** | Tiempo en la ready queue                   | Afecta usabilidad         |
| **Previsibilidad**  | Que la carga no afecte la duración de tareas | Tiempo real               |

## ⚙️ Algoritmos de Calendarización

### 1. **First Come First Served (FCFS)**

- Cola FIFO.
- Justo pero favorece procesos largos y CPU-bound.
- **No preemptive.**

### 2. **Shortest Job First (SJF)**

- Selecciona el proceso más corto.
- **No preemptive.**
- Requiere conocer duración del proceso.
- Riesgo de **starvation**.

### 3. **Shortest Remaining Time (SRT)**

- Variante preemptive de SJF.
- Mejora tiempos de completación.
- También puede causar starvation.

### 4. **Round Robin (RR)**

- Asigna un **quantum** fijo.
- Procesos rotan como en una **cola circular**.
- **Preemptive.**
- Quantum balanceado es clave:
  - Muy grande → se comporta como FCFS.
  - Muy pequeño → demasiado cambio de contexto.

### 5. **Calendarización por Prioridades**

- Se asignan prioridades numéricas.
- Puede ser **preemptive o non-preemptive.**
- Riesgo de starvation → se mitiga con **envejecimiento** (aging).

## 🪜 Cola Multinivel

- Cola dividida en **varias categorías de procesos.**
- Cada cola puede tener su propio algoritmo.
- Con **prioridades estáticas** o **con retroalimentación** (suben o bajan de nivel según comportamiento).

### Ejemplo

- Q0: RR con quantum 8ms.
- Q1: RR con quantum 16ms.
- Q2: FCFS.

## 🎰 Algoritmos adicionales

### 📌 Lotería

- Se asignan “tickets”.
- Se sortea el CPU.
- Se puede ajustar la prioridad dando más tickets a ciertos procesos.

### 📌 Fair Share

- Asigna CPU según el **usuario**, no proceso.
- Cada usuario recibe un porcentaje fijo, sin importar el número de procesos.

## 🧩 Multiprocesadores y Multinúcleo

### Multiprocesamiento

- **Asimétrico:** un procesador coordina.
- **Simétrico (SMP):** todos ejecutan y coordinan tareas.

### Multinúcleo

- OS los ve como **procesadores lógicos**.
- Permiten **hyper-threading** (múltiples hilos por núcleo).
- Reducen **memory stalls** (espera por memoria).

## 🧠 Calendarización multinúcleo

Dos niveles:

1. OS asigna hilos de software a hilos de hardware.
2. Cada núcleo ejecuta sus propios hilos.

### Granularidad del multithreading

- **Gruesa:** cada thread usa su propio pipeline.
- **Fina:** se intercalan ciclos de ejecución entre hilos.

## 📌 Afinidad de CPU

Permite **ligar un proceso a un núcleo específico.**

### Ventajas

- Reducción de problemas de caché.
- Mejora el rendimiento en tareas intensas como edición de video.

## ⚖️ Balanceo de carga

Reparte trabajo entre procesadores.

### Tipos

- **Push:** chequea periódicamente y redistribuye carga.
- **Pull:** un CPU inactivo toma carga de uno ocupado.

⚠️ Contrario a la afinidad, ya que intenta **mover procesos libremente.**

## ✅ Resumen

- La calendarización decide **qué proceso se ejecuta y cuándo.**
- Existen diferentes algoritmos y enfoques, según el **tipo de sistema**.
- El objetivo siempre es lograr un **equilibrio entre eficiencia, justicia y rendimiento.**
