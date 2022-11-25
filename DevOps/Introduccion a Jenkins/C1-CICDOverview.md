# Introducción

Según Watts S. Humphrey, el padre de la calidad del software y la integración del modelo de madurez de capacidad (CMMI), cada negocio es un negocio de software.

Todas las empresas de software necesitan entregar software de manera oportuna, confiable y repetible. En este capítulo, brindaremos una descripción general de Continuous Integration, Continuous Delivery y Continuous Deployment, y explicaremos cómo estas prácticas lo ayudan a lograr sus objetivos de entrega de software.

# CI/CD Overview

## Software Development Life Cycle

Enunciados de nivel 2 podrían ser creados por proveedores del curso en el futuro.
El desarrollo de software sigue un flujo, comenzando con la identificación de nuevas funciones, la planificación, el desarrollo real, la confirmación de los cambios en el código fuente, la ejecución de compilaciones y pruebas (unitarios, integración, funcional, aceptación, etc.) y la despliegue en producción.

![](imagenes/imagen1.png)

Con un enfoque tradicional de entrega de software en cascada, los desarrolladores podrían trabajar de forma independiente durante mucho tiempo. No tendrían ni idea de cuántos problemas se encontrarían durante la fase de integración.

Para abordar este problema, se introdujo el modelo de desarrollo de software Agile. Agile cambió la forma en que trabajaban los equipos de desarrollo de software. Uno de los principios clave de esta metodología era entregar software funcional con frecuencia. El enfoque se movió hacia el lanzamiento de software incremental, en lugar de lanzamientos en cascada de big bang que tomaron meses y años.

Entregar software frecuentemente significaba producir código estable para cada versión incremental. Fue todo un desafío integrar los cambios de varios desarrolladores en los equipos. Esto llevó a los equipos de software a buscar mejores enfoques. La Integración Continua (CI) ofreció un rayo de esperanza y comenzó a ganar popularidad.

## Continuous Integration (CI)

La integración continua es una práctica de ingeniería ágil que se origina en la metodología de programación extrema. Se enfoca principalmente en la compilación y pruebas automatizadas para cada cambio comprometido con el sistema de control de versiones por parte de los desarrolladores.

Según Martín Fowler,

> *"La integración continua (CI) es una práctica de desarrollo de software en la que los miembros de un equipo integran su trabajo con frecuencia; por lo general, cada persona se integra al menos diariamente, lo que lleva a múltiples integraciones por día. Cada integración se verifica mediante una compilación automatizada (incluida la prueba) para detectar errores de integración lo antes posible".*

![](imagenes/imagen2.png)

Para implementar la Integración Continua, necesitará:

- **Un sistema de control de versiones:** Almacena todo el código fuente registrado por los equipos y actúa como la única fuente de información.

- **Prueba unitaria y compilación automatizada:** No es suficiente si el código escrito por un desarrollador funciona solo en su máquina. Cada compromiso que llega al sistema de control de versiones debe ser creado y probado por un servidor de integración continua independiente.

- **Feedback:** Los desarrolladores deben recibir comentarios sobre sus confirmaciones. Cada vez que el cambio de un desarrollador interrumpe la compilación, puede tomar las medidas necesarias (por ejemplo, notificaciones por correo electrónico).

- **Acuerdo sobre las formas de trabajo:** Es importante que todos en el equipo sigan la práctica de registrar cambios incrementales en lugar de esperar hasta que estén completamente desarrollados. Su prioridad debe ser solucionar cualquier problema de compilación que pueda surgir con el código registrado.

## Movimiento DevOps

La integración continua resuelve principalmente la parte de desarrollo del flujo de trabajo. Sin embargo, hay más en la entrega de software que solo el desarrollo de características y la integración de los cambios. Hay un proceso de prueba (manual, automatizado) y de lanzamiento (despliegue real para el cliente o producción).

