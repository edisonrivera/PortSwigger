# Reflected DOM XSS 👩‍💻

<p align="center">
    <img src="/assets/XSS/12-Twelfth/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en la barra de búsqueda

<p align="center">
    <img src="/assets/XSS/12-Twelfth/02-Script.PNG">
</p>

* Vemos que se ejecuta un **script** cada vez que realizamos un búsqueda. 🔍

---

La parte que nos importa del **script** es esta:

<p align="center">
    <img src="/assets/XSS/12-Twelfth/03-Script.PNG">
</p>

* Usar `eval` resulta muy riesgoso ya que podemos ejecutar comandos. ⚠

---

<p align="center">
    <img src="/assets/XSS/12-Twelfth/04-Script.PNG">
</p>

* Se indica el como se realiza una consulta. 🔘

---

En base a lo anterior buscaremos una forma de ejecutar una alerta. ⏰

```js
\"-alert(1)}//
```

<p align="center">
    <img src="/assets/XSS/12-Twelfth/05-Script.PNG">
</p>

* `\"` Escapamos las dobles comillas `"` para que se concatenar nada. Con esto evitamos que nos den errores. ❌
* `-alert(1)` Es signo de menos `-` se usa en este caso para separar expresiones.
* `}//` La llave `}` se usa para cerrar el condicional `if` y las dobles barras invertidas `//` se usan para comentar todo el código que esté por delante.

---

<p align="center">
    <img src="/assets/XSS/12-Twelfth/06-Result.PNG">
</p>