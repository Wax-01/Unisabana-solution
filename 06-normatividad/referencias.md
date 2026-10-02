# 📚 Referencias Bibliográficas del Taller

Este archivo contiene las fuentes consultadas para el desarrollo del taller, tanto para el componente técnico como para la investigación complementaria.

## 🔖 Taller
_Taller 6 - Checklist de Cumplimiento Normativo — Aplicación al cliente real (Universidad de La Sabana, proceso de automatización de encuestas de satisfacción)_

---

## 🏛️ Contexto del cliente

El cliente real de este proyecto es la **Vicerrectoría de Desarrollo de la Universidad de La Sabana** (Coordinación de Experiencia y Servicio). El proceso a automatizar cubre tres tipos de datos/comunicaciones sensibles:

1. **Horarios de los estudiantes**, usados para programar la aplicación de la encuesta de satisfacción anual.
2. **Encuestas de satisfacción**, con las respuestas de estudiantes y docentes.
3. **Correos institucionales**, usados para notificar obligatoriamente a los profesores antes de que inicien las encuestas.

La solución debe apoyarse únicamente en herramientas ya autorizadas por la Universidad (Office 365 / Power Automate / Power BI), lo que también trae consigo obligaciones de cumplimiento propias de ese proveedor.

---

## 📚 Referencias utilizadas

### Normativa nacional (Colombia)

