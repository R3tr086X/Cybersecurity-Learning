# Nginx Hardening & Advanced Configuration

## APARTADO 1 – Configuración Inicial del Servidor

### Configuración del puerto de escucha
Se modifica la configuración por defecto de Nginx para que el servidor deje de escuchar en el puerto 80 y utilice un puerto personalizado. Esta medida reduce la exposición frente a escaneos automáticos y añade una capa básica de ocultación del servicio.  
![Configuración puerto](images/image1.png)

### Configuración de la página de inicio
Se edita el archivo `/var/www/html/index.html` para personalizar la página principal del servidor. El contenido refleja que el servidor está correctamente configurado, securizado y funcionando en el nuevo puerto establecido.  
![Página de inicio 1](images/image2.png)  
![Página de inicio 2](images/image3.png)

---

## APARTADO 2 – Server Blocks (Sitio Web Virtual)

### Creamos el index.html
Se crea un archivo `index.html` específico para el nuevo sitio virtual, incluyendo contenido identificativo que permita diferenciarlo del sitio por defecto.  
![Index HTML](images/image4.png)

### Raíz propia
Se define una raíz de documentos independiente para el nuevo Server Block en `/var/www/[USER]/public_html`, garantizando separación lógica entre sitios y mejor organización del contenido.  
![Raíz propia](images/image5.png)

### Hacemos el enlace
Se habilita el nuevo sitio creando el enlace simbólico correspondiente desde `sites-available` hacia `sites-enabled`, activando así el Server Block en Nginx.  
![Enlace sitio](images/image6.png)

### Añadimos el sitio al archivo hosts
Se añade una entrada en el archivo `/etc/hosts` del servidor para asociar el dominio virtual con la dirección IP local, permitiendo su correcta resolución interna.  
![Hosts servidor](images/image7.png)

### Modificamos el archivo hosts de nuestro Windows para poder acceder a la página
Se edita el archivo `hosts` del sistema Windows para que el dominio configurado apunte a la IP del servidor. Esto permite acceder al sitio virtual desde el navegador del equipo cliente.  
![Hosts Windows](images/image8.png)

---

## APARTADO 3 – Hardening del Servidor

### Ocultación de versión, prevención de DoS y cabecera anti-clickjacking
Se aplica la directiva `server_tokens off` para ocultar la versión de Nginx en las cabeceras HTTP y páginas de error.  
Se limita el tamaño máximo de subida de archivos mediante `client_max_body_size` para evitar ataques de denegación de servicio basados en consumo de almacenamiento.  
Además, se añade la cabecera de seguridad `X-Frame-Options SAMEORIGIN` para mitigar ataques de clickjacking.  
![Hardening 1](images/image9.png)

### Ocultar listado de directorios
Se deshabilita la directiva `autoindex` para impedir que el servidor muestre el contenido de directorios cuando no exista un archivo `index.html`, evitando la exposición innecesaria de archivos internos.  
![Autoindex off](images/image10.png)

### Hacemos las comprobaciones
Se realizan pruebas accediendo a rutas específicas y revisando las cabeceras HTTP para verificar que las medidas de seguridad aplicadas funcionan correctamente.  
![Comprobaciones](images/image11.png)

---

## APARTADO 4 – Control de Acceso y Restricciones

### Protección por IP (acceso restringido)
Se crea una ubicación específica (`/config`) restringida mediante directivas `allow` y `deny`, permitiendo el acceso únicamente a las direcciones IP autorizadas y bloqueando el resto con error 403 Forbidden.  
![Protección IP](images/image12.png)

### Autenticación por contraseña
Se protege la ruta `/admin` mediante autenticación básica HTTP. Se genera un archivo de credenciales utilizando `htpasswd` y se configura Nginx para exigir usuario y contraseña antes de conceder acceso.  
![Autenticación 1](images/image13.png)  
![Autenticación 2](images/image14.png)

### Hacemos las comprobaciones
Se realizan pruebas de acceso desde direcciones IP permitidas y no permitidas, así como intentos de autenticación correctos e incorrectos, verificando que el control de acceso se aplica correctamente.  
![Comprobación 1](images/image15.png)  
![Comprobación 2](images/image16.png)

---

## APARTADO 5 – Reglas de Seguridad Avanzada

### Creamos el archivo de error personalizado
Se diseña un archivo `error404.html` personalizado para sustituir la página de error predeterminada de Nginx, ofreciendo una respuesta más profesional y adaptada al entorno.  
![Error personalizado](images/image17.png)

### Añadimos el archivo al site
Se configura la directiva `error_page` en el Server Block correspondiente para que el servidor muestre el archivo personalizado cuando se solicite un recurso inexistente.  
![Añadir error_page](images/image18.png)

### Bloqueo por User-Agent
Se implementa una regla que detecta solicitudes provenientes de herramientas como `curl` y deniega el acceso con código 403. De este modo, solo se permite el acceso desde navegadores convencionales.  
![Bloqueo User-Agent](images/image19.png)

### Hacemos las comprobaciones
Se realizan pruebas utilizando distintos User-Agents y solicitando recursos inexistentes para verificar el correcto funcionamiento del bloqueo y la página de error personalizada.  
![Comprobaciones finales](images/image20.png)
