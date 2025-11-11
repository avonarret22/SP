================================================================================
    ESTIMADOR DE PUNTOS DE HISTORIA - GUÍA PARA AGILISTAS Y DESARROLLADORES
================================================================================

📊 VERSIÓN: 2.0 (Filosofía Scrum Ortodoxa)
📅 ÚLTIMA ACTUALIZACIÓN: Noviembre 2025
👥 EQUIPO: Santander - Development Team


================================================================================
1. ¿QUÉ ES ESTA HERRAMIENTA?
================================================================================

El Estimador de Puntos de Historia es una herramienta web standalone (sin instalación) 
diseñada para ayudar a equipos Scrum a estimar historias de usuario de forma 
CONSISTENTE y ALINEADA.

🎯 OBJETIVO PRINCIPAL:
Resolver el problema de estimaciones inconsistentes dentro del equipo, donde diferentes 
desarrolladores asignan puntos muy distintos a historias similares.

🔑 FILOSOFÍA BASE:
Esta herramienta sigue la filosofía SCRUM ORTODOXA:
- Los Story Points miden ESFUERZO del equipo, NO tiempo calendario
- Las esperas, bloqueos y aprobaciones NO se cuentan como esfuerzo
- Solo se estima el trabajo activo de desarrollo


================================================================================
2. ¿CÓMO FUNCIONA EL CÁLCULO?
================================================================================

El estimador usa un ALGORITMO DE PROMEDIO PONDERADO que combina 5 criterios 
principales más un factor de experiencia del equipo.

--------------------------------------------------------------------------------
2.1 LOS 5 CRITERIOS DE EVALUACIÓN
--------------------------------------------------------------------------------

Cada criterio se evalúa en una escala Likert de 1 a 5:

┌─────────────────────────────────────────────────────────────────────────────┐
│ 1️⃣  VOLUMEN DE TRABAJO (30% del peso total)                                │
│                                                                             │
│ ¿Qué mide? Cantidad de trabajo activo de desarrollo                        │
│ ¿Qué NO incluye? Esperas, aprobaciones, bloqueos, tiempo entre tareas      │
│                                                                             │
│ Escala:                                                                     │
│   1 = Mínimo (<4 horas de trabajo activo)                                  │
│   2 = Bajo (1 día de trabajo)                                              │
│   3 = Medio (2-3 días de trabajo)                                          │
│   4 = Alto (1 semana de trabajo)                                           │
│   5 = Muy Alto (>1 semana de trabajo)                                      │
│                                                                             │
│ Ejemplo: "Migrar 50 tablas de Excel a BD manualmente"                      │
│   → Volumen = 5 (es trabajo tedioso pero largo)                            │
│   → Aunque sea copiar-pegar, consume 1+ semana de esfuerzo activo          │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 2️⃣  COMPLEJIDAD TÉCNICA (30% del peso total)                               │
│                                                                             │
│ ¿Qué mide? Dificultad del problema a resolver                              │
│ Considera: Algoritmos, arquitectura, patrones, performance, escalabilidad  │
│                                                                             │
│ Escala:                                                                     │
│   1 = Muy Simple (problema conocido, solución estándar)                    │
│   2 = Simple (familiar, ya lo hicimos antes)                               │
│   3 = Moderada (entendible, requiere pensar un poco)                       │
│   4 = Compleja (desafiante, requiere investigación)                        │
│   5 = Muy Compleja (difícil, múltiples componentes interrelacionados)     │
│                                                                             │
│ Ejemplo: "Implementar algoritmo de recomendación personalizado"            │
│   → Complejidad = 5 (machine learning, múltiples variables)                │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 3️⃣  INCERTIDUMBRE / RIESGO (20% del peso total)                            │
│                                                                             │
│ ¿Qué mide? Cuánto desconoces sobre la tarea                                │
│ Considera: Requisitos poco claros, tecnología nueva, dependencias          │
│           inciertas, cambios de alcance                                    │
│                                                                             │
│ Escala:                                                                     │
│   1 = Nula (todo claro, sin sorpresas esperadas)                           │
│   2 = Baja (casi claro, alguna duda menor)                                 │
│   3 = Media (dudas leves, necesito aclarar algunos puntos)                 │
│   4 = Alta (muchas dudas, varios puntos poco claros)                       │
│   5 = Muy Alta (desconocido, muchas variables sin definir)                 │
│                                                                             │
│ Ejemplo: "Integrar con API de proveedor externo sin documentación"         │
│   → Incertidumbre = 5 (no sabemos cómo funciona, puede cambiar)            │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 4️⃣  ESFUERZO TÉCNICO (10% del peso total)                                  │
│                                                                             │
│ ¿Qué mide? Demanda técnica adicional                                       │
│ Considera: Cantidad de código, archivos a modificar, integraciones         │
│                                                                             │
│ Escala:                                                                     │
│   1 = Trivial (cambio menor, 1-2 archivos)                                 │
│   2 = Bajo (simple, pocos archivos)                                        │
│   3 = Medio (normal, varios componentes)                                   │
│   4 = Alto (complejo, múltiples módulos)                                   │
│   5 = Muy Alto (muy complejo, afecta muchos sistemas)                      │
│                                                                             │
│ Ejemplo: "Agregar nuevo campo a formulario existente"                      │
│   → Esfuerzo = 2 (simple, frontend + backend + BD)                         │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 5️⃣  COMPLEJIDAD DE TESTING/QA (10% del peso total)                         │
│                                                                             │
│ ¿Qué mide? Dificultad de probar la funcionalidad                           │
│ Considera: Cantidad de escenarios, casos edge, E2E, regresión,             │
│           performance, múltiples navegadores/dispositivos                  │
│                                                                             │
│ Escala:                                                                     │
│   1 = Trivial (solo happy path, pruebas básicas)                           │
│   2 = Bajo (pocos casos de prueba)                                         │
│   3 = Medio (testing normal, varios escenarios)                            │
│   4 = Alto (E2E, regresión, múltiples casos)                               │
│   5 = Muy Alto (crítico, testing extenso, múltiples ambientes)             │
│                                                                             │
│ Ejemplo: "Flujo de pago con múltiples métodos y validaciones"              │
│   → Testing = 5 (crítico, muchos escenarios, datos sensibles)              │
└─────────────────────────────────────────────────────────────────────────────┘


