# Pendiente / Roadmap

Este archivo recoge lo que queda pendiente por validar, mejorar o desarrollar en la integración **Midea M-Theri ESPHome Modbus**.

---

## Estado general

La integración ya permite controlar y monitorizar gran parte de la aerotermia mediante ESPHome + Modbus RTU, pero todavía hay registros y funciones que deben validarse en más estados de funcionamiento y, si es posible, en más modelos Midea M-Theri.

---

## Pendiente crítico

### 1. Confirmar registros de escritura

Algunos registros funcionan en lectura, pero la escritura debe probarse con cuidado para evitar errores Modbus o cambios no deseados.

Pendiente de validar:

- Curva climática zona 1.
- Nivel modo silencioso.
- ACS rápida.
- Modo ECO.
- Parámetros avanzados de servicio.
- Límites de temperatura.
- Registros relacionados con Smart Grid.

---

### 2. Modo purga

Todavía no está identificado el registro del **modo purga**.

Plan:

1. Activar el modo purga desde el controlador oficial.
2. Ejecutar sniffer Modbus antes, durante y después.
3. Comparar registros modificados.
4. Añadir un `switch` seguro en ESPHome.

---

### 3. Potencia eléctrica instantánea real

La potencia eléctrica instantánea leída por Modbus varía bastante y todavía no está confirmada al 100 %.

Pendiente:

- Comparar con pinza amperimétrica o medidor externo.
- Ver si el registro usado representa potencia real, potencia estimada o un valor interno.
- Confirmar si sirve para COP/EER instantáneo.

---

### 4. COP / EER instantáneo

Actualmente se puede calcular usando:

```text
COP/EER = potencia generada / potencia eléctrica consumida instantánea
```

Pero falta validar que la potencia eléctrica sea correcta.

Pendiente:

- Confirmar potencia eléctrica real.
- Separar claramente COP en calefacción y EER en refrigeración.
- Crear sensores diarios, mensuales y acumulados.

---

## Mejoras funcionales

### 5. Dashboard Home Assistant

Crear un dashboard Lovelace completo y limpio.

Pendiente:

- Tarjeta principal estilo controlador Midea.
- Mostrar solo la consigna de calefacción cuando esté en modo calor.
- Mostrar solo la consigna de refrigeración cuando esté en modo frío.
- Tarjetas de diagnóstico ocultas o plegables.
- Gráficas de presión, COP, consumo, potencia y temperaturas.

---

### 6. Sensor de presión

Funciona con sensor analógico externo, pero queda por mejorar la documentación.

Pendiente:

- Documentar mejor el divisor resistivo.
- Añadir esquema en imagen.
- Recomendar condensador de filtrado.
- Añadir ejemplos de calibración multipunto.
- Añadir automatizaciones de alarma por baja presión o fuga.

---

### 7. Smart Grid / fotovoltaica

Pendiente de investigar registros relacionados con Smart Grid y excedentes FV.

Objetivos:

- Subir ACS con excedentes solares.
- Cambiar consigna según producción FV.
- Priorizar calefacción o ACS según previsión solar.
- Integrar con Forecast.Solar.
- Integrar con batería virtual o batería física si existe.

---

### 8. Antilegionela / desinfección

Hay registros relacionados con desinfección, pero todavía no se han validado en esta instalación.

Pendiente:

- Confirmar activación/desactivación.
- Confirmar temperatura objetivo.
- Confirmar duración.
- Confirmar horarios.
- Crear controles seguros.

---

### 9. Modo vacaciones

Pendiente de validar:

- Holiday Away.
- Holiday Home.
- Parámetros asociados.

---

### 10. Doble zona

La integración está centrada en zona 1.

Pendiente:

- Añadir zona 2.
- Separar consignas zona 1 / zona 2.
- Confirmar modos de instalación zona 2.
- Confirmar curva climática zona 2.

---

## Diagnóstico avanzado

### 11. Tabla completa de bits

Pendiente documentar todos los bits de:

- Registro 0x00.
- Registro 0x05.
- Registro 0x80.
- Registro 0x81.
- Registro 0xD2.
- Registro 0xD3.

