# DOM XSS in jQuery selector sink using a hashchange event

<p align="center">
    <img src="/assets/XSS/06-Sixth/01-Description.PNG">
</p>

Si buscamos en el **código fuente de la página** podemos ver el siguiente trozo de código:

<p align="center">
    <img src="/assets/XSS/06-Sixth/02-Code.PNG">
</p>


```
Una vulnerabilidad al utilizar el tipo de selecto $() en JQuery, es usarlo con location.hash
- location.hash: Sirve para animaciones y hacer auto-scroll a un elemento en específico de la página web.
```

Una forma de inyectar código js para derivarlo en un **Ataque XSS** es:

```html
<iframe src="https://vulnerable-website.com#" onload="this.src+='<img src=x onerror=<Código a Ejecutar>'"></iframe>
```

* Debemos aputar a la página web que sea vulnerable y lo hacemos un el **valor de hash** vacío.
* Al inyectar una **etiqueta <iframe\>**, se cargará como  nuevo valor de hash y se ejecturá.

Nos iremos al **Servidor de Explotación**

<p align="center">
    <img src="/assets/XSS/06-Sixth/03-Server.PNG">
</p>

---

Ahora en **Body** inyectaremos el código visto anteriormente

<p align="center">
    <img src="/assets/XSS/06-Sixth/04-Script.PNG">
</p>

* Ejecutaremos `print()` ya que eso se nos pide en el enunciado. `print()` sirve para imprimir una página web.

---

Seguiremos los siguientes pasos:

<p align="center">
    <img src="/assets/XSS/06-Sixth/05-Steps.PNG">
</p>

Al dar click en **View exploit** tendremo el siguiente resultado

<p align="center">
    <img src="/assets/XSS/06-Sixth/06-Print.PNG">
</p>

* Con esto verificamos que el **código que inyectamos** realmente se interprete.