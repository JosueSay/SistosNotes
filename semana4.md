# 📝 Proceso en Sistemas Operativos

## ✨ Definición de Proceso

Un **proceso** es un programa en ejecución que se encuentra en un estado definido dentro de la memoria del sistema operativo. Se puede considerar como una unidad fundamental del sistema operativo, ya que gestiona el uso del CPU y la memoria.

Conceptualmente, un proceso opera como si tuviera su propio CPU, ejecutándose en un contexto aislado.

### 🖥️ **¿Qué es un proceso?**

Imagina que una computadora es como una oficina con muchas tareas diferentes que hacer al mismo tiempo.

Un **proceso** es como un empleado en esa oficina. Cada empleado (proceso) tiene su propia tarea específica que debe realizar, como escribir un informe o responder correos electrónicos.

### ⚙️ **¿Cómo funciona un proceso?**

Cada proceso en la computadora **cree** que tiene su propio "escritorio de trabajo" (CPU) y que es el único que está ejecutándose. Pero en realidad, la computadora **cambia rápidamente** entre procesos, dándoles un poco de tiempo para ejecutarse antes de pasar al siguiente.

### 🔒 **¿Qué significa “contexto aislado”?**

Cada proceso **no puede ver ni afectar directamente** a otros procesos. Es como si cada empleado tuviera su propio cubículo con sus propios documentos y no pudiera espiar lo que hacen los demás. Si necesitan compartir información, deben usar métodos especiales (como mensajes o archivos compartidos).

### 📌 **Ejemplo simple**

Piensa en una computadora con dos procesos:

1. Un navegador de internet que carga una página.
2. Un programa de música que está reproduciendo una canción.

Cada uno **cree** que está usando el CPU exclusivamente, pero la computadora está alternando entre ambos muy rápido para que parezca que se ejecutan al mismo tiempo.

### 📚 Características principales

- **Instrucciones**: Define el código del programa.
- **Estado**: Indica en qué fase del ciclo de vida se encuentra el proceso.
- **Direcciones de memoria**: Espacios en la memoria asignados al proceso.

Incluso, **dos procesos distintos pueden estar asociados al mismo programa**, ejecutándose de forma independiente.

### 📝 Partes de la memoria

1. **Text**:
   - Es la sección donde se guarda el **código del programa** (las instrucciones que debe ejecutar el CPU).
   - Ejemplo: Si el programa tiene una línea de código que dice `a = 5`, aquí se guarda la instrucción para realizar esa operación.

2. **Data**:
   - Contiene las **variables globales** y datos inicializados del programa.
   - Ejemplo: Si declaraste una variable global como `int x = 10;`, se almacena aquí.

3. **Heap**:
   - Es un área de memoria **dinámica**. Aquí se guarda la memoria que el programa pide mientras está ejecutándose.
   - Ejemplo: Si usas `malloc()` o `new` en C o C++, los datos se almacenan en el heap.
   - **Crecimiento:** Aumenta hacia arriba.

4. **Stack**:
   - Aquí se guardan las **variables locales** de las funciones y la información necesaria para volver a la función anterior.
   - Ejemplo: Si en una función declaras una variable `int y = 3;`, se guarda en el stack.
   - **Crecimiento:** Baja hacia abajo.

![Proceso](../images/proceso.png "Proceso")

---

### 🔄 **Interacción entre el Stack y el Heap**

- **Zona azul**: El **heap** y el **stack** crecen en direcciones opuestas.
  - El **heap** crece hacia arriba cuando solicitas más memoria.
  - El **stack** crece hacia abajo cuando llamas más funciones o guardas más datos locales.
  - **Límite**: Si ambos se encuentran, puede ocurrir un error llamado *desbordamiento de memoria* (*stack overflow* o *heap overflow*).

### **Desbordamiento de memoria (Stack Overflow o Heap Overflow)**

