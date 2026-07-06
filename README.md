<div align="center">

# 🔥 Midea M-Theri ESPHome Modbus

### Integración completa para Home Assistant mediante ESPHome + Modbus RTU

Control local de aerotermias **Midea M-Theri** mediante **ESP32**, sin depender de la nube.

![Version](https://img.shields.io/badge/Version-v1.2.0-blue)
![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-00C853)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5)
![Modbus](https://img.shields.io/badge/Modbus-RTU-orange)
![License](https://img.shields.io/badge/License-GPL--3.0-red)

---

**Control · Monitorización · Diagnóstico · Ingeniería**

</div>

---

# 📖 Descripción

Esta integración permite controlar y monitorizar una **Midea M-Theri** directamente desde **Home Assistant** mediante **ESPHome + RS485 Modbus RTU**, sin utilizar la nube del fabricante.

El proyecto está desarrollado con una arquitectura modular para facilitar su mantenimiento y ampliación, incluyendo sensores calculados, registros de ingeniería y funciones avanzadas.

---

# ✨ Características

## 🎛️ Control

- Auto
- Calefacción
- Refrigeración
- ACS
- ACS rápida
- Curva climática
- ECO
- Silent Mode
- Silent Level

---

## 🌡️ Consignas

- Consigna calefacción
- Consigna refrigeración
- Consigna ACS
- Consigna ambiente

---

## 💧 Circuito hidráulico

- Temperatura de impulsión
- Temperatura de retorno
- Delta T
- Caudal
- Presión hidráulica
- Potencia térmica

---

## ❄️ Circuito frigorífico

- Frecuencia del compresor
- Frecuencia objetivo
- Apertura PMV
- Velocidad del ventilador
- Temperatura de descarga
- Temperatura condensador (T3)
- Temperatura T2 líquido
- Temperatura T2B gas
- Temperatura ambiente (Ta)

---

## ⚡ Energía

- Potencia eléctrica
- Potencia hidráulica
- Energía consumida
- Energía producida
- COP instantáneo
- COP acumulado

---

## 🛠️ Diagnóstico

- Estado completo
- Código de error
- Horas del compresor
- Registros RAW
- Resumen de funcionamiento
- Sensores internos de ingeniería

---

# 🖥️ Hardware

## Obligatorio

- ESP32
- Conversor RS485 (MAX3485 / SP485 recomendado)
- Fuente de alimentación estable

## Opcional

- Sensor de presión 0.5–4.5 V
- Divisor resistivo 10 kΩ / 20 kΩ
- Condensador de filtrado

---

# 🔌 Instalación

Copiar el contenido de la carpeta:

```text
esphome/
```

dentro de:

```text
/config/esphome/
```

quedando:

```text
/config/esphome/
│
├── aerotermia.yaml
│
└── midea/
```

Después únicamente:

```text
Validate

↓

Install
```

---

# 📂 Estructura del proyecto

```text
MIDEA-M-THERI/
│
├── README.md
├── LICENSE
├── ROADMAP.md
├── TODO.md
├── .gitignore
│
├── esphome/
│   ├── aerotermia.yaml
│   └── midea/
│       ├── core/
│       ├── control/
│       ├── sensors/
│       ├── states/
│       ├── calculated/
│       └── engineering/
│
├── dashboards/
│
├── docs/
│
├── images/
│
├── examples/
│
├── scripts/
│
└── tools/
```

---

# 📊 Dashboard

El proyecto incorpora dashboards Lovelace independientes.

Actualmente disponibles:

- 🏠 Control
- 📈 Diagnóstico

Próximamente:

- 🔧 Ingeniería
- ⚙️ Servicio

---

# 📚 Documentación

Toda la documentación técnica se encuentra en:

```text
docs/
```

Incluye:

- Instalación
- Cableado
- Registros Modbus
- Home Assistant
- Dashboard
- Resolución de problemas

---

# 🔧 Compatibilidad

Actualmente validado con:

| Equipo | Estado |
|---------|:------:|
| Midea M-Theri Ultimate 10 kW | ✅ |
| ESP32 | ✅ |
| ESPHome | ✅ |
| Home Assistant | ✅ |

Otros modelos deberán validarse.

---

# 🚀 Roadmap

## ✅ v1.2

- Arquitectura modular
- Reorganización del proyecto
- Primera versión pública estable

## 🔄 v1.3

- Dashboard profesional
- Tarjetas condicionales
- Gráficos avanzados
- Mejoras visuales

## ⏳ v1.4

- Smart Grid
- Integración fotovoltaica
- Automatizaciones energéticas

## ⏳ v1.5

- Fan Coils Midea
- Soporte para doble zona

## 🎯 v2.0

- Integración completamente documentada
- Compatibilidad ampliada
- API estable

---

# 🤝 Contribuciones

Las contribuciones son bienvenidas.

Antes de abrir un Pull Request consulta:

- `ROADMAP.md`
- `TODO.md`

---

# 📄 Licencia

Este proyecto se distribuye bajo licencia **GPL-3.0**.

---

# ⚠️ Aviso

Modificar registros Modbus puede alterar parámetros internos de la aerotermia.

Todos los registros de escritura deben validarse previamente antes de utilizarlos.

El uso de esta integración es responsabilidad del usuario.
