
# Evidencias de la unidad 8


## Autoevaluacion:5.0

Actividad 1: 5.0

Realice todos los puntos de la  actividad, incluyendo bocetos, referencias y explicando lo que queria diseñar.


Actividad 2: 5.0

Documente todo el proceso que realice para llegar al resultado, ademas adjunte todos los codigos requeridos.


## Actividad 01


Documenta los referentes visuales que te inspiren.

<img width="310" height="163" alt="image" src="https://github.com/user-attachments/assets/4d490c42-e81e-4c06-904d-a1389456b7ae" />


<img width="283" height="178" alt="image" src="https://github.com/user-attachments/assets/d734fdc6-4b91-4d7a-b2b6-a7761623f41b" />


Define el concepto de las visuales que quieres crear.

Las visuales que quiero crear es que tanto por medio de el micro:bit y el celular poder enviar emojis que esten relacionados con el tema musical y que mientras tanto en la pantalla del PC se vea una ola que se mueva al ritmo de la cancion.


Explica cómo el móvil y el micro:bit controlarán las visuales.

El celular si deslizas para arriba aparecen nubes y cuando deslizo para abajo aparecen llamas. Por otro lado en el micro:bit cuando se presiona el boton A aparecera un emoji de angel y si se presiona el boton B aparece emojis de demonio.


Haz un bocetos de todas las interfaces del sistema.


<img width="1401" height="785" alt="Captura de pantalla 2025-10-30 150523" src="https://github.com/user-attachments/assets/291ac933-9a14-4b52-879f-8d1440467c23" />



Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema.



<img width="511" height="618" alt="Captura de pantalla 2025-10-30 151856" src="https://github.com/user-attachments/assets/a114a075-ebb5-4072-86c5-6afe40722807" />


## Actividad 02


### Documenta todo el proceso de construcción.

Primero descargue la cancion la cual iba a utilizar y la subi a VS code, despues le explique a la IA lo que queria hacer e hizo los siguientes codigos


codigo desktop
```
let song;
let fft;
let socket;
let started = false;
let visuals = [];

function preload() {
  song = loadSound('zell.mp3'); // Tema musical
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT();
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms");

  // Recibir elementos desde el móvil
  socket.on("newElement", (data) => {
    visuals.push({
      type: data,
      x: random(width),
      y: random(height),
      size: 50
    });
  });

  // Recibir emojis desde micro:bit
  socket.on("microbit", (data) => {
    visuals.push({
      type: data,
      x: random(width),
      y: random(height / 2),
      size: 70
    });
  });

  background(0);
  textAlign(CENTER);
  textSize(24);
  fill(255);
  text("Haz click para iniciar 'Cielo al Infierno'", width / 2, height / 2);
}

function mousePressed() {
  if (!started) {
    song.play();
    started = true;
  }
}

function draw() {
  if (!started) return;

  background(0, 30, 60);
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let amplitude = map(bass, 0, 255, 20, 150);

  // Dibujar olas al ritmo
  noFill();
  stroke(255);
  strokeWeight(3);
  beginShape();
  for (let x = 0; x <= width; x += 10) {
    let y = height / 2 + sin(x * 0.02 + frameCount * 0.05) * amplitude;
    vertex(x, y);
  }
  endShape();

  // Dibujar visuales que llegan del móvil o microbit
  for (let v of visuals) {
    drawVisual(v);
  }
}

function drawVisual(v) {
  textAlign(CENTER);
  textSize(v.size);
  noStroke();
  if (v.type === "nube") text("☁️", v.x, v.y);
  else if (v.type === "fuego") text("🔥", v.x, v.y);
  else if (v.type === "angel") text("😇", v.x, v.y);
  else if (v.type === "demonio") text("😈", v.x, v.y);
}

```

Codigo mobile


```
let socket;
let startY = null;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms");
  textAlign(CENTER);
  textSize(24);
}

function draw() {
  background(20);
  fill(255);
  text("Desliza hacia arriba 🔥 o hacia abajo ☁️", width / 2, height / 2);
}

function touchStarted() {
  startY = mouseY;
}

function touchEnded() {
  if (startY === null) return;
  let deltaY = mouseY - startY;

  if (deltaY > 50) { 
    socket.emit("newElement", "nube");
  } else if (deltaY < -50) {
    socket.emit("newElement", "fuego");
  }
  startY = null;
}


```


