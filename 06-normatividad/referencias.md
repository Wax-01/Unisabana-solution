# 📚 Referencias Bibliográficas del Taller

Este archivo contiene las fuentes consultadas para el desarrollo del taller, tanto para el componente técnico como para la investigación complementaria.

## 🔖 Taller
_Taller 6 - Checklist de Cumplimiento Normativo — Aplicación al cliente real (Universidad de La Sabana, proceso de automatización de encuestas de satisfacción)_

---

## 🏛️ Contexto del cliente

El cliente real de este proyecto es la **Vicerrectoría de Desarrollo de la Universidad de La Sabana** (Coordinación de Experiencia y Servicio). El checklist evalúa el proceso **actual** de logística de la encuesta, que trata tres tipos de datos:

1. **Datos de estudiantes y profesores exportados de SIGA** (nombres, correos, programas, horarios), que se copian a la Hoja de Muestreo y a la Hoja de Asignación PAT en OneDrive y quedan como archivos descargados en el equipo de la coordinadora.
2. **Horarios y disponibilidad de los estudiantes PAT**, usados para asignar quién aplica la encuesta en cada clase.
3. **Correos institucionales** con los que se avisa a cada profesor y se reciben sus respuestas.

Todo el proceso usa herramientas institucionales (SIGA, Excel en OneDrive, Exchange Online), lo que trae las obligaciones de la política de datos de la universidad y las de Microsoft como Encargado del tratamiento.

---

## 📚 Referencias utilizadas

### Normativa nacional (Colombia)

