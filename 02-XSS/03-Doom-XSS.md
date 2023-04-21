# DOM XSS in document.write sink using source location.search 👨‍💻

<p align="center">
    <img src="/assets/XSS/03-Third/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la barra de búsqueda**

<p align="center">
    <img src="/assets/XSS/03-Third/02-Script.PNG">
</p>

**Script XSS**
```html
"><svg src=1 onload=alert('Pwned!')>
```

Colocando el anterior código lo que hacemos es modificar el **HTML** de la página web. 🌐

<p align="center">
    <img src="/assets/XSS/03-Third/03-Explain.PNG">
</p>

* El **atributo onload** sirve para controlar un evento de la etiqueta **svg** y se ejecuta cuando se carga en un navegador web. 🔃

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:

<p align="center">
    <img src="/assets/XSS/03-Third/04-Result.PNG">
</p>

---

## Segunda Forma 🥈
**Script XSS**
```html
"><img src=1 onerror=alert("Pwned!")>
```

* `src` Ruta de la imagen.
* `onerror` En caso de que no se pueda cargar la imagen se ejecutará lo que se indique. 

<p align="center">
    <img src="/assets/XSS/03-Third/05-Other.PNG">
</p>