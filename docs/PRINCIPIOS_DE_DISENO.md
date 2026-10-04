# Principios de diseño

El programa se usará sobre todo en el **curso 2027-28 y siguientes**; lo que sabemos hoy describe 2026-27. Todo debe poder cambiar de un curso a otro **sin tocar el código**.

1. **Nada del colegio está fijo en el código.** Etapas, franjas, duraciones, tipos de actividad (clase, recreo, guardia, seminario, estudio, aula matinal…), tipos de jornada, cuotas de servicios y nombres de asignaturas son **datos editables**.
2. **Un "curso escolar" es un conjunto de datos autocontenido** (franjas, cursos, profesores, asignaciones, aulas, servicios, reglas). Se puede **duplicar el del año anterior** y modificarlo.
3. **Las franjas son configurables por etapa**: número de filas, horas de inicio/fin por etapa, qué tipo es cada una (lectiva, recreo, almuerzo posible, tarde…). Primaria y Secundaria pueden compartir o no filas.
4. **Las etapas y grupos también son datos**: hoy 6 EPO, 4 ESO, 2 Bach, 2 BI con un solo grupo por curso, pero el modelo admitirá varias líneas (A/B) por si aparecen.
5. **Las reglas son un catálogo**: cada regla se activa/desactiva, es dura o blanda y tiene peso. Las reglas nuevas se añaden como módulos sin reescribir lo demás.
6. **Los tipos de servicio y tareas complementarias son extensibles**: se pueden crear nuevos (con sus plazas por franja y cuota por jornada) desde el programa.
7. **Los datos tienen versión** (`version_esquema`) para poder migrar cursos antiguos si el formato evoluciona.
8. **Lo que hoy es excepción debe poder ser regla y viceversa** (p. ej. Matemáticas II / CCSS): sin casos especiales en el código.
9. **Pruebas con varios "colegios" sintéticos** (distintas franjas, jornadas y etapas) para comprobar que nada depende de la configuración de 2026-27.