codigo server

```
import express from "express";
import { createServer } from "http";
import { Server } from "socket.io";
import SerialPort from "serialport";
import Readline from "@serialport/parser-readline";
import path from "path";
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const server = createServer(app);
const io = new Server(server, {
  cors: { origin: "*", methods: ["GET", "POST"] }
});

// --- Comunicación con micro:bit ---
const port = new SerialPort({ path: "COM3", baudRate: 115200 }); // cambia COM3 por el tuyo
const parser = port.pipe(new Readline({ delimiter: "\r\n" }));

parser.on("data", (data) => {
  const msg = data.trim();
  console.log("📡 Microbit:", msg);
  io.emit("microbit", msg);
});

// --- Comunicación con el móvil y el desktop ---
io.on("connection", (socket) => {
  console.log("✅ Cliente conectado:", socket.id);
  socket.on("newElement", (data) => {
    io.emit("newElement", data);
  });
});

server.listen(3000, () => console.log("Servidor en http://localhost:3000"));


```


Luego instale serialport, y tuve que cambiar el codigo del server.js ya que el SerialPort y ReadLine no funcionaban correctamente, y cambie el socket = io.connect por el link que se genero en mi port para desktop y mobile.


Despues me di cuenta de que no estaba correcta la conexion del celular al desktop ya que cuando deslizaba en el celular no pasaba nada asi que cambie los codigos

Codigo Mobile


```
let socket;
let startY = null;

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  // Conexión al túnel (asegúrate de que esté activo)
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms/");

  socket.on("connect", () => {
    console.log("✅ Conectado al servidor con ID:", socket.id);
  });

  textAlign(CENTER);
  textSize(24);
}

function draw() {
  background(20);
  fill(255);
  text("⬆️ Desliza arriba = fuego\n⬇️ Desliza abajo = nubes", width / 2, height / 2);
}

function touchStarted() {
  startY = mouseY;
}

function touchEnded() {
  if (startY === null) return;
  let deltaY = mouseY - startY;

  if (deltaY > 50) {
    socket.emit("newElement", "nube");
    console.log("🌥️ Enviado: nube");
  } 
  else if (deltaY < -50) {
    socket.emit("newElement", "fuego");
    console.log("🔥 Enviado: fuego");
  }

  startY = null;
}

```

Codigo desktop

```
let song;
let fft;
let socket;
let started = false;
let visuals = [];

// 🎵 Carga la canción
function preload() {
  song = loadSound("KHEA - Del cielo al infierno.mp3");
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT();

  // 🔗 Conexión al servidor (usa tu DevTunnel)
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms/");

  // ✅ Escucha los mensajes del móvil
  socket.on("newElement", (data) => {
    console.log("📲 Elemento recibido del móvil:", data);
    crearVisual(data);
  });

  // ✅ Escucha los mensajes del micro:bit
  socket.on("microbit", (data) => {
    console.log("💡 Señal desde micro:bit:", data);
    crearVisual(data);
  });

  // Pantalla inicial
  background(0);
  textAlign(CENTER);
  textSize(24);
  fill(255);
  text("Haz click para iniciar 'Cielo al Infierno'", width / 2, height / 2);
}

function mousePressed() {
  if (!started) {
    song.play();
    started = true;
  }
}

function draw() {
  if (!started) return;

  background(10, 25, 45);

  // 🎚️ Visual del sonido
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let amplitude = map(bass, 0, 255, 20, 150);

  noFill();
  stroke(255);
  strokeWeight(3);
  beginShape();
  for (let x = 0; x <= width; x += 10) {
    let y = height / 2 + sin(x * 0.02 + frameCount * 0.05) * amplitude;
    vertex(x, y);
  }
  endShape();

  // 🎨 Dibujar visuales activos
  for (let v of visuals) {
    v.y += v.velY; // movimiento vertical
    v.x += v.velX; // movimiento horizontal
    drawVisual(v);
  }

  // 🧹 Eliminar los que salen de pantalla
  visuals = visuals.filter((v) => v.y > -100 && v.y < height + 100);
}

// ✨ Crear visuales nuevos con animación
function crearVisual(tipo) {
  console.log("🌈 creando visual de tipo:", tipo); // debug

  let v = {
    type: tipo,
    x: random(width),
    y: tipo === "nube" ? -50 : height + 50, // nubes bajan, fuego sube
    size: random(60, 120),
    velY: tipo === "nube" ? random(1, 2) : random(-3, -1),
    velX: random(-0.5, 0.5),
    life: 255, // transparencia para animación
  };
  visuals.push(v);
}

// 🧩 Dibujar cada visual según tipo
function drawVisual(v) {
  textAlign(CENTER);
  textSize(v.size);
  noStroke();
  fill(255, v.life);

  if (v.type === "nube") text("☁️", v.x, v.y);
  else if (v.type === "fuego") text("🔥", v.x, v.y);
  else if (v.type === "angel") text("😇", v.x, v.y);
  else if (v.type === "demonio") text("😈", v.x, v.y);

  v.life -= 2; // se desvanece lentamente
}


```


