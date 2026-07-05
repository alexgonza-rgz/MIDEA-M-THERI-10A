# 🚀 ROADMAP

> **Objetivo del proyecto**
>
> Desarrollar la integración **ESPHome Modbus RTU** más completa para aerotermias Midea, proporcionando control total, monitorización avanzada, herramientas de ingeniería y documentación abierta del protocolo Modbus.

---

# 📌 Estado del proyecto

## Versión actual

### ✔ Funciones implementadas

### Comunicación

- RS485 Modbus RTU
- ESPHome
- Home Assistant
- Arquitectura modular YAML

### Control

- Encendido / Apagado
- Auto
- Calefacción
- Refrigeración
- ACS
- ACS rápida
- Curva climática
- Modo ECO
- Modo silencioso
- Nivel silencioso

### Consignas

- Agua calefacción
- Agua refrigeración
- ACS
- Ambiente

### Diagnóstico

- Temperaturas internas
- Compresor
- Bomba
- Ventilador
- PMV
- Bus DC
- Potencias
- Energías
- Estados
- Alarmas

### Sensores propios

- Presión hidráulica externa
- COP
- Potencia térmica

---

# 🟢 v1.1 — Estabilidad

Objetivo:
Conseguir una integración totalmente estable.

## Validación

- [ ] Validar ACS rápida
- [ ] Validar Curva climática
- [ ] Validar Silent Level
- [ ] Validar ECO
- [ ] Validar registros de escritura
- [ ] Revisar límites de temperatura
- [ ] Revisar escalas
- [ ] Revisar filtros

## Código

- [ ] Optimización
- [ ] Comentarios
- [ ] Limpieza
- [ ] Eliminación de código duplicado

---

# 🔵 v1.2 — Dashboard profesional

Objetivo:
Crear un dashboard comparable al controlador oficial.

## Vista usuario

- [ ] Estado
- [ ] Consignas
- [ ] ACS
- [ ] Presión
- [ ] COP
- [ ] Potencia

## Vista diagnóstico

- [ ] Temperaturas
- [ ] Compresor
- [ ] Ventilador
- [ ] Bomba
- [ ] PMV

## Vista ingeniería

- [ ] Registros RAW
- [ ] Estados internos
- [ ] Bits

## Vista SAT

- [ ] Parámetros
- [ ] Alarmas
- [ ] Servicio

---

# 🟣 v1.3 — Ingeniería

Objetivo:
Facilitar el descubrimiento de registros.

## Register Explorer

- [ ] Snapshot
- [ ] Snapshot Diff
- [ ] Exportación
- [ ] Comparación

## Register Diff

- [ ] Detectar registros modificados
- [ ] Detectar bits modificados
- [ ] Detectar bytes modificados

## Register Logger

- [ ] Registro automático
- [ ] Histórico
- [ ] Exportación

---

# 🟠 v1.4 — Descubrimiento de registros

## Confirmar

- [ ] Purga
- [ ] Antilegionela
- [ ] Smart Grid
- [ ] Holiday
- [ ] Solar
- [ ] Doble zona

## Documentar

- [ ] Todos los bits
- [ ] Todas las escalas
- [ ] Todos los estados

---

# 🔴 v1.5 — Diagnóstico

## Estados

- [ ] Desescarche
- [ ] Protección
- [ ] Alarmas
- [ ] Ventilador
- [ ] Compresor
- [ ] Bomba
- [ ] Resistencia

## Errores

- [ ] Tabla completa
- [ ] Traducción
- [ ] Soluciones

---

# 🟡 v1.6 — Energía

## COP

- [ ] Instantáneo
- [ ] Diario
- [ ] Mensual
- [ ] Anual

## EER

- [ ] Instantáneo
- [ ] Diario
- [ ] Mensual

## Energías

- [ ] Consumida
- [ ] Generada
- [ ] Balance

---

# 🟢 v1.7 — Fotovoltaica

## Excedentes

- [ ] Forecast.Solar
- [ ] Smart Grid
- [ ] ACS automática
- [ ] Curva dinámica
- [ ] Consigna dinámica

## Baterías

- [ ] Integración
- [ ] Prioridades

---

# 🔵 v1.8 — Automatizaciones

## Home Assistant

- [ ] Baja presión
- [ ] Fuga
- [ ] ACS inteligente
- [ ] Tarifa eléctrica
- [ ] Predicción meteorológica
- [ ] Modo vacaciones

---

# 🟣 v2.0 — Base de datos Modbus

## Base de datos

Cada registro contendrá:

- Dirección
- Nombre
- Unidad
- Escala
- Tipo
- Bits
- Lectura
- Escritura
- Estado
- Modelos compatibles

---

## Registros

- [ ] 100% documentados
- [ ] Bits documentados
- [ ] Escalas documentadas

---

# 🔴 v2.5 — Fan Coils

## Compatibilidad

- [ ] KJRP-75A/BK-E
- [ ] Consola
- [ ] Cassette
- [ ] Conductos

## Funciones

- [ ] Temperatura
- [ ] Consigna
- [ ] Ventilador
- [ ] Alarmas

---

# 🟠 v3.0 — Ecosistema Midea

## Compatibilidad

### Aerotermias

- [ ] M-Theri
- [ ] M Thermal
- [ ] Arctic
- [ ] Nature

### Fan Coils

- [ ] Todos

### Recuperadores

- [ ] HRV
- [ ] ERV

### Enfriadoras

- [ ] Air Cooled
- [ ] Water Cooled

### VRF

- [ ] V4+
- [ ] V6

---

# 🚀 v4.0 — Midea Universal Modbus Toolkit

Objetivo:
Crear una plataforma de ingeniería para cualquier equipo Midea.

## Register Explorer

- [ ] Escaneo automático
- [ ] Baudrate automático
- [ ] Dirección automática
- [ ] Snapshot
- [ ] Snapshot Diff

## Register Database

- [ ] Base de datos abierta

## YAML Generator

Generar automáticamente:

- sensor
- switch
- number
- select
- binary_sensor
- text_sensor

## Documentation Generator

Generar automáticamente:

- registers.md
- README
- tablas

---

# 🌐 v5.0 — Plataforma Web

## Aplicación

- [ ] Escaneo USB-RS485
- [ ] Detección automática
- [ ] Comparación
- [ ] Exportación
- [ ] Generación ESPHome

---

# 🏠 v6.0 — Home Assistant Add-on

- [ ] Descubrimiento automático
- [ ] OTA
- [ ] Diagnóstico
- [ ] Herramientas SAT

---

# 📚 Documentación

## Completar

- [ ] README
- [ ] Registers
- [ ] Wiring
- [ ] Dashboard
- [ ] FAQ
- [ ] Troubleshooting

---

# 🤝 Comunidad

Objetivos

- Crear la mayor base de datos abierta de registros Modbus Midea.
- Facilitar la integración de nuevos modelos.
- Aceptar contribuciones.
- Publicar documentación técnica.
- Compartir dashboards.
- Compartir automatizaciones.

---

# 🎯 Objetivo final

Convertir este proyecto en la referencia Open Source para equipos Midea mediante Modbus RTU.

No solo una integración de ESPHome, sino un conjunto completo de herramientas de ingeniería, documentación y automatización para toda la gama de productos Midea.

---

**Estado del proyecto:** 🟢 Desarrollo activo.
