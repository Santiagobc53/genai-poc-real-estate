# POC GenAI para Proyectos Inmobiliarios (IFC)
## Estructuración según CRISP-DM — Applied Generative AI Workshop (Twarco) + Vertex AI

**Repositorio:** genai-poc-real-estate  
**Plataforma objetivo (requisito del workshop):** Google Cloud Vertex AI (Gemini)  
**Duración demo objetivo:** 60–90 minutos  
**Estado:** POC demostrativa (no productiva)

---

## 0. Resumen Ejecutivo

Esta Prueba de Concepto (POC) demuestra cómo **GenAI** puede responder preguntas en lenguaje natural sobre un **proyecto inmobiliario** utilizando como fuente de verdad datos técnicos de archivos **IFC (Industry Foundation Classes)**.

La POC está diseñada para el **Applied Generative AI Workshop** (Twarco + facilitadores), con enfoque en una demo **robusta**, **repetible** y **alineada a Vertex AI**, y se estructura explícitamente con **CRISP-DM** (6 etapas iterativas).

**Idea central:** transformar datos IFC en un contexto textual/estructurado controlado y consultar ese contexto con prompts cuidadosamente diseñados para evitar alucinaciones (“no inventar datos”).

---

## 0.1 Mapeo de entregables del SOW con CRISP-DM

| Entregable del SOW | Etapa CRISP-DM | Cómo se cubre en este repo |
|---|---:|---|
| Technical Design Document | 5 (Evaluación) | Se documenta arquitectura y viabilidad; ver secciones 5 y docs asociados |
| Sample Prompts | 4 (Modelado) | Se define catálogo de prompts y versiones; ver sección 4 |
| POC Code | 4 (Modelado) | Notebook + scripts; ver `/notebooks` y sección 4 |
| GCP Pricing Calculator | 4 (Modelado) | Se plantea estimación de costo por consulta; ver 4.1.4 y 4.4 |
| Recomendaciones y Next Steps | 5 (Evaluación) | Roadmap y go/no-go; ver sección 5 |
| Workshop Demo (60–90 min) | Todas | Runbook propuesto; ver sección 5.4 |

---

## 0.2 Documentos asociados (este repo)

- **`/notebooks/01_ifc_exploracion.ipynb`**: exploración, extracción y resumen base del IFC.
- **`/docs/INGESTA_PREPROCESAMIENTO_DATOS.md`**: detalle de Etapa 2–3 (Data Understanding + Data Preparation).
- **`/docs/feedback_crisp-dm.md`**: retroalimentación base (referencia).

> Nota: este documento (`poc_crispdm.md`) es el **marco CRISP-DM completo**.  
> Los detalles extensos de datos/pipeline viven en `INGESTA_PREPROCESAMIENTO_DATOS.md` para no mezclar niveles.

---

# 1. Business Understanding (Comprensión del Negocio)

## 1.1 Contexto del proyecto (Workshop)

Esta POC forma parte de un **Applied Generative AI Workshop**, cuyo objetivo es demostrar en una sesión práctica (60–90 min) cómo **Vertex AI (Gemini)** puede responder preguntas en lenguaje natural sobre **datasets técnicos de proyectos inmobiliarios** (principalmente IFC).

## 1.2 Problema de negocio

En proyectos inmobiliarios, la información técnica suele estar en formatos complejos (p.ej., IFC) y es difícil de consumir por perfiles no técnicos (ventas, clientes, stakeholders). Esto genera:

- Dependencia de expertos técnicos para responder preguntas.
- Latencia en respuestas y procesos de preventa.
- Información poco reutilizable para experiencias conversacionales.

**Problema a resolver:**  
¿Cómo permitir que usuarios no técnicos puedan hacer preguntas en lenguaje natural sobre un proyecto inmobiliario y obtener respuestas claras, confiables y rápidas, usando datos técnicos existentes?

## 1.3 Objetivos del negocio (alineados con el SOW)

### Objetivo del workshop
Demostrar que Vertex AI puede:
1) recibir contexto (datos del proyecto) y  
2) responder preguntas relevantes para negocio/técnico  
3) con buena calidad y sin inventar información.

### Objetivo de esta POC
Validar viabilidad técnica y demostrar valor en una demo controlada:
- extracción IFC → representación consultable → Q&A con GenAI (prompts).

## 1.4 KPIs y criterios de éxito (Go/No-Go)

> Los KPIs son para una demo robusta (no producción). Se miden sobre un set de preguntas predefinido.

**KPIs técnicos**
- **Latencia promedio:** < 5s por consulta (objetivo ideal < 3s en condiciones estables).
- **Estabilidad demo:** 0 fallos críticos (crash, bloqueo total, pérdida de contexto).
- **Cobertura:** ≥ 90% de preguntas del set se responden con información disponible, o se responde “no disponible” de forma correcta.

