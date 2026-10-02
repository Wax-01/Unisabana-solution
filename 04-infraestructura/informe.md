# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 4 - Mapa de Infraestructura (AS-IS)

## 👥 Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo

El objetivo del taller es representar la infraestructura sobre la que hoy se ejecuta el proceso de logística de la encuesta anual de autosatisfacción de la Universidad de La Sabana: qué sistemas, herramientas y actores participan, dónde viven los datos y cómo viajan entre un punto y otro.

Es una vista **AS-IS**: documenta cómo funciona el proceso hoy, no cómo debería funcionar. Parte de los contenedores del C2 (Taller 3) y de los procesos del BPMN (Taller 1), pero baja un nivel hacia lo tecnológico: en lugar de preguntar "qué hace el sistema", pregunta "dónde y con qué se hace hoy". El resultado es la base sobre la que se hizo el análisis de seguridad (Taller 5) y sobre la que se construye la propuesta TO-BE (Taller 7).

## 🔧 Proceso de desarrollo

1. Se revisaron los entregables anteriores (`00-preliminary-vision`, `01-bpmn`, `03-arquitectura-c4`) para no volver a levantar actores y sistemas desde cero.
2. Se identificaron los componentes tecnológicos reales del proceso actual con la información entregada por la cliente: la coordinadora consulta en SIGA los horarios de estudiantes y profesores, sus correos y sus datos personales; con esa información arma en hojas de cálculo la muestra y la asignación de estudiantes PAT; y notifica a los profesores por correo institucional.
3. Se agruparon los componentes en zonas: sistemas institucionales, actores de gestión, proceso manual y actores de aplicación.
4. Se marcaron en rojo los componentes que representan un riesgo (fuente única de datos, hojas de cálculo sin control, envío de correos uno a uno).
5. Herramienta usada: **draw.io**, exportado como `mapa-final.drawio`.

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado

El mapa se organiza en cuatro zonas:

1. **Sistemas institucionales:** SIGA y su base de datos académica. Es la fuente de verdad de los horarios, los programas y los datos de estudiantes y profesores. No expone una API de integración conocida: la información sale por consulta directa o por exportación a CSV/Excel.
2. **Actores de gestión:** la coordinadora (Vicerrectoría de Desarrollo) y los estudiantes PAT. La coordinadora opera todo el proceso; los PAT aportan su disponibilidad.
3. **Proceso manual:** tres componentes que concentran el trabajo y el riesgo.
   - Hoja de cálculo de **muestreo** por programa y semestre.
   - Hoja de cálculo de **asignación de PAT a horarios de clase**.
   - **Correo institucional** usado para notificar a los profesores, enviado uno a uno.
4. **Actores de aplicación:** los profesores (reciben el aviso y ceden o no su espacio) y los estudiantes encuestados (muestra por programa y semestre).

El flujo principal es: SIGA exporta datos → la coordinadora los carga en las hojas de cálculo → se cruzan muestra, horarios y disponibilidad PAT → se genera la lista de clases → se notifica por correo a cada profesor → el profesor aplica la encuesta en su clase.

### Cómo representa las necesidades del cliente

El mapa hace visible el problema que la cliente describió en la ficha de caracterización: el manejo manual de grandes volúmenes de datos en tareas repetitivas, lentas y propensas al error. Todo el valor del proceso pasa por tres puntos manuales (dos hojas de cálculo y el envío de correos), y todos dependen de una única persona operando sobre exportaciones de SIGA. También muestra por qué la restricción de la cliente (usar solo herramientas autorizadas por la universidad) es compatible con la mejora: ya existen Office 365, Exchange y Power Automate en el entorno, solo que hoy no se aprovechan para este proceso.

### Hallazgos de infraestructura (riesgos del AS-IS)

| # | Componente | Hallazgo | Consecuencia |
|---|---|---|---|
| H1 | SIGA | Fuente única de datos sin API de integración conocida; la información se obtiene por exportación manual. | No se puede automatizar el cruce de horarios sin un acuerdo con TI; los datos exportados quedan desactualizados apenas se descargan. |
| H2 | Datos personales | La coordinadora tiene acceso a horarios, correos y datos personales de estudiantes y profesores, y esos datos se copian a hojas de cálculo. | Quedan copias de datos personales fuera de SIGA, sin control de acceso ni trazabilidad (riesgo frente a la Ley 1581 de 2012). |
| H3 | Hoja de muestreo | Sin control de versiones ni respaldo. | Pérdida o sobreescritura de la muestra; imposible auditar cómo se construyó. |
| H4 | Hoja de asignación PAT | Cruce manual de horarios, sin automatización ni validación. | Errores de cruce, reprocesos cuando un profesor rechaza, tiempo alto de ejecución. |
| H5 | Correo institucional | Notificación manual, uno a uno, sin seguimiento estructurado de las respuestas. | Profesores sin notificar, respuestas perdidas en la bandeja, demora en cerrar el ciclo. |
| H6 | Operación | Todo el proceso depende de una sola persona. | Punto único de falla y de conocimiento. |

