# Selenium Standalone server

El Selenium Standalone server actúa como un proxy entre su script y los driver específicos del navegador. El servidor se puede usar cuando se ejecuta localmente, pero no se recomienda ya que introduce un salto adicional para cada solicitud y ralentizará las cosas. Sin embargo, se requiere que el servidor use un navegador en un host remoto (la mayoría de los controladores de navegador, como IEDriverServer, no aceptan conexiones remotas).

Para usar el servidor Selenium, deberá instalar el JDK y descargar el servidor más reciente de Selenium . Una vez descargado, ejecuta el servidor con:

```
java -jar selenium-server-standalone-2.45.0.jar
```

..................................................................................................

# Selenium Standalone Server y Selenium Server [Diferencias]

https://www.lambdatest.com/blog/selenium-standalone-server-and-selenium-server/

De los muchos frameworks de automatización de pruebas disponibles en el mercado, Selenium es indiscutiblemente uno de los mejores frameworks de automatización de pruebas para tests de automatización web. Selenium funciona con cualquier lenguaje de programación que le permita crear pruebas, incluidos Java, Python, C#, JavaScript, Ruby, etc. También se puede integrar con otros frameworks de pruebas de automatización como JUnit y TestNG para una mejor gestión y orquestación de pruebas. Sin embargo, para aprovechar al 100 % las pruebas de automatización de Selenium, el conocimiento y la arquitectura de sus componentes, como Selenium Standalone Server y Selenium Server, son muy importantes.

## Componentes de Selenium
Selenium es un conjunto de herramientas con un enfoque distinto para respaldar las pruebas de automatización. Proporciona más que una base para construir un framework de prueba automatizado: Selenium es un proyecto de código abierto con una gran comunidad, lo que significa que hay muchas formas de contribuir al proyecto, participar en la discusión y obtener un conocimiento valioso.

Al escribir este blog, Selenium tiene 22.600 estrellas y 6.700 bifurcaciones en la página de Selenium GitHub. Sin embargo, al integrar Selenium en su proyecto, debe tener en cuenta que existen diferentes formas de hacerlo. La última versión de Selenium (Selenium 4) tiene algunas novedades interesantes. Selenium 4 se lanzó en octubre de 2020, con un emocionante conjunto de nuevas características:

Selenium tiene diferentes componentes, lo que ayuda a lograr múltiples propósitos, como grabar y reproducir casos de prueba directamente desde el navegador, ejecutar casos de prueba en una máquina remota, escribir casos de prueba basados en scripts en varios lenguajes de programación y más.

![](imagenes/types-of-selenium.png)

## Selenium IDE

Es un entorno de desarrollo integrado para grabar y reproducir AUT directamente desde el navegador. Los probadores que no tienen conocimientos de secuencias de comandos pueden usar este IDE de manera efectiva para registrar sus interacciones con el AUT y reproducirlo cualquier cantidad de veces en el futuro.

Selenium IDE está disponible como una extensión del navegador y solo se puede usar con navegadores que admitan extensiones. Inicialmente, en Selenium 2, estaba disponible solo para el navegador Chrome. Sin embargo, ahora podemos usarlo con los navegadores Chrome, Firefox y Edge. Con Selenium 4, Selenium IDE también se puede integrar con Selenium Cloud Grid como LambdaTest. Esto ayuda a acelerar el proceso de prueba, ya que las pruebas de automatización de Selenium se pueden ejecutar en paralelo en diferentes navegadores y combinaciones de sistemas operativos.

## Selenium WebDriver

Selenium WebDriver es una API de código abierto y un framework de prueba basado en secuencias de comandos que ayuda a ejecutar la misma secuencia de comandos en diferentes navegadores con la ayuda de controladores de navegador.

```

Browser         | Supported OS        | Maintained by | Download
......................................................................................

Chromium/Chrome   Windows/macOS/Linux   Google          https://chromedriver.storage.googleapis.com/index.html


Firefox           Windows/macOS/Linux   Mozilla         https://github.com/mozilla/geckodriver/releases

Edge              Windows/macOS         Microsoft       https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/

Internet Explorer Windows               Selenium Project https://www.selenium.dev/downloads

Safari            macOS                 Apple           Built-in

```

Selenium WebDriver se puede integrar con los framework de prueba TestNG y JUnit para lograr una ejecución paralela, administrar scripts de prueba y generar informes de prueba. Para elegir el framework adecuado para sus requisitos de prueba, consulte nuestro tutorial sobre JUnit 5 frente a TestNG.

También puede realizar pruebas de integración continua integrando WebDriver con Maven y pruebas continuas con Jenkins.

## Selenium Grid

Selenium Grid es una herramienta que le permite administrar varias instancias diferentes de Selenium Server en diferentes máquinas. Facilita el proceso de ejecución de pruebas en paralelo y le permite escalar sus pruebas en varios nodos diferentes.

Selenium Grid se usa más comúnmente en pruebas web automatizadas; sin embargo, se puede usar para cualquier tipo de prueba que requiera múltiples nodos de Selenium Server.

## Selenium Standalone Server or Selenium Grid

Selenium Grid facilita la ejecución de casos de prueba en múltiples máquinas y navegadores simultáneamente, lo que acelera la velocidad de ejecución del caso de prueba y reduce drásticamente el tiempo de respuesta. En Selenium 3, Selenium Standalone Server (Selenium Grid) tiene dos componentes diferentes.

* **Selenium Hub:** Hub es un sistema central que acepta solicitudes de casos de prueba de los clientes. También gestiona hilos.

* **Selenium Node:** el nodo se registra en el hub y es un lugar donde existe el navegador real. Una máquina de nodo está conectada al hub, que recibe scripts de prueba del hub y los ejecuta. También es posible lanzar varios nodos en diferentes dispositivos que ejecutan diferentes entornos.

En Selenium 4, Grid se vuelve más flexible. Por ejemplo, una vez que el usuario inicia el servidor, Grid funciona automáticamente como nodos y hubs, por lo que el usuario no necesita iniciar el concentrador y el nodo por separado como en Selenium 3 Grid.

También es compatible con herramientas avanzadas como Docker, que se utiliza en el proceso DevOps. Ahora Grid 4 también tiene una interfaz de usuario más fácil de usar.

Hay tres formas de ejecutar Selenium Grid 4:

* Comenzando como Standalone, el propio Gird actúa como centro y nodo.

* Comience como un hub y un nodo separados.

* Totalmente distribuido (enrutador, sesión, distribuidor, etc.)
