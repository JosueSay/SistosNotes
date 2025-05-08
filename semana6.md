# Proceso de Sincronización

## 🧠 Conceptos básicos

### Productor-Consumidor

El modelo clásico usa una **cola circular** con dos punteros:

- `in`: indica dónde insertar (productor).
- `out`: indica dónde sacar (consumidor).

#### Problemas comunes

- `in == out`: la cola está vacía.
- `out > in`: se accede a datos no válidos → error.

La concurrencia causa errores si ambos acceden al mismo recurso sin control.

## ⚠️ Race Conditions

Una **race condition** ocurre cuando el resultado depende del **orden de ejecución** de procesos concurrentes sobre datos compartidos.

### Ejemplo

```c
// counter = 5 originalmente
register1 = counter;      // 5
register1 = register1 + 1;// 6
register2 = counter;      // 5 (aún)
register2 = register2 - 1;// 4
counter = register1;      // 6
counter = register2;      // 4 ← ERROR!
```

### Caso real

**Therac-25**, una máquina de radiación, causó muertes debido a race conditions.

## 🧩 Problemas con la concurrencia

- Los procesos comparten recursos (RAM, CPU), pero deben evitar interferencias.
- El acceso no controlado puede alterar resultados.
- Esto se soluciona con mecanismos de **sincronización de procesos**.

## 🔄 Tipos de interacción entre procesos

- **Cooperación:** comunicación y coordinación (e.g. shared memory).
- **Competencia:** varios procesos quieren el mismo recurso.

### Problemas

- **Starvation:** un proceso nunca accede al recurso.
- **Deadlock:** procesos se bloquean mutuamente esperando recursos del otro.

## 🔐 Sección crítica

Una **sección crítica** es el bloque de código donde un proceso accede a un recurso compartido.

### Reglas

1. Solo un proceso puede estar en la sección crítica.
2. Los demás deben esperar.
3. Requiere un **protocolo de entrada y salida** (entry/exit section).

### Propiedades deseables

- **Exclusión mutua**
- **Progreso**
- **Espera limitada (bounded waiting)**

## ⚙️ Tipos de Kernel

- **Preemptive:** puede interrumpir un proceso para dar paso a otro.
- **Non-preemptive:** el proceso decide cuándo ceder.

## 🧱 Sincronización a nivel de hardware

### Instrucciones atómicas

Son operaciones que **no pueden ser interrumpidas**, base para mecanismos como los **locks**.

### Lock (bloqueo)

Solo el que posee el lock entra a la sección crítica.

#### Problemas

- **Busy waiting:** el proceso espera en un bucle.
- **Starvation/Deadlock**: si el lock no se libera.

## 🔒 Mutex Locks

Un **mutex lock** es una variable compartida que protege regiones críticas.

### Ejemplo con busy waiting (spinlock)

```c
acquire() {
  while (!available); // espera activa
  available = false;
}

release() {
  available = true;
}
```

En sistemas multiprocesador puede ser eficiente si el tiempo de espera es corto.

## ⚠️ Inversión de prioridades

### Problema

Un proceso de baja prioridad tiene un recurso que necesita uno de alta, pero es interrumpido por uno de prioridad media.

### Ejemplo real

**Mars Pathfinder** (NASA) experimentó errores debido a este fenómeno.

### Solución

**Herencia de prioridades:** el proceso de baja prioridad recibe temporalmente la prioridad alta.

## 🟢 Semáforos

Estructura con un entero `S`:

- **Binario:** actúa como mutex (0 o 1).
- **Contador:** representa múltiples recursos disponibles.

### Operaciones

```c
wait(S) {
  while (S <= 0); // busy wait
  S--;
}

signal(S) {
  S++;
}
```

## 🚫 Sin busy waiting

Los semáforos se implementan con una cola de espera:

```c
typedef struct {
  int value;
  struct process *list;
} semaphore;

wait(semaphore *S) {
  S->value--;
  if (S->value < 0) {
    add this process to S->list;
    block();
  }
}

signal(semaphore *S) {
  S->value++;
  if (S->value <= 0) {
    remove process from list;
    wakeup(process);
  }
}
```

## 🧩 La realidad de los semáforos

- No resuelven completamente el problema de sección crítica.
- Introducen un “mini” critical section dentro de `wait` y `signal`.
- Mal uso → deadlock o starvation.

## 🧭 Monitores

**Abstracción de alto nivel** para sincronización (tipo clase).

### Propiedades

- Exclusión mutua garantizada.
- Gestión automática de espera/continuación.

```cpp
monitor Ejemplo {
  procedure operacion() { ... }
  initialization_code() { ... }
}
```

## ⏳ Variables de condición

Se usan dentro de monitores para suspender/reanudar procesos.

### Operaciones

- `x.wait()` → suspende proceso actual.
- `x.signal()` → despierta uno que hizo `x.wait()`.

## 🗓️ Calendarización dentro de monitores

Se puede usar prioridad como argumento:

```cpp
x.wait(prioridad)
```

El proceso con **menor prioridad numérica** se ejecuta primero.

## 🤖 Ejemplo de uso de monitor

```cpp
R.acquire(t); // t = tiempo planeado de uso
... // uso del recurso
R.release();
```

`R` es un monitor que asigna el recurso con base en prioridad temporal.

## 🔧 Pthreads y sincronización

Pthreads ofrece:

- **Mutexes**
- **Variables de condición**

Mecanismos portables para sincronización entre hilos a nivel usuario.

## 🧪 Problemas clásicos de sincronización

### 1. **Bounded-Buffer Problem**

Productores insertan datos en un buffer limitado.  
Consumidores extraen datos.

#### Solución

- Semáforo `mutex` (acceso).
- Semáforo `empty` (espacios disponibles).
- Semáforo `full` (espacios ocupados).

### 2. **Readers-Writers Problem**

Múltiples procesos leen/escriben un recurso compartido (e.g. base de datos).

#### Variaciones

- **Prioridad para lectores:** evita bloquear lectura innecesaria.
- **Prioridad para escritores:** garantiza actualizaciones oportunas.

Ambas pueden generar starvation.

### 3. **Dining-Philosophers Problem**

Filósofos necesitan 2 tenedores para comer.  
Pueden quedarse esperando indefinidamente → deadlock/starvation.

#### Solución

- Uso controlado de recursos (monitores, semáforos, etc).

## ✅ Conclusión

La sincronización es vital para evitar errores en programas concurrentes.  
Se usan herramientas como:

- Mutex
- Semáforos
- Monitores
- Instrucciones atómicas

Pero deben usarse correctamente para evitar nuevos problemas (como deadlocks o starvation).
