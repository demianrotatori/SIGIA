# Modelado del Sistema SIGIA

En esta sección se presentan los tres diagramas que modelan el comportamiento del Sistema Inteligente de Gestión de Incidencias de Alumbrado (SIGIA), desde una visión general hasta el detalle de un mecanismo de control específico.

---

## 1. Diagrama de Contexto

El diagrama de contexto muestra al **Sistema SIGIA** como una caja negra en el centro, delimitando claramente su frontera con los actores externos y otros sistemas con los que interactúa.

![Diagrama de Contexto](diagrama_contexto.png)

### Descripción de los flujos:
- **Ciudadano → SIGIA:** Envía el reclamo de alumbrado (texto, ubicación, descripción de la falla).
- **SIGIA → Ciudadano:** Solicita datos faltantes o confirma la recepción del reclamo.
- **SIGIA → Operador Humano:** Deriva el reclamo pre-clasificado para su validación.
- **Operador Humano → SIGIA:** Confirma o corrige la clasificación propuesta por el agente (mecanismo de **feedback**).
- **Operador Humano → Sistema de Órdenes de Trabajo Municipal:** Genera la orden de trabajo final una vez validada.

### Conceptos sistémicos representados:
- **Frontera:** El rectángulo central delimita lo que hace SIGIA y lo que queda fuera de su alcance.
- **Sistema abierto:** SIGIA intercambia información con su entorno (ciudadano, operador, sistema externo).
- **Sinergia:** El agente + el operador humano logran una gestión más eficiente que cualquiera de los dos por separado.

---

## 2. Diagrama de Casos de Uso (UML)

Este diagrama representa las funcionalidades del sistema desde la perspectiva de los actores principales: el **Ciudadano** (que inicia el reclamo) y el **Operador Humano** (que valida y aprueba la derivación).

![Diagrama de Casos de Uso](diagrama_casos_uso.png)

### Descripción de los casos de uso:
1. **Ingresar Reclamo de Alumbrado:** Caso de uso principal iniciado por el ciudadano.
2. **Validar y Completar Datos:** Relacionado mediante `<<include>>` con el caso anterior, ya que es una parte **obligatoria** del proceso de ingreso (el agente siempre verifica que haya dirección y tipo de falla).
3. **Revisar y Aprobar Derivación:** Relacionado mediante `<<extend>>` con el caso base, ya que **extiende** el flujo solo cuando se cumple la condición de requerir validación humana.

### Conceptos UML aplicados:
- **Actor:** Representa roles externos que interactúan con el sistema (Ciudadano, Operador Humano).
- **Frontera del sistema:** El rectángulo con esquina recortada contiene todos los casos de uso que pertenecen a SIGIA.
- **`<<include>>`:** Relación obligatoria entre casos de uso.
- **`<<extend>>`:** Relación condicional que amplía un caso de uso base.

---

## 3. Diagrama de Secuencia

Este diagrama ilustra el flujo de mensajes para el escenario de **"Urgencia Alta"** (cuando el ciudadano reporta un cable caído). Es el que mejor representa el **mecanismo de control** interno del agente.

![Diagrama de Secuencia](diagrama_secuencia.png)

### Descripción del flujo cronológico:
1. **`ingresarReclamo()`** → El ciudadano envía el reclamo a la interfaz web/app.
2. **`enviarTextoParaClasificar()`** → La interfaz reenvía el texto al Agente SIGIA.
3. **`evaluarReglas(): detectar("cable caído") → ALTA`** → El agente evalúa internamente el texto contra sus reglas de negocio (auto-mensaje). Esta es la parte central del **mecanismo de control**.
4. **`notificarUrgencia(ficha_pre_clasificada)`** → El agente notifica al operador humano con prioridad alta.
5. **`devolverRespuesta("🚨 Prioridad Alta")`** → El agente devuelve una respuesta a la interfaz.
6. **`mostrarMensaje()`** → La interfaz muestra el mensaje al ciudadano.

### Conceptos sistémicos representados:
- **Mecanismo de control:** El auto-mensaje `evaluarReglas()` representa el procesamiento interno donde el agente aplica sus reglas de negocio antes de emitir una salida.
- **Entrada → Procesamiento → Salida:** Se observa claramente el flujo de información a través del sistema.
- **Regla de negocio encapsulada:** El rectángulo punteado `[Regla: Urgencia Alta]` agrupa las acciones que se ejecutan cuando se detecta una condición específica.

---

## Coherencia entre diagramas

Los tres diagramas son **consistentes entre sí**:
- El **Diagrama de Contexto** muestra los actores y flujos generales.
- El **Diagrama de Casos de Uso** detalla las funcionalidades desde la perspectiva de esos actores.
- El **Diagrama de Secuencia** profundiza en un escenario específico (urgencia alta) mostrando cómo se ejecutan internamente las reglas de negocio.

Esta coherencia demuestra que el modelado del sistema SIGIA es sólido y está bien fundamentado en la Teoría General de Sistemas.