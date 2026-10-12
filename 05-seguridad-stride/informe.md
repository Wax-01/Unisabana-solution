# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 5 - Evaluación de Seguridad con STRIDE

## 👥 Integrantes del equipo
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo
El objetivo del taller es analizar con STRIDE los riesgos de seguridad del proceso con el que hoy se gestiona la logística de la encuesta anual de autosatisfacción de la Universidad de La Sabana. Se trabajó primero el ejemplo guiado de EdukIT para aprender la metodología de 5 pasos y luego se aplicó al flujo actual del cliente: **SIGA → exportación manual → hojas de Excel en OneDrive → correo manual a los profesores**. Ahí se concentran los datos personales de estudiantes y profesores.

> **Corrección del Corte 2.** La primera versión de este taller analizó la solución propuesta (tres flujos de Power Automate, un panel de coordinación y un repositorio en SharePoint), que todavía no existe. El análisis se rehízo sobre el proceso actual, que es donde están los riesgos reales. Las amenazas de la solución propuesta no se perdieron: quedaron como riesgos de diseño del Taller 7 en [`07-opportunities-solutions/riesgos-solucion-propuesta.xlsx`](../07-opportunities-solutions/riesgos-solucion-propuesta.xlsx) (IDs R1 a R7).

## 🔧 Proceso de desarrollo
1. **Elegir el flujo y dibujar el DFD.** El flujo sale del C2 (Taller 3) y del mapa de infraestructura (Taller 4), con los mismos nombres: SIGA, Hoja de Muestreo, Hoja de Asignación PAT y correo institucional (Exchange Online). Se agregaron dos almacenes que el mapa ya mostraba: los archivos exportados de SIGA en el equipo de la coordinadora y su buzón de correo. Se marcaron tres límites de confianza:
   - **TB1 · Infraestructura de TI de la U:** SIGA, que la Vicerrectoría no controla.
   - **TB2 · Equipo de la coordinadora:** donde se ejecutan a mano los cuatro procesos.
   - **TB3 · Tenant Microsoft 365:** OneDrive (las dos hojas) y Exchange Online (buzón).
2. **Identificar los elementos.** Cada proceso, almacén y flujo del DFD se listó como candidato a amenazas (tabla de abajo).
3. **Aplicar STRIDE.** Se partió de los hallazgos **H1 a H6** del Taller 4: cada hallazgo origina al menos una amenaza, y la columna "Componente / Activo" de la tabla indica de qué hallazgo sale.
4. **Evaluar impacto y probabilidad** con la misma matriz del ejemplo de EdukIT: Alto × Media = **Alto**; Alto × Baja = **Medio**; Medio × Media = **Medio**; Medio × Baja = **Bajo**.
5. **Priorizar** de mayor a menor riesgo (hoja "Priorizacion" del Excel).

Antes de llenar la columna "Controles de Seguridad Existentes" se hizo **reconocimiento pasivo autorizado**: solo se leyó la política de protección de datos que la universidad publica y la documentación pública de Microsoft 365 sobre OneDrive y Exchange. No se hicieron pruebas sobre ningún sistema real de la universidad. Lo que no se pudo verificar se marcó como **no confirmado** y quedó como pregunta para la cliente o para TI en [`06-normatividad/preguntas-cliente.md`](../06-normatividad/preguntas-cliente.md), pendiente para el tercer corte.

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El DFD tiene 4 entidades externas (E1 SIGA, E2 Coordinadora, E3 Estudiantes PAT, E4 Profesores), 4 procesos manuales (P1 Exportar datos de SIGA, P2 Construir la muestra, P3 Asignar PAT a clases, P4 Notificar y hacer seguimiento a profesores), 4 almacenes de datos (D1 Archivos exportados de SIGA, D2 Hoja de Muestreo, D3 Hoja de Asignación PAT, D4 Buzón de la coordinadora) y 13 flujos (F1 a F13), dentro de 3 límites de confianza. Sobre esos elementos se identificaron **8 amenazas** que cubren las 6 categorías STRIDE: 4 de riesgo Alto y 4 de riesgo Medio.

