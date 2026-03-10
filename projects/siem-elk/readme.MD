# Implantación de un SIEM con ELK

## Introducción

El objetivo de esta práctica es la implantación de un SIEM (Security Information and Event Management) basado en la pila ELK (Elasticsearch, Logstash, Kibana), desplegado íntegramente en Docker. Sobre este entorno se ha simulado un incidente de seguridad consistente en un flood ICMP, demostrando que el sistema es capaz de detectar, ingestar y visualizar el ataque en tiempo real.

---

## Arquitectura del entorno

El entorno está compuesto por seis contenedores Docker que se comunican a través de una red interna (`siem-net`, subred `172.20.0.0/24`):

**Elasticsearch** actúa como base de datos y motor de búsqueda. Almacena todos los eventos indexados y permite consultarlos de forma eficiente. Se despliega en modo single-node con la seguridad desactivada para simplificar el entorno de laboratorio.

**Kibana** es la interfaz web de visualización. Permite explorar los logs almacenados en Elasticsearch, crear búsquedas y visualizar patrones de eventos en el tiempo.

**Logstash** es el motor de procesamiento de logs. Recibe los eventos desde Filebeat a través del puerto 5044, los parsea mediante una expresión grok para extraer campos estructurados (IP origen, IP destino, tipo de mensaje ICMP) y los envía indexados a Elasticsearch.

**Filebeat** es el agente de ingesta ligero. Monitoriza en tiempo real el fichero `/var/log/icmp.log` de la víctima y reenvía cada nueva línea a Logstash.

**Víctima** es un contenedor Alpine Linux que ejecuta `tcpdump` de forma continua. Captura todos los paquetes ICMP que llegan a su interfaz de red y escribe cada evento en el fichero `/var/log/icmp.log`.

**Atacante** es un contenedor Alpine Linux que ejecuta un flood ICMP contra la víctima (`172.20.0.10`), enviando una ráfaga de paquetes ping en un intervalo muy corto.

---

## Flujo de los logs

El recorrido completo de un evento desde que se genera hasta que es visible en Kibana es el siguiente:

1. El atacante lanza pings contra la víctima (`172.20.0.10`)
2. `tcpdump` en la víctima detecta cada paquete ICMP y escribe una línea en `/var/log/icmp.log`
3. Filebeat detecta la nueva línea y la envía a Logstash por el puerto 5044
4. Logstash parsea la línea con grok, extrayendo `ip_origen`, `ip_destino` e `icmp_tipo`, y asigna el timestamp actual
5. Logstash indexa el documento en Elasticsearch bajo el índice `icmp-logs-YYYY.MM.dd`
6. Kibana consulta Elasticsearch y muestra los eventos en Discover

---

## Incidente simulado — Flood ICMP

El incidente elegido es un flood ICMP, también conocido como ping flood. Consiste en el envío masivo y continuo de paquetes ICMP echo request desde el atacante hacia la víctima en un intervalo de tiempo muy corto.

Este tipo de ataque es relevante desde el punto de vista de la seguridad porque puede utilizarse como técnica de reconocimiento, denegación de servicio (DoS) o simplemente como prueba de conectividad masiva no autorizada. En un entorno real, un patrón de cientos de pings por segundo desde una misma IP hacia un host es una señal clara de actividad maliciosa o anómala.

El ataque se ejecuta con el siguiente comando:

```bash
docker compose --profile ataque run --rm atacante
```

Esto lanza el contenedor atacante, que ejecuta el comando ping directamente desde una imagen Alpine Linux, enviando paquetes ICMP con un intervalo de 10ms entre cada uno.

---

## Evidencias en Kibana

### Contenedores en ejecución

![docker compose ps mostrando todos los contenedores en running](img1.jpg)

### Ejecución del ataque

![terminal con la ejecución del ataque](img2.jpg)

### Histograma de eventos en Kibana

![Kibana Discover con el histograma mostrando el pico de eventos](img3.jpg)

### Tabla con campos estructurados

![tabla con columnas ip_origen, ip_destino, icmp_tipo](img4.jpg)

### Detalle de un evento

![detalle de un evento expandido con todos los campos](img5.jpg) (img6.jpg)

### Múltiples ataques — picos en la gráfica

![ejemplo de varios ataques mostrando los picos en la gráfica](img7.jpg)

### Configuración de la cantidad de paquetes

![configuración de la cantidad de paquetes en el docker-compose.yml](img8.jpg)

### Data view configurado

![data view configurado en Kibana](img9.jpg)

En Kibana se puede observar claramente el patrón del incidente. El histograma de Discover muestra un pico pronunciado de eventos concentrado en el intervalo de tiempo en que se ejecutó el ataque. Cada evento contiene los siguientes campos clave:

- `ip_origen`: dirección IP del atacante (`172.20.0.6`)
- `ip_destino`: dirección IP de la víctima (`172.20.0.10`)
- `icmp_tipo`: tipo de mensaje ICMP (`echo request` o `echo reply`)
- `@timestamp`: momento exacto en que se registró el evento

La combinación del pico temporal en el histograma y la concentración de eventos con la misma IP origen permite identificar inequívocamente el incidente.

---

## Conclusión

El entorno SIEM desplegado cumple con todos los requisitos de la práctica. Los logs generados por la víctima llegan correctamente a Elasticsearch a través de Filebeat y Logstash, y son visualizables en Kibana con los campos estructurados necesarios para identificar el origen, tipo y momento del incidente. El flood ICMP queda reflejado de forma clara en el histograma de Discover, evidenciando el patrón característico de un ataque de este tipo.
