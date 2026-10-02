# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
BPMN

## 👥 Integrantes del equipo
- Julian David Aguilar
- Juan Esteban Ramirez

## 🧠 Descripción general del trabajo
El objetivo del taller es modelar el proceso que se busca mejorar en la empresa, en nuestro caso, se hizo el modelo de ejemplo y posteriormente se hizo el modelo del cliente, dados los tiempos de respuesta y la obtencion de la informacion.

## 🔧 Proceso de desarrollo
Despues del analisis de la empresa, se empezo a identificar a los actores, se definieron 3 actores: la coordinadora, que es la encargada de hacer el analisis de la informacion; Siga, la plataforma de la universidad donde se guardan los datos de las clases y estudiantes y el profesor, que define si en su clase se puede o no hacer la encuesta. Aunque inicialmente se queria incluir al estudiante PAT, se decidio que el no hace parte del proceso de la programacion de la encuesta, que es lo que se quiere optimizar, sino de la implementacion de la encuesta, ademas de que su horario esta en siga, por lo que no vimos conveniente agregar complejidad adicional al modelo. Tambien se pensó que el profesor no seria importante, pues el solo recibia el correo, pero el equipo se fijó en que si el profesor cancela esa clase o por alguna otra razon no puede prestar el espacio, deberia tener la capacidad de aceptar o cancelar para evitar inconvenientes. Para el modelado se uso Draw.io con su apartado de BPMN.


## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El modelo se estructura en tres carriles (lanes) dentro de un mismo pool, cada uno representando a uno de los actores identificados:

1. **Coordinadora**: inicia el proceso, realiza la seleccion de clases y la seleccion de PAT/horarios, evalua si existen horarios compatibles mediante una compuerta de decision (¿Hay horarios compatibles?) y finalmente recibe la confirmacion para la realizacion de la encuesta (evento final).
2. **SIGA**: representa la plataforma institucional que se consulta para obtener la informacion de bases de datos de clases y estudiantes, retroalimentando dicha informacion hacia la coordinadora para continuar con la seleccion de clases.
3. **Profesor**: recibe la notificacion cuando existen horarios compatibles, y mediante una compuerta de decision (¿Acepta?) determina si acepta o no ceder el espacio de su clase para la encuesta; en caso de rechazo, el flujo regresa al inicio del proceso de seleccion de clases para buscar una nueva alternativa.

### Cómo representa las necesidades del cliente
El diagrama representa fielmente el proceso que realiza la cliente cuando tiene que realizar esta actividad, mostrando lo repetitivo que puede llegar a ser incluso haciendo una vez el proceso. Se evidencia claramente el cuello de botella que representa la busqueda manual de horarios compatibles entre los estudiantes PAT y las clases disponibles, asi como la dependencia de la aceptacion del profesor para poder cerrar el ciclo. Esto permite justificar por que un proceso de automatizacion o apoyo tecnologico (por ejemplo, un sistema que cruce automaticamente los horarios de SIGA) representaria una mejora significativa en los tiempos de respuesta.

### Qué supuestos se tomaron
- Los profesores pueden cancelar o rechazar la solicitud de aplicar la encuesta en su clase, lo cual reinicia el ciclo de busqueda de horarios.
- El estudiante PAT no participa directamente en el proceso de programacion de la encuesta, ya que su rol se limita a la aplicacion posterior de la misma; su informacion de horario ya se encuentra disponible en SIGA.
- SIGA se modela como un actor pasivo que solo responde a consultas de informacion, sin tomar decisiones dentro del proceso.
- Se asume que la coordinadora tiene acceso directo y sin restricciones a la base de datos de SIGA para realizar las consultas necesarias.

## 📈 Diagrama final entregado

![Diagrama](/AREM-Proyecto-Cliente/img/BPMN-UniSabana.drawio.png)

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---------------------|------|-------------|-------------|
| Coordinadora | Actor | Encargada de analizar la informacion, seleccionar clases y horarios, y validar la compatibilidad de los mismos | Secretaria / Cliente |
| SIGA | Sistema / Entidad | Plataforma institucional donde se almacenan las bases de datos de clases y estudiantes | Universidad de La Sabana |
| Profesor | Actor | Decide si acepta o no que se realice la encuesta dentro del horario de su clase | Docentes de la universidad |
| Consulta de bases de datos | Actividad | Proceso mediante el cual se obtiene la informacion de clases y estudiantes desde SIGA | SIGA |
| Seleccion de Clases | Actividad | Actividad donde la coordinadora elige las clases candidatas para aplicar la encuesta | Coordinadora |
| Seleccion PAT/horarios | Actividad | Actividad donde se cruzan los horarios de los estudiantes PAT con los de las clases seleccionadas | Coordinadora |
| ¿Hay horarios compatibles? | Compuerta de decision | Evalua si existe compatibilidad entre los horarios encontrados | Coordinadora |
| Notificacion al profesor | Actividad | Envio de la notificacion al profesor sobre la realizacion de la encuesta en su clase | Coordinadora |
| ¿Acepta? | Compuerta de decision | Determina si el profesor acepta o rechaza la realizacion de la encuesta | Profesor |
| Realizacion de la encuesta | Evento final | Cierre del proceso una vez confirmada la disponibilidad del horario y la aceptacion del profesor | Coordinadora |

## 🔍 Investigación complementaria
### Tema investigado:
Buenas prácticas de modelado BPMN para procesos administrativos con multiples actores y ciclos de reintento.

### Resumen:
Para el desarrollo del taller se investigaron las buenas practicas recomendadas por la notacion BPMN 2.0 (Business Process Model and Notation), en especial en lo referente al uso correcto de pools y lanes para representar distintos actores u organizaciones dentro de un mismo proceso, asi como el uso adecuado de compuertas exclusivas (XOR) para modelar puntos de decision con caminos alternativos, como ocurre en las preguntas "¿Hay horarios compatibles?" y "¿Acepta?" del modelo entregado.

Tambien se investigo sobre el modelado de procesos ciclicos o iterativos, comunes en procesos administrativos manuales donde una tarea puede repetirse varias veces antes de completarse exitosamente, tal como sucede en la busqueda de horarios compatibles entre estudiantes PAT y clases. Segun la documentacion oficial del Object Management Group (OMG), estos ciclos deben representarse mediante flujos de secuencia que retornan a actividades previas, evitando el uso de bucles implicitos que dificulten la lectura del diagrama, tal como se aplico en el modelo entregado al hacer que los flujos "No" regresen explicitamente a la actividad de "Seleccion de Clases".

Esta investigacion se relaciona directamente con el taller porque permitio justificar las decisiones de diseño tomadas por el equipo, en particular la inclusion del carril del Profesor como un actor con capacidad de decision propia, y la representacion del proceso como un ciclo retroalimentado en lugar de un flujo lineal simple, reflejando con mayor fidelidad la realidad del proceso manual que hoy realiza la Universidad de La Sabana.

---

_Este documento hace parte de la entrega del taller X del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._