# 🖥️ Curso de Sistemas Operativos

## 🔹 Introducción

El **Sistema Operativo (SO)** cumple funciones esenciales como:

- Ser **flexible**, permitiendo su adaptación a diferentes necesidades y usuarios.
- **Gestionar** recursos y procesos de manera eficiente.
- **Abstraer** la complejidad del hardware y software para facilitar su uso.

## ⚙️ Flujo de encendido de una PC

Cuando una computadora recibe energía, sigue el siguiente flujo:

1. **Se enciende** al recibir corriente eléctrica.
2. **El Kernel** se carga en memoria y se encarga de proteger el sistema, garantizando su seguridad y estabilidad.
3. **El Sistema Operativo** entra en funcionamiento, permitiendo la interacción con el usuario y la gestión de los recursos.

## 🔑 Características del SO

El **Sistema Operativo** se define por cuatro características fundamentales:

- **Seguro** 🔐: Protege la información y evita accesos no autorizados.
- **Confiable** ✅: Funciona de manera estable y continua.
- **Privado** 🛡️: Restringe el acceso a datos sensibles.
- **Eficiente** ⚡: Optimiza el uso de los recursos del sistema.

Estas mismas características aplican al **Kernel**, ya que es el núcleo del sistema operativo.

## 🏛️ Metáfora: Un SO es como un Gobierno

Un **Sistema Operativo** es como un **gobierno**:

- **Gestiona recursos** como el gobierno administra los bienes del país.
- **Controla accesos** estableciendo permisos, como un gobierno define leyes.
- **Proporciona servicios** que permiten la interacción de los usuarios.

## 🔹 Kernel: El Núcleo del SO

El **Kernel** es el programa central del sistema operativo, responsable de:

- Ejecutar **tareas fundamentales** para el funcionamiento del SO.
- Estar **activo todo el tiempo** mientras la PC está encendida.
- Actuar como **abstracción del hardware**, permitiendo que el software interactúe con él sin necesidad de conocer sus detalles internos.

🔎 **¿Por qué es una abstracción del hardware?**
El kernel permite a los programas acceder a los recursos físicos (CPU, memoria, discos, etc.) sin interactuar directamente con ellos, proporcionando una capa de seguridad y eficiencia.

### Seguridad del Kernel

El kernel es:

- **Seguro** 🔐: Evita modificaciones no autorizadas y fallos inesperados.
- **Confiable** ✅: Opera correctamente sin importar las acciones del usuario.
- **Privado** 🛡️: Restringe el acceso a la información.
- **Eficiente** ⚡: Controla el uso adecuado de los recursos.

En resumen, el **Kernel restringe, evita y limita accesos inapropiados**.

## 🔄 Modos de Ejecución: Sistema Dual

El **Sistema Operativo** opera en dos modos:

- **Modo Usuario** 👤: El usuario interactúa con el SO mediante aplicaciones.
- **Modo Kernel** ⚙️: El sistema gestiona los recursos con acceso directo al hardware.

🔎 **Metáfora política:**
Los **diputados** (modo kernel) crean leyes sin consultar a los ciudadanos, mientras que los **ciudadanos** (modo usuario) necesitan permisos para realizar trámites como sacar un pasaporte.

## 📞 Llamadas al Sistema (System Calls)

Las **llamadas al sistema (System Calls)** permiten que un programa pase del **modo usuario** al **modo kernel** para ejecutar funciones esenciales del sistema operativo.

Ejemplos de **System Calls**:

| Categoría | Ejemplo |
|-----------|---------|
| **Control de procesos** | `fork()` crea un nuevo proceso |
| **Gestión de archivos** | `open()` abre un archivo |
| **Gestión de I/O** | `read()` lee datos de un dispositivo |
| **Gestión de información** | `getpid()` obtiene el ID del proceso actual |
| **Comunicación entre procesos** | `pipe()` crea un canal de comunicación |

![Tipos de Llamadas](../images/tipos_llamadas.png "Tipos de Llamadas")

📌 **Ejemplo en C:**

```c
#include <stdio.h>
int main() {
    printf("Hi"); // Llamada a printf
    return 0;
}
```

Aquí, `printf()` usa la biblioteca estándar de C, que internamente realiza una llamada al sistema (`write()`) para imprimir en la consola.

## 💀 Fallas, Muerte y Destrucción del SO

Un **Sistema Operativo no debería fallar pero lo hace (LA RESPUESTA ES NO) por las 4 características anteriores**, pero existen excepciones. Algunos errores pueden causar su colapso, como:

- **Acceso a memoria prohibida** 🚫
- **Errores de hardware** 🔥
- **Fallas del kernel** 💀

🔎 **Ejemplo de fallos graves:**

- **BSOD (Blue Screen of Death)** en Windows 🟦
- **Kernel Panic** en Linux 🛑

Cuando ocurre un error crítico, el SO **puede intentar recuperarse** o, en el peor de los casos, **morir y reiniciarse** y en el acto hay que contener y analizar los daños, esta contención de daños el propio os puede contenerlo pero puede morir.