En la era anterior a DevOps, cada equipo era responsable de su propio trabajo. El equipo de desarrollo se encargaría del desarrollo de características. Ahí es donde terminó su trabajo. Luego se lo pasarían al equipo de control de calidad (QA). El equipo de control de calidad ejecutaría todas las suites de prueba extendidas (manuales y automatizadas). Si las cosas funcionaban bien, le pasaban las funciones al equipo de operaciones, quien finalmente implementaba las nuevas funciones en producción y las administraba.

Cada uno de estos equipos trabajó en silos. Los procesos de lanzamiento eran en su mayoría manuales y propensos a errores, lo que generaba ciclos de lanzamiento más largos y dolorosos. Cada vez que algo salía mal, se dedicaba una gran cantidad de tiempo a tratar de llegar a la raíz del problema, por no hablar del juego de culpas. Todo esto resultó en una gran cantidad de tiempo perdido en varios niveles de la organización.

En realidad, todos los equipos deben ser igualmente responsables del lanzamiento del nuevo software, lo que significa que todos estos equipos deben trabajar en estrecha colaboración entre sí. El movimiento DevOps, que se originó a partir del desarrollo de software Agile, enfatiza fuertemente la necesidad de colaboración entre los diversos equipos involucrados en el proceso de entrega de software. Además de una estrecha colaboración, también se considera extremadamente importante la automatización de cada una de las etapas del proceso de entrega de software y los ciclos de retroalimentación constante. Continuous Delivery proporciona un marco para lograr los objetivos de DevOps a través de la automatización y los bucles de retroalimentación continuos.

## Continuous Delivery

La Entrega Continua es una extensión lógica de la Integración Continua. Mientras que la integración continua le permite automatizar el proceso de compilación y prueba del software, la entrega continua automatiza el proceso completo de entrega de la aplicación al tomar cualquier cambio en el código (nuevas funciones, corrección de errores, etc.) desde el desarrollo (commits de código) hasta el despliegue (para ambientes como la puesta en escena y la producción). Garantiza que pueda lanzar nuevos cambios a sus clientes rápidamente de manera confiable y repetible.

Según Martin Fowler, quien acuñó el término Entrega Continua,

> *"La entrega continua es una disciplina de desarrollo de software en la que se crea software de tal manera que el software se puede lanzar a producción en cualquier momento.*
>
> *Estás haciendo entrega continua cuando:*
>
> *a. Su software se puede desplegar a lo largo de su ciclo de vida.*
>
> *b. Su equipo prioriza mantener el software desplegable antes que trabajar en nuevas funciones.*
>
> *c. Cualquiera puede obtener comentarios rápidos y automatizados sobre la preparación de  producción de sus sistemas cada vez que alguien les hace un cambio.*
>
> *d. Puede realizar despliegues con solo presionar un botón de cualquier versión del software en cualquier entorno bajo demanda.*
>
> *(...)*

Para lograr una entrega continua necesita:

* una relación de trabajo estrecha y colaborativa entre todos los involucrados en la entrega (a menudo denominada cultura DevOps).

* automatización extensiva de todas las partes posibles del proceso de entrega, generalmente utilizando una pipeline de despliegue*".

*Cubriremos esto con un poco más de detalle más adelante en este capítulo.

La incorporación de prácticas de entrega continua hará que su proceso de lanzamiento general sea sencillo, reducirá el tiempo de comercialización de nuevas funciones y aumentará la calidad general del software, lo que conducirá a una mayor satisfacción del cliente. También puede reducir significativamente sus costos de desarrollo de software, ya que sus equipos priorizarán el lanzamiento de nuevas funciones sobre los defectos de depuración.

## Continuous Deployment

A menudo, muchos utilizan los términos Entrega continua e Despliegue continuo como sinónimos, pero en realidad estos conceptos tienen un significado diferente.

Si bien Continuous Delivery le brinda la capacidad de desplegar en producción con frecuencia, no significa necesariamente que esté automatizando el despliegue. Es posible que necesite una aprobación manual antes del despliegue en producción, o es posible que su empresa no desee realizar despliegues con frecuencia.

