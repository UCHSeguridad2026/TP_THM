7. PARTE III: PROTOCOLO DE CONTINGENCIA

Escenario de falla

Al aplicar las correcciones de los hallazgos H-03 y H-04 sobre el servicio SSH (deshabilitar la autenticación por contraseña, rotar la clave privada y ajustar permisos), un error de configuración podría impedir el acceso remoto de los administradores o de los procesos automatizados que dependen de SSH. Lo mismo puede ocurrir al restringir SMB (H-02) o el listado de directorios del servidor web (H-01) si se bloquea un recurso que usan los sistemas internos.

Impacto sobre la continuidad del negocio

Se verían afectados el mantenimiento remoto de los servidores, los procesos de respaldo que usen SSH y cualquier aplicación interna que consuma los recursos SMB o web modificados. Como estimación, una interrupción de este tipo podría durar entre 1 y 4 horas si no hay un procedimiento de reversión ya probado.

Plan de respuesta

Activación: se detecta la falla por alertas de monitoreo, por reportes de los usuarios o por la imposibilidad de acceder a un servicio tras un cambio.
Contención (primeros 15 minutos): se suspende el cambio en curso, se mantiene abierta una sesión de administración activa y se revierte la última modificación de configuración.
Recuperación: se restaura la configuración anterior desde el respaldo versionado de /etc/ssh/sshd_config o del archivo de configuración correspondiente, se verifica el acceso y se vuelve a aplicar el cambio por etapas, con una ventana de prueba.
Comunicación: se notifica al responsable de sistemas de INSECUR S.A. y a los usuarios afectados, con el estado del servicio y el tiempo estimado de restauración.
Post-mortem: se documenta la causa de la falla, la acción correctiva y el cambio en el procedimiento de despliegue, para que no se repita.

RTO y RPO estimados

RTO (Recovery Time Objective): 4 horas.
RPO (Recovery Point Objective): 24 horas, asumiendo respaldos diarios de la configuración.
