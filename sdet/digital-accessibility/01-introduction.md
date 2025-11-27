# 🧠 Accesibilidad Digital: Guía Completa para QA y Testing

## 1. Introducción General

La **accesibilidad digital** garantiza que todas las personas, independientemente de sus capacidades o limitaciones, puedan **percibir, comprender, navegar e interactuar** con productos digitales.

No se trata solo de cumplir normas: la accesibilidad **incluye usuarios**, amplía el alcance de sistemas y mejora la experiencia de todos.

**Datos clave:**

- Más del 15% de la población mundial vive con alguna discapacidad (OMS).

- En Uruguay, casi 17% de la población se encuentra en alguna situación de discapacidad.

- La accesibilidad aumenta la participación de usuarios, reduce riesgos legales y fortalece la reputación.

---

## 2. Principios y Normativas

### 2.1 Principios WCAG

Las **Web Content Accessibility Guidelines (WCAG)** son el estándar global de accesibilidad web y móvil, desarrollado por el **W3C**.

Se organizan en cuatro principios:

| Principio | Qué significa | Ejemplo |

|-----------|---------------|---------|

| **Perceptible** | Toda información debe poder ser percibida por todos los usuarios | Texto alternativo en imágenes |

| **Operable** | Los usuarios deben poder interactuar con todos los elementos | Navegación por teclado |

| **Comprensible** | El contenido debe ser claro y predecible | Lenguaje simple y consistente |

| **Robusto** | El contenido debe funcionar con diversas tecnologías | Compatibilidad con lectores de pantalla |

### 2.2 Evolución de WCAG

- **1.0 (1999)**: Principios generales de diseño accesible.

- **2.0 (2008)**: Recomendaciones para contenido web accesible.

- **2.1 (2018)**: Accesibilidad móvil y cognitiva.

- **2.2 (2023)**: Mejoras en control táctil y autenticación.

- **3.0 / Proyecto Silver**: Futuro modelo más flexible y medible.

### 2.3 Legislación y estándares adicionales

- **ADA (EE. UU.)**: Acceso universal a sistemas públicos y educativos.

- **Secciones 504 y 508**: Acceso al trabajo, educación y tecnología.

- **Leyes locales**: Cada país puede tener requisitos específicos.

---

## 3. Tipos de Discapacidad y Herramientas de Apoyo

| Tipo | Ejemplo | Herramientas de asistencia |

|------|---------|---------------------------|

| **Visual** | Ceguera, baja visión, daltonismo | Lectores de pantalla (NVDA, JAWS, VoiceOver), zoom, contraste alto |

| **Auditiva** | Sordera, hipoacusia | Subtítulos, transcripciones |

| **Motriz** | Movilidad reducida | Navegación por teclado, dispositivos adaptativos |

| **Cognitiva** | Dificultad de comprensión o atención | Lenguaje simple, estructura predecible, etiquetas claras |

---

## 4. Estrategia de Pruebas de Accesibilidad

### 4.1 Objetivos Estratégicos

- Establecer KPIs claros: reducción de tickets de soporte, aumento del uso de funcionalidades accesibles.

- Conocer la audiencia: identificar tecnologías asistivas utilizadas.

- Integrar la accesibilidad en flujos **Agile y DevOps**, desde el inicio del desarrollo.

> La accesibilidad debe formar parte de la _Definition of Done_ en todos los sprints.

### 4.2 Áreas clave del checklist

1. **Estructura y Semántica:** HTML semántico, jerarquía de encabezados, declaración de idioma.

2. **Navegación y enlaces:** total navegabilidad por teclado, orden de foco lógico, enlaces descriptivos.

3. **Diseño visual e imágenes:** contraste adecuado, texto alternativo, minimizar texto en imágenes.

4. **Formularios y entradas:** etiquetas visibles, mensajes de error claros, accesibilidad por teclado.

5. **Contenido dinámico y multimedia:** subtítulos, transcripciones, control de animaciones, roles ARIA.

6. **Accesibilidad móvil:** botones ≥44×44 px, diseño adaptativo, compatibilidad con VoiceOver y TalkBack.

---

## 5. Tipos de Pruebas de Accesibilidad

### 5.1 Pruebas Automáticas

- Analizan **cumplimiento técnico** de WCAG en el código HTML, contraste y estructura.

- Herramientas comunes:

  - **Axe DevTools:** estructura y semántica.

  - **Colour Contrast Analyzer (CCA):** contraste de color.

  - **Lighthouse:** evaluación general.

### 5.2 Pruebas Manuales / de Usuario

- Se enfocan en la **experiencia real** y situaciones específicas de discapacidad.

- Ejemplos:

  - Validar que texto alternativo describa correctamente imágenes.

  - Comprobar navegación por teclado y secuencia de tabulación.

  - Probar zoom hasta 200% y verificar visibilidad de contenido.

  - Validar que lectores de pantalla interpreten correctamente cada elemento.

---

## 6. Automatización del Testing de Accesibilidad

### 6.1 Playwright + AxeDev Tools

- Automatiza la validación de accesibilidad dentro de pipelines CI/CD.

- Permite **integrar pruebas funcionales y de accesibilidad** en flujos end-to-end.

**Ejemplos de uso:**

1. Verificación de accesibilidad de una URL específica.

2. Escaneo de múltiples URLs y consolidación de resultados.

3. Configuración personalizada de reglas y estándar WCAG.

4. Prueba de flujos funcionales completos (end-to-end) con validación simultánea de accesibilidad.

**Beneficios:**

- Ahorro de tiempo y recursos.

- Ejecución continua junto a pruebas funcionales.

- Detección temprana de defectos y regresiones.

---

## 7. Roles y Cultura de Accesibilidad

| Rol | Responsabilidad |

|------|----------------|

| **Diseñadores** | Contraste, jerarquía visual, etiquetas descriptivas |

| **Desarrolladores** | HTML semántico, ARIA, código accesible |

| **Testers** | Validar experiencia, ejecutar pruebas manuales y automatizadas |

| **PMs y líderes** | Integrar accesibilidad en objetivos estratégicos y KPIs |

> La accesibilidad debe ser **cultural, no solo técnica**. Incluir personas con discapacidad en pruebas de usabilidad fortalece la empatía y la calidad.

---

## 8. Mantenimiento y Mejora Continua

- Pruebas en cada release o sprint.

- Auditorías periódicas (trimestrales o semestrales).

- Documentación de hallazgos y KPIs: errores detectados, solucionados y reabiertos.

- Integración de resultados en tableros de QA y paneles de control.

---

## 9. Conclusión

La accesibilidad digital es un **componente esencial de la calidad del software**.

Su implementación permite:

- Ampliar el mercado y alcance de productos.

- Mejorar la experiencia del usuario y la reputación.

- Reducir riesgos legales y aumentar la fidelidad.

Una estrategia integral combina:

1. **Herramientas automatizadas** (Axe, CCA, Playwright).

2. **Pruebas manuales y con usuarios reales**.

3. **Gestión continua y cultura organizacional**.

> **Accesibilidad = Calidad + Inclusión + Confianza.**

---

## 10. Fuentes

https://qalified.com/es/blog/guia-para-las-pruebas-de-accesibilidad/

https://qalified.com/es/blog/lista-verificacion-pruebas-accesibilidad/

https://qalified.com/es/blog/accesibilidad-pruebas-wave-accessibility/

https://qalified.com/es/blog/testing-accesibilidad-herramientas/
