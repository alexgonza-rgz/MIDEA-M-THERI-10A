# Home Assistant

ESPHome no oculta entidades dinámicamente. Para mostrar solo la consigna correspondiente al modo actual, usa tarjetas condicionales en Lovelace.

Entidades recomendadas:

- Estado real
- Resumen aerotermia
- Modo de trabajo
- Consigna agua calefacción zona 1
- Consigna agua refrigeración zona 1
- Consigna ACS
- ACS rápida
- Modo silencioso
- Nivel modo silencioso alto
- Modo ECO
- Curva climática zona 1
- COP instantáneo
- Presión circuito calefacción

## COP diario y mensual

El COP instantáneo es ruidoso porque las temperaturas del agua tienen resolución de 1 °C. Para tener un COP fiable se usan los contadores de energía del equipo en Home Assistant, creados desde **Ajustes → Dispositivos y servicios → Entradas**, sin YAML:

| Entrada | Tipo | Fuente |
|---|---|---|
| Aerotermia consumo eléctrico diario y mensual | `utility_meter` | Energía eléctrica consumida |
| Aerotermia energía térmica diaria y mensual | `utility_meter` | Energía térmica producida |
| Aerotermia COP diario y mensual | `template` (sensor) | Energía térmica / energía eléctrica del mismo periodo |

La plantilla es:

```jinja
{% set e = states('<consumo eléctrico del periodo>') | float(0) %}
{% set t = states('<energía térmica del periodo>') | float(0) %}
{{ (t / e) | round(2) if e > 0.1 else 0 }}
```

Los contadores del equipo suben en pasos de 1 kWh, así que un COP diario con pocos kWh consumidos tiene mucho redondeo. El mensual es más fiable. El COP acumulado de ESPHome es el de toda la vida del contador del equipo.

