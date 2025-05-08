# ⚡ ¿Qué Pasa al Encender una PC?

**Flujo del encendido:**

1. **Se presiona el botón de encendido.**
2. **Power Good Signal:** Se activa una señal en un registro del CPU indicando que la alimentación es estable.
3. **El CPU recibe la instrucción "Roger That".**
4. **ROM ejecuta el POST (Power-On Self Test).**
5. **Componentes inicializan en orden:**
   - CPU es el primero en encender.
   - RAM se activa para cargar el kernel.
6. **Boot Manager carga el kernel en memoria.**
7. **BIOS finaliza su ejecución y se propaga la energía de forma constante.**
8. **Otros componentes como ventiladores y disco duro se activan.**

---

## 🔺 Jerarquía de Memorias

Las memorias en un sistema tienen una jerarquía basada en **velocidad, capacidad, proximidad y costo**:

| Tipo de Memoria   | Ubicación     | Velocidad | Capacidad | Costo |
|------------------|--------------|-----------|----------|------|
| **Registros**    | Dentro del CPU | 🔥 Muy rápida | ⚡ Muy baja | 💰 Alto |
| **Caché**        | Dentro del CPU | 🔥 Rápida | ⚡ Baja | 💰 Alto |
| **RAM**          | Placa base    | 🚀 Media | 📦 Media | 💵 Medio |
| **Disco Duro**   | Unidad externa | 🐢 Lenta | 🏠 Alta | 💲 Bajo |

> 💡 **Diferencia M1 vs M2**: Cambia la jerarquía y ubicación de memoria, haciendo que la RAM sea más rápida al integrarla con el CPU.

---

## 🎯 Gestión, Calendarización y Asignación de Recursos

La administración del sistema operativo involucra distintos enfoques para multitarea:

- **Multitarea**: Alterna entre tareas rápidamente.
- **Multiprogramación**: Varios procesos pueden ejecutarse compartiendo recursos.
- **Concurrencia y paralelismo**: Uso eficiente del CPU para múltiples procesos.

| Enfoque        | Definición | Objetivo | Asignación de Recursos | Requisitos de Hardware |
|---------------|------------|-----------|----------------------|----------------------|
| **Concurrencia** | Ejecuta una tarea a la vez con cambio rápido. | Aprovechar tiempo de CPU. | Basado en colas de procesos. | No requiere múltiples núcleos. |
| **Paralelismo**  | Ejecuta múltiples tareas simultáneamente. | Máximo desempeño. | División de carga en núcleos. | Requiere múltiples núcleos. |

> 💡 **Ejemplo:** En Assembler, cuando se hace un *jump* a un registro, se usa un reloj para luego regresar.

---

## 🏛️ Multiprocesamiento: Simétrico vs Asimétrico

| Tipo de Multiprocesamiento | Definición | Características |
|----------------------------|------------|----------------|
| **Simétrico (SMP)**  | Todos los procesadores tienen acceso igualitario a tareas. | No distingue entre procesos, trabaja en conjunto. |
| **Asimétrico (AMP)** | Requiere un orquestador que asigna tareas. | Un procesador controla a los demás. |

![Simétrico y Asimétrico](../images/simetrico_asimetrico.png "Simétrico y Asimétrico")

> 💡 **Ejemplo:** Un sistema multicore tiene múltiples núcleos compartiendo caché en distintos niveles (L1, L2, L3).

---

## 🖥️ Interfaz vs Shell

| Concepto | Definición |
|----------|------------|
| **Interfaz** | Medio visual para interactuar con el sistema. |
| **Shell** | Programa que recibe instrucciones de usuario. |

> 💡 **Ejemplo:** Proyecto GNU surgió como una alternativa a Unix, promoviendo el uso de software libre.
