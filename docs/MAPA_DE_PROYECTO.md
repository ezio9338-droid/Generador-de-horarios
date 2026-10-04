# Generador de horarios del colegio — Mapa de proyecto

> Borrador v0.1. Se completará con las respuestas de `PREGUNTAS.md`.

## 1. Objetivo

Generar automáticamente los horarios de **todos los profesores** (y, como consecuencia, de todos los grupos y aulas) del colegio, respetando:

- carga lectiva de cada profesor,
- cursos/grupos a los que da clase y asignaturas que imparte,
- desdobles, agrupamientos y optativas,
- servicios (recreos, guardias, biblioteca, comedor, entradas/salidas…),
- restricciones duras (obligatorias) y blandas (deseables, con peso).

## 2. Por qué es difícil (y por qué otros han fallado)

Es un problema NP-difícil (*School Timetabling*) con muchas reglas que se cruzan. Los fallos típicos de las herramientas comerciales:

1. **Reglas mal capturadas**: las reglas reales del colegio están en la cabeza de jefatura de estudios, no escritas. Si no se escriben, el programa "cumple" y el horario no sirve.
2. **Todo duro o todo blando**: sin distinguir "imposible de romper" de "preferible", o no hay solución o sale un horario feo.
3. **Sin explicación cuando no hay solución**: dicen "infactible" sin decir por qué.
4. **Sin edición manual posterior**: el horario perfecto no existe a la primera; hay que poder fijar cosas y regenerar el resto.
5. **Datos sucios**: cargas que no suman, profesores con más horas que huecos disponibles, etc.

**Principio del proyecto:** primero *entender y validar los datos y reglas*, después resolver, y siempre poder *explicar* el resultado.

## 3. Enfoque técnico propuesto

- **Motor de resolución:** programación por restricciones con **Google OR-Tools CP-SAT** (estándar de la industria para este tipo de problemas; permite restricciones duras + función objetivo con penalizaciones; gratuito).
- **Lenguaje:** Python (decisión pendiente de confirmar, ver preguntas).
- **Datos de entrada:** hojas Excel/CSV o JSON/YAML versionados en el repo (fácil de revisar y corregir por jefatura).
- **Salida:** horarios por profesor, grupo y aula en Excel/PDF + informe de calidad (qué reglas blandas se incumplen y cuánto).
- **Interfaz:** empezar por línea de comandos + Excel; web/escritorio sólo si hace falta (fase final).

## 4. Fases

### Fase 0 — Descubrimiento (estamos aquí)
- Responder `PREGUNTAS.md`.
- Recoger **datos reales de un curso anterior** (aunque sea en Excel desordenado) y **el horario que se hizo a mano**: sirve como caso de prueba y para validar el motor.
- Redactar el **catálogo de reglas** (duras/blandas) y que jefatura lo firme.
- **Entregable:** documento de requisitos + conjunto de datos de ejemplo.

### Fase 1 — Modelo de datos y validación de entrada
- Definir esquema: franjas horarias, etapas, cursos, grupos, asignaturas, profesores, aulas, desdobles, servicios.
- Importador desde Excel/CSV + **validador** con mensajes claros (p. ej. "Prof. X tiene 25 h lectivas pero sólo 22 franjas disponibles").
- **Entregable:** `python validar datos.xlsx` que dice si los datos son coherentes *antes* de resolver.

### Fase 2 — Núcleo mínimo (MVP del solver)
- Sólo lo básico: cada asignatura de cada grupo con sus horas semanales, un profesor no en dos sitios a la vez, un grupo no con dos profesores a la vez, disponibilidad de profesores.
- Comprobador independiente del horario (verifica cualquier horario, hecho a mano o por el programa).
- **Entregable:** horario válido para un subconjunto (p. ej. una etapa).

### Fase 3 — Reglas pedagógicas y de centro
- Desdobles, agrupamientos y optativas simultáneas, aulas/laboratorios/pabellón, bloques de 2 horas, distribución semanal (no 2 días seguidos de lo mismo, materias duras a primera hora, etc.), tutorías, reuniones, coordinaciones.
- Máximos de horas seguidas, huecos, días libres, conciliación.
- **Entregable:** horario completo de la etapa con todas las reglas del catálogo.

### Fase 4 — Servicios: recreos, guardias, vigilancias
- Cuadrante de recreos/patios, guardias de aula, de pasillo, biblioteca, comedor, entradas/salidas, transporte.
- Reparto **equitativo** y con reglas (quién puede/no puede, límites semanales).
- Integración con el horario lectivo (los servicios cuentan o no como carga según normativa/convenio).
- **Entregable:** horario completo del profesor incluyendo servicios.

### Fase 5 — Optimización y calidad
- Función objetivo con pesos configurables por jefatura (huecos, preferencias, equilibrio).
- Informe de calidad y de **conflictos explicados** ("no hay solución porque...").
- Rendimiento: tiempos razonables (minutos, no horas) y varias alternativas.
- **Entregable:** 3–5 propuestas de horario comparables.

### Fase 6 — Edición manual y re-planificación
- Fijar (bloquear) clases/servicios y regenerar el resto con el mínimo de cambios.
- Gestión de **incidencias a mitad de curso**: baja de un profesor, cambio de grupo, sustituciones.
- **Entregable:** flujo "cambio → regenerar → ver diferencias".

### Fase 7 — Salidas e interfaz
- Exportación: horario por profesor/grupo/aula (Excel, PDF), formato para importar en la plataforma del colegio (si existe: Séneca, Alexia, Educamos, iSéneca, etc., según el caso).
- Interfaz sencilla para jefatura (probablemente web local).
- **Entregable:** versión utilizable por personal no técnico.

### Fase 8 — Pruebas con datos reales y puesta en producción
- Comparar con el horario manual del curso anterior; piloto en paralelo un curso.
- Documentación y formación; mantenimiento y plan de cambios anuales.

## 5. Riesgos principales

| Riesgo | Mitigación |
|---|---|
| Reglas no escritas / contradictorias | Fase 0: catálogo de reglas firmado; ejemplos reales |
| Datos de entrada incoherentes | Fase 1: validador estricto antes de resolver |
| No hay solución con todas las reglas | Clasificar duras/blandas; explicar el conflicto; relajación controlada |
| Rendimiento (problema enorme) | Resolver por etapas/capas; usar CP-SAT; empezar con un subconjunto |
| Alcance que crece sin fin | Fases con entregables claros; el MVP no incluye servicios |
| Normativa distinta según comunidad/convenio | Definir en Fase 0 qué normativa aplica |

## 6. Criterios de éxito

1. Genera un horario **completo y válido** (0 reglas duras rotas) para el colegio entero.
2. Un humano de jefatura lo revisa y lo considera **aceptable sin rehacerlo desde cero**.
3. Tarda en generarse un tiempo razonable y es **reproducible**.
4. Permite **cambios puntuales** sin romper el resto.
5. Si no hay solución, **dice por qué**.

## 7. Estructura prevista del repositorio

```
Generador-de-horarios/
├── docs/                 # Mapa de proyecto, preguntas, catálogo de reglas
├── datos/                # Datos de ejemplo/reales (anonimizados)
├── src/                  # Código (modelo, validador, solver, exportadores)
├── tests/                # Pruebas con casos pequeños y reales
└── README.md
```