1. **¿Qué es?**  
   Ocurre cuando una de las áreas de memoria (el **stack** o el **heap**) intenta ocupar más espacio del permitido y termina invadiendo el espacio de la otra, o se queda sin espacio en general.

   **Ejemplo simple del stack (Stack Overflow):**
   - Si un programa llama demasiadas funciones sin terminar las anteriores (como en una recursión infinita), el **stack** sigue creciendo hacia abajo hasta que no puede crecer más. Esto genera un *error de stack overflow*.

   **Ejemplo simple del heap (Heap Overflow):**
   - Si un programa pide demasiada memoria dinámica (como usando `malloc()` en C) sin liberar memoria, el **heap** sigue creciendo hacia arriba hasta que no hay más espacio. Esto se llama *heap overflow*.

   En ambos casos, el programa falla porque la memoria no puede crecer indefinidamente.

---

### **¿Qué significan el 0 y max en la imagen?**

- **0 (cero):**  
   Representa el inicio de la memoria del proceso. Este número no es literal "cero" en el hardware real, pero conceptualmente, el sistema operativo lo organiza como el punto inicial donde empieza la memoria asignada para ese proceso.

- **max (máximo):**  

   Representa el límite superior de la memoria que el sistema operativo ha reservado para el proceso. Este límite depende de varios factores:

  - La cantidad de memoria RAM disponible.
  - El sistema operativo y su configuración.
  - El tipo de programa (por ejemplo, programas de 32 bits tienen límites más bajos que los de 64 bits).

---

### **¿Quién pone estos límites?**

- El **sistema operativo (SO)** se encarga de reservar y gestionar la memoria para cada proceso.

  - Cuando un programa se ejecuta, el SO le asigna un rango de memoria, con un inicio (**0**) y un límite (**max**), para que el proceso no interfiera con otros procesos.
  - Si el programa intenta usar más memoria de la que tiene asignada, el sistema operativo detiene el proceso y genera un error.

### **Ejemplo con vocales**

#### **Configuración inicial de la memoria con vocales**

Imagina que las vocales representan el espacio de memoria que tiene un proceso:

```markdown
A - E - I - O - U
```

- **A**: Inicio de la memoria del proceso.
- **U**: Fin de la memoria asignada por el sistema operativo.
- **E, I, O**: Espacio libre entre el inicio y el final.

Ahora, dividimos esta memoria en regiones:

1. **Sección TEXT (código):**  
   - **A**: Aquí se guardan las instrucciones del programa.
   - Ejemplo: "Suma dos números" o "Llama a una función".

2. **Sección DATA (variables globales):**  
   - **E**: Aquí están las variables globales inicializadas, como `globalVariable = 10`.

3. **Heap (memoria dinámica):**  
   - Comienza **justo después de la sección DATA**, en **I**.
   - Crece hacia adelante, usando más letras conforme se necesita más espacio.

4. **Stack (variables locales y funciones):**  
   - Comienza **cerca del final de la memoria**, en **U**.
   - Crece hacia atrás, ocupando letras hacia las anteriores.

---

#### **Cómo trabajan el stack y el heap**

##### **Caso 1: Estado inicial**

```markdown
A (TEXT) - E (DATA) - I (HEAP) - ... espacio libre ... - U (STACK)
```

1. El **heap** comienza en **I**. Si el programa pide memoria dinámica, el heap irá ocupando más letras hacia **O**.
2. El **stack** comienza en **U**. Si se llama una función, el stack ocupará memoria hacia **O**.

##### **Caso 2: Heap pide más memoria**

El programa solicita memoria dinámica (como `allocate(100)`). El **heap** empieza a usar las siguientes letras:

```markdown
A (TEXT) - E (DATA) - I (HEAP --> O) - ... espacio libre ... - U (STACK)
```

El **heap** avanza hacia **O**, dejando menos espacio libre.

##### **Caso 3: Stack usa más memoria**

El programa llama a varias funciones. Cada función usa variables locales, y el **stack** crece hacia atrás:

```markdown
A (TEXT) - E (DATA) - I (HEAP --> O) - ... STACK (<-- U)
```

El **stack** se mueve hacia **O**, dejando menos espacio libre.

---

#### **¿Qué pasa si chocan?**

