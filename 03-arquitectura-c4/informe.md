# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 3 - Arquitectura Actual del Sistema con el Modelo C4_

## 👥 Integrantes del equipo
- Julian David Aguilar 
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo

El objetivo de este taller fue representar, con las vistas **C1 (Contexto)** y **C2 (Contenedores)** del modelo C4, la **arquitectura actual (AS-IS)** con la que la **Vicerrectoría de Desarrollo de la Universidad de La Sabana** gestiona hoy la logística de la encuesta anual de autosatisfacción: cómo arma la muestra, cómo asigna a los estudiantes PAT a las clases y cómo avisa a los profesores.

Hoy no existe una aplicación para este proceso. El "sistema" es un conjunto de herramientas operadas a mano por la coordinadora: exporta datos de **SIGA**, los trabaja en **dos hojas de Excel guardadas en OneDrive** y avisa a cada profesor por **correo institucional**, uno a uno. Eso es lo que se modela aquí.

> **Corrección del Corte 2.** La primera versión de este taller modelaba la solución que el equipo propone (Microsoft Forms, Power Automate, SharePoint y Power BI), que todavía no existe. Esa versión se conserva como vista TO-BE en [`07-opportunities-solutions/c1-contexto-to-be-v1.drawio`](../07-opportunities-solutions/c1-contexto-to-be-v1.drawio) y [`c2-contenedores-to-be-v1.drawio`](../07-opportunities-solutions/c2-contenedores-to-be-v1.drawio).

Este taller continúa los talleres previos con el mismo cliente:
- **Taller 0** (ficha de caracterización): el problema es el manejo manual de grandes volúmenes de datos en tareas repetitivas y propensas al error; la restricción es usar solo herramientas autorizadas por la universidad.
- **Taller 1** (BPMN): tres participantes (Coordinadora, SIGA, Profesor). SIGA es un proveedor pasivo de información y el profesor decide si cede su clase.
- **Taller 2** (modelo de información): entidades Encuesta, Programación, Estudiante, Salón, Profesor y Notificación. Hoy esas entidades viven en las dos hojas de Excel.

## 🔧 Proceso de desarrollo

