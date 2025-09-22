# Introducción

El Unit Testing es la técnica de verificación de software más básica, que se centra en validar las unidades mínimas de código (funciones, clases, métodos). Según ISTQB®, este nivel de prueba forma parte de las pruebas de componente, y su objetivo es detectar defectos de forma temprana antes de la integración.

Los unit tests suelen ser automatizados y forman la primera línea de defensa contra errores, actuando como una red de seguridad para cambios futuros en el código (regresión).

# Características

- Aíslan el código de dependencias externas usando mocks, stubs o fakes.

- Ejecutan de forma rápida, ideal para integración continua (CI/CD).

- Refuerzan prácticas como TDD (Test Driven Development).

# Ejemplo práctico

Si una función suma dos números, un unit test debe verificar:

- Que devuelve el resultado correcto.

- Que maneja valores límite (nulos, negativos, decimales).

# Herramientas comunes

- Java → JUnit, TestNG.

- Python → pytest, unittest.

- JavaScript → Jest, Mocha.

- .NET → NUnit, xUnit.

# Buenas prácticas

- Mantener pruebas pequeñas, independientes y rápidas.

- Nombrar los casos de manera descriptiva.

- Ejecutar en cada commit.
