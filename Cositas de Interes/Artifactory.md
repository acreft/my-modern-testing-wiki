# Artifactory

JFrog Artifactory, o sencillamente **Artifactory**, es un repositorio de artefactos universal que nos permite administrar cualquier pieza de software, binarios o dependencias, en cualquier lenguaje.

En el mundo del desarrollo hay reglas que aplican a todo tipo de compañías, ya sean una pequeña startup recién creada o un gigante en el desarrollo de software. Se necesita entregar el valor generado por la compañía cuanto antes a los clientes, usuarios o empresas contratantes. Nuestro valor es el software y es necesario contar con procesos que nos permitan entregar releases rápidamente, con nuevas funcionalidades, actualizaciones, o corrección de problemas de seguridad.

En ocasiones, esto no es una tarea fácil, sobre todo cuando el código es complejo y la arquitectura de las aplicaciones requiere el uso de diversos tipos de lenguajes, mantenidos en servicios independientes y desarrollados por distintos equipos de trabajo, donde todos deben colaborar en sintonía.

Para responder a esta necesidad, contamos con JFrog Artifactory, el primer repositorio de artefactos universal. Artifactory no es un repositorio de software como los ya conocidos npm, Composer, Maven, Bower…, dedicados a un lenguaje en particular, sino que es capaz de trabajar con todo tipo de piezas de software, en cualquier lenguaje. Además también permite trabajar de manera centralizada y maximizar el provecho de los ambientes de desarrollo o despliegue más utilizados en la actualidad por las empresas modernas, como Vagran, Docker, puppet, etc.

La principal ventaja de Artifactory es evitar que los equipos de trabajo usen diversos repositorios, con distintas versiones o distintas fuentes, centralizando en un único sitio y en un único espacio de almacenamiento todas las dependencias de un proyecto y su gestión durante los ciclos de desarrollo, incluso en ambientes de desarrollo distribuidos.

Al ser universal, se puede integrar con cualquier herramienta de desarrollo, como IDEs, utilidades para devops, herramientas de control de versiones, sistemas operativos, etc. En definitva, es capaz de trabajar con cualquier lenguaje y tecnología que necesite cualquier proyecto IT.

Artifactory es utilizado por compañías grandes, como Google, Twitter, Netflix, etc. Pero cualquier empresa o desarrollador puede sacarle partido:  facilita la entrega del software, haciéndola más rápida y evitando problemas en el despliegue, testing o desarrollo.

# Gestión de paquetes

La plataforma JFrog trae la naturaleza universal de Artifactory a toda su fuerza con la gestión avanzada de paquetes para todos los principales formatos de empaque que se usan en la actualidad. Como el único repositorio con una arquitectura única que incluye una capa de almacenamiento de archivos y una capa de base de datos separada,  Artifactory es el único administrador de repositorios que puede admitir de forma nativa los formatos de paquetes actuales, así como cualquier formato nuevo que pueda surgir de vez en cuando.

Con un paradigma de repositorios de tipo único, a todos los repositorios se les asigna un tipo en el momento de la creación, lo que permite una indexación eficiente para que cualquier cliente o administrador de dependencias pueda trabajar directamente con Artifactory de forma transparente como su repositorio natural.

## Inspección de paquetes

La página Paquetes brinda fácil acceso a la información sobre todos los paquetes en sus repositorios. 

Tiene acceso rápido a la información de resumen más importante sobre las últimas versiones del paquete y puede profundizar fácilmente para obtener más detalles sobre las versiones anteriores. Los filtros y las funciones de clasificación están disponibles para su comodidad, así como los enlaces de referencia cruzada a las páginas de Construcciones y Artefactos. 

Para algunos tipos de paquetes, puede descargar paquetes y copiar comandos de instalación al profundizar en un paquete. 

To view information about packages, from the Application module, go to Artifactory | Packages.

## Maven Repository

Como repositorio de Maven, Artifactory es tanto una fuente de artefactos necesarios para una compilación como un destino para implementar artefactos generados en el proceso de compilación. Maven se configura mediante un archivo settings.xml ubicado en el directorio de inicio de Maven (por lo general, será /user.home/.m2/settings.xml). Para obtener más información sobre la configuración de Maven, consulte la ![ Referencia de configuración del proyecto Apache Maven](https://maven.apache.org/settings.html).

Los valores predeterminados en este archivo configuran a Maven para que funcione con un conjunto predeterminado de repositorios utilizados para resolver artefactos y un conjunto predeterminado de complementos.

### Visualización de artefactos de Maven

Al seleccionar un archivo de metadatos de Maven ( maven-metadata.xml) o un archivo POM ( pom.xml) desde el modo de exploración de árbol en el Navegador de repositorios de artefactos, se le brindan detalles sobre el elemento seleccionado.

https://www.jfrog.com/confluence/display/JFROG/Maven+Repository#MavenRepository-ResolvingArtifactsThroughArtifactory

Vista de metadatos Maven