Y por ultimo realice el codigo del microbit 

```
from microbit import *

while True:
    if button_a.was_pressed():
        print("angel")   # 🔁 Esto sí llega por USB
        display.show("A")
        sleep(300)
        display.clear()

    if button_b.was_pressed():
        print("demonio")  # 🔁 Esto sí llega por USB
        display.show("B")
        sleep(300)
        display.clear()

    sleep(100)
```


### Incluye todos los códigos: servidor, cliente móvil, cliente de escritorio y micro:bit.


Codigo Servidor 

```
import express from "express";
import { createServer } from "http";
import { Server } from "socket.io";
import { SerialPort } from "serialport";
import { ReadlineParser } from "@serialport/parser-readline";
import path from "path";
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const server = createServer(app);
const io = new Server(server, {
  cors: {
    origin: "*",
    methods: ["GET", "POST"],
  },
});

// --- Servir archivos estáticos ---
app.use(express.static(path.join(__dirname, "public")));

app.get("/desktop", (req, res) => {
  res.sendFile(path.join(__dirname, "public/desktop/index.html"));
});

app.get("/mobile", (req, res) => {
  res.sendFile(path.join(__dirname, "public/mobile/index.html"));
});

// --- Comunicación con micro:bit ---
let port;
try {
  port = new SerialPort({ path: "COM5", baudRate: 115200 }); // 👈 ajusta si cambia el COM
  const parser = port.pipe(new ReadlineParser({ delimiter: "\r\n" }));

  port.on("open", () => console.log("✅ Puerto serial abierto con micro:bit"));
  port.on("error", (err) => console.error("❌ Error puerto serial:", err.message));

  parser.on("data", (data) => {
  console.log("📡 Microbit RAW:", JSON.stringify(data)); // debug más preciso
  const msg = data.trim();
  console.log("📡 Microbit limpio:", msg);
  io.emit("microbit", msg);
});

} catch (err) {
  console.error("⚠️ No se pudo abrir el puerto serial:", err.message);
}

// --- Comunicación SOCKET.IO ---
io.on("connection", (socket) => {
  console.log("✅ Cliente conectado:", socket.id);

  // 📱 Móvil → servidor → desktop
  socket.on("newElement", (data) => {
    console.log("📲 Recibido del móvil:", data);

    // 🔁 Reenvía a todos los demás (desktop incluido)
    socket.broadcast.emit("newElement", data);

    // 🔧 También lo envía al micro:bit (si está conectado)
    if (port && port.isOpen) {
      port.write(data + "\n", (err) => {
        if (err) console.error("❌ Error enviando al microbit:", err.message);
        else console.log("📤 Enviado al microbit:", data);
      });
    }
  });

  socket.on("disconnect", () => {
    console.log("❌ Cliente desconectado:", socket.id);
  });
});

server.listen(3000, () => console.log("🚀 Servidor corriendo en http://localhost:3000"));
```


Codigo Cliente Movil


Skecht


```
let socket;
let startY = null;

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  // 🔗 Conexión al túnel
  socket = io("https://3c2w808t-3000.use2.devtunnels.ms", {
    transports: ["websocket", "polling"]
  });

  socket.on("connect", () => {
    console.log("✅ Conectado al servidor con ID:", socket.id);
  });

  textAlign(CENTER);
  textSize(24);
}

function draw() {
  background(20);
  fill(255);
  text("⬆️ Desliza arriba = fuego\n⬇️ Desliza abajo = nubes", width / 2, height / 2);
}

function touchStarted() {
  startY = mouseY;
}

function touchEnded() {
  if (startY === null) return;
  let deltaY = mouseY - startY;

  if (deltaY > 50) {
    socket.emit("newElement", "nube");
    console.log("🌥️ Enviado: nube");
  } else if (deltaY < -50) {
    socket.emit("newElement", "fuego");
    console.log("🔥 Enviado: fuego");
  }

  startY = null;
}


```


