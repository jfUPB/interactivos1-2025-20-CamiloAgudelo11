
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

Binario: compacto, fijo, eficiente, pero depende de endian.


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

Binario: fijo en 6 bytes → más eficiente y rápido.

### Actividad 03

Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

En ASCII, los mensajes varían de longitud , así que \n marca el fin. En binario, tamaño fijo (6 bytes), así que se lee exactamente eso.

¿Qué ves en la consola? ¿Por qué crees que se produce este error?


(Ejemplo: microBitY: 513 en vez de 524). Porque si lee en medio de un paquete, mezcla bytes de mensajes diferentes, dando un error.



¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

micro:bit agrega header y checksum. p5.js usa buffer para buscar 0xAA, verifica checksum. Consola: Datos estables, sin errores.

### Actividad 04

Solucion: https://editor.p5js.org/CamiloAgudelo11/sketches/fGtALbNlG

Proceso de construccion :

Inicio: Tomé el código p5.js de la unidad anterior. Usé el código micro:bit dado.


Prueba intermedia 1: Intenté leer datos binarios sin framing, usando port.readBytes(6) y me salio un error: Valores incorrectos. Solución: Implementé framing como en la actividad 03, agregando serialBuffer, búsqueda de header (0xAA), y verificación de checksum.


Prueba intermedia 2: Añadí función readSerialData(). Error: Dibujo no aparecía correctamente. Solución: Verifiqué que microBitX y microBitY se usaran directamente en draw(), ya que el código original mapea estos valores para radius y circleResolution.


Código final: Integré framing/checksum en readSerialData(). Y me asegure que updateButtonStates detecte el evento de presión de B para limpiar la pantalla. 

Errores encontrados y soluciones:

Error 1: Círculos no se dibujaban al presionar A. Solución: Confirmé que microBitAState se actualizaba en readSerialData. 


Error 2: Pantalla no se limpiaba con botón B. Solución: Verifiqué que updateButtonStates detectara cambio de false a true en microBitBState. 



Experimentos:

Experimento 1: Moví micro:bit sin presionar – valores de microBitX/Y cambian en consola, pero mo dibuja y es correcto debido a que se necesita presionar A.


Experimento 2: Presioné A – dibuja círculos con resolución variable (basada en Y) y radio variable (basado en X). 


Experimento 3: Presioné B – limpia pantalla. 


Experimento 4: Desconecté/reconecté micro:bit – framing recupera sincronización rápidamente.

 

### Rubrica

1)Profundidad de la indagacion:3.5

Justificación: Aunque le di respuesta a la mayoria de preguntas que se propusieron, pude haber hecho una mayor indagacion o formular mas preguntas acerca de los temas que se trataron.


Evidencias: En todas las actividades respondi las preguntas que se formularon.

2)Calidad de la experimentacion:4

Justificación: Diseñe y probe distintos experimentos, como cambiando algunas partes del codigo de algunas actividades y ver que pasa, de igual manera pude haber hecho mas experimentos pero me enfoque especialmente en el codigo de la actividad 04 y pude haber hecho otros experimentos con los codigos anteriores.


Evidencias: Actividad 04


3)Analisis y reflexion:3.4

Justificación: No se pusieron capturas de la terminal o logs de consola, ademas se resuelven los problemas pero de una manera superficial donde se podria indagar mas.


Evidencias: En todas las actividades se evidencia la resolucion de distintos problemas.


4)Apropiación y Articulación de Conceptos:4

Justificación:  Aunque en algunos puntos de las actividades se da una respuesta sencilla, tambien se puede evidenciar que puse ejemplos que ayuda a respaldar la definicion.

Evidencias: De la actividad 01 hasta la 03


Nota: 3.7


