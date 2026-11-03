# Modelo sistémico de SIGIA

## 1. Propósito del modelo

Este documento representa a SIGIA desde los conceptos de la Teoría General de Sistemas (TGS). Su finalidad es identificar los elementos que forman parte de la propuesta, las relaciones entre ellos y los intercambios con el entorno.

SIGIA (Sistema Inteligente de Gestión de Incidencias de Alumbrado Público) es una propuesta académica orientada a organizar la información inicial de incidencias de alumbrado público y facilitar su revisión y seguimiento.

El modelo describe el funcionamiento propuesto para un prototipo independiente. No representa ni afirma describir los procedimientos internos reales de EMVIAL.

## 2. SIGIA como sistema

SIGIA se considera un sistema abierto porque recibe información de actores externos, la procesa y genera respuestas e información que vuelven a relacionarse con esos actores.

Su objetivo es transformar reportes de vecinos en registros estructurados que puedan ser comprendidos, revisados y seguidos por las personas responsables.

La inteligencia artificial funciona como un componente de apoyo dentro del sistema. No reemplaza al personal humano ni toma decisiones administrativas u operativas.

## 3. Objetivo general

Organizar y facilitar el tratamiento inicial y el seguimiento de reportes relacionados con el alumbrado público, mediante la validación de datos, la sugerencia de categorías, la detección de posibles inconsistencias y la generación de información útil para la revisión humana.

## 4. Entradas del sistema

Las entradas son los datos y eventos que SIGIA recibe para iniciar o continuar el tratamiento de una incidencia.

### 4.1. Información inicial del vecino

- Tipo de servicio: alumbrado público.
- Dirección o ubicación precisa de la incidencia.
- Barrio.
- Descripción del problema observado.

### 4.2. Información complementaria

- Aclaraciones aportadas por el vecino.
- Fotografías u otros elementos de evidencia, cuando estén disponibles.
- Información del vecino sobre un posible corte de suministro eléctrico: sí, no o no sabe.

La información sobre un posible corte eléctrico se registra como una observación aportada por el vecino. No constituye una confirmación ni un diagnóstico sobre el origen del problema.

### 4.3. Datos de seguimiento

- Código único de la incidencia.
- Consultas de estado.
- Respuestas del vecino ante pedidos de información.
- Actualizaciones realizadas por los roles de revisión u operación en la simulación.
- Observaciones y evidencias asociadas a los cambios de estado.

En el prototipo, todos los registros y eventos se generan con datos ficticios.

## 5. Procesos o transformaciones

Los procesos representan las actividades mediante las cuales SIGIA transforma las entradas en información organizada y resultados de seguimiento.

### 5.1. Recepción y registro

El sistema recibe los datos iniciales y crea un registro de incidencia con un código único que permite identificarlo y consultarlo posteriormente.

### 5.2. Validación de información

SIGIA comprueba que estén presentes los datos requeridos y busca inconsistencias entre ellos.

Si faltan datos importantes, solicita aclaraciones concretas al vecino. No completa información por su cuenta ni inventa direcciones, ubicaciones o características del problema.

Cuando el vecino aporta información nueva, el sistema vuelve a revisar el conjunto de datos para comprobar que el registro quede coherente.

### 5.3. Interpretación y clasificación preliminar

El componente de inteligencia artificial interpreta la descripción en lenguaje natural y propone una categoría inicial.

La categoría es una sugerencia, no una decisión definitiva. Si la descripción continúa siendo ambigua o la confianza resulta insuficiente, el sistema deja constancia de la incertidumbre y deriva el caso a revisión humana.

### 5.4. Detección de posibles duplicados

SIGIA puede comparar incidencias utilizando datos como la dirección y el tipo de problema para advertir que dos reportes podrían referirse al mismo lugar o elemento.

La coincidencia genera una advertencia para revisión. El sistema no elimina, rechaza ni combina reportes automáticamente, porque una segunda comunicación puede aportar información adicional.

### 5.5. Preparación de información para revisión

El sistema organiza los datos recibidos, identifica información faltante o contradictoria y prepara un resumen de la incidencia.

El personal de revisión analiza ese resultado y determina cómo continuar dentro del flujo propuesto.

### 5.6. Seguimiento

SIGIA registra los cambios de estado, las fechas, los responsables que intervienen en la simulación, las observaciones y las evidencias incorporadas.

El vecino puede consultar el estado mediante el código de incidencia. Las notificaciones se orientan a cada rol según la información que necesita conocer.

### 5.7. Registro de resultado y retroalimentación

Cuando se informa que una intervención fue realizada, el sistema registra esa comunicación y puede solicitar al vecino que indique si el problema fue solucionado.

