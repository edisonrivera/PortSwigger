# DOM XSS in innerHTML sink using source location.search 👨‍💻

<p align="center">
    <img src="/assets/XSS/04-Fourth/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la barra de búsqueda**

<p align="center">
    <img src="/assets/XSS/04-Fourth/02-Script.PNG">
</p>

* Si intentamos inyectar el script directamente `<script>alert("Pwned!")</script>` no nos dejerá.
* Usando las técnicas vistas en el anterior laboratorio, modificaremos el código HTML cargando un `svg` o `img`. 🌆

**Script XSS**
```html
<img src=1 onerror=alert("Pwned!")>
```

Colocando el anterior código lo que hacemos es modificar el **HTML** de la página web. 🌐

<p align="center">
    <img src="/assets/XSS/04-Fourth/03-Explain.PNG">
</p>

* `src` Ruta de la imagen.
* `onerror` En caso de que no se pueda cargar la imagen se ejecutará lo que se indique. 

```
Podemos indicar cualquier cosa en 'src' para forzar un error y ejecutar el código js.
```

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:

<p align="center">
    <img src="/assets/XSS/04-Fourth/04-Result.PNG">
</p>