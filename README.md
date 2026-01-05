# Generative AI POC – Proyectos Inmobiliarios (CRISP-DM)

## Descripción general

Este repositorio contiene una **Prueba de Concepto (POC)** orientada a evaluar el uso de **Inteligencia Artificial Generativa (GenAI)** para la comprensión y análisis de datos técnicos de proyectos inmobiliarios, utilizando archivos **IFC (Industry Foundation Classes)** como fuente principal de información.

La POC forma parte del **Applied Generative AI Workshop para Twarco**, cuyo objetivo es demostrar, en una sesión práctica de **60–90 minutos**, cómo **Google Cloud Vertex AI (Gemini)** puede responder preguntas en lenguaje natural sobre datasets técnicos de proyectos inmobiliarios.

El proyecto está estructurado siguiendo la metodología **CRISP-DM (Cross-Industry Standard Process for Data Mining)**, una metodología estándar y ampliamente utilizada en proyectos reales de ciencia de datos y machine learning.

---

## Objetivo del POC

El objetivo principal de esta POC es:

- Validar la **viabilidad técnica** de utilizar GenAI para interpretar datos técnicos complejos (IFC).
- Transformar información **estructurada y semi-estructurada** en respuestas comprensibles para usuarios no técnicos.
- Demostrar **valor práctico** para casos de uso como ventas, soporte comercial y comprensión general de proyectos inmobiliarios.

Esta POC **no busca construir una solución productiva**, sino servir como base técnica y demostrativa para el workshop.

---

## Alcance y limitaciones

### Dentro del alcance

- Análisis y exploración de archivos IFC de ejemplo.
- Ingesta, preparación y transformación de datos técnicos para consumo por modelos GenAI.
- Documentación detallada de las etapas:
  - Business Understanding
  - Data Understanding
  - Data Preparation  
  siguiendo la metodología CRISP-DM.
- Validación técnica inicial mediante notebooks.

### Fuera del alcance (en esta fase)

- Integración directa con Vertex AI (pendiente de aprobación).
- Despliegue productivo o escalabilidad.
- Interfaces de usuario finales.
- Entrenamiento o ajuste fino de modelos de IA.

---

## Estructura del repositorio

```text
.
├── notebooks/
│   └── 01_ifc_exploracion.ipynb     # Exploración técnica y validación inicial
├── docs/
│   ├── poc_crispdm.md               # Propuesta del POC estructurada por CRISP-DM
│   ├── INGESTA_PREPROCESAMIENTO_DATOS.md
│   │                               # Ingesta y preparación de datos (Etapas 2 y 3)
│   └── feedback_crisp-dm.md         # Feedback recibido para la propuesta
├── data/
│   └── sample.ifc                   # Archivo IFC de ejemplo
├── requirements.txt
└── README.md
Metodología
La POC sigue explícitamente la metodología CRISP-DM, cubriendo en esta fase:

Etapa 1 – Business Understanding

Etapa 2 – Data Understanding

Etapa 3 – Data Preparation

Las etapas posteriores (Modeling con Vertex AI, Evaluation y Deployment) están planificadas, pero no se ejecutan en esta fase hasta contar con aprobación formal de la propuesta.

Datasets utilizados
Archivos IFC (buildingSMART)
Archivos de ejemplo públicos utilizados para pruebas y demostración de interoperabilidad BIM.

Structured3D (extensión futura)
Dataset sintético considerado únicamente como posible extensión del proyecto.
No se utiliza en la fase actual del POC.

No se emplean datos reales ni información sensible.

Estado actual del proyecto
✔ Propuesta documentada y estructurada según CRISP-DM

✔ Ingesta y preparación de datos completamente documentadas

✔ Notebook funcional para exploración y validación técnica

⏳ Integración con Vertex AI pendiente de aprobación

Próximos pasos (una vez aprobada la propuesta)
Etapa 4: Modelado con Vertex AI (Gemini)

Diseño y validación de prompts optimizados

Definición de métricas de evaluación

Estimación de costos con GCP Pricing Calculator

Preparación de demo para el workshop

Nota final

Este repositorio representa una POC realista, acotada y alineada con prácticas profesionales, diseñada para ser evaluada, iterada y extendida una vez aprobada la fase de propuesta.


