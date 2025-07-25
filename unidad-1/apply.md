# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

Explica cómo funciona el sistema físico interactivo que acabamos de crear.

Lo que hace el sistema es que cuando presionamos el boton A en el microbit en el programa p5.js se muestra un cuadro color rojo, y cuando no se presiona el cuadro se muestra verde; Ademas hay un boton en pantalla para conectar y desconectar el microbit.

Inputs: Boton A y boton para conectar y desconectar en p5.js.

Outputs: Color del cuadro(Verde o Rojo) y texto del boton de desconectar y conectar.

### Actividad 06

Escribe el enlace a tu programa en el editor de p5.js.

[Enlace a el código en p5.js](https://editor.p5js.org/CamiloAgudelo11/sketches/FwlyIeqTw)


Copia el código de tu programa en la bitácora (recuerda insertarlo usando markdown y el lenguaje javascript).

``` js
let port;
let x = 200;

function setup() {
  createCanvas(400, 400);
  port = createSerial();
  port.open("MicroPython", 115200);
}

function draw() {
  background(220);

  if (port.availableBytes() > 0) {
    let data = port.read(1);
    if (data == "A") {
      x -= 5; 
    } else if (data == "B") {
      x += 5; 
    }
  }

  x = constrain(x, 0, width);

  circle(x, height / 2, 50, 50);
}
```


Copia el código del micro:bit en la bitácora (recuerda insertarlo usando markdown y el lenguaje python).

``` py
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('A')
    elif button_b.is_pressed():
        uart.write('B')
    sleep(100)

