# Funcionamiento del agente de IA de SIGIA

## 1. Propósito

Este documento define el comportamiento esperado del componente de inteligencia artificial integrado en SIGIA.

El agente tiene como objetivo asistir en el tratamiento inicial de reportes de alumbrado público: comprender la descripción del vecino, detectar información faltante o contradictoria, solicitar aclaraciones, sugerir una categoría preliminar y preparar un resumen para la revisión humana.

El agente no reemplaza al personal municipal ni toma decisiones administrativas u operativas. El diseño corresponde a un prototipo académico independiente que se probará exclusivamente con datos ficticios.

## 2. Ubicación del agente dentro de SIGIA

La inteligencia artificial es un componente interno del sistema. No es un actor externo ni se comunica directamente con la Municipalidad, EMVIAL o EDEA.

SIGIA administra el registro, los estados, los permisos, el historial y las comunicaciones con los actores. El agente recibe la información necesaria para analizarla y devuelve resultados estructurados que SIGIA puede presentar o utilizar en el flujo de trabajo.

La decisión de aceptar una incidencia para continuar su tratamiento, derivarla o cerrarla corresponde al personal humano definido en el modelo.

## 3. Objetivos específicos

El agente debe poder:

1. Interpretar descripciones escritas en lenguaje natural.
2. Identificar los datos obligatorios que faltan.
3. Detectar contradicciones o expresiones ambiguas.
4. Formular preguntas concretas para obtener la información necesaria.
5. Proponer una categoría preliminar del problema.
6. Señalar posibles reportes duplicados cuando SIGIA le proporcione registros comparables.
7. Preparar un resumen claro y ordenado para el personal de revisión.
8. Expresar sus dudas y limitaciones sin presentar suposiciones como hechos.

## 4. Información que recibe

El agente puede recibir los siguientes datos, según la etapa del proceso:

### 4.1. Datos del reporte

- Tipo de servicio, que en el prototipo debe corresponder a alumbrado público.
- Dirección o ubicación indicada por el vecino.
- Altura o referencia de ubicación, cuando sea necesaria.
- Barrio.
- Descripción del problema.
- Descripción complementaria.
- Fotografía u otra evidencia, si el prototipo contempla su análisis.

### 4.2. Información complementaria

- Respuestas del vecino a preguntas anteriores.
- Datos ya registrados en la incidencia.
- Registros de otras incidencias que SIGIA permita comparar para advertir posibles duplicados.

El agente solo puede analizar la información que SIGIA le proporciona. No debe suponer que tiene acceso a mapas, catastros, bases municipales, sistemas de EDEA ni servicios externos de validación.

## 5. Datos necesarios para considerar completo un reporte

Para el flujo inicial del prototipo se consideran necesarios:

- Tipo de servicio: alumbrado público.
- Dirección o ubicación suficientemente precisa.
- Barrio.
- Descripción del problema.

La fotografía es complementaria y no debe ser obligatoria.

El agente debe diferenciar entre:

- **Dato ausente:** el vecino no lo proporcionó.
- **Dato ambiguo:** la información no permite identificar claramente el lugar o problema.
- **Dato contradictorio:** dos datos aportados parecen incompatibles.
- **Dato no verificado:** el vecino lo informó, pero SIGIA no dispone de una fuente confiable para comprobarlo.

Por ejemplo, el agente puede detectar que falta la altura de una dirección o que la ubicación es demasiado general. Sin una fuente externa confiable, no puede afirmar que una dirección existe o que pertenece realmente al barrio indicado.

## 6. Flujo de funcionamiento

### Etapa 1. Recepción

SIGIA recibe el reporte del vecino y entrega sus datos al agente para el análisis inicial.

### Etapa 2. Comprensión

El agente interpreta la descripción y reconoce el tipo de problema que el vecino intenta comunicar.

Debe conservar el sentido de lo informado sin agregar causas, ubicaciones ni detalles que no hayan sido aportados.

### Etapa 3. Validación de información

