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
