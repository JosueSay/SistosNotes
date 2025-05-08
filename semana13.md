
# Sistemas de Entrada/Salida (I/O Systems)

## ¿Qué sabemos de I/O?

* **Entrada/Salida (I/O)**: Procesos que involucran dispositivos para ingresar o mostrar datos.
* **Puertos**: Interfaces para enviar y recibir datos.
* **Dispositivos**: Periféricos como teclados, ratones, impresoras, etc.
* **Controladores**: Hardware que permite al SO comunicarse con los dispositivos.

  * Necesitan **drivers** (software) para funcionar correctamente.

## Tipos de I/O

1. **Almacenamiento**: discos duros, memorias.
2. **Pantalla y otros**: monitores, impresoras.
3. **Transmisión**: redes, internet.
4. **HCI (Human-Computer Interface)**: interfaz usuario-dispositivo.

## Comunicación con el Hardware de I/O

* Se usan instrucciones de software para controlar dispositivos.
* Los dispositivos tienen registros como:

  * `data-in`, `data-out`, `status`, `control`
* Registros ocupan 1-4 bytes o utilizan buffers FIFO.
* Acceso mediante:

  * **Instrucciones directas**
  * **Memory-mapped I/O**: se asignan direcciones físicas a registros.

## Polling

* El CPU consulta continuamente el estado de un dispositivo (**busy waiting**).
* Ejemplo (coordinación productor-consumidor):

  1. El host lee el bit “busy”.
  2. Escribe en `data-out`.
  3. Activa el bit “ready”.
  4. El controlador ejecuta la acción.
  5. Limpia los bits de estado tras completar.

## Interrupciones

Permiten al CPU **interrumpir su flujo** para atender eventos urgentes.

### Tipos

* **Hardware**: generadas por dispositivos externos (impresoras, teclado).
* **Software**: generadas por instrucciones en el código (como `int`).
* **Excepciones**: división entre cero, acceso inválido a memoria, etc.

### Mecanismos

* `trap`: permite al sistema ejecutar rutinas del kernel.
* Soporte en sistemas multi-CPU para concurrencia.
* Cruciales para procesamiento en tiempo real.

## DMA (Direct Memory Access)

Permite a los dispositivos transferir datos directamente con la memoria sin involucrar al CPU. Es un chip de hacer procesamiento sin CPU.

* Ejemplo: copiar archivos desde disco a RAM sin usar CPU.
* Mejora el rendimiento en aplicaciones de alto volumen de datos.
* **DVMA**: versión para memoria virtual, más eficiente.

## Application I/O Interface

* Requiere **abstracción, encapsulamiento y capas de software**.
* Permite mover datos entre almacenamiento interno y periféricos.
* Los dispositivos necesitan interfaces de comunicación específicas para conectarse con el CPU.

## Características de dispositivos I/O

* Se clasifican como:

  * **Block I/O**: datos en bloques (ej. discos).
  * **Character I/O**: datos como flujo (ej. teclado).
  * **Memory-mapped files**: acceden como si fueran memoria.
  * **Sockets de red**: para comunicaciones.
* En UNIX, la llamada `ioctl()` transfiere control al dispositivo mediante bits específicos.

## Subsistema I/O del Kernel

* **Caching**: uso de caché para mejorar velocidad.
* **Spooling**: buffer intermedio para dispositivos de una sola conexión (ej. impresora).
* **Device Reservation**: exclusividad de uso para evitar conflictos.

## Manejo de errores

* El SO puede detectar y manejar errores de I/O como:

  * Dispositivos no disponibles, errores de lectura/escritura.
* Solución común: **reintentar la operación**.
* El sistema registra todos los errores en un **log**.

## Estructuras de datos del Kernel

* Mantiene el estado de:

  * Archivos abiertos
  * Conexiones de red
  * Dispositivos de caracteres
* Usa estructuras para rastrear:

  * Buffers
  * Memorias
  * Bloques dañados
* **Mensajería entre objetos** (especialmente en Windows) para transferir información entre kernel y user space.

## Power Management

* Aunque no exclusivo de I/O, **consume energía** y requiere enfriamiento.
* El SO debe gestionar:

  * Consumo eléctrico de dispositivos
  * Métodos para ahorro energético
* Ventajas para empresas:

  * Reducción de costos
  * Mayor sostenibilidad
  * Compatible con virtualización y cloud computing
