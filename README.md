# monitor-wms
Monitor de servicios WMS que alerta vía mail cuando alguno está caído.

1. Verificar que este instalado php5 o superior
1. Instalar drivers para sqlite (Ej: `apt-get install php5-sqlite`)
1. Configurar en `config/config-mail.php` los parátros de phpmailer (host, puerto, smtpSecure, usuario, contraseña,setFrom) y la ruta completa donde estámplementado el servicio 
1. Debe existir el directorio `capabilities/` (donde guarda el doc capabilities de cada servidor)
1. Ejecutar la primera vez el script `monitor.php` mediante linea de comandos
1. Ejecutar la primera vez el script `mails.php` mediante linea de comandos
1. Ubicar archivos de la carpeta `crons/` (ver README)

## Prueba de mail

Para probar si se estan enviando las notificaciones via mail, cambiar la variable $test_mail = true en el archivo monitor.php
Al hacer esto no se comprobará ninguno de los servidores, sólo se envia un mail de prueba.

# Protocolo de verificación:
1. Extrae los servicios de IDERA desde http://servicios.idera.gob.ar/geoservicios/sources.json.
2. Intenta descargar el catálogo de cada servicio.
    * Si se descarga el xml del servicio la aplicación asume que el servidor funciona
    * Si no se descarga el xml del servicio:
        * consulta la tabla emails y extrae el email del proveedor
        * si existe mail envía al proveedor la notificación de servidor caído, sino lo envía al administrador de IDERA
