# Ingesta y Preprocesamiento de Datos  
## POC GenAI para Proyectos Inmobiliarios

---

## 2. Data Understanding (Comprensión de los Datos)

### 2.1 Fuentes de Datos Utilizadas

Para esta Prueba de Concepto (POC) se utilizan exclusivamente **datasets de ejemplo y datos sintéticos**, con fines demostrativos y sin información sensible.

Las principales fuentes de datos son:

#### 2.1.1 Archivos IFC (Industry Foundation Classes)

Los archivos IFC son un estándar abierto desarrollado por **buildingSMART** para representar información de proyectos de construcción e inmobiliarios.

Estos archivos contienen información estructurada sobre:
- Espacios
- Elementos constructivos
- Relaciones entre componentes del proyecto

En esta POC, los archivos IFC funcionan como la **fuente principal de datos técnicos**.

**Características clave de los IFC utilizados:**
- Datos estructurados y jerárquicos
- Información técnica rica pero compleja
- Diseñados para interoperabilidad entre herramientas BIM

---

#### 2.1.2 Datasets Sintéticos (Extensión futura)

Como posible extensión del POC, se considera el uso de datasets sintéticos como **Structured3D**, que contienen representaciones semánticas de espacios interiores.

Estos datasets permitirían explorar:
- Escenarios más avanzados
- Combinación de datos estructurados y visuales
- Casos de uso más complejos para GenAI

En la fase actual del POC, el foco principal está en archivos IFC.

---

### 2.2 Tipos de Datos Procesables

Desde el punto de vista de ciencia de datos y GenAI, los datos utilizados pueden clasificarse de la siguiente forma:

#### 2.2.1 Datos Estructurados
- Conteos de elementos (número de espacios, muros, puertas, ventanas)
- Tipos de entidades IFC (IfcSpace, IfcWall, IfcDoor, IfcWindow)
- Relaciones explícitas entre elementos

#### 2.2.2 Datos Semi-estructurados
- Atributos textuales de elementos IFC (nombres, descripciones)
- Jerarquías del modelo (espacios contenidos en niveles, edificios)
- Metadatos del proyecto

#### 2.2.3 Datos No Estructurados
- Texto generado a partir de los datos técnicos
- Resúmenes descriptivos del proyecto
- Contexto textual utilizado como entrada para modelos de GenAI

---

### 2.3 Elementos IFC Relevantes para la POC

Para esta POC, se consideran prioritarios los siguientes tipos de entidades IFC:

| Entidad IFC | Descripción | Uso en la POC |
|------------|-------------|---------------|
| IfcSpace | Representa espacios o ambientes | Conteo, resumen del proyecto |
| IfcWall | Muros del proyecto | Análisis de complejidad |
| IfcDoor | Puertas | Circulación y conectividad |
| IfcWindow | Ventanas | Iluminación y ventilación |

Otros elementos IFC existen, pero quedan fuera del alcance inicial de esta POC.

---

### 2.4 Descripción Inicial de los Datos

A partir del archivo IFC de ejemplo procesado en el notebook, se observa:

- Número total de espacios: 21
- Número total de muros: 57
- Número total de puertas: 14
- Número total de ventanas: 24

Estos valores se utilizan como base para generar resúmenes textuales y responder preguntas en lenguaje natural.

---

### 2.5 Calidad de los Datos

La calidad de los datos IFC presenta las siguientes características:

**Fortalezas:**
- Estructura consistente
- Tipos de entidades bien definidos
- Relaciones claras entre elementos

**Limitaciones:**
- Ausencia de información sobre:
  - Uso del edificio
  - Materiales
  - Dimensiones exactas
  - Ubicación geográfica
- Nombres de espacios pueden ser genéricos o repetidos
- No todos los atributos están siempre presentes

Estas limitaciones deben ser explícitamente consideradas al diseñar prompts para GenAI.

---

### 2.6 Implicaciones para Generative AI

Dado el tipo y la calidad de los datos:

