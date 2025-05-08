# Sistema de Archivos (File System)

## ¿Qué es un File System?

Es el componente que organiza cómo se almacenan y recuperan los datos en medios físicos. Sin un sistema de archivos, los datos estarían sin estructura, imposibilitando su uso eficiente.

Desde los inicios, como tarjetas perforadas y cintas magnéticas, se ha requerido una estructura lógica para acceder a los datos, aunque antes solo se podía acceder de forma secuencial.

## Funciones del File System

1. **Asignación y administración del espacio libre.**
2. **Búsqueda, lectura, almacenamiento, edición y eliminación de archivos.**
3. **Gestión de directorios y estructura de archivos.**
4. **Mantenimiento del registro de sectores usados/libres.**

## Instalación y uso

- Para usar un medio de almacenamiento, este debe ser **formateado** con un sistema de archivos.
- Antes era común que el usuario lo hiciera manualmente; hoy, la mayoría de dispositivos ya vienen formateados.
- Incluso puede emplearse para datos no almacenados localmente, como los recibidos por red.

## Características comunes

- Todos los sistemas de archivos usan una **estructura de árbol** desde un directorio raíz (`/` en Unix/Linux).
- A partir del directorio raíz se ramifican carpetas y subcarpetas.

## Compatibilidad y diferencias

- Los sistemas de archivos no son compatibles entre sí por defecto.
- Por ejemplo, **APFS** de Apple no es leído por Windows.
- Se puede acceder mediante **software de terceros** que permite lectura y/o escritura en sistemas no nativos.

## Principales Sistemas de Archivos

### FAT (FAT12/16/32)

- Desde 1980.
- **FAT32** es ampliamente usado en dispositivos extraíbles.
- Límite de tamaño por archivo: **4 GB**.
- Máxima compatibilidad, pero baja seguridad y sin cifrado.

### exFAT

- Evolución de FAT, lanzado en 2006.
- Soporta archivos más grandes que FAT32.
- Ideal para memorias USB y SD.
- Compatible con Windows 7+ y macOS 10.6.4+.
- **Tamaño máx. de archivo**: 512 TB.

### NTFS

- Estándar desde Windows Vista.
- Soporta compresión, cifrado, y gestión detallada de permisos.
- Alta seguridad y rendimiento.
- No recomendado para discos pequeños.
- **Tamaño máx. de archivo**: 256 TB.

### HFS+ (Mac OS Extended)

- Reemplazó al antiguo HFS.
- Mejor rendimiento y capacidad que HFS.
- Soporta hasta 4 mil millones de archivos.
- No optimizado para SSD.
- **Volumen máximo**: 8 exbibytes.

### APFS (Apple File System)

- Desde 2017, para SSDs.
- Sistema de 64 bits, cifrado, espacio compartido, protección contra fallos.
- Reemplaza automáticamente HFS+ en macOS High Sierra en adelante.
- **Volumen máximo**: 8 exbibytes.

### ext4

- Desde 2008, estándar en Linux.
- Mejora en fragmentación, rendimiento y seguridad.
- Soporta archivos grandes y cambios en caliente.
- **Volumen máximo**: 1 exabyte.

## Comparativa Rápida

| Sistema | Compatibilidad | Tamaño Máx. | Cifrado | Uso común |
|--------|----------------|-------------|---------|-----------|
| FAT32 | Alta | 4 GB | No | USBs, cámaras |
| exFAT | Alta | 512 TB | No | USB, SD |
| NTFS | Media | 256 TB | Sí | Windows interno |
| HFS+ | Baja | 8 EiB | No | macOS antiguo |
| APFS | Baja | 8 EiB | Sí | macOS moderno |
| ext4 | Media | 1 EiB | Sí (Linux 4.1+) | Linux |

## RAID (Redundant Array of Independent Disks)

RAID es una técnica que combina múltiples discos duros en un solo volumen lógico para:

- **Aumentar velocidad** (striping).
- **Proporcionar redundancia** (mirroring).
- Presentado como un único disco al sistema operativo.

### RAID 0 – Striping

- Distribuye datos en paralelo entre discos.
- **Ventaja**: máximo rendimiento.
- **Desventaja**: si falla uno, se pierde todo.
- Tamaño total = suma de los discos.

### RAID 1 – Mirroring

- Duplicación exacta de datos entre dos discos.
- **Ventaja**: alta tolerancia a fallos.
- **Desventaja**: no mejora rendimiento, espacio = disco más pequeño.

### RAID 5

- Requiere mínimo 3 discos.
- **Ventaja**: velocidad + tolerancia a fallo de 1 disco.
- **Desventaja**: si fallan 2 discos, se pierde todo.

### RAID 6

- Como RAID 5 pero con tolerancia a 2 fallos.
- **Requiere más inversión**, pero mayor seguridad.

### RAID 1+0 (10)

- Combinación de RAID 1 y RAID 0.
- Alta velocidad y redundancia.
- Necesita mínimo 4 discos.

## Tecnologías Avanzadas

### MAMR (Microwave-assisted Magnetic Recording)

- Usa microondas para alterar la orientación magnética.
- Permite **mayor precisión con menor energía**.

### HAMR (Heat Assisted Magnetic Recording)

- Usa **calor** para reorganizar regiones magnéticas.
- Permite **mayor densidad de almacenamiento** reduciendo errores.

## Cita clave
>
> “Ningún sistema RAID del mundo sirve como copia de seguridad como tal, no en la definición informática en sí misma.”