1. **Choque del Stack y Heap:**
   - Si el **heap** sigue creciendo hacia **O** y el **stack** sigue creciendo hacia **O**, ambos terminan usando la misma letra.
   - Ejemplo: El **heap** llega a ocupar **O**, y el **stack** también intenta usar **O**.

   Resultado: **Error de memoria (choque)**. El sistema operativo detiene el programa porque las dos partes están usando el mismo espacio.

   Representación del choque:

   ```markdown
   A (TEXT) - E (DATA) - I (HEAP --> O) <-- STACK (U)
   ```

2. **Por qué ocurre el error:**
   - En la vida real, la memoria necesita que cada región esté claramente separada. Si dos regiones intentan usar la misma letra, el sistema operativo no puede determinar qué dato pertenece a quién.

### 🌍 Ejemplo de Componentes en un Programa C

```c
#include <stdio.h>
#include <stdlib.h>

int global_var = 10;  // Sección de datos

void funcion() {
    int local_var = 5; // Pila
    printf("Valor local: %d\n", local_var);
}

int main() {
    funcion();
    int *ptr = (int*) malloc(sizeof(int)); // Heap
    *ptr = 20;
    printf("Valor en Heap: %d\n", *ptr);
    free(ptr);
    return 0; // Sección de texto
}
```

---

## 🌟 Estados de un Proceso

### 📗 Ciclo de Vida de un Proceso

Un proceso pasa por diferentes estados en su ejecución:

1. **Nuevo**: El proceso se crea pero aún no se ha cargado en memoria.
2. **Listo**: El proceso está en cola, esperando ser ejecutado.
3. **En ejecución**: El proceso tiene un procesador asignado y está corriendo.
4. **Esperando/Bloqueado**: El proceso espera un evento externo para continuar (ejemplo: entrada/salida).
5. **Suspendido**: Ha sido temporalmente detenido por el sistema operativo y se encuentra inactivo.
6. **Terminado**: El proceso ha concluido y está listo para ser eliminado.

![Ciclo de Videa de un Proceso](../images/ciclo_vida_proceso.png "Ciclo de Videa de un Proceso")

![Cilo de Vida Real de un Proceso](../images/ciclo_vida_real_proceso.png "Cilo de Vida Real de un Proceso")

#### 📝 Ejemplo de Estado de Bloqueo

Un proceso entra en **estado bloqueado** cuando espera una operación de entrada/salida (E/S).

Ejemplo en Python:

```python
input("Presiona Enter para continuar...")
```

Este programa permanecerá bloqueado hasta que el usuario presione la tecla "Enter".

#### 🎉 Homología con una Cajera de Supermercado

Imagina una **cajera** en un supermercado:

- **Nuevo**: Se contrata a una cajera.
- **Listo**: La cajera está esperando un cliente en su caja.
- **En ejecución**: Atiende a un cliente.
- **Bloqueado**: Espera que el cliente busque su billetera.
- **Suspendido**: Es enviada a su hora de almuerzo.
- **Terminado**: Termina su turno y se retira a casa.

#### 🔎 Reflexión sobre Suspensión

- **¿Cuándo es útil el estado bloqueado?**
  - Cuando un proceso está esperando una respuesta de un dispositivo externo (ejemplo: impresora).

- **¿Cuándo es útil la suspensión?**
  - Cuando otro proceso de mayor prioridad necesita los recursos actuales.

## 🖥️ **PCB (Process Control Block)**

El **PCB (Bloque de Control de Procesos)** es una estructura fundamental dentro del sistema operativo, encargada de almacenar toda la información necesaria para gestionar la ejecución de un proceso.

![Process Control Block](../images/pcb.png "Process Control Block")

**Descripción de imágen:**

1. **Estado del proceso:** Indica si el proceso está ejecutándose, en espera o detenido.
2. **Número de proceso:** Un identificador único que distingue al proceso en el sistema.
3. **Contador de programa:** Señala la instrucción que está siendo ejecutada actualmente.
4. **Registros:** Incluye el estado actual de los registros del CPU para permitir cambios de contexto.
5. **Límites de memoria:** Especifica el rango de memoria asignado al proceso.
6. **Lista de archivos abiertos:** Archivos que el proceso tiene abiertos actualmente.

