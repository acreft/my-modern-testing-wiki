# Qué es un servidor proxy?

Un proxy es un equipo informático que hace de intermediario entre las conexiones de un cliente y un servidor de destino, filtrando todos los paquetes entre ambos. Siendo tú el cliente, esto quiere decir que el proxy recibe tus peticiones de acceder a una u otra página, y se encarga de transmitírselas al servidor de la web para que esta no sepa que lo estás haciendo tú.

![](imagenes/proxy.png)

De esta manera, cuando vayas a visitar una página web, en vez de establecer una conexión directa entre tu navegador y ella puedes dar un rodeo y enviar y recibir los datos a través de esta proxy. La página que visites no sabrá tu IP sino la del proxy, y podrás hacerte pasar por un internauta de otro país distinto al tuyo.

Los proxys son utilizados muy a menudo para acceder a servicios que tienen bloqueado su contenido en determinado país. Por ejemplo, si una web no ofrece determinado contenido en tu país pero sí en otro, haciéndote pasar por un internauta de ese otro país puedes acceder a él.

Por último, ten en cuenta que lo único que hace un servidor proxy es esconder tu IP. Esto quiere decir que no suelen eliminar ningún otro tipo de identificador adicional que pueda revelar tu identidad, por lo que aunque tu IP esté oculta, alguien con acceso a tu red y los datos que transmites podría espiar tu tráfico.

# Proxyweb: ¿qué es y cómo protege a mi empresa?

Un servidor proxy,  o proxyweb, es un dispositivo o un software que actúa como intermediario entre un ordenador o una red empresarial y la red externa. Un proxyweb puede residir en el mismo ordenador o un servidor separado. Un servidor proxy puede servir para muchos propósitos, dependiendo del tipo de usuario.

En un entorno empresarial, es donde un servidor proxy cobra mucha más importancia, contribuyendo a tareas críticas como el control del tráfico de la red de empresa, el aumento del rendimiento, el ahorro de ancho de banda y a la seguridad de la empresa.

## ¿Cómo funciona un proxyweb?
En general, el funcionamiento de un servidor proxy es bastante sencillo: cuándo un usuario hace una petición de un recurso en Internet (como una página web), el proxy busca en su caché local de páginas visitadas anteriormente.

Si el recurso se encuentra en caché, este se envía al usuario sin la necesidad de buscarlo en Internet. En caso contrario, el servidor proxy realiza la petición del recurso en nombre del usuario, pero con su propia IP, escondiendo la de origen.