El agente revisa si están presentes los datos requeridos y si son suficientemente claros para continuar.

Si detecta datos faltantes, ambiguos o contradictorios, devuelve a SIGIA una lista de observaciones y preguntas concretas.

### Etapa 4. Solicitud de aclaraciones

SIGIA presenta las preguntas al vecino. El vecino puede completar la información y el sistema vuelve a enviar el reporte actualizado al agente.

El agente debe evaluar nuevamente el conjunto completo de datos, no solamente la última respuesta.

Debe evitar repetir preguntas que ya fueron respondidas de forma suficiente.

### Etapa 5. Clasificación preliminar

Cuando la información disponible permite interpretar el problema, el agente propone una categoría preliminar.

La propuesta debe incluir una explicación breve y un indicador cualitativo de confianza, por ejemplo: alta, media o baja. Este indicador orienta la revisión, pero no constituye una medición de certeza ni una decisión automática.

Si la descripción continúa siendo ambigua, el agente debe señalar que no puede clasificarla con suficiente confianza y recomendar revisión humana.

### Etapa 6. Detección de posibles duplicados

Si SIGIA proporciona incidencias existentes, el agente puede señalar coincidencias posibles considerando la ubicación y el tipo de problema.

La advertencia no significa que dos reportes sean necesariamente iguales. El personal de revisión debe comprobarlo.

El agente nunca debe eliminar, rechazar ni fusionar incidencias por su cuenta. Un nuevo reporte puede aportar información adicional sobre un problema ya informado.

### Etapa 7. Preparación del resumen

El agente prepara un resumen con:

- Descripción organizada del problema.
- Ubicación informada.
- Datos faltantes o dudosos.
- Categoría preliminar sugerida, si corresponde.
- Posibles duplicados, si se detectaron.
- Motivos por los que recomienda revisión humana, si aplica.

### Etapa 8. Entrega a SIGIA

El agente devuelve el resultado a SIGIA. El sistema lo registra y lo presenta al personal de revisión cuando corresponda.

El agente no contacta por su cuenta al área operativa ni deriva directamente una incidencia.

## 7. Resultados que puede generar

El agente debe devolver resultados que permitan distinguir claramente entre información y sugerencias.

| Resultado | Significado |
| --- | --- |
| Información incompleta | Faltan datos necesarios para continuar. |
| Requiere aclaración | Hay datos ambiguos o contradictorios. |
| Información organizada | Los datos requeridos están presentes y pueden presentarse para revisión. |
| Clasificación sugerida | El agente propone una categoría preliminar. |
| Posible duplicado | Existen coincidencias que debe revisar una persona. |
| Revisión humana necesaria | El agente no puede interpretar el caso con suficiente confianza o detecta una situación que requiere evaluación. |

Estos resultados son estados de análisis del agente y no reemplazan los estados administrativos de la incidencia definidos por SIGIA.

## 8. Límites y acciones prohibidas

El agente no debe:

- Inventar direcciones, alturas, barrios ni características del problema.
- Afirmar que una dirección es real sin una fuente de verificación disponible.
- Diagnosticar con certeza una falla eléctrica o determinar su causa técnica.
- Afirmar que un problema es responsabilidad de EDEA o de un área municipal.
- Consultar o modificar sistemas internos municipales o de EDEA.
- Aprobar o rechazar administrativamente una incidencia.
- Asignar cuadrillas, personal, materiales o recursos.
- Emitir órdenes de trabajo.
- Eliminar o fusionar reportes automáticamente.
- Confirmar que una reparación fue realizada o que el problema quedó solucionado.
- Cerrar administrativamente una incidencia.
- Ocultar la incertidumbre o presentar una sugerencia como una decisión confirmada.

## 9. Tratamiento de casos especiales

### 9.1. Dirección incompleta

Si el vecino informa una calle sin altura ni referencia suficiente, el agente debe pedir una ubicación más precisa. No debe inventar una altura ni elegir una dirección por aproximación.

