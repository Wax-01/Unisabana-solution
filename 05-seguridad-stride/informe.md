# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 5 - Evaluación de Seguridad con STRIDE

## 👥 Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo
El objetivo del taller es analizar los riesgos de seguridad de una parte crítica del sistema de programación y ejecución de encuestas de satisfacción de la Universidad de La Sabana, usando el marco STRIDE. Se trabajó primero el ejemplo guiado de EdukIT para interiorizar la metodología de 5 pasos, y luego se aplicó sobre el flujo más sensible del sistema del cliente real: el cruce de horarios, la notificación a profesores y la distribución/registro de la encuesta, que es donde confluyen los datos personales de estudiantes y profesores identificados desde el ERD del Taller 2.

## 🔧 Proceso de desarrollo
Se partió del C2 (vista de contenedores) construido en el Taller 3 para delimitar el flujo a analizar: el proceso completo entre el Panel de Coordinación, los tres flujos de Power Automate (Cruce de Horarios, Notificación a Profesores, Distribución y Registro de Encuesta) y el Repositorio de Programación en SharePoint/Excel, incluyendo los dos sistemas externos ya identificados (SIGA y el servicio de correo institucional). Con esos elementos se dibujó el DFD marcando el límite de confianza en el tenant de Microsoft 365 de la universidad: todo lo que está dentro de ese límite es responsabilidad directa del equipo del proyecto; SIGA y los propios actores humanos quedan fuera.

Antes de completar la columna "Controles de Seguridad Existentes" se hizo reconocimiento pasivo autorizado: se revisó la política de protección de datos publicada por la Universidad de La Sabana (`unisabana.edu.co/nosotros/politica-de-proteccion-de-datos`), confirmando que la institución está sujeta a la Ley 1581 de 2012 (Habeas Data) y que declara públicamente su gobernanza de datos personales. No se realizó reconocimiento activo ni pruebas de intrusión contra ningún sistema real de la universidad, siguiendo el límite estricto de la guía del taller; el sistema en alcance (flujos de Power Automate, listas de SharePoint) tampoco expone una interfaz pública sobre la que aplicar cabeceras HTTP o escaneo TLS, así que los controles existentes se documentaron a partir de la configuración por defecto conocida del ecosistema Microsoft 365/Power Platform y de lo que el equipo pudo confirmar con el cliente, marcando explícitamente cuando algo "no se confirmó" en vez de asumirlo como implementado.

Se aplicaron las 6 categorías STRIDE sobre los procesos y el almacén de datos del DFD, se evaluó impacto y probabilidad para cada amenaza, y se priorizó la tabla de mayor a menor riesgo.

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El DFD representa 3 actores (Coordinador, Profesor, Estudiante), 4 procesos (Panel de Coordinación, Flujo de Cruce de Horarios, Flujo de Notificación a Profesores, Flujo de Distribución y Registro de Encuesta), 1 almacén de datos (Repositorio de Programación) y 2 sistemas externos (SIGA, Servicio de Correo), con el límite de confianza dibujado alrededor del tenant Microsoft 365 de la universidad. Sobre esos elementos se identificaron 7 amenazas que cubren las 6 categorías STRIDE, priorizadas por nivel de riesgo en la tabla `tabla-stride-cliente.xlsx`.

### Cómo representa las necesidades del cliente
El análisis se concentra en los puntos donde el sistema maneja datos personales de estudiantes y profesores (correos, horarios, respuestas a la encuesta), que es exactamente el tipo de información que la Ficha de Caracterización (Taller 0) señala como sensible y sujeta a la restricción del cliente de usar solo herramientas autorizadas por la universidad. Las dos amenazas de mayor riesgo (T1: exposición del repositorio de datos, T2: suplantación del coordinador) están directamente ligadas a esa restricción: si los controles de acceso de SharePoint/Azure AD fallan, se compromete tanto la privacidad de los estudiantes como la integridad del proceso institucional de acreditación que depende de esta encuesta.

### Diferencias con el caso base (EdukIT)
- **Superficie de ataque:** EdukIT es una aplicación web con servidor propio, API y base de datos expuestas, por lo que dominan amenazas como inyección SQL, manipulación de parámetros o DoS por flooding (las que se practicaron en OWASP Juice Shop). El sistema del cliente son servicios SaaS de Microsoft 365 orquestados por Power Automate, sin interfaz pública propia: las amenazas se desplazan hacia configuración y gobierno (permisos de SharePoint, MFA, cuentas de conexión, políticas DLP).
- **Responsabilidad de los controles:** en EdukIT el equipo implementa los controles en código (validación de entradas, sesiones, cifrado). En el cliente, Microsoft asegura la infraestructura y el equipo solo controla la configuración; por eso muchas mitigaciones (MFA, Conditional Access, etiquetas de sensibilidad) dependen del área de TI de la universidad, y así se refleja en la columna "Responsable".
- **Origen de la evidencia:** en el caso base se pudo explotar el sistema de práctica y observar el resultado. En el cliente real solo se hizo reconocimiento pasivo, por lo que los controles existentes se marcaron como "no confirmado" cuando no hubo evidencia.
- **Riesgo dominante:** en EdukIT el riesgo principal es el pago y las credenciales; en el cliente es la exposición de datos personales de estudiantes y profesores (Ley 1581 de 2012), con un impacto más normativo que financiero.
- **Amenaza de DoS:** en EdukIT es saturación de un servidor; en el cliente es la dependencia de SIGA y los límites de solicitudes (throttling) de los conectores (T4).

