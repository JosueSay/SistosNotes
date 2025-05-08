# 💾 Memoria Principal

## 🧠 Memoria principal vs secundaria

- CPU **solo accede directamente** a registros y memoria principal.
- La memoria secundaria (disco) es solo para almacenamiento.
- Los programas deben ser cargados desde memoria secundaria a principal para ejecutarse.
- El SO debe proteger la memoria y usar registros base y límite para evitar accesos inválidos.

## 🔍 Acceso y abstracción de memoria

- Sin abstracción, cada proceso debería gestionar TODA la memoria: peligroso y poco práctico.
- Solución: gestor de memoria del SO, reubicación y protección.

### Tipos de direcciones

- **Lógica:** usada por el proceso (relativas).
- **Física:** usadas por el hardware (reales).
- Traducción mediante registros base/límite y la **MMU (Memory Management Unit).**

## 📁 Espacios de direcciones

- Cada proceso tiene un **espacio de direcciones lógico** (virtual).
- Se traduce a espacio físico con ayuda de la **MMU**.
- Hay diferentes momentos para "ligar" (binding) direcciones:
  - **Compilación**
  - **Carga**
  - **Ejecución** (con MMU)

## 🧠 Técnicas modernas

### 📦 Dynamic Loading

- Cargar solo código necesario en el momento.
- Ahorra memoria (ej: rutinas de error).

### 🔗 Dynamic Linking

- Uso de DLLs (shared libraries).
- Evita duplicar código en memoria.

### 💽 Swapping

- Mover procesos entre memoria secundaria y principal.
- En SO modernos: swap de porciones, no procesos completos.

## 🧩 Asignación de memoria

### Particionamiento fijo

- Divisiones iguales o predefinidas.
- Riesgo: **fragmentación interna**.

### Particionamiento dinámico

- Divisiones según necesidad.
- Riesgo: **fragmentación externa**.
- Técnicas:
  - **First-fit**
  - **Best-fit**
  - **Worst-fit**
  - **Compactación** para resolver huecos.

## ✂️ Fragmentación

| Tipo       | Ejemplo |
|------------|---------|
| **Interna** | Bloques asignados parcialmente usados. |
| **Externa** | Espacios libres dispersos, no aprovechables. |

## 📚 Segmentación

- Memoria dividida en **segmentos lógicos** (código, datos, pila, etc).
- Cada segmento tiene:
  - Permisos (read, write, execute)
  - Longitud
- Direcciones: `(segmento, offset)`
- Mayor modularidad y protección.

## 🔀 Paginación

- Divide memoria física en **marcos** y lógica en **páginas**.
- Cada proceso tiene su **tabla de páginas**.
- Traduce direcciones lógicas a físicas.
- Apoyo de hardware: **Translation Lookaside Buffer (TLB)** para acelerar.

## 📛 Page Fault y Thrashing

- Si una página no está en memoria → **page fault**
- Se trae desde disco.
- **Thrashing:** exceso de page faults → sistema se pasa swappeando.

## ⚖️ Tamaño de página

| Tamaño     | Ventaja                  | Desventaja                     |
|------------|--------------------------|--------------------------------|
| Pequeño    | Menos fragmentación      | Tablas grandes                 |
| Grande     | Menor overhead de tabla  | Más fragmentación interna      |

- Ideal: **balance entre ambas.**

## 🔄 Movimiento de páginas

- **Política de obtención:**
  - Demand Paging
  - Prepaging
- **Política de posicionamiento:** ¿dónde se coloca la nueva página?
- **Política de reemplazo:** ¿qué página se elimina?

### Técnica: **Frame locking**

- Impide que páginas críticas del sistema (kernel) sean reemplazadas.

## 🕰️ Política del Reloj

- Eficiente algoritmo de reemplazo.
- Bit de uso → indica si la página fue referenciada.
- Recorrido circular:
  - Si bit = 0 → se reemplaza.
  - Si bit = 1 → se pone en 0 y se sigue.

## 🧠 Paginación vs Segmentación

| Característica       | Segmentación                         | Paginación                         |
|----------------------|--------------------------------------|------------------------------------|
| Visibilidad          | Programador                          | Transparente                       |
| Fragmentación        | Externa                              | Interna                            |
| Protección/Modularidad | Muy buena                          | No tan detallada                   |
| Tamaño               | Variable                             | Fijo                               |

- Ambas permiten **memoria no contigua**, **protección** y **memoria virtual**.

## 🧱 Paginación jerárquica

- Para reducir espacio ocupado por tablas grandes.
- Divide tabla de páginas en niveles (multi-nivel).
- Permite manejar direcciones virtuales muy grandes (64 bits, etc).

## ✅ Conclusión

La gestión de memoria es esencial para:

- Aislamiento entre procesos.
- Uso eficiente de memoria física.
- Soporte para memoria virtual y multiprogramación.

El sistema operativo usa técnicas como **reubicación, segmentación, paginación, swapping** y más para lograrlo.