### 9.2. Barrio no informado

El agente debe solicitar el barrio si es un campo requerido en el prototipo. No debe deducirlo como dato confirmado a partir de una dirección si no dispone de una fuente confiable.

### 9.3. Descripción ambigua

Si el vecino indica, por ejemplo, que hay un problema con una luminaria sin explicar qué sucede, el agente debe formular una pregunta concreta para precisar el problema.

Si luego de las aclaraciones continúa la ambigüedad, debe recomendar revisión humana.

### 9.4. Posible corte de suministro eléctrico

Si el vecino informa que podría existir un corte de suministro, el agente registra ese dato como una observación aportada por el vecino.

No debe confirmar el corte ni atribuirle automáticamente la causa de la incidencia. El caso queda disponible para evaluación humana.

### 9.5. Posible duplicado

Si existen reportes con ubicación y problema similares, el agente genera una advertencia. El personal de revisión determina si se trata de la misma incidencia o de reportes diferentes.

### 9.6. Fotografía poco clara o ausente

La ausencia de una fotografía no invalida por sí sola el reporte. Si se adjunta una imagen y no permite comprender el problema, el agente puede indicarlo y solicitar una descripción adicional o revisión humana.

## 10. Relación con los estados de SIGIA

El agente puede aportar información para que SIGIA gestione el flujo, pero no modifica por sí mismo los estados administrativos.

Como orientación:

- Si faltan datos, SIGIA puede mantener la incidencia como incompleta y solicitar información.
- Si los datos están organizados, SIGIA puede dejarla lista para revisión.
- Si existe incertidumbre importante, SIGIA puede marcar que requiere revisión humana.
- Las decisiones de revisión, derivación y cierre son registradas por el personal autorizado.

La correspondencia exacta entre los resultados del agente y los estados de la incidencia se implementará mediante reglas de SIGIA, no mediante decisiones autónomas del modelo de IA.

## 11. Ejemplo de funcionamiento

**Reporte inicial ficticio del vecino:**

"Hay una luminaria apagada en la calle San Martín".

**Análisis esperado:**

- Tipo de problema probable: luminaria apagada.
- Dirección: incompleta, porque no se indicó altura ni referencia suficiente.
- Barrio: no informado.
- Estado del análisis: requiere aclaración.

**Preguntas que podría presentar SIGIA:**

1. ¿A qué altura de la calle San Martín se encuentra la luminaria?
2. ¿En qué barrio está ubicada?
3. Si es posible, ¿podés indicar una esquina o referencia cercana?

Cuando el vecino responda, SIGIA actualizará el registro y solicitará un nuevo análisis del conjunto de datos.

Si la información queda suficientemente clara, el agente podrá preparar una clasificación preliminar y un resumen para el personal de revisión. La ubicación seguirá siendo un dato informado por el vecino, salvo que exista una fuente confiable para verificarla.

## 12. Evaluación del agente en el prototipo

El funcionamiento podrá evaluarse con casos ficticios que incluyan:

- Reportes completos.
- Reportes sin dirección.
- Reportes sin barrio.
- Descripciones ambiguas.
- Datos contradictorios.
- Posibles duplicados.
- Menciones de cortes eléctricos.
- Reportes sin fotografías.
- Respuestas del vecino que completan información faltante.

Se observará si el agente solicita los datos adecuados, evita inventar información, distingue sugerencias de hechos y deriva a revisión humana los casos que no puede interpretar con suficiente claridad.

## 13. Síntesis

El agente de IA de SIGIA funciona como asistente para el análisis inicial de las incidencias. Comprende las descripciones, identifica faltantes, solicita aclaraciones, sugiere categorías y organiza la información para facilitar la revisión humana.

Su función es mejorar la calidad y organización de los datos recibidos, no reemplazar a las personas ni tomar decisiones administrativas u operativas. La responsabilidad sobre la revisión, derivación y cierre administrativo permanece en los roles humanos definidos por el proyecto.
