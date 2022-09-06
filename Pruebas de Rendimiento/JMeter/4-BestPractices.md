# Buenas practicas JMETER	📚

https://jmeter.apache.org/usermanual/best-practices.html

## Utilice siempre la última versión de JMeter 1️⃣

El rendimiento de JMeter se mejora constantemente, por lo que se recomienda encarecidamente a los usuarios que utilicen la versión más actualizada.
Asegúrese de leer siempre la [lista de cambios](https://jmeter.apache.org/changes.html) para estar al tanto de las nuevas mejoras y componentes. Debe evitar absolutamente el uso de versiones anteriores a 3 versiones anteriores a la última.

## Utilice el número correcto de Threads 2️⃣

Las capacidades de su hardware, así como el diseño del plan de prueba, afectarán la cantidad de Threads que puede ejecutar de manera efectiva con JMeter. El número también dependerá de qué tan rápido sea su servidor (un servidor más rápido hace que JMeter trabaje más porque devuelve una respuesta más rápido). Al igual que con cualquier herramienta de prueba de carga, si no dimensiona correctamente la cantidad de Thread, se enfrentará al problema de "omisión coordinada" que puede generar resultados incorrectos o inexactos. Si necesita pruebas de carga a gran escala, considere ejecutar varias instancias de CLI JMeter en varias máquinas usando el modo distribuido (o no). Cuando se usa el modo distribuido, el archivo de resultados se combina en el nodo del controlador; si se usan varias instancias autónomas, los archivos de resultados de muestra se pueden combinar para un análisis posterior. Para probar cómo funciona JMeter en una plataforma determinada, se puede utilizar el muestreador JavaTest. No requiere ningún acceso a la red, por lo que puede dar una idea del rendimiento máximo que se puede lograr.

JMeter tiene una opción para retrasar la creación de Threads hasta que el thread comience a muestrear, es decir, después de cualquier retraso de grupo de thread y el tiempo de aceleración del thread en sí. Esto permite un número total muy grande de threads, siempre que no haya demasiados activos al mismo tiempo.

## Dónde colocar el administrador de cookies 3️⃣

Casi todas las pruebas web deben usar compatibilidad con cookies, a menos que su aplicación específicamente no use cookies. Para agregar compatibilidad con cookies, simplemente agregue un administrador de cookies HTTP a cada grupo de subprocesos en su plan de prueba. Esto asegurará que cada subproceso obtenga sus propias cookies, pero compartidas entre todos los objetos de solicitud HTTP .

![](imagenes/http-cookie-manager.png)

Para agregar el Administrador de cookies HTTP , simplemente seleccione el Grupo de subprocesos y elija Agregar → Elemento de configuración → Administrador de cookies HTTP, ya sea desde el menú Editar o desde el menú emergente del botón derecho.

## Dónde colocar el Administrador de autorizaciones 4️⃣

El administrador de encabezado HTTP le permite personalizar qué información envía JMeter en el encabezado de solicitud HTTP. Este encabezado incluye propiedades como "User-Agent", "Pragma", "Referer", etc.

El Administrador de encabezados HTTP , al igual que el Administrador de cookies HTTP , probablemente debería agregarse en el nivel de Grupo de subprocesos, a menos que, por alguna razón, desee especificar encabezados diferentes para los diferentes objetos de Solicitud HTTP en su prueba.

## Uso de la grabadora de secuencias de comandos de prueba HTTP(S) 5️⃣

Consulte  [HTTP(S) Test Script Recorder](https://jmeter.apache.org/usermanual/component_reference.html#HTTP(S)_Test_Script_Recorder) para obtener detalles sobre cómo configurar la grabadora. Lo más importante que debe hacer es filtrar todas las solicitudes que no le interesen. Por ejemplo, no tiene sentido registrar solicitudes de imágenes (se puede indicar a JMeter que descargue todas las imágenes en una página; consulte Solicitud HTTP ). Estos solo desordenarán su plan de prueba. Lo más probable es que haya una extensión que compartan todos sus archivos, como .jsp , .asp , .php , .html o similares. Estos debe " incluirlos " ingresando " .*\.jsp " como un "Patrón de inclusión".

Alternativamente, puede excluir imágenes ingresando " .*\.gif " como "Excluir patrón". Dependiendo de su aplicación, esta puede ser o no una mejor manera de hacerlo. También es posible que deba excluir hojas de estilo, archivos javascript y otros archivos incluidos. Pruebe su configuración para verificar que está grabando lo que desea, y luego borre y comience de nuevo.

La grabadora de secuencias de comandos de prueba HTTP(S) espera encontrar un elemento ThreadGroup con un controlador de grabación debajo del cual registrará las solicitudes HTTP. Esto empaqueta convenientemente todas sus muestras bajo un solo controlador, al que se le puede dar un nombre que describa el caso de prueba.

Ahora, siga los pasos de un caso de prueba. Si no tiene casos de prueba predefinidos, use JMeter para registrar sus acciones para definir sus casos de prueba. Una vez que haya terminado una serie definida de pasos, guarde todo el caso de prueba en un archivo con el nombre apropiado. Luego, limpie y comience un nuevo caso de prueba. Al hacer esto, puede registrar rápidamente una gran cantidad de "borradores preliminares" de casos de prueba.

Una de las características más útiles de HTTP(S) Test Script Recorder es que puede abstraer ciertos elementos comunes de las muestras grabadas. Al definir algunas variables definidas por el usuario en el nivel del Plan de prueba o en los elementos de Variables definidas por el usuario , puede hacer que JMeter reemplace automáticamente los valores en sus muestras registradas. Por ejemplo, si está probando una aplicación en el servidor " xxx.example.com ", entonces puede definir una variable llamada " servidor " con el valor de " xxx.example.com ", y en cualquier lugar que se encuentre ese valor en su registro. las muestras se reemplazarán con " ${servidor} ".

Tenga en cuenta que la coincidencia distingue entre mayúsculas y minúsculas.
Si JMeter no registra ninguna muestra, verifique que el navegador realmente esté usando el proxy. Si el navegador funciona bien incluso si JMeter no se está ejecutando, entonces el navegador no puede usar el proxy. Algunos navegadores ignoran la configuración de proxy para localhost o 127.0.0.1 ; intente usar el nombre de host local o la IP en su lugar.

El error " unknown_ca " probablemente significa que está intentando registrar HTTPS y el navegador no ha aceptado el certificado del servidor JMeter Proxy.

## Variables de usuario 6️⃣

Algunos planes de prueba necesitan usar diferentes valores para diferentes usuarios/subprocesos. Por ejemplo, es posible que desee probar una secuencia que requiera un inicio de sesión único para cada usuario. Esto es fácil de lograr con las instalaciones proporcionadas por JMeter.

Por ejemplo:

* Cree un archivo de texto que contenga los nombres de usuario y las contraseñas, separados por comas. Ponga esto en el mismo directorio que su plan de prueba.

* Agregue un elemento de configuración CSV DataSet al plan de prueba. Nombra las variables USUARIO y PASS .

* Reemplace el nombre de inicio de sesión con ```${USUARIO}``` y la contraseña con ```${PASS}``` en las muestras apropiadas. El elemento CSV Data Set leerá una nueva línea para cada subproceso.

## Reducción de los requisitos de recursos 7️⃣

Algunas sugerencias para reducir el uso de recursos.

* Utilice el modo CLI(command-line interface): 
```
jmeter -n -t test.jmx -l test.jtl
```

* Utilice la menor cantidad posible de oyentes; si usa el indicador -l como se indicó anteriormente, todos pueden eliminarse o deshabilitarse.

* No utilice los oyentes "Ver árbol de resultados" o "Ver resultados en la tabla" durante la prueba de carga, utilícelos solo durante la fase de sscripting para depurar sus script.

* En lugar de usar muchos muestreadores similares, use el mismo muestreador en un bucle y use variables (Conjunto de datos CSV) para variar la muestra. [Incluir controlador no ayuda aquí, ya que agrega todos los elementos de prueba en el archivo al plan de prueba].

* No utilice el modo funcional.

* Utilice la salida CSV en lugar de XML.

* Guarda solo los datos que necesites.

* Use la menor cantidad de aserciones posible.

* Use el lenguaje de script  de mayor rendimiento (consulte la sección JSR223).

* Si su prueba necesita grandes cantidades de datos, particularmente si necesita ser aleatoria, cree los datos de prueba en un archivo que se pueda leer con CSV Dataset. Esto evita desperdiciar recursos en tiempo de ejecución.scripting.

## Servidor BeanShell 8️⃣ Dudas???

El intérprete BeanShell tiene una función muy útil: puede actuar como un servidor al que se puede acceder mediante telnet o http.

```
No hay seguridad. Cualquiera que pueda conectarse al puerto puede emitir cualquier comando BeanShell. Estos pueden proporcionar acceso sin restricciones a la aplicación JMeter y al host. No habilite el servidor a menos que los puertos estén protegidos contra el acceso, por ejemplo, mediante un cortafuegos.
```

Si desea utilizar el servidor, defina lo siguiente en **jmeter.properties** :

```
beanshell.servidor.port=9000
beanshell.server.file=../extras/startup.bsh
```

En el ejemplo anterior, el servidor se iniciará y escuchará en los puertos 9000 y 9001 . El puerto 9000 se utilizará para el acceso http. El puerto 9001 se utilizará para el acceso telnet. El archivo startup.bsh será procesado por el servidor y puede usarse para definir varias funciones y configurar variables. El archivo de inicio define métodos para configurar e imprimir JMeter y las propiedades del sistema. Esto es lo que debería ver en la consola de JMeter:

```
Script de inicio ejecutándose
Script de inicio completado
Httpd comenzó en el puerto: 9000
Sesión iniciada en el puerto: 9001
```

Hay un script de muestra ( extras/remote.bsh ) que puede usar para probar el servidor. [Échele un vistazo para ver cómo funciona.]
Al iniciarlo en el directorio bin de JMeter (ajuste las rutas según sea necesario si se ejecuta desde otro lugar), la salida debería verse así:

```
$ java -jar ../lib/bshclient.jar localhost 9000 ../extras/remote.bsh
Conexión al servidor BSH en localhost:9000
Leyendo respuestas del servidor...
BeanShell 2.0b5 - por Pat Niemeyer (pat@pat.net)
bsh % remoto.bsh comenzando
usuario.home = C:\Documentos y Configuraciones\Usuario
usuario.dir = D:\eclipseworkspaces\main\JMeter_trunk\bin
Establecer la propiedad 'EJEMPLO' en '0'.
Establecer la propiedad 'EJEMPLO' en '1'.
Establecer la propiedad 'EJEMPLO' en '2'.
Establecer la propiedad 'EJEMPLO' en '3'.
Establecer la propiedad 'EJEMPLO' en '4'.
Establecer la propiedad 'EJEMPLO' en '5'.
Establecer la propiedad 'EJEMPLO' en '6'.
Establecer la propiedad 'EJEMPLO' en '7'.
Establecer la propiedad 'EJEMPLO' en '8'.
Establecer la propiedad 'EJEMPLO' en '9'.
EJEMPLO = 9
remoto.bsh finalizó
bsh %... desconectado del servidor.
```

Como ejemplo práctico, suponga que tiene una prueba JMeter de ejecución prolongada en modo CLI y desea variar el rendimiento en varios momentos durante la prueba. El plan de prueba incluye un temporizador de rendimiento constante que se define en términos de una propiedad, por ejemplo, ${__P(rendimiento)} . Los siguientes comandos BeanShell podrían usarse para cambiar la prueba:

```
printprop("rendimiento");
curr = Integer.decode(args[0]); // Valor inicial
inc = Integer.decode(args[1]); // Incremento
end = Integer.decode(argumentos[2]); // Valor final
segundos = Integer.decode(args[3]); // Esperar entre cambios
while(actual <= final) {
  setprop("rendimiento",curr.toString()); // Tiene que ser una cadena aquí
  Thread.sleep (segundos * 1000);
  corriente += inc;
}
printprop("rendimiento");
```

La secuencia de comandos se puede almacenar en un archivo ( throughput.bsh , por ejemplo) y enviarse al servidor mediante bshclient.jar . Por ejemplo:

```
java -jar ../lib/bshclient.jar host local 9000 rendimiento.bsh 70 5 100 60
```

## Scripts BeanShell 9️⃣

```
Desde JMeter 3.1, recomendamos cambiar de BeanShell a JSR223 Test Elements (consulte la sección JSR223 a continuación para obtener más detalles) y cambiar de la función __Beanshell a la función __groovy .
```

* Resumen

Cada elemento de prueba BeanShell tiene su propia copia del intérprete (para cada hilo). Si el elemento de prueba se llama repetidamente, por ejemplo, dentro de un bucle, entonces el intérprete se retiene entre invocaciones a menos que se seleccione la opción **"Reset bsh.Interpreter before each call"**.

Algunas pruebas de ejecución prolongada pueden hacer que el intérprete use mucha memoria; si este es el caso, intente usar la opción de reinicio.

Puede probar los scripts de BeanShell fuera de JMeter utilizando el intérprete de línea de comandos:

```
$ java -cp bsh-xxx.jar[;otros jars según sea necesario] bsh.Archivo de intérprete.bsh [parámetros]
```
o
```
$ java -cp bsh-xxx.jar bsh.Interpreter 
bsh% fuente("archivo.bsh"); 
bsh% salida(); // o use la tecla EOF (por ejemplo, ^Z o ^D)
```

* Compartir variables

Las variables se pueden definir en scripts de inicio (inicialización). Estos se conservarán entre las invocaciones del elemento de prueba, a menos que se utilice la opción de reinicio.

Los scripts también pueden acceder a las variables de JMeter usando los métodos get() y put() de la variable " vars ", por ejemplo:

```
vars.get("HOST"); 
vars.put("MSG","Exitoso");
```

Los métodos get() y put() solo admiten variables con valores de String, pero también hay métodos getObject() y putObject() que se pueden usar para objetos arbitrarios. Las variables de JMeter son locales para un subproceso, pero pueden ser utilizadas por todos los elementos de prueba (no solo por Beanshell).

Si necesita compartir variables entre subprocesos, se pueden usar las propiedades de JMeter:

```
import org.apache.jmeter.util.JMeterUtils;
String value = JMeterUtils.getPropDefault("name","");
JMeterUtils.setProperty("name", "value");
```

Los archivos .bshrc de muestra contienen definiciones de muestra de los métodos getprop() y setprop() .

Otro posible método de compartir variables es utilizar el espacio de nombres compartido " bsh.shared ". Por ejemplo:

```
if (bsh.shared.myObj == void){
    // not yet defined, so create it:
    myObj = new AnyObject();
}
bsh.shared.myObj.process();

```

En lugar de crear el objeto en el elemento de prueba, se puede crear en el archivo de inicio definido por la propiedad de JMeter " beanshell.init.file ". Esto solo se procesa una vez.

## Desarrollo de funciones de script en Groovy o Jexl3, etc.🔟

Es bastante difícil escribir y probar scripts como funciones. Sin embargo, JMeter tiene los muestreadores JSR223 que se pueden usar en su lugar con cualquier idioma que lo admita. Recomendamos utilizar Apache Groovy o cualquier lenguaje que admita la interfaz compilable de JSR223 .

Cree un plan de prueba simple que contenga el JSR223 Sampler y Tree View Listener. Codifique el script en el panel de scripts de muestra y pruébelo ejecutando la prueba. Si hay algún error, aparecerá en la vista de árbol y en el archivo jmeter.log . Además, el resultado de ejecutar el script se mostrará como respuesta.

Una vez que el script funciona correctamente, se puede almacenar como una variable en el plan de prueba. La variable de script se puede usar para crear la llamada de función. Por ejemplo, supongamos que un script Groovy está almacenado en la variable RANDOM_NAME . La llamada a la función se puede codificar como ```${__groovy(${RANDOM_NAME})}``` . No es necesario escapar de las comas en el script, porque la llamada a la función se analiza antes de que se interpole el valor de la variable.

## Pruebas de parametrización 1️⃣1️⃣

A menudo, es útil poder volver a ejecutar la misma prueba con diferentes configuraciones. Por ejemplo, cambiar la cantidad de subprocesos o bucles, o cambiar un nombre de host.

Una forma de hacer esto es definir un conjunto de variables en el plan de prueba y luego usar esas variables en los elementos de prueba. Por ejemplo, se podría definir la variable LOOPS=10 y referirse a ella en el Grupo de subprocesos como ${LOOPS} . Para ejecutar la prueba con 20 bucles, simplemente cambie el valor de la variable LOOPS en el Plan de prueba.

Esto rápidamente se vuelve tedioso si desea ejecutar muchas pruebas en modo CLI. Una solución a esto es definir la variable Plan de prueba en términos de una propiedad, por ejemplo ```LOOPS=${__P(loops,10)}``` . Esto usa el valor de la propiedad " loops ", por defecto es 10 si no se encuentra la propiedad. La propiedad " loops " se puede definir en la línea de comandos de JMeter:

```
jmetro … -Jbucles=12 …
```

Si hay muchas propiedades que deben cambiarse juntas, entonces una forma de lograrlo es usar un conjunto de archivos de propiedades. El archivo de propiedades apropiado se puede pasar a JMeter usando la opción de línea de comando -q .

## Elementos JSR223 1️⃣2️⃣

Para pruebas de carga intensivas, el lenguaje de secuencias de comandos recomendado es uno cuyo ScriptingEngine implementa la interfaz Compilable . El motor de secuencias de comandos Groovy implementa Compilable . Sin embargo, ni Beanshell ni Javascript lo hacen a partir de la fecha de lanzamiento de JMeter 3.1, por lo que se recomienda evitarlos para pruebas de carga intensivas.

```
Nota: Beanshell implementa la interfaz Compilable pero no ha sido codificada; el método simplemente lanza una excepción. JMeter tiene una ronda de trabajo explícita para este error.
```

Al usar elementos JSR 223, se recomienda verificar la propiedad **Cache compiled script if available** para asegurarse de que la compilación del script se almacene en caché si el lenguaje subyacente lo admite. En este caso, asegúrese de que el script no use ninguna variable usando ```${varName}``` ya que el almacenamiento en caché solo tomaría el primer valor de ```${varName}``` . En su lugar, use:

```
vars.get("varNombre")
```

También puede pasarlos como Parámetros al script y usarlos de esta manera.

## Compartir variables entre hilos y grupos de hilos 1️⃣3️⃣

Las variables son locales para un subproceso; una variable establecida en un subproceso no se puede leer en otro. Esto es por diseño. Para conocer las variables que se pueden determinar antes de que comience una prueba, consulte Pruebas de parametrización (arriba). Si el valor no se conoce hasta que comienza la prueba, hay varias opciones:

* Almacene la variable como una propiedad: las propiedades son globales para la instancia de JMeter.
* Escriba variables en un archivo y vuelva a leerlas.
* Use el espacio de nombres bsh.shared - vea arriba.
* Escriba sus propias clases de Java.

## Administrar propiedades 1️⃣4️⃣

Cuando necesite modificar las propiedades de jmeter, asegúrese de no modificar el archivo jmeter.properties ; en su lugar, copie la propiedad de jmeter.properties y modifique su valor en el archivo user.properties .
Si lo hace, facilitará la migración a la próxima versión de JMeter.
Tenga en cuenta que en la documentación jmeter.properties se menciona con frecuencia, pero esto debe entenderse como "Copie de jmeter.properties a user.properties la propiedad que desea modificar y hágalo en este último archivo".

El archivo user.properties reemplaza las propiedades definidas en jmeter.properties

## Elementos obsoletos 1️⃣5️⃣

Se recomienda no utilizar elementos en desuso (marcados como tales en la lista de cambios y en la referencia del componente ) y migrar a nuevos elementos recomendados si están disponibles o a una nueva forma de hacer lo mismo.
Los elementos en desuso se eliminan del menú en la versión N, pero se pueden habilitar para la migración modificando la propiedad not_in_menu en el archivo user.properties y eliminando el nombre de clase completo del elemento de allí.
