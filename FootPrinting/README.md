# Cheatsheet ⚙

## FTP 📂 **(Puerto 21)**

| Comando | Descripción |
| --- | --- |
| `ftp <Dominio/IP>` | Interactuamos directamente con el servicio. |
| `nc -nv <Dominio/IP> 21` | Obtener un banner e interactuar con el servicio. |
| `telnet <Dominio/IP> 21` | Usamos telnet para interactuar con el servicio. |
| `openssl s_client -connect <Dominio/IP>:21 -starttls ftp` | Interactuamos con ftp usando una conexión encriptada. |
| `wget -m --no-passive ftp://<user>:<password>@<IP>` | Descargamos todos lo que esté disponible en el servicio. |

## NFS 💿 (Puerto 111, 2049)

| Comando | Descripción |
| --- | --- |
| `showmount -e <Dominio/IP>` | Mostramos los recursos disponibles. |
| `mount -t nfs <IP>:/<Recurso> <Path Montaje> -o noloc`k | Montamos el recurso compartido. |
| `umount ./target-NFS` | Desmontamos el recurso compartido. |

## SMB 🗃 (Puerto 445)

| Comando | Descripción |
| --- | --- |
| `smbclient -L -N //<IP/Dominio>` | Listamos recursos compartidos usando una Sesión NULA |
| `smbclient ////<IP/Dominio>//<Recurso>` | Nos conectamos a un recurso en específico. |
| `crackmapexec smb —shares <IP/Dominio> -u ‘User’ -p ‘Password’` | Listamos los recursos compartidos autenticándonos con credenciales. |
| `rpcclient -U ‘User’ <IP/Dominio>` | Usamos rpc para interactuar con el servicio. |

Comandos de **RPC**:
- `srvinfo`
- `enumdomains`
- `querydominfo`
- `netshareenumall`
- `netsharegetinfo <Recurso>`
- `enumdomusers`
- `queryuser <RID>`


## SNMP 📱 (Puerto 161)

| Comando | Descripción |
| --- | --- |
| `snmpwalk -v2c -c <Community String> <IP/Dominio>` | Ver OID’s y posibles scripts. |
| `onesixtyone -c <Diccionario> <IP/Dominio>`  | Descubrimos Community Strings. |
| `braa <Community String>@<IP/Dominio>:.1.*` | Descubrimos OID’s. |

## DNS 🌐 (Puerto 53)

| Comando | Descripción |
| --- | --- |
| `dig ns <dominio> @<IP>` | Petición NS al servidor. |
| `dig any <dominio> @IP> `| Mostramos todo sobre el servidor. |
| `dig axfr <dominio> @<IP>` | Ataque de transferencia de zona. |
| `dnsenum --dnsserver <IP> --enum -p 0 -s 0 -o evidencia.txt -f <Diccionario> <dominio>` | Descubrimiento de subdominios. |
| `wfuzz -c -t <N Hilos> --hh=404 -w <Diccionario> -H "Host: FUZZ.dominio" <dominio>` | Usamos wfuzz para el descubrimiento de subdominios. |

## SMTP 📧 (Puerto 25)

| Comandos | Descripción |
| --- | --- |
| `telnet <IP/Dominio> 25` | Interactuamos con el servicio |

## IMAP/POP3 📨 (Puerto 111, 143, 993, 995)

| Comando | Descripción |
| --- | --- |
| `curl -k 'imaps://<dominio/IP>' --user <Usuario>:<Contraseña>` | Usamos curl para interactuar con el servicio. |
| `openssl s_client -connect <Dominio/IP>:[imaps o pop3s]` | Podemos conectarnos a imaps o pop3s. |

Comandos para **IMAPS**:
- `A LOGIN "Usuario" "Contraseña"`
- `A LIST "" *`
- `A SELECT "Carpeta"`
- `A FETCH <ID> BODY[ |HEADER]`

## MySQL 🗄 (Puerto 3306)

| Comando | Descripción |
| --- | --- |
| `mysql -u 'Usuario' -p 'Contraseña' -h <IP>` | Interactuamos con MySQL. |

## MSSQL 🐍 (Puerto 1443)

| Comando | Descripción |
| --- | --- |
| `mssqlclient.py <usuario>@<Dominio/IP> -windows-auth` | Interactuamos con MSSQL. |

## IPMI 👷‍♀️ (Puerto 23)

| Comando | Descripción |
| --- | --- |
| `msf auxiliary(scanner/ipmi/ipmi_version)` | Conocer versión del servicio. |
| `msf auxiliary(scanner/ipmi/ipmi_dumphashes)` | Descubrimos hashes. |

## Manejo Remoto de Linux 🐧 (SSH: 22)

| Comando | Descripción |
| --- | --- |
| `ssh-audit.py <Dominio/IP> `| Auditoria del servicio. |
| `ssh <usuario>@<Dominio/IP>` | Nos autenticamos en el servidor. |
| `ssh -i id_rsa <usuario>@<Dominio/IP>` | Usamos una clave id_rsa para autenticarnos. |
| `ssh <usuario>@<Dominio/IP> -o PreferredAuthentications=password` | Usamos autenticación mediante contraseña. |
| `sshpass -p'Contraseña' ssh <usuario>@<IP>` | Ponemos la contraseña con anterioridad. |

## Manejo Remoto de Windows 🍃

| Comando | Descripción |
| --- | --- |
| `rdp-sec-check.pl <Dominio/IP>` | Auditamos la seguridad del servicio RDP. |
| `xfreerdp /u:<Usuario> /p:"<Constraseña>" /v:<Dominio/IP>` | Nos autenticamos en el servicio RDP. |
| `evil-winrm -i <Dominio/IP> -u <Usuario> -p <Contraseña>` | Nos autenticamos en el servicio WinRm |
| `wmiexec.py <usuario>:"<constraseña>"@<FQDN/IP> "<comando>"` | Ejecutamos comandos usando el servicio WMI. |
| `crackmapexec winrm <IP> -u "Usuario" -p"Contraseña>` | Verificamos la autenticidad de credenciales. |