# Códigos de error

El sensor de texto **Error actual (texto)** convierte el registro `0x7C` (PLC 124) en el código y la descripción del fallo. Ese registro devuelve el **número de serie** del fallo en la tabla del manual de servicio de Midea M-Thermal (E0 = 1, E8 = 9, P1 = 21, F1 = 116), no el código de letras. Los códigos L0-L9 no tienen número de serie y no se pueden mostrar. El valor 0 se muestra como «Sin error» y cualquier número que no esté en la tabla como «Código desconocido (n)».

Los textos de la tabla se mantienen en [`esphome/midea/states/text_sensors.yaml`](../esphome/midea/states/text_sensors.yaml).

| Nº | Código y descripción |
|---:|---|
| 1 | E0 – Fallo de caudal de agua (E8 x3, reinicio manual) |
| 2 | E1 – Error de secuencia de fases |
| 3 | E2 – Comunicación placa hidrónica / interfaz de usuario |
| 4 | E3 – Sensor temperatura salida de agua final (T1) |
| 5 | E4 – Sensor temperatura depósito ACS (T5) |
| 6 | E5 – Sensor refrigerante salida intercambiador de aire (T3) |
| 7 | E6 – Sensor temperatura ambiente exterior (T4) |
| 8 | E7 – Sensor depósito de inercia superior (Tbt1) |
| 9 | E8 – Fallo de caudal de agua |
| 10 | E9 – Sensor tubo de aspiración (Th) |
| 11 | EA – Sensor tubo de descarga (Tp) |
| 12 | Eb – Sensor panel solar (Tsolar) |
| 13 | Ec – Sensor depósito de inercia inferior (Tbt2) |
| 14 | Ed – Sensor agua de entrada al intercambiador (Tw_in) |
| 15 | EE – Error EEPROM de la caja hidrónica |
| 20 | P0 – Protección presostato de baja |
| 21 | P1 – Protección presostato de alta |
| 23 | P3 – Protección de corriente del compresor |
| 24 | P4 – Protección temperatura de descarga |
| 25 | P5 – Diferencia excesiva de temperatura entrada/salida de agua |
| 26 | P6 – Protección del módulo inverter |
| 31 | Pb – Protección anticongelación del intercambiador de agua |
| 33 | Pd – Alta temperatura refrigerante en refrigeración |
| 38 | PP – Agua de entrada más caliente que la de salida |
| 39 | H0 – Comunicación unidad exterior / caja hidrónica |
| 40 | H1 – Comunicación unidad exterior / driver del inverter |
| 41 | H2 – Sensor refrigerante salida línea líquido (T2) |
| 42 | H3 – Sensor refrigerante entrada línea gas (T2B) |
| 43 | H4 – P6 repetido 3 veces en una hora |
| 44 | H5 – Sensor temperatura ambiente (Ta) |
| 45 | H6 – Error ventilador DC |
| 46 | H7 – Tensión del circuito principal anómala |
| 47 | H8 – Error sensor de presión |
| 48 | H9 – Sensor salida de agua circuito 2 (Tw2) |
| 49 | HA – Sensor salida de agua del intercambiador (Tw_out) |
| 50 | Hb – PP repetido 3 veces y Tw_out < 7 °C |
| 54 | HF – Error EEPROM del inverter |
| 55 | HH – Error ventilador DC repetido (10 veces en 120 min) |
| 57 | HP – Protección baja presión en refrigeración |
| 65 | C7 – Temperatura excesiva del módulo del inverter |
| 112 | bH – Error placa PED |
| 116 | F1 – Tensión del bus DC demasiado baja |

## Cómo se resetean

- **E8** (fallo de caudal) se rearma solo cuando el caudal vuelve a ser correcto.
- **E0** aparece tras tres E8 en 9 minutos y exige un reinicio manual: corta la alimentación de la unidad unos 60 segundos y restáurala.
- Antes de resetear cualquier fallo, revisa su causa (caudal, presión del circuito, purga de aire, filtros). Un reinicio sin corregirla solo repite el fallo.

Estado de la validación: la tabla está sin comprobar con un fallo real.
