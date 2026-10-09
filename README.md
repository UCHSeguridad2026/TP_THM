# TP_TryHackMe

Repositorio de entrega del trabajo práctico de TryHackMe.

Este repositorio está destinado exclusivamente a la entrega individual del estudiante. Cada alumno debe trabajar en su propia branch y mantener evidencia ordenada del proceso realizado.

## Política de ramas

- Cada estudiante debe crear una branch personal con su nombre/apellido.
- La entrega debe realizarse desde esa branch.
- No se permite reemplazar la entrega con un pull request.

## Penalización

Si un estudiante envía un pull request en lugar de trabajar en su propia branch, se descontarán 3/10 puntos del trabajo.

## Reglas adicionales

- Cada estudiante es responsable de su propia branch.
- No se permite hacer `git push --force` sobre ramas compartidas.
- Si se comete un error sobre `main` o la rama de otro compañero, debe comunicarse de inmediato al docente.
- Se deben respetar las buenas prácticas de GitHub y la guía de la actividad.

## Ética y legalidad

La actividad debe desarrollarse únicamente en entornos controlados y autorizados. No se permite aplicar estas técnicas sobre sistemas reales sin autorización.

# TP_THM - Auditoría de Seguridad y Hacking Ético

**Cliente:** INSECUR S.A. 
**Asignatura:** Seguridad Aplicada a Sistemas de Información (FID-UCH) 
**Docente:** Ing. Rodrigo Atilio Elgueta 
**Estudiante:** Camila Borodij 
**Username TryHackMe:** *camilaborodijferrari* 
**Repositorio Oficial:** `https://github.com/UCHSeguridad2026/TP_THM.git` 
**Branch de Trabajo:** `borodij-camila` 

---

## 1. Descripción del Proyecto

El presente repositorio contiene la documentación técnica, registros de bitácora y evidencias del trabajo práctico de Hacking Ético contratado por **INSECUR S.A.**. Las pruebas se realizaron en entornos controlados de laboratorio (sandbox) en la plataforma **TryHackMe**, aplicando el marco metodológico **PTES** (Penetration Testing Execution Standard) y las recomendaciones del **OWASP Testing Guide**.

El objetivo principal es evaluar la postura de seguridad de la infraestructura asignada, documentar los hallazgos identificados (fase de pentesting) y presentar las salvaguardas de *hardening* y el protocolo de contingencia para garantizar la continuidad del negocio.

---

## 2. Alcance y Salas Trabajadas

### Nivel 1: Núcleo Obligatorio
1. **Pentesting Fundamentals:** Conceptos, metodología y fases del pentesting profesional.
2. **Basic Pentesting (`10.66.171.56`):** Aplicación práctica completa de reconocimiento, enumeración de servicios (SMB, HTTP, SSH), análisis de mecanismos de autenticación y evaluación de permisos locales.

### Nivel 2: Sala de Elección
* **Kenobi:** Enumeración de servicios compartidos (Samba, NFS), explotación e inspección de privilegios locales en Linux (SUID/capabilities).

---

## 3. Estructura del Repositorio

TP_THM/
├── bitacora/
│   ├── nmap_inicial.txt          # Escaneo de puertos y servicios expuestos
│   ├── gobuster_inicial.txt      # Enumeración de directorios web
│   ├── notas_development.txt     # Análisis de componentes y versiones web
│   ├── notas_samba.txt           # Auditoría del recurso compartido SMB Anonymous
│   ├── notas_ssh.txt             # Evaluación de la autenticación SSH y hardening
│   ├── notas_escalada.txt        # Análisis de permisos locales y sudoers
│   ├── conclusiones.txt          # Matriz de remediación y conclusiones técnicas
│   └── clase_09_20261008.txt     # Historial filtrado de comandos de la sesión
├── evidencias/
│   ├── reconocimiento/           # Capturas de pantalla de fase de reconocimiento
│   ├── escaneo/                  # Capturas de escaneo (H-01: SMB)
│   ├── explotacion/              # Capturas de autenticación (H-02: SSH)
│   └── post/                     # Capturas de escalada/sudoers (H-03: Sudo)
├── reportes/
│   ├── informe_pentesting.md     # Plantilla de informe completada en Markdown
│   └── informe_pentesting.pdf    # Entregable final compilado en formato PDF
└── README.md                     # Índice principal y documentación del repositorio
### 4. Resumen Ejecutivo de Hallazgos

| ID | Hallazgo / Vulnerabilidad | Fase | Componente Afectado | Severidad (CVSS) | Impacto CIA | Estado |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **H-01** | Exposición de Recursos Compartidos Anónimos | Enumeración | Samba / SMB (139/445) | Medio (5.3) | Confidencialidad: Alta | Mitigado |
| **H-02** | Mecanismo de Autenticación Débil en SSH | Explotación | OpenSSH (22/tcp) | Alto (7.5) | Confidencialidad / Integridad | Mitigado |
| **H-03** | Asignación Insegura de Privilegios Administrativos | Post-explotación | Linux / `/etc/sudoers` | Alto (7.8) | Confidencialidad / Integridad / Disponibilidad | Mitigado |

---

#### Resumen Consolidado por Severidad

| Severidad | Cantidad | ID de Hallazgos |
| :--- | :---: | :--- |
| **Crítico** | 0 | - |
| **Alto** | 2 | H-02, H-03 |
| **Medio** | 1 | H-01 |
| **Bajo** | 0 | - |
| **Total** | **3** |


## 5. Instrucciones de Verificación y Control de Autenticidad

Para garantizar la integridad, autoría y autenticidad de los entregables presentados en este repositorio:

1. **Bitácora de Comandos Sanitizada:** Todos los registros de la sesión de trabajo fueron exportados e inspeccionados previamente, aplicando filtros de sanitización para eliminar cualquier contraseña, token, clave privada o credencial sensible (`[REDACTED]`).
2. **Hashes SHA-256 de Flags:** Los hashes criptográficos de las banderas obtenidas en los laboratorios se encuentran documentados en el **Anexo C** del informe final (`reportes/informe_pentesting.md`), permitiendo la validación docente sin exponer las cadenas originales.
3. **Control de Identidad en Commits:** Las contribuciones del repositorio fueron configuradas utilizando el nombre completo y correo institucional del estudiante.


## Anexo D/6: Declaración Ética Firmada

Declaro que todas las actividades técnicas, pruebas de penetración y análisis documentados en este proyecto se realizaron estrictamente dentro del alcance autorizado, en entornos controlados de laboratorio (*sandbox*) de la plataforma TryHackMe y con fines exclusivamente académicos para la asignatura **Seguridad Aplicada a Sistemas de Información**. 

Queda absolutamente prohibida la aplicación de las técnicas, herramientas o procedimientos descritos contra sistemas reales, redes de producción o infraestructuras sin la correspondiente autorización explícita y por escrito.

---

**Firma del estudiante:** Camila Borodij 
**Asignatura:** Seguridad Aplicada a Sistemas de Información (FID-UCH) 
**Fecha:** 8 de Octubre de 2026
