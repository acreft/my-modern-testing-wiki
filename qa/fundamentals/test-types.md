# Niveles de Pruebas 🔬

## Introducción 🚀

Habitualmente, cuando se habla de automatizar procesos de testing en el mundo del software, se asocia a automatizar la ejecución de pruebas solo a nivel de interfaz gráfica. De forma tradicional, los proyectos que tenían algún tipo de prueba automática lo concentraban en esta capa. Además, estos ciclos de prueba eran completamente End-to-End, es decir, podían probar un ciclo de pruebas o proceso de negocio completo, desde el inicio hasta el final, lo que las hace muy susceptible a los cambios y muy costosas para mantenerlas vivas, con el consiguiente número de falsos positivos en cada ejecución. Esto deteriora la confianza en las pruebas, que es uno de los objetivos claves de la calidad, y que es necesario mantener independientemente de que el proceso sea manual o automático. El catálogo principal de las pruebas eran manuales y costosas, existiendo contados Unit Test o ninguno, que se evitaban con un "Skip" en fase de compilación por estar obsoletos o por no ofrecer garantías.

## Niveles de Pruebas en base a Criticidad de los Procesos de Negocio 📝

Cuando se disponga de pruebas para todos los niveles de la pirámide será necesario hacer una subdivisión en aquellos donde el diseño y la ejecución sean costosos (por ejemplo, niveles API y E2E), para intentar focalizar en los procesos críticos cuando no sea posible cubrir todo el catálogo de pruebas.

- **Smoke Tests**

Conjunto de pruebas que verifican el correcto funcionamiento de la funcionalidad más crítica del Sistema. Validan que está funcionando correctamente tras un despliegue o instalación, garantizando que el producto está listo para ejecutar otros niveles de prueba. Suelen utilizarse para validar los despliegues de los Pipeline de Despliegue Continuo.

- **Sanity Tests**

Conjunto de pruebas que verifican rápidamente las funcionalidades más críticas del sistema, con más alcance que los Smoke Tests.

- **Regression Tests**

Conjunto de pruebas que realizan una regresión completa de la funcionalidad del sistema, probando la mayoría de los procesos de negocio, para validar que las modificaciones incluidas recientemente no provocan errores inesperados.

- **Integration Tests**

Conjunto de pruebas que ponen el foco en las funcionalidades que tienen integraciones con otros productos o sistemas horizontales, para verificar que funcionan de forma correcta tras cambios o despliegues.

Tanto las pruebas automáticas como las pruebas manuales deben estar etiquetadas con su nivel correcto, usando las siguientes etiquetas:

@SmokeTest

@SanityTest

@RegressionTest

@IntegrationTest
