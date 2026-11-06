# Prototipo de Simulación Conceptual - SIGIA

## 1. Propósito de la Simulación
Dado el alcance académico del proyecto, este prototipo se presenta como una **simulación conceptual basada en escenarios con datos ficticios**. Su objetivo es validar el flujo lógico, las reglas de negocio y los mecanismos de control definidos en el modelado sistémico, sin requerir la implementación de infraestructura de software real ni la conexión a bases de datos de la Municipalidad de General Pueyrredon.

## 2. Escenario A: Incidente de Alta Prioridad

**2.1. Entrada del Sistema (Input)**
> "Se reporta caída de cableado eléctrico en la vía pública, Avenida Independencia 500, con generación de chispas y riesgo para peatones."

**2.2. Procesamiento Interno (Motor de Reglas)**
- **Validación de entidades:** Se detecta ubicación geográfica válida ("Avenida Independencia 500").
- **Análisis léxico:** Se identifican términos críticos: "caída de cableado", "chispas", "riesgo".
- **Evaluación de regla de negocio:** La combinación de términos activa la **Regla de Prioridad Alta**.

**2.3. Salidas del Sistema (Outputs)**
- **Hacia el Ciudadano:** "Su reporte ha sido registrado con carácter de URGENCIA. El personal de guardia ha sido notificado. Por motivos de seguridad, se le solicita mantenerse alejado de la zona."
- **Hacia el Operador Humano (Panel de Gestión):** "[ALERTA PRIORITARIA] Ticket #2026-8842. Ubicación: Av. Independencia 500. Clasificación automática: Riesgo eléctrico inminente. Requiere validación y despacho inmediato de cuadrilla."

## 3. Escenario B: Incidente Estándar (Flujo Normal)

**3.1. Entrada del Sistema (Input)**
> "Falta de alumbrado en calle 123, entre calles 45 y 46, desde las 20:00 hs del día de ayer."

**3.2. Procesamiento Interno (Motor de Reglas)**
- **Validación de entidades:** Se detecta ubicación válida y referencia temporal.
- **Análisis léxico:** Se identifica falla estándar ("Falta de alumbrado") sin indicadores de riesgo inmediato.
- **Evaluación de regla de negocio:** Se clasifica como **Prioridad Media** (Mantenimiento programado).

**3.3. Salidas del Sistema (Outputs)**
- **Hacia el Ciudadano:** "Su solicitud ha sido registrada correctamente. Será evaluada por el área competente en el próximo ciclo de revisión (48 a 72 horas hábiles)."
- **Hacia el Operador Humano:** Ficha de reclamo pre-clasificada ingresada en la cola de validación estándar.

## 4. Validación del Alcance y Frontera
Esta simulación demuestra que el sistema respeta estrictamente su **frontera operativa**. El agente SIGIA actúa como un filtro y clasificador, pero no ejecuta acciones autónomas de campo ni toma decisiones administrativas finales. La derivación a un operador humano para su validación garantiza el principio de "Humano en el bucle" (*Human-in-the-loop*), mitigando riesgos operativos y legales.