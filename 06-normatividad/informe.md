# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 6 - Checklist de Cumplimiento Normativo

## 👥 Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo
El objetivo del taller es verificar el cumplimiento normativo del proceso con el que **hoy** se gestiona la logística de la encuesta anual de autosatisfacción de la Universidad de La Sabana. Los marcos de referencia son la Ley 1581 de 2012 (Habeas Data) y sus decretos, la política de tratamiento de datos de la universidad, ISO/IEC 27001 y los lineamientos de acreditación del CESU. Se trabajó primero el ejemplo guiado de GobData para aprender la metodología de 5 pasos y luego se aplicó al mismo proceso actual de los talleres 3, 4 y 5: **SIGA → exportación manual → Hoja de Muestreo y Hoja de Asignación PAT en OneDrive → correo manual a los profesores**.

> **Corrección del Corte 2.** La primera versión evaluaba en parte la solución propuesta (Power Automate y un repositorio en SharePoint), que todavía no existe. Se reevaluaron todos los ítems sobre el proceso actual:
> - El antiguo ítem #5 (Cumple, porque Power Automate exige OAuth) pasó a dos ítems: el envío desde la cuenta institucional (#7, Cumple con evidencia actual) y el registro de las respuestas de los profesores (#8, Parcial).
> - El antiguo ítem #7 (Cumple, por la restricción de usar solo herramientas autorizadas) era un requisito y no un control. Se reformuló como el ítem #11 (Parcial).
> - Se agregaron cuatro ítems sobre las hojas de Excel en OneDrive y las exportaciones de SIGA, que son el riesgo normativo más claro del proceso (hallazgo H2): quién tiene acceso (#5), con qué enlace se comparten (#6), minimización de campos (#4) y cuánto tiempo se conservan (#14).

## 🔧 Proceso de desarrollo
1. **Identificar el marco normativo** aplicable a cada dato del proceso (ver el mapa dato → norma en [`referencias.md`](referencias.md)).
2. **Construir el checklist** a partir de los componentes del C2 (Taller 3), los hallazgos H1 a H6 del mapa (Taller 4) y las amenazas T1 a T8 del STRIDE (Taller 5). El checklist tiene **17 ítems en 8 categorías**: Consentimiento, Protección de Datos, Correos Institucionales, Seguridad (ISO 27001), Retención, Registro de Bases de Datos, Roles y Responsabilidades, y Aseguramiento de la Calidad (CNA).
3. **Evaluar cada ítem** como ✅ Cumple o ⚠️ Parcial (los dos estados de la plantilla), siempre con evidencia del proceso actual: lo confirmado con la cliente, el texto de la política institucional o un hallazgo de otro taller.
4. **Documentar cada brecha** en la hoja "Brechas Identificadas", con su riesgo y el número del ítem de origen.
5. **Priorizar y recomendar.** Las brechas se ordenan de mayor a menor prioridad, y cada recomendación es una acción que la coordinadora o TI pueden tomar sin herramientas nuevas.

Antes de completar la evidencia, el equipo leyó el texto completo de la **Política de Tratamiento de Datos Personales de la Universidad de La Sabana** (vigente desde el 19 de agosto de 2013). De ahí salen los numerales citados: principio de finalidad (Num. 4-a), supresión al cumplir la finalidad (Num. 9), PQR (Num. 10), Encargados del tratamiento (Num. 6-C) y la tabla de áreas responsables. También se incorporó el **Acuerdo 01 de 2025 del CESU** porque la encuesta es insumo de la autoevaluación institucional.

Donde la evidencia depende de un dato que no pudimos verificar, el ítem quedó Parcial y se convirtió en una **pregunta cerrada para la cliente o para TI** en [`preguntas-cliente.md`](preguntas-cliente.md) (P1 a P7). En este corte no fue posible consultar a la cliente ni a TI, así que las preguntas quedan **pendientes para el tercer corte**. Al recibir cada respuesta se actualizará la evidencia del ítem con la fecha de la consulta.

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El checklist (`checklist-cliente.xlsx`) tiene 17 ítems en 8 categorías. **2 ítems Cumplen**, ambos con evidencia del proceso actual:
- **#7:** los avisos se envían desde la cuenta institucional (confirmado con la cliente).
- **#16:** la universidad tiene una política publicada que designa responsable y áreas encargadas.

Los **15 ítems Parciales** tienen cada uno su fila en "Brechas Identificadas": 5 de riesgo Alto, 8 Medio y 2 Bajo.

| Prioridad | Ítem | Brecha | Amenaza (T5) | Pregunta |
|---|---|---|---|---|
| Alta | #5 | No se confirmó quién tiene acceso a las hojas | T1 | P2 |
| Alta | #6 | No se confirmó el tipo de enlace con el que se comparten | T1 | P2 |
| Alta | #10 | No se confirmó MFA en la cuenta de la coordinadora | T2 | P3 |
| Alta | #13 | Hojas sin respaldo independiente y una sola operadora | T4 | — |
| Alta | #14 | Sin plazo de conservación ni borrado de hojas y exportaciones | T3 | P4 |

### Cómo representa las necesidades del cliente
Las brechas de mayor riesgo están en las copias de datos personales que salen de SIGA hacia las hojas de Excel y el equipo de la coordinadora: el hallazgo H2 del Taller 4 y las amenazas T1 y T3 del Taller 5. La recomendación principal no requiere tecnología nueva: revisar con quién se comparten las hojas, exportar solo los campos necesarios y borrar las exportaciones al terminar la encuesta. Esto es coherente con la restricción de la cliente de usar solo herramientas autorizadas por la universidad.

Varias brechas dependen de confirmar configuraciones que podrían ya existir (MFA, auditoría de Purview, RNBD). No se marcaron Cumple sin evidencia: quedaron Parciales y con una pregunta concreta.

### Diferencias con el caso base (GobData)
- **Origen normativo:** en GobData se usó un marco genérico de portal estatal. En el cliente se citó la política propia de la universidad, numeral por numeral.
- **Categoría adicional:** "Aseguramiento de la Calidad (CNA)" no existe en GobData. Se agregó porque la encuesta alimenta la autoevaluación institucional, un requisito propio de las instituciones de educación superior.
- **Encargado del tratamiento:** en el cliente los datos viven en Microsoft 365, así que se evalúa la figura de Encargado (Num. 6-C de la política) y el contrato que exige el Decreto 1377 de 2013, art. 25 (ítem #11).
- **Estado de verificación:** GobData llegó con 7 Cumple y 5 Parcial sobre un sistema simulado. El cliente real tiene 2 Cumple y 15 Parcial, porque el proceso es manual y casi ningún control está documentado o confirmado.

### Qué supuestos se tomaron
- La política de tratamiento de datos obtenida (vigente desde 2013) sigue siendo la versión aplicable.
- Los profesores de planta quedan cubiertos como "empleados" en la tabla de áreas responsables de la política (Dirección de Desarrollo Humano).
- Microsoft actúa como Encargado del tratamiento de los datos guardados en OneDrive y Exchange Online. No se confirmó el contrato específico (pregunta adicional para TI).
- El aviso a los profesores no incluye datos de estudiantes (mismo supuesto de la amenaza T8).

## 📈 Diagrama final entregado
> Este taller no produce un diagrama nuevo. Los entregables son:
> - [`checklist-cliente.xlsx`](checklist-cliente.xlsx), con las hojas "Checklist General" y "Brechas Identificadas".
> - [`preguntas-cliente.md`](preguntas-cliente.md), con las preguntas que cierran las brechas no confirmadas.
>
> El checklist usa los mismos componentes del C2 ([`03-arquitectura-c4/c2-contenedores-final.drawio`](../03-arquitectura-c4/c2-contenedores-final.drawio)), del mapa ([`04-infraestructura/mapa-final.drawio`](../04-infraestructura/mapa-final.drawio)) y del DFD ([`05-seguridad-stride/dfd-proceso-actual.drawio`](../05-seguridad-stride/dfd-proceso-actual.drawio)).

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Director General Administrativo | Responsable del Tratamiento | Responsable designado por la política institucional para el tratamiento de datos personales | Universidad de La Sabana |
| Dirección de Registro Académico | Área encargada | Área encargada de los datos de estudiantes según la política | Vicerrectoría de Profesores y Estudiantes |
| Dirección de Desarrollo Humano | Área encargada | Área encargada de los datos de empleados (incluye profesores de planta) según la política | Vicerrectoría de Proyección y Desarrollo |
| Coordinadora de la encuesta | Usuaria del dato | Exporta los datos de SIGA y los trata en la Hoja de Muestreo y la Hoja de Asignación PAT | Vicerrectoría de Desarrollo |
| Microsoft (OneDrive, Exchange Online) | Encargado del Tratamiento | Proveedor que almacena las hojas y los correos del proceso | Microsoft Corporation |
| Superintendencia de Industria y Comercio (SIC) | Autoridad de control | Entidad ante la que se presentan quejas y donde se inscriben las bases en el RNBD | Estado colombiano |

## 🔍 Investigación complementaria
### Tema investigado:
Texto completo y vigente de la Política de Tratamiento de Datos Personales de la Universidad de La Sabana, y los Lineamientos para la acreditación en alta calidad del CESU (Acuerdo 01 de 2025), en la parte del Sistema Interno de Aseguramiento de la Calidad.

### Resumen:
Se leyó el documento oficial de la Política de Tratamiento de Datos Personales de la Universidad de La Sabana, vigente desde el 19 de agosto de 2013. El documento define:
- Los principios aplicables: finalidad, libertad, veracidad, transparencia, acceso y circulación restringida, seguridad y confidencialidad.
- Los derechos de los titulares.
- Los deberes de la universidad como Responsable y como Encargado.
- El procedimiento de PQR, con plazo de quince días hábiles prorrogables ocho más.
- Una tabla de áreas responsables por tipo de dato.

Esta lectura permitió citar numerales concretos en el checklist. También permitió detectar que el documento no menciona el Registro Nacional de Bases de Datos (RNBD), creado por el Decreto 886 de 2014, posterior a la versión publicada (ítem #15).

Aplicada al proceso actual, la política deja una conclusión clara: el principio de acceso y circulación restringida y el deber de suprimir el dato al cumplir la finalidad (Num. 9) aplican también a las copias de SIGA que viven en Excel y en el equipo de la coordinadora, no solo a SIGA. Por eso los ítems #4, #5, #6 y #14 son los de mayor prioridad.

También se revisó el Acuerdo 01 de 2025 del CESU, en particular el Factor 4 (Sistema Interno de Aseguramiento de la Calidad) y su Característica 13, que exige información "veraz, actualizada" para la autoevaluación. Como la encuesta es insumo de ese proceso, se agregó la categoría "Aseguramiento de la Calidad (CNA)" (ítem #17). Así se evita el error común #3 de la guía: copiar el checklist genérico sin adaptarlo al sector del cliente.

## 📚 Referencias
Ver [`referencias.md`](referencias.md), que incluye el mapa dato/proceso → normativa aplicable y las referencias legales, institucionales y técnicas consultadas.

---

_Este documento hace parte de la entrega del taller 6 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
