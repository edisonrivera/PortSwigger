# Stored DOM XSS 👩‍💻

<p align="center">
    <img src="/assets/XSS/13-Thirteenth/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en la parte de **comentarios de los blogs**

<p align="center">
    <img src="/assets/XSS/13-Thirteenth/02-Script.PNG">
</p>

* Vemos que existe un **script**, una vez lo hayamos visto, existe una sola parte interesante.

<p align="center">
    <img src="/assets/XSS/13-Thirteenth/03-Script.PNG">
</p>

* La función `escapeHTML` lo que hará es reemplazar la conincidencia de `<` o `>` por `&lt;` y `&gt;`
  
* A pesar de que reemplace caracteres podemos inyectar código js.

```
La función `replace` únicamente reemplaza la PRIMERA COINCIDENCIA
```

---

Con lo anterior en mente, podemos hacer algo como esto
`<><img src=x onerror=alert(document.cookie)>`

* Los dos primeros `<>` servirán de 'señuelo' para que la función que los reemplaza únicamente afecte a los primeros y el resto del código se mantenga igual.

<p align="center">
    <img src="/assets/XSS/13-Thirteenth/04-Result.PNG">
</p>

---

Si vemos el resultado del comentario


<p align="center">
    <img src="/assets/XSS/13-Thirteenth/05-Script.PNG">
</p>

* Notamos que `<>` se representaron como texto y no cómo código.