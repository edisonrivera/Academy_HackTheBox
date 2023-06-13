# Laboratorio: Enumeration Services 🔢

1. Agregamos todos los dominios y la dirección IP al archivo **`/etc/hosts`**

---

2. Ahora, agregamos todos los dominios a un archivo

* **scope-list.txt**
```
blog.inlanefreight.local
drupal.inlanefreight.local
drupal-acc.inlanefreight.local
drupal-qa.inlanefreight.local
drupal-dev.inlanefreight.local
dev.inlanefreight.local
app.inlanefreight.local
```

---

3. Ahora, realizamos un análisis con **nmap** exportando la evidencia en formato `XML`
* `nmap -p- --open -oX nmap_evidence -iL scope-list.txt`

---

4. Ahora usamos `eyewitness` para recopilar más información sobre todos los dominios
* `eyewitness --web -x nmap_evidence.xml -d [Directorio Output]`

* `Respuesta`: El nombre del archivo de **base de datos** es `ew.db`

---

5. Usamos `aquatone` para generar un informe sobre todos los dominios en el **scope**
* `cat /home/kali/Desktop/Academy/nmap_evidence.xml | ./aquatone -nmap`

+ Como **output** tenemos un archivo `.html` el cual podemos ver desde el navegador, pero, primero levantamos un servicor http con `python` 🐍 (**`python3 -m http.server 80`**)

* `Respuesta`: **Pages by Similarity**