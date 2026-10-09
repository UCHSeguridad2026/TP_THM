# Bitácora — Sala Nmap (TryHackMe)

**Autor:** Juan Manuel Maure Spinelli — usuario THM: `juanchomaure1`
**Fecha:** 2026-10-08
**Host objetivo:** 10.65.150.223 (máquina redesplegada; la IP original de la primera corrida fue 10.65.185.14, mismos resultados)
**Herramienta:** Nmap 7.99 (Kali Linux)


## 1. Descubrimiento de host — ICMP echo (ping)

```bash
ping -c 4 10.65.185.14
```

**Resultado:** 0 paquetes recibidos, 100% packet loss. El host no responde a ICMP echo (firewall bloquea ICMP).

**Respuesta:** ¿Responde a ICMP echo? **N**


## 2. Xmas scan — primeros 999 puertos

```bash
sudo nmap -sX -p 1-999 --reason -Pn -T4 10.65.150.223
```

**Resultado:**
```
Nmap scan report for 10.65.150.223 (10.65.150.223)
Host is up, received user-set.
All 999 scanned ports on 10.65.150.223 (10.65.150.223) are in ignored states.
Not shown: 999 open|filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 109.61 seconds
```

**Respuestas:**
- Puertos `open|filtered`: **999**
- Razón: **no-response**

**Evidencia:** `evidencias/nmap/01_nmap_xmas_scan_999puertos.png`


## 3. TCP SYN scan — primeros 5000 puertos

```bash
sudo nmap -sS -p1-5000 -Pn -T4 10.65.150.223
```

**Resultado:**
```
Nmap scan report for 10.65.150.223 (10.65.150.223)
Host is up (0.15s latency).
Not shown: 4995 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
53/tcp   open  domain
80/tcp   open  http
135/tcp  open  msrpc
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 25.05 seconds
```

**Respuesta:** Puertos abiertos: **5** (21/ftp, 53/domain, 80/http, 135/msrpc, 3389/ms-wbt-server)


**Evidencia:** `evidencias/nmap/02_nmap_syn_scan_5000puertos.png`


## 4. TCP Connect scan — puerto 80 (monitoreado con Wireshark)

```bash
sudo nmap -sT -p80 -Pn 10.65.185.14
```

Realizado en la corrida original de la sala; captura de Wireshark con el 3-way handshake (SYN → SYN/ACK → ACK) ya tomada ese mismo día.


## 5. Script ftp-anon — puerto 21

```bash
nmap -p21 --script ftp-anon -Pn 10.65.150.223
```

**Resultado:**
```
PORT   STATE SERVICE
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT

Nmap done: 1 IP address (1 host up) scanned in 31.04 seconds
```

**Respuesta:** ¿Nmap logra login anónimo en FTP? **Y**

**Evidencia:** `evidencias/nmap/03_nmap_ftp_anon.png`


## Evidencias asociadas (evidencias/nmap/)

01_nmap_xmas_scan_999puertos.png · 02_nmap_syn_scan_5000puertos.png · 03_nmap_ftp_anon.png
