# Construcción de Planes de Prueba con JMeter 💥

## Descripción 📋

Este manual explica los conceptos necesarios para ejecutar testplans (ficheros .jmx) de JMeter. En particular, se explican las posibilidades de las opciones de línea de comandos para ejecutar scripts .jmx, el orden en que se leen las propiedades que aplican a la ejecución de JMeter, los conceptos de testing remoto y distribuido, y un ejemplo de como se pueden llevar a cabo ambos con JMeter, como JMeter captura la información durante la ejecución de un testplan (por ejmeplo para un posterior estudio del rendimiento en base a ésta), y finalmente se explica que el estudio del rendimiento de una aplicación es realmente un estudio estadístico, se explican las medidas estadísticas que implementa JMeter para testear el rendimiento de una aplicación, y los listeners de JMeter que las implementan.

## Modo de empleo 🚂

Para la instalación de la herramienta y configuración de idioma, consultar la referencia Introducción a JMeter / Modo de empleo / Instalación, configuración, y acceso a la documentación.

## Opciones de línea de comando 📳

Una vez diseñado un testplan (fichero .jmx), vía la interfaz GUI, este se puede ejecutar desde la misma interfaz GUI o desde la línea de comando.

La línea de comando proporciona muchas más posibilidades que la interfaz GUI para ejecutar scripts de JMeter, y además es necesario emplearla para automatizar tareas de JMeter.

La sintaxis general de la línea de comando es:

```
${JMETER_HOME}/bin/jmeter -n -t path/to/testplan.jmx [resto de opciones ...]
```

Donde -n indica a JMeter que NO ejecute la interfaz GUI (por defecto, si no se emplea esta opción, JMeter ejecutará la interfaz GUI), y con -t se indica a JMeter el fichero .jmx a ejecutar.

Otras opciones de la línea de comando muy utilizadas son:

### -d PATH

Establece el directorio que JMeter asumirá como directorio por defecto durante su ejecución. Por ejemplo, si no se especifica un path en el argumento de -j, el fichero de log se generará en este directorio.

### -l FILEPATH

Especifica el filepath del fichero de result samples que generará JMeter en la ejecución. Si no se especifica esta opción, no se generará un fichero de result samples, excepto si un listener del testplan lo genera explícitamente.

Esta opción es equivalente a especificar un listener en el testplan, situado en éste de forma que se asocie a todos los samplers que se ejecutan.

### -j FILEPATH

Es el filepath al fichero de log de JMeter. Si no se especifica esta opción, se asume por defecto jmeter.log en el directorio desde el que se ha lanzado la ejecución de JMeter, o el que especifique la opción -d . Puede establecerse también mediante propiedades: ver log_file en jmeter.properties

Para las opciones -l y -j El nombre de fichero que se especiqique con la opción -l ó -j puede ser variable en función de la fecha y la hora actual. Por ejemplo si se especifica -j 'jmeter_'yyyyMMddHHmmss'.log' (incluidas las comillas, idem para la opción -l), el fichero se genera con ese formato de nombre. Los formatos de fecha y hora que se pueden utilizar son los que se especiifcan en la clase SimpleDateFormat del JDK.


```
-L [package_name[.classname]=]PRIORITY_LEVEL
```


En JMeter se puede especificar el nivel de log para cada uno de los diferentes packages y clases que componen JMeter, o bien un mismo nivel de log para todos ellos. En jmeter.properties, sección Logging Configuration, pueden verse los packages y clases para los que se puede especificar un nivel de log. Las propiedades tienen el formato log_level.[package_name][.classname]=[PRIORITY_LEVEL] (los corchetes indican que la parte incluida dentro es opcional). Donde PRIORITY_LEVEL es el nivel de log, puede ser uno de estos: FATAL_ERROR, ERROR, WARN, INFO, DEBUG
Pues bien, este modificador de la línea de comando permite especificar esto mismo, pero en la línea de comando. Nótese que en la línea de comando NO se especifica el prefijo log_level. de los nombres de propiedades.

