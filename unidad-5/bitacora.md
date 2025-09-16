
# Evidencias de la unidad 5


## Actividad 01

Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

- Comunicación vía UART / puerto serie (`uart.write()` ↔ p5.webserial).  
- Envía: `xValue,yValue,aState,bState\n` (acelerómetro X, acelerómetro Y, botón A, botón B).


¿Cómo es la estructura del protocolo ASCII usado?

- Línea por paquete, separada por comas y terminada en `\n`.  
- Ejemplo: `-123,456,True,False\n`.

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

Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.


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


### Rubrica

poner cada item y explicar el porque de la nota

