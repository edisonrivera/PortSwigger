# Stored XSS into HTML context with nothing encoded 👨‍💻

<img align="center" src="/assets/XSS/02-Second
/01-Description.PNG">

La vulnerabilidad se encuentra en **la sección de comentarios de los posts** 

<img align="center" src="/assets/XSS/02-Second/02-Script.PNG">

**Script XSS**
```js
<script>alert("Pwned!");</script>
```

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:

<img align="center" src="/assets/XSS/02-Second/03-Result.PNG">