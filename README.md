# test_web
repo de codigo, para las pruebas y experimentos de Tona, Charly y Carlos

Resumen de pasos que dio Chat GPT:


Claro, aquí tienes un texto detallado para incluir en un archivo README.md que describe los pasos necesarios para crear y montar una página web en Apache en un puerto específico (8082) en Ubuntu:

markdown
Copiar código
# Configuración de una Página Web en Apache en el Puerto 8082

Este documento describe los pasos para crear y montar una página web en Apache utilizando el puerto 8082 en un servidor Ubuntu.

## Pasos para Configurar la Página Web

### 1. Instalar Apache
Asegúrate de que Apache esté instalado en tu servidor Ubuntu.

bash
sudo apt update
sudo apt install apache2

2. Configurar Apache para Escuchar en el Puerto 8082
Edita el archivo ports.conf para agregar el puerto 8082.

bash
sudo nano /etc/apache2/ports.conf
Agrega la siguiente línea:

plaintext
Listen 8082

3. Crear un Nuevo Archivo de Configuración de Sitio Virtual
Crea un nuevo archivo de configuración para tu sitio web.

bash
sudo nano /etc/apache2/sites-available/mywebsite.conf
Agrega la siguiente configuración:

plaintext
<VirtualHost *:8082>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/mywebsite

    <Directory /var/www/mywebsite>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/mywebsite_error.log
    CustomLog ${APACHE_LOG_DIR}/mywebsite_access.log combined
</VirtualHost>

4. Crear el Directorio del Sitio Web
Crea el directorio donde se almacenará tu página web.

bash
sudo mkdir /var/www/mywebsite

5. Agregar Contenido HTML al Directorio del Sitio Web
Crea un archivo HTML dentro de tu nuevo directorio del sitio web.

bash
sudo nano /var/www/mywebsite/index.html
Agrega el siguiente contenido HTML:

html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Nueva Página en el Puerto 8082</title>
</head>
<body>
    <h1>¡Bienvenido a mi nueva página web en el puerto 8082!</h1>
    <p>Esta es una página de ejemplo servida por Apache en el puerto 8082 en Ubuntu.</p>
</body>
</html>

6. Configurar Permisos del Directorio
Asegúrate de que los permisos del directorio y los archivos sean correctos.

bash
sudo chown -R www-data:www-data /var/www/mywebsite
sudo chmod -R 755 /var/www/mywebsite

7. Habilitar el Nuevo Sitio Web
Habilita el nuevo sitio web utilizando a2ensite.

bash
sudo a2ensite mywebsite.conf
Deshabilita y vuelve a habilitar el sitio para asegurar que los cambios se apliquen correctamente.

bash
sudo a2dissite mywebsite.conf
sudo a2ensite mywebsite.conf

8. Reiniciar Apache
Reinicia el servicio de Apache para aplicar los cambios.

bash
sudo systemctl restart apache2

9. Abrir el Nuevo Puerto en el Firewall
Si estás utilizando ufw, permite el tráfico en el puerto 8082.

bash
sudo ufw allow 8082

10. Acceder a tu Página Web
Abre un navegador web y visita la dirección IP de tu servidor seguida del puerto 8082.

http
http://your_server_ip:8082

11. Verificar el Estado de Apache
Asegúrate de que Apache esté corriendo sin errores.

bash
sudo systemctl status apache2

12. Revisar los Logs de Apache (si es necesario)
Si encuentras problemas, revisa los logs de Apache para obtener más detalles.

bash
sudo tail -f /var/log/apache2/error.log
sudo tail -f /var/log/apache2/mywebsite_error.log
Siguiendo estos pasos, deberías poder montar y acceder a tu nueva página web en Apache utilizando el puerto 8082.

css
Este documento proporciona una guía completa y detallada para configurar una página web en Apache en el puerto 8082, cubriendo todos los aspectos necesarios para asegurar una configuración exitosa.
