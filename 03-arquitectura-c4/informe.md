# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 3 - Arquitectura Actual del Sistema con el Modelo C4_

## 👥 Integrantes del equipo
- Julian David Aguilar 
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo

El objetivo de este taller fue representar, con las vistas **C1 (Contexto)** y **C2 (Contenedores)** del modelo C4, la arquitectura del sistema que nuestro cliente real — la **Universidad de La Sabana**, a través de la Vicerrectoría de Desarrollo — necesita para automatizar la logística de su encuesta anual de satisfacción estudiantil.

Este taller es la continuación directa de los talleres previos hechos con el mismo cliente:
- **Taller 0** (ficha de caracterización y visión) identificó el problema: la programación de horarios para aplicar la encuesta y el envío de notificaciones a profesores se hace manualmente, es repetitivo y propenso a errores, y la solución debe construirse solo con herramientas ya aprobadas por la universidad (Power Automate, Office 365, Power BI).
- **Taller 1** (BPMN) modeló el proceso con tres actores (Coordinadora, SIGA, Profesor) y dejó explícito que SIGA es un proveedor pasivo de información, y que el profesor conserva la autoridad de aprobar o rechazar la aplicación de la encuesta en su horario.
- **Taller 2** (modelo de información) identificó las seis entidades centrales (Encuesta, Programación, Estudiante, Salón, Profesor, Notificación) y las responsabilidades del sistema: recibir criterios, consultar disponibilidad, programar, notificar con una semana de antelación y registrar respuestas.

Este taller traduce esos hallazgos a un nivel de abstracción C4: primero se practicó la metodología con el caso base de clase (RedExpress) y luego se aplicó al cliente real.

## 🔧 Proceso de desarrollo

