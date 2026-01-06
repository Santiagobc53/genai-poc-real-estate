# Generative AI POC – Proyectos Inmobiliarios (CRISP-DM)

Este repositorio contiene una **Prueba de Concepto (POC)** orientada a evaluar el uso de **Inteligencia Artificial Generativa (GenAI)** para la comprensión y análisis de datos técnicos de proyectos inmobiliarios, utilizando archivos **IFC (Industry Foundation Classes)** como fuente principal.

La POC forma parte de un **Applied Generative AI Workshop (60–90 min)**, cuyo objetivo es demostrar cómo un modelo de GenAI (p. ej., **Vertex AI / Gemini**) puede responder preguntas en lenguaje natural sobre **datasets técnicos** (IFC), manteniendo un alcance controlado y evitando inferencias no sustentadas.

---

## Objetivo del POC

- Validar la **viabilidad técnica** de transformar datos IFC en **contexto estructurado y texto comprensible** para consultas en lenguaje natural.
- Generar un flujo reproducible de **ingesta, exploración, limpieza mínima y métricas derivadas** (sin análisis geométrico/estructural).
- Demostrar **valor práctico** para audiencias ejecutivas, comerciales y técnicas **sin inventar datos**.

> Esta POC **no busca construir una solución productiva**, sino servir como base técnica y demostrativa para el workshop.

---

## Alcance y limitaciones (resumen)

### Dentro del alcance
- Exploración de un **IFC de ejemplo**.
- Conteo e inventario de entidades (p. ej., `IfcSpace`, `IfcWall`, `IfcDoor`, `IfcWindow`).
- Limpieza mínima y **métricas derivadas simples** (relaciones/promedios).
- Generación de **contexto estructurado (JSON)** + **resumen textual** para consultas con GenAI.
- Trazabilidad básica (validación del archivo, tamaño, hash).

### Fuera del alcance (en esta fase)
- Integración productiva con **Vertex AI** (pendiente de aprobación).
- Análisis geométrico, estructural, energético, normativo o de costos.
- Enriquecimiento con fuentes externas (catálogos, GIS, precios, normativas, etc.).
- UI, base de datos, despliegue o escalabilidad.
- Fine-tuning / entrenamiento de modelos.

---

## Metodología (CRISP-DM)

La POC sigue explícitamente **CRISP-DM**:

- **Etapa 1 – Business Understanding:** documentada en `docs/` (propuesta / CRISP-DM).
- **Etapas 2 y 3 – Data Understanding & Data Preparation:** implementadas y demostradas en el notebook (ingesta, inventario, limpieza y métricas controladas).
- **Etapa 4 – Modeling (Vertex AI):** planificada como siguiente paso (no ejecutada en esta fase).

---

## Estructura del repositorio

```text
.
├── notebooks/
│   └── 01_ifc_exploracion.ipynb        # Exploración técnica + contexto para GenAI (Etapas 2–3)
├── docs/
│   ├── poc_crispdm.md                  # Propuesta del POC estructurada por CRISP-DM
│   ├── INGESTA_PREPROCESAMIENTO_DATOS.md  # Detalle de ingesta y preparación (Etapas 2–3)
│   └── feedback_crisp-dm.md            # Feedback recibido para la propuesta
├── data/
│   └── sample.ifc                      # IFC de ejemplo
├── requirements.txt
└── README.md
Requisitos
Python 3.10+ (recomendado 3.10/3.11)

Entorno virtual (venv)

Jupyter (o VS Code con extensión Jupyter)

Dependencias en requirements.txt (incluye ifcopenshell)

Quickstart (ejecución local)
1) Crear y activar venv
Windows (PowerShell):

bash
Copiar código
python -m venv venv
.\venv\Scripts\Activate.ps1
Windows (CMD):

bash
Copiar código
python -m venv venv
venv\Scripts\activate
Linux / macOS:

bash
Copiar código
python -m venv venv
source venv/bin/activate
2) Instalar dependencias
bash
Copiar código
pip install -r requirements.txt
3) Ejecutar el notebook
Abre notebooks/01_ifc_exploracion.ipynb en VS Code (Jupyter) y ejecuta en orden, o:

bash
Copiar código
jupyter notebook
Qué produce el notebook
A partir del IFC de ejemplo, el flujo genera:

Conteos base (espacios, muros, puertas, ventanas).

Limpieza mínima de nombres de espacios y validación de consistencia.

Métricas derivadas simples (p. ej., muros por espacio, ventanas por espacio).

Contexto estructurado (JSON) y resumen textual para ser usados como entrada a un modelo de GenAI.

Sección de preguntas de demostración alineadas con el alcance y con control explícito de inferencias.

Datasets utilizados
IFC (buildingSMART / ejemplos públicos): archivos de demostración para interoperabilidad BIM.

Structured3D (extensión futura): considerado como posible ampliación, no usado en esta fase.

No se emplean datos reales ni información sensible.

Estado del proyecto
✅ Propuesta documentada y estructurada según CRISP-DM (docs/)

✅ Ingesta y preparación de datos documentadas

✅ Notebook funcional y reproducible para exploración y validación técnica

⏳ Integración con Vertex AI (Gemini) pendiente de aprobación

Próximos pasos (cuando se apruebe Etapa 4)
Integración conceptual con Vertex AI (Gemini) usando el contexto generado.

Estandarización/versionado del esquema de contexto (JSON + texto).

Variantes de prompt por perfil (ejecutivo / comercial / técnico).

Definición de métricas de evaluación y guion de demo.

Nota final
Este repositorio representa una POC realista, acotada y alineada con buenas prácticas, diseñada para ser evaluada, iterada y extendida una vez aprobada la fase de arquitectura/modelado.

