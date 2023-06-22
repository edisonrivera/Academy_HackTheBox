# Laboratorio: Linux Methods 🏆

1. Leemos la **flag** que está en el directorio raíz **`/`** del servicio web.
* **URL:** `wget -qO- http://<IP>/flag.txt`

* **Output:** `5d21cf3da9c0ccb94f709e2559f3ea50`
---

2. Descomprimimos el `.zip`, y leemos el contenido del archivo resultante para encodearlo en **base64**
   * `base64 -w 0 upload_nix.txt`
    * **Otra Forma de Subir el archivo es:** `scp upload_nix.txt htb-student@<IP>:/home/htb-student`

* Nos autenticamos en el servicio **SSH** y decodeamos el contenido para depositarlo en `upload_nix.txt`
  * `echo -n "MDQ4MDkwYmM3ZWQwNGY3NTg2NTg5NzVkZjhmODYyYzg=" | base64 -d > upload_nix.txt`

* Ahora ejecutamos el comando que nos indican en **`HackTheBox`**
    * `hasher upload_nix.txt`

* **Output:** `159cfe5c65054bbadb2761cfa359c8b0`
---

