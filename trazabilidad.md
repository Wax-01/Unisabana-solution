# 🔗 Trazabilidad entre talleres (AS-IS)

Los talleres 3 a 6 describen el **mismo proceso actual**: SIGA → exportación manual → Hoja de Muestreo y Hoja de Asignación PAT (Excel en OneDrive) → correo manual a los profesores. Cada componente usa el mismo nombre en todas las carpetas. La solución propuesta (TO-BE) vive solo en `07-opportunities-solutions/`.

## Componentes

| Componente | C2 (Taller 3) | Mapa (Taller 4) | DFD (Taller 5) | Hallazgos (T4) | Amenazas (T5) | Ítems del checklist (T6) |
|---|---|---|---|---|---|---|
| SIGA | Sistema externo | Sistemas institucionales | E1 | H1 | T7 | #3, #4, #15 |
| Hoja de Muestreo (Excel en OneDrive) | Contenedor | Microsoft 365 → OneDrive | D2 | H2, H3 | T1 | #5, #6, #12, #13, #14 |
| Hoja de Asignación PAT (Excel en OneDrive) | Contenedor | Microsoft 365 → OneDrive | D3 | H2, H3, H4 | T1, T5 | #5, #6, #12, #13, #14 |
| Correo institucional (Exchange Online) | Sistema externo | Microsoft 365 | D4 (buzón), F10, F11 | H5 | T6, T8 | #1, #2, #7, #8, #9 |
| Archivos exportados de SIGA | Relación SIGA → hojas | Equipo de la coordinadora | D1 | H2 | T3, T7 | #4, #14 |
| PC / portátil de la coordinadora | (infraestructura, no es contenedor) | Equipo de la coordinadora | TB2 (límite de confianza) | H6 | T3, T4 | #13 |
| Cuenta institucional de la coordinadora | (credencial del actor) | — | E2 | H6 | T2 | #10, #11 |

## Actores

| Actor | C1 / C2 | Mapa | DFD | Papel |
|---|---|---|---|---|
| Coordinadora de la encuesta | Sí | Sí | E2 | Opera todo el proceso |
| Estudiante PAT | Sí | Sí | E3 | Reporta su disponibilidad y aplica la encuesta en el salón (por confirmar con la cliente, pregunta P7) |
| Profesor | Sí | Sí | E4 | Recibe el aviso y acepta o rechaza ceder su clase |
| Estudiantes encuestados | No (no interactúan con el sistema) | Sí | No | Responden la encuesta en el salón |

## Del hallazgo a la brecha

| Hallazgo (T4) | Prioridad | Amenazas (T5) | Ítems del checklist (T6) | Pregunta pendiente |
|---|---|---|---|---|
| H6 Operadora única | Alta | T2, T4 | #10, #13 | P3 |
| H3 Hojas sin respaldo | Alta | T1, T4, T5 | #12, #13 | P5 |
| H2 Datos personales fuera de SIGA | Alta | T1, T3, T7, T8 | #4, #5, #6, #14 | P2, P4 |
| H4 Cruce manual PAT | Media | T5 | #17 | P7 |
| H5 Correo uno a uno | Media | T6, T8 | #1, #2, #8 | — |
| H1 SIGA sin API | Media | T7 | #3, #4 | — |

Las preguntas P1 a P7 están en [`06-normatividad/preguntas-cliente.md`](06-normatividad/preguntas-cliente.md). Quedan **pendientes para el tercer corte**, porque en este corte no fue posible consultar a la cliente ni a TI.