---

### 12. Registros RAW

Pendiente:

- Mantener una tabla de registros RAW.
- Marcar cuáles están identificados.
- Marcar cuáles cambian en calefacción, refrigeración, ACS y espera.
- Eliminar o esconder los registros inútiles.

---

### 13. Códigos de error

Pendiente:

- Crear tabla de códigos de error Midea.
- Convertir el código numérico en texto descriptivo.
- Añadir entidad `text_sensor` con error legible.
- Añadir notificaciones en Home Assistant.

---

## Documentación

### 14. Completar `docs/registers.md`

Añadir:

- Dirección.
- Nombre.
- Tipo.
- Escala.
- Unidad.
- Lectura/escritura.
- Estado de validación.
- Observaciones.

Ejemplo:

```markdown
| Registro | Nombre | Tipo | Escala | R/W | Estado |
|---:|---|---|---:|---|---|
| 0x07 | ACS rápida | U_WORD | 1/2 | W | Probado |
```

---

### 15. Añadir capturas

Pendiente añadir imágenes en:

```text
images/
docs/screenshots/
```

Capturas recomendadas:

- Dashboard principal.
- Diagnóstico.
- Gráfica de presión.
- ESPHome logs.
- Cableado RS485.
- Sensor de presión.

---

### 16. Añadir esquema eléctrico

Pendiente dibujar:

- ESP32.
- RS485.
- Midea M-Theri.
- Sensor de presión.
- Divisor resistivo.
- Condensadores de filtrado.

---

## Integraciones futuras

### 17. Fan coils Midea

Pendiente futura integración de fan coil Midea con controlador:

```text
KJRP-75A/BK-E
```

Objetivos:

- Leer temperatura ambiente.
- Cambiar consigna.
- Cambiar modo.
- Cambiar velocidad ventilador.
- Leer alarmas.
- Integrar por RS485 Modbus.

---

### 18. Automatizaciones Home Assistant

Pendiente crear ejemplos:

- Alarma por presión baja.
- Alarma por presión cayendo rápido.
- Subida ACS con excedentes FV.
- Modo silencioso nocturno.
- Reducción de consigna por tarifa cara.
- Arranque anticipado según previsión meteorológica.

---

## Organización recomendada en GitHub

Estructura recomendada:

```text
Midea-MTheri-ESPHome/
│
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── TODO.md
├── .gitignore
│
├── aerotermia.yaml
│
├── midea/
│   ├── 00_base.yaml
│   ├── 10_modbus.yaml
│   ├── 30_controls.yaml
│   ├── 40_switches.yaml
│   ├── 60_temperatures.yaml
│   ├── 61_water.yaml
│   ├── 62_compressor.yaml
│   ├── 63_energy.yaml
│   ├── 64_extra_diagnostics.yaml
│   ├── 70_binary_sensors.yaml
│   ├── 80_text_sensors.yaml
│   ├── 90_pressure.yaml
│   ├── 91_cop.yaml
│   ├── 92_climate_curve.yaml
│   └── 99_raw_registers.yaml
│
├── docs/
│   ├── wiring.md
│   ├── registers.md
│   ├── homeassistant.md
│   └── dashboard.yaml
│
└── images/
    └── screenshots/
```

---

## Prioridad recomendada

### Prioridad alta

- Validar ACS rápida.
- Validar curva climática.
- Confirmar potencia eléctrica real.
- Mejorar dashboard.
- Completar tabla de registros.

### Prioridad media

- Modo purga.
- Antilegionela.
- Smart Grid.
- Fotovoltaica.
- Doble zona.

### Prioridad baja

- Fan coils.
- Automatizaciones avanzadas.
- Estadísticas mensuales.
- Mejoras visuales del repositorio.

---

## Notas

Antes de añadir cualquier registro de escritura nuevo, se recomienda:

1. Leer el registro en varios estados.
2. Compararlo con la pantalla oficial.
3. Cambiarlo desde el controlador oficial y ver qué valor toma.
4. Solo después implementar escritura desde ESPHome.

