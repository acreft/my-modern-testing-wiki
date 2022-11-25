# Selenium Grid

Selenium Grid es un servidor proxy basado en una arquitectura de nodos centrales. Facilita un proceso sencillo para ejecutar pruebas en paralelo en varias máquinas (nodos).

En Selenium Grid, un servidor actúa como el concentrador que enruta los comandos de prueba con formato JSON a uno o más nodos Grid registrados. Las pruebas se ponen en contacto con el concentrador para obtener acceso a las instancias del navegador remoto.

Por ejemplo: un concentrador se puede conectar a tres nodos diferentes, cada uno de los cuales ejecuta un navegador independiente o una versión de navegador diferente. Cuando se ejecutan las pruebas, la solicitud se envía al concentrador que busca el nodo con criterios específicos (como la versión del navegador, el tipo de navegador). Una vez que el concentrador logra ubicarlo, se envían scripts al nodo y se ejecutan las pruebas.