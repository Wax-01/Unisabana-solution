<!--
Esta es la puerta de entrada de su repositorio. Complétela pensando en que la primera
persona que la abra puede ser alguien del área de negocio del cliente, no un técnico.
Evite jerga (TOGAF, ArchiMate, STRIDE, etc.) en esta parte — eso queda para las carpetas
técnicas de abajo.
-->

# Arquitectura Empresarial — [Nombre del Cliente]

**Equipo:** [AGY] · [Julian David Aguilar, Juan esteban Ramirez]
**Curso:** Arquitectura Empresarial — Universidad de La Sabana

---

## 📌 En una frase

[Ej: "Rediseñamos cómo Fundación Salud Viva conecta su app móvil, su ERP y su plataforma de telemedicina, para que la atención a pacientes sea más rápida y los datos clínicos queden protegidos."]

## 🩺 El problema

Hoy se tienen que manejar manualmente grandes cantidades de datos al momento de revisar la logistica de la encuesta anual de satisfaccion, en tareas repetitivas que consumen mucho tiempo y son propensas al error. 

## 💡 Lo que proponemos

[3-5 líneas o viñetas, en lenguaje de negocio, sin nombrar herramientas ni marcos técnicos. Ej:
- Integrar los tres sistemas para que la información del paciente se actualice en tiempo real en todos lados.
- Reforzar la protección de los datos clínicos según la normativa vigente.
- Un plan de implementación en fases, empezando por lo más urgente y de menor costo.]

## 🗺️ Cómo se implementa

Ver el **[Resumen Ejecutivo](resumen-ejecutivo.md)** — ahí está el detalle de beneficios esperados, fases de implementación y tiempos, en un solo documento pensado para el negocio, no para el equipo técnico.

## 📂 Si quiere ver el detalle técnico completo

Todo el análisis que sustenta esta propuesta está documentado carpeta por carpeta, siguiendo el método usado durante el proyecto:

| Carpeta | Qué contiene |
|---|---|
| `00-preliminary-vision/` | Contexto del cliente y visión de la solución |
| `01-bpmn/` | Cómo funciona hoy el proceso de negocio analizado |
| `02-modelo-informacion/` | Qué información maneja el negocio y cómo fluye |
| `03-arquitectura-c4/` | Los sistemas actuales y cómo están construidos |
| `04-infraestructura/` | Dónde corre todo hoy y qué riesgos técnicos tiene |
| `05-seguridad-stride/` | Análisis de seguridad de la información |
| `06-normatividad/` | Cumplimiento legal y normativo |
| `07-opportunities-solutions/` | La solución propuesta y qué brechas cierra |
| `08-integracion-vistas/` | Cómo se conecta todo lo anterior en una sola arquitectura |
| `09-presentacion-final/` | Presentación ejecutiva, plan de implementación y gobernanza |

## 👥 Contacto

Julian David Aguilar Zambrano
Julianagza@unisabana
