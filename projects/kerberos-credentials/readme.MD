# Kerberos Identity Hardening / Bastionado de identidad con Kerberos

---

## Español

### Descripción

Documentación de la implementación de un sistema de autenticación centralizado y seguro usando **Kerberos** en un entorno Windows/Linux.

### Escenario

- **Servidor:** Windows Server con Active Directory  
- **Cliente:** Linux (Debian) con SSSD y Kerberos configurados  

### Pasos clave

1. Instalación y bastionado del cliente Linux  
2. Unión al dominio y configuración de SSSD con permisos restrictivos  
3. Gestión del ciclo de vida de credenciales (`kinit`, `klist`, `kdestroy`)  
4. Acceso a recursos compartidos con Single Sign-On (SSO)  
5. Bastionado mediante políticas de Kerberos y reducción del desfase de tiempo  

---

## English

### Description

Documentation of the implementation of a centralized and secure authentication system using **Kerberos** in a Windows/Linux environment.

### Scenario

- **Server:** Windows Server with Active Directory  
- **Client:** Linux (Debian) with SSSD and Kerberos configured  

### Key Steps

1. Linux client installation and hardening  
2. Domain joining and SSSD configuration with restrictive permissions  
3. Credential lifecycle management (`kinit`, `klist`, `kdestroy`)  
4. Access to shared resources using Single Sign-On (SSO)  
5. Hardening via Kerberos policies and reduced clock skew  
