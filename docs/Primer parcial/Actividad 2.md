---
Titulo: Blink en ESP32
Resumen: Práctica para encender y apagar un LED periódicamente con un ESP32 usando salidas digitales y delays.
hide:
  - navigation
---

# Blink en ESP32

## Objetivo
Generar un parpadeo de 1 segundo encendido y 1 segundo apagado en un LED controlado por un GPIO del ESP32.

## Materiales
- ESP32 DOIT DEVKIT V1.
- LED rojo y resistencia limitadora (~220–330 Ω).
- Protoboard, jumpers y cable USB.

## Conexiones
1. Ánodo del LED al GPIO 23 a través de la resistencia.  
2. Cátodo del LED a GND del ESP32.

## Código

```python
#define LED 23

void setup() {
  pinMode(LED, OUTPUT); // Configura el pin del LED como salida
}

void loop() {
  digitalWrite(LED, HIGH); // Enciende el LED
  delay(1000);             // Espera 1 segundo
  digitalWrite(LED, LOW);  // Apaga el LED
  delay(1000);             // Espera 1 segundo
}
```

## Prueba
- Cargar el sketch y observar el parpadeo continuo.  
- Si no parpadea: comprobar el pin elegido, polaridad del LED y continuidad de la resistencia.

## Evidencias
<img src="../recursos/imgs/blink_diagrama.png" alt="Diagrama de conexiones para Blink" width="560">