--------------------------------------------------------------------------------
2.2 FACTOR DE EXPERIENCIA DEL EQUIPO
--------------------------------------------------------------------------------

Este factor MULTIPLICA el resultado del promedio ponderado.

Escala:
  1 = Primera vez      → Multiplicador 1.5x  (+50% de dificultad)
  2 = Poco familiarizado → Multiplicador 1.25x (+25% de dificultad)
  3 = Moderado         → Multiplicador 1.0x  (sin cambio)
  4 = Expertos         → Multiplicador 0.80x (-20% de dificultad)
  5 = Ya lo hicimos    → Multiplicador 0.60x (-40% de dificultad)

🔑 RAZÓN: Un equipo experto completa tareas más rápido y con menos riesgo.


================================================================================
3. FÓRMULA DE CÁLCULO PASO A PASO
================================================================================

PASO 1: Calcular el Promedio Ponderado Base
────────────────────────────────────────────

Promedio = (Volumen × 0.30) + (Complejidad × 0.30) + (Incertidumbre × 0.20) +
           (Esfuerzo × 0.10) + (Testing × 0.10)

Ejemplo:
  Volumen = 3
  Complejidad = 4
  Incertidumbre = 2
  Esfuerzo = 3
  Testing = 2

  Promedio = (3×0.30) + (4×0.30) + (2×0.20) + (3×0.10) + (2×0.10)
          = 0.90 + 1.20 + 0.40 + 0.30 + 0.20
          = 3.00


PASO 2: Aplicar el Factor de Experiencia
─────────────────────────────────────────

Promedio Ajustado = Promedio Base × Factor de Experiencia

Siguiendo el ejemplo (con Experiencia = 4 "Expertos"):
  Promedio Ajustado = 3.00 × 0.80 = 2.40


PASO 3: Mapear a la Secuencia de Fibonacci
───────────────────────────────────────────

El promedio ajustado se convierte en puntos de Fibonacci según estos umbrales:

  Promedio ≤ 1.8  →  1 punto   (Tareas triviales)
  Promedio ≤ 2.6  →  2 puntos  (Tareas simples)
  Promedio ≤ 3.8  →  3 puntos  (Tareas normales)
  Promedio ≤ 4.5  →  5 puntos  (Tareas complejas)
  Promedio > 4.5  →  8 puntos  (Tareas muy complejas)

En nuestro ejemplo:
  Promedio Ajustado = 2.40
  → Cae en el rango ≤ 2.6
  → RESULTADO FINAL: 2 puntos


PASO 4: Aplicar Reglas Especiales
──────────────────────────────────

Existen reglas que pueden SOBREESCRIBIR el resultado anterior:

