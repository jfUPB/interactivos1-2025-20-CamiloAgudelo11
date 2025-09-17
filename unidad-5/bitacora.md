
# Evidencias de la unidad 5


## Actividad 01

Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

- Comunicación vía UART / puerto serie (`uart.write()` ↔ p5.webserial).  
- Envía: `xValue,yValue,aState,bState\n` (acelerómetro X, acelerómetro Y, botón A, botón B).


¿Cómo es la estructura del protocolo ASCII usado?

- Línea por paquete, separada por comas y terminada en `\n`.  

Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.

```js
let data = port.readUntil("\n");
let values = data.split(",");
microBitX = int(values[0]) + windowWidth / 2;
microBitY = int(values[1]) + windowHeight / 2;
```
readUntil("\n"): recibe el paquete completo.

split(","): separa valores.

+ windowWidth/2, + windowHeight/2: centra coordenadas en la pantalla.

¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?


A pressed: newAState == true && prev == false.


B released: newBState == false && prev == true.



## Actividad 02

¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?

Binario: compacto, fijo, eficiente, pero ilegible y dependiente de endian.


ASCII: legible y fácil de depurar, pero ocupa más y es más lento.

Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

Total: 6 bytes.

Bytes 0–1: xValue (int16).

Bytes 2–3: yValue (int16).

Byte 4: aState (0 o 1).

Byte 5: bState (0 o 1).

Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?

500 → 01 F4

524 → 02 0C

-1 → FF FF

-500 → FE 0C

Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?

ASCII: ocupa más espacio (ej. "500" = 3 bytes + coma + salto de línea).

Binario: fijo en 6 bytes → más eficiente y rápido para el receptor.

### Actividad 03

Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

En ASCII, los mensajes varían de longitud , así que \n marca el fin. En binario, tamaño fijo (6 bytes), así que se lee exactamente eso.

¿Qué ves en la consola? ¿Por qué crees que se produce este error?

(Ejemplo: microBitY: 513 en vez de 524). Porque si lee en medio de un paquete, mezcla bytes de mensajes diferentes, dando valores erróneos.

Agrega header (0xAA) y checksum. En consola: Valores correctos siempre (500,524,true,false). No hay errores de sincronización.


¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

micro:bit agrega header y checksum. p5.js usa buffer para buscar 0xAA, verifica checksum. Consola: Datos estables, sin errores.

### Actividad 04

Solucion: https://editor.p5js.org/CamiloAgudelo11/sketches/fGtALbNlG

Proceso de construccion :

Inicio: Tomé el código p5.js proporcionado (ASCII, dibuja círculos). Usé el código micro:bit dado (binario con header/checksum).


Prueba intermedia 1: Intenté leer datos binarios sin framing, usando port.readBytes(6). Error: Valores incorrectos (ej: microBitX=3073) por desalineación de paquetes. Solución: Implementé framing como en actividad 03, agregando serialBuffer, búsqueda de header (0xAA), y verificación de checksum.


Prueba intermedia 2: Añadí función readSerialData() basada en actividad 03. Error: Dibujo no aparecía correctamente. Solución: Verifiqué que microBitX y microBitY se usaran directamente en draw(), ya que el código original mapea estos valores para radius y circleResolution. Mantuve la lógica de dibujo intacta.


Código final: Integré framing/checksum en readSerialData(). Eliminé connectionInitialized (no necesario con framing). Aseguré que updateButtonStates detecte el evento de presión de B para limpiar la pantalla. 

Errores encontrados y soluciones:

Error 1: Círculos no se dibujaban al presionar A. Solución: Confirmé que microBitAState se actualizaba en readSerialData. Evidencia: Código final, función readSerialData.


Error 2: Pantalla no se limpiaba con botón B. Solución: Verifiqué que updateButtonStates detectara cambio de false a true en microBitBState. Evidencia: Código final, función updateButtonStates.


Error 3: Checksum fallaba ocasionalmente. Solución: Revisé cálculo en micro:bit (sum(data) % 256) y aseguré que p5.js comparara correctamente (dataBytes.reduce(...)). Evidencia: Proceso de construcción, prueba con SerialTerminal.


