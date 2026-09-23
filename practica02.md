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
