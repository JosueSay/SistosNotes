# Almacenamiento: Disco Duro

## ¿Qué es la memoria secundaria?

Es el conjunto de dispositivos y medios de almacenamiento no volátil que complementan la memoria primaria. Se utiliza para guardar datos de forma permanente, incluso cuando el sistema se apaga.

## Entrada/Salida (I/O)

### Características importantes

- **Propósito del dispositivo**: ¿Con qué se comunica? ¿Qué requiere del SO?
- **Velocidad de transferencia (data rate)**: Teclado ≈ lenta, Disco Duro ≈ millones de bits por segundo.
- **Complejidad de control**: ¿Qué tanto interviene el procesador?

## Data Rates Típicos

- Dispositivos humanos: bajos (e.g. teclado).
- Discos duros: altos (hasta cientos de MB/s).
- Unidades modernas se miden en **bps** (bits por segundo) o **MB/s**.

## Direct Memory Access (DMA)

Permite que los dispositivos I/O se comuniquen directamente con la memoria, sin intervención constante del CPU. El CPU solo da instrucciones al módulo DMA y sigue con otras tareas.

## Discos Duros: Funcionamiento

- Platos cubiertos con material magnético.
- Lectura/escritura por cabezales que **flotan** a nanómetros del plato.
- Movimiento hacia el cilindro → *seek time*.
- Espera a que el sector deseado rote → *latencia rotacional*.
- Velocidades comunes: 5400, 7200, 10000, 15000 RPM.
- Fallo por contacto físico con la superficie: **head crash**.

## ¿Qué es formatear?

### Formateo de Bajo Nivel

- Primer paso para preparar el disco.
- Define sectores (típicamente 512 bytes).
- Crea encabezados y colas que organizan los datos.
- Lo realiza el **fabricante** o **firmware** del disco.

### Formateo Lógico

- Lo realiza el usuario/OS.
- Instala un sistema de archivos (filesystem).
- Organiza los sectores en bloques o clusters para gestionar archivos.

## File System (Sistema de Archivos)

- Provee abstracción del almacenamiento.
- Un **archivo** es la unidad mínima que maneja.
- Opera con **bloques** que traduce a sectores.
- Funciones clave:
  - Crear/eliminar archivos.
  - Leer/escribir.
  - Abrir/cerrar.
- Tipos:
  - **Orientados a registros** (record-oriented): archivos estructurados.
  - **Orientados a flujo** (stream-oriented): secuencias sin estructura (e.g. UNIX).

## Ejemplos: FAT vs NTFS

### FAT

- Maneja una **tabla de asignación** por cluster.
- Cada archivo es una cadena de clusters.
- El fin del archivo se marca con un valor especial.
  
### NTFS

- Usa una **Master File Table (MFT)**.
- Datos como atributo llamado `$DATA`.
- Puede ser **residente** (dentro de MFT) o no (referencia a sectores externos).

## Áreas Especiales en el Disco

- **Boot Block**: Código para cargar el sistema operativo.
- **Bloques corruptos**:
  - Hard error: pérdida irrecuperable.
  - Soft error: recuperable mediante códigos de corrección (ECC).
  - **Sector sparing**: redirección automática de sectores malos.

## Swap Space

- Espacio usado para memoria virtual.
- Puede ser una **partición** (raw) o un archivo.
- Acceso optimizado para velocidad.
- Datos temporales → baja optimización de espacio aceptable.

## Algoritmos de Calendarización de Disco

- Ordenan las solicitudes de acceso a disco para mejorar desempeño.

### Ejemplos

- **FCFS (First Come First Served)**: como FIFO, lento.
- **SSTF (Shortest Seek Time First)**: al cilindro más cercano.
- **SCAN y C-SCAN**: recorrido tipo ascensor.
- **LOOK y C-LOOK**: solo hasta donde hay solicitudes.

> LOOK y SSTF suelen ser mejores por defecto.  
> FCFS es usado en SSDs por su acceso aleatorio.

## Analogías Filosóficas

### ¿Podemos comparar esto con nuestra mente?

1. **Memoria primaria/secundaria** ↔ corto/largo plazo.
2. ¿Existe “memoria virtual” en el cerebro?
3. ¿Hay estructuras o métodos mentales para recordar?
4. ¿Cómo intentamos recordar? ¿Repetición, patrones?
5. Procesos complejos (matemáticas, programación) implican una gestión activa de memoria, similar a swap o buffer.

## Términos Clave

- **bps**: bits por segundo (velocidad).
- **Seek Time**: tiempo que tarda el brazo en posicionarse en el cilindro correcto.
- **Latencia rotacional**: espera a que el plato gire hasta el sector deseado.
- **Head crash**: contacto físico con el disco, causa fallos.
- **Sector sparing**: sectores de repuesto para sectores defectuosos.
- **Swap**: espacio para memoria virtual.
- **Filesystem**: organiza y gestiona archivos.
- **DMA**: comunicación directa con la memoria sin CPU.
