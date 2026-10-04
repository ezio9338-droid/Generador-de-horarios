# Respuestas y decisiones (ronda 1)

## Contexto confirmado
- Colegio **privado en Andalucía**: libertad curricular, nombres de asignaturas variables, cargas de profesor que **no** coinciden con las de la pública.
- Usuaria principal: **jefa de estudios**. Hoy usa Excel, casi todo a mano, sin programación detrás → el programa debe ser **usable por una persona no técnica**.
- Plazo: **todo el curso actual** para desarrollarlo; el curso en marcha ya está montado (no hay presión de entrega inmediata, pero sí un objetivo claro: el curso siguiente).
- Empresas anteriores fallaron por **la cantidad de condicionantes** del centro (no recuerda nombres).
- Reglas de jefatura: **pendientes** (jefatura debe responder a la petición).

## Modelo de datos (lo que el programa debe relacionar)
Cada **asignación** = `profesor ↔ asignatura ↔ curso/grupo ↔ horas semanales`.

## Desdobles = "bloques simultáneos"
Ejemplo: en una rama de Bachillerato, Química, Dibujo Técnico e Historia del Arte se dan **a la misma hora y día**, con **3 profesores distintos** (cada alumno cursa una de ellas).
→ El programa debe permitir **declarar qué asignaturas desdoblan entre sí** y forzar que coincidan en día y franja.
(Más abajo hay preguntas para cerrar los detalles.)

## Servicios (carga complementaria)
- Tipos conocidos: **recreo de Primaria, recreo de Secundaria, 2 comedores de Primaria, guardia de biblioteca**.
- A cada profesor se le indica en el programa **cuántos** de cada tipo le corresponden, **según su tipo de jornada**.
- Cuentan como **carga complementaria** y ocurren **mientras otros cursos tienen clase** (por tanto interactúan con el horario lectivo del profesor).

## Franjas horarias
- La tabla de franjas **cambia de un curso a otro** → debe ser **editable en el programa**, y fija durante todo el curso.

## Consecuencias para el diseño
1. Necesitamos **interfaz de entrada de datos** desde el principio (no sólo importar Excel): profesores, asignaturas, cursos, asignaciones, franjas, servicios. Se mantendrá importación/exportación Excel.
2. **Nada fijo en el código**: franjas, nombres de asignaturas, tipos de servicio, tipos de jornada y cuotas deben ser **datos configurables**.
3. Las **reglas** también deben ser configurables (catálogo con activar/desactivar y peso), porque aún no están definidas.
4. Producto pensado para evolucionar durante el curso: entregar en incrementos que la jefa de estudios pueda probar.

---

# Respuestas y decisiones (ronda 2)

## Bloques simultáneos (desdobles)
- Las asignaturas de un bloque tienen **la misma carga semanal** y se **reparten igual entre días** (mismos días y franjas para todas).
- Hay bloques simultáneos también en **ESO** (no sólo Bachillerato).
- Existe un 2º tipo: **un mismo curso/grupo numeroso se parte** y se da **la misma asignatura a la vez con profesores distintos** (por nº de alumnos).
- Regla general (muy prioritaria): **una asignatura no se imparte dos veces el mismo día en el mismo curso**, "por todos los medios" (blanda con peso muy alto, o dura si la matemática lo permite).

## Jornada y servicios
- Tipos de jornada: **completa** y **reducida**. Hay que **indicar las horas de cada profesor** previamente.
- Nuevos tipos de actividad en el horario del profesor (además de recreos/comedor/guardia biblioteca):
  - **Guardias** (de sustitución, ver módulo de sustituciones).
  - **Seminarios por la tarde** (refuerzo, profesores de Secundaria; también hay de Primaria).
  - **Atención a familias** (tutorías).
  - **Almuerzo**: una hora obligatoria por profesor.
  - **Reuniones de equipos de trabajo**: los miembros del equipo deben **coincidir**.
- Reglas de lugar: no hay; sólo importa que no coincidan en franja con otra cosa.
- **Jornada completa de ejemplo: 8:30–16:30.**

## Ejemplo real (jefa de estudios, jornada completa)
| Concepto | Cantidad |
|---|---|
| Clases con 2º ESO | 3 |
| Clases con 3º ESO | 3 |
| Clases con 4º ESO | 3 |
| Clases con 1º Bach (rama salud) | 4 |
| Clases con 1º Bach (rama tecnológica) | 4 |
| Clases con 2º Bach (rama salud) | 4 |
| Clases con 2º Bach (rama tecnológica) | 4 |
| Seminarios (1 Secundaria, 1 Primaria) | 2 |
| Recreo | 1 |
| Guardias | 3 |
| Atención a familias | 1 |
| Almuerzo | 1 (obligatorio) |