Cada proceso en ejecución en un sistema operativo tiene su propio PCB, que contiene datos como:

- **Identificación del proceso (Process ID, PID):** Es un número único que identifica al proceso dentro del sistema. El primer proceso creado es el "proceso raíz" y generalmente tiene el PID 1.
- **Program Counter:** Indica la posición actual de ejecución dentro del código del proceso. Esto es esencial para que el sistema operativo pueda continuar la ejecución después de un cambio de contexto.
- **Límites de memoria:** Define el espacio de memoria asignado al proceso. Un error común es el **"segmentation fault"**, que ocurre cuando un proceso intenta acceder a una zona de memoria no permitida.
- **Lista de archivos abiertos:** Contiene información sobre los archivos a los que el proceso tiene acceso en un momento determinado.

---

### **Cambio de Contexto**

El **cambio de contexto** es el proceso mediante el cual el sistema operativo guarda el estado de un proceso y carga el estado de otro.

![Cambio entre Procesos](../images/cambio_proceso.png "Cambio entre Procesos")

**Descripción de imágen:**

1. El sistema operativo pausa el proceso actual y guarda su estado en el PCB.
2. Selecciona un nuevo proceso y carga su estado desde su PCB.
3. La CPU reanuda la ejecución del nuevo proceso desde donde se pausó.

#### **¿Cómo ocurre un cambio de contexto?**

1. El sistema operativo pausa la ejecución del proceso actual y guarda su estado en su PCB.
2. Se selecciona un nuevo proceso para ejecutar.
3. El estado del nuevo proceso se carga en la CPU.
4. Se reanuda la ejecución del nuevo proceso desde la última instrucción ejecutada.

Este cambio es necesario para permitir la ejecución simultánea de múltiples procesos en un sistema con múltiples núcleos, garantizando un uso eficiente del procesador.

---

### **Creación y Finalización de Procesos**

Cuando un proceso se crea en el sistema operativo, se genera una estructura jerárquica en forma de **árbol**, donde el proceso padre es la raíz y sus procesos hijos dependen de él.

#### **Inicio de un Proceso**

El proceso inicial del sistema operativo (conocido como **init** en UNIX y **systemd** en sistemas modernos) se encarga de la inicialización del sistema.

**Diferencias entre `init` y `systemd`**:

- **init:** Es el sistema de inicio tradicional en UNIX/Linux. Gestiona procesos de forma secuencial.
- **systemd:** Es un reemplazo moderno de `init` que permite iniciar procesos de manera más eficiente y paralela.

---

#### **Finalización de un Proceso**

Un proceso puede terminar de dos formas:

1. **Voluntaria**: Llamando a una syscall como `exit()`, que indica que el proceso ha finalizado su ejecución.
2. **Involuntaria**: Puede ocurrir por errores fatales (como intentos de acceso a memoria inválida) o porque otro proceso con privilegios suficientes lo termina.

**Opciones cuando un proceso padre termina:**

- **Los procesos hijos quedan huérfanos** → Son adoptados por `init` o `systemd`.
- **Terminación en cascada** → Se eliminan también los procesos hijos.

**¿Qué es un proceso zombie?**  
Cuando un proceso hijo termina antes de que su padre lo espere, se convierte en un **proceso zombie**, ocupando una entrada en la tabla de procesos hasta que el padre recoge su estado con `wait()`.

---

### **Señales y SIGKILL**

**SIGKILL** (`kill -9` en UNIX) es una señal enviada a un proceso para forzarlo a terminar inmediatamente. No puede ser interceptada ni ignorada por el proceso.

---

### **Comunicación entre Procesos (IPC - Interprocess Communication)**

Dado que los procesos en ejecución son independientes y tienen su propia memoria, es necesario establecer mecanismos de comunicación para compartir información.

#### **Tipos de Comunicación entre Procesos**

1. **Memoria compartida (Shared Memory)**
2. **Paso de mensajes (Message Passing - Queues)**

---

##### 🔗 **Memoria Compartida (Shared Memory)**