1. Congreso de la República de Colombia. *Constitución Política de Colombia*, Art. 15 (derecho al Habeas Data y a la intimidad). 1991.
2. Congreso de la República de Colombia. *Ley 1581 de 2012, "Por la cual se dictan disposiciones generales para la protección de datos personales"*. Diario Oficial No. 48.587. [Función Pública](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981). Fecha de consulta: 26/09/2026.
3. Presidencia de la República de Colombia. *Decreto 1377 de 2013*, reglamentario de la Ley 1581 de 2012, compilado actualmente en el *Decreto Único Reglamentario 1074 de 2015* (Título 2, Capítulos 25-26, Sector Comercio, Industria y Turismo). [Función Pública](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=77067). Fecha de consulta: 26/09/2026.
4. Presidencia de la República de Colombia. *Decreto 886 de 2014*, por el cual se reglamenta el Registro Nacional de Bases de Datos (RNBD). [Superintendencia de Industria y Comercio](https://www.sic.gov.co/registro-nacional-de-bases-de-datos). Fecha de consulta: 26/09/2026.
5. Superintendencia de Industria y Comercio (SIC). *Circular Externa No. 002 de 2015* y guías de responsabilidad demostrada (*accountability*) en el tratamiento de datos personales. [sic.gov.co](https://www.sic.gov.co). Fecha de consulta: 26/09/2026.
6. Congreso de la República de Colombia. *Ley 1273 de 2009, "Ley de Delitos Informáticos"* (Arts. 269A-269J: protección de la información, los datos y la confidencialidad de las comunicaciones electrónicas) — aplica al uso del correo institucional para avisar a los profesores.
7. Congreso de la República de Colombia. *Ley 1266 de 2008* (Habeas Data financiero) — marco complementario de referencia sobre administración de bases de datos personales, aunque su aplicación principal es al sector financiero/crediticio.

### Normativa y documentos institucionales — Universidad de La Sabana

8. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (Versión 5.0), aprobada por la Comisión de Asuntos Generales del Consejo Superior, en cumplimiento de la Ley 1581 de 2012. [unisabana.edu.co/politica-de-proteccion-de-datos](https://www.unisabana.edu.co/politica-de-proteccion-de-datos). Fecha de consulta: 26/09/2026.
9. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (documento completo, PDF). [Dirección de Publicaciones Unisabana](https://publicaciones.unisabana.edu.co/politica-de-tratamiento-de-datos-personales-universidad-de-la-sabana/). Fecha de consulta: 26/09/2026. *(Nota: el enlace directo al PDF no fue accesible desde este entorno; se recomienda verificar la versión vigente directamente en el portal antes de la entrega final).*
10. Universidad de La Sabana. *Reglamento de Estudiantes de Pregrado*, Resolución N.° 485 del 19 de noviembre de 2003 y sus modificaciones — capítulo de Derechos y Deberes de los Estudiantes, que reconoce el derecho a la confidencialidad de los datos personales e historia académica del estudiante, y el deber de mantener actualizada su información en los sistemas institucionales. [unisabana.edu.co/nosotros/reglamento-de-estudiantes/pregrado](https://www.unisabana.edu.co/nosotros/reglamento-de-estudiantes/pregrado). Fecha de consulta: 26/09/2026.
11. Universidad de La Sabana. *Reglamento de Estudiantes de Posgrado*. [unisabana.edu.co/nosotros/reglamento-de-estudiantes/posgrado](https://www.unisabana.edu.co/nosotros/reglamento-de-estudiantes/posgrado). Fecha de consulta: 26/09/2026.
12. Universidad de La Sabana. *Código de Ética y Buen Gobierno*. Listado en [Documentos Institucionales](https://www.unisabana.edu.co/nosotros/documentos-institucionales). Fecha de consulta: 26/09/2026.
13. Universidad de La Sabana. *Lineamientos para el uso de la Inteligencia Artificial Generativa* — relevante si la solución propuesta (Taller 7) llega a incorporar IA generativa. Listado en [Documentos Institucionales](https://www.unisabana.edu.co/nosotros/documentos-institucionales). Fecha de consulta: 26/09/2026.
14. Universidad de La Sabana. Canales oficiales para ejercicio de derechos de protección de datos: `protecciondedatos@unisabana.edu.co` (solicitudes de habeas data) y `notificacioneslegales@unisabana.edu.co` (notificaciones legales), referenciados en la Política de Tratamiento de Datos Personales.

### Estándares y marcos técnicos de referencia

15. International Organization for Standardization. *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection — Information security management systems — Requirements*.
16. Microsoft. *Microsoft Trust Center / Documentación de cumplimiento de Microsoft 365 y Power Automate* (procesamiento de datos de M365, DLP, retención) — aplica porque las hojas y los correos del proceso viven en el tenant Microsoft 365 de la universidad. [learn.microsoft.com/power-automate](https://learn.microsoft.com/power-automate/). Fecha de consulta: 26/09/2026.

### Documento completo de la política institucional y acreditación (usados para completar el checklist)

17. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (documento completo, vigente desde el 19 de agosto de 2013). Dirección de Publicaciones. [editorial.unisabana.edu.co/wp-content/uploads/2016/04/Tratamiento-datos.pdf](https://editorial.unisabana.edu.co/wp-content/uploads/2016/04/Tratamiento-datos.pdf). Fecha de consulta: 02/10/2026. *(Esta vez sí se pudo leer el documento completo; reemplaza la nota de acceso fallido de la referencia 9.)*
18. Consejo Nacional de Acreditación (CNA) / Consejo Nacional de Educación Superior (CESU). *Lineamientos y aspectos por evaluar para la acreditación en alta calidad de los programas académicos, las unidades académicas y las instituciones de educación superior* (Acuerdo 01 de 2025 CESU), aprobado el 16 de diciembre de 2025 — usado para fundamentar la categoría "Aseguramiento de la Calidad (CNA)" del checklist, dado que la encuesta es insumo del proceso de acreditación institucional (ver informe del Taller 6).

### Fuente asistida por IA
19. Fuente asistida por IA: Claude (Anthropic, modelo Sonnet 5), septiembre-octubre 2026 — usada para localizar y resumir las fuentes normativas anteriores; toda cita legal/institucional fue verificada contra la fuente primaria enlazada.

---

## 🧭 Mapa preliminar: dato/proceso del cliente → normativa aplicable

Este mapa es el insumo para el **Paso 1** de la metodología (ver la [guía paso a paso](https://github.com/Wax-01/Taller-Normatividad/blob/main/clase/guia_paso_a_paso_normatividad.md)) aplicado al cliente. Los controles que no se pudieron verificar quedaron como preguntas en [`preguntas-cliente.md`](preguntas-cliente.md).

| Dato / Proceso del cliente | Sensibilidad | Normativa aplicable |
|---|---|---|
| Horarios de estudiantes (usados para programar la aplicación de encuestas) | Dato académico / personal | Ley 1581 de 2012; Reglamento de Estudiantes (confidencialidad de datos e historia académica); Política de Tratamiento de Datos Personales Unisabana |
| Respuestas de la encuesta de satisfacción (estudiantes y docentes) | Dato personal (opiniones/percepciones; podría volverse sensible si se cruza con datos de salud, creencias o discapacidad) | Ley 1581 de 2012 (finalidad y consentimiento); Política institucional de tratamiento de datos |
| Correos institucionales de notificación obligatoria a profesores | Dato de contacto / comunicación institucional | Ley 1273 de 2009 (protección de la información y confidencialidad de comunicaciones electrónicas); no se halló un reglamento público específico de uso del correo institucional |
| Copias de datos de SIGA en la Hoja de Muestreo, la Hoja de Asignación PAT (OneDrive) y en archivos exportados en el equipo de la coordinadora | Datos personales fuera del sistema de origen | Ley 1581 de 2012 (acceso y circulación restringida, seguridad); Política institucional, Num. 4-a y Num. 9; Decreto 886 de 2014 (RNBD); ISO/IEC 27001 |

---


_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._
