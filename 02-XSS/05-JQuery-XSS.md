# DOM XSS in jQuery anchor href attribute sink using location.search source 👨‍💻

<p align="center">
    <img src="/assets/XSS/05-Fifth/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en **la barra de búsqueda**

<p align="center">
    <img src="/assets/XSS/05-Fifth/02-Script.PNG">
</p>

**Script XSS**
```h
javascript:alert("Pwned!")
```

Colocando el anterior código lo que hacemos es modificar el **comportamiento** de la url, con lo cual, podemos ejecutar código `js`. 🌐

<p align="center">
    <img src="/assets/XSS/05-Fifth/03-Result.PNG">
</p>

* Para mostrar la **alerta** tenemos que presionar 'back'

En este caso el ejercicios nos pide mostrar la cookie. Esto lo podemos hacer con `javascript:alert(document.cookie)`