Sin embargo, Continuous Deployment es una forma automatizada de desplegar sus versiones en producción. Debe realizar una entrega continua para poder realizar un despliegue automatizado. Empresas como Netflix, Amazon, Google y Facebook despliegan automáticamente a producción varias veces al día.

![](imagenes/imagen3.png)

Ya sea que esté realizando una  Continuous Delivery o Continuous Deployment, ya sabe que necesita una pipeline de despliegue. A continuación, echemos un vistazo a lo que es la canalización de despliegue.

## Deployment Pipelines

Las canalizaciones de despliegue (o pipelines de entrega continua) son la piedra angular de la entrega continua, ya que automatizan todas las etapas (construcción, prueba, lanzamiento, etc.) de su proceso de entrega de software.

El uso de canalizaciones de implementación continua ofrece numerosos beneficios. Una canalización automatizada permite que todas las partes interesadas supervisen el progreso, elimina la sobrecarga de todo el trabajo manual, proporciona comentarios rápidos y, lo que es más importante, genera confianza en la calidad del código.

![](imagenes/imagen4.png)

La ejecución de la tubería de despliegue comienza con un desarrollador que comittea el cambio del código fuente en un repositorio de control de versiones. El servidor de CI detecta la nueva confirmación, compila el código y ejecuta pruebas unitarias. La siguiente etapa es desplegar los artefactos (archivos generados a partir de una compilación) en un entorno de ensayo o de prueba de funciones en el que se ejecutan pruebas funcionales, de regresión y de aceptación adicionales. Una vez que todas las pruebas sean exitosas, estará listo para desplegar en producción. En caso de falla durante cualquier etapa, el flujo de trabajo se detiene y se envía una respuesta inmediata al desarrollador.

## Tools for Deployment Pipeline

Para automatizar las diversas etapas de su proceso de implementación, necesitará varias herramientas. Por ejemplo:

- Un sistema de control de versiones como Git para almacenar su código fuente.

- Una herramienta de integración continua (CI) como Jenkins para ejecutar compilaciones automatizadas.

- Framework de prueba como xUnit, Selenium, etc., para ejecutar varias suites de prueba.

- Un repositorio binario como Artifactory para almacenar artefactos de compilación.

- Herramientas de gestión de configuración como Ansible.

- Un dashboard para que el progreso sea visible para todos.

- Comentarios frecuentes en forma de correos electrónicos o notificaciones de Slack.

Y eso no es todo. También necesitará una herramienta única que pueda reunir todas estas herramientas para lograr los objetivos de CI/CD, que es automatizar la entrega de software.

## CI/CD Tools

Existe una gran cantidad de herramientas CI/CD de código abierto (gratuitas) y empresariales (de pago) disponibles en el mercado. Aquí hay una matriz que compara algunas de las herramientas de CI/CD más populares en función del tipo de oferta (de pago o gratuita), licencias (de código abierto o de código cerrado), alojamiento (en las instalaciones o en la nube) y extensiones/complementos.

[Tabla]

## GitLab CI/CD vs Jenkins

Como puede ver, solo hay dos opciones gratuitas, GitLab CI/CD y Jenkins. Sin embargo, la edición comunitaria de GitLab no le brinda la flexibilidad de usar un repositorio de control de versiones de su elección y no ofrece muchas integraciones a través de los complementos. Por otro lado, Jenkins es una herramienta gratuita y de código abierto que ha resistido la prueba del tiempo. Ha existido por más de 15 años. Tiene una comunidad de código abierto grande y activa que lanza constantemente nuevas versiones, correcciones de errores, etc. Hay muchas fuentes en línea (documentación, grupos de Google, etc.) para obtener ayuda.

Jenkins se puede instalar en cualquier sistema operativo local o en la nube. Su sólida integración con muchas otras herramientas de terceros lo convierte en una excelente opción.

![](imagenes/imagen5.png)