## Centro
- **Etapas:** 6 cursos de Primaria, 4 de ESO, 2 de Bachillerato, 2 de Bachillerato Internacional.
- Horario **igual todos los días**; Primaria y Secundaria **no comparten todas las franjas** (algunas sí).
- **Aulas y profesores dinámicos** (se mueven los alumnos): el reparto de grupos debe **tener en cuenta la capacidad de las aulas**.
- **No hay condiciones personales** de profesores (días libres, etc.).
- Hay **profesores que dan clase en todas las etapas**.
- El Excel del curso actual llegará cuando jefatura responda; mientras tanto se avanza con lo disponible.

## Nuevo módulo: Sustituciones
Si un profesor falta un día:
1. Se toman todas sus **horas de clase** de ese día.
2. Cada una se **cubre con un profesor que tenga guardia asignada en esa franja**.
3. Se **genera un Excel de ese día** con el cuadrante de cobertura.
(Con reparto equitativo y avisos si faltan guardias en alguna franja.)

---

# Respuestas y decisiones (ronda 3) — a partir del horario de ejemplo (profesor de ejemplo, FQ, curso 2026-27)

## Aclaraciones
- **Cada curso tiene un único grupo** (no hay 2º ESO A/B). Lo máximo es que el grupo se **desdoble por modalidades/optativas**. "3 clases con 2º ESO" = **3 horas semanales** con ese grupo.
- La carga del ejemplo cuadra con la imagen: 2º/3º/4º ESO → 3 h cada uno; 1º Bach FQ Salud y FQ Tecn → 4 h cada uno; 2º Bach Física y Química → 4 h cada una; 2 seminarios, 1 recreo, 3 guardias, 1 tutoría de familias, 1 tutoría personal, 1 reunión, 1 estudio, almuerzo.
- **Jornada completa = 40 h/semana (8:30–16:30, L–V)**. Lo que no es clase ni complementaria son **"horas en blanco"** (disponibles para sustituciones). **Jornadas reducidas**: cada profesor tiene la suya (20, 30, 35 h…) y su horario se adapta a sus asignaturas/servicios.
- Un mismo profesor puede tener **tutoría personal** (horas con su propio grupo; **el nº varía de un curso a otro**). En Secundaria los tutores son profesores de área.
- El **reparto de alumnos y la asignación de aula en desdobles** la deciden los profesores; el programa **asigna aula según nº de alumnos**.
- **≈18 aulas**, cada una con nombre y **condicionantes** (p. ej. 1º–3º EPO sólo rotan entre aula 1 y aula 3). El detalle llegará más adelante.
- Matemáticas II / Matemáticas CCSS: el único caso de una asignatura repetida por bloques/modalidades de Bachillerato.

## Franjas del curso 2026-27 (de la imagen)
Cada fila es una franja global; las horas exactas dependen de la etapa (EPO = Primaria; ESO-BACH = Secundaria y Bachillerato).

| Fila | EPO | ESO-BACH |
|---|---|---|
| 0 | 7:30–8:45 (aula matinal / guardia) | igual |
| 1 | 8:45–9:45 | 8:45–9:45 |
| 2 | 9:45–10:45 | 9:45–10:45 |
| 3 | 10:45–11:15 **recreo** | 10:45–11:45 clase |
| 4 | 11:15–12:15 clase | 11:45–12:15 **recreo** |
| 5 | 12:15–13:15 | 12:15–13:15 |
| 6 | 13:15–14:15 | 13:15–14:15 (franja de **almuerzo posible**) |
| 7 | 14:15–15:05 | 14:15–15:15 |
| 8 | 15:05–15:50 | 15:15–15:40 **almuerzo** |
| 9 | 15:50–16:30 | 15:40–16:30 |

*(Pendiente de confirmar fila a fila; ver preguntas.)*

## Tipos de actividad vistos en el horario de ejemplo
Clase · Recreo (por zona: zona 1, pista, zona 2; **3 profesores por recreo**) · Guardia (hora de sustitución) · Almuerzo · Seminario (tarde; ESO / Bach / Primaria) · Tutoría de familias · Tutoría personal (con su grupo) · Reunión de equipo (innovación, I+D…) · Estudio (L–V, última franja de la tarde) · Aula matinal (7:30–8:15) y guardia de aula matinal.

## Equipos de trabajo y reuniones
- Equipos de **trabajo**: profesores de **cualquier etapa**. Reuniones de **departamento**: profesores del mismo departamento.
- Mínimo **1 reunión semanal por equipo**; el programa debe hacer **coincidir a los miembros**.

## Almuerzo
- Lo **elige el programa** dentro de las franjas posibles (en 2026-27: 13:15–14:15, 14:15–… y 15:05/15:15–…; puede cambiar cada curso).

## Sustituciones (ampliado)
- Si faltan guardias: se usan profesores con **hora en blanco**; si tampoco hay, **reestructuración temporal** (p. ej. "hoy este profesor come a otra hora y sustituye en ésta").
- **Excursiones**: el profesor que acompaña a un grupo necesita sustitución en las clases con **otros** grupos, **no** en las clases con el grupo que se va.
- Equidad deseable pero limitada por los huecos de cada docente (algunos casi no tienen).
