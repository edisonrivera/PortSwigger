# Stored XSS into anchor href attribute with double quotes HTML-encoded 👩‍💻

<p align="center">
    <img src="/assets/XSS/08-Eight/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la sección de comentarios de los posts** 

<p align="center">
    <img src="/assets/XSS/08-Eight/02-Comments.PNG">
</p>

* En la descripción del laboratorio nos dicen que la inyección XSS se encuentra en la parte de `href` lo cual se refiere a un enlace. En la sección de comentarios esto se refiere a `Website`

Ahora lo que tenemos que hacer es inyectar el código para lograr el ataque XSS

<p align="center">
    <img src="/assets/XSS/08-Eight/03-Script.PNG">
</p>

* La etiqueta `input` es de **tipo text** por lo cual no existe alguna restricción al momento de enviar nuestro comentario.

---

<p align="center">
    <img src="/assets/XSS/08-Eight/04-Result.PNG">
</p>

* Si colocanos el cursor sobre usuario de post que previamente creamos, vemos que nos lleva a `javascript:alert("Pwned!")`