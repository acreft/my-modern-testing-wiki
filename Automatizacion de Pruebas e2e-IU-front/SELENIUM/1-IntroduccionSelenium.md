# Resumen de Selenium

Selenium no es solo una herramienta o API, sino que compone muchas herramientas:

## WebDriver

Si está comenzando con la automatización de pruebas de sitios web de escritorio o sitios web móviles, entonces utilizará las API de WebDriver. WebDriver utiliza las API de automatización del navegador proporcionadas por los proveedores de navegadores para controlar el navegador y ejecutar pruebas. Esto es como si un usuario real estuviera operando el navegador. Dado que WebDriver no requiere que su API se compile con el código de la aplicación; No es intrusivo. Por lo tanto, está probando la misma aplicación que impulsa en vivo.

## IDE

IDE (Entorno de desarrollo integrado) es la herramienta que utiliza para desarrollar sus casos de prueba de Selenium. Es una extensión de Chrome y Firefox fácil de usar y generalmente es la forma más eficiente de desarrollar casos de prueba. Registra las acciones de los usuarios en el navegador por usted, utilizando los comandos existentes de Selenium, con parámetros definidos por el contexto de ese elemento. Esto no solo ahorra tiempo, sino que también es una excelente manera de aprender la sintaxis de scripts de Selenium.

## Grid

Selenium Grid le permite ejecutar casos de prueba en diferentes máquinas en diferentes plataformas. El control de la activación de los casos de prueba está en el extremo local y, cuando se activan los casos de prueba, el extremo remoto los ejecuta automáticamente.

Después del desarrollo de las pruebas de WebDriver, es posible que tenga que ejecutar sus pruebas en múltiples navegadores y combinaciones de sistemas operativos. Aquí es donde Grid entra en escena.

## Componentes de Selenium

La creación de un conjunto de pruebas con WebDriver requerirá que comprenda y utilice de forma eficaz varios componentes. Como ocurre con todo lo relacionado con el software, diferentes personas utilizan diferentes términos para la misma idea. A continuación se muestra un desglose de cómo se utilizan los términos en esta descripción.

**Terminología**

* API: Interfaz de programación de aplicaciones. Este es el conjunto de "comandos" que usa para manipular WebDriver.

* Biblioteca: un módulo de código que contiene las API y el código necesario para implementarlas. Las bibliotecas son específicas para cada enlace de idioma, por ejemplo, archivos .jar para Java, archivos .dll para .NET, etc.

* Driver: Responsable de controlar el navegador real. La mayoría de los controladores son creados por los propios proveedores de navegadores. Los controladores son generalmente módulos ejecutables que se ejecutan en el sistema con el propio navegador, no el sistema que ejecuta el conjunto de pruebas. (Aunque pueden ser el mismo sistema). NOTA: Algunas personas se refieren a los controladores como proxies.

* Framework: una biblioteca adicional que se utiliza como soporte para las suites de WebDriver. Estos marcos pueden ser marcos de prueba como JUnit o NUnit. También pueden ser marcos que admitan funciones de lenguaje natural como Cucumber o Robotium. Los marcos también se pueden escribir y usar para tareas como manipular o configurar el sistema bajo prueba, creación de datos, oráculos de prueba, etc.

**Las partes y piezas**

Como mínimo, WebDriver se comunica con un navegador a través de un controlador. La comunicación es bidireccional: WebDriver pasa los comandos al navegador a través del controlador y recibe la información a través de la misma ruta.


El controlador es específico para el navegador, como ChromeDriver para Chrome/Chromium de Google, GeckoDriver para Firefox de Mozilla, etc. El controlador se ejecuta en el mismo sistema que el navegador. Este puede o no ser el mismo sistema donde se ejecutan las pruebas.

![Comunicación básica](imagenes/basic_comms.png)


Este simple ejemplo anterior es comunicación directa . La comunicación con el navegador también puede ser comunicación remota a través de Selenium Server o RemoteWebDriver. RemoteWebDriver se ejecuta en el mismo sistema que el controlador y el navegador.


![Comunicación remota](imagenes/remote_comms.png)

La comunicación remota también puede tener lugar utilizando Selenium Server o Selenium Grid, los cuales a su vez se comunican con el controlador en el sistema host.

![Comunicación Remota con Grid](imagenes/remote_comms.png)


**Donde encajan los marcos**

WebDriver tiene un trabajo y solo un trabajo: comunicarse con el navegador a través de cualquiera de los métodos anteriores. WebDriver no sabe nada sobre pruebas: no sabe cómo comparar cosas, afirmar que pasa o falla, y ciertamente no sabe nada sobre informes o gramática dada/cuando/entonces.

Aquí es donde entran en juego varios marcos. Como mínimo, necesitará un marco de prueba que coincida con los enlaces del lenguaje, por ejemplo, NUnit para .NET, JUnit para Java, RSpec para Ruby, etc.

El marco de prueba es responsable de ejecutar y ejecutar su WebDriver y los pasos relacionados en sus pruebas. Como tal, puede pensar que se parece a la siguiente imagen.

![Comunicación Remota con Grid](imagenes/test_framework.png)

Los marcos/herramientas de lenguaje natural como Cucumber pueden existir como parte de ese cuadro de marco de prueba en la figura anterior, o pueden envolver el marco de prueba por completo en su implementación personalizada.