REGLA 1: "Todo al máximo"
  SI todos los criterios = 5 → ENTONCES 13 puntos (requiere refinamiento)

REGLA 2: "Incertidumbre extrema"
  SI incertidumbre = 5 Y promedio > 4.2 → ENTONCES 13 puntos

REGLA 3: "Testing crítico"
  SI testing = 5 Y volumen ≥ 4 → ENTONCES suma 2 puntos
  (No puede exceder 13)

REGLA 4: "Primera vez + complejo"
  SI experiencia = 1 Y promedio > 3.5 → ENTONCES suma 2 puntos
  (No puede exceder 13)


================================================================================
4. EJEMPLOS PRÁCTICOS COMPLETOS
================================================================================

────────────────────────────────────────────────────────────────────────────
EJEMPLO 1: Tarea Simple
────────────────────────────────────────────────────────────────────────────
HU: "Cambiar el color de un botón en la pantalla principal"

Evaluación:
  • Volumen: 1 (<4 horas)
  • Complejidad: 1 (muy simple)
  • Incertidumbre: 1 (todo claro)
  • Esfuerzo: 1 (trivial)
  • Testing: 1 (solo happy path)
  • Experiencia: 5 (ya lo hicimos mil veces)

Cálculo:
  Promedio = (1×0.30) + (1×0.30) + (1×0.20) + (1×0.10) + (1×0.10) = 1.00
  Ajustado = 1.00 × 0.60 = 0.60
  → 0.60 ≤ 1.8 → 1 PUNTO ✅

────────────────────────────────────────────────────────────────────────────
EJEMPLO 2: Tarea Media con Incertidumbre
────────────────────────────────────────────────────────────────────────────
HU: "Integrar con nueva API de notificaciones push"

Evaluación:
  • Volumen: 3 (2-3 días)
  • Complejidad: 3 (moderada, tenemos experiencia con APIs)
  • Incertidumbre: 4 (documentación incompleta, puede cambiar)
  • Esfuerzo: 3 (varios componentes)
  • Testing: 4 (E2E, múltiples dispositivos)
  • Experiencia: 3 (moderado)

Cálculo:
  Promedio = (3×0.30) + (3×0.30) + (4×0.20) + (3×0.10) + (4×0.10) = 3.40
  Ajustado = 3.40 × 1.0 = 3.40
  → 3.40 ≤ 3.8 → 3 PUNTOS ✅

────────────────────────────────────────────────────────────────────────────
EJEMPLO 3: Tarea Compleja Primera Vez
────────────────────────────────────────────────────────────────────────────
HU: "Implementar sistema de recomendaciones con Machine Learning"

Evaluación:
  • Volumen: 5 (>1 semana)
  • Complejidad: 5 (muy compleja, múltiples componentes)
  • Incertidumbre: 5 (tecnología nueva para el equipo)
  • Esfuerzo: 5 (muy alto, muchos sistemas afectados)
  • Testing: 5 (crítico, validación de precisión, performance)
  • Experiencia: 1 (primera vez)

Cálculo:
  Promedio = (5×0.30) + (5×0.30) + (5×0.20) + (5×0.10) + (5×0.10) = 5.00
  Ajustado = 5.00 × 1.5 = 7.50

  ⚠️ REGLA ESPECIAL APLICA:
  - Todos los criterios = 5 → 13 PUNTOS
  - Promedio > 4.5 → 8 puntos
  - Experiencia = 1 Y promedio > 3.5 → suma 2 puntos

  → RESULTADO: 13 PUNTOS (REQUIERE REFINAMIENTO) 🚨

────────────────────────────────────────────────────────────────────────────
EJEMPLO 4: Tarea Tediosa pero Simple
────────────────────────────────────────────────────────────────────────────
HU: "Migrar 100 registros manualmente de sistema legacy"

Evaluación:
  • Volumen: 4 (1 semana de trabajo tedioso)
  • Complejidad: 1 (es copy-paste)
  • Incertidumbre: 1 (sabemos exactamente qué hacer)
  • Esfuerzo: 2 (bajo, pero voluminoso)
  • Testing: 2 (validar migraciones)
  • Experiencia: 4 (expertos)

