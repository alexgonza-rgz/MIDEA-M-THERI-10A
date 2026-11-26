<div align="center">

# Midea M-Theri Ultimate en ESPHome

### Control y monitorización local mediante ESP32, RS485 y Modbus RTU

![Version](https://img.shields.io/badge/Version-v2.0.1-blue)
![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-00C853)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5)
![Modbus](https://img.shields.io/badge/Modbus-RTU-orange)
![License](https://img.shields.io/badge/License-GPL--3.0-red)

</div>

Integración local para una aerotermia **Midea M-Theri Ultimate 10 A**. Un ESP32 conectado al bus RS485 lee estados, temperaturas y presiones, controla las funciones principales y publica las entidades en Home Assistant mediante ESPHome, sin depender de la nube de Midea.

La configuración incluida es **la que está instalada y funcionando** en la unidad usada para desarrollar el proyecto (última sincronización: 26 de noviembre de 2026). Lo que todavía no está validado figura como pendiente o experimental en [Estado de validación](#estado-de-validación) y en [TODO](TODO.md).

## Instalación real

<p align="center">
  <img src="docs/images/PCB%20prototipo%20ESPHOME.jpeg" alt="ESP32 con el módulo RS485 montado junto a la unidad" height="320">
  <img src="docs/images/sensor%20de%20presion%20unidad%20interior.jpeg" alt="Sensor de presión instalado en un racor de latón de la unidad interior" height="320">
  <img src="docs/images/cableado%20pantalla%20unidad%20interior.jpeg" alt="Conexión al bus H1/H2 en la placa de la pantalla de la unidad interior" height="320">
</p>

De izquierda a derecha: ESP32 en placa de prototipos junto a la unidad, sensor de presión en el circuito de calefacción y conexión al bus H1/H2 en la placa de la pantalla.

## Funciones incluidas

### Control

- Modo de trabajo: Auto, Frío y Calor.
- Activación independiente de climatización de zona 1 y de ACS.
- Consigna de agua de zona 1 (5-65 °C; en Frío se limita a 5-25 °C y en Calor a 35-65 °C).
- Consigna ambiente (17-30 °C) y consigna de ACS (20-60 °C).
- Curva climática de zona 1: activación y selección de curva de calefacción y de refrigeración (0-9).
- Modo ECO, modo silencioso, nivel de silencioso alto y nivel modo silencioso (0-2).
- ACS rápida.
- Tipo de emisor de zona 1 para calefacción y para refrigeración (fancoil, radiador o suelo radiante).
- Botón para reiniciar el ESP32.

### Monitorización

- Temperaturas de impulsión, retorno, exterior, descarga del compresor y depósito de ACS.
- Temperaturas del circuito frigorífico (T1, T1B, T2, T2B, T3, Ta) y del módulo inverter.
- Caudal de agua y presión del circuito de calefacción en bar.
- Frecuencia real y objetivo del compresor, velocidad del ventilador exterior, apertura de la válvula PMV y horas de compresor.
- Presiones alta y baja del refrigerante en kPa.
- Intensidad y tensión de la unidad exterior, y corriente y tensión del bus DC.
- Estados de compresor, bomba interna y exterior, válvula de ACS, resistencias IBH1 y TBH, desescarche, retorno de aceite, curva climática, ACS rápida y alarma.
- Energía eléctrica consumida y energía térmica producida.

### Calculados

- ΔT del agua.
- Potencia eléctrica estimada (tensión × intensidad de la unidad exterior, más la resistencia de apoyo IBH1 cuando está activa).
- Potencia de la resistencia de apoyo estimada (3 kW fijos cuando IBH1 está activa; ajustable con `resistencia_apoyo_kw` en `calculated/cop.yaml`).
- Potencia térmica calculada a partir de caudal y ΔT, en calefacción, refrigeración y ACS.
- COP instantáneo (media de 2 minutos), que incluye la resistencia de apoyo, y COP acumulado, que solo recoge el compresor porque usa los contadores del equipo.

### Texto, alarmas y diagnóstico

- **Estado real**: Apagada, Desescarche, Retorno de aceite, ACS, Frío, Calor o En espera.
- **Resumen aerotermia**: una línea con estado, ida, retorno, ACS, compresor, caudal, COP y presión.
- **Error actual (texto)**: convierte el código numérico de fallo en su código y descripción (por ejemplo, `E0 – Fallo de caudal de agua`). Consulta [Códigos de error](docs/errores.md).
- Avisos de presión del circuito de calefacción: baja por debajo de 0,8 bar y alta por encima de 1,8 bar, porque la válvula de seguridad abre a 2 bar.
- Diagnóstico del ESP32: tiempo activo, señal Wi-Fi, memoria libre, fragmentación, tiempo de bucle y motivo del último reinicio.

## Estado de validación

| Área | Estado | Observaciones |
|---|---|---|
| Comunicación Modbus | En uso | 9600 8N1, esclavo 1, sondeo cada 10 s. Energías, horas de compresor y curvas se leen cada 60 s |
| Lecturas principales | En uso | Temperaturas, caudal, compresor, estados y ACS |
| Climatización zona 1 | En uso | Bit independiente del ACS; la automatización debe actuar sobre su interruptor |
| Consignas | En uso | Agua zona 1, ambiente y ACS |
| Sensor de presión | En uso | Calibrado con cuatro puntos frente a un manómetro de 0-6 bar el 01/11/2026; error máximo de 0,06 bar |
| Potencia eléctrica | En uso (estimada) | Tensión × intensidad. Contrastada con un medidor externo el 02/11/2026: queda unos 0,15 kW por debajo, con ±10 % |
| COP | En uso | Depende de la potencia eléctrica estimada. El instantáneo incluye la resistencia IBH1; el acumulado y los COP diario y mensual de HA solo recogen el compresor |
| Resistencia de apoyo IBH1 | En uso (estimada) | Entra cuando el compresor se para (por ejemplo, al acabar un ciclo de ACS) y consume unos 3 kW, medidos con el Deye el 22/11/2026. Ni los contadores del equipo ni la tensión × intensidad la cuentan |
| Código de error en texto | Implementado | Tabla del manual de servicio de Midea. Falta comprobarlo con un fallo real |
| Dashboard v1.3 | En uso | Control, Energía, Diagnóstico e Ingeniería |
| Potencia del módulo hidráulico | En uso (contraste) | El registro 0x8C (kW ×0,01) da valores reales con el compresor en marcha, del orden de la potencia térmica calculada, y 0 con la máquina parada. Al final de un ciclo reacciona con algo de retraso. Todavía no se usa en el COP |
| Registros 0x93 y 0x94-0x9B | Retirados | 0x93 no da valores reales y 0x94-0x9B responden con excepción Modbus 2 |
| Registros 0x12, 0x13, 0x16 y 0x17 | Retirados | Excepción Modbus 2 («dirección no válida») en esta unidad |
| Controles avanzados | No implementados | Smart Grid, purga, antilegionela, vacaciones y zona 2 |

El sensor «Presión tensión ADC cruda (temporal)» se conserva solo para recalibrar y debe retirarse cuando termine la calibración.

## Hardware

### Necesario

- ESP32 `esp32dev`.
- Transceptor RS485 compatible con lógica de 3,3 V, por ejemplo MAX3485.
- Fuente estable para el ESP32.
- Acceso a los terminales H1/H2 de la Midea.

### Sensor de presión (opcional)

- Sensor analógico de 0-5 bar con salida de 0,5-4,25 V y alimentación de 8,5-30 V (aquí, 24 V).
- Cable rojo: +24 V.
- Cable negro: GND de la fuente de 24 V y GND común con el ESP32.
- Cable azul: señal, a través de un divisor de 10 kΩ en serie y 20 kΩ a GND.
- Entrada ADC: GPIO34, con atenuación de 12 dB.
- Una lectura por debajo de 0,2 V se trata como sensor desconectado y se publica «sin dato», no 0 bar.

La calibración incluida corresponde a esta instalación y debe repetirse si cambia el sensor, el divisor o el ESP32. Consulta [Cableado](docs/wiring.md).

## Comunicación RS485

| Parámetro | Valor |
|---|---|
| Protocolo | Modbus RTU |
| Velocidad | 9600 bit/s |
| Datos | 8 bits |
| Paridad | Ninguna |
| Parada | 1 bit |
| Dirección | `0x01` |
| TX ESP32 | GPIO17 |
| RX ESP32 | GPIO16 |
| DE + /RE | GPIO4 |
| Intervalo de actualización | 10 s |
| Espera entre comandos | 200 ms (`send_wait_time` y `turnaround_time`) |

## Estructura

```text
MIDEA-M-THERI-10A/
├── esphome/
│   ├── aerotermia.yaml
│   └── midea/
│       ├── core/            base del ESP32 y Modbus
│       ├── control/         selectores, consignas e interruptores
│       ├── sensors/         temperaturas, hidráulica, compresor, energía y diagnóstico
│       ├── states/          sensores binarios y de texto
│       ├── calculated/      presión, COP y curva climática
│       └── engineering/     registros internos y código de error
├── dashboards/              dashboard_v1.3.yaml (actual) y dashboard_principal_V1.2.yaml
├── docs/                    cableado, registros, errores, Home Assistant e imágenes
├── examples/
├── ROADMAP.md
├── TODO.md
└── VERIFY.md
```

`aerotermia.yaml` carga el resto de los archivos como paquetes y aplica ajustes con `!extend` (aviso de presión alta a 1,8 bar y lectura más espaciada de los datos lentos). No es necesario unirlos en un único YAML.

## Instalación rápida

1. Copia la carpeta `esphome/midea/` a la carpeta `esphome/` de tu Home Assistant (la que usa el add-on ESPHome).
2. Copia `esphome/aerotermia.yaml` a esa misma carpeta.
3. Añade al `secrets.yaml` de ESPHome estos valores:

```yaml
wifi_ssid: "NOMBRE_WIFI"
wifi_password: "CONTRASEÑA_WIFI"
ota_password: "CONTRASEÑA_OTA"
fallback_password: "CONTRASEÑA_PUNTO_DE_ACCESO"
aerotermia__encryption_key: "CLAVE_API_BASE64_DE_32_BYTES"
```

4. Revisa GPIO, polaridad RS485 y cableado del sensor de presión.
5. Valida `aerotermia.yaml` en ESPHome.
6. Instala el firmware y añade el dispositivo descubierto a Home Assistant.

El proyecto se ha probado con ESPHome 2026.10.2 y el framework ESP-IDF.

### Seguridad del firmware

- La API de ESPHome va cifrada.
- La actualización OTA exige contraseña (`ota_password`).
- El panel web del ESP32 (puerto 80) pide usuario `admin` y la misma contraseña OTA.
- Si no hay Wi-Fi, el ESP32 crea el punto de acceso `Aerotermia-Setup`, protegido con `fallback_password`.

## Dashboard

La versión actual es [`dashboards/dashboard_v1.3.yaml`](dashboards/dashboard_v1.3.yaml) e incluye cuatro vistas:

- Control.
- Energía.
- Diagnóstico.
- Ingeniería.

Los identificadores de entidad del dashboard corresponden a la instalación original y comienzan por `climatizacion_y_luces_midea_m_theri_ultimate_`. Si Home Assistant genera otros identificadores, deben sustituirse antes de importar el dashboard.

Las capturas de `docs/images/dashboard_resumen.png` y `docs/images/dashboard_diagnostico.png` son de una versión anterior: todavía muestran los registros RAW R148-R155, ya retirados.

Consulta [Uso en Home Assistant](docs/homeassistant.md) y [Dashboards](dashboards/README.md).

## Automatización de demanda y ACS

La calefacción de zona 1 y el ACS son bits independientes del registro `0x00`:

| Función | Máscara |
|---|---:|
| Climatización zona 1 | `0x0002` |
| ACS | `0x0004` |

Para detener la calefacción sin apagar el ACS se debe apagar solamente la entidad **Calefacción y refrigeración zona 1**. No debe utilizarse `climate.turn_off`, el modo HVAC `off` ni una escritura completa de valor `0`.

Los interruptores no publican un estado falso antes de leer Modbus y no escriben sobre registros compartidos hasta haberlos leído.

## Documentación

- [Códigos de error y cómo se resetean](docs/errores.md)
- [Cableado](docs/wiring.md)
- [Mapa de registros Modbus](docs/registers.md)
- [Home Assistant](docs/homeassistant.md)
- [Dashboards](dashboards/README.md)
- [Tareas pendientes](TODO.md)
- [Roadmap](ROADMAP.md)
- [Verificación de la documentación](VERIFY.md)

## Seguridad

- Desconecta completamente la unidad interior y exterior antes de manipular el bus o la electrónica.
- No conectes directamente una señal superior a 3,3 V a un GPIO del ESP32.
- Conserva una copia de los valores originales antes de escribir registros de configuración.
- No publiques `secrets.yaml`, claves de API, contraseñas Wi-Fi ni copias de seguridad de Home Assistant.
- Los registros marcados como experimentales deben probarse de forma controlada.
- No resetees un error sin haber comprobado antes su causa.

## Compatibilidad

| Equipo | Estado |
|---|---|
| Midea M-Theri Ultimate 10 A | Validado en la instalación original |
| ESP32 `esp32dev` con ESP-IDF | En uso |
| Home Assistant + ESPHome | En uso |
| Otros modelos Midea M-Thermal/M-Theri | No validados por este proyecto |

## Licencia

Este proyecto se distribuye bajo licencia [GPL-3.0](LICENSE).

El uso y la modificación de registros Modbus se realizan bajo responsabilidad de quien instala el proyecto.
