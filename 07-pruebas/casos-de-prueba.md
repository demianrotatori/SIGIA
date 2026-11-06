# 2 de octubre · Secuencia, reglas y control

En esta sección se documentan los recorridos, las reglas de negocio y las pruebas de validación del caso de uso principal: **"Ingresar Reclamo de Alumbrado"**.

## 1. Reglas de Negocio
1. **Si** el reclamo contiene una dirección válida y no presenta palabras de peligro, **el sistema debe** clasificarlo como prioridad media y derivarlo a la cola de validación estándar.
2. **Si** falta la dirección o la ubicación, **el sistema debe** detener la derivación y solicitar al ciudadano que complete el dato faltante antes de continuar.
3. **Si** el texto contiene indicadores de riesgo inminente (ej: "cable caído", "chispas"), **el sistema debe** ignorar el flujo estándar, clasificarlo como prioridad alta y notificar inmediatamente al operador de guardia.

## 2. Tabla de Pruebas (Consigna 2 de octubre)

A continuación, se detallan las tres pruebas requeridas (normal, falta de información y contradicción/riesgo), utilizando datos ficticios para simular el comportamiento del agente.

| Prueba | Datos ficticios (Entrada) | Resultado esperado | Criterio para aceptar | Resultado observado o simulado | ¿Cumplió? |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **Normal** | "No hay luz en calle 123 entre 45 y 46 desde ayer." | El sistema clasifica como "Prioridad Media" y deriva a la cola de validación estándar. | El sistema no solicita más datos y genera la ficha para el operador sin demoras. | Se generó la ficha #2026-1001 con clasificación "Media" y se mostró mensaje de registro al ciudadano. | **Sí** |
| **Falta información** | "Hola, hay una lámpara rota en mi barrio." | El sistema detecta que no hay dirección válida y detiene el flujo. | El sistema no deriva al operador y responde pidiendo la calle y altura exacta. | El sistema respondió: "Por favor, indicá la calle y la altura para procesar tu reclamo". No se generó ficha. | **Sí** |
| **Contradicción / Riesgo** | "Es solo una chispa pequeña, pero el cable está en el medio de la vereda y pasa gente." | El sistema prioriza las palabras de riesgo ("chispa", "cable en la vereda") sobre la minimización del usuario ("es solo una"). | El sistema ignora la contradicción del usuario, activa la alerta de prioridad alta y notifica al operador de guardia. | Se activó la etiqueta "[ALERTA PRIORITARIA]", se notificó al panel del operador y se advirtió al ciudadano que se aleje. | **Sí** |

## 3. Corrección y Ajuste (Si fue necesaria)
Durante la simulación de la **Prueba 3 (Contradicción/Riesgo)**, inicialmente el sistema dudaba entre "Prioridad Media" (por "chispa pequeña") y "Prioridad Alta". 
- **Ajuste realizado:** Se modificó la Regla N.º 3 para que *cualquier* mención de "cable" junto a "vereda" o "chispas" anule automáticamente otras clasificaciones y fuerce la alerta alta. 
- **Nueva prueba:** Se volvió a ejecutar la Prueba 3 con el mismo dato ficticio y el sistema ahora deriva directamente a prioridad alta sin dudar, cumpliendo el criterio de aceptación.

---

## 4. Coherencia con el Modelado
Estas pruebas validan directamente el **Diagrama de Secuencia** de la carpeta `04-modelado`. El "Resultado observado" confirma que el mecanismo de control (`evaluarReglas()`) funciona como se dibujó: el sistema evalúa la entrada antes de emitir la salida, garantizando que las reglas de negocio se respeten en cada escenario.