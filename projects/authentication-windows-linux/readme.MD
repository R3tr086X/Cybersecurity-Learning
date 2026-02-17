# Authentication Hardening in Linux & Windows / Bastionado de Autenticación en Linux y Windows

---

## Español

### Descripción

Documentación de la implementación y hardening de sistemas de autenticación en entornos Linux (Debian) y Windows Server (Active Directory). Se aplican políticas de contraseñas, bloqueo de cuentas y autenticación multifactor para asegurar el acceso local y remoto.

### Linux (Debian)

- Configuración de políticas de contraseñas con PAM: longitud mínima, complejidad y restricciones de secuencias.  
- Bloqueo de cuentas tras múltiples intentos fallidos.  
- Habilitación de 2FA (OTP) en SSH manteniendo acceso local por contraseña.  
- Hardening de SSH: deshabilitación de root, acceso restringido a usuarios autorizados.  

### Windows Server

- Configuración de GPO para políticas de contraseñas y bloqueo de cuentas.  
- Restricción de acceso remoto solo a administradores y usuarios autorizados.  
- Integración de clientes Windows al dominio y validación del Single Sign-On.  

---

## English

### Description

Documentation for implementing and hardening authentication systems in Linux (Debian) and Windows Server (Active Directory). Password policies, account lockout, and multifactor authentication are applied to secure local and remote access.

### Linux (Debian)

- Password policies configured via PAM: minimum length, complexity, and sequence restrictions.  
- Account lockout after consecutive failed login attempts.  
- 2FA (OTP) enabled for SSH while preserving local password access.  
- SSH hardening: root login disabled, access restricted to authorized users.  

### Windows Server

- GPO configuration for password policies and account lockout.  
- Remote access restricted to administrators and authorized users.  
- Client machines joined to the domain and Single Sign-On validated.  