En este modelo, los procesos acceden a un espacio de memoria común, donde pueden leer y escribir datos.

![Shared Memory](../images/shared_memory.png "Shared Memory")

**Descripción de imágen:**

- **Acceso compartido:** Dos o más procesos (como A y B) tienen acceso a un espacio común en memoria.
- **Rapidez:** La memoria compartida suele ser más rápida que otras formas de comunicación porque minimiza la intervención del sistema operativo.
- **Problemas potenciales:** Sincronización incorrecta puede causar conflictos, como sobrescritura de datos.

#### **Ventajas**

✔️ **Rápido** → Requiere menos intervención del sistema operativo que el paso de mensajes.  
✔️ **Eficiente** → Permite compartir grandes volúmenes de datos rápidamente.

#### **Desventajas**

❌ **Mayor riesgo de errores** → Si dos procesos intentan acceder y modificar la misma zona de memoria al mismo tiempo, pueden ocurrir inconsistencias.  
❌ **Más difícil de implementar** → Es necesario gestionar acceso concurrente y sincronización.

---

### 📬 **Paso de Mensajes (Message Passing - Queues)**

En este modelo, los procesos se comunican enviando mensajes a través de **colas de mensajes**.

![Queue](../images/queue.png "Queue")

**Descripción de imágen:**

- **Acceso compartido:** Dos o más procesos (como A y B) tienen acceso a un espacio común en memoria.
- **Rapidez:** La memoria compartida suele ser más rápida que otras formas de comunicación porque minimiza la intervención del sistema operativo.
- **Problemas potenciales:** Sincronización incorrecta puede causar conflictos, como sobrescritura de datos.

#### **Concepto**

Los procesos intercambian información sin compartir memoria, sino a través de un **enlace de comunicación** que puede ser directo o indirecto.

**Operaciones básicas:**

- `send()` → Envía un mensaje.
- `receive()` → Recibe un mensaje.

#### **Ventajas**

✔️ **Evita problemas de acceso concurrente** → No requiere sincronización manual.  
✔️ **Más seguro en sistemas distribuidos** → No expone memoria compartida.

#### **Desventajas**

❌ **Más lento** → Implica más intervención del sistema operativo.  
❌ **Mayor sobrecarga** → Se necesita administrar el enlace de comunicación.

---

### **Comunicación Directa e Indirecta**

1. **Comunicación Directa**
   - Los procesos se envían mensajes entre sí especificando explícitamente el destinatario.
   - Puede ser **simétrica** (ambos procesos especifican con quién se comunican) o **asimétrica** (solo el emisor lo especifica).

2. **Comunicación Indirecta**
   - Utiliza **buzones** o **colas de mensajes** para facilitar la comunicación entre múltiples procesos.
   - Más flexible pero requiere una gestión adecuada.

---

### **Sincronización en la Comunicación**

#### **Sincronía**

Determina si un proceso debe esperar o no para enviar o recibir un mensaje.

- **Sincronía (bloqueante)** → El proceso espera hasta que el mensaje sea enviado/recibido.  
- **Asincronía (no bloqueante)** → El proceso continúa su ejecución sin esperar.

---

### **Buffering en la Comunicación**

**El buffering define cómo se almacenan los mensajes antes de ser entregados.**

1. **Sin buffering** → La cola tiene capacidad **cero**, el emisor se bloquea hasta que el receptor reciba el mensaje.  
2. **Buffering automático finito** → La cola tiene capacidad **limitada** y el emisor se bloquea cuando está llena.  
3. **Buffering automático ilimitado** → La cola puede crecer indefinidamente y el emisor nunca se bloquea.

---

### **Problema del Productor-Consumidor**

Este es un problema clásico en IPC donde:

- **El productor** genera datos y los coloca en un buffer.
- **El consumidor** toma los datos del buffer y los procesa.

#### **Posibles problemas**

❌ **Condición de carrera:** Si el productor y el consumidor acceden simultáneamente al buffer sin sincronización, pueden sobrescribirse datos.  
❌ **Subdesbordamiento:** Si el consumidor intenta leer cuando el buffer está vacío, se bloquea.  
❌ **Sobreflujo:** Si el productor sigue generando datos cuando el buffer está lleno, se bloquea o pierde datos.

