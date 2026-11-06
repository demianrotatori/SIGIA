# Análisis Sistémico de SIGIA

Este documento integra la definición del problema, los objetivos, el alcance, la frontera y el modelo sistémico del Agente SIGIA, cumpliendo con los requisitos de la Teoría General de Sistemas.

---

## 1. Problema y Objetivos

### 1.1 Problema Detectado
La Dirección de Alumbrado Público de la Municipalidad de General Pueyrredon recibe una alta volumen de reclamos a través de la Plataforma 147, WhatsApp y web. Gran parte de estos reclamos llegan con datos incompletos (sin dirección, sin descripción clara de la falla) o duplicados. El personal operativo pierde tiempo valioso clasificando manualmente cada caso, lo que retrasa la atención de emergencias reales (ej: cables caídos) y satura la agenda de trabajo.

### 1.2 Objetivos del Sistema
- **Objetivo General:** Optimizar el proceso de recepción, clasificación y derivación de incidencias de alumbrado público mediante un agente de IA.
- **Objetivos Específicos:**
  1. Detectar y solicitar automáticamente datos faltantes en los reclamos.
  2. Clasificar la urgencia del reclamo (Alta, Media, Baja) según reglas de negocio predefinidas.
  3. Derivar el reclamo pre-estructurado al operador humano para su validación final.

---

## 2. Alcance y Frontera del Sistema

Para garantizar la seguridad operativa y legal, es fundamental definir los límites (frontera) del sistema.

### 2.1 Alcance (LO QUE SÍ HACE SIGIA)
- Recibe y procesa texto en lenguaje natural proveniente del ciudadano.
- Detecta entidades clave (dirección, tipo de falla, palabras de urgencia).
- Solicita interactivamente datos faltantes al usuario.
- Genera una "Ficha de Reclamo Pre-clasificada" con una sugerencia de prioridad.
- Notifica al operador humano y mantiene un registro del intercambio.

### 2.2 Frontera (LO QUE NO HACE SIGIA)
- **NO toma decisiones administrativas finales:** La orden de trabajo solo se genera tras la validación humana.
- **NO repara fallas físicas ni asigna recursos:** Eso corresponde al sistema de Órdenes de Trabajo y al personal de campo.
- **NO accede a datos sensibles:** No consulta historias crediticias, datos financieros ni información privada más allá de la necesaria para el trámite.
- **NO diagnostica causas técnicas complejas:** Solo clasifica la *sintomatología* reportada por el ciudadano.

*Esta frontera actúa como un mecanismo de encapsulamiento, protegiendo al sistema municipal de acciones autónomas no supervisadas.*

---

## 3. Modelo Sistémico (Teoría General de Sistemas)

### 3.1 Sistema Abierto
SIGIA es un **sistema abierto** porque intercambia materia, energía e información con su entorno. 
- **Entradas:** Reclamos de ciudadanos, normativas municipales, horarios de atención.
- **Salidas:** Fichas pre-clasificadas, respuestas automáticas, alertas de urgencia.
- **Retroalimentación (Feedback):** El operador humano puede corregir la clasificación del agente, lo que permite ajustar futuras reglas de negocio.

### 3.2 Sinergia
El sistema demuestra sinergia porque el resultado del conjunto (Agente SIGIA + Operador Humano) es superior a la suma de sus partes. El agente filtra el "ruido" (datos incompletos, duplicados, consultas fuera de alcance), permitiendo que el recurso humano se enfoque exclusivamente en la validación y la gestión de excepciones, aumentando la eficiencia global del proceso.

### 3.3 Recursividad
SIGIA puede analizarse como un sistema compuesto por subsistemas interrelacionados:
1. **Subsistema de Interfaz:** Captura y normaliza la entrada del usuario.
2. **Subsistema de Motor de Reglas:** Evalúa el texto contra patrones (ej: "cable caído" = Urgencia Alta).
3. **Subsistema de Derivación:** Formatea la salida y la envía al canal correspondiente (Operador o Ciudadano).
Cada subsistema tiene su propia lógica, pero todos sirven al propósito del sistema mayor: la gestión eficiente del alumbrado público.

### 3.4 Mecanismos de Control
El sistema incorpora reglas explícitas para mantener la homeostasis y el correcto funcionamiento:
- **Control de Datos:** Si falta la dirección, el flujo se detiene y se solicita el dato (no avanza a derivación).
- **Control de Urgencia:** Si se detectan palabras clave de peligro, se ignora el flujo estándar y se activa la notificación prioritaria.
- **Control Humano en el Loop (Human-in-the-loop):** Ninguna orden de trabajo se emite sin la aprobación final del operador, garantizando la supervisión.

### 3.5 Perturbaciones y Preguntas de Investigación (Clase 12)

**Perturbaciones del entorno (factores externos que afectan al sistema):**
1. Saturación del sistema municipal en días de tormentas (aumento abrupto e inesperado de entradas).
2. Fallas en la conexión a internet del ciudadano (pérdida o interrupción del flujo de entrada).
3. Cambios en la normativa municipal de tiempos de respuesta (modificación externa de las reglas de control).

**5 Preguntas de investigación pendientes (antes del diseño final del agente):**
1. ¿Qué porcentaje de los reclamos actuales llega sin dirección válida o datos incompletos?
2. ¿Cuál es el tiempo promedio de respuesta humana actual para una urgencia alta?
3. ¿Qué canales de entrada (WhatsApp, web, teléfono) generan más datos incompletos?
4. ¿Cómo afecta la estacionalidad (ej. tormentas de verano) a la carga y rendimiento del sistema?
5. ¿Qué nivel de precisión en la clasificación automática es aceptable para la municipalidad antes de requerir intervención humana obligatoria?

---

## 4. Relación con el Modelado

Los conceptos descritos en este análisis se materializan visualmente en los diagramas de la carpeta `04-modelado/`:
- La **Frontera** y los **Actores** se reflejan en el *Diagrama de Contexto*.
- El **Alcance** y las interacciones obligatorias/condicionales se