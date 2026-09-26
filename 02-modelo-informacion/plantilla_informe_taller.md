# 🗒️ Registro de Trabajo en Clase - Taller X

## 📆 Fecha de la sesión
21 de agosto de 2026

## 👥 Integrantes presentes
- Julián David Aguilar
- Juan Esteban Ramirez

## 🧠 Actividades realizadas en clase
Durante la sesión se analizaron los requerimientos del caso de la universidad para automatizar la realización de encuestas de autoevaluación a los estudiantes.

### ¿Qué se discutió con el equipo?
Se discutió cómo representar el proceso de programación de las encuestas, teniendo en cuenta la búsqueda automática de salones disponibles, los estudiantes que se encuentran disponibles en un horario determinado y la notificación previa de una semana a los respectivos profesores.

### ¿Qué decisiones de modelado se tomaron?
Se definieron las siguientes entidades principales:
- Encuesta
- Programación
- Estudiante
- Salón
- Profesor
- Notificación

También se estableció que la relación entre Encuesta y Programación debe ser de muchos a muchos, ya que una encuesta puede realizarse en varias programaciones y una programación puede incluir diferentes encuestas.

En el diagrama de contexto se decidió representar al sistema central como el encargado de:
- Recibir los criterios definidos por el coordinador.
- Consultar los salones disponibles.
- Consultar los estudiantes disponibles.
- Programar la realización de las encuestas.
- Notificar al profesor con una semana de anticipación.
- Registrar las respuestas de los estudiantes.

### ¿Qué herramientas se usaron?
- draw.io

### ¿Qué parte del trabajo se alcanzó a desarrollar?
Se desarrollaron los siguientes diagramas:
- Diagrama ERD.
- Diagrama de contexto.
- Relaciones y cardinalidades entre las entidades principales.

## 🧩 Modelo ERD
El modelo representa la información necesaria para gestionar la programación de encuestas dentro de la universidad.

Las principales relaciones son:
- Una encuesta puede estar asociada a varias programaciones.
- Una programación puede involucrar varios estudiantes.
- Una programación puede realizarse en diferentes salones.
- Una programación genera notificaciones.
- Cada notificación está dirigida a un profesor.

![alt text](/img/BPMN-UniSabana.drawio.png)

## 🌐 Diagrama de contexto
El diagrama de contexto representa las interacciones entre el sistema y los actores externos.

Los principales actores son:
- **Coordinador de encuestas**: define la fecha, horario, capacidad y criterios.
- **Sistema de horarios académicos**: proporciona información sobre los salones disponibles.
- **Base de datos de personas o estudiantes**: proporciona información sobre las personas disponibles.
- **Profesor**: recibe una notificación antes de la realización de la encuesta.
- **Estudiante**: recibe y responde la encuesta.
- **Notificador**: envía la notificación al profesor.

 ![alt text](/img/contexto.png)

---
