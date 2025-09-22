# Introducción

La calidad del código no se limita a que “funcione”, sino a que el software sea legible, mantenible, escalable y seguro.
La norma ISO/IEC 25010 define características de calidad de software como: mantenibilidad, portabilidad, eficiencia y seguridad.

Un código de calidad reduce la deuda técnica y acelera el desarrollo en el largo plazo.

# Dimensiones clave

- Legibilidad → fácil de entender por otros desarrolladores.

- Mantenibilidad → cambios futuros no generan efectos secundarios.

- Complejidad → baja complejidad ciclomática, bajo acoplamiento, alta cohesión.

- Consistencia → estilo de codificación uniforme.

- Testabilidad → facilidad para escribir pruebas automáticas.

# Ejemplo práctico

- Un método de 300 líneas con múltiples responsabilidades → baja calidad.
- Refactorizarlo en funciones pequeñas y específicas mejora claridad y pruebas.

# Herramientas comunes

- SonarQube (análisis de calidad).

- ESLint (JavaScript).

- Pylint / flake8 (Python).

- Checkstyle / PMD (Java).

- Istanbul, JaCoCo (cobertura).

# Buenas prácticas

- Revisiones de código (peer reviews).

- Uso de linters y análisis estático.

- Refactorizar constantemente.

- Medir cobertura, pero sin obsesionarse con el 100%
