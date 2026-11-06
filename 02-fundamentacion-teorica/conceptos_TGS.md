# Fundamentación Teórica: Teoría General de Sistemas (TGS)

Este documento presenta los conceptos clave de la Teoría General de Sistemas aplicados al proyecto SIGIA (Sistema Inteligente de Gestión de Incidencias de Alumbrado).

## 1. Sistema
Un sistema es un conjunto de elementos interrelacionados que interactúan para lograr un objetivo común. En SIGIA, el sistema está compuesto por el agente de IA, la interfaz de usuario, el motor de reglas y los operadores humanos de la municipalidad.

## 2. Sistema Abierto
SIGIA es un **sistema abierto** porque intercambia información constantemente con su entorno:
- **Entradas:** Reclamos de ciudadanos (texto, ubicación), normativas municipales y horarios de atención.
- **Salidas:** Fichas de reclamo pre-clasificadas, respuestas automáticas al ciudadano y alertas al operador.
- **Interacción:** Se adapta al contexto externo y recibe retroalimentación del operador humano.

## 3. Frontera (Límites del Sistema)
La frontera define qué está dentro y qué está fuera del alcance del agente, garantizando la seguridad operativa:
- **Dentro de la frontera:** Recepción de texto, detección de datos faltantes, sugerencia de prioridad y derivación para validación.
- **Fuera de la frontera:** Reparación física de fallas, asignación de presupuestos, decisiones administrativas finales y acceso a datos sensibles no relevantes para el trámite.

## 4. Sinergia
La sinergia ocurre cuando el resultado del sistema completo es mayor que la suma de sus partes. En SIGIA:
**Agente IA + Operador Humano > Operador Humano solo**
El agente filtra y estructura los reclamos incompletos, permitiendo que el operador se enfoque exclusivamente en la validación y gestión de excepciones, aumentando la eficiencia global.

## 5. Recursividad
La recursividad establece que todo sistema es un subsistema de uno mayor, y a su vez contiene subsistemas propios:
- **Sistema mayor:** Municipalidad de General Pueyrredon.
  - **Sistema:** Dirección de Alumbrado Público / Plataforma 147.
    - **Subsistema:** SIGIA (Agente de IA).
      - **Sub-subsistema:** Motor de Reglas (evaluación de urgencia).
      - **Sub-subsistema:** Módulo de Interfaz (captura de datos).

## 6. Mecanismos de Control
Son las reglas que gobiernan el comportamiento del sistema para mantener su estabilidad:
1. **Control de datos:** Validación de información obligatoria (dirección) antes de avanzar.
2. **Control de urgencia:** Detección de palabras clave ("cable caído", "chispas") para priorización inmediata.
3. **Control humano (Human-in-the-loop):** Validación obligatoria del operador antes de generar una orden de trabajo final.

## Referencias
- Bertalanffy, L. von. *Teoría General de Sistemas*.
- Lorenzón, A. *Sistemas de Información*.
- Apuntes de clase: Sistemas y Organización, ISFT N° 151.