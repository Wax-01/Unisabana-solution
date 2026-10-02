# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 6 - Checklist de Cumplimiento Normativo

## 👥 Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo
El objetivo del taller es verificar el cumplimiento normativo del sistema de programación y ejecución de encuestas de satisfacción de la Universidad de La Sabana, usando como marcos de referencia Habeas Data (Ley 1581 de 2012), ISO/IEC 27001 y los controles propios del ecosistema Microsoft 365/Power Platform. Se trabajó primero el ejemplo guiado de GobData para interiorizar la metodología de 5 pasos, y luego se aplicó sobre el mismo flujo analizado en los Talleres 3, 4 y 5 (Panel de Coordinación, los tres flujos de Power Automate y el Repositorio de Programación en SharePoint/Excel), evaluando cada ítem como Cumple o Parcial y documentando cada incumplimiento real como una brecha priorizada.

## 🔧 Proceso de desarrollo
Se partió de la tabla de actores y componentes del Taller 5 (STRIDE) y del DFD/C2 de los Talleres 3 y 5, que ya delimitan qué datos procesa el sistema (horarios, respuestas de la encuesta, correos institucionales) y qué controles de seguridad se habían identificado como no confirmados (T1: exposición del repositorio, T2: suplantación del coordinador). Sobre esa base se construyó el checklist agrupando los ítems en seis categorías (Consentimiento, Protección de Datos, Correos Institucionales, Seguridad, Retención, Registro de Bases de Datos, Roles y Responsabilidades), siguiendo la metodología de 5 pasos de la guía del taller.

Antes de completar las columnas de Evidencia/Justificación y Recomendación, el equipo ubicó y leyó el texto completo de la **Política de Tratamiento de Datos Personales de la Universidad de La Sabana** (documento oficial de la Dirección de Publicaciones, vigente desde el 19 de agosto de 2013), en lugar de asumir su contenido a partir de referencias indirectas. De ese documento se extrajeron los principios aplicables (finalidad, libertad, seguridad, confidencialidad), el procedimiento formal de PQR (quince días hábiles), la tabla de áreas responsables por tipo de dato (estudiantes → Dirección de Registro Académico; empleados, incluidos profesores de planta → Dirección de Desarrollo Humano) y el tratamiento de "Encargados" externos del dato (aplicable a Microsoft como proveedor de O365/Power Automate). También se incorporó, por indicación explícita del equipo del proyecto, el **Acuerdo 01 de 2025 del CESU** ("Lineamientos y aspectos por evaluar para la acreditación en alta calidad"), ya que el informe del Taller 5 y el del Taller 7 documentan que esta encuesta es un insumo directo del proceso de acreditación institucional — esto motivó agregar una categoría adicional ("Aseguramiento de la Calidad (CNA)") que no está en el checklist base de GobData, evaluando si la trazabilidad de los datos del proceso es suficiente para soportar la autoevaluación institucional exigida por el Factor 4 del Acuerdo.

A diferencia del Taller 5, aquí no se hizo reconocimiento pasivo sobre un sitio institucional específico sino lectura directa del texto legal de la política publicada, complementada con el comportamiento documentado (y verificable sin acceso privilegiado) de Power Automate y Microsoft Purview como plataforma. Donde no hubo evidencia suficiente para confirmar un control, el ítem se marcó **Parcial** en vez de asumir cumplimiento, siguiendo el error común #1 de la guía del taller ("marcar Cumple sin evidencia concreta").

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El checklist (`checklist-cliente.xlsx`) cubre 12 ítems en 7 categorías. De estos, 2 se marcaron ✅ Cumple (uso exclusivo de herramientas autorizadas por restricción contractual del cliente, y trazabilidad nativa de ejecución de Power Automate) y 10 se marcaron ⚠️ Parcial, cada uno con su fila correspondiente en la hoja **Brechas Identificadas**, con riesgo (2 Alto, 6 Medio, 2 Bajo) y nivel de prioridad.

