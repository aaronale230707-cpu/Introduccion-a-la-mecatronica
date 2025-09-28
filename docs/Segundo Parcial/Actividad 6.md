---
Titulo: Control de motor DC con ESP32 y L298N
Resumen: Documentación breve de práctica para controlar velocidad y dirección de un motor DC con ESP32, L298N y fuente DC de laboratorio.
hide:
  - navigation
---

# Control de velocidad con motor DC con ESP32 y L298N

## Objetivo
Controlar un motor DC variando velocidad mediante PWM y fijando dirección con dos pines digitales del ESP32, usando el L298N y una fuente DC con límite de corriente. 

## Descripción rápida
- El L298N es un puente H: IN1/IN2 definen el sentido y ENA recibe el PWM de velocidad. 
- La fuente mostró ~11.9 V y ~0.20 A durante la prueba del motor TT; el segundo canal quedó sin carga. 

## Materiales
- Fuente GW Instek GPE‑3323 (CC/CV, 2 canales).
- Módulo L298N (OUT1–OUT4, VIN 12V, GND, 5V, ENA/IN1/IN2). 
- ESP32 DOIT DEVKIT V1. [attached_file:4]  
- Motorreductor DC tipo TT, protoboard y jumpers. [attached_file:2]

## Conexiones
1. Fuente + → “12V” del L298N; fuente − → GND del L298N y GND del ESP32 (tierra común). 
2. Motor → OUT1 y OUT2 (canal A del L298N). 
3. IN1 → GPIO 25 (ESP32) e IN2 → GPIO 26 para dirección. 
4. ENA → GPIO 27 para PWM (1 kHz, 8 bits).  
5. Verificar polaridades y jumper “5V‑EN” según el módulo; mantener GND común siempre.

## Código 

```python
#define in1 25
#define in2 26
#define pwm 27

void setup() {
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  ledcAttach(pwm, 1000, 8); // 1 kHz, 8 bits
}

void loop() {
  // Acelera
  for (int i = 0; i <= 255; i++) {
    ledcWrite(pwm, i);
    digitalWrite(in1, 1);
    digitalWrite(in2, 0);
    delay(10);
  }
  // Desacelera
  for (int i = 255; i >= 0; i--) {
    ledcWrite(pwm, i);
    digitalWrite(in1, 1);
    digitalWrite(in2, 0);
    delay(10);
  }
}
```

## Parámetros y notas
- Usar ~12 V como entrada al L298N y ajustar límite de corriente para cubrir el pico de arranque del motor.  
- Si no gira: revisar GND común, estado de ENA, inversión de IN1/IN2 y límite de corriente de la fuente. 

## Evidencias
<img src="../recursos/imgs/fuente_gwinstek.jpg" alt="Canal activo 11.9 V, 0.20 A" width="420"> 

<img src="../recursos/imgs/montaje_breadboard.jpg" alt="Montaje ESP32 + L298N + motor TT" width="420"> 

<img src="../recursos/imgs/diagrama_l298n.png" alt="Esquema L298N–ESP32–motor" width="420"> 

<img src="../recursos/imgs/sketch_esp32_pwm.jpg" alt="Sketch PWM pines 25/26/27" width="420"> 

> Video opcional:  
> [Video en plataforma externa](https://tu-enlace-de-video.com) 
