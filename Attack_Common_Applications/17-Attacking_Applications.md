# Laboratorio: Attacking Client Applications 💆‍♂️

1. Nos **autenticamos** en el servicio `SSH` con las credenciales que nos dan en `HackTheBox` y analizamos el archivo con `gbd-peda`
* `gdb octopus_checker`
---
2. Ejecutamos `run`, y luego `disas main` con lo cual veremos lo siguiente

```asm
<SNIP>
0x0000555555555607 <+433>:   call   0x5555555551b0 <SQLDriverConnect@plt>
<SNIP>
```

* Vemos que se hace el llamado a una cadena para autenticarse en `MSSQL`
---
3. Creamos un `breakpoint` en ***0x5555555551b0** con `b *0x5555555551b0` y luego de nuevo a **`run`**

```asm
RDX: 0x7fffffffdf10 ("DRIVER={ODBC Driver 17 for SQL Server};SERVER=localhost, 1401;UID=SA;PWD=N0tS3cr3t!;")
````

* Vemos credenciales de autenticación: **`SA:N0tS3cr3t!`**