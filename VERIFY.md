# Verificación de la documentación

Revisión del 27 de noviembre de 2026.

- La carpeta `esphome/` coincide con la configuración en uso en Home Assistant.
- README, TODO y ROADMAP actualizados a lo realmente implementado.
- Corregida la codificación de caracteres del README (UTF-8).
- Añadido `docs/errores.md`.
- Los registros R148-R155, 0x93 y 0x94-0x9B figuran como retirados.
- No se ha compilado el firmware en esta revisión.
- `energy.yaml` incluye el filtro `filter_out: 0` en los contadores de energía; la configuración es válida en ESPHome, pero no se ha compilado el firmware.
- Versiones del equipo (0x82 y 0x83): configuración válida, pero aún no se ha visto qué valor devuelven con el firmware instalado.
- `calculated/cop.yaml` incluye la resistencia IBH1; la configuración es válida en ESPHome, pero no se ha compilado el firmware.
- Documentados el COP diario y mensual y el estado del registro 0x8C.