Si no se especifica un package o/y una clase, el PRIORITY_LEVEL aplica a todos los packages o/y classes de JMeter.
Esta opción se puede especificar tantas veces como se desee en la línea de comando.

Los valores por defecto de esta opción para cada package/clase son los que se especifican en el fichero jmeter.properties.

El nivel de detalle que se especique con esta opción aplica al fichero especificado con la opción -j (ó para jmeter.log si no se especifica aquella opción).

### -q FILEPATH

Cuando se ejecuta JMeter, el usuario pueden especificar nuevas propiedades, además de las que JMeter lee del fichero jmeter.properties y de las propiedades del sistema que aporta la JVM. Esto se puede hacer de dos maneras: con el modificador -J o con el modificador -q.
Este último permite especificar en la línea de comando un fichero de propiedades que serán leídas por JMeter durante el arranque y mantenidas en memoria durante la ejecución.

Las propiedades que se especifiquen en este fichero pueden ser cualesquiera que no se especifiquen en jmeter.properties, por ejemplo propiedades utilizadas en el testplan mediante las funciones __P y __property.

### -Jpropiedad=valor

La opción -J permite especificar en la línea de comando el valor de cualquier propiedad de JMeter (las que se especifican en jmeter.properties) o propiedad de usuario. Si no existe, la propiedad se crea con el valor que se especifique.

Esta opción se puede especificar tantas veces como se desee en la línea de comando.

### -p FILEPATH

Especifica el filepath del fichero de propiedades de JMeter que se asumirá como tal durante el arranque de JMeter. Por defecto, si no se especifica esta opción, el fichero es jmeter.properties, en el directorio bin/ de la instalación de JMeter.

### -Dpropiedad=valor

Permite cambiar el valor de una propiedad de sistema (las definidas por la JVM). Esta opción se puede especificar tantas veces como se desee en la línea de comando.

### -S FILEPATH

Permite especificar un fichero de propiedades (con la sintaxis de los mficheros .properties) que cambia el valor de varias propiedades de sistema para la ejecución de JMeter.

