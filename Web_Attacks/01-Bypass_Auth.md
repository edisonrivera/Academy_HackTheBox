# Laboratorio: Bypass Basic Authentication 🚗

1. Visitamos la web 

<p align="center">
    <img src="./assets/01-ByPass_Basic/01-Web.PNG" width=520>
</p>

---
2. Interceptamos la petición con **`Burp Suite`** y probamos a cambiar por los demás métodos HTTP `POST` `PUT` `DELETE` `PATCH` `HEAD`

<p align="center">
    <img src="./assets/01-ByPass_Basic/02-Patch.PNG"s>
</p>

* A la final el método usado para **`bypassear`** la autenticación fue **`PATCH`**
---
3. En la web veremos la **flag** 🏴

<p align="center">
    <img src="./assets/01-ByPass_Basic/03-Flag.PNG"s>
</p>