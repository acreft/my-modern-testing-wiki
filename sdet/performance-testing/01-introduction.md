# Introducción

El Performance Testing evalúa cómo responde un sistema bajo diferentes condiciones de carga, midiendo atributos no funcionales como tiempo de respuesta, estabilidad, escalabilidad y uso de recursos.
Según ISTQB®, es parte de las pruebas de calidad no funcional, clave para aplicaciones con alto volumen de usuarios.

# Objetivos

- Identificar cuellos de botella.

- Verificar cumplimiento de SLAs (Service Level Agreements).

- Validar escalabilidad (cómo se comporta al aumentar la carga).

- Garantizar estabilidad a largo plazo.

# Tipos de pruebas de rendimiento

- Load Testing → rendimiento bajo carga esperada.

- Stress Testing → comportamiento en condiciones extremas.

- Spike Testing → respuesta ante incrementos bruscos de usuarios.

- Endurance/Soak Testing → estabilidad durante uso prolongado.

- Scalability Testing → capacidad de crecer horizontal/verticalmente.

# Métricas clave

- Tiempo de respuesta promedio y percentiles (p95, p99).

- Throughput (peticiones/segundo).

- Uso de CPU, memoria, ancho de banda.

- Tasa de errores.

# Herramientas comunes

- JMeter (open source, muy usado).

- k6 (moderno, scriptable en JS).

- Gatling (Scala/Java).

- Locust (Python).

- LoadRunner (comercial).

# Buenas prácticas

- Probar en entornos representativos.

- Usar datos realistas.

- Monitorizar tanto la aplicación como la infraestructura.

- Definir criterios de aceptación claros (SLAs/SLOs).