- GenAI puede responder **preguntas descriptivas y de conteo**
- GenAI **no debe inferir información no presente**
- Las respuestas deben incluir aclaraciones cuando los datos sean incompletos

Esto refuerza la necesidad de:
- Prompts bien diseñados
- Contexto claro
- Instrucciones explícitas para no inventar información

---

### 2.7 Conclusión de Data Understanding

Esta etapa confirma que los datos disponibles son **adecuados para una POC demostrativa**, permitiendo validar el uso de GenAI para comprensión básica de proyectos inmobiliarios.

Sin embargo, también evidencia que una solución productiva requeriría:
- Mayor riqueza de datos
- Normalización más avanzada
- Integración con fuentes adicionales

Esta conclusión alimenta directamente la siguiente etapa de CRISP-DM: **Data Preparation**.

---

## 3. Data Preparation (Preparación de los Datos – CRISP-DM)

Esta etapa describe el proceso mediante el cual los datos técnicos de proyectos inmobiliarios
(archivos IFC) son preparados para ser utilizados como entrada en modelos de
Inteligencia Artificial Generativa (GenAI).

A diferencia de la etapa anterior, aquí no se analiza *qué son* los datos,
sino *cómo se transforman* para que puedan ser consumidos de forma confiable,
reproducible y controlada por modelos de lenguaje.

---

### 3.1 Ingesta de Datos

La ingesta de datos corresponde al proceso mediante el cual los archivos IFC
son incorporados al flujo del POC, asegurando que los datos de entrada
cumplan con condiciones mínimas de validez, integridad y trazabilidad.

El objetivo principal de esta etapa es garantizar que únicamente archivos IFC
válidos y procesables ingresen al pipeline de preparación de datos,
reduciendo errores posteriores y asegurando consistencia en el análisis.

#### 3.1.1 Fuentes de Datos

En la fase actual del POC, la ingesta se realiza a partir de:

- Archivos IFC de ejemplo provenientes de repositorios públicos (buildingSMART)
- Archivos almacenados localmente dentro del repositorio del proyecto

No se realiza ingesta desde fuentes productivas ni sistemas externos.

#### 3.1.2 Validaciones Iniciales

Antes de procesar un archivo IFC, se aplican las siguientes validaciones básicas:

- Existencia del archivo
- Extensión válida (.ifc)
- Capacidad de apertura mediante librerías IFC (ifcopenshell)
- Estructura general consistente (sin errores críticos de parsing)

Los archivos que no cumplen estas condiciones son descartados del flujo.

#### 3.1.3 Resultado de la Ingesta

El resultado de esta etapa es un archivo IFC validado y listo para ser
procesado en las etapas posteriores de limpieza, transformación y
estructuración para su uso en modelos de Generative AI.

---

### 3.2 Selección de Datos

Los archivos IFC contienen una gran cantidad de entidades, atributos y
relaciones que describen múltiples aspectos de un proyecto inmobiliario.
Sin embargo, no toda esta información es necesaria ni adecuada para una
Prueba de Concepto de Generative AI enfocada en comprensión básica del proyecto.

El objetivo de esta etapa es **definir de manera explícita qué datos se
seleccionan y cuáles se excluyen**, asegurando foco, simplicidad y
alineación con los objetivos del POC.

#### 3.2.1 Criterios de Selección

Para esta POC, los datos se seleccionan con base en los siguientes criterios:

- Relevancia para responder preguntas en lenguaje natural
- Claridad semántica para usuarios no técnicos
- Presencia consistente en archivos IFC de ejemplo
- Bajo riesgo de interpretación ambigua
- Utilidad demostrativa para el workshop

Elementos que no cumplen estos criterios se excluyen del alcance inicial.

#### 3.2.2 Entidades IFC Seleccionadas

Las siguientes entidades IFC son consideradas prioritarias para el POC:

- **IfcSpace**  
  Utilizada para identificar espacios o ambientes dentro del proyecto.
  Es clave para conteos, descripciones generales y resúmenes del proyecto.

