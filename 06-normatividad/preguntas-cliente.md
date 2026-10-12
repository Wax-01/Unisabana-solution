# ❓ Preguntas pendientes para la cliente (y para TI)

Varias brechas del checklist y amenazas del STRIDE dependen de un dato que no pudimos verificar con reconocimiento pasivo. Estas preguntas son cerradas para que se respondan rápido. Si la cliente no sabe la respuesta, la pregunta pasa a la Dirección de TI.

> **Estado: pendiente para el tercer corte.** En el segundo corte no fue posible consultar a la cliente ni a la Dirección de TI. Las preguntas quedan formuladas y se responderán en el tercer corte. Mientras tanto, los ítems y amenazas que dependen de ellas se mantienen como "no confirmado" (Parcial en el checklist).

**Cómo usar este archivo:** al recibir cada respuesta, se llenan las columnas *Respuesta*, *Fecha* y *Quién respondió*, y se actualiza la evidencia de los ítems y amenazas que aparecen en la última columna (con la fecha de la consulta).

| # | Pregunta | Opciones de respuesta | Para | Respuesta | Fecha | Quién respondió | Actualiza |
|---|---|---|---|---|---|---|---|
| P1 | ¿Las hojas de Muestreo y de Asignación PAT están en el OneDrive de su cuenta institucional (@unisabana.edu.co)? | Sí / No (cuenta personal) / Otro sitio | Cliente | | | | Checklist #11 · Taller 4, supuestos |
| P2 | ¿Con quién están compartidas las dos hojas y con qué tipo de enlace? | Nadie / Personas específicas (¿cuántas?) / Personas de la organización / Cualquier persona | Cliente | | | | Checklist #5, #6 · STRIDE T1, T7 |
| P3 | Al iniciar sesión en su cuenta institucional, ¿le pide un segundo factor (código, app Authenticator, SMS)? | Siempre / Solo a veces / Nunca | Cliente (confirmar con TI) | | | | Checklist #10 · STRIDE T2 |
| P4 | ¿Cuánto tiempo se conservan las hojas y los archivos que se descargan de SIGA? ¿Se borran al terminar la encuesta? ¿Se usan para otros reportes? | Se borran al terminar / Se guardan ___ años / No se borran · Sí / No se reutilizan | Cliente | | | | Checklist #3, #14 · STRIDE T3 |
| P5 | ¿Está activado el registro de auditoría de Microsoft Purview en el tenant de la universidad? ¿Con qué retención? | Sí (___ días) / No / No sabe | Dirección de TI | | | | Checklist #12 · STRIDE T6 |
| P6 | ¿Las bases de datos de estudiantes y empleados de la universidad están inscritas en el Registro Nacional de Bases de Datos (RNBD) de la SIC? | Sí / No / No sabe | Dirección General Administrativa o TI | | | | Checklist #15 |
| P7 | ¿Qué hace el estudiante PAT y cómo reporta su disponibilidad? | Aplica la encuesta en el salón / La responde / Ambas · Por correo / Edita la hoja / Formulario / Otro | Cliente | | | | C1 y C2 (Taller 3) · mapa (Taller 4) · DFD F7 · STRIDE T1, T7 |

## Preguntas adicionales para TI (no bloquean la entrega)

- ¿SIGA y su base de datos tienen redundancia (réplica o respaldo)? ¿Están on-premise o en una nube contratada por la U? (Taller 4, redundancia de SIGA)
- ¿El tenant permite enlaces de OneDrive de tipo "Cualquier persona"? (STRIDE T1)
- ¿Los equipos institucionales tienen el disco cifrado (BitLocker)? (STRIDE T3)
- ¿Existe un contrato o adenda de protección de datos con Microsoft como Encargado del tratamiento (Decreto 1377 de 2013, art. 25)? (Checklist #11)
