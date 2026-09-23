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