**KPIs de calidad**
- **Exactitud/Corrección:** ≥ 80% respuestas correctas (según respuestas esperadas / rubric).
- **No-alucinación:** 0 respuestas que inventen atributos inexistentes (materiales, ubicación, metraje, pisos) sin evidencia.

**Criterio de éxito final**
- Demo fluida + resultados aceptables de exactitud + transparencia cuando faltan datos.

## 1.5 Stakeholders y usuarios objetivo

- **Twarco / negocio:** producto + equipo comercial (requiere respuestas rápidas, entendibles).
- **Usuarios finales:** interactúan con un asistente/avatar (no técnicos).
- **Equipo técnico:** define pipeline, controla calidad de datos, limita inferencias.
- **Facilitadores del workshop:** ejecutan demo, validan entregables.

## 1.6 Casos de uso priorizados (Top 3 para demo)

1) **Ventas / Comercial**
   - Resumen del proyecto, atributos observables, comunicación de limitaciones.
2) **Usuario final (Q&A simple)**
   - Preguntas sobre espacios/ambientes y componentes principales.
3) **Técnico**
   - Conteos, consistencia, límites de la información, explicación “de dónde sale”.

## 1.7 Alcance y fuera de alcance (Scope Control)

**Dentro del alcance (POC/Demo)**
- Procesar IFC(s) de ejemplo.
- Extraer entidades prioritarias: IfcSpace, IfcWall, IfcDoor, IfcWindow (mínimo viable).
- Generar contexto textual/estructurado para prompts.
- Definir y probar prompts con reglas anti-alucinación.
- Documentación CRISP-DM + set de preguntas demo + plan de evaluación.

**Fuera de alcance (por ahora)**
- Solución productiva end-to-end (UI final, backend completo).
- Fine-tuning / entrenamiento.
- Integración completa multi-fuente (Structured3D) en esta iteración base.
- Despliegue productivo y monitoreo (solo conceptual en Etapa 6).

## 1.8 Riesgos, supuestos y mitigaciones

**Supuestos**
- IFC(s) de muestra son suficientes para demostrar valor.
- Se obtendrán credenciales Vertex AI para integración real en Etapa 4 (cuando el proyecto lo habilite).

**Riesgos**
- **Datos incompletos o ambiguos** → el modelo podría inferir.
  - *Mitigación:* prompts con “no inventar”, validación/normalización, y respuestas “no disponible”.
- **Latencia o cuotas en demo**.
  - *Mitigación:* prompts pre-validados, dataset preprocesado, plan B (fallback).
- **Bloqueo por credenciales Vertex**.
  - *Mitigación:* avanzar con diseño, test set y evaluación local/estructurada; integrar cuando haya acceso.

## 1.9 Plan de alto nivel (alineado con ~3 semanas)

**Semana 1**
- Etapa 1 (negocio) + Etapa 2 (comprensión de datos) + checklist de calidad.

**Semana 2**
- Etapa 3 (pipeline y formatos) + inicio Etapa 4 (prompts + test set + diseño Vertex).

**Semana 3**
- Etapa 5 (evaluación + recomendaciones + costos) + runbook demo.

---

# 2. Data Understanding (Comprensión de los Datos)

> Esta etapa se documenta en detalle en: **`docs/INGESTA_PREPROCESAMIENTO_DATOS.md`** (Sección 2).  
Aquí dejamos el resumen ejecutivo para trazabilidad CRISP-DM.

## 2.1 Fuentes de datos

- **IFC (buildingSMART sample files):** fuente principal de datos técnicos.
- **Structured3D:** considerado como **extensión futura** (no requerido para el MVP de la demo, salvo que se priorice explícitamente).

## 2.2 Inventario de entidades IFC (MVP)

- IfcSpace (ambientes/espacios)
- IfcWall (muros)
- IfcDoor (puertas)
- IfcWindow (ventanas)

## 2.3 Observaciones del IFC procesado en el notebook

A partir del IFC de ejemplo procesado se observaron (conteos base de demo):

- Espacios: 21
- Muros: 57
- Puertas: 14
- Ventanas: 24

## 2.4 Calidad y limitaciones (resumen)

- Fortalezas: estructura consistente, tipos definidos, jerarquía.
- Limitaciones típicas: nombres repetidos, atributos faltantes, falta de metraje/uso/ubicación/materiales (si no están en IFC o no se extrajeron).

---

# 3. Data Preparation (Preparación de los Datos)

> Documentación completa en: **`docs/INGESTA_PREPROCESAMIENTO_DATOS.md`** (Secciones 3–6).  
Aquí queda el resumen CRISP-DM + decisiones para el workshop.