La respuesta se incorpora como retroalimentación. Si el vecino informa que el problema continúa o se resolvió parcialmente, el caso vuelve a revisión. La falta de respuesta no se interpreta como confirmación de que el problema fue solucionado.

## 6. Salidas del sistema

Las salidas son los resultados que SIGIA produce a partir de sus procesos.

- Registro de incidencia con código único.
- Solicitudes de información adicional cuando faltan datos.
- Categoría preliminar sugerida.
- Advertencias por posibles inconsistencias o duplicados.
- Resumen estructurado para revisión humana.
- Estado actual e historial de cambios.
- Notificaciones según el rol y la situación del caso.
- Registro de observaciones y evidencias.
- Resultado de la consulta de satisfacción o confirmación del vecino, cuando exista respuesta.
- Información para evaluar el funcionamiento del prototipo mediante casos de prueba.

Estas salidas facilitan la organización y el seguimiento, pero no equivalen a una orden de trabajo, una aprobación administrativa ni una certificación técnica de reparación.

## 7. Controles del sistema

Los controles establecen límites y reglas para que el sistema funcione de manera coherente y segura.

### 7.1. Controles de datos

- Verificar la presencia de los campos obligatorios.
- Comprobar la coherencia básica de los datos.
- Solicitar aclaraciones ante información insuficiente.
- No inventar ni completar datos desconocidos.
- Mantener identificadores únicos para las incidencias.

### 7.2. Controles de inteligencia artificial

- La clasificación siempre se presenta como preliminar.
- La incertidumbre debe quedar visible.
- Los casos ambiguos se envían a revisión humana.
- La IA no aprueba ni rechaza incidencias.
- La IA no asigna personal, materiales ni recursos.
- La IA no determina con certeza el origen técnico de una falla ni atribuye responsabilidades a EDEA.

### 7.3. Controles de intervención humana

- El personal de revisión analiza las sugerencias y advertencias.
- Las decisiones administrativas propuestas quedan a cargo de personas.
- Los roles tienen permisos diferenciados.
- El área operativa puede informar avances, obstáculos y resultados, pero no realizar aprobaciones administrativas que no correspondan a su función.

Estos roles son una propuesta funcional para el prototipo y no una afirmación sobre la estructura interna real de EMVIAL.

### 7.4. Controles de trazabilidad

Cada cambio relevante debe conservar, como mínimo:

- Código de incidencia.
- Fecha y hora.
- Actor o rol que realizó la acción.
- Estado anterior y nuevo estado, cuando corresponda.
- Descripción u observación.
- Referencia a la evidencia incorporada, si existe.

Las fotografías son elementos complementarios y no constituyen por sí solas una prueba concluyente de que una reparación se realizó correctamente.

### 7.5. Controles de notificaciones y tiempos

Los avisos deben enviarse según el rol y el evento que los justifica, evitando notificaciones innecesarias.

Los plazos de recordatorio o seguimiento serán configurables en el prototipo. Cualquier plazo utilizado en las pruebas será un parámetro de simulación y no se presentará como un tiempo oficial de EMVIAL.

## 8. Retroalimentación

La retroalimentación es la información que vuelve al sistema después de una salida o de una acción y permite actualizar el registro o revisar el funcionamiento.

En SIGIA se identifican dos formas principales:

1. **Retroalimentación sobre una incidencia:** el vecino aporta aclaraciones, informa si el problema continúa o indica si la solución fue satisfactoria. El personal de revisión y el área operativa simulada también pueden incorporar observaciones y actualizaciones.
2. **Retroalimentación sobre el funcionamiento del prototipo:** los resultados de las pruebas permiten detectar errores de validación, clasificación, seguimiento o notificación y ajustar el diseño.

La retroalimentación no implica que el sistema pueda verificar por sí mismo el estado físico de una luminaria. SIGIA registra y organiza la información que recibe.

## 9. Subsistemas propuestos

Para facilitar el análisis, SIGIA puede dividirse en los siguientes subsistemas funcionales:

| Subsistema | Responsabilidad principal |
| --- | --- |
| Recepción y registro | Recibir la información y generar el código de incidencia. |
| Validación de datos | Comprobar campos requeridos, coherencia y datos faltantes. |
| Interpretación y clasificación | Analizar la descripción y sugerir una categoría preliminar. |
| Detección de coincidencias | Advertir posibles reportes duplicados para revisión humana. |
| Gestión y seguimiento | Mantener estados, historial y consultas de las incidencias. |
| Notificaciones | Preparar avisos pertinentes para cada rol. |
| Evidencias y auditoría | Registrar observaciones, evidencias y trazabilidad de acciones. |
| Revisión humana | Permitir que las personas evalúen la información y decidan cómo continuar. |

