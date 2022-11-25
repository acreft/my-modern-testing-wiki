# Introducción

En este capítulo, repasaremos los requisitos previos necesarios para instalar Jenkins y explicaremos cómo puede configurar un servidor de automatización de Jenkins.

# Jenkins y Java

Jenkins está escrito en Java, un lenguaje de programación independiente de la plataforma. Como cualquier otra aplicación Java, se puede instalar en una variedad de sistemas operativos como Linux, Windows, MacOS, etc.

# Lanzamientos de Jenkins

El proyecto Jenkins produce dos líneas de lanzamiento: LTS (soporte a largo plazo) y semanal.

| Stable (LTS) | Regular Releases (Weekly) | 
| -- | -- | 
|Lanzamiento cada 12 semanas. Seleccionado del flujo de lanzamientos regulares como el lanzamiento estable para ese período de tiempo. | Lanzado semanalmente para ofrecer correcciones de errores y funciones a los usuarios finales y desarrolladores de complementos. |

# Requisitos previos para instalar Jenkins

Antes de instalar Jenkins, debe asegurarse de que su sistema cumpla al menos con los requisitos mínimos de hardware y software:

- RAM de 256 MB

- 1 GB de espacio en disco (10 GB si se ejecuta como contenedor Docker)

- Java 8 o Java 11

- Navegadores web modernos: Google Chrome, Mozilla Firefox, Microsoft Internet Explorer, Apple Safari.

Estos requisitos mínimos son lo suficientemente buenos para comenzar, por ejemplo, con fines de desarrollo o prueba. Sin embargo, estos deben ajustarse para la producción, ya que los sistemas de producción necesitan muchos más recursos. [Jenkins Documentation](https://www.jenkins.io/doc/book/scaling/hardware-recommendations/) tiene recomendaciones sensatas sobre cómo establecer los requisitos de hardware para su sistema de producción.

# Canales de Instalación

Jenkins se distribuye a través de muchos canales:

- Standalone WAR
- Gestores de paquetes de Linux (RPM, DEB, etc.)
- Instaladores de Windows
- Contenedores

Instalar Jenkins es bastante sencillo. Una instalación típica tarda unos 10 minutos. La [documentación de instalación de Jenkins](https://www.jenkins.io/doc/book/installing/) tiene instrucciones completas para usar cada uno de estos canales para la instalación. En las siguientes páginas, exploraremos la instalación de Jenkins utilizando cada uno de los canales de distribución mencionados anteriormente.

## Standalone WAR

Con este método, Jenkins se ejecuta como una aplicación independiente en su propio proceso con su contenedor de servlet de Java integrado, Jetty. Esta aplicación independiente se puede descargar como un archivo Java WAR (Web Application Archive) con extensión **.war**. Este archivo WAR puede ejecutarse en cualquier sistema operativo, Linux, Windows, Mac OS, etc.

Estos son los pasos para lanzar Jenkins como una standalone war:

- Descargue el archivo **jenkins.war** de la descarga e implementación de Jenkins.
- Inicie una ventana de terminal y ejecute el siguiente comando:

`java -jar jenkins.war`

De manera predeterminada, Jenkins usa el puerto 8080. Su aplicación de Jenkins estará disponible en **http://<su dirección IP>:8080**. Puede pasar argumentos JVM adicionales especificando JENKINS_OPTS y JAVA_OPTS a la llamada de Java como se muestra a continuación:

`java ${JAVA_OPTS} -jar jenkins.war ${JENKINS_OPTS}`

Aquí hay un ejemplo del uso de banderas de inicio:

`java -Dhudson.footerURL=http://example.org -jar jenkins.war \ --httpPort=8083 --prefix=/ci --httpListenAddress=127.0.0.1`

En este ejemplo:

- establecer la propiedad del sistema Java **(JAVA_OPTS) -Dhudson.footerURL=http://example.org** cambiará el pie de página predeterminado en la interfaz de usuario de Jenkins a http://example.com
- -**-httpPort**, **--prefix** y **--httpListenAddress** son las banderas proporcionadas como **JENKINS_OPTS**.
- **--httpPort=8083** establecerá el puerto de Jenkins en 8083 en lugar del 8080 predeterminado.
- **--prefix=/ci** agregará un prefijo al final de la URL de Jenkins.
- **--httpListenAddress=127.0.0.1** vincula a Jenkins con la dirección IP.

Finalmente, solo se podrá acceder a un servicio de Jenkins lanzado por el comando anterior en http://127.0.0.1:8083/ci.

Para obtener una lista de todas las opciones de JAVA y JENKINS disponibles, consulte ["Características de Jenkins controladas con las propiedades del sistema"](https://www.jenkins.io/doc/book/managing/system-properties/) .