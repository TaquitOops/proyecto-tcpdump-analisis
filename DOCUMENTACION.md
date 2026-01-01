# Documentación Técnica: tcpdump

Este documento proporciona un desglose técnico de los comandos y parámetros utilizados durante la práctica de análisis de red.

##  Referencia de Comandos (Flags)

| Parámetro | Función | Justificación Técnica |
| :--- | :--- | :--- |
| `-i [interfaz]` | Interface | Define en qué dispositivo de red se escuchará el tráfico. |
| `-v` | Verbose | Aumenta el detalle del reporte (TTL, IDs, longitud de encabezado). |
| `-c [n]` | Count | Limita la captura a 'n' paquetes. Evita el llenado innecesario de memoria. |
| `-nn` | No Name Lookup | Desactiva la resolución de nombres (DNS). Es más rápido y evita alertar a atacantes. |
| `-w [nombre]` | Write | Exporta los datos crudos a un archivo binario compatible con otras herramientas. |
| `-r [nombre]` | Read | Lee y procesa un archivo de captura previamente guardado. |
| `-X` | Hex/ASCII | Muestra el contenido del paquete (Payload). Vital para detectar malware. |

---

##  Anatomía de la Salida de tcpdump

Al analizar un paquete capturado, se identifican los siguientes campos críticos:

1. **Timestamp:** La hora exacta (`10:57:33.427749`) útil para líneas de tiempo en incidentes.
2. **Protocolo:** IP y el protocolo interno (TCP/UDP/ICMP).
3. **Flujo de Tráfico:** `Origen.Puerto > Destino.Puerto`.
4. **Flags TCP:**
   - `[S]`: SYN (Inicio de conexión).
   - `[P]`: PUSH (Envío de datos).
   - `[.]`: ACK (Agradecimiento/Confirmación).
5. **Checksum:** Utilizado para verificar que el paquete no fue alterado o dañado.

##  Mejores Prácticas Aplicadas
- **Uso de sudo:** `tcpdump` requiere privilegios de superusuario ya que pone la interfaz en modo promiscuo.
- **Filtrado por Puerto:** El uso de `port 80` reduce el "ruido" en la captura, permitiendo al analista enfocarse en el tráfico relevante.
- **Análisis Offline:** Leer archivos guardados (`-r`) permite realizar análisis detallados sin afectar el rendimiento de la red en tiempo real.
