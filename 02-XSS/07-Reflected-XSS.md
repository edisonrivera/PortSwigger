# Reflected XSS into attribute with angle brackets HTML-encoded 👩‍💻

<p align="center">
    <img src="/assets/XSS/07-Seventh/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la barra de búsqueda**, si buscamos algo para realizar un prueba de lo que sucede por detrás, veremos que en el código fuente de la página se tramita lo siguiente

<p align="center">
    <img src="/assets/XSS/07-Seventh/02-Script.PNG">
</p>

* Vemos que lo que buscamos se iguala en el **atributo value** de la `etiqueta input`

Si seguimos probando con cadenas, llegamos a la siguiente búsqueda

<p align="center">
    <img src="/assets/XSS/07-Seventh/03-Test.PNG">
</p>

Explicación

<p align="center">
    <img src="/assets/XSS/07-Seventh/04-Script.PNG">
</p>

---

Ahora solo nos queda buscar un `atributo` de la `etiqueta input` el cual nos permita ejecutar un script.
* Uno de los **atributos** es `oninput`, con el cual podremos ejecutar un script cada vez que el usuario escriba en la **barra de búsqueda**

<p align="center">
    <img src="/assets/XSS/07-Seventh/05-Script.PNG">
</p>

* En el código fuente de la página vemos `event`, esto nos indica que secuderá algo cada vez que se interactue con la `etiqueta input`, por lo que sabemos que nuestro XSS fue inyectado con éxito 🌟

Cada vez que escribamos algo veremos una alerta

<p align="center">
    <img src="/assets/XSS/07-Seventh/06-Alert.PNG">
</p>