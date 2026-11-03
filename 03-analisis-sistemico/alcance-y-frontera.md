# Alcance y frontera del sistema

**Proyecto:** SIGIA — Sistema Inteligente de Gestión de Incidencias de Alumbrado Público  
**Organización de referencia:** Municipalidad del Partido de General Pueyrredon, con foco de estudio en EMVIAL.  
**Tipo de trabajo:** propuesta académica y prototipo de simulación.

## 1. Propósito del sistema

SIGIA se propone como un sistema independiente de apoyo a la recepción, comprensión, clasificación, validación, organización y seguimiento de incidencias relacionadas exclusivamente con el alumbrado público.

Su finalidad es mejorar la calidad de la información con la que se inicia cada reclamo, facilitar su revisión por parte del personal responsable y ofrecer trazabilidad sobre los cambios de estado y las novedades del caso.

SIGIA no reemplaza los canales municipales existentes, al personal de la organización ni los sistemas institucionales. Tampoco se afirma que reproduzca el procedimiento interno real de EMVIAL: los roles y circuitos descritos en este documento son una **propuesta de diseño académico**.

## 2. Alcance de la primera versión

La primera versión del proyecto será un prototipo independiente, sin conexión con sistemas informáticos internos de la Municipalidad, EMVIAL o EDEA.

### Funcionalidades incluidas

- Registrar incidencias de alumbrado público mediante información aportada por el vecino.
- Solicitar los datos obligatorios que falten.
- Comprobar formatos y coherencia básica entre los datos ingresados.
- Utilizar inteligencia artificial para comprender la descripción y sugerir una categoría.
- Señalar dudas, contradicciones o posibles incidencias duplicadas para revisión humana.
- Preparar un resumen estructurado para el personal responsable.
- Permitir la revisión humana y registrar la decisión sobre la continuidad del reclamo.
- Generar un código o ticket para consultar el estado y el historial.
- Registrar cambios de estado, fechas, responsables, observaciones y evidencias.
- Permitir que el área operativa informe avances, dificultades y finalización de una intervención.
- Incorporar fotografías u otros archivos como evidencia complementaria.
- Consultar al vecino sobre el resultado de la intervención y su experiencia con la gestión.
- Generar recordatorios y alertas cuando una incidencia permanezca sin actualizaciones durante un plazo configurable.
- Registrar los cierres administrativos, distinguiendo los casos confirmados por el vecino de aquellos cerrados sin respuesta.

### Funcionalidades fuera del alcance inicial

- Recibir o enviar reclamos reales a organismos municipales.
- Integrarse con plataformas, bases de datos o sistemas internos de EMVIAL.
- Asignar operarios, cuadrillas, materiales, vehículos o recursos municipales.
- Ordenar o ejecutar trabajos de reparación.
- Diagnosticar técnicamente fallas eléctricas.
- Consultar o confirmar automáticamente interrupciones del suministro eléctrico de EDEA.
- Aprobar administrativamente reclamos sin intervención humana.
- Confirmar por cuenta propia que una reparación fue realizada correctamente.
- Gestionar reclamos de otros servicios municipales, como bacheo, residuos, agua o tránsito.

## 3. Frontera del sistema

La frontera delimita qué elementos forman parte de SIGIA y cuáles pertenecen a su entorno.

### Elementos dentro de SIGIA

- Módulo de recepción y registro de incidencias.
- Módulo de comprensión y clasificación asistida por IA.
- Módulo de validación de datos.
- Módulo de revisión y seguimiento.
- Registro de estados, historial y evidencias.
- Mecanismo de notificaciones y recordatorios.
- Perfiles, permisos y registro de acciones de los usuarios.

### Elementos del entorno

- Vecinos que informan incidencias y consultan su seguimiento.
- Personal de revisión, que evalúa la información y autoriza la continuidad de la gestión.
- Área operativa, que informa avances y resultados de las intervenciones.
- EMVIAL y la Municipalidad, como contexto institucional de la propuesta.
- EDEA, como distribuidora de energía cuyo servicio puede influir en el funcionamiento del alumbrado.
- Red eléctrica, suministro de energía, barrios e infraestructura urbana.
- Normativa y condiciones del territorio.

**Aclaración sobre EDEA:** se la considera parte del entorno, no un actor con interacción informática en el prototipo. SIGIA no consultará sus sistemas ni podrá confirmar cortes de suministro. Si el vecino aporta información sobre un posible corte, el sistema podrá registrarla como dato orientativo para que el personal responsable la evalúe.