Cálculo:
  Promedio = (4×0.30) + (1×0.30) + (1×0.20) + (2×0.10) + (2×0.10) = 2.10
  Ajustado = 2.10 × 0.80 = 1.68
  → 1.68 ≤ 1.8 → 1 PUNTO

  ⚠️ PERO ESPERA:
  Aunque la complejidad sea baja, el VOLUMEN es 4 (1 semana).
  En filosofía Scrum: 1 semana de trabajo ≠ 1 punto

  💡 RECOMENDACIÓN AUTOMÁTICA:
  "⏰ Alto volumen + baja complejidad: Aunque sea tedioso, considera 
  dividir la HU o estimar según el tiempo real que consume del sprint"

  → DECISIÓN DEL EQUIPO: Podría ser 3 puntos (más realista)


================================================================================
5. ¿POR QUÉ ESTOS PESOS?
================================================================================

┌──────────────────┬────────┬───────────────────────────────────────────────┐
│ CRITERIO         │ PESO   │ JUSTIFICACIÓN                                 │
├──────────────────┼────────┼───────────────────────────────────────────────┤
│ Volumen          │ 30%    │ El trabajo activo es el principal driver de   │
│                  │        │ consumo de capacity en el sprint. Más trabajo │
│                  │        │ = más puntos, independiente de complejidad.   │
├──────────────────┼────────┼───────────────────────────────────────────────┤
│ Complejidad      │ 30%    │ La dificultad técnica afecta directamente el  │
│                  │        │ tiempo y riesgo. Tareas complejas requieren   │
│                  │        │ más esfuerzo cognitivo y debugging.           │
├──────────────────┼────────┼───────────────────────────────────────────────┤
│ Incertidumbre    │ 20%    │ El riesgo e incertidumbre agregan tiempo por  │
│                  │        │ investigación, prueba-error y re-trabajo.     │
├──────────────────┼────────┼───────────────────────────────────────────────┤
│ Esfuerzo         │ 10%    │ Es un complemento al volumen y complejidad.   │
│                  │        │ Peso menor porque ya está capturado en otros. │
├──────────────────┼────────┼───────────────────────────────────────────────┤
│ Testing          │ 10%    │ Testing es crítico pero a menudo es paralelo  │
│                  │        │ al desarrollo. Peso menor pero explícito.     │
└──────────────────┴────────┴───────────────────────────────────────────────┘

🔑 FILOSOFÍA: Volumen + Complejidad son los drivers principales (60%).
              Los demás factores son ajustes (40%).


================================================================================
6. DEPENDENCIAS Y BLOQUEADORES
================================================================================

La herramienta incluye 5 checkboxes de dependencias:

  ☐ Depende de Backend
  ☐ Requiere Diseño
  ☐ Requiere API Externa
  ☐ Requiere Testing Extensivo
  ☐ Requiere Documentación

⚠️ IMPORTANTE: Estos checkboxes NO afectan el cálculo de puntos directamente.

¿Para qué sirven entonces?
  • Generan RECOMENDACIONES automáticas
  • Si marcas ≥3 dependencias → alerta de riesgo alto de bloqueos
  • Si marcas alto volumen + ≥2 dependencias → alerta sobre tiempo calendario


================================================================================
7. SISTEMA DE RECOMENDACIONES INTELIGENTES
================================================================================

La herramienta analiza tus inputs y genera recomendaciones contextuales.

Ejemplos de recomendaciones:

┌─────────────────────────────────────────────────────────────────────────────┐
│ ⚠️ ALTA: Mucha incertidumbre + poca experiencia = Riesgo muy alto.         │
│ La HU no está suficientemente definida. Considera hacer un SPIKE técnico   │
│ ANTES de commitear.                                                         │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ ✂️ Tarea compleja y larga: DIVIDIRLA en subtareas. Una HU grande es        │
│ difícil de testear, revisar y deployar.                                    │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 🧪 Testing complejo: El esfuerzo de QA es significativo. Asegúrate de      │
│ incluir tiempo para preparación de datos de prueba y casos edge.           │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ 🔗 3 dependencias: RIESGO ALTO de bloqueos. ¿Puedes priorizar las          │
│ dependencias primero o reducirlas?                                         │
└─────────────────────────────────────────────────────────────────────────────┘


================================================================================
8. HISTORIAL Y COMPARACIÓN
================================================================================

La herramienta guarda las estimaciones de la sesión actual.

Funcionalidades:
  • Muestra historial de HUs estimadas
  • Exporta a CSV con todos los detalles
  • Busca automáticamente historias SIMILARES en el historial
  • Ayuda a calibrar futuras estimaciones

Algoritmo de similitud:
  Suma la diferencia absoluta de todos los criterios:
  
  Diferencia = |volumen₁ - volumen₂| + |complejidad₁ - complejidad₂| + ...
  
  Si Diferencia ≤ 4 → Se considera "historia similar"