Los subsistemas se relacionan entre sí. Por ejemplo, la recepción entrega los datos a validación; la información validada puede pasar a interpretación y clasificación; y los resultados se presentan para revisión y seguimiento.

## 10. Sistema, suprasistema y entorno

### 10.1. Sistema

El sistema analizado en este trabajo es SIGIA, entendido como la propuesta de software y sus componentes funcionales.

### 10.2. Suprasistema

En el contexto institucional del proyecto, la Municipalidad del Partido de General Pueyrredon constituye el marco organizacional más amplio. EMVIAL es el organismo municipal relacionado con la competencia de alumbrado público considerada en este trabajo.

SIGIA no se presenta como un sistema oficial de la Municipalidad ni como una herramienta actualmente utilizada por EMVIAL.

### 10.3. Entorno

El entorno comprende los elementos externos que pueden influir en las incidencias o aportar información al sistema, por ejemplo:

- Vecinos y características del espacio urbano.
- Red e infraestructura de suministro eléctrico.
- Condiciones climáticas y ambientales.
- Normativa y procedimientos públicos aplicables.
- Canales municipales existentes para comunicar incidencias.

EDEA se considera parte del contexto externo relacionado con el suministro eléctrico. En el prototipo no existe conexión con EDEA ni posibilidad de consultar sus sistemas. SIGIA solamente puede registrar información vecinal sobre un posible corte y dejar su evaluación para la revisión humana.

## 11. Frontera del sistema

La frontera define qué actividades forman parte de SIGIA y cuáles quedan fuera de la propuesta.

**Dentro de la frontera:**

- Recepción y organización de reportes ficticios.
- Validación de datos.
- Clasificación preliminar asistida por IA.
- Detección de posibles duplicados.
- Preparación de resúmenes y advertencias.
- Seguimiento de estados.
- Registro de observaciones, evidencias y retroalimentación.
- Simulación de revisión humana y actualizaciones operativas.

**Fuera de la frontera:**

- Recepción real de reclamos municipales.
- Conexión con sistemas internos de la Municipalidad o EMVIAL.
- Integración con plataformas de EDEA.
- Diagnóstico técnico automático de instalaciones o redes eléctricas.
- Asignación real de cuadrillas, materiales o recursos.
- Emisión de órdenes de trabajo reales.
- Aprobaciones administrativas reales.
- Confirmación autónoma de que una reparación se realizó correctamente.

## 12. Esquema general del funcionamiento

El flujo general propuesto puede resumirse de la siguiente manera:

1. El vecino ingresa un reporte.
2. SIGIA registra la incidencia y genera un código.
3. El sistema valida los datos.
4. Si falta información, solicita una aclaración y vuelve a validar al recibirla.
5. Si los datos son suficientes, la IA propone una categoría y prepara un resumen.
6. El sistema señala posibles duplicados o incertidumbres.
7. El personal de revisión analiza la información y decide cómo continuar.
8. En la simulación, el área operativa registra avances, obstáculos y evidencias.
9. SIGIA actualiza el estado y comunica las novedades pertinentes.
10. Se registra la respuesta del vecino, si la hubiera, y se utiliza como retroalimentación.

Este esquema describe el funcionamiento deseado del prototipo y no debe interpretarse como una descripción del procedimiento interno vigente de EMVIAL.

## 13. Criterios para evaluar el modelo

El modelo podrá evaluarse mediante casos de prueba con información ficticia, observando si:

- Los reportes generan un código único.
- Los campos obligatorios se validan correctamente.
- El sistema solicita aclaraciones cuando faltan datos.
- La clasificación se presenta como sugerencia y no como decisión definitiva.
- Los casos ambiguos quedan identificados para revisión humana.
- Los posibles duplicados generan advertencias sin eliminar reportes.
- Los cambios de estado quedan registrados con trazabilidad.
- Las notificaciones respetan los roles.
- La respuesta del vecino se registra sin asumir una confirmación cuando no existe.
- Los límites de la IA y del prototipo se mantienen durante todo el flujo.

## 14. Síntesis

Desde la TGS, SIGIA se plantea como un sistema abierto compuesto por subsistemas relacionados, que recibe información del entorno, la transforma mediante procesos de validación y organización, y genera salidas para facilitar la revisión y el seguimiento de incidencias.

El control se expresa en las reglas de validación, los permisos, la trazabilidad y los límites impuestos a la inteligencia artificial. La retroalimentación permite actualizar los casos y evaluar el propio prototipo.

La intervención humana permanece como condición central: SIGIA ayuda a organizar información, pero no sustituye las decisiones administrativas, técnicas ni operativas de las personas.
