# DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded 👩‍💻

<p align="center">
    <img src="/assets/XSS/11-Eleventh/01-Description.PNG">
</p>

La vulnerabilidad se encuentra en la barra de búsqueda

<p align="center">
    <img src="/assets/XSS/11-Eleventh/02-Angular.PNG">
</p>

* Vemos que la página web usa `angular`, por el atributo `ng-app`, así que si no se controla el input del usuario apropiadamente se pueden producir ataques XSS.

---

Con esta expresión `{{$on.constructor('alert(1)')()}}` podemos ejecutar una alerta.

* Cuando usamos un `constructor` hacemos referencia a un objeto definido previamente, en este caso, no hicimos eso y ejecutamos directamente una alerta.


<p align="center">
    <img src="/assets/XSS/11-Eleventh/03-Result.PNG">
</p>

---


