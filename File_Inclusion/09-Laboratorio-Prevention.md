# LFI: Prevencion de LFI 🛡

1. Una vez que nos conectemos por **ssh** a la máquina, buscaremos el `archivo php.ini`

```bash
find / -name php.ini 2>/dev/null
```

<p align="center">
    <img src="./assets/09-Noveno/01-php.PNG">
</p>

2. El comando `system()` se encuentra deshabilitado por razones de seguridad.

Respuesta: `security`