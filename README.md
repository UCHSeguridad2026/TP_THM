# Auditoría de Seguridad y Pentesting — Actividad A08

**Cliente simulado:** INSECUR S.A.  
**Cátedra:** Seguridad Aplicada a Sistemas de Información — Licenciatura en Sistemas de Información, Facultad de Informática y Diseño  
**Docente:** Ing. Rodrigo Atilio Elgueta  
**Estudiante:** María Paz Sinner — DNI: 46403629  
**Email institucional:** sinnerpaz@uch.edu.ar  
**Usuario de TryHackMe:** `mariapazsinner`  
**Rama de entrega:** `sinner-maria-paz`  
**Ciclo académico:** 2026  
**Período de trabajo:** 05-10-2026 al 07-10-2026  

---

## Presentación del trabajo

Este repositorio reúne el informe de pentesting del caso académico INSECUR S.A., junto con las evidencias y las bitácoras de las prácticas realizadas en TryHackMe.

El objetivo fue aplicar una metodología de hacking ético para reconocer los sistemas del laboratorio, identificar los servicios disponibles, analizar posibles vulnerabilidades y documentar los resultados. A partir de los hallazgos, se elaboraron recomendaciones de seguridad y un protocolo de contingencia orientado a reducir los riesgos y preservar la continuidad del negocio.

## Salas realizadas

Se completaron **Pentesting Fundamentals** y **Basic Pentesting**, correspondientes al núcleo obligatorio de la actividad, y **Vulnversity** como sala de elección.

Las prácticas permitieron trabajar los conceptos de alcance, autorización y metodología, además de las etapas técnicas de escaneo, enumeración, explotación y escalada de privilegios. El informe distingue las observaciones obtenidas durante el reconocimiento de las vulnerabilidades efectivamente comprobadas.

## Informe y resultados

El [informe de pentesting](reportes/informe_pentesting.pdf) presenta los datos generales, el alcance autorizado, las reglas de enfrentamiento y la metodología utilizada, tomando como referencia NIST SP 800-115.

En Vulnversity se documentaron dos vulnerabilidades confirmadas: la carga de un archivo ejecutable que permitió acceder al servidor como `www-data` y la configuración de `systemctl` con SUID, que permitió realizar una acción con privilegios de root. Para cada hallazgo se describen las evidencias, las herramientas utilizadas, el impacto sobre la confidencialidad, la integridad y la disponibilidad, y las medidas de remediación propuestas.

Las recomendaciones incluyen controles sobre la carga y ejecución de archivos, revisión de permisos y servicios, registro de cambios y pruebas de restauración de respaldos. Se presentan como medidas propuestas; no se afirma que hayan sido implementadas o verificadas después del laboratorio.

## Protocolo de contingencia

El informe desarrolla un escenario de interrupción del portal web de INSECUR S.A. y propone acciones de detección, contención, recuperación y comunicación.

También contempla un canal alternativo de atención durante la recuperación y objetivos estimados de RTO y RPO. Estos valores corresponden al escenario académico planteado y deberían validarse mediante pruebas de restauración.

## Organización del repositorio

- **[reportes/](reportes/):** informe de pentesting en PDF, con recomendaciones, protocolo de contingencia y declaración ética firmada.
- **[evidencias/](evidencias/):** capturas de las salas y de las prácticas, organizadas por fase.
- **[bitacora/](bitacora/):** registros de los comandos y actividades documentados durante las sesiones.

Las evidencias permiten relacionar los resultados del informe con el proceso seguido en los laboratorios. Las respuestas obtenidas se documentan mediante hashes SHA-256, evitando publicar los valores completos de las flags.

## Documentación de la entrega

- [x] Informe de pentesting en `reportes/informe_pentesting.pdf`.
- [x] Salas Pentesting Fundamentals, Basic Pentesting y Vulnversity completadas.
- [x] Hallazgos confirmados y observaciones de escaneo diferenciados.
- [x] Capturas organizadas en `evidencias/`.
- [x] Bitácoras disponibles en `bitacora/`.
- [x] Hashes SHA-256 incluidos en el Anexo C.
- [x] Declaración ética firmada incluida en el Anexo D.
- [x] Entrega realizada en la rama personal `sinner-maria-paz`.

## Alcance y ética

Todas las actividades se realizaron exclusivamente en entornos controlados y autorizados de TryHackMe, con fines académicos y dentro del alcance establecido por la cátedra.

El caso de INSECUR S.A. es una simulación académica. No se realizaron pruebas sobre sistemas reales de la organización ni sobre equipos de terceros.
