---
Titulo: LED con botón en ESP32
Resumen: Práctica básica para leer un pulsador y encender un LED con ESP32 usando entradas y salidas digitales.
hide:
  - navigation
---

# LED con botón en ESP32

## Objetivo
Encender un LED cuando se presiona un botón, empleando un pin de entrada para el pulsador y un pin de salida para el LED, con monitoreo por puerto serie. [attached_file:1]

## Materiales
- ESP32 DOIT DEVKIT V1 y cable USB. [attached_file:1]  
- LED rojo y resistencia limitadora (~220–330 Ω). [attached_file:3]  
- Pulsador y resistencia de pull‑down (~10 kΩ) o uso de pull‑up interno. [attached_file:3]  
- Protoboard y jumpers para el cableado. [attached_file:1]

## Conexiones
1. LED: ánodo al GPIO 12 mediante la resistencia; cátodo a GND. [attached_file:3]  
2. Botón: un lado a 3V3; el otro al GPIO 34 con resistencia de pull‑down a GND para leer “1” al presionar. [attached_file:3]  
3. Alternativa: usar pull‑up interno y cablear el botón a GND para leer “0” al presionar. [attached_file:2]

## Código

```python
const int led = 12;
const int btn = 34;

void setup() {
  Serial.begin(115200);
  pinMode(led, OUTPUT);
  pinMode(btn, INPUT); // con pull‑down externo; si usas pull‑up: INPUT_PULLUP
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
[attached_file:2]

## Prueba y verificación
- Al presionar el botón, el LED enciende y el monitor serie muestra “on”; al soltar, muestra “off”. [attached_file:1]  
- Si hay parpadeos: revisar tierras, continuidad de la resistencia, rebote del botón y considerar una pausa corta o filtrado por software. [attached_file:3]

## Evidencias
<img src="../recursos/imgs/montaje_btn_led.jpg" alt="Montaje en protoboard con LED y botón" width="420"> [attached_file:1]

<img src="../recursos/imgs/sketch_btn_led.jpg" alt="Sketch de lectura digital" width="420"> [attached_file:2]

<img src="../recursos/imgs/diagrama_btn_led.png" alt="Diagrama de conexiones" width="420"> [attached_file:3]
