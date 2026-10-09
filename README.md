# Actividad A08 — Informe de Pentesting Ético (INSECUR S.A.)

**Materia:** Seguridad Aplicada a Sistemas de Información
**Docente:** Ing. Rodrigo Atilio Elgueta
**Alumno/a:** Diego Daniel Jofré Winterstetter
**Username TryHackMe:** `ddjwinter`
**Branch:** `jofre-diego`

## Descripción

Informe de pentesting ético sobre entornos controlados de TryHackMe, realizado como
trabajo práctico final de la cátedra. El trabajo cubre el núcleo obligatorio
(*Pentesting Fundamentals* + *Basic Pentesting*) y la sala de elección
(*Vulnversity*), siguiendo la metodología PTES / NIST SP 800-115.

> Todas las pruebas se ejecutaron exclusivamente contra las IP asignadas por
> TryHackMe a través de la VPN oficial de la plataforma, dentro del alcance
> autorizado por la cátedra. No se realizó ninguna acción contra sistemas reales.


## Estructura del repositorio

```
.
├── reportes/
│   └── informe_pentesting.pdf      # Informe final
├── bitacora/
│   ├── vulnversity_nmap_puertos.txt
│   ├── gobuster.txt
│   └── hydra.txt                   # credenciales sanitizadas como [REDACTED]
├── evidencias/
│   ├── reconocimiento/
│   ├── escaneo/
│   ├── explotacion/
│   └── post/
└── README.md
```


## Higiene de secretos y flags

- Las credenciales obtenidas (bitácora `hydra.txt`) figuran sanitizadas como
  `[REDACTED]`.
- Las flags obtenidas se documentan únicamente como hash SHA-256 (Anexo C del
  informe), nunca en texto plano.

## Checklist antes del push

- [x] Informe en `reportes/informe_pentesting.pdf`
- [x] Evidencias en `evidencias/` (por fase) — **revisar que ninguna muestre
      flags en texto plano** antes de subirlas
- [x] Bitácoras en `bitacora/`
- [x] Branch nombrado `apellido-nombre`
- [x] Commits con identidad institucional real
- [x] Datos personales completados en el informe (nombre, DNI, email)
- [x] Declaración ética (Anexo D) firmada

## Alcance ético

Trabajo realizado en entornos sandbox de TryHackMe con fines exclusivamente
académicos, dentro del alcance autorizado por la cátedra (ver Anexo D del
informe).