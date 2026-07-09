# Registros Modbus - Midea M-Thermal 2 R32

Este documento recopila los registros Modbus conocidos de la aerotermia Midea M-Thermal 2 R32 obtenidos a partir de la documentación oficial del fabricante.

## Comunicación

| Parámetro | Valor |
|-----------|-------|
| Protocolo | Modbus RTU |
| Interfaz | RS-485 |
| Puerto | H1 / H2 |
| Velocidad | 9600 bps |
| Bits de datos | 8 |
| Paridad | Ninguna |
| Bits de parada | 1 |

---

# Registros de control (Lectura / Escritura)

| Registro | PLC | Nombre | Unidad | Acceso | Descripción |
|---------:|----:|---------|---------|--------|-------------|
|40001|0|Control ON/OFF|Bits|R/W|Activación calefacción, ACS y zonas|
|40002|1|Modo de funcionamiento|Enum|R/W|1 Auto · 2 Frío · 3 Calor|
|40003|2|Consigna agua (T1S)|°C|R/W|Temperatura objetivo del agua|
|40004|3|Consigna ambiente (Ts)|0,5°C|R/W|Temperatura ambiente objetivo|
|40005|4|Consigna ACS (T5S)|°C|R/W|Temperatura objetivo del depósito ACS|
|40006|5|Funciones|Bits|R/W|ECO, Silencio, Curva climática, Desinfección...|
|40007|6|Selección curva climática|Bits|R/W|Zona 1 y Zona 2|
|40008|7|Calentamiento ACS forzado|Enum|R/W|0 Inválido · 1 ON · 2 OFF|
|40009|8|TBH forzado|Enum|R/W|Resistencia del depósito|
|40010|9|IBH1 forzado|Enum|R/W|Resistencia auxiliar|

---

# Registros de funcionamiento

| Registro | PLC | Nombre | Unidad | Observaciones |
|---------:|----:|---------|---------|--------------|
|40101|100|Frecuencia compresor|Hz|Frecuencia real del inverter|
|40102|101|Modo de funcionamiento|Enum|0 Apagado · 2 Frío · 3 Calor|
|40103|102|Velocidad ventilador|rpm|Ventilador exterior|
|40104|103|Apertura válvula electrónica (PMV)|Paso|Válvula de expansión|
|40105|104|Temperatura entrada agua|°C|Tw_in|
|40106|105|Temperatura salida agua|°C|Tw_out|
|40107|106|Temperatura T3|°C|Condensador|
|40108|107|Temperatura exterior|°C|T4|
|40109|108|Temperatura descarga compresor|°C|Tp|
|40110|109|Temperatura retorno compresor|°C||
|40111|110|T1|°C|Salida total de agua|
|40112|111|T1B|°C|Después del apoyo eléctrico|
|40113|112|T2|°C|Refrigerante líquido|
|40114|113|T2B|°C|Refrigerante gas|
|40115|114|Temperatura ambiente|°C|Ta|
|40116|115|Temperatura depósito ACS|°C|T5|
|40117|116|Presión alta|kPa||
|40118|117|Presión baja|kPa||
|40119|118|Corriente unidad exterior|A||
|40120|119|Tensión unidad exterior|V||
|40121|120|Temperatura depósito inercia Tbt1|°C||
|40122|121|Temperatura depósito inercia Tbt2|°C||
|40124|123|Capacidad de la unidad|Código||
|40125|124|Fallo actual|Código||
|40126|125|Histórico fallo 1|Código||
|40127|126|Histórico fallo 2|Código||
|40128|127|Histórico fallo 3|Código||
|40129|128|Bits de estado|Bits|Estado general|
|40130|129|Bits de salidas|Bits|Bombas, resistencias, alarma...|
|40133|132|Frecuencia objetivo|Hz||
|40134|133|Corriente bus CC|A||
|40135|134|Tensión bus CC|V ×10|Dividir entre 10|
|40136|135|Temperatura módulo inverter|°C||
|40137|136|Curva climática Zona 2|°C||
|40138|137|Curva climática Zona 1|°C||
|40139|138|Caudal de agua|m³/h ×100|Dividir entre 100|
|40140|139|Limitación de potencia|Código||
|40141|140|Capacidad módulo hidráulico|Código||
|40142|141|Temperatura solar|°C|Tsolar|
|40144|143|Consumo eléctrico (parte alta)|uint16||
|40145|144|Consumo eléctrico (parte baja)|uint16||
|40146|145|Potencia térmica (parte alta)|uint16||
|40147|146|Potencia térmica (parte baja)|uint16||

---

# Registro 40129 (Bits de estado)

| Bit | Significado |
|----:|-------------|
|11|Electricidad gratuita|
|10|Estado Smart Grid|
|9|Antihielo depósito|
|8|Entrada solar|
|7|Termostato refrigeración activo|
|6|Termostato calefacción activo|
|5|Modo prueba unidad exterior|
|4|Encendido remoto|
|3|Retorno de aceite|
|2|Modo antihielo|
|1|Desescarche|

---

# Registro 40130 (Bits de salida)

| Bit | Descripción |
|----:|-------------|
|15|Desescarche|
|14|Fuente de calor auxiliar|
|13|RUN (Unidad funcionando)|
|12|Alarma|
|11|Bomba solar|
|10|HEAT4|
|9|SV3|
|8|Bomba mezcladora|
|7|Bomba retorno ACS|
|6|Bomba exterior|
|5|SV2|
|4|SV1|
|3|Bomba principal|
|2|Resistencia depósito (TBH)|
|1|Resistencia auxiliar IBH2|
|0|Resistencia auxiliar IBH1|

---

# Registros especialmente útiles

- Frecuencia del compresor → **40101**
- Velocidad del ventilador → **40103**
- Apertura PMV → **40104**
- Temperatura entrada agua → **40105**
- Temperatura salida agua → **40106**
- Corriente eléctrica → **40119**
- Tensión eléctrica → **40120**
- Caudal de agua → **40139**
- Consumo eléctrico acumulado → **40144-40145**
- Potencia térmica → **40146-40147**