### Qué supuestos se tomaron

- La coordinadora tiene acceso desde SIGA a los horarios de estudiantes y profesores, sus correos y sus datos personales (confirmado por el equipo con la cliente). No se asume que el acceso sea programático: se asume consulta/exportación manual.
- Los horarios de los estudiantes PAT están en SIGA, por lo que no se modela una fuente de datos adicional para ellos; su "disponibilidad" se maneja en la hoja de asignación.
- Las hojas de cálculo viven en un OneDrive (confirmado por la cliente). No se confirmó si es la cuenta institucional de la coordinadora ni con quién se comparten, lo que determina el alcance real del riesgo H3.
- El correo es el de Microsoft 365 (Exchange Online) de la universidad; no se usan herramientas de terceros, coherente con la restricción del cliente.
- Se mantiene el nombre genérico "Sistema Académico Institucional" del diagrama para SIGA; ambos se refieren al mismo sistema.
- La responsable del proceso pertenece a la Vicerrectoría de Desarrollo (coordinadora de experiencia y servicio), de acuerdo con la ficha de caracterización y el resto de los talleres. El diagrama se ajustó para reflejarlo.

## 📈 Diagrama final entregado

- [`mapa-final.drawio`](mapa-final.drawio) — Mapa de infraestructura AS-IS del proceso de la encuesta de autosatisfacción.

Se abre con [draw.io / diagrams.net](https://app.diagrams.net/) (File → Open From → Device).

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Sistema Académico Institucional (SIGA) | Sistema institucional | Fuente única de horarios, matrícula, programas y datos personales de estudiantes y profesores; sin API de integración conocida | Dirección de TI - Universidad de La Sabana |
| Base de datos académica | Base de datos | Almacena la información de SIGA | Dirección de TI - Universidad de La Sabana |
| Coordinadora de la encuesta | Actor de gestión | Opera todo el proceso: consulta SIGA, arma la muestra y las asignaciones y notifica | Vicerrectoría de Desarrollo (Johanna Molina) |
| Estudiantes PAT | Actor de gestión | Aportan su disponibilidad para aplicar la encuesta | Estudiantes PAT |
| Hoja de cálculo - Muestreo | Herramienta (Excel en OneDrive) | Selección de estudiantes por programa y semestre | Coordinadora |
| Hoja de cálculo - Asignación PAT | Herramienta (Excel en OneDrive) | Cruce manual de PAT con horarios de clase | Coordinadora |
| Correo institucional | Servicio (Exchange Online) | Envío manual de la notificación a cada profesor | Coordinadora / TI (servicio) |
| Profesores | Actor de aplicación | Reciben el aviso y aceptan o rechazan ceder su clase | Docentes de la universidad |
| Estudiantes encuestados | Actor de aplicación | Responden la encuesta en clase (muestra por programa/semestre) | Estudiantes |

## 🔍 Investigación complementaria

### Tema investigado:
Infraestructura típica de procesos administrativos universitarios basados en sistemas académicos cerrados y hojas de cálculo, y su ruta de evolución hacia plataformas de automatización de bajo código.

### Resumen:
Es frecuente que los procesos administrativos de apoyo de una universidad se sostengan sobre un sistema académico central (en este caso SIGA) del que se extraen datos por exportación, y sobre hojas de cálculo que cumplen el papel de "base de datos informal" del proceso. Este patrón se conoce como *shadow IT* de baja escala: es rápido de montar, pero concentra riesgos de integridad, respaldo y protección de datos personales, porque cada copia exportada queda fuera de los controles del sistema original.

La ruta de evolución habitual dentro del ecosistema Microsoft 365, y compatible con la restricción de la cliente, es reemplazar las exportaciones y hojas aisladas por listas de SharePoint o tablas de Dataverse gobernadas, y automatizar el cruce y la notificación con flujos de Power Automate. Ese es el punto de partida de los talleres 3 (C2 propuesto) y 7 (TO-BE) de este proyecto. El presente mapa documenta el estado previo a esa transición y justifica por qué el acceso programático a SIGA (H1) es la dependencia crítica de toda la mejora.

Esta investigación se relaciona con el taller porque explica por qué los componentes marcados en rojo del mapa son riesgos de infraestructura y no solo molestias operativas, en especial por el manejo de datos personales (H2) bajo la Ley 1581 de 2012 y la política de protección de datos de la universidad.

## 📚 Referencias

Ver [`referencias.md`](referencias.md) para el listado completo de fuentes consultadas.

---

_Este documento hace parte de la entrega del Taller 4 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