1. Congreso de la República de Colombia. *Constitución Política de Colombia*, Art. 15 (derecho al Habeas Data y a la intimidad). 1991.
2. Congreso de la República de Colombia. *Ley 1581 de 2012, "Por la cual se dictan disposiciones generales para la protección de datos personales"*. Diario Oficial No. 48.587. [Función Pública](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981). Fecha de consulta: 26/09/2026.
3. Presidencia de la República de Colombia. *Decreto 1377 de 2013*, reglamentario de la Ley 1581 de 2012, compilado actualmente en el *Decreto Único Reglamentario 1074 de 2015* (Título 2, Capítulos 25-26, Sector Comercio, Industria y Turismo). [Función Pública](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=77067). Fecha de consulta: 26/09/2026.
4. Presidencia de la República de Colombia. *Decreto 886 de 2014*, por el cual se reglamenta el Registro Nacional de Bases de Datos (RNBD). [Superintendencia de Industria y Comercio](https://www.sic.gov.co/registro-nacional-de-bases-de-datos). Fecha de consulta: 26/09/2026.
5. Superintendencia de Industria y Comercio (SIC). *Circular Externa No. 002 de 2015* y guías de responsabilidad demostrada (*accountability*) en el tratamiento de datos personales. [sic.gov.co](https://www.sic.gov.co). Fecha de consulta: 26/09/2026.
6. Congreso de la República de Colombia. *Ley 1273 de 2009, "Ley de Delitos Informáticos"* (Arts. 269A-269J: protección de la información, los datos y la confidencialidad de las comunicaciones electrónicas) — aplica directamente al uso del correo institucional en el flujo de notificación a profesores.
7. Congreso de la República de Colombia. *Ley 1266 de 2008* (Habeas Data financiero) — marco complementario de referencia sobre administración de bases de datos personales, aunque su aplicación principal es al sector financiero/crediticio.

### Normativa y documentos institucionales — Universidad de La Sabana

8. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (Versión 5.0), aprobada por la Comisión de Asuntos Generales del Consejo Superior, en cumplimiento de la Ley 1581 de 2012. [unisabana.edu.co/politica-de-proteccion-de-datos](https://www.unisabana.edu.co/politica-de-proteccion-de-datos). Fecha de consulta: 26/09/2026.
9. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (documento completo, PDF). [Dirección de Publicaciones Unisabana](https://publicaciones.unisabana.edu.co/politica-de-tratamiento-de-datos-personales-universidad-de-la-sabana/). Fecha de consulta: 26/09/2026. *(Nota: el enlace directo al PDF no fue accesible desde este entorno; se recomienda verificar la versión vigente directamente en el portal antes de la entrega final).*
10. Universidad de La Sabana. *Reglamento de Estudiantes de Pregrado*, Resolución N.° 485 del 19 de noviembre de 2003 y sus modificaciones — capítulo de Derechos y Deberes de los Estudiantes, que reconoce el derecho a la confidencialidad de los datos personales e historia académica del estudiante, y el deber de mantener actualizada su información en los sistemas institucionales. [unisabana.edu.co/nosotros/reglamento-de-estudiantes/pregrado](https://www.unisabana.edu.co/nosotros/reglamento-de-estudiantes/pregrado). Fecha de consulta: 26/09/2026.
11. Universidad de La Sabana. *Reglamento de Estudiantes de Posgrado*. [unisabana.edu.co/nosotros/reglamento-de-estudiantes/posgrado](https://www.unisabana.edu.co/nosotros/reglamento-de-estudiantes/posgrado). Fecha de consulta: 26/09/2026.
12. Universidad de La Sabana. *Código de Ética y Buen Gobierno*. Listado en [Documentos Institucionales](https://www.unisabana.edu.co/nosotros/documentos-institucionales). Fecha de consulta: 26/09/2026.
13. Universidad de La Sabana. *Lineamientos para el uso de la Inteligencia Artificial Generativa* — relevante si el flujo de Power Automate llega a incorporar componentes de IA generativa. Listado en [Documentos Institucionales](https://www.unisabana.edu.co/nosotros/documentos-institucionales). Fecha de consulta: 26/09/2026.
14. Universidad de La Sabana. Canales oficiales para ejercicio de derechos de protección de datos: `protecciondedatos@unisabana.edu.co` (solicitudes de habeas data) y `notificacioneslegales@unisabana.edu.co` (notificaciones legales), referenciados en la Política de Tratamiento de Datos Personales.

### Estándares y marcos técnicos de referencia

15. International Organization for Standardization. *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection — Information security management systems — Requirements*.
16. Microsoft. *Microsoft Trust Center / Documentación de cumplimiento de Microsoft 365 y Power Automate* (procesamiento de datos de M365, DLP, retención) — aplica porque el cliente exige que la automatización use exclusivamente herramientas ya autorizadas (Office 365, Power Automate). [learn.microsoft.com/power-automate](https://learn.microsoft.com/power-automate/). Fecha de consulta: 26/09/2026.

### Documento completo de la política institucional y acreditación (usados para completar el checklist)

18. Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (documento completo, vigente desde el 19 de agosto de 2013). Dirección de Publicaciones. [editorial.unisabana.edu.co/wp-content/uploads/2016/04/Tratamiento-datos.pdf](https://editorial.unisabana.edu.co/wp-content/uploads/2016/04/Tratamiento-datos.pdf). Fecha de consulta: 02/10/2026. *(Esta vez sí se pudo leer el documento completo; reemplaza la nota de acceso fallido de la referencia 9.)*
19. Consejo Nacional de Acreditación (CNA) / Consejo Nacional de Educación Superior (CESU). *Lineamientos y aspectos por evaluar para la acreditación en alta calidad de los programas académicos, las unidades académicas y las instituciones de educación superior* (Acuerdo 01 de 2025 CESU), aprobado el 16 de diciembre de 2025 — usado para fundamentar la categoría "Aseguramiento de la Calidad (CNA)" del checklist, dado que la encuesta es insumo del proceso de acreditación institucional (ver informes de los Talleres 5 y 7).

### Fuente asistida por IA
20. Fuente asistida por IA: Claude (Anthropic, modelo Sonnet 5), septiembre-octubre 2026 — usada para localizar y resumir las fuentes normativas anteriores; toda cita legal/institucional fue verificada contra la fuente primaria enlazada.

---

## 🧭 Mapa preliminar: dato/proceso del cliente → normativa aplicable

Este mapa es el insumo para el **Paso 1** de la metodología (ver [guía paso a paso](../clase/guia_paso_a_paso_normatividad.md)) aplicado al cliente. Aún debe validarse con el cliente cuál de estos controles existe realmente hoy en el proceso (evaluación Cumple/Parcial de los Pasos 3-5).

| Dato / Proceso del cliente | Sensibilidad | Normativa aplicable |
|---|---|---|
| Horarios de estudiantes (usados para programar la aplicación de encuestas) | Dato académico / personal | Ley 1581 de 2012; Reglamento de Estudiantes (confidencialidad de datos e historia académica); Política de Tratamiento de Datos Personales Unisabana |
| Respuestas de la encuesta de satisfacción (estudiantes y docentes) | Dato personal (opiniones/percepciones; podría volverse sensible si se cruza con datos de salud, creencias o discapacidad) | Ley 1581 de 2012 (finalidad y consentimiento); Política institucional de tratamiento de datos |
| Correos institucionales de notificación obligatoria a profesores | Dato de contacto / comunicación institucional | Ley 1273 de 2009 (protección de la información y confidencialidad de comunicaciones electrónicas); no se halló un reglamento público específico de uso del correo institucional |
| Flujo automatizado end-to-end en Power Automate (integra horarios + correos + encuestas) | Sistema de tratamiento automatizado de datos personales | ISO/IEC 27001; Decreto 886 de 2014 (Registro Nacional de Bases de Datos); documentación de cumplimiento de Microsoft 365 / Power Automate |

---

## 📌 Recomendaciones

- Usa formato APA o IEEE para citar.
- No incluyas fuentes como Wikipedia si hay mejores alternativas.
- Si usas inteligencia artificial para redactar o investigar, cítalo como "Fuente asistida por IA: ChatGPT, julio 2025".

---

_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._
