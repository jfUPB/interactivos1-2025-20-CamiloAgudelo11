# Unidad 2

## 🔎 Fase: Set + Seek


### Actividad 01

Describe detalladamente cómo funciona este ejemplo.

Se crean dos luces en el microbit que parpadean, uno prende y apaga cada 1 segundo y el otro cada 0.5 segundos.

¿Cuáles son los estados en el programa?

Tiene 2 estados.

1. Init: Cuando el pixel se enciende por primera vez

2. WaitTimeout: Cuando espera el tiempo pase para cambiar la luz.

¿Cuáles son los eventos/inputs en el programa?

El unico evento que se puede evidenciar es el paso del tiempo para que el programa se ejecute, ya que no hay botones.

¿Cuáles son las acciones en el programa?

1. Encender y apagar la pixel.

2. Contar el tiempo que transcurre.

3. Cambiar el brillo del pixel.

### Actividad 02

Escribe el código que soluciona este problema en tu bitácora.

```Ph
from microbit import *
import utime


RED = "RED"
YELLOW = "YELLOW"
GREEN = "GREEN"


led_positions = {
    RED: (0, 0),      
    YELLOW: (1, 0),  
    GREEN: (2, 0)    
}


intervals = {
    RED: 3,
    YELLOW: 1,
    GREEN: 3
}


current_state = RED
start_time = utime.ticks_ms()


def turn_on(state):
    display.clear()
    x, y = led_positions[state]
    display.set_pixel(x, y, 9)


turn_on(current_state)


while True:
    now = utime.ticks_ms()
    elapsed = utime.ticks_diff(now, start_time) / 1000  

  
    if elapsed >= intervals[current_state]:
      
        if current_state == RED:
            current_state = GREEN
        elif current_state == GREEN:
            current_state = YELLOW
        elif current_state == YELLOW:
            current_state = RED

        
        turn_on(current_state)
        start_time = utime.ticks_ms()

    sleep(100)
```

Identifica los estados, eventos y acciones en tu código.

Estados: Green, Red y Yellow

Eventos: Cuando se da el cumplimiento del tiempo en un estado.

Acciones: Apagar todos los led, encender led y cambiar al siguiente color 

### Actividad 03

Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.

Esto significa que el programa hacer distintas acciones al mismo tiempo, ya que el programa sigue comprobando constantemente distintas funciones leer eventos del boton mientras se mide el paso del tiempo.


Identifica los estados, eventos y acciones en el programa.

Estados: STATE_INIT, STATE_HAPPY, STATE_SMILE, STATE_SAD

Eventos: Presionar el boton A y el paso del tiempo

Acciones: Mostrar imagen y cambiar estado


Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.

Vector de Prueba 1

- Condición Inicial: current_state = STATE_HAPPY, tiempo = 0 ms
- Evento: Se presiona el botón A
- Estado: STATE_SAD
- Acción: Se muestra la imagen Image.SAD, se reinicia el tiempo, interval = SAD_INTERVAL
- Resultado Obtenido: Coincide con lo esperado

 Vector de Prueba 2

- Condición Inicial: current_state = STATE_SMILE, botón A no se presiona y pasan más de 1 segundo
- Evento: Expira SMILE_INTERVAL (1000 ms)
- Estado Esperado: STATE_SAD
- Acción Esperada: Se muestra Image.SAD, nuevo intervalo SAD_INTERVAL
- Resultado Obtenido: El sistema muestra SAD y cambia de estado

 Vector de Prueba 3

- Condición Inicial: current_state = STATE_SAD, botón A presionado
- Evento: Se presiona el botón A antes de que termine SAD_INTERVAL
- Estado: STATE_SMILE
- Acción: Se muestra Image.SMILE, intervalo se reinicia
- Resultado Obtenido:  El sistema cambia correctamente a SMILE







