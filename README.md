# Arquitectura Empresarial — Universidad de La Sabana (Vicerrectoría de Desarrollo)

**Equipo:** AGY · Julian David Aguilar, Juan Esteban Ramirez
**Cliente:** Johanna Andrea Molina Rodriguez — Coordinadora de experiencia y servicio, Vicerrectoría de Desarrollo
**Curso:** Arquitectura Empresarial — Universidad de La Sabana

---

## 📌 En una frase

Rediseñamos cómo se organiza la encuesta anual de autosatisfacción para que programar las clases, avisar a los profesores y recoger sus respuestas deje de ser un trabajo manual y repetitivo, y los datos de estudiantes y profesores queden mejor protegidos.

## 🩺 El problema

Hoy se tienen que manejar manualmente grandes cantidades de datos al revisar la logística de la encuesta anual de satisfacción, en tareas repetitivas que consumen mucho tiempo y son propensas al error.

En la práctica, el proceso funciona así:

- La coordinadora consulta en el sistema académico los horarios de estudiantes y profesores, sus correos y sus datos personales.
- Con esa información arma en hojas de cálculo la muestra de estudiantes (por programa y semestre) y cruza a mano la disponibilidad de los estudiantes PAT con los horarios de clase.
- Avisa a cada profesor por correo, uno a uno. Si un profesor no puede ceder su clase, hay que empezar de nuevo.

Esto genera demoras, errores de cruce, profesores que pueden quedar sin avisar, datos personales copiados en archivos sin control y un proceso que depende de una sola persona.

## 💡 Lo que proponemos

- **Automatizar el cruce de horarios y la selección de clases**, para que la muestra por programa y semestre se arme sola en lugar de a mano.
- **Avisar a todos los profesores automáticamente** y permitirles aceptar o rechazar con un solo clic, de modo que ninguna clase se use sin que su profesor lo sepa.
- **Reprogramar automáticamente** cuando un profesor rechaza, sin que la coordinadora tenga que empezar de cero.
- **Guardar los datos en un lugar seguro y con permisos por rol**, en lugar de hojas de cálculo sueltas, cumpliendo la ley de protección de datos personales.
- Todo con las herramientas que la universidad ya tiene autorizadas, sin contratar plataformas externas.

## 🗺️ Cómo se implementa

El detalle de beneficios esperados, fases y tiempos estará en el **Resumen Ejecutivo** (en preparación).

Mientras tanto, la propuesta de mejora y su priorización están en [`07-opportunities-solutions/mejora-arquitectura.md`](07-opportunities-solutions/mejora-arquitectura.md).

## 📂 Si quiere ver el detalle técnico completo

Todo el análisis que sustenta esta propuesta está documentado carpeta por carpeta, siguiendo el método usado durante el proyecto:

| Carpeta | Qué contiene | Estado |
|---|---|---|
| [`00-preliminary-vision/`](00-preliminary-vision/) | Contexto del cliente y visión de la solución | Disponible |
| [`01-bpmn/`](01-bpmn/) | Cómo funciona hoy el proceso de negocio analizado | Disponible |
| [`02-modelo-informacion/`](02-modelo-informacion/) | Qué información maneja el negocio y cómo fluye | Disponible |
| [`03-arquitectura-c4/`](03-arquitectura-c4/) | Los sistemas y cómo se conectan | Disponible |
| [`04-infraestructura/`](04-infraestructura/) | Dónde corre todo hoy y qué riesgos técnicos tiene | Disponible |
| [`05-seguridad-stride/`](05-seguridad-stride/) | Análisis de seguridad de la información | Disponible |
| `06-normatividad/` | Cumplimiento legal y normativo | En preparación |
| [`07-opportunities-solutions/`](07-opportunities-solutions/) | La solución propuesta y qué brechas cierra | Disponible |
| `08-integracion-vistas/` | Cómo se conecta todo lo anterior en una sola arquitectura | En preparación |
| `09-presentacion-final/` | Presentación ejecutiva, plan de implementación y gobernanza | En preparación |

## 👥 Contacto

- Julian David Aguilar Zambrano — Julianagza@unisabana.edu.co
- Juan Esteban Ramirez — juanramher@unisabana.edu.co
