# Especificación de Requisitos del Sistema (SRS)
## MVP – Sistema de Gestión de Préstamo y Devolución de Libros
**Autor:** Jose Gabriel David Mendez Roncancio  
**Curso:** Análisis y Diseño de Sistemas  
**Fecha:** Mayo 2025

---

## 1. Requisitos Funcionales (RF)

| ID | Nombre | Descripción | Criterio de aceptación |
|----|--------|-------------|------------------------|
| RF-01 | Autenticación de usuario | El sistema permite iniciar sesión con correo institucional y contraseña. | Dado un usuario registrado, cuando ingresa credenciales válidas, accede al dashboard. Si son inválidas, muestra mensaje de error. |
| RF-02 | Buscar libro en catálogo | El usuario puede buscar libros por título, autor o categoría. | Dado un estudiante autenticado, cuando escribe "Cien años" y presiona buscar, se muestran los libros coincidentes. Si no hay resultados, muestra mensaje "No se encontraron libros". |
| RF-03 | Realizar préstamo | El estudiante puede solicitar préstamo de un libro disponible. | Dado un libro con estado "Disponible", cuando el estudiante hace clic en "Pedir prestado", el sistema cambia el estado a "Prestado", registra fecha de préstamo y fecha de devolución (hoy + 7 días), y envía correo de confirmación. |
| RF-04 | Registrar devolución | El bibliotecario registra la devolución de un libro. | Dado un libro prestado, cuando el bibliotecario escanea el código del libro, el sistema cambia el estado a "Disponible" y, si hay retraso, calcula la multa automáticamente. |
| RF-05 | Consultar historial de préstamos | El usuario puede ver su historial de préstamos (activos y pasados). | Dado un estudiante autenticado, cuando accede a "Mi historial", se muestra una tabla con libros, fechas, estado actual y multas pendientes. |
| RF-06 | Enviar notificación de vencimiento | El sistema envía correo electrónico 1 día antes de la fecha de devolución. | Dado un préstamo cuya fecha de devolución es mañana, el sistema a las 8:00 AM envía un correo recordatorio al estudiante. |
| RF-07 | Calcular multa automática | Al devolver un libro tarde, el sistema calcula el valor de la multa ($1.000 por día). | Dado un préstamo con fecha esperada 10/05/2025 y devolución real 13/05/2025, el sistema calcula multa = 3 * $1.000 = $3.000 COP. |
| RF-08 | Gestionar multas | El estudiante ve sus multas pendientes y el bibliotecario puede registrar el pago. | Dado un estudiante con multa de $3.000, cuando el bibliotecario marca "Pagar", el sistema cambia el estado de la multa a "Pagada" y registra la fecha de pago. |
| RF-09 | Generar reporte de préstamos activos | El bibliotecario genera un reporte en CSV con todos los préstamos no devueltos. | Dado un bibliotecario autenticado, cuando selecciona "Reporte de préstamos activos", se descarga un archivo .csv con columnas: estudiante, correo, título del libro, fecha préstamo, fecha devolución esperada. |
| RF-10 | Ver catálogo completo | Cualquier usuario autenticado puede ver la lista completa de libros disponibles. | Dado un usuario logueado, cuando accede a "Catálogo", se muestran todos los libros paginados de 20 en 20, con título, autor, categoría y estado (Disponible/Prestado). |

---

## 2. Requisitos No Funcionales (RNF)

| ID | Nombre | Descripción | Criterio de aceptación |
|----|--------|-------------|------------------------|
| RNF-01 | Rendimiento | Tiempo de respuesta de búsqueda < 2 segundos. | Con base de datos de 5.000 libros, la búsqueda promedio no supera los 2 segundos. |
| RNF-02 | Disponibilidad | Sistema disponible 95% en horario de biblioteca (8:00 - 20:00). | Se permiten caídas programadas en horario nocturno (20:00 - 8:00). |
| RNF-03 | Seguridad | Contraseñas encriptadas con hash SHA-256. | En la base de datos no se guarda texto plano de contraseñas. |
| RNF-04 | Usabilidad | Interfaz responsive (funciona en móvil y escritorio). | Se puede navegar y realizar préstamos desde un celular de gama media sin distorsión. |
| RNF-05 | Escalabilidad | Soporte inicial para 5.000 usuarios y 20.000 libros. | El diseño de base de datos permite particionar tablas si crece el volumen. |
| RNF-06 | Mantenibilidad | Todo el código y diagramas versionados en Git con comentarios. | El repositorio incluye README y carpetas organizadas. |
| RNF-07 | Compatibilidad | Funciona en las últimas dos versiones de Chrome, Firefox y Edge. | Las pruebas de navegador pasan sin errores visuales o funcionales. |
| RNF-08 | Auditoría | El sistema registra en un log cada préstamo, devolución, creación de multa y pago. | Existe una tabla `logs` con campos: usuario, acción, fecha_hora, IP (si aplica). |
| RNF-09 | Backup | La base de datos se respalda automáticamente cada día. | Se genera un archivo de respaldo a las 2:00 AM y se almacena en ubicación segura. |
| RNF-10 | Accesibilidad | Navegación posible con teclado y etiquetas ARIA básicas. | Cumple con nivel A de WCAG 2.1 (contraste mínimo, navegación por tabulador). |

---

## 3. Matriz de trazabilidad (RF → Diagramas de casos de uso)

| RF ID | Nombre del RF | Diagrama de Caso de Uso (N°) |
|-------|---------------|------------------------------|
| RF-01 | Autenticación | #1 (Estudiante), #2 (Bibliotecario), #3 (Administrador) |
| RF-02 | Buscar libro | #1 (Estudiante) |
| RF-03 | Realizar préstamo | #1 (Estudiante) |
| RF-04 | Registrar devolución | #2 (Bibliotecario) |
| RF-05 | Consultar historial | #1 (Estudiante) |
| RF-06 | Enviar notificación vencimiento | #4 (Sistema de Notificaciones) |
| RF-07 | Calcular multa | #2 (Bibliotecario) |
| RF-08 | Gestionar multas | #2 (Bibliotecario) |
| RF-09 | Generar reporte | #5 (Reportes) |
| RF-10 | Ver catálogo completo | #1 (Estudiante) |

---

## 4. Tabla de versión

| Versión | Fecha | Autor | Cambios |
|---------|-------|-------|---------|
| 1.0 | 19/05/2025 | Jose Gabriel David Mendez Roncancio | Creación inicial del SRS para MVP |