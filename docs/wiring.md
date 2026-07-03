# Wiring

## RS485

```text
ESP32 GPIO17 TX2  -> DI / RXD RS485
ESP32 GPIO16 RX2  -> RO / TXD RS485
ESP32 GPIO4       -> DE + /RE RS485
ESP32 GND         -> GND RS485

RS485 A           -> A/H1
RS485 B           -> B/H2
```

Si no comunica, invertir A y B.

## Sensor de presión

```text
Sensor rojo   -> +24 V
Sensor negro  -> GND 24 V
Sensor azul   -> divisor resistivo

Azul sensor -> 10 kΩ -> GPIO34 -> 20 kΩ -> GND
```

Recomendado:

```text
GPIO34 -> + condensador 47-100 µF
GND    -> - condensador
GPIO34 -> 100 nF -> GND
```
