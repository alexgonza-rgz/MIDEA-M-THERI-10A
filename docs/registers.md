# Register map

| Registro | Tipo | Función |
|---:|---|---|
| 0x00 | bits | Potencias / activaciones principales |
| 0x01 | word | Modo de trabajo |
| 0x02 | word | Consigna agua: byte bajo calefacción zona 1, byte alto refrigeración zona 1 |
| 0x03 | word | Consigna ambiente |
| 0x04 | word | Consigna ACS |
| 0x05 | bits | Funciones: silencioso, ECO, curva climática |
| 0x07 | word | ACS rápida / forzar ACS |
| 0x64 | word | Frecuencia compresor |
| 0x65 | word | Modo actual leído |
| 0x66 | word | Velocidad ventilador |
| 0x67 | word | Apertura PMV |
| 0x68 | sword | Temperatura retorno agua |
| 0x69 | sword | Temperatura impulsión agua |
| 0x6A | sword | Temperatura condensador T3 |
| 0x6B | sword | Temperatura exterior |
| 0x6C | sword | Temperatura descarga |
| 0x6D | sword | Temperatura retorno aire |
| 0x6E | sword | Temperatura salida total T1 |
| 0x6F | sword | Temperatura salida sistema T1B |
| 0x70 | sword | Refrigerante líquido T2 |
| 0x71 | sword | Refrigerante gas T2B |
| 0x72 | sword | Temperatura ambiente Ta |
| 0x73 | sword | Temperatura depósito ACS |
| 0x74 | word | Presión alta refrigerante |
| 0x75 | word | Presión baja refrigerante |
| 0x76 | word | Intensidad unidad exterior |
| 0x77 | word | Tensión unidad exterior |
| 0x7A | word | Horas compresor |
| 0x7C | word | Código de error actual |
| 0x80 | bits | Estados 1 |
| 0x81 | bits | Salidas / cargas |
| 0x84 | word | Frecuencia objetivo compresor |
| 0x85 | word | Corriente bus DC |
| 0x86 | word | Tensión bus DC |
| 0x87 | sword | Temperatura módulo inverter |
| 0x88 | sword | Curva climática T1S calculada zona 1 |
| 0x89 | sword | Curva climática T1S calculada zona 2 |
| 0x8A | word | Caudal de agua |
| 0x8C | word | Potencia módulo hidráulico |
| 0x8F | dword | Energía eléctrica consumida |
| 0x91 | dword | Energía térmica producida |
| 0x110 | word | Modos de instalación zona 1 |
