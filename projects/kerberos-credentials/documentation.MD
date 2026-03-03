# DOCUMENTACIÓN

## Personalización de las máquinas

- **Establecemos la IP del Windows Server**  
  Configuramos una dirección IP estática en el servidor Windows para asegurar conectividad consistente y evitar conflictos de red.  
  ![img1](images/img1.jpg)

- **Equipo controlador del dominio**  
  Verificamos que el servidor funciona como controlador de dominio, gestionando usuarios y políticas de seguridad para el entorno de pruebas.  
  ![img2](images/img2.jpg)

- **Usuarios creados**  
  Creamos los usuarios necesarios para simular accesos distintos y pruebas de autenticación en el dominio.  
  ![img3](images/img3.jpg)

- **Comprobamos que están los servicios necesarios**  
  Revisamos que servicios como Active Directory, Kerberos y DNS estén activos y funcionando correctamente.  
  ![img4](images/img4.jpg)

- **En Debian añadimos la interfaz estática**  
  Configuramos la IP estática en la máquina cliente para que pueda comunicarse de forma confiable con el servidor.  
  ![img5](images/img5.jpg)

- **Apuntamos al Windows Server**  
  Configuramos el DNS y la ruta hacia el controlador de dominio para que el cliente reconozca y confíe en el servidor.  
  ![img6](images/img6.jpg)

---

## APARTADO 1: Preparación y bastionado del cliente

- **Instalamos los paquetes y configuramos Kerberos**  
  Instalamos herramientas necesarias para la integración con el dominio, gestión de usuarios y tickets Kerberos.  
  ![img7](images/img7.jpg)

- **Configuramos la sincronización horaria**  
  Ajustamos la hora de Debian para que coincida con la del servidor, ya que Kerberos utiliza marcas de tiempo para validar los tickets y prevenir ataques de repetición.  
  ![img8](images/img8.jpg)

---

## APARTADO 2: Unión al dominio e identidad

- **Configuración de Kerberos**  
  Editamos los archivos de configuración para que la máquina cliente reconozca el dominio y pueda solicitar tickets de autenticación.  
  ![img9](images/img9.jpg)

- **Configuramos los permisos**  
  Aseguramos que los archivos de configuración solo puedan ser leídos y modificados por el usuario root, protegiendo información sensible del dominio.  
  ![img10](images/img10.jpg)

- **Nos unimos al dominio**  
  Ejecutamos los comandos necesarios para registrar la máquina Debian en el dominio y permitir la autenticación centralizada.  
  ![img11](images/img11.jpg)

- **Configuramos el SSSD**  
  Definimos dominios, usuarios y políticas de caché de autenticación en `sssd.conf` para que el sistema cliente pueda consultar al controlador de dominio.  
  ![img12](images/img12.jpg)

- **Establecemos los permisos**  
  Confirmamos que los permisos de los archivos de configuración sean restrictivos y solo accesibles por root.  
  ![img13](images/img13.jpg)

- **Hacemos las comprobaciones del Realm y el dominio, todo correcto**  
  Verificamos que el cliente reconoce correctamente el dominio y que los usuarios pueden autenticarse sin problemas.  
  ![img14](images/img14.jpg)

---

## APARTADO 3: Ciclo de vida de las credenciales

- **Usamos los comandos principales para gestionar el acceso a Kerberos**  
  Ejecutamos los comandos principales para solicitar, consultar y eliminar tickets de Kerberos, asegurando que las credenciales se gestionan de forma segura:  
  - `kinit`: Solicita un ticket inicial.  
  - `klist`: Lista los tickets activos y su expiración.  
  - `kdestroy`: Borra las credenciales de la caché para mantener la seguridad.  
  ![img15](images/img15.jpg)

---

## APARTADO 4: Acceso a recursos y Single Sign-On

- **Creamos la carpeta compartida**  
  Configuramos un recurso compartido en el servidor para probar el acceso remoto desde el cliente.  
  ![img16](images/img16.jpg)

- **Creamos un archivo de prueba**  
  Generamos un archivo de ejemplo en la carpeta compartida para verificar permisos y accesibilidad.  
  ![img17](images/img17.jpg)

- **Pedimos el ticket**  
  Solicitamos un ticket Kerberos desde el cliente para poder acceder al recurso compartido sin introducir contraseña.  
  ![img18](images/img18.jpg)

- **Añadimos servicios necesarios**  
  Configuramos servicios adicionales que permiten la autenticación SSO en el entorno de pruebas.  
  ![img19](images/img19.jpg)

- **Añadimos el host**  
  Registramos el host del servidor para que el cliente lo reconozca en el contexto de Kerberos.  
  ![img20](images/img20.jpg)

- **Al pedir el ticket con -k, da error**  
  Probamos `smbclient -k` y documentamos el error, mostrando cómo Kerberos responde ante configuraciones incorrectas o desfases de tiempo.  
  ![img21](images/img21.jpg)

- **Accedemos al recurso compartido correctamente**  
  Tras ajustes, el cliente logra acceder al recurso utilizando SSO, demostrando el funcionamiento seguro de Kerberos.  
  ![img22](images/img22.jpg)

---

## APARTADO 5: Bastionado mediante GPO de Kerberos

- **Aplicamos la restricción en el servidor**  
  Configuramos el desfase máximo permitido en Kerberos para endurecer la seguridad y prevenir el uso de tickets antiguos.  
  ![img23](images/img23.jpg)

- **Editamos la configuración de sincronización de tiempo**  
  Ajustamos manualmente la hora en el cliente para simular desfases y verificar que los tickets expiran correctamente.  
  ![img24](images/img24.jpg)

- **Realizamos el proceso y se produce el error esperado**  
  Al solicitar un ticket con desfase de tiempo, Kerberos falla correctamente, demostrando que el sistema está correctamente bastionado.  
  ![img25](images/img25.jpg)
