# Contributing

## Añadir registros nuevos

1. Añade primero el registro como sensor de solo lectura.
2. Verifica que no genera errores Modbus.
3. Comprueba el valor en varios estados: apagada, calefacción, frío y ACS.
4. Documenta el registro en `docs/registers.md`.
5. Solo después de validar, añade escritura si procede.

## Organización

- `30_controls.yaml`: selects y numbers principales.
- `40_switches.yaml`: switches de control.
- `60_*`: sensores principales.
- `64_extra_diagnostics.yaml`: sensores de diagnóstico.
- `70_binary_sensors.yaml`: estados ON/OFF.
- `80_text_sensors.yaml`: estados de texto.
- `90_pressure.yaml`: sensor de presión externo.
- `91_cop.yaml`: cálculos.
- `99_raw_registers.yaml`: registros internos/RAW.
