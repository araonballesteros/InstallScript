# Script de instalación de [Odoo](https://www.odoo.com)

Este script está basado en el instalador de André Schenkels (https://github.com/aschenkels-ictstudio/openerp-install-scripts) y ha sido adaptado por SofBiz Technologies para Odoo 18 Community Edition. Permite definir el puerto xmlrpc en el archivo `.conf` generado en `/etc/`, por lo que puede utilizarse en servidores con varias instancias de Odoo.

## Instalación de Nginx
Si establece el parámetro `INSTALL_NGINX` en `True` también debe configurar los workers. Sin ellos es probable que tenga pérdidas de conexión. Consulte la [guía de despliegue de Odoo](https://www.odoo.com/documentation/18.0/administration/install/deploy.html) para configurarlos.

## Procedimiento de instalación

1. Descargue el script:
```
sudo wget https://raw.githubusercontent.com/Yenthe666/InstallScript/18.0/odoo_install.sh
```
2. Modifique los parámetros según sus necesidades. Los más habituales son:
`OE_USER` será el usuario del sistema.
`GENERATE_RANDOM_PASSWORD` genera una contraseña aleatoria si está en `True`; si está en `False` se utilizará la definida en `OE_SUPERADMIN`.
`INSTALL_WKHTMLTOPDF` póngalo en `False` si no desea instalar Wkhtmltopdf.
`OE_PORT` es el puerto donde se ejecutará Odoo (ejemplo 8069).
`OE_VERSION` versión de Odoo a instalar, por defecto `18.0`.
`IS_ENTERPRISE` instala la versión Enterprise si se establece en `True`, en caso contrario instala la Community.
`OE_SUPERADMIN` contraseña maestra de Odoo.
`INSTALL_NGINX` está en `False` por defecto. Cámbielo a `True` para instalar Nginx.
`WEBSITE_NAME` nombre del sitio web para la configuración de Nginx.
`ENABLE_SSL` instala certbot y configura https si se establece en `True`.
`ADMIN_EMAIL` correo utilizado para registrar Let's Encrypt.
`INSTALL_NGINX` y `ENABLE_SSL` deben estar en `True` y `ADMIN_EMAIL` debe contener un email válido para que certbot se instale.
_Al habilitar SSL mediante Let's Encrypt acepta sus [políticas](https://www.eff.org/code/privacy/policy)._ 

3. Haga ejecutable el script:
```
sudo chmod +x odoo_install.sh
```
4. Ejecute el script:
```
sudo ./odoo_install.sh
```

## ¿Dónde hospedar Odoo?
Existen numerosos servicios con buen rendimiento. El script se ha probado con [Google Cloud](https://cloud.google.com/), [Hetzner](https://www.hetzner.com/), [Amazon AWS](https://aws.amazon.com/) y [DigitalOcean](https://www.digitalocean.com/products/droplets/). Puede usar este [enlace de referencia de DigitalOcean](https://m.do.co/c/d605cc420682) que ofrece 200$ de crédito durante los primeros 60 días.

## Requisitos mínimos del servidor
Aunque técnicamente es posible ejecutar Odoo con 1GB de RAM no se recomienda. Una distribución Linux consume entre 300MB y 500MB y el resto debe repartirse entre Odoo, PostgreSQL y otros servicios. Utilice al menos 2GB de RAM. De lo contrario la instalación podría fallar. Se conocen problemas en DigitalOcean al instalar en máquinas de 1GB de RAM. Consulte https://github.com/Yenthe666/InstallScript/issues/243
