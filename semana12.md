# Implementación de FileSystem

## ¿Qué es un File System?

Un **File System** (sistema de archivos) es la **abstracción del almacenamiento** en un disco, igual que la CPU abstrae el procesamiento. Su función es organizar cómo se almacenan y recuperan datos del disco duro. Sin él, los datos estarían almacenados como un gran bloque sin estructura.

### Requisitos esenciales

1. **Eficiencia**: debe usar los recursos de almacenamiento de forma óptima. Aunque el almacenamiento físico se puede ampliar (comprando más discos), **el recurso como tal es limitado**.
2. **Fiabilidad**: los datos deben almacenarse correctamente para evitar pérdidas.
3. **Seguridad**: debe controlar el acceso mediante permisos, crucial en entornos compartidos (como Google Drive).

## Tipos de sistemas de archivos

1. **Locales**: funcionan en una sola máquina.
2. **Distribuidos**: permiten que múltiples nodos accedan y gestionen archivos en clústeres. Tienen ventajas en Big Data y minería de datos por su capacidad de replicación (por ejemplo, en AWS se usa un factor de replicación de 3).
3. **En red**: como Google Drive, no replican todo localmente, pero se comportan similar a un sistema distribuido.

## Estructura interna del File System

1. **Metadata**: información básica de cada archivo (nombre, permisos, tamaño), como el ADN de un archivo.
2. **Bloques y clusters**: los archivos se dividen en bloques, que se pueden replicar en diferentes sectores del disco.
3. **Tablas de asignación** (FAT): indican dónde está almacenado cada bloque.

## Operaciones básicas

* Crear, leer, escribir y eliminar archivos/directorios.

## Estándares

Los sistemas operativos siguen estándares como **POSIX** para compatibilidad entre plataformas. Ejemplo: sistemas de pago deben seguir reglas como las **OWASP** (por seguridad en tarjetas de crédito).

## Sistemas de archivos comunes

| Sistema       | Uso                   | Características                                               |
| ------------- | --------------------- | ------------------------------------------------------------- |
| **FAT32**     | Memorias USB, cámaras | Alta compatibilidad, pero limitado a archivos ≤4 GB           |
| **exFAT**     | USB modernos          | Sin límite práctico de tamaño, sin compresión ni permisos     |
| **NTFS**      | Windows               | Soporta compresión, cifrado y gestión de permisos             |
| **HFS+/APFS** | macOS                 | APFS optimizado para SSD, HFS+ más antiguo                    |
| **ext4**      | Linux                 | Soporta archivos grandes, menos fragmentación, admite cifrado |

## Hadoop Distributed File System (HDFS)

Es un **sistema de archivos distribuido** creado por Apache como parte de Hadoop.

### Componentes principales

* **NameNode**: administra la metadata (dónde están los bloques).
* **DataNode**: almacena físicamente los bloques de datos.
* **Secondary NameNode**: no es un respaldo, sino una ayuda para gestionar el NameNode.

HDFS permite leer archivos desde cualquier nodo. Pero **no permite escritura directa** sobre los archivos. Para modificar uno, se debe descargar, cambiar y volver a subir.

## Hive

**Hive** es una base de datos distribuida que permite procesar datos tipo SQL sobre archivos como CSV. No se hacen `INSERT` directos; los datos se leen desde archivos planos, lo cual es ideal para grandes volúmenes de datos particionados.

## Blockchain como sistema de archivos

Es un sistema distribuido donde cada nodo tiene una copia completa del historial. Los archivos (transacciones) son **inmutables** y **encriptados**, lo que le da seguridad. Aunque se asocia a criptomonedas, también se usa en **votaciones electrónicas**, ya que múltiples computadoras validan simultáneamente las acciones.

## RAID: almacenamiento con redundancia y velocidad

**RAID** (Redundant Array of Independent Disks) combina varios discos duros para mejorar **rendimiento** o **seguridad**.

### Tipos

* **RAID 0**: divide los datos entre discos (velocidad, pero sin tolerancia a fallos).
* **RAID 1**: duplica los datos (seguridad, pero sin aumento de capacidad).
* **RAID 5**: necesita ≥3 discos, almacena datos y paridad (tolerancia a 1 fallo).
* **RAID 6**: como RAID 5 pero con doble paridad (tolerancia a 2 fallos).
* **RAID 10**: combina RAID 1 + RAID 0 (alta velocidad y tolerancia, pero costoso).

## Tecnologías futuras: MAMR y HAMR

* **MAMR**: usa microondas para escribir datos con menos energía.
* **HAMR**: calienta zonas del disco para escribir datos con mayor densidad.
