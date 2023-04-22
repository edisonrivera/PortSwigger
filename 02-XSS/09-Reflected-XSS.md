# Reflected XSS into attribute with angle brackets HTML-encoded 👩‍💻

<p align="center">
    <img src="/assets/XSS/09-Ninth/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en la **barra de búsqueda** 🔍

<p align="center">
    <img src="/assets/XSS/09-Ninth/02-Script.PNG">
</p>

* Lo que busquemos se guarda en la **variable searchTerms**
* Ahora lo que haremos es malformar el código ya definido para desplegar una **alerta**

---

Después de algunas pruebas tendremos que inyectar el siguiente código
```js
' alert("Pwned!"); var x = '
```

<p align="center">
    <img src="/assets/XSS/09-Ninth/03-Script.PNG">
</p>

* **(1)** La primera comilla simple (`'`) y (`;`), nos sirve para igualar a nada la variable `searchTerms` y cerrarla.
  *  Es importante poner `;` ya que con esto indicamos que queremos iniciar otra sección de código.

* **(2)** Colocamos el código para que se ejecute una alerta.
* **(3)** Como nos queda una comilla simple (`'`) por cerrar, lo que haremos es definir una variable con cualquier nombre, para después, igualarla a nada.

---

Si presionamos en **Buscar** la alerta se ejecutará

<p align="center">
    <img src="/assets/XSS/09-Ninth/04-Result.PNG">
</p>