## 4. Actores y responsabilidades propuestas

Los siguientes roles son una separación funcional diseñada para el prototipo. No representan una descripción verificada de la estructura jerárquica interna de EMVIAL.

| Actor | Responsabilidades propuestas |
|---|---|
| Vecino | Registrar una incidencia, completar datos solicitados, consultar el ticket y su historial, informar si observa que el problema continúa o fue solucionado y evaluar la gestión. |
| Personal de revisión | Consultar incidencias, revisar la información organizada por SIGIA, evaluar advertencias, resolver dudas de clasificación, decidir si corresponde aprobar la continuidad y derivar el caso al área operativa. También controla demoras y discrepancias. |
| Área operativa | Consultar incidencias derivadas, informar el inicio y avance de una intervención, registrar dificultades, indicar motivos de demora, adjuntar evidencias e informar la finalización o imposibilidad de resolver el caso. |
| SIGIA / módulo de IA | Procesar y organizar la información según las reglas definidas, sugerir categorías, detectar faltantes o posibles inconsistencias y generar avisos. No toma decisiones administrativas ni ejecuta reparaciones. |

Los permisos deben corresponder a las responsabilidades de cada perfil. Por ejemplo, el vecino consulta y aporta información, pero no modifica el historial de intervenciones; el área operativa informa su trabajo, pero no reemplaza la aprobación administrativa del personal de revisión.

## 5. Información de entrada

Los datos iniciales propuestos para registrar una incidencia son:

| Dato | Condición | Uso |
|---|---|---|
| Tipo de servicio / incidencia | Obligatorio | Limitar el ingreso a alumbrado público. |
| Dirección exacta | Obligatorio | Ubicar el problema informado. |
| Barrio | Obligatorio | Aportar contexto territorial. |
| Descripción del problema | Obligatorio | Comprender qué sucede. |
| Descripción complementaria | Opcional | Aportar detalles adicionales. |
| Fotografía | Opcional | Ofrecer evidencia visual complementaria. |
| Información sobre posible corte eléctrico | Opcional | Registrar lo que conoce el vecino, sin considerarlo diagnóstico confirmado. |

SIGIA debe volver a validar el conjunto de datos cuando el vecino complete o corrija información. No debe inventar datos faltantes ni corregir silenciosamente información proporcionada por el usuario.

## 6. Procesamiento y reglas de control

El procesamiento propuesto contempla las siguientes etapas:

1. **Recepción:** registrar la información y generar un identificador único o ticket.
2. **Validación de campos:** comprobar que estén presentes los datos obligatorios y que respeten los formatos esperados.
3. **Comprensión y clasificación asistida:** la IA interpreta la descripción y sugiere una categoría, sin presentarla como diagnóstico técnico.
4. **Control de coherencia:** señalar contradicciones, datos dudosos o información insuficiente.
5. **Detección de posibles duplicados:** comparar datos relevantes, como ubicación y tipo de problema. Una coincidencia genera una advertencia; no elimina ni rechaza automáticamente el nuevo reporte.
6. **Preparación del resumen:** organizar los datos y las observaciones para la revisión humana.
7. **Revisión y decisión:** el personal responsable evalúa el caso y decide si corresponde aprobar su continuidad y derivarlo.
8. **Seguimiento:** registrar los cambios de estado y las novedades comunicadas por los actores.
9. **Evaluación del resultado:** registrar la información del área operativa y la opinión del vecino.
10. **Cierre:** dejar constancia de la decisión administrativa y de si hubo o no confirmación del vecino.

### Reglas ante incertidumbre

- Si faltan datos obligatorios, SIGIA solicita completarlos y mantiene el caso pendiente de validación.
- Si hay contradicciones, las señala y solicita aclaración o revisión.
- Si la IA no puede clasificar con suficiente seguridad, registra la clasificación como pendiente de revisión y explica el motivo.
- Si existe una posible coincidencia con otro reclamo, advierte al personal para que determine si se trata de la misma incidencia.
- Si aparece una posible relación con un corte eléctrico, registra la observación sin atribuir automáticamente la responsabilidad a EDEA ni descartar el reclamo.
- La IA no aprueba reclamos, no asigna trabajos y no confirma reparaciones.

## 7. Estados propuestos para el seguimiento

Los estados son una propuesta funcional para el prototipo. Su denominación y secuencia podrán ajustarse durante el modelado y las pruebas.

