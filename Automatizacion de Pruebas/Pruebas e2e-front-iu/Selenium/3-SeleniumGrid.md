# GRID

**¿Quiere ejecutar pruebas en paralelo en varias máquinas? Entonces, Grid es para ti.**

Selenium Grid permite la ejecución de scripts de WebDriver en máquinas remotas mediante el enrutamiento de comandos enviados por el cliente a instancias de navegador remotas.

La red tiene como objetivo:

* Proporcione una manera fácil de ejecutar pruebas en paralelo en varias máquinas.

* Permitir pruebas en diferentes versiones del navegador

* Habilitar pruebas multiplataforma

## ¿Que es Selenium?

Selenium es un framework de herramientas de automatización de pruebas. 

La suite Selenium consta de cuatro componentes:

* Selenium Grid

* Selenium IDE

* Selenium RC

* Selenium Webdriver

## ¿Que es Selenium Grid?

Selenium Grid es un servidor proxy inteligente que facilita la ejecución de pruebas en paralelo en varias máquinas. Esto se hace mediante el enrutamiento de comandos a instancias remotas del navegador web, donde un servidor actúa como un hub. Este concentrador enruta los comandos de prueba que están en formato JSON a varios nodos Grid registrados.

Hub permite la ejecución simultánea de pruebas en múltiples máquinas, administrando diferentes navegadores de forma centralizada, en lugar de realizar diferentes pruebas para cada uno de ellos. Selenium Grid facilita las pruebas entre navegadores, ya que se puede realizar una sola prueba en varias máquinas y navegadores, todos juntos, lo que facilita el análisis y la comparación de los resultados.

Los dos componentes principales de la arquitectura Selenium Grid son:

* **Hub** es un servidor que acepta las solicitudes de acceso del cliente WebDriver, enrutando los comandos de prueba JSON a las unidades remotas en los nodos. Toma instrucciones del cliente y las ejecuta de forma remota en los distintos nodos en paralelo.

* **El nodo** es un dispositivo remoto que consta de un sistema operativo nativo y un WebDriver remoto. Recibe solicitudes del hub en forma de comandos de prueba JSON y los ejecuta mediante WebDriver.

![](imagenes/Selenium-Grid-Basic-Diagram.png)
