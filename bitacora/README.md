# Bitácora de comandos (Anexo A)

Acá van los logs de comandos **relevantes** de cada sesión de trabajo.

## Cómo generar la bitácora al cerrar cada sesión

El comando de la guía (adaptado) exporta el historial **filtrando secretos**
antes de guardarlo. En **fish shell** (tu caso) el historial no es el mismo que
en bash, así que usá:

```fish
# fish guarda el historial con `history`; lo pasamos por un filtro de secretos
history | sed -E 's/(password|passwd|token|secret|api[_-]?key)[^ ]*/\1=[REDACTED]/Ig' > bitacora/sesion_(date +%Y%m%d_%H%M).txt
```

> **IMPORTANTE:** la bitácora NO reemplaza la revisión manual. Abrí el archivo
> y borrá a mano cualquier contraseña, token, clave privada o IP personal que
> el filtro no haya captado, **antes** de hacer `git add`.

## Convención de nombres

- `sesion_YYYYMMDD_HHMM.txt` — export de historial por sesión
- `nmap_<sala>.txt`, `gobuster_<sala>.txt`, etc. — salidas de herramientas que
  quieras conservar como evidencia de proceso
