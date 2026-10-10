# TP_THM – Prácticas de Seguridad Informática

Repositorio correspondiente a la Actividad A08 de la materia **Seguridad Aplicada a Sistemas de Información** (Universidad CAECE / UCH).

El objetivo del trabajo es documentar las prácticas realizadas en TryHackMe, registrando las fases de reconocimiento, escaneo, enumeración, explotación, escalada de privilegios y análisis de vulnerabilidades, junto con sus evidencias e informes.

---

## Datos generales

- **Alumno:** Tomas Ortiz
- **Sala de TryHackMe:** Kenobi
- **Rama de trabajo:** `ortiz-tomas`

---

## Laboratorios realizados

### 1. Basic Pentesting

El laboratorio se orienta a la identificación y análisis de servicios expuestos en un sistema objetivo.

Las actividades incluyen:

1. **Reconocimiento y escaneo:** identificación de puertos abiertos y servicios mediante Nmap.
2. **Enumeración de servicios:** análisis de los servicios SMB y HTTP, junto con los recursos y directorios accesibles.
3. **Análisis web:** revisión de rutas y servicios web disponibles.
4. **Registro de resultados:** documentación de los comandos, hallazgos y evidencias obtenidas durante la práctica.

**Archivos relacionados:**

- `bitacora/basic_pentesting.txt`
- `bitacora/nmap_inicial.txt`
- `evidencias/escaneo/`
- `evidencias/enumeracion/`

### 2. Kenobi

El laboratorio **Kenobi** aborda la explotación de servicios mal configurados en un entorno Linux, recorriendo distintas etapas de una prueba de penetración.

#### Fases del laboratorio

1. **Reconocimiento y escaneo:** enumeración de puertos mediante Nmap e identificación de servicios como Samba (SMB), RPCbind y NFS.

2. **Explotación inicial (ProFTPD):** aprovechamiento de la vulnerabilidad `mod_copy`, asociada a CVE-2015-3306, para copiar la clave privada SSH del usuario al directorio `/var/tmp`.

3. **Pivoteo y acceso:** montaje del recurso NFS exportado para obtener la clave privada `id_rsa` y utilizarla para autenticarse mediante SSH como el usuario `kenobi`.

4. **Escalada de privilegios:** auditoría de binarios SUID y análisis de una técnica de *PATH hijacking* sobre `/usr/bin/menu`, con el objetivo de obtener privilegios de superusuario (`root`).

#### Evidencias y documentación

- **Bitácora:** `bitacora/kenobi.txt`
- **Evidencias de escaneo:** `evidencias/escaneo/`
- **Evidencias de explotación:** `evidencias/explotacion/`
- **Captura del escaneo:** [Ver evidencia de Kenobi](evidencias/explotacion/escaneo_kenobi.png)

#### Flag obtenida

- **Flag de Root:** `177b3cd8562289f37382721c28381f02`

---

## Estructura del repositorio

```text
TP_THM/
├── bitacora/
│   ├── basic_pentesting.txt
│   ├── kenobi.txt
│   └── nmap_inicial.txt
├── evidencias/
│   ├── enumeracion/
│   ├── escaneo/
│   ├── explotacion/
│   └── reconocimiento/
├── reportes/
│   └── informe_pentesting_.pdf
└── README.md
```

La estructura organiza los registros de comandos, las capturas y los informes para facilitar la revisión de las actividades realizadas.

---

## Herramientas utilizadas

- **Nmap:** escaneo de puertos y detección de servicios.
- **SMBClient:** enumeración e interacción con recursos compartidos SMB.
- **Gobuster:** enumeración de directorios y rutas web.
- **SSH:** acceso remoto al sistema objetivo.
- **Git y GitHub:** control de versiones y almacenamiento del trabajo.

También se utilizaron herramientas y técnicas específicas de cada laboratorio para la enumeración de servicios, el análisis de configuraciones y la evaluación de privilegios.

---

## Metodología

En cada laboratorio se siguió una metodología de prueba de penetración:

1. Reconocimiento del objetivo.
2. Escaneo y enumeración de servicios.
3. Identificación de posibles vulnerabilidades y configuraciones inseguras.
4. Explotación controlada dentro del entorno autorizado de TryHackMe.
5. Análisis de privilegios y resultados obtenidos.
6. Registro de evidencias y elaboración de documentación técnica.

---

## Informe de pentesting

El informe formal se encuentra en:

`reportes/informe_pentesting_.pdf`

Este documento presenta los hallazgos relevados, su evaluación, las recomendaciones de seguridad y las medidas propuestas para reducir los riesgos identificados.

---

## Consideraciones éticas

Todas las actividades se realizaron en entornos de laboratorio autorizados con fines educativos. Las técnicas descriptas se utilizan para comprender vulnerabilidades, evaluar riesgos y proponer medidas de mitigación.

---

**Actividad A08 – Seguridad Aplicada a Sistemas de Información**