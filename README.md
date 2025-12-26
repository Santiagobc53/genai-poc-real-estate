# Generative AI POC – Comprensión de Datos de Proyectos Inmobiliarios

## Descripción general

Este proyecto presenta una Prueba de Concepto (POC) enfocada en evaluar el uso de Inteligencia Artificial Generativa (GenAI) para la comprensión y análisis de datos técnicos de proyectos inmobiliarios.

La POC explora cómo los modelos de GenAI pueden interpretar información estructurada y semi-estructurada —como archivos IFC y datasets sintéticos de proyectos inmobiliarios— y responder preguntas en lenguaje natural sobre las características de un proyecto.

Los datos utilizados corresponden a archivos de muestra y conjuntos de datos sintéticos, diseñados para pruebas y experimentación. Estos datos no representan información productiva final, lo cual es consistente con el objetivo de la POC: validar la viabilidad técnica del enfoque y demostrar el valor potencial del uso de GenAI, sin desarrollar una solución lista para producción.

Este trabajo forma parte de la fase de preparación para un Applied Generative AI Workshop.

## Objetivo y alcance del POC

### Objetivo

El objetivo principal de esta Prueba de Concepto (POC) es evaluar la viabilidad técnica de utilizar Inteligencia Artificial Generativa (GenAI) para interpretar datos técnicos de proyectos inmobiliarios y permitir la consulta de dicha información mediante preguntas en lenguaje natural.

La POC busca demostrar que, a partir de datasets estructurados o semi-estructurados, es posible extraer información relevante y presentarla de forma comprensible para distintos perfiles de usuario.

### Alcance

Dentro del alcance de esta POC se incluyen las siguientes actividades:

- Análisis de datasets de proyectos inmobiliarios (por ejemplo, archivos IFC y datasets sintéticos).
- Transformación de información técnica a un formato textual o estructurado comprensible.
- Diseño de prompts para la interacción con modelos de Generative AI.
- Demostración de respuestas a preguntas relacionadas con las características de un proyecto inmobiliario.

Fuera del alcance de esta POC se encuentran:

- Desarrollo de una solución lista para producción.
- Implementación de interfaces de usuario finales.
- Optimización avanzada, escalabilidad o despliegue en entornos productivos.
- Entrenamiento o ajuste fino de modelos de IA.

## Dataset y material de trabajo

Para el desarrollo de esta Prueba de Concepto (POC) se utilizarán datasets de muestra y datos sintéticos relacionados con proyectos inmobiliarios. Estos datasets permiten trabajar con información técnica realista sin depender de datos productivos.

### Archivos IFC (buildingSMART)

Se utilizarán archivos IFC (Industry Foundation Classes) provenientes de repositorios de ejemplo de buildingSMART. Estos archivos contienen información estructurada sobre elementos de un proyecto inmobiliario, como espacios, componentes y relaciones entre elementos.

Los archivos IFC empleados corresponden a datos de prueba diseñados para interoperabilidad y validación de conceptos, lo cual resulta adecuado para el alcance de esta POC.

Referencia:
- buildingSMART Community Sample Test Files

### Structured3D

Como material complementario, se considera el uso del dataset Structured3D, un conjunto de datos sintético y fotorealista que contiene diseños de espacios interiores con anotaciones estructurales y semánticas.

Este dataset se plantea como una posible extensión del POC para explorar escenarios más avanzados de análisis y comprensión de información espacial y estructurada.

Referencia:
- Structured3D dataset

### Consideraciones sobre los datos

Los datasets utilizados en esta POC tienen un propósito exclusivamente exploratorio y demostrativo. No se utilizan datos reales de clientes ni información sensible, y no se busca representar un entorno productivo final.

## Arquitectura propuesta (alto nivel)

La arquitectura propuesta para esta Prueba de Concepto (POC) se plantea de forma simple y modular, con el objetivo de facilitar la comprensión del flujo de datos y la interacción con modelos de Inteligencia Artificial Generativa.

A alto nivel, el flujo del POC se compone de las siguientes etapas:

1. **Adquisición de datos**  
   Carga de datasets de proyectos inmobiliarios, tales como archivos IFC y datos sintéticos estructurados.

2. **Procesamiento de datos**  
   Extracción de información relevante desde los datasets y transformación de los datos técnicos a un formato estructurado o textual comprensible (por ejemplo, JSON o texto descriptivo).

3. **Diseño de prompts**  
   Definición de prompts que permitan guiar al modelo de Generative AI para interpretar la información del proyecto y responder preguntas en lenguaje natural.

4. **Interacción con Generative AI**  
   El modelo de GenAI recibe una pregunta del usuario y genera una respuesta basada en la información procesada del proyecto inmobiliario.

5. **Salida de resultados**  
   Presentación de respuestas en lenguaje natural, enfocadas en describir características, componentes y atributos del proyecto inmobiliario.

## Ejemplos de preguntas

A continuación se presentan ejemplos de preguntas que pueden realizarse al sistema durante la demostración de la POC:

- ¿Qué tipo de proyecto inmobiliario representa este dataset?
- ¿Cuántos espacios o ambientes contiene el proyecto?
- ¿Cuáles son los principales componentes del edificio?
- ¿Se puede generar un resumen general del proyecto?
- ¿Qué información técnica relevante se puede extraer a partir de los datos disponibles?

Estas preguntas ilustran cómo la información técnica puede ser consultada mediante lenguaje natural, facilitando la comprensión del proyecto.

## Resultados esperados y próximos pasos

### Resultados esperados

Se espera que esta Prueba de Concepto (POC) permita demostrar que:

- Los datos técnicos de proyectos inmobiliarios pueden ser procesados y transformados en información comprensible.
- Los modelos de Inteligencia Artificial Generativa pueden responder preguntas en lenguaje natural a partir de datasets estructurados y semi-estructurados.
- El enfoque propuesto tiene valor potencial para casos de uso como análisis de proyectos, soporte a ventas y comprensión de información técnica.

Estos resultados buscan validar la viabilidad del enfoque y servir como base para futuras iteraciones.

### Próximos pasos

Como pasos posteriores a esta propuesta inicial, se consideran las siguientes actividades:

- Implementar un prototipo funcional mínimo (por ejemplo, mediante un notebook o script).
- Ajustar y mejorar los prompts utilizados para la interacción con el modelo de GenAI.
- Evaluar la integración con servicios de Generative AI en Google Cloud (por ejemplo, Vertex AI).
- Analizar la ampliación del POC a otros datasets o escenarios de uso más avanzados.

Estos pasos se plantean como una evolución progresiva del POC, sin comprometer aún una implementación productiva.



