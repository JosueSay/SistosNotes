# 🔒 Deadlocks (Interbloqueos)

## ¿Qué es un Deadlock?

Un **deadlock** es un estado en el que **dos o más procesos quedan bloqueados** indefinidamente, **esperando recursos que están siendo utilizados entre ellos**.

### Etapas típicas en el uso de recursos por parte de un hilo

1. **Solicitud:** pide el recurso.
2. **Uso:** trabaja con el recurso.
3. **Liberación:** devuelve el recurso.

## 🛑 ¿Cuándo ocurre un deadlock?

Un conjunto de hilos entra en deadlock cuando:

- Cada hilo **espera un recurso** que está siendo usado por **otro hilo del mismo conjunto**.
- Nadie puede continuar.

Ejemplo: múltiples procesos esperando bloqueos (mutex, semáforos, archivos, etc.) que nunca se liberan.

## 🤔 Deadlock vs. Livelock

| Deadlock | Livelock |
|----------|----------|
| Hilos bloqueados, ninguno avanza. | Hilos activos, pero no progresan. |
| Esperan recursos mutuamente. | Intentan actuar repetidamente sin éxito. |

## 📌 Condiciones necesarias para un Deadlock

1. **Exclusión mutua:** solo un proceso puede usar un recurso.
2. **Retención y espera:** un proceso con un recurso espera por otro.
3. **No expropiación:** recursos no pueden ser forzadamente quitados.
4. **Espera circular:** cada proceso espera un recurso de otro en un ciclo.

## 🔍 ¿Cómo tratamos los Deadlocks?

### 1. Ignorar

- Muchos SOs (Linux, Windows) **no los manejan**.

### 2. Prevenir

- Asegurarse de que **no se cumpla alguna de las 4 condiciones** necesarias.

### 3. Evitar

- Usar algoritmos como el **del banquero**.
- Asegura que el sistema **nunca entre en un estado inseguro**.

### 4. Detectar y recuperar

- Permitir que ocurran y luego **detectar el ciclo** de espera.
- Requiere ejecutar algoritmos de detección de ciclos en grafos.

## 🧮 Algoritmo del Banquero

- Simula un sistema financiero.
- Solo se aprueban peticiones si el sistema **permanece en estado seguro**.
- Requiere conocer:
  - Recursos disponibles y asignados.
  - Máxima demanda de cada proceso.

### Limitaciones

- Difícil de implementar.
- Procesos deben ser independientes.
- El número de procesos/recursos debe ser fijo.

## 📊 Representación con grafos

- **Procesos** → círculos.
- **Recursos** → rectángulos.
- Aristas:
  - **Solicitud:** proceso → recurso.
  - **Asignación:** recurso → proceso.
- Detectar ciclos implica detectar deadlocks.

## 🧠 Detección de Deadlocks

- Algoritmos se ejecutan periódicamente.
- Requiere balance entre:
  - Detección temprana.
  - **Costo en CPU.**

### ¿Cuándo ejecutar?

- Por cada solicitud (caro).
- A intervalos regulares (e.g., cada hora).
- Cuando el uso de CPU cae por debajo de cierto umbral.

## 🛠️ Estrategias de recuperación

1. **Abortar todos los procesos involucrados.**
2. **Abortar procesos uno por uno** (por costo).
3. **Retroceder (rollback)** a un estado anterior.
4. **Apropiarse de recursos y forzar liberación.**

### Criterios para selección

- Menor tiempo usado.
- Menor cantidad de recursos.
- Menor prioridad.
- Mayor tiempo restante estimado.

## 🚫 Prevención

- **Evitar exclusión mutua:** difícil, casi siempre necesaria.
- **Evitar retención y espera:** pedir todos los recursos de una vez.
- **Eliminar no expropiación:** permitir quitar recursos (raro).
- **Evitar espera circular:** imponer orden jerárquico en peticiones.

## ⚖️ Starvation

Cuando un proceso **nunca avanza** porque siempre es elegido como "víctima".

### ¿Cómo evitarlo?

- Incluir número de rollbacks como factor de decisión.
- Asegurar que cada proceso tenga **número finito de abortos**.

## 🎯 Conclusiones

- **Deadlocks son difíciles de manejar.**
- Muchos SOs **no los previenen por defecto**.
- El manejo queda en manos del **programador**.
- Con la demanda creciente de **concurrencia y paralelismo**, los deadlocks y otros problemas de liveness **son más críticos que nunca.**
