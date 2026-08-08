# 🛠️ Cómo Armar el Repositorio del Proyecto con el Cliente Real

Esta guía es para el **equipo**, no para un taller específico: explica cómo organizar en un solo repositorio de GitHub todo el trabajo de la Parte 2 ("Aplicación al Cliente Real") de los 10 talleres del curso, de modo que el resultado final sea algo que **el cliente pueda usar**, no solo una carpeta de entregables académicos.

---

## 1. Dos audiencias, un repositorio

El repositorio de su proyecto lo van a leer dos tipos de personas muy distintas:

- **El área de negocio del cliente** — quiere entender rápido cuál era el problema, qué se propone y cómo se implementa. No necesita (ni quiere) leer 10 informes técnicos para llegar a esa respuesta.
- **El docente y ustedes mismos** — necesitan ver el detalle completo, taller por taller, para verificar la trazabilidad y el rigor del análisis.

Por eso el repositorio tiene una estructura de dos capas: un **README raíz liviano y de negocio** en la puerta de entrada, y el detalle técnico organizado por carpetas debajo, para quien quiera profundizar. Nadie del área de negocio debería tener que abrir la carpeta `05-seguridad-stride/` para entender qué se les está proponiendo — para eso está el resumen ejecutivo.

---

## 2. Un repositorio por equipo, con una carpeta por taller

Cada equipo crea **un solo repositorio** (no diez) para su cliente real, nombrado así: `AREM-EquipoX-NombreCliente` (ej. `AREM-Equipo3-FundacionSaludViva`). Dentro, una carpeta por taller — solo con lo de la Parte 2 (Aplicación al Cliente Real); lo de la Parte 1 (caso de clase) se queda en los repos de taller, no aquí.

```text
AREM-EquipoX-NombreCliente/
├── README.md                          # ⭐ Punto de entrada — ver plantilla en este repo
├── resumen-ejecutivo.md               # Copia del Taller 9 — lo primero que debe leer el cliente
├── 00-preliminary-vision/
│   ├── ficha-caracterizacion.md
│   ├── vision.md
│   └── referencias.md
├── 01-bpmn/
│   ├── modelo-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 02-modelo-informacion/
│   ├── modelo-final-er.drawio
│   ├── diagrama-contexto-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 03-arquitectura-c4/
│   ├── c1-contexto-final.drawio
│   ├── c2-contenedores-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 04-infraestructura/
│   ├── mapa-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 05-seguridad-stride/
│   ├── tabla-stride-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
├── 06-normatividad/
│   ├── checklist-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
├── 07-opportunities-solutions/
│   ├── to-be-aplicaciones-final.drawio
│   ├── to-be-tecnologia-final.drawio
│   ├── matriz-brechas.xlsx
│   ├── informe.md
│   └── referencias.md
├── 08-integracion-vistas/
│   ├── tablero-integrado-cliente.drawio
│   ├── informe.md
│   └── referencias.md
└── 09-presentacion-final/
    ├── presentacion.pdf
    ├── matriz-evaluacion.xlsx
    ├── plan-implementacion.md
    ├── plan-gobernanza.md
    ├── procedimiento-cambios.md
    ├── vistas-finales/
    └── reflexiones/
```

Cada carpeta usa las plantillas del repo del taller correspondiente — cópielas de `plantillas/` de cada `AREM-Taller_N_...` a la carpeta de aquí y llénelas con el trabajo del cliente real.

---

## 3. Cómo fluye la información entre carpetas (trazabilidad)

Cada carpeta no es un ejercicio aislado: usa lo que produjo la anterior. Si dos carpetas se contradicen, algo quedó mal — revisen esta tabla antes de dar por cerrado un corte.

| De → A | Qué se traslada |
|---|---|
| 00 → 01 | Un proceso de "Procesos clave del negocio" de la Ficha se convierte en el proceso a modelar en BPMN |
| 00 → 02 | El contexto del negocio (sistemas y actores mencionados en la Ficha) informa el ERD y el diagrama de contexto |
| 01, 02 → 03 | Los procesos y entidades ya modelados delimitan qué sistema se documenta en C1/C2 |
| 03 → 04 | Los contenedores del C2 aparecen como componentes en el mapa de infraestructura |
| 03, 04 → 05 | Los componentes y flujos de C4/infraestructura son el objeto del análisis STRIDE |
| 00, 02 → 06 | Los datos sensibles identificados en la Ficha y el ERD se evalúan contra el checklist normativo |
| 03, 04, 05, 06 → 07 | Los riesgos y brechas de C4, infraestructura, STRIDE y normatividad se consolidan en el TO-BE |
| 00–07 → 08 | Todas las vistas (AS-IS y TO-BE) se integran en un solo tablero coherente |
| 00–08 → 09 | Todo se condensa en la narrativa de 4 actos, el plan de implementación, la gobernanza y el resumen ejecutivo |

---

## 4. Cronograma de entrega por corte — ⚠️ pendiente de confirmar

Con el Taller 7 (Opportunities & Solutions) insertado entre Normatividad y Presentación Final, el mapeo original del enunciado ("Corte 2 = Aplicaciones + Tecnológica + Opportunities & Solutions") ya no encaja tal cual, porque el TO-BE ahora depende de que Seguridad (05) y Normatividad (06) ya estén hechos, y esos dos no tenían fecha propia en el enunciado. Propuesta de recalibración — **falta que el docente la confirme**:

| Corte | Fecha | Carpetas que deberían estar completas |
|---|---|---|
| Corte 1 | 14 ago | `00-preliminary-vision/`, `01-bpmn/`, `02-modelo-informacion/` |
| Corte 2 | 25 sep | `03-arquitectura-c4/`, `04-infraestructura/`, `05-seguridad-stride/`, `06-normatividad/` (AS-IS + riesgos completos, ya no el TO-BE) |
| — | antes del 13 nov | `07-opportunities-solutions/`, `08-integracion-vistas/` (preparación para el cierre) |
| Corte 3 | 13 nov | `09-presentacion-final/` y ajustes finales a todo lo anterior |

---

## 5. Cómo compartir el repositorio

- Agregue al docente como colaborador del repositorio, o déjelo público (igual que los repos de taller).
- Comparta el link por el canal que ya usa el curso (Aula Virtual / correo) — no hace falta una organización de GitHub aparte.

---

## 6. Plantilla del README raíz (la puerta de entrada para el cliente)

Copie [`plantilla_readme_equipo.md`](plantilla_readme_equipo.md) como `README.md` en la raíz de su repositorio y complétela. Es lo primero — y para muchos lectores del área de negocio, lo único — que van a leer.

---

## ✅ Licencia

Este repositorio es de uso académico bajo licencia MIT. Hace parte del curso de Arquitectura Empresarial - Universidad de La Sabana.