Index.html


```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch.js" defer></script>
  </head>
  <body style="margin:0;overflow:hidden;background:#111;"></body>
</html>


```


Codigos Cliente Escritotio


Sketch.js


```
let song;
let fft;
let socket;
let started = false;
let visuals = [];

// 🎵 Carga la canción
function preload() {
  song = loadSound("KHEA - Del cielo al infierno.mp3");
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT();

  // 🔗 Conexión al servidor (usa tu DevTunnel)
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms/");

  // ✅ Escucha los mensajes del móvil
  socket.on("newElement", (data) => {
    console.log("📲 Elemento recibido del móvil:", data);
    crearVisual(data);
  });

  // ✅ Escucha los mensajes del micro:bit
  // ✅ Escucha los mensajes del micro:bit
socket.on("microbit", (data) => {
  console.log("💡 Señal cruda desde micro:bit:", data);

  const msg = (data || "").trim().toLowerCase();
  console.log("🧠 Señal procesada:", msg);

  if (msg.includes("angel")) {
    crearVisual("angel");
  } else if (msg.includes("demonio")) {
    crearVisual("demonio");
  } else if (msg.includes("fuego")) {
    crearVisual("fuego");
  } else if (msg.includes("nube")) {
    crearVisual("nube");
  } else {
    console.warn("⚠️ Mensaje desconocido del microbit:", msg);
  }
});


  // Pantalla inicial
  background(0);
  textAlign(CENTER);
  textSize(24);
  fill(255);
  text("Haz click para iniciar 'Cielo al Infierno'", width / 2, height / 2);
}

function mousePressed() {
  if (!started) {
    song.play();
    started = true;
  }
}

function draw() {
  if (!started) return;

  background(10, 25, 45);

  // 🎚️ Visual del sonido
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let amplitude = map(bass, 0, 255, 20, 150);

  noFill();
  stroke(255);
  strokeWeight(3);
  beginShape();
  for (let x = 0; x <= width; x += 10) {
    let y = height / 2 + sin(x * 0.02 + frameCount * 0.05) * amplitude;
    vertex(x, y);
  }
  endShape();

  // 🎨 Dibujar visuales activos
  for (let v of visuals) {
    v.y += v.velY; // movimiento vertical
    v.x += v.velX; // movimiento horizontal
    drawVisual(v);
  }

  // 🧹 Eliminar los que salen de pantalla
  visuals = visuals.filter((v) => v.y > -100 && v.y < height + 100);
}

// ✨ Crear visuales nuevos con animación
function crearVisual(tipo) {
  console.log("🌈 creando visual de tipo:", tipo);

  let v = {
    type: tipo,
    x: random(width),
    y: tipo === "nube" ? -50 : height + 50,
    size: random(60, 120),
    velY: tipo === "nube" || tipo === "angel" ? random(1, 2) : random(-3, -1),
    velX: random(-0.5, 0.5),
    life: 255,
  };
  visuals.push(v);
}

// 🧩 Dibujar cada visual según tipo
function drawVisual(v) {
  textAlign(CENTER);
  textSize(v.size);
  noStroke();
  fill(255, v.life);

  if (v.type === "nube") text("☁️", v.x, v.y);
  else if (v.type === "fuego") text("🔥", v.x, v.y);
  else if (v.type === "angel") text("😇", v.x, v.y);
  else if (v.type === "demonio") text("😈", v.x, v.y);

  v.life -= 2;
}
```


Index.html

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch.js" defer></script>
  </head>
  <body style="margin:0;overflow:hidden;background:black;"></body>
</html>

```



Codigo micro:bit

```
from microbit import *

while True:
    if button_a.was_pressed():
        print("angel")   # 🔁 Esto sí llega por USB
        display.show("A")
        sleep(300)
        display.clear()

    if button_b.was_pressed():
        print("demonio")  # 🔁 Esto sí llega por USB
        display.show("B")
        sleep(300)
        display.clear()

    sleep(100)

```
