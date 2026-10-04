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