1. Se estudió la [guía paso a paso del taller](../clase/guia_paso_a_paso_c4.md) y se practicó la metodología de 4 pasos por vista sobre RedExpress en la sesión de clase (ver [`clase/notas.md`](../clase/notas.md) y los borradores en `clase/*.drawio`).
2. Para el cliente real, se revisaron los tres entregables previos (`00-preliminary-vision`, `01-bpmn`, `02-modelo-informacion`) para extraer actores, sistemas y responsabilidades ya validadas, en vez de volver a levantarlas desde cero.
3. **C1**: se definió el sistema en alcance como el "Sistema de Automatización de Logística de Encuestas de Satisfacción" (una sola caja). Se identificaron tres actores (Coordinadora de Encuestas, Profesor, Estudiante PAT) y dos sistemas externos que el equipo no controla: **SIGA** (plataforma académica institucional que provee horarios y disponibilidad) y el **Correo Institucional** (Exchange Online, usado para notificar).
4. **C2**: se decidió que, dado que la solución está restringida a herramientas Microsoft ya aprobadas por la universidad, los contenedores naturales son flujos de **Power Automate** (programación y notificación), formularios de **Microsoft Forms** (configuración de criterios y aplicación de la encuesta), un repositorio de datos en **SharePoint List/Excel Online** (infraestructura) y un **Power BI** de seguimiento — en vez de proponer una arquitectura de microservicios ajena a las restricciones del cliente.
5. Se etiquetó cada relación con el mecanismo real de comunicación entre servicios Microsoft 365 (conectores REST, Exchange/SMTP), y se validaron ambas vistas contra la [checklist de autoevaluación](../clase/guia_paso_a_paso_c4.md#checklist-de-autoevaluación-antes-de-entregar).
6. Herramienta usada: **draw.io**, exportado como `.drawio` para conservar la edición nativa de los diagramas.

## 🧩 Análisis del modelo propuesto

- **Estructura del modelo**: el C1 deja el sistema como una sola caja frente a sus tres actores y dos integraciones externas, sin exponer todavía la decisión de implementación. El C2 desglosa esa caja en 5 contenedores + 1 infraestructura compartida, cada uno con una responsabilidad separada (captura de criterios, orquestación/programación, notificación, captura de respuestas, reporting), evitando el error común de un "contenedor que hace de todo".
- **Cómo representa las necesidades del cliente**: la decisión de modelar los contenedores como flujos de Power Automate y formularios de Microsoft Forms —en vez de servicios custom— refleja directamente el requisito del cliente de usar únicamente herramientas ya aprobadas por la universidad (ver `00-preliminary-vision/ficha_caracterizacion.md`). El flujo de notificación con respuesta del profesor (`Responde aprobación/rechazo`) traduce al C2 la compuerta de decisión "¿Acepta?" que el equipo ya había modelado en BPMN.
- **Supuestos tomados**:
  - Se asume que SIGA expone algún mecanismo de consulta (API o extracción periódica) accesible desde Power Automate; no se tiene aún confirmación técnica de este acceso, por lo que queda documentado como riesgo a validar con el área de TI de la universidad.
  - Se asume que la aplicación de la encuesta al estudiante se realiza mediante un formulario de Microsoft Forms distribuido junto con la notificación, ya que el modelo de información previo señala "registrar respuestas de estudiantes" como responsabilidad del sistema sin especificar el canal.
  - El repositorio de programación se modela como infraestructura compartida (SharePoint List/Excel Online) y no como un contenedor de aplicación, porque no expone lógica propia — solo almacena datos que los demás contenedores leen y escriben.

## 📈 Diagrama final entregado

- [`c1-contexto-final.drawio`](c1-contexto-final.drawio) — Vista de Contexto (C1) del Sistema de Automatización de Logística de Encuestas.
- [`c2-contenedores-final.drawio`](c2-contenedores-final.drawio) — Vista de Contenedores (C2) del mismo sistema.

Ambos archivos se abren con [draw.io / diagrams.net](https://app.diagrams.net/) (File → Open From → Device).

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Coordinadora de Encuestas | Actor | Define criterios y parámetros de la encuesta (fechas, muestra) | Vicerrectoría de Desarrollo (Johanna Molina) |
| Profesor | Actor | Recibe notificación y aprueba/ajusta la aplicación en su horario | Facultades |
| Estudiante PAT | Actor | Diligencia la encuesta en el horario asignado | Estudiantes participantes |
| Sistema de Automatización de Logística de Encuestas | Sistema en alcance | Sistema propuesto por el equipo (C1) | Equipo del taller |
| SIGA | Sistema externo | Provee horarios de clase y disponibilidad de estudiantes | Dirección de TI - Unisabana |
| Correo Institucional (Exchange Online) | Sistema externo | Canal de entrega de notificaciones | Dirección de TI - Unisabana |
| Formulario de Configuración | Contenedor (Microsoft Forms/SharePoint List) | Captura de criterios de la coordinadora | Equipo del taller |
| Flujo de Programación | Contenedor (Power Automate) | Cruza disponibilidad y genera la programación | Equipo del taller |
| Flujo de Notificación | Contenedor (Power Automate) | Notifica a profesores y recoge su respuesta | Equipo del taller |
| Formulario de Encuesta | Contenedor (Microsoft Forms) | Captura las respuestas del estudiante | Equipo del taller |
| Dashboard de Seguimiento | Contenedor (Power BI) | Métricas de participación y avance | Equipo del taller |
| Repositorio de Programación | Infraestructura (SharePoint List / Excel Online) | Almacena criterios, programación y resultados | Equipo del taller |

## 🔍 Investigación complementaria

### Tema investigado:
Arquitecturas de automatización sobre Microsoft Power Platform en instituciones de educación superior, y su representación con el modelo C4.

### Resumen:
El modelo C4 fue diseñado originalmente pensando en arquitecturas de software a medida (microservicios, SPAs, bases de datos propias), por lo que aplicarlo a una solución basada en Power Automate/SharePoint/Power BI exige un ajuste de vocabulario: cada "contenedor" no es un servicio desplegado por el equipo, sino un artefacto configurado dentro de un mismo tenant de Microsoft 365 (un flujo, una lista, un dashboard). Esta decisión es consistente con guías de referencia de Microsoft sobre la arquitectura de soluciones en Power Platform, que recomiendan documentar cada flujo y cada conector como un componente independiente con una responsabilidad única, incluso cuando todos corren sobre la misma plataforma — exactamente el mismo principio que persigue el C2 de C4 al pedir "responsabilidades separadas, no un contenedor que hace de todo".

En el sector educativo, este patrón (automatizar procesos administrativos de bajo volumen y alto costo manual —como programaciones y notificaciones— con herramientas *low-code* ya licenciadas institucionalmente) es común en universidades que buscan evitar el costo y el riesgo de mantenimiento de desarrollos a medida, priorizando en cambio gobernanza sobre datos (quién puede leer/escribir el repositorio de programación) y trazabilidad de las aprobaciones (por qué se documentó explícitamente la respuesta del profesor como una relación de vuelta hacia el Flujo de Notificación, reflejando la compuerta de decisión ya identificada en el BPMN del Taller 1).

## 📚 Referencias

Ver [`referencias.md`](referencias.md) para el listado completo de fuentes consultadas.

---

_Este documento hace parte de la entrega del Taller 3 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