- **IfcWall**  
  Representa muros del proyecto y permite inferir nivel de compartimentación
  y complejidad básica de la distribución interna.

- **IfcDoor**  
  Permite analizar conectividad y circulación entre espacios.

- **IfcWindow**  
  Asociada a iluminación natural y ventilación, aspectos relevantes desde
  una perspectiva funcional y comercial.

Estas entidades permiten cubrir una amplia variedad de preguntas sin
introducir complejidad innecesaria.

#### 3.2.3 Atributos Prioritarios

Para cada entidad seleccionada, se consideran únicamente atributos básicos,
como:

- Identificadores
- Nombres o etiquetas
- Relaciones jerárquicas (pertenencia a espacios o niveles)

Atributos geométricos complejos, materiales y propiedades avanzadas
quedan fuera del alcance de esta POC.

#### 3.2.4 Datos Excluidos del Alcance

Se excluyen explícitamente del POC:

- Elementos estructurales avanzados (ej. vigas, columnas)
- Sistemas MEP (eléctrico, sanitario, HVAC)
- Información de costos o presupuestos
- Datos temporales (cronogramas de obra)
- Información normativa o legal

Estos datos podrían incorporarse en fases futuras, pero no son necesarios
para cumplir los objetivos actuales del workshop.

#### 3.2.5 Impacto en Generative AI

La selección controlada de datos permite:

- Reducir ruido en el contexto entregado al modelo GenAI
- Mejorar la precisión de las respuestas
- Evitar inferencias incorrectas
- Mantener tiempos de respuesta adecuados para una demo en vivo

Esta decisión es clave para garantizar una experiencia estable y confiable
durante el workshop.

---

### 3.3 Limpieza de Datos

Los archivos IFC, incluso cuando cumplen el estándar, pueden presentar
inconsistencias, valores faltantes o información redundante. Antes de
utilizar estos datos como entrada para modelos de Generative AI, es
necesario aplicar un proceso de limpieza controlado.

El objetivo de esta etapa es **reducir ambigüedades, eliminar ruido y
asegurar coherencia**, sin alterar el significado original de los datos.

#### 3.3.1 Problemas Comunes en Archivos IFC

Durante el análisis de archivos IFC de ejemplo, se identifican los
siguientes problemas frecuentes:

- Atributos opcionales ausentes (valores nulos)
- Nombres genéricos o repetidos en espacios (ej. "Room", "Space")
- Entidades sin relaciones claras con otros elementos
- Información duplicada o redundante
- Atributos técnicos presentes pero no relevantes para el POC

Estos problemas son comunes en datasets BIM reales y deben ser tratados
explícitamente.

#### 3.3.2 Estrategias de Limpieza Aplicadas

Para esta POC, se aplican las siguientes estrategias de limpieza:

- **Manejo de valores nulos**  
  Los atributos faltantes no se completan artificialmente. En su lugar,
  se documenta su ausencia y se evita inferir información no disponible.

- **Normalización de nombres**  
  Cuando los nombres de espacios son genéricos o inconsistentes, se
  utilizan identificadores únicos o etiquetas neutrales para evitar
  ambigüedad.

- **Eliminación de duplicados lógicos**  
  Entidades repetidas o referencias redundantes se consolidan cuando es
  posible, manteniendo una sola representación coherente.

- **Filtrado de atributos irrelevantes**  
  Atributos técnicos que no aportan valor a las preguntas del POC se
  excluyen del contexto entregado al modelo GenAI.

#### 3.3.3 Validación de Relaciones

Se verifica que las entidades seleccionadas mantengan relaciones válidas,
por ejemplo:

- Espacios asociados correctamente a niveles o edificios
- Puertas y ventanas vinculadas a muros o espacios
- Ausencia de entidades huérfanas sin contexto

Las entidades que no cumplen estas validaciones pueden ser excluidas o
marcadas como incompletas.

#### 3.3.4 Impacto en la Calidad del Contexto GenAI

La limpieza de datos permite:

