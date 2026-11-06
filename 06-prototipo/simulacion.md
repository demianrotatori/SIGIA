# Prototipo de Simulación de SIGIA

Dado que este es un proyecto académico conceptual, el prototipo se implementa como una **simulación basada en escenarios** con datos ficticios. Esto demuestra el flujo lógico del agente sin requerir despliegue de infraestructura real ni conexión a sistemas municipales.

## Escenario 1: Reclamo de Urgencia Alta

**1. Entrada del Usuario (Ciudadano):**
> "Hola, hay un cable de luz caído en la vereda de Av. Independencia 500, está haciendo chispas y hay gente pasando."

**2. Procesamiento Interno del Agente (Motor de Reglas):**
- *Detección de entidad:* Dirección = "Av. Independencia 500" ✅ (Válido).
- *Detección de palabras clave:* "cable caído", "chispas" ⚠️.
- *Evaluación de regla:* Coincide con la **Regla de Urgencia Alta**.

**3. Salida del Sistema:**
- **Al Ciudadano (vía Interfaz):** "🚨 Hemos detectado una situación de PELIGRO INMINENTE. Su reclamo ha sido priorizado. Un operador de la Dirección de Alumbrado se comunicará a la brevedad. Por favor, aléjese de la zona."
- **Al Operador Humano (vía Panel Interno):** "[PRIORIDAD ALTA] Reclamo #2026-1145. Dirección: Av. Independencia 500. Descripción: Cable caído con chispas. Requiere validación y despacho inmediato de cuadrilla."

---

## Escenario 2: Reclamo Estándar (Camino Feliz)

**1. Entrada del Usuario (Ciudadano):**
> "No hay luz en la calle 123 entre 45 y 46 desde ayer a la noche."

**2. Procesamiento Interno del Agente:**
- *Detección de entidad:* Dirección = "calle 123 entre 45 y 46" ✅ (Válido).
- *Detección de palabras clave:* "no hay luz" (Sin indicadores de peligro inmediato).
- *Evaluación de regla:* Coincide con **Urgencia Media** - "Lámpara apagada".

**3. Salida del Sistema:**
- **Al Ciudadano:** "Su reclamo fue registrado correctamente. Será atendido en las próximas 48 horas hábiles."
- **Al Operador Humano:** Ficha pre-clasificada enviada a la cola de validación en horario normal.

---

## Validación del Alcance
Esta simulación demuestra que el agente respeta su **frontera**: no envía una cuadrilla automáticamente, sino que *pre-clasifica y notifica* para que el humano tome la decisión final, cumpliendo con el criterio de "Human-in-the-loop" (Humano en el bucle de decisión).