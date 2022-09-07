# Selenium Standalone server

El Selenium Standalone server actúa como un proxy entre su script y los driver específicos del navegador. El servidor se puede usar cuando se ejecuta localmente, pero no se recomienda ya que introduce un salto adicional para cada solicitud y ralentizará las cosas. Sin embargo, se requiere que el servidor use un navegador en un host remoto (la mayoría de los controladores de navegador, como IEDriverServer, no aceptan conexiones remotas).

Para usar el servidor Selenium, deberá instalar el JDK y descargar el servidor más reciente de Selenium . Una vez descargado, ejecuta el servidor con:

```
java -jar selenium-server-standalone-2.45.0.jar
```