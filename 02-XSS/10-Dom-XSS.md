# DOM XSS in document.write sink using source location.search inside a select element 👩‍💻

<p align="center">
    <img src="/assets/XSS/10-Tenth/01-Description.PNG">
</p>

Si inspeccionamos en el código de la página veremos el siguiente **script**

<p align="center">
    <img src="/assets/XSS/10-Tenth/02-Code.PNG">
</p>

* **Función**: Busca parámetros en la URL.
* **Parámetro**: Detecta si este parámetro se encuentra en la URL.

Vemos que en caso de que ese parámetro exista se ejecutará el siguiente código

<p align="center">
    <img src="/assets/XSS/10-Tenth/03-Code.PNG">
</p>

* Se añadirá una etiqueta `<option>` con el contenido del parámetro `storeId`

---

Ahora añadiremos el parámetro `storeId` a la URL indicando igualandolo a algo

* URL: `<LAB-DOMINIO>/product?productId=1&storeId=Pwned`
  
<p align="center">
    <img src="/assets/XSS/10-Tenth/04-HTML.PNG">
</p>

* Se añadió una nueva etiqueta con el valor que igualamos. 👀

---

Con lo anterior en mente, inyectaremos algo de código para ejecutar una alerta

* Código: `</option></select><img src=x onerror=alert("Pwned!")>`

<p align="center">
    <img src="/assets/XSS/10-Tenth/05-Labels.PNG">
</p>

* **(1)** Forzamos el cierre de la etiqueta `<select>`. Esta etiqueta se usa para realizar un combobox. 📦
* Vemos que creamos la etiqueta `<img>` que generará una alerta. ⏰

---

<p align="center">
    <img src="/assets/XSS/10-Tenth/06-Result.PNG">
</p>