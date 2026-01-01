# Análisis de Tráfico de Red con tcpdump 

Este proyecto documenta una práctica de laboratorio de ciberseguridad enfocada en la captura y análisis de paquetes en un entorno Linux. Se exploran técnicas para identificar interfaces de red, filtrar tráfico en vivo y realizar análisis forense básico sobre archivos de captura.

##  Tabla de Contenidos
- [Escenario](#escenario)
- [Tareas Realizadas](#tareas-realizadas)
- [Guía de Ejecución](#guía-de-ejecución)
- [Conclusiones](#conclusiones)

##  Escenario
Como analista de seguridad, se requiere capturar y analizar el tráfico de red de una máquina virtual Linux para identificar posibles anomalías. El objetivo es filtrar tráfico específico (HTTP/Puerto 80) y examinar el contenido de los paquetes para entender la comunicación entre sistemas.

##  Tareas Realizadas
1. **Identificación de interfaces:** Localización de la interfaz activa para la escucha.
2. **Inspección en vivo:** Uso de filtros para limitar la captura de paquetes.
3. **Persistencia de datos:** Generación de archivos `.pcap` (Packet Capture).
4. **Análisis de carga útil:** Inspección de datos en formatos Hexadecimal y ASCII.

##  Guía de Ejecución

### Fase 1: Identificación de Interfaces
Primero, listamos las interfaces disponibles en el sistema para determinar dónde capturar:
```bash
sudo tcpdump -D
```
### Fase 2: Filtrado en Tiempo Real
Capturamos una muestra pequeña (5 paquetes) de forma detallada en la interfaz eth0:

```bash
sudo tcpdump -i eth0 -v -c5
```
### Fase 3: Captura y Guardado de Tráfico
Filtramos únicamente el tráfico del puerto 80 (HTTP) y lo guardamos en un archivo para análisis posterior:

```bash
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
```
Generamos tráfico de prueba usando curl:
```bash
curl opensource.google.com
```
## Fase 4: Análisis del Archivo PCAP
Leemos el archivo guardado utilizando el modo de inspección profunda:

```bash
sudo tcpdump -nn -r capture.pcap -X
```

# Conclusiones
La herramienta tcpdump es esencial para cualquier analista de seguridad. Permite no solo monitorear la red, sino también documentar incidentes mediante archivos PCAP que pueden ser analizados posteriormente con herramientas más avanzadas como Wireshark.