| Prioridad | ID | Tipo STRIDE | Elemento del DFD | Hallazgo (T4) | Riesgo |
|---|---|---|---|---|---|
| 1 | T1 | Information Disclosure | D2 Hoja de Muestreo, D3 Hoja de Asignación PAT | H2, H3 | **Alto** |
| 2 | T2 | Spoofing | Cuenta de la coordinadora (E2) | H6, H2 | **Alto** |
| 3 | T3 | Information Disclosure | D1 Archivos exportados de SIGA | H2 | **Alto** |
| 4 | T4 | Denial of Service | P1–P4 y equipo de la coordinadora | H6, H3 | **Alto** |
| 5 | T5 | Tampering | D3 Hoja de Asignación PAT, F6 | H3, H4 | Medio |
| 6 | T6 | Repudiation | D4 Buzón, F11 | H5 | Medio |
| 7 | T7 | Elevation of Privilege | F1 exportación de SIGA → D1, D2, D3 | H1, H2 | Medio |
| 8 | T8 | Information Disclosure | F10 aviso por correo | H5, H2 | Medio |

Los seis hallazgos del Taller 4 quedan cubiertos: H1 → T7; H2 → T1, T3, T7, T8; H3 → T1, T4, T5; H4 → T5; H5 → T6, T8; H6 → T2, T4.

### Cómo representa las necesidades del cliente
Las amenazas de mayor riesgo están en las copias de datos personales que salen de SIGA (T1, T3, T7). Ese es el hallazgo H2 del Taller 4 y la principal preocupación normativa de la universidad (Ley 1581 de 2012). La amenaza T4 (detención del proceso por depender de una sola persona) es el mismo problema que la cliente describió en la ficha: un proceso manual, repetitivo y concentrado en ella. Las mitigaciones son acciones que la coordinadora puede tomar hoy, sin herramientas nuevas: revisar con quién comparte las hojas, borrar las exportaciones, registrar las respuestas y documentar el procedimiento. Las que dependen de TI (MFA, auditoría, cifrado del disco) quedaron como preguntas concretas.

### Diferencias con el caso base (EdukIT)
- **Superficie de ataque:** EdukIT es una aplicación web con servidor, API y base de datos expuestas; dominan la inyección SQL y la manipulación de parámetros (lo practicado en OWASP Juice Shop). El proceso del cliente no tiene aplicación propia: son archivos y correos operados por una persona, así que las amenazas están en cómo se comparten los archivos, en la cuenta de la coordinadora y en los errores manuales.
- **Quién implementa los controles:** en EdukIT el equipo de desarrollo los programa. En el cliente, Microsoft asegura la plataforma, TI configura el tenant y la coordinadora decide con quién comparte cada archivo. Por eso la columna "Responsable" reparte las mitigaciones entre la coordinadora y TI.
- **Origen de la evidencia:** en el caso base se pudo explotar el sistema de práctica. En el cliente solo se hizo reconocimiento pasivo, y lo no verificado se marcó "no confirmado".
- **Denegación de servicio:** en EdukIT es saturar un servidor. En el cliente es que falte la única persona que opera el proceso o que se borre una hoja (T4).

### Qué supuestos se tomaron
- Las hojas están en el OneDrive de la cuenta institucional de la coordinadora (confirmado en el Taller 4). Con quién se comparten no está confirmado (P2); por eso T1 tiene probabilidad Media y no Alta.
- Las exportaciones de SIGA se descargan al equipo de la coordinadora antes de cargarlas a las hojas, porque SIGA no tiene API (H1). Si no se borran, se acumulan año tras año (T3).
- El canal por el que el PAT reporta su disponibilidad no está confirmado (P7). Si es editando la hoja directamente, T1 y T7 suben de probabilidad.
- No se sabe si el aviso a los profesores incluye datos de estudiantes. Se asumió que no, por eso T8 queda en Medio.

