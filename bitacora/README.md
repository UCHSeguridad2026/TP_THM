# Bitácora de comandos

Exportá los comandos relevantes de cada sesión de Kali al finalizar cada clase.

## Comando de export (con redacción automática de secretos)

```bash
history | sed -E 's/(password|passwd|token|secret|api[_ -]?key)[^ ]*/\1=[REDACTED]/Ig' \
  > bitacora/clase_XX_$(date +%Y%m%d).txt
```

## Antes de commitear (revisión manual obligatoria)

1. Abrir el archivo y buscar contraseñas, tokens, claves privadas, IPs personales.
2. Reemplazar todo por `[REDACTED]`.
3. Verificar que **no** se suba ningún archivo `.ovpn` ni credencial de THM/GitHub.

> La bitácora no reemplaza la revisión manual de secretos.
