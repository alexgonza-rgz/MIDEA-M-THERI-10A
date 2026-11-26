# Cambios

## 27/11/2026

- `extra_diagnostics.yaml`: sensores de solo lectura «Versión software equipo» (registro 0x82) y «Versión mando cableado» (0x83), y tarjeta «Versiones del equipo» en la pestaña Diagnóstico del dashboard. Pendiente de instalar el firmware y de comprobar qué valor devuelve el equipo.
- `calculated/cop.yaml`: se tiene en cuenta la resistencia de apoyo IBH1 (3 kW, medidos con el Deye el 22/11/2026). Entra cuando el compresor se para y los contadores del equipo no la cuentan, así que el COP salía 0 con la casa consumiendo unos 3 kW.
  - Sensor nuevo «Potencia resistencia apoyo estimada» (`resistencia_apoyo_kw`, 3,0 kW).
  - «Potencia eléctrica estimada» suma esa resistencia.
  - «Potencia térmica calculada» da la potencia de la resistencia cuando trabaja sola (compresor a 0 Hz).
  - «COP instantáneo» ya no devuelve 0 mientras la resistencia está activa.
- `energy.yaml`: los contadores de energía eléctrica y térmica descartan las lecturas iguales a 0 (`filter_out: 0`), para que los contadores diarios y mensuales de Home Assistant no sumen el contador completo tras una reconexión.
- El comentario de `energy.yaml`, el README y el TODO corrigen lo del registro 0x8C: da valores reales con el compresor en marcha y 0 con la máquina parada. Sigue sin usarse en el COP.
- `docs/homeassistant.md`: documenta los contadores y el COP diario y mensual, y cómo recalibrar un contador mensual.

## 26/11/2026 (v2.0.1)

- Error actual en texto, sensor de presión calibrado, potencia eléctrica estimada, COP, API cifrada y OTA con contraseña, y dashboard v1.3. Ver el [README](README.md).
