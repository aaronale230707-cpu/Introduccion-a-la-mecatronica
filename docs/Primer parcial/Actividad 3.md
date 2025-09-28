---
Titulo: LED con botón en ESP32
Resumen: Práctica básica para leer un pulsador y encender un LED con ESP32 usando entradas y salidas digitales.
hide:
  - navigation
---

# LED con botón en ESP32

## Objetivo
Encender un LED cuando se presiona un botón, usando un pin de entrada para el pulsador y un pin de salida para el LED, con mensajes por puerto serie.

## Materiales
- ESP32 DOIT DEVKIT V1 y cable USB.
- LED rojo y resistencia limitadora (~220–330 Ω).
- Pulsador y resistencia de pull‑down (~10 kΩ) o uso de pull‑up interno.
- Protoboard y jumpers.

## Conexiones
1. LED: ánodo al GPIO 12 mediante la resistencia; cátodo a GND.
2. Botón: un lado a 3V3; el otro al GPIO 34 con resistencia de 10 kΩ a GND (pull‑down).  
   Alternativa: configurar INPUT_PULLUP y llevar el botón a GND.

## Código

```python
const int led = 12;
const int btn = 34;

void setup() {
  Serial.begin(115200);
  pinMode(led, OUTPUT);
  pinMode(btn, INPUT); // si usas pull‑up interno, cambia a INPUT_PULLUP
}

void loop() {
  int estado = digitalRead(btn);
  if (estado == 1) {
    digitalWrite(led, 1);
    Serial.println("on");
  } else {
    digitalWrite(led, 0);
    Serial.println("off");
  }
}
```

## Prueba y verificación
- Al presionar el botón, el LED enciende y el monitor serie muestra “on”; al soltar, “off”.
- Si hay falsos disparos: comprobar tierra común, resistencias, contactos del pulsador y considerar un pequeño delay o antirrebote por software.

## Evidencias
<img src="../recursos/imgs/montaje_btn_led.jpg" alt="Montaje en protoboard con LED y botón" width="420">

<img src="../recursos/imgs/sketch_btn_led.jpg" alt="Sketch de lectura digital" width="420">

<img src="../recursos/imgs/diagrama_btn_led.png" alt="Diagrama de conexiones" width="420">