### Cómo representa las necesidades del cliente
La mayoría de las brechas identificadas no son fallas de diseño sino **ausencia de confirmación por parte del cliente** sobre configuración que ya podría existir (p. ej. si el registro de auditoría de Microsoft Purview está activado, o si la base está cubierta por el RNBD institucional). Esto es intencional: el checklist documenta honestamente qué está pendiente de validar con el cliente antes de la sustentación, en lugar de asumir un estado de cumplimiento que el equipo no pudo verificar. Las dos brechas de riesgo Alto (control de acceso al repositorio e inactividad no confirmada del log de auditoría) son consistentes con las amenazas T1 y T2 ya priorizadas como Alto riesgo en el análisis STRIDE del Taller 5, reforzando la trazabilidad entre talleres que exige la tabla de dependencias del README del Repo Cliente (03, 04 → 05 → 06).

### Diferencias con el caso base (GobData)
- **Origen normativo:** en GobData se asumió un marco normativo genérico de "portal estatal"; en el cliente se usó el texto completo y vigente de la política propia de la Universidad, lo que permitió citar artículos y numerales concretos (p. ej. Num. 9 sobre límites temporales al tratamiento) en vez de evidencia genérica.
- **Categoría adicional:** se agregó la categoría "Aseguramiento de la Calidad (CNA)", inexistente en GobData, porque el sistema del cliente alimenta directamente un proceso de acreditación institucional (CESU/CNA) — un requisito sectorial propio de instituciones de educación superior que no aplica a un portal de trámites ciudadanos.
- **Encargado del tratamiento:** en GobData no se discute la figura de terceros procesando los datos; en el cliente, el hecho de que la Universidad reste solo herramientas de Microsoft obliga a evaluar expresamente la figura de "Encargado del Tratamiento" (Num. 6-C de la política) y el contrato de transmisión de datos exigido por el Decreto 1377 de 2013, artículo 25.
- **Estado de verificación:** GobData llegó con 7 Cumple y 5 Parcial, ya validados sobre el sistema simulado; el cliente real llegó con solo 2 Cumple confirmables sin acceso privilegiado y 10 Parcial, reflejando que gran parte de la evidencia depende de configuración interna del tenant de M365 que el equipo no puede auditar directamente (mismo límite de reconocimiento pasivo del Taller 5).

### Qué supuestos se tomaron
- Se asume que el texto de la Política de Tratamiento de Datos Personales obtenido (vigente desde 2013, "Versión 5.0" según la página institucional) sigue siendo la versión aplicable; no se pudo confirmar una fecha de actualización posterior visible en el documento descargado.
- Se asume que "profesores de planta" quedan cubiertos como "Empleados activos" en la tabla de áreas responsables de la política (Vicerrectoría de Proyección y Desarrollo → Dirección de Desarrollo Humano), dado que la política no lista una categoría separada para "profesores" como titulares de datos.
- Se asume que Microsoft, como proveedor de Office 365/Power Automate, actúa como "Encargado del Tratamiento" bajo el Decreto 1377 de 2013 y que su marco contractual estándar (Data Protection Addendum) satisface el deber de exigir medidas de seguridad apropiadas (Num. 6-C-v de la política), sin haber confirmado la existencia de un contrato de transmisión de datos específico suscrito por la Universidad.
- Se asume, como en el Taller 5, que los flujos de Power Automate se ejecutan bajo una cuenta de conexión institucional (no personal), lo cual es coherente con la restricción tecnológica del cliente y con el comportamiento por defecto del conector de Office 365 Outlook.

