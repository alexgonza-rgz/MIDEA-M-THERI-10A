<div align="center">

# Midea M-Theri Ultimate en ESPHome

### Control y monitorizaciÃ³n local mediante ESP32, RS485 y Modbus RTU

![Version](https://img.shields.io/badge/Version-v2.0.0-blue)
![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-00C853)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5)
![Modbus](https://img.shields.io/badge/Modbus-RTU-orange)
![License](https://img.shields.io/badge/License-GPL--3.0-red)

</div>

IntegraciÃ³n local para una aerotermia **Midea M-Theri Ultimate 10 A**. Un ESP32 conectado al bus RS485 permite leer estados y temperaturas, controlar las funciones principales y publicar las entidades en Home Assistant mediante ESPHome, sin depender de la nube de Midea.

La configuraciÃ³n incluida es la que estÃ¡ instalada y funcionando en la unidad usada para desarrollar el proyecto. Los registros de ingenierÃ­a y los controles todavÃ­a no validados estÃ¡n identificados como experimentales.

## Funciones incluidas

### Control

- Modo Auto, Frío y Calor.
- Activación independiente de climatización de zona 1 y ACS.
- Consigna activa de agua de zona 1.
- Consigna ambiente y consigna de ACS.
- Curva climática de zona 1.
- Modo ECO y modo silencioso.
- ACS rápida.
- Selección del tipo de emisor de zona 1.

### MonitorizaciÃ³n

- Temperaturas de impulsión, retorno, exterior y depósito de ACS.
- Caudal y presión del circuito de calefacción.
- Frecuencia del compresor y velocidad del ventilador exterior.
- Presiones y temperaturas del circuito frigorÃ­fico.
- Estados de bomba, válvula de ACS, resistencias, desescarche y alarma.
- Energí­a consumida y producida.
- Potencia tÃ©rmica calculada, COP instantáneo y COP acumulado.
- Registros RAW para diagnóstico.

## Estado de validaciÃ³n

| Área | Estado | Observaciones |
|---|---|---|
| ComunicaciÃ³n Modbus | En uso | 9600 8N1, esclavo 1, actualizaciÃ³n cada 10 s |
| Lecturas principales | En uso | Temperaturas, caudal, compresor, estados y ACS |
| ClimatizaciÃ³n zona 1 | En uso | Bit independiente del ACS; la automatizaciÃ³n debe actuar sobre su interruptor |
| Consignas | En uso | Agua zona 1, ambiente y ACS |
| Sensor de presiÃ³n | En uso | AlimentaciÃ³n 5 V, seÃ±al verde y calibraciÃ³n propia |
| Dashboard v1.3 | En uso | Control, EnergÃ­a, DiagnÃ³stico e IngenierÃ­a |
| Potencia elÃ©ctrica instantÃ¡nea | Experimental | Registro 0x93 pendiente de contrastar con medidor externo |
| Potencia del mÃ³dulo hidrÃ¡ulico | Pendiente de confirmar | Revisar la interpretaciÃ³n del registro 0x8C |
| Controles avanzados | Experimental | Smart Grid, purga, antilegionela y doble zona no implementados |

## Hardware

### Necesario

- ESP32 `esp32dev`.
- Transceptor RS485 compatible con lÃ³gica de 3,3 V, por ejemplo MAX3485.
- Fuente estable para el ESP32.
- Acceso a los terminales H1/H2 de la Midea.

### Sensor de presiÃ³n instalado

- Alimentación a 5 V.
- Cable rojo: +5 V.
- Cable negro: GND comÃºn con el ESP32.
- Cable verde: seÃ±al analógica.
- Divisor: 10 k ohms en serie y 20 k ohms a GND.
- Entrada ADC: GPIO34.

El sensor de presión es opcional. La calibración incluida corresponde a la instalación original y debe ajustarse si cambia el sensor, el divisor o el ESP32.

Consulta [Cableado](docs/wiring.md) para ver el conexionado completo.

## ComunicaciÃ³n RS485

| Parámetro | Valor |
|---|---|
| Protocolo | Modbus RTU |
| Velocidad | 9600 bit/s |
| Datos | 8 bits |
| Paridad | Ninguna |
| Parada | 1 bit |
| DirecciÃ³n | `0x01` |
| TX ESP32 | GPIO17 |
| RX ESP32 | GPIO16 |
| DE + /RE | GPIO4 |
| Intervalo de actualizaciÃ³n | 10 s |
| Espera entre comandos | 200 ms |

## Estructura

```text
MIDEA-M-THERI-10A/
â”œâ”€â”€ esphome/
â”‚   â”œâ”€â”€ aerotermia.yaml
â”‚   â””â”€â”€ midea/
â”‚       â”œâ”€â”€ core/
â”‚       â”œâ”€â”€ control/
â”‚       â”œâ”€â”€ sensors/
â”‚       â”œâ”€â”€ states/
â”‚       â”œâ”€â”€ calculated/
â”‚       â””â”€â”€ engineering/
â”œâ”€â”€ dashboards/
â”‚   â”œâ”€â”€ dashboard_principal_V1.2.yaml
â”‚   â””â”€â”€ dashboard_v1.3.yaml
â”œâ”€â”€ docs/
â”œâ”€â”€ examples/
â”œâ”€â”€ ROADMAP.md
â”œâ”€â”€ TODO.md
â””â”€â”€ VERIFY.md
```

`aerotermia.yaml` carga el resto de los archivos como paquetes. No es necesario unirlos en un Ãºnico YAML.

## InstalaciÃ³n rÃ¡pida

1. Copia la carpeta `esphome/midea/` a `/homeassistant/esphome/midea/`.
2. Copia `esphome/aerotermia.yaml` a `/homeassistant/esphome/aerotermia.yaml`.
3. AÃ±ade al `secrets.yaml` de ESPHome:

```yaml
wifi_ssid: "NOMBRE_WIFI"
wifi_password: "CONTRASEÃ‘A_WIFI"
```

4. Revisa GPIO, polaridad RS485 y cableado del sensor de presiÃ³n.
5. Valida `aerotermia.yaml` en ESPHome.
6. Instala el firmware y aÃ±ade el dispositivo descubierto a Home Assistant.

La instalaciÃ³n original tambiÃ©n utiliza cifrado de la API de ESPHome. Puede aÃ±adirse localmente sin publicar la clave:

```yaml
api:
  encryption:
    key: !secret aerotermia__encryption_key
```

Consulta la [guÃ­a de instalaciÃ³n](docs/installation.md) para el procedimiento completo.

## Dashboard

La versiÃ³n actual es [`dashboards/dashboard_v1.3.yaml`](dashboards/dashboard_v1.3.yaml) e incluye cuatro vistas:

- Control.
- EnergÃ­a.
- DiagnÃ³stico.
- IngenierÃ­a.

Los identificadores de entidad del dashboard corresponden a la instalaciÃ³n original y comienzan por `climatizacion_y_luces_midea_m_theri_ultimate_`. Si Home Assistant genera otros identificadores, deben sustituirse antes de importar el dashboard.

Consulta [Uso en Home Assistant](docs/homeassistant.md) y [Dashboards](dashboards/README.md).

## AutomatizaciÃ³n de demanda y ACS

La calefacciÃ³n de zona 1 y el ACS son bits independientes del registro `0x00`:

| FunciÃ³n | MÃ¡scara |
|---|---:|
| ClimatizaciÃ³n zona 1 | `0x0002` |
| ACS | `0x0004` |

Para detener la calefacciÃ³n sin apagar el ACS se debe apagar solamente la entidad **CalefacciÃ³n y refrigeraciÃ³n zona 1**. No debe utilizarse `climate.turn_off`, el modo HVAC `off` ni una escritura completa de valor `0`.

Consulta [Automatizaciones](docs/automations.md) para ver un ejemplo seguro basado en una demanda global `1/0`.

## DocumentaciÃ³n

- [InstalaciÃ³n](docs/installation.md)
- [Cableado](docs/wiring.md)
- [Mapa de registros implementados](docs/registers.md)
- [Home Assistant](docs/homeassistant.md)
- [Automatizaciones](docs/automations.md)
- [ResoluciÃ³n de problemas](docs/troubleshooting.md)
- [Tareas pendientes](TODO.md)
- [Roadmap](ROADMAP.md)
- [VerificaciÃ³n de la documentaciÃ³n](VERIFY.md)

## Seguridad

- Desconecta completamente la unidad interior y exterior antes de manipular el bus o la electrÃ³nica.
- No conectes directamente una seÃ±al superior a 3,3 V a un GPIO del ESP32.
- Conserva una copia de los valores originales antes de escribir registros de configuraciÃ³n.
- No publiques `secrets.yaml`, claves de API, contraseÃ±as Wi-Fi ni copias de seguridad de Home Assistant.
- Los registros marcados como experimentales deben probarse de forma controlada.

## Compatibilidad

| Equipo | Estado |
|---|---|
| Midea M-Theri Ultimate 10 A | Validado en la instalaciÃ³n original |
| ESP32 `esp32dev` con ESP-IDF | En uso |
| Home Assistant + ESPHome | En uso |
| Otros modelos Midea M-Thermal/M-Theri | No validados por este proyecto |

## Licencia

Este proyecto se distribuye bajo licencia [GPL-3.0](LICENSE).

El uso y la modificaciÃ³n de registros Modbus se realizan bajo responsabilidad de quien instala el proyecto.
