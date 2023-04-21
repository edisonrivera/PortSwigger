# Reflected XSS into HTML context with nothing encoded 👨‍💻
<p align="center">
    <img src="/assets/XSS/01-First/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la barra de búsqueda** 

<p align="center">
    <img src="/assets/XSS/01-First/02-Script.PNG">
<p>

**Script XSS**
```js
<script>alert("Pwned!");</script>
```

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:

<p align="center">
<img src="/assets/XSS/01-First/03-Result.PNG">
</p>