## 📈 Diagrama final entregado
> Este taller no produce un diagrama nuevo: el entregable es `checklist-cliente.xlsx` (hojas "Checklist General" y "Brechas Identificadas"), adjunto en esta carpeta. El checklist referencia directamente los componentes ya modelados en `03-arquitectura-c4/c2-contenedores-final.drawio` y en el DFD del Taller 5.

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Director General Administrativo | Responsable del Tratamiento | Responsable designado por la política institucional para el tratamiento general de datos personales | Universidad de La Sabana |
| Dirección de Registro Académico | Unidad encargada | Área encargada de los datos de estudiantes activos/inactivos según la política institucional | Vicerrectoría de Profesores y Estudiantes |
| Dirección de Desarrollo Humano | Unidad encargada | Área encargada de los datos de empleados (incluye profesores de planta) según la política institucional | Vicerrectoría de Proyección y Desarrollo |
| Microsoft (Office 365 / Power Automate) | Encargado del Tratamiento | Proveedor externo que procesa los datos por cuenta de la Universidad | Microsoft Corporation |
| Superintendencia de Industria y Comercio (SIC) | Autoridad de control | Entidad ante la cual se presentan PQR y reportes de violaciones a códigos de seguridad | Estado colombiano |

## 🔍 Investigación complementaria
### Tema investigado:
Texto completo y vigente de la Política de Tratamiento de Datos Personales de la Universidad de La Sabana, y los Lineamientos y aspectos por evaluar para la acreditación en alta calidad del CESU (Acuerdo 01 de 2025), en la parte referida al Sistema Interno de Aseguramiento de la Calidad.

### Resumen:
Se ubicó y leyó el documento oficial de la Política de Tratamiento de Datos Personales de la Universidad de La Sabana (Dirección de Publicaciones, NIT 860.075.558-1), vigente desde el 19 de agosto de 2013. El documento define con precisión los principios aplicables (finalidad, libertad, veracidad, transparencia, acceso y circulación restringida, seguridad, confidencialidad), los derechos de los titulares (acceso, actualización, rectificación, supresión, queja ante la SIC), los deberes de la Universidad como Responsable y como Encargado, el procedimiento formal de PQR con plazos concretos (quince días hábiles, prorrogables ocho días más), y una tabla de áreas responsables por tipo de dato. Esta lectura directa permitió reemplazar varias evidencias genéricas del borrador inicial del checklist (que solo decían "pendiente confirmar con el cliente") por citas concretas a numerales de la política, y detectar una brecha real: el documento no menciona el Registro Nacional de Bases de Datos (RNBD), creado por el Decreto 886 de 2014, posterior a la versión del texto disponible públicamente.

Adicionalmente, se revisó el documento "Lineamientos y aspectos por evaluar para la acreditación en alta calidad de los programas académicos, las unidades académicas y las instituciones de educación superior" (CESU, Acuerdo 01 de 2025), con foco en el Factor 4 (Sistema Interno de Aseguramiento de la Calidad) y su Característica 13, que exige que la institución consolide información "veraz, actualizada" para sus procesos de autoevaluación y autorregulación. Este documento no es un marco de protección de datos sino de calidad educativa, pero se incorporó porque los informes de los Talleres 5 y 7 ya habían establecido que esta encuesta es un insumo directo del proceso de acreditación institucional — su inclusión responde al error común #3 de la guía del taller ("copiar el checklist genérico sin adaptarlo al sector del cliente"), adaptando el checklist a una normativa sectorial propia de instituciones de educación superior acreditadas.

## 📚 Referencias
Ver `entrega/referencias.md`, que incluye el mapa preliminar dato/proceso → normativa aplicable y las referencias legales, institucionales y técnicas consultadas, más las dos fuentes ampliadas en este taller:
- Universidad de La Sabana. *Política de Tratamiento de Datos Personales* (documento completo). Dirección de Publicaciones. https://editorial.unisabana.edu.co/wp-content/uploads/2016/04/Tratamiento-datos.pdf
- Consejo Nacional de Acreditación (CNA) / CESU. *Lineamientos y aspectos por evaluar para la acreditación en alta calidad de los programas académicos, las unidades académicas y las instituciones de educación superior* (Acuerdo 01 de 2025 CESU), 16 de diciembre de 2025.
- Fuente asistida por IA: Claude (Anthropic), octubre 2026.

---

_Este documento hace parte de la entrega del taller 6 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
