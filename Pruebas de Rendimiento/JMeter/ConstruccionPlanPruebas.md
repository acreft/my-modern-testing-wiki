# Construcción de Planes de Prueba con JMeter 🛠️

JMeter es una herramienta de testing cuyas funcionalidades se pueden resumir en tres:

* Diseñar un testplan, esto es, generar un fichero .jmx. Este es el objeto de este documento.

* Ejecutar un testplan.

* Ver de distintas formas los resultados de la ejecución de un testplan (vía listeners).

Para diseñar un testplan, JMeter dispone de una interfaz GUI a modo de diseñador, en la que el tester puede ir agregando componentes de manera visual, y ejecutar los componentes agregados, viendo el resultado. Una vez finalizado el diseño del testplan, la herramienta permite grabar este como un fichero .jmx.

La propia herramienta permite ejecutar un fichero .jmx previamente generado, vía línea de comandos o vía la propia interfaz GUI. La ejecución de un fichero .jmx realiza peticiones contra la aplicación objetivo a testear (peticiones del tipo que se hayan especificado al generar el fichero .jmx, JMeter dispone de la posibilidad de generar muchos tipos de peticiones: HTTP, FTP, LDAP, ...). Para cada petición ejecutada, JMeter recopila ciertos datos. Además, en el fichero .jmx se puede especificar que número de usuarios de cada tipo ejecuta las peticiones contra la aplicación, es decir, el .jmx simula una o mas comunidades de usuarios (roles) trabajando contra la aplicación objetivo.

Los datos generados por la herramienta para cada petición se procesan o bien con un tipo de componente que proporciona la interfaz GUI llamados listeners, o bien con herramientas externas. Los listeners permiten ver los resultados de una o mas ejecuciones de múltiples maneras (cada listener de una manera).

Este manual explica los conceptos necesarios para construir testplans (ficheros .jmx) configurables y mantenibles con JMeter. En particular, se explica el concepto de componente y tipo de componente de un testplan, el orden en que estos se asocian a los samplers, el ámbito de los diferentes tipos de componentes, los métodos para grabar un testplan, y como construir testplan configurables y mantenibles mediante el uso de variables, propiedades y funciones.

Está orientado principalmente a técnicos y testers involucrados en la construcción de ficheros .jmx de JMeter o a técnicos que deseen iniciarse en el uso de la herramienta para implementarlos.

## Modo de empleo 🔩

**NOTA:**
Por qué es importante la configuración del idioma (Inglés) en la herramienta: la interfaz GUI dispone de un sistema de ayuda online que muestra la documentación de referencia de un componente (opción Help del menú emergente del componente en el árbol del testplan). Este sistema de ayuda online obtiene la documentación de ayuda accediendo, vía http a la referencia de componentes sita en la web del proyecto JMeter, realizando una búsqueda por el nombre del componente en INglés. Si la interfaz GUI se configura en Español, el sistema de ayuda obline no encontrará ninguna concidencia y no funcionará correctamente.
Este detalle es importante sobre todo para aquellos que se incian en la construcción de testplans, pues necesitan consultar frecuentemente la referencia de los componentes de JMeter.

### Modos de ejecución de JMeter
Hay dos formas de ejecutar JMeter según que queramos que se muestre o no la interfaz GUI:

* Desde línea de comando SIN mostrar la interfaz GUI (especificar la opción -n en la línea de comando).
* Mostrando la interfaz GUI: no especificar la opción -n al arrancar JMeter.

La mayoría de las restantes opciones de la línea de comando son aplicables a la ejecución de JMeter tanto si se utilizan con el modificador -n como sin él.

Para diseñar un testplan, utilizamos la interfaz GUI, una de cuyas funcionalidades es además de ejecutar testplans, proporcionar un entorno para diseñarlos. Por tanto, para diseñar un testplan arrancaremos JMeter sin el modificador -n, por ejmeplo:


```
${JMETER_HOME}/bin/jmeter
```

### Componentes y tipos de componentes de un testplan

