# Cambios

## 27/11/2026

- `energy.yaml`: los contadores de energía eléctrica y térmica descartan las lecturas iguales a 0 (`filter_out: 0`), para que los contadores diarios y mensuales de Home Assistant no sumen el contador completo tras una reconexión.
- El comentario de `energy.yaml`, el README y el TODO corrigen lo del registro 0x8C: da valores reales con el compresor en marcha y 0 con la máquina parada. Sigue sin usarse en el COP.
- `docs/homeassistant.md`: documenta los contadores y el COP diario y mensual, y cómo recalibrar un contador mensual.

## 26/11/2026 (v2.0.1)

- Error actual en texto, sensor de presión calibrado, potencia eléctrica estimada, COP, API cifrada y OTA con contraseña, y dashboard v1.3. Ver el [README](README.md).
