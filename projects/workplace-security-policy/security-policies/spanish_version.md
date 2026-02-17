# Políticas de Seguridad en el Puesto de Trabajo

---

## Puestos de Trabajo Analizados

### Puesto Directivo

Los directivos poseen altos privilegios y acceso a información crítica, lo que implica un riesgo considerable. Su movilidad y acceso remoto requieren políticas de seguridad robustas para proteger los activos sensibles.

**Activos utilizados:**
- Portátil, móvil y tablet corporativos
- Credenciales con privilegios elevados
- Acceso remoto a correo, ERP y documentación sensible

---

### Puesto Tienda Online

Este puesto se encarga del contacto directo con los clientes externos. La exposición a Internet y la gestión de datos personales son esenciales, lo que conlleva riesgos importantes de seguridad.

**Activos utilizados:**
- PC de atención al cliente
- Datos de clientes y pedidos
- Navegador, correo electrónico y acceso parcial al ERP

---

### Puesto Administrativo

El puesto administrativo tiene acceso a datos sensibles y sistemas centrales, lo que implica riesgos elevados. Es fundamental implementar políticas de seguridad para proteger la información personal y la facturación.

**Activos utilizados:**
- PC fijo
- Impresora compartida
- Documentos impresos con datos sensibles
- Software de oficina

---

## Análisis A.A.V.R.

### Directivos

Este análisis destaca las vulnerabilidades y amenazas que enfrentan los directivos, incluyendo el acceso a información sensible y los riesgos asociados a la pérdida de dispositivos móviles en entornos públicos.

- **Activos:** dispositivos móviles, credenciales, documentos estratégicos  
- **Riesgos:** fuga de información, fraude económico, daños reputacionales  
- **Escenario real:** pérdida del móvil en un aeropuerto → acceso total a correo y documentos

### Tienda Online

La tienda online enfrenta amenazas significativas como malware y ataques de ingeniería social, lo que puede resultar en la fuga de datos de clientes y pérdida de confianza en la marca.

- **Amenazas principales:** malware por adjuntos, webs falsas, ingeniería social  
- **Riesgos:** fuga de datos de clientes, pérdida de confianza, acceso al ERP  
- **Escenario real:** cliente envía archivo infectado como justificante de pago

### Administrativo

El puesto administrativo presenta riesgos significativos debido al acceso a datos sensibles y la posibilidad de accesos no autorizados, lo que podría resultar en incumplimientos legales y vulnerabilidades de seguridad.

- **Amenazas:** accesos físicos no autorizados, USBs infectados, ransomware  
- **Riesgos:** incumplimiento RGPD, pérdida de integridad de facturas  
- **Escenario real:** PC desbloqueado visible al público con datos de clientes

---

## Principios de Seguridad

### Contraseñas Fuertes

Utilizar contraseñas complejas que incluyan letras mayúsculas, minúsculas, números y símbolos para asegurar que sean difíciles de adivinar y proteger el acceso a la información.

### Autenticación Multifactor (MFA)

Implementar MFA añade una capa adicional de seguridad, requiriendo que los usuarios verifiquen su identidad a través de múltiples métodos antes de acceder a las cuentas.

### Uso Seguro del Correo

Mantener un uso responsable del correo electrónico es crucial; esto incluye no abrir correos de remitentes desconocidos y evitar hacer clic en enlaces sospechosos.

---

## Políticas Generales

### Formación

La formación en phishing y seguridad es esencial para educar a los empleados sobre cómo identificar correos electrónicos y enlaces maliciosos, reduciendo el riesgo de ataques cibernéticos exitosos.

### Confidencialidad

Controlar los accesos a la información sensible, garantizando que solo el personal autorizado pueda visualizar o manipular datos críticos.

### Integridad

Proteger los datos mediante medidas de seguridad, como antivirus y actualizaciones regulares, previniendo malware y asegurando que la información permanezca intacta.

### Disponibilidad

- **Copias de seguridad:** garantizar recuperación de datos críticos en caso de ataque.  
- **Actualizaciones de software:** proteger sistemas contra vulnerabilidades.  
- **Formación continua:** preparar a empleados para identificar y evitar amenazas.

---

## Políticas Específicas por Puesto

### Directivos

- Cifrado completo de dispositivos  
- Uso obligatorio de VPN para acceso remoto  

### Tienda Online

- Navegación segura y uso de HTTPS  
- Bloqueo de descargas no autorizadas  
- Segmentación de red para aislar sistemas críticos  

### Administrativo

- Escritorio limpio y pantalla bloqueada  
- Prohibición de USBs no autorizados  
- Protección de información sensible en documentos físicos y digitales

---

## Checklist de Verificación

### Directivos

- ¿El dispositivo está cifrado?  
- ¿Usa MFA en todos los accesos?  
- ¿Está inscrito el móvil en MDM?  
- ¿Usa VPN fuera de la sede?  
- ¿Ha recibido formación contra phishing?  
- ¿Se verifica cumplimiento cada 6 meses?

### Administrativo

- ¿PC se bloquea automáticamente?  
- ¿No están habilitados USBs no autorizados?  
- ¿Documentos impresos se guardan o destruyen?  
- ¿Pantalla no visible desde el público?  
- ¿Empleado formado en phishing?  
- ¿Accesos limitados a ventas/facturación?

### Tienda Online

- ¿Se usa MFA en acceso a la tienda?  
- ¿Antivirus activo y actualizado?  
- ¿Navegador actualizado?  
- ¿Puesto en subred aislada?  
- ¿Empleado sigue procedimiento de no abrir adjuntos externos?  
- ¿Pantalla no visible al público?

---

## Preguntas Frecuentes

- **¿Por qué no usar dispositivos personales como USBs o discos externos?**  
  Pueden contener malware y suponer una vía directa de infección para los sistemas corporativos.

- **¿Qué pasa si cometo un error sin intención?**  
  Comunicarlo inmediatamente puede evitar que el incidente se agrave.

- **¿Estas políticas aplican bajo presión o prisas?**  
  Sí. Los atacantes aprovechan el estrés, por lo que cumplir las políticas siempre es clave.

---

## Consecuencias de Incumplir

- **Sanciones internas:** desde advertencias hasta pérdida de acceso a sistemas.  
- **Pérdida de confianza:** daña la reputación y relaciones dentro de la organización.  
- **Riesgos globales:** incrementa la exposición a ciberataques y pone en peligro los datos de la empresa.

---

## Resumen de Buenas Prácticas

- Bloquear siempre el equipo al ausentarse  
- Usar contraseñas seguras y MFA  
- Revisar correos cuidadosamente y no abrir adjuntos sospechosos  
- Mantener escritorio limpio y proteger información sensible  
- Utilizar solo dispositivos y software autorizados  
- Notificar cualquier incidente inmediatamente

