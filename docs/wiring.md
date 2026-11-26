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

Sensor analógico de 0-5 bar, salida de 0,5-4,25 V, alimentado a 24 V.

```text
Sensor rojo   -> +24 V
Sensor negro  -> GND de 24 V (unido al GND del ESP32)
Sensor azul   -> 10 kΩ -> GPIO34 -> 20 kΩ -> GND
```

Con el divisor, 4,25 V llegan al ADC como unos 2,83 V. Por debajo de 0,2 V en la entrada se considera sensor desconectado. La calibración de `calculated/pressure.yaml` es de esta instalación; repítela si cambias el sensor o el divisor.

Recomendado:

```text
GPIO34 -> + condensador 47-100 µF
GND    -> - condensador
GPIO34 -> 100 nF -> GND
```
