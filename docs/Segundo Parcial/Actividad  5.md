
---
title: Control de un motor DC con ESP32 y L298N
summary: Práctica para controlar un motor DC con ESP32 usando PWM (velocidad) y dos pines de dirección por medio del L298N.
hide:
  - navigation
---

# Control de un motor DC con ESP32 y L298N

## Objetivo
Variar la velocidad y el sentido de un motor DC con ESP32 y L298N alimentado desde fuente de laboratorio, dejando evidencia del cableado y el sketch. [attached_file:3]

## Conceptos clave
- Frecuencia: ciclos por segundo del PWM. [attached_file:4]  
- Duty: porcentaje en ALTO que fija la potencia media al motor. [attached_file:4]  
- Resolución: pasos del duty (2^bits). [attached_file:4]

## Materiales
- ESP32 con IDE de Arduino. [attached_file:1]  
- Módulo L298N (canal A: ENA, IN1, IN2; OUT1, OUT2). [attached_file:2]  
- Un motor DC tipo TT. [attached_file:3]  
- Fuente DC de laboratorio; protoboard y jumpers. [attached_file:3]

## Conexiones (un canal)
1. Fuente + → “12V” del L298N; Fuente − → GND del L298N y GND del ESP32 (tierra común). [attached_file:2]  
2. Motor → OUT1 y OUT2 del L298N (canal A). [attached_file:2]  
3. IN1 → GPIO 18, IN2 → GPIO 19; ENA (PWM) → GPIO 21 del ESP32. [attached_file:1]

## Código

```python
#define IN1 18
#define IN2 19
#define PWM 21

void setup() {
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  ledcAttach(PWM, 1000, 8); // 1 kHz, 8 bits
}

void loop() {
  // Adelante
  digitalWrite(IN1, 1);
  digitalWrite(IN2, 0);
  ledcWrite(PWM, 200);
  delay(4000);

  // Atrás
  digitalWrite(IN1, 0);
  digitalWrite(IN2, 1);
  ledcWrite(PWM, 200);
  delay(4000);

  // Alto
  ledcWrite(PWM, 0);
  delay(2000);
}
```
[attached_file:1]

## Verificación
- Ajustar la fuente y el límite de corriente; observar cambio de sentido y velocidad según duty. [attached_file:3]  
- Si no arranca: revisar GND común, jumper de habilitación ENA y polaridad de VIN. [attached_file:2]

## Evidencias
<img src="../recursos/imgs/ide_subida.jpg" alt="Carga del sketch" width="420"> [attached_file:1]

<img src="../recursos/imgs/diagrama_un_motor.png" alt="L298N con un motor y ESP32" width="420"> [attached_file:2]

<img src="../recursos/imgs/montaje_un_motor.jpg" alt="Montaje con fuente y motor" width="420"> [attached_file:3]

<img src="../recursos/imgs/pwm_conceptos.png" alt="Resumen PWM" width="420"> [attached_file:4]
