# Historias de Usuario – MVP Biblioteca

## Historia #1: Búsqueda de libro

**Título:** Buscar libro por título  
**Como** estudiante de la universidad  
**Quiero** buscar un libro escribiendo su título  
**Para** saber si está disponible en la biblioteca  

**Criterios de aceptación:**
- Dado que estoy en la pantalla de catálogo, cuando escribo "Cien años" y presiono buscar, entonces se muestran los libros que contengan esas palabras.
- Si ningún libro coincide, muestra mensaje "No se encontraron resultados".
- Los resultados se muestran en menos de 2 segundos.

**Definition of Ready (DoR):**
- El mockup de búsqueda está aprobado.
- Los datos de prueba (10 libros) están disponibles.

**Definition of Done (DoD):**
- La funcionalidad está implementada y probada en navegador.
- El código está en el repositorio.

---

## Historia #2: Realizar préstamo

**Título:** Pedir prestado un libro disponible  
**Como** estudiante autenticado  
**Quiero** pedir prestado un libro que aparece como disponible  
**Para** llevármelo a casa  

**Criterios de aceptación:**
- Dado un libro disponible, cuando hago clic en "Pedir prestado", el sistema cambia el estado a "Prestado".
- Se registra fecha de devolución = fecha actual + 7 días.
- Recibo un correo de confirmación.

**DoR:** Prototipo de préstamo validado con bibliotecario.  
**DoD:** El préstamo persiste en BD y el libro ya no aparece como disponible en búsquedas.

---

## Historia #3: Registrar devolución con multa

**Título:** Devolver libro y calcular multa automática  
**Como** bibliotecario  
**Quiero** registrar la devolución escaneando el código del libro  
**Para** que el sistema calcule automáticamente si hay multa por retraso  

**Criterios de aceptación:**
- Dado un libro prestado hace 10 días (devolución esperada hace 3 días), cuando escaneo el código, el sistema muestra multa de $3.000.
- El libro cambia a "Disponible".
- Se envía correo al estudiante notificando la multa.

**DoR:** Caso de uso "Devolución" aprobado.  
**DoD:** La multa queda registrada en el historial del estudiante.

---

## Historia #4: Recordatorio de vencimiento

**Título:** Recibir correo de recordatorio  
**Como** estudiante  
**Quiero** recibir un correo un día antes de que venza mi préstamo  
**Para** no olvidar devolver a tiempo  

**Criterios de aceptación:**
- Dado un préstamo que vence mañana, el sistema envía correo a las 8 AM.
- El correo incluye título del libro y fecha límite.

**DoR:** Base de datos con préstamos de prueba.  
**DoD:** El correo se envía efectivamente (se verifica en bandeja de entrada).

---

## Historia #5: Generar reporte de préstamos activos

**Título:** Generar reporte en CSV  
**Como** bibliotecario  
**Quiero** generar un reporte con todos los préstamos no devueltos  
**Para** hacer seguimiento a los libros prestados  

**Criterios de aceptación:**
- Dado que tengo rol bibliotecario, cuando selecciono "Reporte activos", se descarga un archivo .csv.
- El archivo contiene: estudiante, correo, título del libro, fecha préstamo, fecha devolución esperada.

**DoR:** Mínimo 3 préstamos activos en BD de prueba.  
**DoD:** El archivo se abre correctamente en Excel.