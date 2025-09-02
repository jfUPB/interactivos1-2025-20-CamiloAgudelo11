# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/P_2_3_2_01)

Código a modificar:

``` js
// P_2_3_2_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * draw tool. shows how to work with relations between elements.
 *
 * MOUSE
 * drag                : draw
 *
 * KEYS
 * 1                   : draw mode 1 - fixed distance
 * 2                   : draw mode 2 - distance threshold
 * del, backspace      : clear screen
 * arrow up            : line length +
 * arrow down          : line length -
 * s                   : save png
 */
'use strict';

var drawMode = 1;

var col;
var x = 0;
var y = 0;
var stepSize = 5.0;
var lineLength = 25;

function setup() {
  // use full screen size
  createCanvas(displayWidth, displayHeight);
  background(255);
  col = color(random(255), random(255), random(255), random(100));
  x = mouseX;
  y = mouseY;
  cursor(CROSS);
}

function draw() {
  if (mouseIsPressed && mouseButton == LEFT) {
    var d = dist(x, y, mouseX, mouseY);

    if (d > stepSize) {
      var angle = atan2(mouseY - y, mouseX - x);

      push();
      translate(x, y);
      rotate(angle);
      stroke(col);
      if (frameCount % 2 == 0) stroke(150);
      line(0, 0, 0, lineLength * random(0.95, 1) * d / 10);
      pop();

      if (drawMode == 1) {
        x = x + cos(angle) * stepSize;
        y = y + sin(angle) * stepSize;
      } else {
        x = mouseX;
        y = mouseY;
      }
    }
  }
}

function mousePressed() {
  x = mouseX;
  y = mouseY;
  col = color(random(255), random(255), random(255), random(100));
  // lineLength = random(15, 50);
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);

  if (key == '1') drawMode = 1;
  if (key == '2') drawMode = 2;
}

function keyPressed() {
  // lineLength ctrls arrowkeys up/down
  if (keyCode == UP_ARROW) lineLength += 5;
  if (keyCode == DOWN_ARROW) lineLength -= 5;
}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/CamiloAgudelo11/sketches/BtjMVGZXd)

Código modificado:

``` js
let drawMode = 1;
let col;
let x = 0;
let y = 0;
let stepSize = 5.0;
let lineLength = 25;


const STATES = {
  WAITING: "WAITING", // esperando conexión micro:bit
  RUNNING: "RUNNING"  // micro:bit conectado
};
let appState = STATES.WAITING;

let serial;
let mbX = 0, mbY = 0, mbA = 0, mbB = 0;
let microBitConnected = false;

function setup() {
  createCanvas(displayWidth, displayHeight);
  background(255);
  col = color(random(255), random(255), random(255), random(100));
  x = width / 2;
  y = height / 2;
  cursor(CROSS);

  
  serial = new p5.WebSerial();
  serial.getPorts();
  serial.on("noport", makePortButton);
  serial.on("portavailable", openPort);
  serial.on("data", serialEvent);
}

function makePortButton() {
  let button = createButton("Conectar Micro:bit");
  button.mousePressed(() => serial.requestPort());
}

function openPort() {
  serial.open();
}

function serialEvent() {
  let inString = serial.readLine().trim();
  if (!inString) return;

  let values = inString.split(",");
  if (values.length === 4) {
    mbX = int(values[0]);
    mbY = int(values[1]);
    mbA = int(values[2]);
    mbB = int(values[3]);
  }
}

function draw() {
  
  microBitConnected = serial.opened();

  switch (appState) {
    case STATES.WAITING:
      if (microBitConnected) {
        print("Micro:bit conectado");
        noCursor();
        appState = STATES.RUNNING;
      }
      break;

    case STATES.RUNNING:
      if (!microBitConnected) {
        print("Micro:bit desconectado");
        cursor();
        appState = STATES.WAITING;
        break;
      }

      
      let curX = map(mbX, -1024, 1024, 0, width);
      let curY = map(mbY, -1024, 1024, 0, height);

     
      if (mbB === 1) {
        background(255);
      }

     
      if (mbA === 1) {
        drawStroke(curX, curY);
      } else {
        x = curX;
        y = curY;
      }
      break;
  }

 
  if (mouseIsPressed && mouseButton === LEFT) {
    drawStroke(mouseX, mouseY);
  }
}

function drawStroke(targetX, targetY) {
  let d = dist(x, y, targetX, targetY);
  if (d > stepSize) {
    let angle = atan2(targetY - y, targetX - x);

    push();
    translate(x, y);
    rotate(angle);
    stroke(col);
    if (frameCount % 2 === 0) stroke(150);
    line(0, 0, 0, lineLength * random(0.95, 1) * d / 10);
    pop();

    if (drawMode == 1) {
      x = x + cos(angle) * stepSize;
      y = y + sin(angle) * stepSize;
    } else {
      x = targetX;
      y = targetY;
    }
  }
}

function mousePressed() {
  x = mouseX;
  y = mouseY;
  col = color(random(255), random(255), random(255), random(100));
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);

  if (key == '1') drawMode = 1;
  if (key == '2') drawMode = 2;
}

function keyPressed() {
  if (keyCode == UP_ARROW) lineLength += 5;
  if (keyCode == DOWN_ARROW) lineLength -= 5;
}

function timestamp() {
  return (
    year() +
    nf(month(), 2) +
    nf(day(), 2) +
    "_" +
    nf(hour(), 2) +
    nf(minute(), 2) +
    nf(second(), 2)
  );
}


```

## Video

[Video demostratativo](URL)