## 📈 Diagrama final entregado
- [`dfd-proceso-actual.drawio`](dfd-proceso-actual.drawio): DFD del proceso actual, con los límites de confianza y la ubicación de cada amenaza.
- [`tabla-stride-cliente.xlsx`](tabla-stride-cliente.xlsx): tabla STRIDE completa (12 columnas de la plantilla) y hoja de priorización.

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo DFD | Descripción | Elemento en C2 / mapa | Responsable |
|---|---|---|---|---|
| SIGA | Entidad externa (E1) | Fuente de horarios, programas y datos personales | Sistema externo (C2) / Sistemas institucionales (mapa) | Dirección de TI |
| Coordinadora de la encuesta | Entidad externa (E2) | Define los criterios y opera los procesos P1–P4 | Actor | Vicerrectoría de Desarrollo |
| Estudiantes PAT | Entidad externa (E3) | Reportan su disponibilidad horaria | Actor | Estudiantes PAT |
| Profesores | Entidad externa (E4) | Reciben el aviso y responden si ceden su clase | Actor | Facultades |
| Exportar datos de SIGA | Proceso (P1) | Consulta web y descarga de CSV/Excel | Relación SIGA → hojas (C2) | Coordinadora |
| Construir la muestra | Proceso (P2) | Selección de estudiantes por programa y semestre | Uso de la Hoja de Muestreo | Coordinadora |
| Asignar PAT a clases | Proceso (P3) | Cruce de clases muestreadas con disponibilidad PAT | Uso de la Hoja de Asignación PAT | Coordinadora |
| Notificar y hacer seguimiento a profesores | Proceso (P4) | Correo uno a uno y lectura de respuestas | Relación hoja → correo (C2) | Coordinadora |
| Archivos exportados de SIGA | Almacén (D1) | CSV/Excel en carpeta local del equipo | Equipo de la coordinadora (mapa) | Coordinadora |
| Hoja de Muestreo | Almacén (D2) | Excel en OneDrive | Contenedor (C2) / Microsoft 365 (mapa) | Coordinadora |
| Hoja de Asignación PAT | Almacén (D3) | Excel en OneDrive | Contenedor (C2) / Microsoft 365 (mapa) | Coordinadora |
| Buzón de la coordinadora | Almacén (D4) | Avisos enviados y respuestas en Exchange Online | Correo institucional (C2 y mapa) | Coordinadora / TI |

## 🔍 Investigación complementaria
### Tema investigado:
Riesgos de seguridad de los procesos administrativos que trabajan con exportaciones de un sistema central y archivos compartidos en Microsoft 365, y marco colombiano de protección de datos aplicable.

### Resumen:
Cuando los datos salen de un sistema con control de acceso por rol (SIGA) a un archivo, el control de acceso deja de ser el del sistema y pasa a ser el del archivo: quién lo tiene, con qué enlace se compartió y si se borró. La documentación de OneDrive distingue tres tipos de enlace. "Cualquier persona" funciona para quien lo reciba, aunque sea reenviado fuera de la organización. "Personas de la organización" da acceso a cualquier usuario interno que tenga el enlace. "Personas específicas" solo da acceso a quienes se nombran. El administrador del tenant puede deshabilitar el primer tipo [1][2]. Por eso T1 y T7 dependen de una pregunta concreta (P2) y su mitigación principal es compartir solo con personas específicas.

Para la cuenta de la coordinadora (T2), la documentación de Microsoft Entra explica que autenticar solo con contraseña deja un vector de ataque inseguro si la contraseña es débil o se filtró, y que un segundo factor (por ejemplo, la app Authenticator) no es fácil de obtener ni duplicar para un atacante. Además, el MFA se puede activar sin cambiar las aplicaciones [3]. Como en este proceso una sola cuenta da acceso a SIGA, a las dos hojas y al buzón, el MFA es el control que más reduce el riesgo con menos esfuerzo.

En lo normativo, la Ley 1581 de 2012 y la política de tratamiento de datos de la universidad exigen seguridad, confidencialidad y acceso restringido a los datos personales [4][5]. Por eso las amenazas de divulgación (T1, T3, T8) no son solo un problema técnico: son un posible incumplimiento que el Taller 6 evalúa ítem por ítem.

## 📚 Referencias
Ver [`referencias.md`](referencias.md).

---

_Este documento hace parte de la entrega del taller 5 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
