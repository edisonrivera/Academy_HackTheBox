# Cheatsheet ⚙


## nslookup 🔍

| Herramienta | Modo de Uso |
| --- | --- |
| `nslookup “Objetivo”` | Información sobre el servidor DNS del dominio. |
| `nslookup -query=[NS/A/MX/ANY/PTR] -type=[NS/A/MX/ANY/PTR] "Objetivo"` | Realizar una petición de registros a un dominio. |

## Información Pasiva 🧆

| Página | Link |
| --- | --- |
| VirusTotal | https://www.virustotal.com/gui/home/url |
| Censys | https://censys.io/ |
| Crt | https://crt.sh/ |

******************motores.txt******************

```sql
baidu
bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye
```

| Herramienta | Modo de Uso |
| --- | --- |
| theHarvester | `theHarvester -d “Objetivo” -b “Recurso” -f “Recurso_Objetivo”` |
| TheHarvester (Todos Los Motores) | `cat motores.txt \| while read motor; do theHarvester -d "${Objetivo}" -b $motor -f "${motor}-${Objetivo}";done` |
| whois | `whois <Dominio/IP>` |


## Identificación Pasiva de Infraestructura 🏦

| Herramienta | Modo de Uso |
| --- | --- |
| NetCraft | https://sitereport.netcraft.com/ |
| Wayback Machine | http://web.archive.org/ |
| wafw00f | `wafw00f -v <Dominio>` |


## Identificación Activa de Subdominios 🌐💪

| Transferencia de Zona | https://hackertarget.com/zone-transfer/ |
| --- | --- |
| Script Bash | `while read linea; do dig <Tipo Registro> "$linea" @10.129.81.216; done < domains.txt;` |
| wfuzz (V Hosts) | `wfuzz -c -t <N Hilos> --hc=<Estado> --hh=<Caracteres> -w <Diccionario> -H "Host: FUZZ.dominio" dominio` |
| dig (Trasferencia de Zona) | `dig axfr dominio @IP` |
| Extraer subdominios de dig | `dig axfr <Dominio> @<IP> \| awk '{print $1}' \| grep <Keyword Domain> \| sort -u \| uniq > <Nombre Archivo>.txt` |
| curl | `curl -I "Dominio"` |

## Virtual Host 🤖

| Script Bash | `cat ./vhosts \| while read vhost;do echo "\n-\nFUZZING: ${vhost}\n-";curl -s -I <IP> -H "HOST: ${vhost}.randomtarget.com" \| grep "Content-Length: ";done` |
| --- | --- |

## Fuff 🐕‍🦺

| Herramienta | Modo de Uso |
| --- | --- |
| Fuff (Simple) | `ffuf -recursion -recursion-depth <N> -u <Objetivo>/FUZZ -w <Diccionario>.txt` |
| Fuff (Complejo) | `ffuf -w ./folders.txt:CARPETAS,./wordlist.txt:LISTA,./extensions.txt:EXTENSIONES -u <IP>/CARPETAS/LISTAEXTENSIONES` |