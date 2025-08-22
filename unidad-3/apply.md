# Unidad 3


## 🛠 Fase: Apply

### Actividad 06

El código fuente de la bomba en p5.js. Debes utilizar la técnica de máquina de estados y la biblioteca de manejo de serial que estamos trabajando en el curso.

```
let estado = "CONFIG";   
let count = 20;                    
let password = ['A','B','A'];
let keyInput = [];
let lastMillis = 0;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(30);
}

function draw() {
  background(0);

  if (estado === "CONFIG") {
    fill(0, 255, 0);
    text("CONFIG", width/2, 50);
    text("Tiempo: " + count, width/2, height/2);

  } else if (estado === "ARMED") {
    fill(255, 255, 0);
    text("ARMED", width/2, 50);
    text("Tiempo: " + count, width/2, height/2);

  
    if (millis() - lastMillis > 1000) {
      lastMillis = millis();
      count--;
      if (count <= 0) {
        estado = "EXPLODED";
      }
    }

  } else if (estado === "EXPLODED") {
    fill(255, 0, 0);
    text(" EXPLODED ", width/2, height/2);
  }
}


function keyPressed() {
  let tecla = key.toUpperCase();  

  if (estado === "CONFIG") {
    if (tecla === 'A') {
      count = min(count + 1, 60);
    } else if (tecla === 'B') {
      count = max(count - 1, 10);
    } else if (tecla === 'S') {
      estado = "ARMED";
      lastMillis = millis();
    }
  }
  else if (estado === "ARMED") {
    if (tecla === 'A' || tecla === 'B') {
      keyInput.push(tecla);
      if (keyInput.length === password.length) {
        if (arraysEqual(keyInput, password)) {
          estado = "CONFIG";
          count = 20;
        }
        keyInput = [];
      }
    }
  }
  else if (estado === "EXPLODED") {
    if (tecla === 'T') {
      estado = "CONFIG";
      count = 20;
    }
  }
}

function arraysEqual(a, b) {
  if (a.length !== b.length) return false;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) return false;
  }
  return true;
}
````




### Actividad 07

Código p5.js


Enlace al editor de p5.js con tu código.


Código del micro:bit.