1. Se estudió la [guía paso a paso del taller](https://github.com/Wax-01/Taller-Arquitectura/blob/main/clase/guia_paso_a_paso_c4.md) y se practicó la metodología de 4 pasos por vista sobre el caso RedExpress (notas y borradores en la carpeta `clase/` del [repositorio del taller](https://github.com/Wax-01/Taller-Arquitectura)).
2. Para el cliente se tomaron los actores, sistemas y herramientas ya confirmados en los talleres 0, 1 y 4, en lugar de volver a levantarlos.
3. **C1**: el sistema en alcance es la **gestión manual de la logística de la encuesta** (una sola caja). Actores: la coordinadora, el estudiante PAT y el profesor. Sistemas externos que la Vicerrectoría no controla: **SIGA** y el **correo institucional (Exchange Online)**.
4. **C2**: se abrió la caja en los dos contenedores de datos que existen hoy, la **Hoja de Muestreo** y la **Hoja de Asignación PAT** (libros de Excel en OneDrive). Cada relación indica el mecanismo real: exportación manual CSV/Excel desde SIGA, edición de Excel por HTTPS y correo escrito a mano en Outlook.
5. Se revisó que los nombres de los contenedores y sistemas externos fueran idénticos a los del mapa de infraestructura (Taller 4), el DFD (Taller 5) y el checklist (Taller 6). Ver la [tabla de trazabilidad](../trazabilidad.md).
6. Herramienta usada: **draw.io**, exportado como `.drawio`.

## 🧩 Análisis del modelo propuesto

- **Estructura del modelo**: el C1 muestra el proceso como una sola caja frente a tres actores y dos sistemas externos. El C2 abre esa caja en dos contenedores con responsabilidades distintas: la Hoja de Muestreo decide *a quién* se encuesta y la Hoja de Asignación PAT decide *en qué clase y con qué PAT*. No hay contenedores de aplicación (flujos, servicios, formularios) porque hoy no existen: toda la lógica la ejecuta la coordinadora a mano.
- **Cómo representa las necesidades del cliente**: el modelo deja a la vista los tres puntos manuales de la ficha de caracterización. Las relaciones punteadas son exactamente el trabajo repetitivo que la cliente quiere eliminar: la exportación desde SIGA, la copia entre hojas y el correo uno a uno. También muestra que los datos personales salen de SIGA y quedan copiados en las hojas, que es el punto de partida del análisis de seguridad (Taller 5) y de normatividad (Taller 6).
- **Papel de cada actor** (definición única para todos los talleres):
  - **Coordinadora de la encuesta**: opera todo el proceso. Exporta de SIGA, arma la muestra, asigna PAT a clases y escribe los correos.
  - **Estudiante PAT**: reporta su disponibilidad horaria y aplica la encuesta en el salón. No diseña la muestra ni responde la encuesta. Entra al C1 porque su disponibilidad es un insumo de la Hoja de Asignación PAT.
  - **Profesor**: recibe el aviso por correo y responde si cede o no su clase.
  - **Estudiantes encuestados**: no aparecen en el C1 porque responden la encuesta en el salón y no interactúan con las hojas ni con el correo del proceso. Sí aparecen en el mapa de infraestructura (Taller 4), que muestra a todos los participantes.
- **Supuestos tomados**:
  - SIGA no expone una API de integración conocida; los datos salen por consulta web y exportación a CSV/Excel (hallazgo H1 del Taller 4).
  - Las dos hojas viven en OneDrive. Según el Taller 4, la cuenta es la institucional de la coordinadora; con quién se comparten está pendiente (pregunta P2 de [`06-normatividad/preguntas-cliente.md`](../06-normatividad/preguntas-cliente.md)).
  - El canal por el que el PAT reporta su disponibilidad (correo, edición directa de la hoja u otro) no está confirmado (pregunta P7). En el C2 se dibuja como entrada a la Hoja de Asignación PAT.
  - El equipo de cómputo de la coordinadora no se dibuja en el C2 porque es infraestructura, no un contenedor. Aparece en el mapa del Taller 4.

## 📈 Diagrama final entregado

- [`c1-contexto-final.drawio`](c1-contexto-final.drawio): vista de contexto (C1) del proceso actual.
- [`c2-contenedores-final.drawio`](c2-contenedores-final.drawio): vista de contenedores (C2) del proceso actual.

Ambos archivos se abren con [draw.io / diagrams.net](https://app.diagrams.net/) (File → Open From → Device).

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Coordinadora de la encuesta | Actor | Opera todo el proceso: exporta de SIGA, arma la muestra, asigna PAT y avisa a los profesores | Vicerrectoría de Desarrollo (Johanna Molina) |
| Estudiante PAT | Actor | Reporta su disponibilidad horaria y aplica la encuesta en el salón | Estudiantes PAT |
| Profesor | Actor | Recibe el aviso por correo y acepta o rechaza ceder su clase | Facultades |
| Gestión manual de la logística de la encuesta | Sistema en alcance (AS-IS) | Proceso actual, operado a mano con Excel y correo | Vicerrectoría de Desarrollo |
| SIGA | Sistema externo | Fuente de horarios, programas y datos personales; sin API conocida, exportación manual | Dirección de TI - Unisabana |
| Correo institucional (Exchange Online) | Sistema externo | Canal por el que se avisa a cada profesor y se reciben sus respuestas | Dirección de TI - Unisabana |
| Hoja de Muestreo | Contenedor de datos (Excel en OneDrive) | Muestra de estudiantes por programa y semestre; contiene copias de datos personales de SIGA | Coordinadora de la encuesta |
| Hoja de Asignación PAT | Contenedor de datos (Excel en OneDrive) | Cruce de clases muestreadas con la disponibilidad de los PAT; lista de clases a notificar | Coordinadora de la encuesta |

## 🔍 Investigación complementaria

### Tema investigado:
Las hojas de cálculo como "sistema" de un proceso administrativo: qué riesgos documenta la literatura y cómo se representan en C4.

### Resumen:
El modelo C4 se pensó para software a medida, pero define un contenedor como "una aplicación o un almacén de datos" e incluye como ejemplos un esquema de base de datos o una carpeta en un sistema de archivos [1]. Eso permite modelar un proceso basado en hojas de cálculo: cada libro de Excel que guarda datos del proceso es un contenedor de datos, y los sistemas de los que se copia la información son sistemas externos [2]. Por eso el C2 no tiene contenedores de aplicación: no hay código, la lógica la ejecuta una persona.

La investigación sobre errores en hojas de cálculo respalda que esto se trate como un riesgo de arquitectura y no solo como una incomodidad. Panko [3] resume quince años de estudios: los errores en hojas de cálculo son frecuentes y significativos, se presentan en todos los grupos estudiados (estudiantes y profesionales) y la única técnica con efectividad demostrada para detectarlos es la revisión celda por celda. En este proceso, la Hoja de Asignación PAT se llena copiando datos a mano entre archivos, que es justo el tipo de operación donde se concentran esos errores (hallazgo H4 del Taller 4).

El segundo riesgo del modelo está en cómo se comparten los archivos. OneDrive permite enlaces de tipo "Cualquier persona", que funcionan para quien reciba el enlace aunque se reenvíe fuera de la organización, y enlaces de tipo "Personas de la organización", que dan acceso a cualquier usuario interno que tenga el enlace [4][5]. Como las dos hojas contienen datos personales copiados de SIGA, el tipo de enlace con el que se comparten define el alcance real de la exposición. Por eso esa pregunta quedó abierta con la cliente y es la amenaza T1 del Taller 5.

Por último, se buscó cómo han resuelto otras universidades este mismo patrón de hoja de cálculo más correo masivo. La Universidad Nacional de Singapur (NUS) documenta áreas administrativas que usan Power Automate para enviar correos masivos personalizados (por ejemplo, invitaciones con un adjunto distinto para cada destinatario) a partir de hojas de Excel, en lugar de enviarlos a mano. El equipo que lo implementó advierte que para que funcione la hoja de origen tiene que estar correcta [6]. Esto confirma que el punto de partida de cualquier mejora (Taller 7) es la calidad y el control de las dos hojas que este C2 modela.

## 📚 Referencias

Ver [`referencias.md`](referencias.md) para el listado completo de fuentes consultadas.

---

_Este documento hace parte de la entrega del Taller 3 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