| Estado | Significado |
|---|---|
| Recibido | SIGIA registró la información inicial. |
| En validación | Se están comprobando los datos. |
| Incompleto | Faltan datos obligatorios o se necesita una corrección. |
| Listo para revisión | La información superó los controles automáticos iniciales. |
| Pendiente de revisión | Hay dudas, advertencias o una clasificación que requiere evaluación humana. |
| Aprobado para derivación | El personal responsable autorizó que continúe la gestión. |
| Derivado al área operativa | El caso fue remitido para su atención. |
| En gestión | El área operativa informó que está trabajando en el caso. |
| Pendiente de materiales | Se informó que hacen falta materiales para continuar. |
| Reparación informada | El área operativa comunicó que realizó el trabajo. |
| Pendiente de confirmación | Se consultó al vecino sobre el resultado. |
| Con observaciones | El vecino informó que el problema continúa o que la solución fue parcial, o existe una discrepancia que requiere revisión. |
| Cerrado administrativamente | Una persona responsable registró el cierre y su fundamento. |

El cierre debe distinguir expresamente entre **solución confirmada por el vecino** y **cierre sin respuesta del vecino**. La falta de respuesta después de un plazo definido no debe registrarse como una confirmación. El plazo y el procedimiento de cierre son parámetros propuestos que deberán definirse y justificarse en el proyecto.

## 8. Seguimiento, notificaciones y trazabilidad

Cada incidencia tendrá un ticket y un historial de eventos. Como mínimo, cada actualización registrará:

- Fecha y hora.
- Actor o perfil que realizó la acción.
- Estado anterior y nuevo estado.
- Descripción de la novedad.
- Observaciones y motivo de una demora, cuando corresponda.
- Evidencias adjuntas, si existen.

Los recordatorios se dirigirán según la responsabilidad de cada actor. Por ejemplo, ante una incidencia sin novedades, SIGIA podrá recordar al área operativa que actualice el caso y alertar al personal de revisión para que controle la demora. El vecino recibirá información sobre el estado, sin promesas de fechas que no hayan sido confirmadas.

Los plazos de recordatorio serán configurables y se definirán como parámetros del prototipo, no como tiempos oficiales de la Municipalidad o EMVIAL.

Las fotografías serán evidencia complementaria: por sí solas no garantizan que el trabajo se haya realizado correctamente. Si la evidencia no resulta suficiente, el personal de revisión podrá solicitar información adicional.

## 9. Resultado esperado

Como salida, SIGIA deberá producir:

- Un reclamo estructurado con un ticket único.
- Una indicación de si la información está incompleta, requiere revisión o está lista para evaluación humana.
- Una categoría sugerida y un resumen de la incidencia.
- Advertencias sobre inconsistencias o posibles duplicados.
- Un historial consultable de estados y actualizaciones.
- Notificaciones acordes a las responsabilidades de los actores.
- Un registro del resultado informado por el área operativa y de la opinión del vecino.
- Una constancia del cierre administrativo y de las evidencias asociadas.

## 10. Limitaciones y posibilidades futuras

El prototipo se probará exclusivamente con datos ficticios. No recibirá reclamos reales, no enviará comunicaciones a vecinos ni interactuará con sistemas municipales o de la distribuidora eléctrica.

En una etapa futura, y solo si existieran autorización institucional, análisis de seguridad, protección de datos, viabilidad técnica y acuerdos con los organismos correspondientes, podrían estudiarse integraciones con plataformas existentes. Esa posibilidad no forma parte de la primera versión ni se considera una condición para validar el proyecto académico.

## 11. Criterio de evaluación del alcance

La primera versión podrá considerarse alineada con su alcance si demuestra, mediante casos de prueba ficticios, que:

- Limita el registro a incidencias de alumbrado público.
- Detecta datos obligatorios faltantes y vuelve a validar la información corregida.
- Señala inconsistencias y dudas de clasificación sin inventar respuestas.
- Prepara resúmenes útiles para revisión humana.
- Advierte posibles duplicados sin descartar automáticamente reportes.
- Mantiene un historial de estados, responsables y evidencias.
- Genera recordatorios según reglas configurables.
- Diferencia una solución confirmada de un cierre sin respuesta del vecino.
- Respeta la separación de responsabilidades y permisos.
- No realiza acciones fuera de los límites establecidos.

---

**Nota metodológica:** este documento describe el alcance y la frontera de una propuesta académica. Los flujos, actores, estados, reglas y funcionalidades de SIGIA son decisiones de diseño del proyecto y no deben presentarse como procedimientos internos comprobados de EMVIAL.
