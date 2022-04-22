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