================================================================================
9. GUÍA DE PLANNING MEETING (INCLUIDA EN LA HERRAMIENTA)
================================================================================

La herramienta incluye una guía completa colapsable que explica:

  • ¿Qué es una Planning Meeting?
  • ¿Quiénes participan? (roles y responsabilidades)
  • Proceso paso a paso (6 pasos del dimensionamiento)
  • ¿Quién decide? (consenso del equipo)
  • Roles especializados según tipo de HU
  • Duración recomendada

Esta guía está diseñada para educar al equipo y estandarizar el proceso.


================================================================================
10. PREGUNTAS FRECUENTES (FAQ)
================================================================================

────────────────────────────────────────────────────────────────────────────
P1: ¿Por qué mi tarea de 3 días dio solo 1 punto?
────────────────────────────────────────────────────────────────────────────

   
   Versión antigua: "Tiempo Requerido" medía días calendario
   Versión nueva: "Volumen de Trabajo" mide trabajo ACTIVO
   
   Además, los pesos cambiaron:
   - Antes: Tiempo 25%
   - Ahora: Volumen 30%
   
   Con los nuevos criterios, una tarea de 3 días de trabajo activo con 
   complejidad baja debería dar al menos 2-3 puntos.


────────────────────────────────────────────────────────────────────────────
P2: ¿Qué hago si el equipo no está de acuerdo con el resultado?
────────────────────────────────────────────────────────────────────────────

R: ¡Perfecto! Esa es exactamente la intención.
   
   La herramienta es un FACILITADOR de la conversación, no un dictador.
   
   Pasos:
   1. Usa el resultado como punto de partida
   2. Discute POR QUÉ el equipo cree que debería ser diferente
   3. Revisen los criterios: ¿evaluaron bien cada uno?
   4. Ajusten la evaluación si descubren algo nuevo
   5. O decidan como equipo usar otro valor (Planning Poker)
   
   La herramienta NO reemplaza el consenso del equipo.


────────────────────────────────────────────────────────────────────────────
P3: ¿Por qué Volumen y Complejidad tienen el mismo peso (30%)?
────────────────────────────────────────────────────────────────────────────

R: Porque ambos son drivers igualmente importantes:
   
   • Volumen: Cantidad de trabajo (tiempo activo)
   • Complejidad: Dificultad del problema
   
   Una tarea puede ser:
   - Alta complejidad + bajo volumen (algoritmo difícil, pocas líneas)
   - Baja complejidad + alto volumen (migración manual, mucho trabajo)
   
   Ambos casos merecen puntos significativos. El peso 30/30 refleja esto.


────────────────────────────────────────────────────────────────────────────
P4: ¿Qué significa "trabajo activo" en Volumen?
────────────────────────────────────────────────────────────────────────────

R: Trabajo activo = Tiempo que estás realmente codificando/implementando
   
   INCLUYE:
   • Escribir código
   • Hacer testing
   • Debugging
   • Code review
   • Refactoring
   
   NO INCLUYE:
   • Esperar aprobaciones
   • Esperar que backend termine su parte
   • Esperar diseños de UX
   • Tiempo bloqueado por dependencias
   • Tiempo entre tareas
   
   Pregunta clave: "Si me siento sin interrupciones, ¿cuánto tardo?"


────────────────────────────────────────────────────────────────────────────
P5: ¿Por qué las dependencias no afectan el puntaje directamente?
────────────────────────────────────────────────────────────────────────────

R: Porque en Scrum, los Story Points miden ESFUERZO del equipo, no tiempo 
   calendario.
   
   Ejemplo:
   - Tarea: Cambiar un texto (1 hora de trabajo)
   - Dependencia: Esperar 3 días a que diseño apruebe
   
   Esfuerzo real = 1 hora → 1 punto
   Tiempo calendario = 3 días → NO se cuenta en puntos
   
   PERO: Las dependencias SÍ generan alertas y recomendaciones para que 
   el equipo sea consciente del riesgo de bloqueos.


────────────────────────────────────────────────────────────────────────────
P6: ¿Qué hago si obtengo 13 puntos?
────────────────────────────────────────────────────────────────────────────

R: 13 puntos es una SEÑAL DE ALARMA que indica:
   
   "Esta HU es DEMASIADO GRANDE o DEMASIADO INCIERTA"
   
   Acciones recomendadas:
   1. DIVIDIR la HU en historias más pequeñas
   2. Si no se puede dividir: Hacer un SPIKE primero (2-3 pts)
   3. Volver a Planning cuando esté mejor definida
   
   Regla de oro: Ninguna HU debería ser > 8 puntos en el sprint.


