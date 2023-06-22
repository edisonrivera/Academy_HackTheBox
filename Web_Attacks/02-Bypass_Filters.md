# Laboratorio: Bypass Basic Filters 🚗

1. Visitamos la web 

<p align="center">
    <img src="./assets/01-ByPass_Basic/01-Web.PNG" width=400>
</p>

---

2. Si creamos un archivo normalmente notaremos que no existe ningún problema, pero si colocamos un `;` nos lo tomará como un `intento malicioso`

<p align="center">
    <img src="./assets/02-ByPass_Filters/01-Error.PNG" width=350>
</p>

---

3. Interceptamos la solicitud con **`Burp Suite`** y cambiaremos el método HTTP
* En la petición colocamos la pista de **HackTheBox**  ` file; cp /flag.txt ./`
* **URL:** `http://[IP]/index.php?filename=file; cp /flag.txt ./`

<p align="center">
    <img src="./assets/02-ByPass_Filters/02-Change.PNG">
</p>

* Damos clic en **`Change request method`**

---
4. Una vez que se cambie la petición la enviamos, recargamos la página y podremos leer la **flag** 🏴

<p align="center">
    <img src="./assets/02-ByPass_Filters/03-Flag.PNG">
</p>

* **Flag:** `HTB{b3_v3rb_c0n51573n7}`