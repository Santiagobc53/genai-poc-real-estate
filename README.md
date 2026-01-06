# Generative AI POC – Proyectos Inmobiliarios (CRISP-DM)

Este repositorio contiene una **Prueba de Concepto (POC)** orientada a evaluar el uso de **Inteligencia Artificial Generativa (GenAI)** para la comprensión y análisis de datos técnicos de proyectos inmobiliarios, utilizando archivos **IFC (Industry Foundation Classes)** como fuente principal.

La POC forma parte de un **Applied Generative AI Workshop (60–90 minutos)**, cuyo objetivo es demostrar cómo un modelo de GenAI (por ejemplo, **Gemini en Vertex AI**) puede responder preguntas en lenguaje natural sobre datasets técnicos (IFC), manteniendo un **alcance controlado**, **trazabilidad de datos** y evitando **inferencias no sustentadas**.

Este repositorio está diseñado para ser revisado por perfiles técnicos, de negocio y de arquitectura, y sirve como base para validación conceptual y técnica antes de una posible fase de implementación.

---

## Objetivo del POC

El objetivo principal de esta POC es:

- Validar la viabilidad técnica de transformar datos IFC en **contexto estructurado** y **texto comprensible** para consultas en lenguaje natural.
- Diseñar un flujo reproducible de **ingesta**, **exploración**, **limpieza mínima** y **métricas derivadas**, sin análisis geométrico, estructural o normativo.
- Demostrar valor práctico para audiencias **ejecutivas**, **comerciales** y **técnicas**, sin inventar datos ni sobreinterpretar la información disponible.
- Mantener un enfoque realista, acotado y alineado con buenas prácticas de ingeniería y data.

Esta POC no busca construir una solución productiva, sino servir como **base técnica y demostrativa** para el workshop y para discusión de arquitectura.

---

## Alcance y limitaciones

### Dentro del alcance

- Exploración de un archivo IFC de ejemplo.
- Conteo e inventario de entidades (por ejemplo: IfcSpace, IfcWall, IfcDoor, IfcWindow).
- Limpieza mínima de datos y normalización básica de atributos.
- Cálculo de métricas derivadas simples (por ejemplo, relaciones entre espacios y elementos).
- Generación de contexto estructurado (JSON) y resumen textual para consumo por GenAI.
- Trazabilidad básica del archivo (validación, tamaño, hash).

### Fuera del alcance (en esta fase)

- Integración productiva con Vertex AI (pendiente de aprobación).
- Análisis geométrico, estructural, energético, normativo o de costos.
- Enriquecimiento con fuentes externas (catálogos, precios, GIS, normativas, etc.).
- Interfaz de usuario, backend, base de datos, despliegue o escalabilidad.
- Fine-tuning o entrenamiento de modelos de IA.

---

## Metodología (CRISP-DM)

La POC sigue explícitamente la metodología **CRISP-DM**, adaptada al contexto de GenAI:

- **Etapa 1 – Business Understanding**  
  Documentada en `docs/poc_crispdm.md`. Define el problema, los objetivos de negocio, los stakeholders y los criterios de éxito.

- **Etapas 2 y 3 – Data Understanding & Data Preparation**  
  Implementadas y demostradas en el notebook `notebooks/01_ifc_exploracion.ipynb` y documentadas en `docs/INGESTA_PREPROCESAMIENTO_DATOS.md`.  
  Incluyen ingesta, inventario de entidades, limpieza mínima y métricas controladas.

- **Etapa 4 – Modeling (Vertex AI / GenAI)**  
  Planificada como siguiente paso. No ejecutada en esta fase.  
  Se contempla el uso de modelos fundacionales (Gemini) con contexto estructurado generado desde IFC.

- **Etapas 5 y 6 – Evaluation & Deployment**  
  Consideradas a nivel conceptual para futuras fases.

---


## Estructura del repositorio

<pre>
.
├── notebooks/
│   └── 01_ifc_exploracion.ipynb               # Exploración técnica + contexto para GenAI (Etapas 2–3)
├── docs/
│   ├── poc_crispdm.md                         # Propuesta del POC estructurada por CRISP-DM
│   ├── INGESTA_PREPROCESAMIENTO_DATOS.md      # Detalle de ingesta y preparación (Etapas 2–3)
│   └── feedback_crisp-dm.md                   # Feedback recibido para la propuesta
├── data/
│   └── sample.ifc                             # IFC de ejemplo
├── requirements.txt
└── README.md
</pre>

## Requisitos

- Python 3.10+ (recomendado 3.10 / 3.11)
- Entorno virtual (venv)
- Jupyter Notebook o VS Code con extensión Jupyter
- Dependencias listadas en `requirements.txt` (incluye ifcopenshell)

---

## Quickstart (ejecución local)

### 1. Crear y activar entorno virtual

**Windows (PowerShell):**
python -m venv venv
.\venv\Scripts\Activate.ps1

markdown
Copiar código

**Windows (CMD):**
python -m venv venv
venv\Scripts\activate

markdown
Copiar código

**Linux / macOS:**
python -m venv venv
source venv/bin/activate

shell
Copiar código

### 2. Instalar dependencias
pip install -r requirements.txt

css
Copiar código

### 3. Ejecutar el notebook

Abrir `notebooks/01_ifc_exploracion.ipynb` en VS Code (Jupyter) y ejecutarlo en orden, o bien:
jupyter notebook

yaml
Copiar código

---

## ¿Qué produce el notebook?

A partir del IFC de ejemplo, el flujo genera:

- Conteos base de entidades (espacios, muros, puertas, ventanas).
- Limpieza mínima de nombres y validación de consistencia.
- Métricas derivadas simples (por ejemplo, muros por espacio, ventanas por espacio).
- Contexto estructurado en formato JSON.
- Resumen textual listo para ser usado como entrada a un modelo de GenAI.
- Preguntas de demostración alineadas con el alcance y con control explícito de inferencias.

---

## Datasets utilizados

- IFC (buildingSMART / ejemplos públicos): archivos de demostración para interoperabilidad BIM.
- Structured3D (extensión futura): considerado como posible ampliación, no usado en esta fase.

No se emplean datos reales ni información sensible.

---

## Estado del proyecto

- Propuesta documentada y estructurada según CRISP-DM.
- Ingesta y preparación de datos implementadas y documentadas.
- Notebook funcional y reproducible para exploración y validación técnica.
- Integración con Vertex AI (Gemini) pendiente de aprobación.

---

## Próximos pasos (cuando se apruebe Etapa 4)

- Integración conceptual con Vertex AI (Gemini) usando el contexto generado.
- Estandarización y versionado del esquema de contexto (JSON + texto).
- Definición de variantes de prompt por perfil (ejecutivo / comercial / técnico).
- Definición de métricas de evaluación y guion de demo para el workshop.

---

## Nota final

Este repositorio representa una **POC realista, acotada y alineada con buenas prácticas**, diseñada para ser evaluada, iterada y extendida una vez aprobada la fase de arquitectura y modelado.

No es una solución productiva, sino un artefacto técnico y conceptual para validación y discusión.