────────────────────────────────────────────────────────────────────────────
P7: ¿Cómo uso el Factor de Experiencia correctamente?
────────────────────────────────────────────────────────────────────────────

R: Evalúa la FAMILIARIDAD DEL EQUIPO con esta tecnología/dominio:
   
   1 (Primera vez): 
      • Nadie en el equipo hizo esto antes
      • Ejemplo: Primera app React Native del equipo
   
   2 (Poco familiarizado):
      • Alguien lo hizo, pero no todos
      • Ejemplo: Solo 1 dev conoce GraphQL
   
   3 (Moderado):
      • La mitad del equipo tiene experiencia
      • Ejemplo: Algunos hicieron integraciones con SAP
   
   4 (Expertos):
      • Todo el equipo domina la tecnología
      • Ejemplo: APIs REST con Spring Boot (hacemos 10 por sprint)
   
   5 (Ya lo hicimos):
      • Literalmente YA hicimos esta tarea antes
      • Ejemplo: Agregar un campo a un formulario (lo hicimos 50 veces)


────────────────────────────────────────────────────────────────────────────
P8: ¿Por qué Testing solo pesa 10%?
────────────────────────────────────────────────────────────────────────────

R: Tres razones:
   
   1. Testing a menudo es PARALELO al desarrollo (no suma tiempo lineal)
   2. Ya está parcialmente capturado en "Volumen" y "Esfuerzo"
   3. 10% es suficiente para diferenciar entre HUs simples vs críticas
   
   Sin embargo, si testing = 5 (crítico), la herramienta aplica reglas 
   especiales que pueden sumar +2 puntos adicionales.
   
   El peso es bajo, pero el impacto puede ser alto cuando corresponde.


────────────────────────────────────────────────────────────────────────────
P9: ¿Puedo modificar los pesos de los criterios?
────────────────────────────────────────────────────────────────────────────

R: Sí, pero NO es recomendable a menos que:
   
   1. Tu equipo tiene datos históricos que justifiquen el cambio
   2. Han probado los pesos actuales por al menos 3 sprints
   3. Toda el equipo está de acuerdo en el cambio
   
   Los pesos actuales (30/30/20/10/10) están basados en la filosofía 
   Scrum ortodoxa y experiencia de múltiples equipos.
   
   Si decides cambiarlos:
   - Edita el objeto 'weights' en el código JavaScript (línea ~1265)
   - Asegúrate que la suma sea 1.0 (100%)
   - Documenta POR QUÉ hiciste el cambio


────────────────────────────────────────────────────────────────────────────
P10: ¿Cómo calibro al equipo para usar esta herramienta?
────────────────────────────────────────────────────────────────────────────

R: Proceso de calibración (sesión de 2 horas):
   
   PASO 1: Seleccionar 5-7 HUs del sprint anterior
          (historias completadas que el equipo conoce bien)
   
   PASO 2: Para cada HU, el equipo evalúa los 5 criterios en conjunto
          (sin ver el puntaje final)
   
   PASO 3: Comparar el resultado de la herramienta vs lo que estimaron
          originalmente
   
   PASO 4: Discutir las diferencias:
          • ¿Evaluamos bien cada criterio?
          • ¿Los criterios reflejan la realidad?
          • ¿Faltó considerar algo?
   
   PASO 5: Crear "Ejemplos de Referencia" del equipo:
          • "Una HU como X vale 3 puntos"
          • "Una HU como Y vale 5 puntos"
   
   PASO 6: Documentar estos ejemplos en la herramienta
   
   PASO 7: Usar en las próximas 2-3 Plannings y ajustar según aprendizaje


────────────────────────────────────────────────────────────────────────────
P11: ¿Qué hago si dos devs evalúan los mismos criterios diferente?
────────────────────────────────────────────────────────────────────────────

R: ¡Excelente! Esa diferencia es VALIOSA. Significa que hay distintas 
   perspectivas.
   
   Proceso:
   1. Cada dev comparte POR QUÉ evaluó así
      • Frontend: "Para mí Complejidad = 2 porque solo es un formulario"
      • Backend: "Para mí Complejidad = 4 porque hay validaciones complejas"
   
   2. Discuten y llegan a consenso
      • Deciden: Complejidad = 3 (término medio)
   
   3. Usan ese valor consensuado en la herramienta
   
   La herramienta NO es para estimar solo. Es para estimar EN EQUIPO.