## 3.1 Ingesta (qué hacemos y por qué)

- Validar archivo(s) IFC: existencia, formato, tamaño, lectura con ifcopenshell.
- Registrar metadatos mínimos (nombre, hash/versión, fecha, conteos).
- Mantener un flujo reproducible: “misma entrada → misma salida”.

## 3.2 Selección (MVP de demo)

- Priorizar entidades clave (IfcSpace/Wall/Door/Window) para:
  - preguntas de conteo
  - resumen del proyecto
  - explicaciones comerciales simples
- Mantener extensible a otras entidades (IfcBuildingStorey, IfcSlab, IfcBeam) si el workshop lo pide.

## 3.3 Limpieza

- Manejo de nulos (name/longname).
- Normalización de textos (espacios, mayúsculas, caracteres).
- Detección básica de duplicados (p.ej. espacios con mismo nombre) sin borrar, solo reportar.

## 3.4 Transformación

- Generar:
  - **contexto textual** (resumen) para prompts.
  - **estructura JSON** si se requiere (para control y trazabilidad).
- Mantener el “no inventar”: solo describir lo extraído.

## 3.5 Normalización y estandarización (documentado)

- Unificación de nombres (mapeos simples: “Bath” → “Bathroom”, etc.) si aplica.
- Formatos consistentes para salida (listas, bullets, JSON).
- Unidades: si se extraen áreas/longitudes, normalizar a métrico (cuando exista dato).

## 3.6 Enriquecimiento (MVP y controlado)

- Derivados “seguros”:
  - densidad de componentes por espacio (si aplica)
  - top espacios por repetición de nombre (indicador de calidad)
- No inferir: no clasificar “residencial/comercial” si no hay evidencia.

## 3.7 Integración de datos (decisión de alcance)

El feedback menciona combinar IFC + Structured3D. Para esta iteración:

- **Decisión:** mantener Structured3D como **extensión futura**.
- **Justificación:** el objetivo inmediato es una demo de 60–90 min enfocada en IFC (fuente estándar BIM).
- **Condición para activar Structured3D:** si el workshop requiere explícitamente escenarios visuales/semánticos.

## 3.8 Optimización para GenAI

- Control de tamaño del contexto:
  - resumir y priorizar lo esencial
  - chunking si el IFC es grande (solo si se necesita)
- Versionado de formato de contexto (“schema v1” del resumen).

## 3.9 Pipeline completo (end-to-end)

Pipeline propuesto (MVP):
1) Ingesta IFC → 2) extracción entidades → 3) limpieza/normalización → 4) generación contexto → 5) ejecución de prompts (Etapa 4) → 6) evaluación (Etapa 5)

---

# 4. Modeling (Modelado)

**Nota de proyecto (bloqueo de credenciales):**  
La integración real con Vertex AI se ejecuta cuando se habiliten credenciales. Mientras tanto, se avanza completamente en:
- selección técnica (documentada),
- catálogo de prompts,
- set de pruebas y métricas,
- diseño de integración.

## 4.1 Selección de técnicas y plataforma (Vertex AI — requerido)

### 4.1.1 Modelos candidatos (Vertex AI)
- **Gemini (Pro / 1.5 / equivalente vigente en Vertex AI)**: modelo principal recomendado para texto.
- **Gemini multimodal (si aplica)**: solo si se incluyen entradas visuales (no MVP).
- **Vertex AI Search / RAG**: opción si se requiere búsqueda semántica sobre documentos largos.

### 4.1.2 Criterios de selección
- Integración nativa GCP (Vertex AI).
- Latencia y confiabilidad en demo.
- Costo por consulta (estimable).
- Capacidad de contexto (tokens).
- Controles de seguridad y gobernanza (empresa).

### 4.1.3 Decisión (propuesta)
- **Modelo base:** Gemini (texto) en Vertex AI para Q&A sobre contexto IFC.
- **Estrategia:** prompt + contexto estructurado (y RAG solo si crece el volumen).

### 4.1.4 Costos (entregable SOW)
Se estimará costo por:
- tokens de entrada (contexto + pregunta)
- tokens de salida (respuesta)
- volumen de consultas en demo y escenarios futuros

> Se documenta en el entregable “GCP Pricing Calculator” cuando se confirme modelo/región/cotas.

## 4.2 Diseño del esquema de testing (CRÍTICO)

### 4.2.1 Catálogo de preguntas (test set)
Se construirá un set mínimo con:
- **preguntas de conteo** (espacios, muros, puertas, ventanas)
- **preguntas descriptivas** (resumen del proyecto)
- **preguntas comerciales** (atributos observables + limitaciones)
- **preguntas “trampa”** (materiales/ubicación/metraje) para verificar “no inventar”