#### **Solución**

✔️ **Uso de semáforos o mutex** para garantizar acceso exclusivo.  
✔️ **Buffers circulares** con punteros `in` y `out` que indican la posición de escritura y lectura.

---

#### **Errores relacionados con la posición de los punteros en un buffer circular**

1. **Si `in` y `out` apuntan al mismo lugar:** El buffer está vacío.
2. **Si `in` está una posición delante de `out`:** El buffer está lleno.
3. **Si `in` sobrepasa `out` sin control:** Se pierden datos o se sobrescriben.

##### **¿Dónde deberían estar los punteros?**

- `in` debe avanzar solo cuando el productor escribe datos.
- `out` debe avanzar solo cuando el consumidor lee datos.
- Deben estar correctamente sincronizados para evitar pérdida de datos.

---

## 🌐 **Sistema Cliente-Servidor**

El **sistema cliente-servidor** es un modelo de comunicación en el que los dispositivos (clientes) solicitan servicios o recursos a un servidor centralizado, que se encarga de procesar las solicitudes y responder a ellas.

![Sistema Cliente Servidor](../images/sistema_cliente_servidor.png "Sistema Cliente Servidor")

**Descripción de imágen:**

1. **Servidor:** Es el nodo central que almacena, procesa y provee servicios, como bases de datos, archivos o aplicaciones.
2. **Cliente:** Son dispositivos como computadoras, laptops o smartphones que hacen solicitudes al servidor a través de una red.

**Relación con Internet:**  
El sistema cliente-servidor es la base de la comunicación en Internet. Los navegadores web (clientes) solicitan páginas web a los servidores, los cuales responden enviando los datos solicitados.

---

### 🔌 **¿Qué es un Socket?**

Un **socket** es un punto de conexión que permite la comunicación entre procesos, ya sea dentro de un mismo sistema o a través de una red.

**Características principales:**

- Se identifican con una **dirección IP** y un **puerto**. Ejemplo: `161.25.19.8:1625`.
- Permiten la comunicación en tiempo real, como en aplicaciones de chat o juegos en línea.
- El sistema operativo gestiona los sockets y los asigna a procesos que los solicitan.

**Dirección especial:**

- `127.0.0.1`: Es conocida como **loopback** y permite que un dispositivo se comunique consigo mismo.

**Tipos de puertos:**

- **Puertos bien conocidos (1-1024):** Usados por protocolos comunes como HTTP (80) o FTP (21).
- Puertos superiores pueden usarse para aplicaciones específicas.

**Funcionamiento:**

- Un proceso solicita un socket para escuchar un puerto.
- El sistema operativo crea el socket y permite al proceso interactuar con otros.

---

### 📡 **TCP y UDP Explicados con Ejemplos**

#### **TCP (Transmission Control Protocol)**

TCP es un protocolo orientado a la conexión que asegura la entrega correcta de los datos.

**Ejemplo:**

1. Punto B quiere enviar información a punto A.
2. El mensajero (TCP) llega al punto A y dice: "Este paquete es de B, ¿lo aceptas?".
3. Punto A puede responder:
   - "Sí, lo acepto" → TCP asegura que el paquete se entregue correctamente.
   - "No, recházalo" → TCP no entrega el paquete.
4. TCP verifica que todos los datos lleguen en orden y sin errores.

**Ventaja:** Fiabilidad en la entrega de datos.  
**Desventaja:** Más lento debido al control y confirmación.

---

#### **UDP (User Datagram Protocol)**

UDP es un protocolo no orientado a la conexión, lo que significa que no verifica si los datos fueron recibidos correctamente.

**Ejemplo:**

1. Punto B envía algo al punto A usando UDP.
2. El mensajero (UDP) llega, deja el paquete en la puerta de A y se va, sin confirmar si alguien lo recibió.

**Ventaja:** Rápido y eficiente para aplicaciones como streaming o videojuegos.  
**Desventaja:** No garantiza la entrega ni el orden de los datos.