────────────────────────────────────────────────────────────────────────────
P12: ¿Cuándo marco "Requiere Testing Extensivo" en dependencias?
────────────────────────────────────────────────────────────────────────────

R: Marca este checkbox cuando:
   
   ✅ SÍ marcar:
   • Requiere testing E2E completo
   • Necesita testing de regresión extenso
   • Debe probarse en múltiples ambientes/configuraciones
   • Testing es crítico para el negocio (ej: flujo de pagos)
   
   ❌ NO marcar:
   • Testing normal de unit tests
   • Pruebas básicas de integración
   • Testing que ya está incluido en el proceso estándar
   
   Nota: Esto es DIFERENTE al criterio "Complejidad de Testing/QA".
         El checkbox es para marcar dependencias que pueden bloquear.


────────────────────────────────────────────────────────────────────────────
P13: ¿La herramienta guarda las estimaciones permanentemente?
────────────────────────────────────────────────────────────────────────────

R: NO. La herramienta guarda el historial solo durante la SESIÓN ACTUAL.
   
   ¿Qué significa?
   • Mientras tengas la pestaña abierta: historial disponible
   • Si cierras la pestaña o recargas la página: historial se pierde
   
   ¿Cómo guardar permanentemente?
   1. Usar el botón "📥 Exportar a CSV" al final de la Planning
   2. Guardar el CSV en una carpeta compartida del equipo
   3. Usar ese CSV como referencia histórica para próximas Plannings
   
   Futuro: Podríamos agregar LocalStorage para persistencia entre sesiones.


────────────────────────────────────────────────────────────────────────────
P14: ¿Qué significa "Promedio ponderado: 3.50" en el resultado?
────────────────────────────────────────────────────────────────────────────

R: Es el valor ANTES de mapear a Fibonacci. Es útil para entender el cálculo.
   
   Interpretación:
   • < 2.0: Tarea simple
   • 2.0 - 3.5: Tarea normal
   • 3.5 - 4.5: Tarea compleja
   • > 4.5: Tarea muy compleja
   
   Si ves "Promedio ponderado: 3.50" y el resultado es "5 puntos", 
   significa que:
   1. El cálculo base dio 3.50
   2. Aplicando reglas especiales o factor de experiencia, se ajustó
   3. Se mapeó al Fibonacci más cercano → 5 puntos
   
   Este número es TRANSPARENTE para que el equipo entienda el cálculo.


────────────────────────────────────────────────────────────────────────────
P15: ¿Puedo usar esta herramienta para otros frameworks además de Scrum?
────────────────────────────────────────────────────────────────────────────

R: SÍ, con adaptaciones:
   
   KANBAN:
   • Los criterios siguen siendo relevantes
   • Usa "Tamaño de Tarea" en lugar de "Story Points"
   • Los umbrales Fibonacci pueden ser S/M/L/XL
   
   SCRUMBAN:
   • Funciona igual que con Scrum
   • Útil para dimensionar el WIP limit
   
   CASCADA ÁGIL:
   • Puedes usarlo para estimar complejidad
   • Los puntos se traducen a días/semanas
   
   XP (Extreme Programming):
   • Compatible 100%
   • XP usa Story Points igual que Scrum
   
   SAFe:
   • Compatible con PI Planning
   • Usa los mismos criterios a nivel de Features/Epics
   
   ADAPTACIÓN: Ajusta la terminología pero mantén la filosofía de evaluar 
               múltiples dimensiones de complejidad.


================================================================================
11. TIPS Y MEJORES PRÁCTICAS
================================================================================

✅ DO (Hacer):
  • Usar la herramienta EN EQUIPO durante Planning
  • Discutir las diferencias de evaluación entre miembros
  • Revisar el historial para calibrar futuras estimaciones
  • Exportar a CSV al final de cada Planning
  • Usar las recomendaciones como guía de discusión
  • Marcar dependencias para visibilidad de riesgos

❌ DON'T (No hacer):
  • Usar la herramienta en solitario y decir "esta es la estimación"
  • Confiar ciegamente en el resultado sin discutir
  • Ignorar el contexto del equipo (experiencia, velocidad)
  • Forzar el uso si el equipo prefiere Planning Poker puro
  • Modificar pesos sin justificación basada en datos

⚠️ CUIDADO CON:
  • Confundir "volumen de trabajo" con "tiempo calendario"
  • Evaluar testing muy bajo por default (suele ser subestimado)
  • Marcar todas las dependencias "por si acaso"
  • Usar experiencia = 5 cuando en realidad es 3
  • Aceptar 13 puntos sin dividir la HU