- Reducir el riesgo de respuestas incorrectas
- Mejorar la coherencia de los resúmenes generados
- Aumentar la confiabilidad de las respuestas en lenguaje natural
- Mantener transparencia sobre las limitaciones de la información

Este enfoque prioriza la **honestidad del modelo** frente a la
completitud artificial de los datos.

---

### 3.4 Transformación de Datos

Una vez que los datos IFC han sido seleccionados y limpiados, se procede a
su transformación en formatos adecuados para su consumo por modelos de
Inteligencia Artificial Generativa (GenAI).

El objetivo de esta etapa es **traducir información técnica compleja en
representaciones estructuradas y textuales que preserven el significado
original del proyecto**, pero que sean comprensibles para modelos de
lenguaje y usuarios no técnicos.

#### 3.4.1 Representación Estructurada

Los datos extraídos del archivo IFC se transforman inicialmente en
estructuras de datos intermedias, como diccionarios o formatos tipo JSON.

Estas representaciones incluyen, entre otros:

- Conteo total de entidades relevantes (espacios, muros, puertas, ventanas)
- Listas de entidades por tipo
- Relaciones básicas entre elementos
- Identificadores y etiquetas normalizadas

Este formato estructurado permite:
- Inspección clara de los datos
- Reutilización en diferentes etapas del pipeline
- Trazabilidad entre el IFC original y el contexto GenAI

#### 3.4.2 Generación de Resúmenes Textuales

A partir de la representación estructurada, se genera un **resumen textual
del proyecto**, que describe de forma clara y concisa:

- El número de espacios y su distribución general
- La cantidad de elementos constructivos relevantes
- Características observables del proyecto basadas en los datos disponibles

Este resumen textual actúa como **contexto principal** que se proporciona
al modelo GenAI para responder preguntas en lenguaje natural.

#### 3.4.3 Principios de Transformación

Durante la transformación se siguen los siguientes principios:

- **Fidelidad a los datos**: No se agrega información que no esté presente
- **Claridad semántica**: Se utilizan descripciones simples y comprensibles
- **Consistencia**: El formato del resumen se mantiene estable entre ejecuciones
- **Tamaño controlado**: El texto generado se limita para evitar contextos excesivos

Estos principios son fundamentales para garantizar respuestas confiables
durante la demo del workshop.

#### 3.4.4 Relación con el Notebook

La lógica de transformación descrita en esta sección se implementa en los
notebooks del proyecto, donde se realiza:

- Extracción de entidades IFC
- Construcción de estructuras intermedias
- Generación del resumen textual utilizado en los prompts

Esta documentación permite comprender el proceso sin depender
exclusivamente del código.

---

### 3.5 Normalización y Estandarización

Para asegurar consistencia en el contexto entregado a los modelos de
Generative AI, se aplica un proceso de normalización y estandarización
sobre los datos transformados.

El objetivo de esta etapa es **reducir variabilidad innecesaria** y
facilitar la interpretación uniforme de la información por parte del
modelo y de los usuarios.

#### 3.5.1 Normalización de Nombres y Etiquetas

- Los nombres de entidades se estandarizan a un formato consistente
- Se evita el uso de etiquetas ambiguas o dependientes del modelador
- En caso de nombres genéricos, se prioriza el uso de identificadores únicos

Esto permite que las respuestas generadas mantengan coherencia entre
ejecuciones.

#### 3.5.2 Estandarización de Formatos

Se define un formato estable para:

- Conteos numéricos
- Listados de entidades
- Resúmenes textuales del proyecto

La estandarización garantiza que el contexto proporcionado al modelo
mantenga una estructura predecible, reduciendo interpretaciones erróneas.

#### 3.5.3 Beneficios para GenAI

Este proceso contribuye a:

- Respuestas más claras y consistentes
- Menor variación semántica innecesaria
- Mejor control del comportamiento del modelo
- Mayor confiabilidad durante demostraciones en vivo

---

### 3.6 Enriquecimiento de Datos

