# Práctica Calificada 002 - Llamadas al Sistema en xv6

**Estudiante:** Fredy Delacruz Huaraca  
**Curso:** Sistemas Operativos (IS-380)  
**Semana:** Práctica 02  

---
## 1. Interfaz, tabla de despacho e implementación de dos llamadas al sistema
A continuación se detalla el rastreo completo de las llamadas `read` y `getpid`.

### A. RASTREO COMPLETO DE LA LLAMADA AL SISTEMA: `read`

#### 1. Interfaz en el Kernel (`kernel/syscall.h`)
Al realizar la búsqueda en los archivos de cabecera del núcleo, localizamos la directiva del preprocesador que asigna el identificador numérico único a la llamada mediante el macro `#define SYS_read 5`. Este número entero representa la interfaz que el espacio de usuario emplea para invocar el servicio.

![Rastreo de la interfaz de SYS_read](imgs/1_read_interfaz.png)

#### 2. Entrada en la Tabla de Despacho (`kernel/syscall.c`)
La constante `SYS_read` se utiliza directamente como un índice posicional 
dentro del arreglo global de punteros de función `static uint64 (*syscalls)(void)`. 
La línea exacta mapea la relación `[SYS_read] sys_read`,
 asociando el identificador 5 con la función encargada de su despacho.

![Rastreo de la tabla de despacho para SYS_read](imgs/2_read_despacho.png)


#### 3. Implementación de la Función (`kernel/sysfile.c`)
La lógica operativa e interna se encuentra codificada dentro de `kernel/sysfile.c` bajo la firma `uint64 sys_read(void)`. Esta rutina se encarga de validar los descriptores de archivos del proceso, interactuar con los buffers del sistema de almacenamiento y transferir los bloques de datos leídos hacia el espacio de memoria asignado al usuario.

![Rastreo de la implementación de sys_read](imgs/3_read_implementacion.png)

*   **Párrafo de Conexión Integral:** 
    Cuando un programa de usuario invoca la función estándar `read()`, la arquitectura de hardware y las bibliotecas cargan el identificador numérico `SYS_read` (5) como parámetro de la interfaz. Al cruzar la frontera del núcleo mediante el mecanismo de excepciones, la función de despacho utiliza este índice 5 para consultar de forma atómica el arreglo vectorizado `syscalls`. Este mapeo redirige de inmediato el flujo del procesador hacia la dirección exacta de memoria donde reside la función de aislamiento `sys_read()`, resolviendo la solicitud dentro del espacio protegido del kernel de manera monolítica.

---

### B. RASTREO COMPLETO DE LA LLAMADA AL SISTEMA: `getpid`

#### 1. Interfaz en el Kernel (`kernel/syscall.h`)
El rastreo localiza la definición simbólica del identificador mediante el macro `#define SYS_getpid 11`. El entero 11 actúa como el token contractual inalterable entre el modo usuario y el modo supervisor para realizar la solicitud de identidad del proceso.

![Rastreo de la interfaz de SYS_getpid](imgs/4_getpid_interfaz.png)