Cada pregunta tendrá:
- respuesta esperada (o regla esperada: “no disponible”)
- criterio de scoring (correcto/parcial/incorrecto)

### 4.2.2 Métricas
- Exactitud (% correctas)
- No-alucinación (% respuestas que inventan = objetivo 0)
- Relevancia (1–5)
- Completitud (1–5)
- Latencia (segundos)

## 4.3 Construcción del “modelo” (prompting)

### 4.3.1 Estrategias de prompt
- **Zero-shot con reglas estrictas** (MVP).
- **Few-shot** (2–3 ejemplos) para consistencia de estilo.
- Plantillas por tipo:
  - Técnico
  - Comercial
  - Ejecutivo

### 4.3.2 Parámetros (cuando se ejecute en Vertex)
- temperature: baja (0.1–0.3) para respuestas deterministas
- max_output_tokens: controlado para no divagar
- top_p / top_k: según recomendaciones internas y pruebas

### 4.3.3 Control anti-alucinación (regla obligatoria)
El prompt debe obligar:
- “Si el dato no está, decir no disponible”
- “No inferir, no estimar”
- “Citar qué parte del contexto respalda la respuesta (cuando aplique)”

## 4.4 Evaluación del modelo (durante iteración)
- Comparar versiones de prompts.
- Analizar fallas:
  - inventa datos
  - se contradice
  - responde incompleto
- Seleccionar el set final de prompts “demo-safe”.

---

# 5. Evaluation (Evaluación)

## 5.1 Evaluación contra objetivos del negocio (Etapa 1)
Se validará:
- KPIs (latencia, exactitud, cobertura, estabilidad)
- Valor para casos de uso (ventas/usuario/técnico)

## 5.2 Revisión del proceso (lecciones aprendidas)
- Qué funcionó (extracción, formato, prompts)
- Qué no funcionó (datos insuficientes, ambigüedad)
- Qué requiere expansión (más entidades, RAG, Structured3D)

## 5.3 Recomendaciones y Next Steps (roadmap)
- Corto plazo: integración Vertex AI + prompts pre-validados + test set.
- Mediano: ampliar extracción (niveles, áreas) si están disponibles; añadir RAG si el contexto crece.
- Largo: evaluar Structured3D si el producto requiere señal visual/semántica.

## 5.4 Runbook para la demo (60–90 min)

**Parte A (10–15 min):** contexto y objetivo  
- Qué es IFC, qué extraemos, qué problema resuelve

**Parte B (20–30 min):** pipeline  
- ingesta → extracción → contexto → prompt

**Parte C (20–30 min):** Q&A en vivo  
- set de preguntas pre-validadas (incluye 2–3 “trampa”)

**Parte D (10–15 min):** evaluación y costos  
- KPIs logrados + costo por consulta (estimado)

**Plan B (backup)**
- dataset procesado pre-cargado
- prompts “golden”
- respuestas de referencia para contingencias

---

# 6. Deployment (Despliegue) — (futuro / fuera del alcance actual)

Aunque despliegue productivo no es objetivo del POC, se documenta conceptualmente:

## 6.1 Arquitectura objetivo (conceptual)
- Ingesta a Cloud Storage
- Preprocesamiento (Cloud Run / Functions / Vertex Pipelines)
- Serving GenAI (Vertex AI)
- Observabilidad (logging, métricas, tracing)

## 6.2 Monitoreo y mantenimiento (conceptual)
- Métricas: latencia, costo, tasa de “no disponible”, drift de datos
- Versionado: prompts, schema de contexto, datasets
- Feedback loop con usuarios

---

## 7. Checklist de cumplimiento (feedback CRISP-DM)

- [x] Etapa 1: objetivos, KPIs, stakeholders, casos de uso, riesgos, alcance
- [x] Etapa 2: fuentes, entidades, calidad (detalle en `INGESTA_PREPROCESAMIENTO_DATOS.md`)
- [x] Etapa 3: ingesta→preprocesamiento→optimización (detalle en `INGESTA...`)
- [ ] Etapa 4: prompts + test set + diseño Vertex (parcial; integración cuando haya credenciales)
- [ ] Etapa 5: evaluación formal + costos + recomendaciones (cuando estén prompts/test set definitivos)
- [ ] Etapa 6: despliegue conceptual (incluido)

---

## 8. Referencias (dentro de este archivo, URLs en contexto de documentación)

- CRISP-DM 1.0 (guía paso a paso)
- Google Cloud Vertex AI (documentación oficial)
- Gemini en Vertex AI (model reference)
- GCP Pricing Calculator
- buildingSMART IFC (estándar) y sample files
- Structured3D dataset (extensión futura)
