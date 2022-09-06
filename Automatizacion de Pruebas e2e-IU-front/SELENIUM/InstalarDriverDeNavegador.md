# Instalar controladores de navegador

https://www.selenium.dev/documentation/webdriver/getting_started/install_drivers/

**Configurar su sistema para permitir la automatización de un navegador.**

A través de WebDriver, Selenium admite todos los principales navegadores del mercado, como Chrome/Chromium, Firefox, Internet Explorer, Edge, Opera y Safari. Siempre que sea posible, WebDriver controla el navegador mediante el soporte integrado del navegador para la automatización.

Dado que todas las implementaciones de controladores, excepto Internet Explorer, son proporcionadas por los propios proveedores de navegadores, no se incluyen en la distribución estándar de Selenium. Esta sección explica los requisitos básicos para comenzar a usar los diferentes navegadores.

Lea sobre opciones más avanzadas para iniciar un controlador en nuestra documentación de configuración del controlador .

![](imagenes/Arquitectura-de-Selenium-WebDriver.png)

## Tres formas de usar controladores

**1. Software de gestión de controladores**

La mayoría de las máquinas actualizan automáticamente el navegador, pero el controlador no lo hace. Para asegurarse de obtener el controlador correcto para su navegador, existen muchas bibliotecas de terceros que pueden ayudarlo.


* Importar WebDriverManager

```
import io.github.bonigarcia.wdm.WebDriverManager;
```


* Llamar setup()coloca automáticamente el controlador de navegador correcto donde el código lo verá:

```
WebDriverManager.chromedriver().setup();
```

* Simplemente inicialice el controlador como lo haría normalmente:

```
ChromeDriver driver = new ChromeDriver();
```

Vea el ejemplo completo en [GitHub](https://github.com/SeleniumHQ/seleniumhq.github.io/blob/trunk/examples/java/src/test/java/dev/selenium/getting_started/InstallDriversTest.java).

**2. La PATH variable del entorno**  -- 😰AXA

Esta opción primero requiere descargar manualmente el controlador (consulte la sección de referencia rápida para ver los enlaces).

Esta es una opción flexible para cambiar la ubicación de los controladores sin tener que actualizar su código y funcionará en varias máquinas sin necesidad de que cada máquina coloque los controladores en el mismo lugar.

Puede colocar los controladores en un directorio que ya aparece en la lista PATH o puede colocarlos en un directorio y agregarlo a PATH.

* Para ver en qué directorios ya están PATH, abra una Terminal y ejecute:

Bash:

```
echo $PATH
```
Windows:

```
echo %PATH%
```

* Si la ubicación de su controlador no está ya en un directorio de la lista, puede agregar un nuevo directorio a PATH:

Bash:

```
echo 'export PATH=$PATH:/path/to/driver' >> ~/.bash_profile
source ~/.bash_profile
```

Windows:
```
setx PATH "%PATH%;C:\WebDriver\bin"
```

Puede probar si se ha agregado correctamente iniciando el controlador:

```
chromedriver
```

Si **PATH** está configurado correctamente arriba, verá algunos resultados relacionados con el inicio del controlador:

```
Starting ChromeDriver 95.0.4638.54 (d31a821ec901f68d0d34ccdbaea45b4c86ce543e-refs/branch-heads/4638@{#871}) on port 9515
Only local connections are allowed.
Please see https://chromedriver.chromium.org/security-considerations for suggestions on keeping ChromeDriver safe.
ChromeDriver was started successfully.

```
Puede recuperar el control de su símbolo del sistema presionando Ctrl+C

**3. Ubicación codificada**

Similar a la opción 2 anterior, debe descargar manualmente el controlador (consulte la sección de referencia rápida para ver los enlaces). Especificar la ubicación en el código en sí tiene la ventaja de no tener que averiguar las variables de entorno en su sistema, pero tiene la desventaja de hacer que el código sea mucho menos flexible.

```
System.setProperty("webdriver.chrome.driver","/path/to/chromedriver");
ChromeDriver driver = new ChromeDriver();
```
