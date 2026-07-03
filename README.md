# Midea M-Theri ESPHome Modbus

Integración modular para controlar y monitorizar una aerotermia **Midea M-Theri** desde **Home Assistant** usando **ESPHome + RS485 Modbus RTU**.

El objetivo es tener una integración local, sin nube, con control de calefacción, refrigeración, ACS, curva climática, modo silencioso, diagnóstico avanzado y sensor de presión hidráulica externo.

> Proyecto en desarrollo. Algunos registros de escritura se han probado en una instalación real, pero otros deben validarse en cada máquina antes de usarlos.

## Características

- ESP32 + ESPHome.
- RS485 Modbus RTU local.
- Sin nube.
- Modo Auto / Frío / Calor.
- ACS y ACS rápida.
- Consignas separadas para calefacción y refrigeración.
- ACS limitada a 60 °C.
- Curva climática zona 1.
- Modo silencioso y nivel silencioso.
- Modo ECO.
- Diagnóstico de compresor, bomba, ventilador e inverter.
- Temperaturas internas del circuito frigorífico.
- Energía consumida y energía producida.
- Potencia del módulo hidráulico.
- COP/EER calculado.
- Sensor de presión hidráulica externo por ADC.
- Proyecto separado por YAMLs modulares.

## Hardware

### Obligatorio

- ESP32.
- Conversor RS485, recomendado SP485 / MAX3485.
- Fuente estable para ESP32.
- Cableado RS485 hacia la Midea M-Theri.

### Opcional

- Sensor de presión analógico 0,5-4,25 V / 0-5 bar.
- Fuente 24 V para el sensor.
- Divisor resistivo 10 kΩ / 20 kΩ.
- Condensador de filtrado en GPIO34.

## Cableado RS485

```text
ESP32 GPIO17 TX2  -> DI / RXD módulo RS485
ESP32 GPIO16 RX2  -> RO / TXD módulo RS485
ESP32 GPIO4       -> DE y /RE unidos
ESP32 GND         -> GND módulo RS485

RS485 A           -> A / H1 / H2 según equipo
RS485 B           -> B / H2 / H1 según equipo
```

Si no comunica, invertir A y B.

## Sensor de presión hidráulica

```text
Sensor rojo   -> +24 V
Sensor negro  -> GND 24 V común con GND ESP32
Sensor azul   -> divisor resistivo -> GPIO34

Azul sensor -> 10 kΩ -> GPIO34 -> 20 kΩ -> GND
```

Archivo:

```text
midea/90_pressure.yaml
```

## Instalación

1. Copia `aerotermia.yaml` en:

```text
/config/esphome/aerotermia.yaml
```

2. Copia la carpeta completa `midea/` en:

```text
/config/esphome/midea/
```

3. Asegúrate de tener en `secrets.yaml`:

```yaml
wifi_ssid: "TU_WIFI"
wifi_password: "TU_PASSWORD"
```

4. Desde ESPHome:

```text
Validate -> Install
```

## Estructura

```text
aerotermia.yaml
midea/
  00_base.yaml
  10_modbus.yaml
  30_controls.yaml
  40_switches.yaml
  60_temperatures.yaml
  61_water.yaml
  62_compressor.yaml
  63_energy.yaml
  64_extra_diagnostics.yaml
  70_binary_sensors.yaml
  80_text_sensors.yaml
  90_pressure.yaml
  91_cop.yaml
  92_climate_curve.yaml
  99_raw_registers.yaml
docs/
  wiring.md
  registers.md
  homeassistant.md
  dashboard.yaml
```

## Funciones implementadas

### Control

- Modo de trabajo: Auto / Frío / Calor.
- Activación zona 1.
- ACS activada.
- ACS rápida.
- Curva climática zona 1.
- Modo silencioso.
- Nivel modo silencioso alto.
- Modo ECO.

### Consignas

- Consigna agua calefacción zona 1: 25-60 °C.
- Consigna agua refrigeración zona 1: 5-25 °C.
- Consigna ambiente.
- Consigna ACS: 20-60 °C.

### Modos de instalación

Zona 1 en calefacción y refrigeración:

- Fan coil.
- Radiador.
- Suelo radiante.

### Sensores principales

- Temperatura impulsión.
- Temperatura retorno.
- Temperatura exterior.
- Temperatura ACS.
- Frecuencia compresor.
- Frecuencia objetivo compresor.
- Caudal de agua.
- Potencia módulo hidráulico.
- Energía eléctrica consumida.
- Energía térmica producida.
- Horas compresor.
- Código de error actual.

### Diagnóstico adicional

- PMV / válvula electrónica.
- Temperatura condensador T3.
- T2 líquido.
- T2B gas.
- Ta ambiente.
- T1 / T1B.
- Bus DC.
- Temperatura módulo inverter.
- Curva climática calculada.

### Sensores calculados

- Delta T agua.
- Potencia térmica calculada.
- COP instantáneo.
- COP acumulado.
- Resumen de estado.

## Registros importantes

### ACS rápida

```text
Registro 0x07
1 = ON
2 = OFF
```

### Curva climática zona 1

```text
Registro 0x05
Bit 12
Máscara 0x1000
```

### Modo silencioso

```text
Registro 0x05
Bit 6
Máscara 0x40
```

### Nivel silencioso

```text
Registro 0x05
Bit 7
Máscara 0x80
```

## Roadmap

- Confirmar registro de modo purga.
- Dashboard Lovelace completo.
- FV / excedentes solares.
- Smart Grid real.
- Histórico diario/mensual de COP/EER.
- Tabla completa de códigos de error.
- Soporte para varias zonas.
- Integración de fan coils Midea por RS485.

## Advertencia

Modificar registros Modbus puede alterar parámetros de servicio de la aerotermia. Usa esta integración bajo tu responsabilidad. Antes de escribir registros desconocidos, prueba siempre en modo lectura.