Un testplan (fichero .jmx) es una JERARQUÍA de componentes en forma de árbol. Puede verse abriendo un fichero .jmx en la interfaz GUI, en el frame de la izquierda (en el directorio de la instalacion _${JMETER_HOME}/printable_docs/demos/_ hay varios .jmx de ejemplo).

Cada nodo del árbol es un componente. A su vez, un componente es una instancia de un tipo de componente en la que quizás se han configurado algunas de sus propiedades (en el panel de control de la derecha).

La tabla siguiente explica para que sirve cada uno de los tipos de componentes que existen en JMeter:

| Tipo de componente | Uso |
| ------------- | ------------- |
| Testplan  | Es el tipo de componente que representa la raíz del árbol. En todo testplan existe uno y sólo un componente de este tipo  |
| Thread Group | Representa un grupo de usuarios. En JMeter cada thread es un usuario virtual. Este tipo de componente permite representar grupos de usuarios. Cada grupo de usuarios del testplan representa un rol o perfil. Todos los threads de un mismo thread group (i.e. todos los usuarios de un grupo) realizan la misma secuencia de acciones, representada por los samplers que agrupa el thread group.  |
| Controllers: Sampler, Logic Controler | Son los únicos componentes del testplan que hacen algo: los **samplers** realizan peticiones contra la aplicación, y los **logic controlers** establecen el orden en que se ejecutan los samplers que agrupan. El resto de componentes (Config Element, Assertion, ...) "matizan" la forma en que se ejecutan los samplers, pero no varían sustancialmente su comportamiento. |
| Config Element | Establecen propiedades de configuración que se aplican a los samplers a los que afectan. |
| Assertion | Comprueban condiciones que aplican a las peticiones que los samplers a los que afectan realizan contra la aplicación. |
| Listener | Recopilan datos de las peticiones que realizan los samplers a los que afectan. |
| Timer | Añaden tiempo extra a la ejecución de las peticiones que realizan contra la aplicación los samplers a los que afectan. |
| Pre-Processor element | Realizan acciones o establecen configuraciones previa a la ejecución de los samplers a los que afectan. |
| Post-Processor element | Realizan acciones o establecen configuraciones posteriormente a la ejecución de los samplers a los que afectan. |


