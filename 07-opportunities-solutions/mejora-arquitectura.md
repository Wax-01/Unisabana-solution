# Mejora de Arquitectura (TO-BE) — Identificación y Priorización de Mejoras

## Cliente
Vicerrectoría de Desarrollo — Universidad de La Sabana

## Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

---

## 1. Diagnóstico inicial

> Este diagnóstico parte del estado actual (AS-IS) documentado en los talleres 3 a 6: C2 en `03-arquitectura-c4/`, mapa en `04-infraestructura/`, STRIDE en `05-seguridad-stride/` y checklist en `06-normatividad/`.

### Fricción operativa
Hoy no hay ninguna automatización en el proceso. La coordinadora exporta a mano los datos de SIGA, arma la muestra en la **Hoja de Muestreo**, cruza a mano la disponibilidad de los estudiantes PAT en la **Hoja de Asignación PAT** (las dos en Excel sobre OneDrive) y avisa a cada profesor por **correo institucional**, uno a uno. Las respuestas de aceptación o rechazo llegan a su buzón sin registro estructurado, y cada rechazo obliga a repetir el cruce.

### Problemas recurrentes (hallazgos del Taller 4)
1. **Re-procesamiento por rechazo de profesores (H4, H5):** cuando un profesor no cede su clase, la coordinadora debe volver a cruzar horarios en la hoja y escribir nuevos correos.
2. **Dependencia de una sola persona y de archivos sin respaldo (H6, H3):** si la coordinadora falta o una hoja se daña, el proceso se detiene.
3. **SIGA sin API de integración conocida (H1):** los datos salen por exportación manual y quedan desactualizados apenas se descargan.