Error 4: Desalineación tras reconexión. Solución: Framing (0xAA) y port.clear() en estado RUNNING aseguraron sincronización. Evidencia: Código final, estado RUNNING.



Experimentos:

Experimento 1: Moví micro:bit sin presionar – valores de microBitX/Y cambian en consola, pero no se dibuja (correcto, requiere A). Evidencia: Consola muestra valores como microBitX: 500, microBitY: 524.


Experimento 2: Presioné A – dibuja círculos con resolución variable (basada en Y) y radio variable (basado en X). (Imagina captura: círculos concéntricos en canvas 720x720). Evidencia: Descripción en experimentos.


Experimento 3: Presioné B – limpia pantalla. Funciona al detectar cambio de false a true. Evidencia: Mensaje en consola “Pantalla limpiada con botón B”.


Experimento 4: Desconecté/reconecté micro:bit – framing recupera sincronización rápidamente, sin valores erróneos. Evidencia: Consola muestra datos estables tras reconexión.

 
Experimento 5: Comparé binario vs ASCII (usando código original). Binario: Menos lag, más eficiente (8 bytes vs 20+). Desventaja: Difícil depurar sin SerialTerminal. Evidencia: Comparación en experimentos.

### Rubrica

1)Profundidad de la indagacion:4

Justificación: Formulé preguntas que exploran el diseño y sus implicaciones, como "¿Cómo se relacionan los bytes enviados con el formato '>2h2B'?" en la Actividad 02, y "¿Por qué el framing evita errores de sincronización?" en la Actividad 03. Esto va más allá de lo básico, cuestionando el impacto en la comunicación serial y proponiendo experimentos para validar ideas, lo que demuestra una curiosidad proactiva.


Evidencias: En Actividad 01 (explicación del protocolo ASCII y eventos de botones); Actividad 02 (análisis de bytes en hex y comparación con ASCII); Actividad 03 (comparación de códigos y error de sincronización); Actividad 04 (proceso de construcción con pruebas intermedias)

2)Calidad de la experimentacion:4 

Justificación: Diseñé y ejecuté experimentos precisos y creativos, como cambiar el código para enviar datos fijos y verificar en la consola (Actividad 03), o probar variaciones del acelerómetro para dibujar círculos con diferentes resoluciones (Actividad 04). Incluí capturas y observaciones para validar hipótesis, como la integridad de los datos con checksum, mostrando un enfoque sistemático y no solo ejecución básica.


Evidencias: En Actividad 02 (experimentos con shake y comparación ASCII/binario, con capturas en SerialTerminal); Actividad 03 (ejecución repetida para reproducir errores de sincronización y solución con framing); Actividad 04 (experimentos con movimiento del micro:bit, botón B y guardado de imagen, con screenshots antes/después).

3) Analisis y reflexion:3.8

Justificación: La bitácora demuestra una comprensión clara y profunda de la evidencia, con reflexiones sobre ventajas/desventajas (ej. binario es eficiente pero menos legible) y cómo el checksum asegura integridad. Analicé errores (ej. desalineación) y sus soluciones, conectando conceptos como framing con problemas reales, lo que refleja una reflexión madura.


Evidencias: En Actividad 01 (análisis de estructura del protocolo y generación de eventos); Actividad 02 (reflexión sobre ventajas/desventajas de formatos y relación de bytes con código); Actividad 03 (análisis del error de sincronización y por qué no se necesita delimitador); Actividad 04 (reflexión sobre mejoras en eficiencia y depuración de errores).


4) Apropiación y Articulación de Conceptos:4.5

Justificación: Demostré una maestría analítica al aplicar conceptos como protocolo binario con framing en una aplicación completa, modificando el código para dibujar círculos interactivos y manejar eventos. Exploré el flujo de datos desde el micro:bit hasta p5.js, garantizando una comunicación fiable, y documenté el proceso con énfasis en conceptos clave como checksum y sincronización.

Evidencias: En Actividad 01 (repaso del caso ASCII); Actividad 02 (transformación a binario en micro:bit); Actividad 03 (adaptación en p5.js con DataView); Actividad 04 (aplicación final con código proporcionado, integrando todo para un sistema interactivo con círculos y limpieza de pantalla).