El apartado [4. Elements of a Test Plan](https://jmeter.apache.org/usermanual/test_plan.html) explica en detalle cada uno de los tipos de componentes.

El apartado  [18. Component Reference](https://jmeter.apache.org/usermanual/component_reference.html) contiene la referencia de todos los tipos de componentes que existen en JMeter.

### Ambito y orden de ejecución de componentes de un testplan

Cada componente, según su tipo, es un elemento de Orden (O = Ordered) o Jerárquico (H = Hierarchy).

Los tipos de componentes son (entre paréntesis indicamos si es un elemento de orden o jerárquico):

* Testplan
* Thread Group
* Controllers: Sampler, Logic Controler (O)
* Config Element (H)
* Assertion (H)
* Listener (H)
* Timer (H)
* Pre-Processor element (H)
* Post-Processor element (H)

El ámbito establece a que elementos de tipo O (samplers y logic controlers) afecta un elemento de tipo H.

El orden de ejecución establece en que orden se ejecutan los elementos de un test plan según su tipo y ciertas reglas de asociación entre ellos.

Reglas de ámbito y orden de ejecución:

* Los componentes de tipo Sampler y Logic Controler son de tipo Orden (O), por lo que se ejecutan en la secuencia en que aparecen en el testplan (de arriba a abajo).
* Algunos componentes Logic Controler pueden cambiar el orden en que se ejecutan sus componentes anidados.
* El resto de elementos son de tipo Jerarquico (H), lo que significa que aplican solo a (TODOS) los componentes Samplers descendientes (hermanos, hijos, nietos, ...) de su padre.
* Cuando varios componentes Jerarquicos (H) aplican a un sampler, hay un orden de ejecución que establece en que orden se le aplican:

     1. Configuration elements
     2. Pre-Processors
     3. Timers
     4. Sampler
     5. Post-Processors
     6. Assertions
     7. Listeners

* Si a un Sampler le aplican dos elementos con el mismo orden (según la regla anterior, por ejemplo dos Listeners), se le aplican en el orden en que aparecen en el testplan: de arriba a abajo
* Los elementos jerárquicos que se asocian a los samplers solo se ejecutan si se ejecuta el sampler. Si por ejemplo el sampler esta en un logic controler que hace que no se ejecute, no se ejecutan los elementos asociados.

Veamos el siguiente ejemplo poara ilustrar los conceptos anteriores:

IMAGENNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNn



Este ejemplo es un testplan con un sólo Thread Group. Hay cinco samplers (de nombres One, Two, Three, Four y Five). Hay dos logic controlers, de tipo Simple Controler, con este mismo nombre. Los controlers de este tipo solo agrupan, no alteran el orden de ejecución, por lo que el orden en que se ejecutan los samplers es de arriba a abajo: One, Two, Three, Four y Five.

Hay tres elementos jerárquicos: Timer#1, Assertion#1 y Timer#2. Además, por el tipo de estos elementos, se ejecutan despues de los samplers a los que afectan.

El elemento Timer#2 cuelga directamente del Thread Group, por lo que afecta a todos los samplers que cuelgan (directa o indirectamente) de este elemento, es decir, a todos los samplers.

El elemento Timer#1 cuelga del controller Simple Controller, por lo que afecta a todos los samplers que cuelgan de este mismo controllers directa o indirectamente, esto es, a Two, Three y Four.

El elemento Assertion#1 cuelga del sampler Three, por lo que sólo afecta a este.

Con lo anterior, el orden en que se ejecuta el testplan es (recordemos que si dos componentes jerárquicos del mismo tipo afectan a un mismo sampler, se aplican en el orden en que aparecen en el testplan de arriba a bajo):

```
One
Time#2
```
```
Two
Timer#1
Time#2
```
```
Three
Assertion#1
Timer#1
Time#2
```
```
Four
Timer#1
Time#2
```
```
Five
Time#2
```

El apartado  [4.9 Execution order y 4.10 Scoping Rules](https://jmeter.apache.org/usermanual/test_plan.html#executionorder) del manual de usuario de JMeter explican esto mismo, pero con menos detalle.

### Samplers para peticiones HTTP

Dedicamos una especial atención a los samplers que se utilizan para realizar peticiones HTTP a una aplicación, por ser el tipo de sampler que más se utiliza en JMeter, con diferencia.

Según se documenta en el apartado [HTTP Request](https://jmeter.apache.org/usermanual/component_reference.html#HTTP_Request), existen tres tipos de samplers para realizar peticiones HTTP:

* HTTP Request

* HTTP Request HTTPClient

* AJP/1.3 Sampler

El tercero sirve para probar un servidor Tomcat vía peticiones AJP (sobre HTTP). Este tipo lo ignoraremos en la discusión que sigue. Los otros dos son que se utilizan para que JMeter haga a una aplicación el mismo tipo de petición HTTP que haría un navegador.

Pero existen importantes diferencias entre los dos primeros a nivel de implementación de códígo fuente (por el contrario, a nivel de interfaz GUI el panel de control de ambos componentes es prácticamente igual):

El tipo de componente HTTP Request está basado en la implementación de HTTP que por defecto realiza Java (el JDK). A veces la documentación de JMeter se refiere a él como default (Java) implementation. Por el contrario, el componente HTTP Request HTTPClient está basado en la implementación de HTTP que realiza el framework Apache Commons HttpClient (http://hc.apache.org/httpclient-3.x/). Esta diferencia en la implementación de ambos provoca diferencias cruciales. Resumiendo, la implementación Java por defecto del tipo de sampler HTTP tiene una serie de carencias / defectos que lo hacen inadecuado para su uso en pruebas de rendimiento. Esto lo documenta el manual de usuario en 18.1.2 HTTP Request.

### Grabación de un testplan (para aplicaciones web)

Existen básicamente dos estrategias para diseñar un testplan de JMeter (un fichero .jmx) para una aplicación web:

* A mano: creando cada componente mano en el lugar adecuado del árbol, y configurando el componente vía su panel de control.

* De forma automatizada: utilizando una herramienta que capture las peticiones HTTP que realiza el navegador, a medida que uno navega por la aplicación, y genere con cada una de estas peticiones HTTP un componente sampler en el árbol del testplan.

La primera es la estrategia que podríamos llamar de hacerlo todo a mano. La segunda, si bien no nos genera el testplan completamente, si al menos los samplers HTTP que el testplan tiene que ejecutar contra la aplicación. Además, la segunda requerirá que una vez creados los samplers HTTP con la herramienta que sea, modifiquemos la configuración por defecto de estos y añadamos nuevos componentes (timers, listeners, ...) que no crea la herramienta. En cualquier caso, la segunda estrategia ahorra trabajo.

Existen básicamente dos herramientas que nos permiten generar de forma automática los samplers HTTP de un testplan:

* El componente HTTP Proxy Server de JMeter.

* La utilidad Badboy© (http://www.badboy.com.au/)

Ambas herramientas generan un .jmx, que como decimos más arriba, normalmente no es directamente utilizable por JMeter y suele requerir ajustes adicionales.


**HTTP Proxy Server**

El HTTP Proxy Server es un tipo de componente de JMeter, igual que cualquier otro componente como el HTTP Request o el SMTP Sampler (por citar algunos). La diferencia respecto a éstos es que el HTTP Proxy Server sólo se puede crear en el Workbench de la interfaz GUI, con lo que no se graba en el fichero .jmx cuando grabamos el testplan vía la interfaz GUI.

Nota:

Hay también otros componentes muy útiles que sólo se pueden crear en el Workbench, ver en el menú emergente del Workbench la entrada Non-Test Elements.

El panel de control de este componente tiene un botón Start que al ser pulsado arranca un servidor proxy embebido en JMeter. Como cualquier servidor proxy, escucha en un puerto de la máquina por el que recibe peticiones HTTP de un navegador cliente, y las envía a la URL que estas indican. Cuando la URL (aplicación web) responde, devuelve la respuesta al navegador que hizo la petición. Esto es exactamente lo que hace el HTTP Proxy Server de JMeter, pero a diferencia de otros proxys, no cachea las peticiones HTTP ni las respuestas a estas por parte de la aplicación, sino que el procesamiento que realiza con las peticiones consiste en generar para cada una de ellas un componente HTTP Request (o HTTP Request HTTPCLient, según se configure).

La conclusión es que a medida que el usuario navega por la aplicación con su navegador cliente, el HTTP Proxy Server traduce éstas en componentes HTTP Request del testplan. Para ello evidentemente se necesita configurar el navegador utilizado para que haga peticiones al HTTP Proxy Server, en lugar de hacerlas directamente a la aplicación.

El panel de control del HTTP Proxy Server permite establecer cosas como:

* El puerto de escucha del proxy.

* El tipo del sampler que debe generarse para cada petición HTTP (HTTP Request ó HTTP Request HTTPClient, recordar que la primera NO es adecuada para pruebas de rendimiento).

* El componente del árbol en que se crearán los samplers.

* Si se deben excluir de la grabación peticiones que obtienen imágenes, hojas de estilo, scripts JavaScript u otras URLs o tipos de contenidos.

* ...

En el enlace [Recording Tests](https://jmeter.apache.org/usermanual/jmeter_proxy_step_by_step.pdf) del sitio oficial de JMeter se puede descargar un tutorial que explica como configurar el HTTP Proxy Server y el navagador para capturar un testplan.

En el apartado [HTTP Proxy Server](https://jmeter.apache.org/usermanual/component_reference.html#HTTP_Proxy_Server) del manual de usuario puede encontrarse la documentación de referencia de este componente.

En versiones de JMeter anteriores a la 2.4, el HTTP Proxy Server no podía capturar peticiones HTTPS, por lo que cuando la aplicación a testear utilizaba este protocolo, se requería otra herramienta como Badboy© (que si puede capturar peticiones HTTPS) para generar los samplers HTTP. En la versión actual de JMeter (2.4) no existe esta limitación. Aún así, el tutorial mencionado más arriba está sin actualizar, por lo que sigue dando la referencia de Badboy© cuando el protocolo es HTTPS.