# Introducción

El API Testing consiste en validar las interfaces de comunicación entre diferentes componentes de software. Como las APIs suelen ser el “pegamento” de sistemas distribuidos, su fiabilidad es crítica.

Según ISTQB®, entran en la categoría de pruebas de integración y sistema, y suelen abordarse mediante técnicas de caja negra (probar entradas/salidas) o caja blanca (cuando hay acceso al código).

# Tipos de pruebas

- Funcionales → endpoints responden lo esperado.

- Contract testing → asegura que la API cumple con el contrato (OpenAPI/Swagger).

- Rendimiento → mide latencia, throughput y resistencia.

- Seguridad → protege contra ataques (inyecciones, exposición de datos).

# Ejemplo práctico

Una API de autenticación:

- Debe aceptar credenciales válidas y devolver un token.

- Debe rechazar credenciales incorrectas con el código HTTP adecuado.

# Herramientas comunes

- Postman (manual y automatización).

- REST Assured (Java).

- Karate DSL.

- JMeter, k6 (rendimiento).

# Buenas prácticas

- Usar entornos de prueba representativos.

- Automatizar pruebas críticas en CI/CD.

- Seguir las guías de OWASP API Security Top 10.