El enriquecimiento de datos consiste en generar información adicional
derivada a partir de los datos ya existentes, con el objetivo de
mejorar la capacidad descriptiva del contexto utilizado por GenAI.

En esta POC, el enriquecimiento se realiza de forma **limitada y
controlada**, evitando inferencias complejas o supuestos no sustentados
por los datos originales.

#### 3.6.1 Métricas Derivadas Básicas

A partir de los conteos extraídos del archivo IFC, se calculan métricas
simples que aportan valor contextual, tales como:

- Número total de espacios del proyecto
- Número total de elementos constructivos relevantes
- Relación básica entre espacios y elementos (ej. densidad de muros por espacio)

Estas métricas permiten enriquecer las respuestas sin introducir
complejidad innecesaria.

#### 3.6.2 Clasificación Descriptiva del Proyecto

Con base en las métricas derivadas, el proyecto puede ser descrito de
forma cualitativa, por ejemplo:

- Proyecto con múltiples espacios diferenciados
- Distribución interna con nivel de compartimentación medio
- Presencia significativa de elementos de iluminación natural

Estas clasificaciones son **descriptivas**, no normativas ni técnicas,
y siempre se basan exclusivamente en datos disponibles.

#### 3.6.3 Limitaciones del Enriquecimiento

Quedan explícitamente fuera del alcance de esta etapa:

- Inferencias sobre uso específico del edificio
- Cálculos de áreas, volúmenes o costos
- Clasificaciones funcionales avanzadas
- Comparaciones entre múltiples proyectos

Estas capacidades se consideran para fases posteriores del proyecto.

#### 3.6.4 Beneficio para Generative AI

El enriquecimiento controlado permite que GenAI:

- Genere respuestas más contextuales
- Ofrezca resúmenes más informativos
- Mantenga coherencia sin inventar información
- Mejore la experiencia durante la demo del workshop

### 3.7 Integración de Datos

En la fase actual de la POC, se trabaja con una única fuente de datos
principal (archivos IFC), lo que permite mantener el alcance acotado
y garantizar estabilidad en la demostración.

Como extensión futura, se contempla la integración de datasets
sintéticos como Structured3D, los cuales permitirían:

- Combinar información estructurada (IFC) con datos semánticos
- Explorar casos de uso más avanzados
- Evaluar escenarios de mayor complejidad

La integración con Structured3D no se implementa en esta fase,
pero se considera explícitamente en el diseño para asegurar
escalabilidad del enfoque.

### 3.8 Optimización de Datos para Generative AI

Para garantizar un uso eficiente de modelos de Generative AI, los datos
preprocesados deben adaptarse a las limitaciones y características de los
modelos de lenguaje.

Las principales estrategias consideradas en esta POC son:

- Definición de un formato estándar de entrada para GenAI
- Priorización de información relevante del proyecto
- Control del tamaño del contexto enviado al modelo
- Preparación de resúmenes estructurados y texto enriquecido

En esta fase del POC, se utiliza un resumen compacto del proyecto como
entrada al modelo, evitando sobrecargar el contexto y asegurando
respuestas claras y consistentes.

Para escenarios más complejos o proyectos de mayor tamaño, se
considerarían técnicas adicionales como fragmentación (chunking),
indexación semántica y recuperación selectiva de contexto.

### 3.9 Pipeline Completo de Preparación de Datos

El pipeline de preparación de datos definido para esta POC sigue un flujo
secuencial y controlado, compuesto por las siguientes etapas:

1. Ingesta de archivos IFC
2. Validación básica del formato y estructura
3. Selección de entidades relevantes
4. Limpieza y normalización de atributos
5. Transformación a formato estructurado/textual
6. Optimización del contexto para GenAI

Este pipeline permite reproducibilidad, trazabilidad y control del
proceso, asegurando que los datos utilizados por el modelo GenAI sean
consistentes y adecuados para una demostración en tiempo real.

En una fase productiva, este pipeline podría automatizarse y escalarse
utilizando servicios de Google Cloud como Cloud Storage, Dataflow o
Vertex AI Pipelines.
    



