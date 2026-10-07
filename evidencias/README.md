# Evidencias — A08 / INSECUR S.A.

Una carpeta por fase del pentesting. Nomenclatura de archivos: `<fase>_<hallazgoID>.png`

| Carpeta | Fase |
|---|---|
| `reconocimiento/` | OSINT, enumeración pasiva, descubrimiento de activos |
| `escaneo/` | puertos, servicios y versiones (nmap, nikto, gobuster) |
| `explotacion/` | obtención de acceso |
| `post/` | escalada de privilegios, post-explotación |

## Reglas de las capturas

- Visible: **username de THM**, **fecha/hora del sistema** y **IP de la máquina objetivo**.
- Nunca subir la flag en claro: solo su hash SHA-256 (ver Anexo C del informe).
- Nunca subir el archivo `.ovpn` ni tokens de THM/GitHub.