### Qué supuestos se tomaron
- No se tuvo acceso a la configuración real de permisos del sitio de SharePoint ni a si el tenant tiene MFA obligatorio, por lo que esos controles se marcaron como "no confirmado" en vez de asumir que existen o no.
- Se asume que los flujos de Power Automate se ejecutan bajo una cuenta de conexión (service account) compartida, práctica común en implementaciones de bajo código, hasta que el cliente confirme lo contrario.
- Se asume que Microsoft Forms es la herramienta usada para la encuesta, dado que es el componente estándar del ecosistema Microsoft 365 para este propósito y es coherente con la restricción tecnológica del cliente.
- El "Servicio de Correo" del C1/C2 se trata como un solo activo externo (Outlook/Exchange Online) para efectos del DFD, aunque en la práctica el envío puede hacerse vía conector de Power Automate en lugar de un endpoint expuesto directamente.

## 📈 Diagrama final entregado
> Ver `dfd-cruce-notificacion.drawio` (diagrama de flujo de datos del proceso analizado) y `tabla-stride-cliente.xlsx` (análisis STRIDE completo) adjuntos en esta carpeta.

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Coordinador de Encuestas | Actor externo (E1) | Define criterios y consulta reportes | Cliente (Vicerrectoría de Desarrollo) |
| Profesor | Actor externo (E2) | Acepta o rechaza ceder el espacio de su clase | Docentes de la universidad |
| Estudiante | Actor externo (E3) | Responde la encuesta | Muestra seleccionada de estudiantes PAT |
| Panel de Coordinación | Proceso (P1) | Interfaz donde se definen criterios y se consultan reportes | Coordinador de Encuestas |
| Flujo de Cruce de Horarios | Proceso (P2) | Cruza horarios de SIGA con disponibilidad de estudiantes PAT | Equipo de Automatización |
| Flujo de Notificación a Profesores | Proceso (P3) | Envía notificación y procesa aceptación/rechazo | Equipo de Automatización |
| Flujo de Distribución y Registro de Encuesta | Proceso (P4) | Envía el enlace y registra las respuestas | Equipo de Automatización |
| Repositorio de Programación | Almacén de datos (D1) | SharePoint Lists/Excel: Encuesta, Programación, Estudiante, Salón, Profesor, Notificación | Equipo de Automatización |
| SIGA | Sistema externo (E4) | Sistema de Información Académica: horarios y estudiantes | Universidad de La Sabana |
| Servicio de Correo | Sistema externo (E5) | Outlook / Exchange Online | Universidad de La Sabana (M365) |

## 🔍 Investigación complementaria
### Tema investigado:
Buenas prácticas de seguridad para automatizaciones de bajo código sobre Microsoft Power Platform, y marco normativo colombiano de protección de datos aplicable al sector educación.

### Resumen:
Se investigó cómo aplicar el marco STRIDE a sistemas construidos sobre Power Automate y SharePoint, que no son aplicaciones tradicionales con un servidor propio sino servicios SaaS orquestados por conectores y cuentas de conexión. La práctica recomendada, documentada por Microsoft, es aplicar controles de identidad y acceso (MFA, RBAC, Conditional Access), protección de datos mediante políticas de prevención de pérdida de datos (DLP) que restrinjan qué conectores puede usar cada entorno, y principio de mínimo privilegio en las cuentas que ejecutan los flujos — justamente los controles que se propusieron como mitigación para las amenazas T1 y T2 (riesgo Alto) y T5 (riesgo Medio, mínimo privilegio en la cuenta de conexión) de la tabla entregada.

También se revisó el marco normativo colombiano de protección de datos personales: la Ley 1581 de 2012 (Habeas Data) y sus decretos reglamentarios, que aplican directamente a este sistema porque procesa datos personales de estudiantes y profesores (correos institucionales, horarios, respuestas a la encuesta). Se confirmó mediante reconocimiento pasivo que la Universidad de La Sabana publica su propia política de tratamiento de datos personales, lo que sitúa el nivel de riesgo de una fuga de datos (T1) no solo como un problema técnico sino como un posible incumplimiento normativo institucional.

Esta investigación se relaciona directamente con el taller porque fundamentó por qué la amenaza T1 (exposición del repositorio de datos) se priorizó como riesgo Alto: no es solo una fuga técnica, sino un incumplimiento potencial de la política de datos que la propia universidad se comprometió públicamente a cumplir.

## 📚 Referencias
- [1] Microsoft. *Prevent data exfiltration with data loss prevention policies*. https://learn.microsoft.com/en-us/power-automate/guidance/coding-guidelines/prevent-data-exfiltration
- [2] Microsoft. *Security in Microsoft Power Platform*. Microsoft Learn. https://learn.microsoft.com/en-us/power-platform/admin/security/security-overview
- [3] Congreso de Colombia. *Ley 1581 de 2012 (Habeas Data)*. https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981
- [4] Universidad de La Sabana. *Política de Protección de Datos*. https://www.unisabana.edu.co/nosotros/politica-de-proteccion-de-datos
- [5] OWASP. *Threat Modeling - STRIDE*. https://owasp.org/www-community/Threat_Modeling
- [6] OWASP. *OWASP Juice Shop Project*. https://owasp.org/www-project-juice-shop/
- [7] Fuente asistida por IA: Claude (Anthropic), septiembre 2026.

---

_Este documento hace parte de la entrega del taller 5 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
