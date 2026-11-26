# Pendiente

Lo que falta por validar, mejorar o desarrollar. Lo ya implementado y en uso está en el [README](README.md).

## Pendiente de validar

- Texto de **Error actual**: comprobar la tabla con un fallo real (ver [errores](docs/errores.md)).
- Escritura de parámetros avanzados de servicio y límites de temperatura.
- Potencia eléctrica estimada (V×I): sigue unos 0,15 kW por debajo del medidor externo, con ±10 %. Valorar un medidor dedicado para el COP.
- Valorar usar la potencia térmica del módulo hidráulico (0x8C) en el COP instantáneo, por tener mejor resolución que las temperaturas de agua de 1 °C. Hoy se compara con la potencia térmica calculada pero no se usa en el COP.
- Contar la resistencia IBH1 en la energía: crear en HA un contador de energía de «Potencia resistencia apoyo estimada» (`integration`), sus contadores diario y mensual, y COP diario y mensual del sistema: (térmica del equipo + energía de la resistencia) / (eléctrica del equipo + energía de la resistencia). Requiere instalar antes el firmware con el sensor nuevo.
- Comprobar la potencia real de la resistencia IBH1 (se ha medido unos 3 kW en un solo episodio) y, si algún día se activa, la de TBH (no se calcula).
- Retirar el sensor temporal «Presión tensión ADC cruda» cuando termine la calibración del sensor de presión.

## Por descubrir (sniffer Modbus)

- Registro del modo purga.
- Smart Grid y excedentes fotovoltaicos.
- Antilegionela (activación, temperatura, duración y horario).
- Modo vacaciones.
- Zona 2.
- Curvas climáticas por registros 0x12, 0x13, 0x16 y 0x17: en esta unidad responden con excepción Modbus 2.
- Registros 0x94-0x9B (excepción 2).

## Mejoras

- Automatizaciones de ejemplo: alarma por presión baja o cayendo rápido, ACS con excedentes FV, silencioso nocturno y consigna según tarifa.
- Esquema eléctrico en imagen (ESP32, RS485, sensor de presión y divisor) y capturas de los logs de ESPHome.
- Actualizar las capturas del dashboard (muestran todavía los registros RAW retirados).
- Posible integración del fan coil Midea con controlador KJRP-75A/BK-E por RS485.

## Hecho

- Comunicación Modbus, lecturas y controles principales.
- Climatización zona 1 y ACS independientes.
- Curva climática de zona 1 (registro 0x06).
- Sensor de presión calibrado y avisos de presión baja y alta.
- Potencia eléctrica estimada, potencia térmica y COP.
- Error actual en texto.
- Estado real y Resumen aerotermia.
- Diagnóstico del ESP32, API cifrada y OTA con contraseña.
- Dashboard v1.3.
