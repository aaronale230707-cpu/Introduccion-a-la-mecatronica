---
Titulo: Control de LED por Bluetooth (ESP32)
Resumen: Práctica para recibir texto por Bluetooth Serial con ESP32 y encender/apagar un LED desde el teléfono.
hide:
  - navigation
---

# Control de LED por Bluetooth (ESP32)

## Objetivo
Conectar el ESP32 por Bluetooth clásico (SPP) a un teléfono y, al recibir “ON” u “OFF”, cambiar el estado de un LED, mostrando en el monitor serie lo recibido.

## Materiales
- ESP32 DOIT DEVKIT V1 e IDE de Arduino.
- LED y resistencia limitadora (~220–330 Ω).
- Protoboard y jumpers.
- App de terminal Bluetooth (por ejemplo, “Serial Bluetooth Terminal”).

## Conexiones
1. LED: ánodo a un GPIO (ej. 12 o 23) por medio de la resistencia; cátodo a GND.
2. USB para alimentar el ESP32 y usar el monitor serie.

## Código

```python
#include "BluetoothSerial.h"
BluetoothSerial SerialBT;
byte led = 12; // o 23

void setup() {
  Serial.begin(115200);
  SerialBT.begin("el tlacoyo"); // nombre visible del dispositivo
  pinMode(led, OUTPUT);
}

void loop() {
  if (SerialBT.available()) {
    String mensaje = SerialBT.readString();
    Serial.println("Recibido: " + mensaje);

    if (mensaje == "ON") {
      digitalWrite(led, 1);
      Serial.println("On");
    } else if (mensaje == "OFF") {
      digitalWrite(led, 0);
      Serial.println("Off");
    }
  }
  delay(1000);
}
```

## Prueba
- Emparejar el teléfono con el nombre del ESP32 y abrir la app de terminal.
- Enviar “ON” para encender y “OFF” para apagar; verificar en el monitor serie las cadenas recibidas.

## Notas rápidas
- Si no aparece el dispositivo, reiniciar el ESP32 y comprobar que el Bluetooth del teléfono esté activo.
- Para tolerar mayúsculas/minúsculas: usar mensaje.toUpperCase() antes de comparar.
- Evitar pines solo‑entrada para el LED (p. ej., 34–39).

## Evidencias
<img src="../recursos/imgs/bt_codigo_captura.png" alt="Sketch con BluetoothSerial y control de LED" width="420">
<img src="../recursos/imgs/bt_monitor_captura.jpg" alt="Monitor serie mostrando cadenas recibidas" width="420">
<img src="../recursos/imgs/bt_telefono_terminal.jpg" alt="Terminal Bluetooth en el teléfono controlando el LED" width="420">
