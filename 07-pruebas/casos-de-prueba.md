# Casos de Prueba y Mecanismos de Control

Este documento presenta las pruebas realizadas sobre el sistema SIGIA, utilizando datos ficticios para validar el comportamiento del agente frente a diferentes escenarios.

## Reglas de Negocio (Mecanismos de Control)

Las siguientes reglas gobiernan el comportamiento del agente y están modeladas en el **Diagrama de Secuencia**:

### Regla 1: Datos Obligatorios
Si el reclamo no contiene una dirección o calle, el agente NO deriva. Responde solicitando el dato faltante.

### Regla 2: Urgencia Alta
Si el texto contiene "cable caído", "chispas" o "peligro", el agente etiqueta el reclamo como **PRIORIDAD ALTA** y notifica inmediatamente al operador humano.

### Regla 3: Validación Humana Obligatoria
Toda derivación requiere confirmación del operador antes de generar una orden de trabajo final. El agente solo pre-clasifica, nunca decide por sí solo.

---

## Casos de Prueba

### Prueba T1: Camino Feliz - Reclamo estándar
| Campo | Valor |
|-------|-------|
| **Entrada** | "No hay luz en la calle 123 entre 45 y 46" |
| **Proceso** | El agente detecta dirección válida, clasifica como "Lámpara apagada", urgencia Media |
| **Salida esperada** | Ficha pre-clasificada enviada al operador para validación |
| **Resultado** | ✅ Éxito |

### Prueba T2: Urgencia Alta (Escenario del Diagrama de Secuencia)
| Campo | Valor |
|-------|-------|
| **Entrada** | "Cable caído en Av. Independencia 500, haciendo chispas" |
| **Proceso** | El agente detecta palabras clave de peligro (`evaluarReglas()`), clasifica como Urgencia ALTA |
| **Salida esperada** | Notificación inmediata al operador + mensaje al ciudadano: "🚨 Prioridad Alta" |
| **Resultado** | ✅ Éxito (ver Diagrama de Secuencia) |

### Prueba T3: Datos Faltantes
| Campo | Valor |
|-------|-------|
| **Entrada** | "Hay una lámpara rota" |
| **Proceso** | El agente detecta falta de dirección, aplica Regla 1 |
| **Salida esperada** | "Por favor, indicá la calle y la altura para procesar tu reclamo" |
| **Resultado** | ✅ Éxito |

### Prueba T4: Fuera de Alcance
| Campo | Valor |
|-------|-------|
| **Entrada** | "¿A qué hora cierra la municipalidad?" |
| **Proceso** | El agente detecta que no es un reclamo de alumbrado |
| **Salida esperada** | "Este canal es solo para reclamos de alumbrado. Para otras consultas, llame al 147" |
| **Resultado** | ✅ Éxito |

---

## Coherencia con los Diagramas

Las pruebas realizadas son **consistentes** con los diagramas modelados:

- **T2** corresponde exactamente al escenario del **Diagrama de Secuencia** (urgencia alta con cable caído).
- **T1 y T3** validan la relación `<<include>>` del **Diagrama de Casos de Uso** (validación obligatoria de datos).
- **Todas las pruebas** respetan la frontera del sistema mostrada en el **Diagrama de Contexto** (el agente nunca toma decisiones finales sin el operador humano).

---

## Conclusión de las Pruebas

El sistema SIGIA cumple con los mecanismos de control definidos:
- ✅ Detecta correctamente las urgencias altas
- ✅ Solicita datos faltantes antes de derivar
- ✅ Mantiene al operador humano en el loop de decisión
- ✅ Respeta la frontera del sistema (no toma decisiones administrativas)

El prototipo de simulación demuestra que el modelo sistémico es viable y está bien fundamentado en la Teoría General de Sistemas.