Como sucede con un navegador, a veces entre el cliente JMeter y la aplicación puede haber un servidor proxy. Para esto JMeter dispone de opciones de línea de comando para especificar el acceso a la aplicación vía el proxy: -H, -P, -N, -u y -a. [1.4.3 Using JMeter behind a proxy](https://jmeter.apache.org/usermanual/get-started.html#proxy_server).

Por ejemplo, el siguiente comando ejecuta el testplan naos.jmx desde línea de comando, indicando a JMeter que asuma /home/ecastilla como directorio home, especificando un fichero de log con el formato de nombre jmeter_yyyyMMddHHmmss.log, que genere un fichero de result sample con el nombre naos_yyyyMMddHHmmss.csv, definidiendo las propiedades user.name, user.pass, mas las que establezca el fichero /home/ecastilla/user.properties (el carácter \ indica continuación de línea):

```
/usr/local/jmeter/bin/jmeter -n -d /home/ecastilla -t /home/ecastilla/naos.jmx  \
                                  -j 'jmeter_'yyyyMMddHHmmss'.log' -L DEBUG \
                                  -l 'naos_'yyyyMMddHHmmss'.csv' \
                                  -Juser.name=ecastilla -Juser.pass=2.3rt5@7 \
                                  -q /home/ecastilla/user.properties
```

Casi todas las opciones tienen un nombre corto y un nombre largo que NO hemos especificado en las anteriores descripciones.

En el manual de JMeter, en la sección [2.5 Configuring JMeter](https://jmeter.apache.org/usermanual/get-started.html#running) puede encontrarse la referencia completa de las opciones de línea de comando.

En las secciones que siguen mencionaremos otras opciones que NO aparecen en la lista anterior.

## Orden de procesamientos en el arranque 🔣
Nótese que una misma propiedad podría especificarse a la vez en varios sitios, para una misma ejecución de JMeter, en cada uno de estos sitios con un valor distinto. Por ejemplo:

* Con el modificador -J en la línea de comando
* En un fichero especificado con el modificador -q
* En el fichero jmeter.properties o/y en user.properties o/y en system.properties
* ...

¿Cual de los valores acaba teniendo la propiedad durante la ejecución de JMeter ? Esto es lo que explica este apartado.

El orden en que se procesan las cosas durante el arranque de JMeter es:

* -p propfile es procesado

* jmeter.properties o el fichero que se especifique con -p. Si se especifican ambos, primero se carga jmeter.properties y luego el fichero especificado con -p

* -j logfile

* Se inicializa el sistema de logging

* user.properties es procesado

* system.properties es procesado

* Se procesan el resto de opciones de línea de comando

[1.5 Configuring JMeter](https://jmeter.apache.org/usermanual/get-started.html#configuring_jmeter)

## Modos de ejecución de JMeter ⛽

Como hemos explicado en secciones anteriores, hay dos formas de ejecutar JMeter según que queramos que se muestre o no la interfaz GUI:

* Desde línea de comando sin mostrar la interfaz GUI.

Especificar la opción -n en la línea de comando.

* Mostrando la interfaz GUI: no especificar la opción -n al arrancar JMeter.
* Si ejecutamos un testplan desde la interfaz GUI, el menú Run proporciona opciones para arrancar y parar la ejecución. Si ejecutamos un testplan desde la línea de comando (con los modificacdores -n y -t), el directorio bin/ proporciona ejecutables para parar la ejecución desde la línea de comando.

Aparte, JMeter se puede ejecutar de una de estas dos maneras:

* Como cliente

* Como servidor
Como cliente, JMeter hace de cliente de la aplicación a testear, mas o menos como el navegador de un usuario (diferencia: JMeter puede simular n usuarios).

Como cliente, JMeter hace de cliente de la aplicación a testear, mas o menos como el navegador de un usuario (diferencia: JMeter puede simular n usuarios).

JMeter también se puede arrancar como un software servidor: se pueden arrancar n instancias de JMeter en modo servidor, en otras tantas máquinas, y controlar estas instancias servidoras con otro JMeter que actúa como cliente de éstos, enviándoles el testplan y recopilando y fusionando los resultados de sus ejecuciones. A esto último es a lo que se le llama testing remoto/distribuido (remoto cuando hay una sola instancia de JMeter servidor, y distribuido cuando hay varias instancias de JMeter servidores).

El testing distribuido se usa por ejemplo cuando no se dispone de una máquina capaz de crear el número de threads suficiente que se necesitan para testear la aplicación. En este caso, en lugar de disponer de una gran máquina con recursos suficientes para crear un gran número de threads, es preferible diponer de varias máquinas más pequeñas. En cada una de ellas se ejecuta una instancia servidora de JMeter. Desde otra máquina se ejecuta una instancia cliente de JMeter, que envía a todas las instancias servidoras el testplan. Todas las instancias servidoras ejecutarán el mismo testplan, con el mismo número de threads. La instancia cliente se encarga internamente de unificar los resultados de las ejecuciones de todas las instancias servidoras.

El testing remoto se usa por ejemplo cuando no se dispone de una máquina con conectividad directa con la aplicación (con lo que no puede ejecutar un testplan que le envíe peticiones), pero si con conectividad con una instancia servidora de JMeter (que si tiene conectividad directa con la aplicación). En este caso, la instancia cliente de JMeter envía el testplan a la instancia servidora, esta lo ejecuta contra la aplicación, y devuelve a la instancia cliente los resultados de la ejecución. Toda esta comunicación sucede internamente entre la instancia cliente y la instancia servidora de JMeter.

En el testing remoto/distribuido aplica lo siguiente:

* El ejecutable que se utiliza para arrancar una instancia servidora de JMeter es bin/jmeter-server (bin\jmeter-server.bat en Windows). Excepto algunas opciones de línea de comando como -n y -t, que no tienen sentido para el ejecutable de instancias servidoras, el resto aplican a ambos ejecutables.

* Las instancias servidoras de JMeter NO se pueden ejecutar en modo GUI, sólo en modo línea de comando.

* Todas las instancias de JMeter, tanto el cliente como los servidores deben ejecutar la misma versión de JMeter y la misma versión de la máquina vitual de Java.

* Cuando se ejecuta un fichero .jmx de manera distribuida, todas las instancias servidoras ejecutan el mismo testplan, con el mismo número de usuarios, no hay una distribución de la carga de threads entre los nodos servidores ni nada parecido. Los resultados de las ejecuciones del testplan por todos los servidores se generan en la máquina de la instancia cliente: no hay un resultado de la ejecución por cada instancia servidora, por lo que no hay necesidad de hacer fusiones de ficheros.

* La diferencia entre una ejecución distribuida y ejecutar un cliente de JMeter en cada una de las máquinas es que 1) No hay que ejecutar el testplan en cada una de las máquinas, sino que la instancia cliente le envía el testplan a todas las instancias servidoras, y 2) No hay que unificar los n ficheros de sample result que se generarían entre las diferentes máquinas, porque la instancia cliente ya se encarga de unificar los resultados de todos los servidores.

* Si el testplan utiliza un fichero de datos para su ejecución (p.e. un fichero CSV), la instancia cliente NO envía estos ficheros a las instancias servidoras, sino que el usuario debe asegurarse de que cada instancia servidora tiene acceso a su fichero de datos antes de comenzar la ejecución del testplan.Consejo: en estos casos, poner los ficheros en una unidad de red o ejecutar el test dentro de un script o tarea de ant a modo de wrapper que envíe los ficheros antes de ejecutar el test.

* La comunicación entre la instancia cliente de JMeter y las instancias servidoras se realiza internamente mediante protocolo RMI. Desde la version 2.3.1 no es necesario ejecutar por separado el servidor rmiregistry, pues el proceso servidor de JMeter ya se encarga de ello (ver fuentes de bin/jmeter-server y bin\jmeter-server.bat)

* Por defecto, el puerto de escucha de las instancias servidoras de JMeter es el 1099, por lo que no pueden ejecutarse dos instancias servidoras en la misma máquina, a menos que cada una utilice un puerto distinto. Cuando se arranca una instancia servidora, se le puede indicar un puerto distinto del 1099 de dos maneras:

* * Estableciendo una variable de entorno SERVER_PORT, cuyo valor sea el número de puerto, en el proceso en el que se va a ejecutar JMeter.

* * Modificando la propiedad server_port de jmeter.properties, por ejemplo con el modificador -J desde la línea de comando.

* Nótese que ejecutar una instancia servidora en la máquina del servidor de aplicaciones afecta al rendimiento de ésta. El procedimiento recomendado es disponer de varias máquinas pequeñas en el mismo segmento de red que el servidor de aplicaciones, para ejecutar en ellas las instancias servidoras [13. Remote Testing](https://jmeter.apache.org/usermanual/remote-test.html)

## Un ejemplo de sesión de testing distribuido

La siguiente secuencia es un ejemplo de sesión de testing distribuido en el que se arrancan dos instancias servidoras de JMeter y una instancia cliente.

El ejemplo no es nada real porque las dos instancias servidoras y el cliente se ejecutan en la misma máquina Windows, pero es ilustrativo de los conceptos explicados más arriba, y con mínimos cambios puede trasladerse a un entorno realmente distribuido.

Asumimos que en la sesión de línea de comando de Windows se ha definido una variable de entorno JMETER_HOME, cuyo valor es el path absoluto al directorio raiz de la instalación de JMeter. Si no tiene definida esa variable, en la sesión de línea de comando teclear:

```
set JMETER_HOME=path\to\JMeter
```

(sustituyendo path\to\JMeter por el path absoluto que sea)

* Arrancar los servidores (no admiten modo GUI):

```
> start %JMETER_HOME%\bin\jmeter-server.bat 
```

```
> start %JMETER_HOME%\bin\jmeter-server.bat -Jserver_port=1234
```

El segundo servidor lo hemos arrancado estableciando el puerto 1234 para RMI. Lo hemos hecho estableciendo un valor para la propiedad server_port desde la línea de comando, con lo que no hay que modificar jmeter.properties, pero igual podríamos haberlo hecho modificando modificando el fichero de propiedades antes de arrancar la segunda instancia o arrancándola desde otra sesión de línea de comando en la que previamente hubiesemos ejecutado set SERVER_PORT=1234.

* Arrancar el cliente (modo GUI)

```
>%JMETER_HOME%\bin\jmeter.bat -Jremote_hosts=127.0.0.1:1099,127.0.0.1:1234
```

Al cliente hay que especificarle la IP o hostaname y puerto de cada instancia servidora. Esto se hace con la propiedad remote_hosts (ver bin/jmeter.properties).

* En el cliente, cargar un testplan:

```
File / Open
```

Seleccionar por ejemplo %JMETER_HOME%\printable_docs\demos\SimpleTestPlan.jmx, que viene con la distro de JMeter. Observar que el testplan especifica un solo usuario y una sola ejecución.

* Desde la interfaz GUI, modificar el testplan cargado en la instancia cliente, añadiendo un listener de tipo Aggregate Report (para ver cuantas veces se ejecuta cada sampler). Colgarlo del Thread Group Jakarta Users.

* Ejecutar el testplan en local:

```
Run / Clear All , Run / Start
```

Observar que hay dos ejecuciones del sampler Home Page, y una de los restantes, total 4 samples ejecutados.

* Ejecutar el testplan de forma remota:

```
Run / Clear All , Run / Remote Start / 127.0.0.1:1234
```

Observar que se realiza el mismo número de ejecuciones de los samplers (hemos ejecutado en un solo servidor).

* Ejecutar el testplan de forma distribuida:

```
Run / Clear All , Run / Remote Start All
```

Observar que realizan el doble de ejecuciones de cada sampler, porque hemos ejecutado el testplan sobre dos servidores a la vez.

* Ejecutar el testplan de forma distribuida, pero desde línea de comando:

```
> %JMETER_HOME%\bin\jmeter.bat -n -r -Jremote_hosts=127.0.0.1:1099,127.0.0.1:1234 -t \ 
```

```
%JMETER_HOME%\printable_docs\demos\SimpleTestPlan.jmx -j SimpleTestPlan.jtl
```
También  se puede ejecutar el testplan de forma distribuida de otra forma: en el  fichero jmeter.propertiesz de la instalación cliente, especificar en la  propiedad remote_hosts la lista de direcciones IP o nombres de host de  las instancias servidoras, opcionalmente con el puerto de RMI, separados  por comas. Por ejemplo:

```
remote_hosts=192.168.20.34:1234,192.168.20.60
```

Una vez hecho, utilizar la opción -r (remote) de la línea de comando de la instancia cliente. Esta opción hace que la línea de comando se refiera a una ejecución remota / distribuida:

```
> %JMETER_HOME%\bin\jmeter.bat -n -r -t \
       %JMETER_HOME%\printable_docs\demos\SimpleTestPlan.jmx -j SimpleTestPlan.jtl

```

O en lugar de esto se puede utilizar la opción -R LISTA (donde LISTA es un valor como el de remote_hosts. Esta opción es una abreviatura de -r -Jremote_hosts=LISTA:

```
> %JMETER_HOME%\bin\jmeter.bat -n -R 127.0.0.1:1099,127.0.0.1:1234 -t \
 %JMETER_HOME%\printable_docs\demos\SimpleTestPlan.jmx -j SimpleTestPlan.jtl 

```

Resumen de opciones de línea de comando específicas para ejecuciones remotas / distribuidas

**-J**

Establece por línea de comando el valor de la propiedad remote_hosts, server_port, server.rmi.port y server.rmi.localport

**-r**

Indica que la línea de comando se refiere a las instancias servidoras especificadas con la propiedad remote_hosts

**-R**

Indica que la línea de comando se refiere a las instancias servidoras que se especifiquen como argumento

**-G**

Establece propiedades en las instancias servidoras: igual que -J, pero se refiere a las instancias servidoras en lugar de a la instancia cliente como hace -J

**-X**

Especifica que las instancias servidoras terminen después de ejecutar el testplan. Se emplea con las opciones -r y -t

## Ejecución de un testplan. Captura y procesamiento de la información
Una vez generado el fichero .jmx, se puede ejecutar o bien desde la línea de comando o bien desde la interfaz GUI.

## Ejecutar un testplan desde la línea de comando
Lo fundamental que hay que saber para ejecutar un script .jmx desde la línea de comando es que cuando se especifica la opción -n en la línea de comando, se le indica a JMeter que NO muestre la interfaz GUI y que ejecute el .jmx que se le especifique con la opción -t .

Para más información sobre opciones de la línea de comando, consultar el apartado Opciones de línea de comando.

Por ejemplo (con el caracter \ indicamos continuación de la línea de comando):

```
/usr/local/jmeter/bin/jmeter -n -t /home/ecastilla/eco/eCO_bandejas.jmx  \
                                  -Jjmeter.save.saveservice.output_format=csv \
                                  -l /home/ecastilla/eco/eCO_bandejas_20101124103504.csv \
                                  -j /home/ecastilla/eco/eCO_bandejas_20101124103504.log  \
                                  -q /home/ecastilla/eco/eCO_bandejas.properties
```

Este ejemplo ejecuta desde línea de comando un testplan /home/ecastilla/eco/eCO_bandejas.jmx. Además, para la ejecución establece la propiedad jmeter.save.saveservice.output_format de forma que el fichero de sample result se genere en formato CSV, especifica el fichero de sample result con el modificador -l y bel fichero de log de la ejecución con el modificador -j (estos dos ficheros los establece de forma que su nombre es función de la hora de ejecución). Además, con el modificador -q especifica un fichero de propiedades que serán leídas por JMeter durante el arranque.

Si en logar de ejecutar el testplan en local, se ejecutara en dos instancias servidoras de JMeter con las direccciones IP 192.168.10.25 y 192.168.10.26 (puerto por defecto 1099), el comando sería:

```
Created the tree successfully using eCO_bandejas.jmx
Starting the test @ Wed Nov 24 10:35:05 CET 2010 (1290591305401)
Waiting for possible shutdown message on port 4445
Tidying up …    @ Wed Nov 24 10:36:36 CET 2010 (1290591396889)
… end of run
```

Observese que JMeter escucha en el puerto 4445 mensajes de shutdown. Para enviarle un mensaje de éstos y terminar la ejecución del proceso de JMeter basta con ejecutar el comando.

```
/usr/local/jmeter/bin/shutdown.sh
```

## Ejecutar un testplan desde la interfaz GUI
Arrancar JMeter en modo GUI, esto es, sin especificar el modificador -n en el comando de arranque. Opcionalmente, si no se especificó el modificador -t en el comando de arranque, hay que seleccionar la opción File / Open para abrir el fichero .jmx que se desee ejecutar. A continuación, en el menú Run seleccionar la opción que deseemos.

Por ejemplo, supongamos que el comando de arranque es:

```
/usr/local/jmeter/bin/jmeter -t /home/ecastilla/eco/eCO_bandejas.jmx  \
                                  -Jjmeter.save.saveservice.output_format=csv \
                                  -l /home/ecastilla/eco/eCO_bandejas_20101124103504.csv \
                                  -j /home/ecastilla/eco/eCO_bandejas_20101124103504.log  \
                                  -q /home/ecastilla/eco/eCO_bandejas.properties \
                                  -Jremote_hosts=192.168.10.25,192.168.10.26
```

Nótese que no especificamos el modificador -n ni -r (no queremos ejecutar desde la línea de comando ni en remoto).

Con este comando de arranque JMeter muestra la interfaz GUI al tiempo que carga el testplan que se especifica con -t, se prepara para guardar datos en los ficheros de sample result y log que se especifican, y lee las propiedades que se especifican en el fichero .properties (una vez abierta la interfaz GUI se puede hacer la prueba de crear en el Workbench un componente Non-Test Elements / Property Display, y comprobar que las propiedades del fichero .properties se muestran con los valores que se le han asignado).

Si simplemente se quiere arrancar la interefaz GUI sin cargar un .jmx ni configurar nada mas, el comando de arranque sería:

```
/usr/local/jmeter/bin/jmeter
```

En el menú Run hay opciones para ejecutar un testplan en local (opción Start) y en remoto (opción Remote Start All), o en remoto pero solo en alguna de las instancias servidoras de JMeter (opciones Remote Start).

Análogamente, hay opciones para parar una ejecución local (opciones Stop y Shutdown) o remota, o parar las instancias servidoras.

## Como JMeter captura la información de la ejecución de un testplan

JMeter captura la información de ejecución de un testplan de una de estas dos formas:

* Mediante el modificador -l de la línea de comando (ver apartado Opciones de línea de comando).

* Mediante listeners (ver apartados Listeners y Tipos de componentes de un testplan).

Internamente, la información capturada por JMeter durante la ejecución de un testplan es siempre la misma: para cada ejecución de un sampler que figure en el testplan, JMeter captura los campos de información que se especificaron para los ficheros de result samples (ver apartado Ficheros de sample result), mas opcionalmente la respuesta de la aplicación. La diferencia entre los listeners y el modificador -l reside en como se filtra y muestra al usuario la información interna capturada por JMeter:

* Los listeners pueden procesar la información capturada de muchas formas distintas (cada listener procesa y muestra la información de una manera), y opcionalmente, pueden filtrar los campos de información capturados, generando un fichero en disco.

* Por el contrario, la opción -l simplemente genera un fichero de result sample en disco, con los campos que se especifiquen en el fichero jmeter.properties .

Pero en cualquiera de los dos casos, internamente la información capturada por JMeter es la misma.

Para información sobre los ficheros de result sample que se generan con la copción -l, ver Ficheros de sample result.

En cuanto a los listeners, existen varias funcionalidades comunes a todos ellos, además de la funcionalidad específica de cada uno en cuanto a como muestran la información capturada. Las funcionalidades comunes a todos los listeners son:

* Opcionalmente, todos los listeners pueden persistir la información que capturan en un fichero en disco. Para ello, cumplimentar el campo Filename:.

* Opcionalmente, también pueden filtrar que columnas de los result samples se quiere grabar en ese fichero: botón Configure.

* Opcionalmente también, se puede filtrar para que en el fichero se capturen solo las peticiones que con exito, las peticiones con error, o ambas: checks Errors y Successes.

El listener más simple de todos es el Simple Data Writer, que no tiene ninguna funcionalidad específica sino sólo las comunes a todos los demas listeners, explicadas mas arriba.

Otra funcionalidad de los listeners es mostrar un fichero de sample result una vez generado (bien con la opción -l o bien con otro listener). Para ello, crear un listener con el que se quiera ver el fichero, por ejemplo en el Workbench, y cargar el fichero con el botón Browse en el campo Filename:.

## Medición del rendimiento con JMeter. Conceptos estadísticos

**Concepto de serie estadística** 

Una serie estadística es una lista de valores referidos a los individuos de una población, cada no de los valores de la lista se llama una muestra (sample en inglés).

Los ficheros de result samples son series estadísticas en las que los individuos son las peticiones (cada una de las líneas del fichero, identificados por el campo timestamp), y algún valor que se pueda extraer del fichero para cada sampler, bien tomándolo directamente de alguna de las columnas del fichero, o bien porque sea un valor calculado entre varias columnas.

Por ejemplo, supongamos que extraemos del result file todas las líneas correspondientes a un mismo sampler (= un determinado valor del campo label), y para cada línea extraida nos quedamos con la columna timestamp y bytes. Tenemos una serie estadística: número de bytes por milisegundo. Si sumamos todos los bytes que están dentro del mismo segundo tenemos el número de bytes por segundo (esto también lo hacen algunos de los listeners de JMeter).

Conclusiones:

* Los ficheros de result samples nos permiten generar series estadísticas para estudiar el rendimiento, y la mayoría de los listeners de JMeter lo que hacen es esto mismo.

* Hacer una prueba de rendimiento consiste básicamente en generar una o varias series estadísticas (vía la ejecución de un fichero .jmx), que nos permiten estudiar el rendimiento de la aplicación extrayendo de ellas una o varias medidas estadísticas.

**Medidas estadísticas**

* Mínimo (Máximo)
El mínimo (máximo) de una serie estadística es el menor (mayor) de los valores entre todas las muestras que componen la serie.

* Media (Average o menos frecuentemente Mean en inglés)
La suma de todos los valores de la serie partido por el número de muestras. Conceptualmente es el valor más representativo de la serie (no el que más se repite, que sería la moda). Es decir, si nos pidieran dar un solo valor que represente a toda la serie, daríamos este. Otra forma de verlo es como el punto medio entre el mínimo y el máximo.

* Mediana (Median en inglés)
Se obtiene poniendo en secuencia todos los valores de la serie, y a cada valor asociado a un individuo le asocio además la suma de él mismo con todos los anteriores (tengo dos series para los mismos individos: la original y la de los acumulados). Por otra parte, sumo todos los valores de la serie y eso nos da una cantidad N. Pues bien, la mediana es el valor de la serie (original) tal que su acumulado asociado es el primero que supera o es igual al 50% de N. Dicho de otra forma, la mediana es el valor de la serie que deja a su izquierda el 50% de la distribución. A la mediana también se le llama percentil 50. Conceptualmente es una medida que nos indica como de cerca del mínimo o del máximo está la primera mitad de los valores de la serie, lo que nos da una idea de hacia cual de los dos extremos se agrupa. Idem para el percentil 90, 95, ...

* Desviación estándard (standard deviation en inglés)
Para cada valor de la serie obtenermos el cuadrado de su distancia respecto a la media (calculando (valor – media)2). Para esta nueva serie de valores calculamos su media y le hacemos la raiz cuadrada. Conceptualmente es una medida como de agrupados respecto a la media (average) están los valores de la serie. Una desviación estándar pequeña significa que la mayoría de los valores están muy cerca (a derecha e izquierda) de la media. En suma, nos dice como de representativa de la serie es el valor de la media. La desviación estándard tiene la particularidad de que se expresa en la misma unidad de medida que los valores de la serie.

**Medidas del rendimiento en JMeter**

Los listeners de JMeter orientados al estudio del rendimiento de una aplicación son:

* Aggregate Graph

* Aggregate Report

* Summary Report

Además, existen proyectos de código abierto cuyo objetivo es construir nuevos listeneres para JMeter: http://code.google.com/p/jmeter-plugins/

Los listener anteriores permiten medir el rendimiento de una aplicación en términos de:

* Tiempo de respuesta

* % de errores respecto al número total de peticiones

* Throughput (número de páginas por segundo)

* Número de bytes por unidad de tiempo.

Listener proporciona ciertos valores del tiempo de respuesta, por ejemplo el Aggregate Report proporciona los valores mínimo, máximo, medio, mediana, y percentil 90 del tiempo de respuesta. Para información de referencia sobre que es cada uno de los datos que se muestran en los listeners, consultar el manual de usuario, sección 18.3 Listeners.

Conociendo la especificación de los ficheros de result samples (ver apdo Ficheros sample result), y con la ayuda de otras herramientas (Excel, Pentaho, lenguajes de programación, ...), podemos construir nuestras propias medidas del rendimiento.