### Vulnerabilidades de seguridad y cumplimiento (talleres 5 y 6)
- **T1 - Divulgación de datos personales en las hojas de OneDrive (riesgo Alto):** las copias de datos de SIGA quedan expuestas según con quién y con qué enlace se compartan las hojas (checklist #5 y #6).
- **T2 - Suplantación de la cuenta de la coordinadora (riesgo Alto):** una sola cuenta da acceso a SIGA, a las hojas y al buzón; no se confirmó MFA (checklist #10).
- **T3 - Exportaciones de SIGA en el equipo local (riesgo Alto):** archivos con datos personales sin borrado ni cifrado confirmados (checklist #14).
- **T4 - Detención del proceso por operadora única (riesgo Alto):** sin respaldo ni procedimiento documentado (checklist #13).

### Resumen del problema actual (foto del AS-IS)
El proceso actual es manual y depende de una persona, dos hojas de Excel y el correo. Los datos personales salen de SIGA y quedan copiados fuera de sus controles, y la trazabilidad de la muestra no alcanza para soportar la autoevaluación institucional (checklist #17).

---

## 2. Propuesta de mejoras

### 2.1 Lluvia de ideas (sin censura inicial)

| # | Idea de mejora | Tipo |
|---|---|---|
| 1 | Integración por API REST síncrona con SIGA y envío de Tarjetas Adaptativas (Adaptive Cards) en Outlook/Teams para confirmación con 1-click por parte de docentes. | Proceso / Tecnología |
| 2 | Migración del almacenamiento desde SharePoint Lists a Microsoft Dataverse / Azure SQL Database con encriptación TDE y RBAC granular. | Tecnología / Seguridad |
| 3 | Configuración e implementación de Políticas de Prevención de Pérdida de Datos (DLP) en el tenant de Power Platform. | Seguridad / Normatividad |
| 4 | Sustitución de cuentas de servicio compartidas por Identidades Administradas (Azure Managed Identities / Service Principals) con MFA y Acceso Condicional. | Seguridad |
| 5 | Automatización de recordatorios inteligentes con lógica predictiva basada en la fecha límite de la encuesta. | Proceso |
| 6 | Rediseño del formulario en Microsoft Forms / Power Apps con autenticación SSO y generación de tokens de respuesta única de solo un uso. | Tecnología / Seguridad |

### 2.2 Priorización (2-3 soluciones priorizadas)

| Solución priorizada | Esfuerzo | Impacto | Quick win / Largo plazo | Justificación |
|---|---|---|---|---|
| **Solución A:** Implementación de Tarjetas Adaptativas (Adaptive Cards en Outlook/Teams) + Integración API con SIGA para confirmación docente en 1-click. | Medio | Alto | Quick Win | Elimina el principal cuello de botella operativo del proceso al permitir que el docente acepte o rechace ceder su espacio de clase directamente desde la notificación sin cambiar de ventana, automatizando la reprogramación en tiempo real. |
| **Solución B:** Migración a Microsoft Dataverse / Azure SQL con RBAC estricto y configuración de Políticas DLP en Power Platform. | Medio | Alto | Quick Win | Cierra las amenazas T1, T3 y T7 del STRIDE AS-IS (Taller 5), al reemplazar las hojas y las exportaciones sueltas por un almacén con control de acceso por rol, y garantiza el cumplimiento normativo con la Ley 1581 de 2012, asegurando los datos personales de estudiantes y profesores contra accesos no autorizados y exfiltración. |
| **Solución C:** Transición a Service Principals (Azure Active Directory / Entra ID) y uso de Tokens de Respuesta Única para estudiantes. | Alto | Alto | Largo plazo | Mitiga la suplantación de la cuenta de la coordinadora (T2) y evita que la automatización herede sus riesgos y previene el fraude o llenado múltiple de encuestas, elevando la confiabilidad de los datos de acreditación. |

---

## 3. Visualización TO-BE

### 3.1 Proceso mejorado
En la arquitectura TO-BE, el proceso se transforma de la siguiente manera:
1. El **Coordinador** configura los parámetros en el Panel de Coordinación.
2. El **Flujo de Cruce de Horarios** consulta mediante API REST el sistema **SIGA**, valida disponibilidades de aulas/estudiantes PAT de manera automática e invoca el envío de la encuesta.
3. El docente recibe una **Tarjeta Adaptativa (Adaptive Card)** en Microsoft Teams y Outlook. Al hacer clic en "Aceptar", el flujo agenda la encuesta instantáneamente. Si selecciona "Rechazar", el sistema busca automáticamente la siguiente mejor alternativa horaria en SIGA.
4. El estudiante recibe un enlace individual respaldado por token único vía **Microsoft Forms con Azure AD SSO**, registrando la respuesta de forma cifrada.

### 3.2 Cambios en aplicaciones, infraestructura y flujos de información
- **Contenedor de Persistencia:** Se reemplaza SharePoint Lists por **Microsoft Dataverse / Azure SQL Database**.
- **Canal de Interacción con Docentes:** Incorporación de **Adaptive Cards (Actionable Messages)** sobre Outlook y Teams.
- **Gestión de Identidades:** Reemplazo de credenciales compartidas por **Service Principals en Azure Entra ID**.
- **Flujo de Integración SIGA:** Creación de un conector personalizado seguro (Custom Connector con OAuth 2.0) hacia las APIs de SIGA.

> **Anexos del modelo:**
> - Diagrama C2 TO-BE de Aplicaciones: [`to-be-aplicaciones-final.drawio`](to-be-aplicaciones-final.drawio)
> - Mapa TO-BE de Tecnología e Infraestructura: [`to-be-tecnologia-final.drawio`](to-be-tecnologia-final.drawio)

### 3.3 Controles de seguridad integrados (amenazas del STRIDE AS-IS, Taller 5)
| Amenaza AS-IS | Cómo la atiende el TO-BE |
|---|---|
| T1 y T7 - Divulgación y acceso a datos de SIGA en las hojas | Almacén en Dataverse con roles restringidos por unidad; los datos dejan de copiarse a hojas compartidas. |
| T2 - Suplantación de la cuenta de la coordinadora | Autenticación con Entra ID, MFA y acceso condicional; los flujos se ejecutan con Service Principals y no con la cuenta de la coordinadora. |
| T3 - Exportaciones de SIGA en el equipo local | Integración por API con SIGA: no hay archivos descargados. |
| T4 - Operadora única | Los flujos y el almacén no dependen del equipo ni de la presencia de una persona. |
| T5 y T6 - Errores en la hoja y respuestas sin registro | Confirmación del profesor con Adaptive Cards, registrada automáticamente con fecha y usuario. |

La solución propuesta trae sus propios riesgos (cuentas de conexión, conectores, límites de solicitudes, enlaces de aprobación). Están en [`riesgos-solucion-propuesta.xlsx`](riesgos-solucion-propuesta.xlsx), IDs R1 a R7. Ese fue el primer análisis STRIDE del equipo, hecho sobre la solución y no sobre el proceso actual. La mitigación de exfiltración por conectores (políticas DLP en Power Platform) responde a esos riesgos de la solución, no a una amenaza actual.

---

## 4. Análisis de beneficios y riesgos

| Mejora / Solución | Beneficio de negocio | Beneficio tecnológico/seguridad | Riesgo, limitación o dependencia de implementación |
|---|---|---|---|
| **Tarjetas Adaptativas (Adaptive Cards) + API SIGA** | Reducción del tiempo de programación de semanas a horas; incremento en el cumplimiento de encuestas. | Eliminación de correos no estructurados y automatización síncrona de eventos de agendamiento. | Dependencia de la disponibilidad y tiempo de respuesta de las APIs de SIGA desarrolladas por la Universidad. |
| **Dataverse / Azure SQL + Políticas DLP** | Garantía de cumplimiento legal (Ley 1581 de 2012) ante auditorías y protección de reputación institucional. | Cierre de las amenazas T1, T3 y T7 del AS-IS; almacenamiento escalable de alta concurrencia. | Costo adicional de licenciamiento (Dataverse / Azure SQL) dentro del tenant de la universidad. |
| **Service Principals + Tokens Únicos (Entra ID)** | Elevada validez de la información recolectada para los procesos institucionales de acreditación. | Mitigación de la suplantación de identidades (T2); trazabilidad y auditoría completa en Azure Logs. | Requiere permisos de administración global de Entra ID para la creación y gestión de App Registrations. |

---

## Anexos
- **Diagrama TO-BE de Aplicaciones:** [`to-be-aplicaciones-final.drawio`](to-be-aplicaciones-final.drawio)
- **Diagrama TO-BE de Tecnología:** [`to-be-tecnologia-final.drawio`](to-be-tecnologia-final.drawio)
- **Matriz de brechas (Gap Analysis):** [`matriz-brechas.xlsx`](matriz-brechas.xlsx)
- **Primera propuesta C1/C2 (Taller 3, versión inicial):** [`c1-contexto-to-be-v1.drawio`](c1-contexto-to-be-v1.drawio) y [`c2-contenedores-to-be-v1.drawio`](c2-contenedores-to-be-v1.drawio). Usa Forms, Power Automate, SharePoint y Power BI; antecede a la propuesta con Dataverse de esta carpeta.
- **Riesgos de la solución propuesta (R1 a R7):** [`riesgos-solucion-propuesta.xlsx`](riesgos-solucion-propuesta.xlsx)

---

