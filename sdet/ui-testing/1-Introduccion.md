# Introducción

El UI Testing (User Interface Testing) consiste en verificar que la interfaz gráfica de usuario cumpla con los requisitos funcionales y de diseño, garantizando una experiencia de usuario (UX) consistente.

Mientras que los unit tests validan lógica interna, los UI tests simulan el uso real de la aplicación desde la perspectiva del usuario.

# Características

- Validan flujos críticos: login, formularios, navegación, botones, interacciones.

- Involucran aspectos funcionales (el botón guarda datos) y no funcionales (usabilidad, accesibilidad).

- Son más costosos y frágiles que las pruebas de menor nivel (dependen de cambios en la interfaz).

# Tipos de pruebas de UI

- Pruebas funcionales → validan que los elementos respondan correctamente.

- Pruebas de regresión visual → detectan cambios inesperados en diseño o estilo.

- Pruebas de accesibilidad → cumplen con estándares WCAG/ARIA.

# Herramientas comunes

- Selenium WebDriver (web).

- Cypress (moderno, rápido para web).

- Playwright (multi-navegador, estable).

- Applitools o Percy (pruebas visuales).

- AXE Core (accesibilidad).

# Buenas prácticas

- Priorizar pruebas críticas, no cubrir el 100% de la UI.

- Evitar flaky tests (esperas explícitas, usar selectores estables).

- Complementar con pruebas manuales exploratorias.