================================================================================
12. TROUBLESHOOTING
================================================================================

PROBLEMA: "La herramienta da puntos muy bajos"
CAUSA: Probablemente estás subestimando volumen o complejidad
SOLUCIÓN: Revisa si evaluaste el trabajo REAL necesario

PROBLEMA: "Todos los resultados dan 3 o 5 puntos"
CAUSA: Falta granularidad en las evaluaciones
SOLUCIÓN: Sé más específico al evaluar. No uses "3" por default.

PROBLEMA: "El equipo no confía en los resultados"
CAUSA: Falta calibración inicial
SOLUCIÓN: Haz la sesión de calibración (ver P10)

PROBLEMA: "Los pesos no reflejan nuestra realidad"
CAUSA: Cada equipo es diferente
SOLUCIÓN: Documenta casos específicos y ajusta pesos con consenso

PROBLEMA: "Las recomendaciones son muy genéricas"
CAUSA: Es inteligencia artificial simple basada en reglas
SOLUCIÓN: Úsalas como punto de partida, no como verdad absoluta


================================================================================
13. GLOSARIO DE TÉRMINOS
================================================================================

Story Points: Unidad de medida relativa de complejidad/esfuerzo en Scrum

Fibonacci: Secuencia 1,2,3,5,8,13... usada para forzar diferenciación

Likert Scale: Escala de 1-5 para evaluar cada criterio

Promedio Ponderado: Suma de valores multiplicados por sus pesos

Mapeo a Fibonacci: Conversión del promedio a la secuencia de Fibonacci

Spike: Historia técnica de investigación (2-3 puntos típicamente)

Refinamiento: Dividir una historia grande en historias más pequeñas

Velocity: Cantidad promedio de puntos que el equipo completa por sprint

Capacity: Puntos totales que el equipo puede comprometer en un sprint

Planning Poker: Técnica de estimación colaborativa con cartas

Buffer: Margen de seguridad adicional en la estimación


================================================================================
14. REFERENCIAS Y RECURSOS
================================================================================

📚 LECTURAS RECOMENDADAS:

• "Agile Estimating and Planning" - Mike Cohn
  (Fundamentos de Story Points y Planning Poker)

• "Scrum Guide" - Ken Schwaber & Jeff Sutherland
  (Definición oficial de Scrum y Planning Meeting)

• "User Stories Applied" - Mike Cohn
  (Cómo escribir y estimar historias de usuario)


🔗 RECURSOS ONLINE:

• Mountain Goat Software - Agile Estimating
  https://www.mountaingoatsoftware.com/agile/planning-poker

• Scrum.org - Evidence-Based Management
  https://www.scrum.org/resources/evidence-based-management

• Atlassian - Story Points and Estimation
  https://www.atlassian.com/agile/project-management/estimation


================================================================================
15. CHANGELOG - HISTORIAL DE VERSIONES
================================================================================

VERSION 2.0 (Noviembre 2025) - FILOSOFÍA SCRUM ORTODOXA
  • Renombrado "Tiempo Requerido" → "Volumen de Trabajo"
  • Redistribución de pesos: 30/30/20/10/10
  • Énfasis en trabajo activo vs tiempo calendario
  • Nueva escala Likert para Volumen
  • Nota educativa sobre filosofía Scrum
  • Recomendación específica para volumen + dependencias

VERSION 1.5 (Octubre 2025) - TESTING COMO CRITERIO EXPLÍCITO
  • Agregado "Complejidad de Testing/QA" como 5to criterio
  • Redistribución de pesos: 25/25/20/15/15
  • Regla especial para testing crítico
  • Tooltips en dependencias
  • Exportación incluye columna Testing

VERSION 1.0 (Septiembre 2025) - RELEASE INICIAL
  • 4 criterios: Tiempo, Esfuerzo, Complejidad, Incertidumbre
  • Factor de experiencia del equipo
  • Mapeo a Fibonacci
  • Sistema de recomendaciones
  • Guía de Planning Meeting colapsable
  • Historial y exportación CSV


================================================================================
16. SOPORTE Y CONTACTO
================================================================================

Para preguntas, sugerencias o reportar problemas:

📧 Email: [Tu email de equipo]
💬 Slack: #agile-tools
📊 Retrospectiva: Compartir feedback en Retro del sprint


================================================================================
ÚLTIMA ACTUALIZACIÓN: Noviembre 7, 2025
VERSIÓN: 2.0 - Filosofía Scrum Ortodoxa
EQUIPO: Santander Development Team
================================================================================
