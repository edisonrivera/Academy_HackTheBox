# Laboratorio: Virtual Hosting 🤖

1. Para empezar tenemos que hacer **virtual hosting**, para eso debemos incluir la **IP** que de la **máquina victima** y el **dominio (FQDN)**
- Archivo **`/etc/hosts`**

![vhosts.PNG](./assets/VHosting/01-vhost.png)

2. Ahora visitamos ese **dominio** en el navegador y **obtenemos la `Primera Bandera`**

![flag.PNG](./assets/VHosting/02-flag.png)

3. Para enumerar **vhosts** usaremos **wfuzz** 

```bash
wfuzz -c -t <N Hilos> --hc=404 --hh=10918 -w <Diccionario> -H "Host: FUZZ.inlanefreight.htb" inlanefreight.htb
```

- **`-c`** Veremos el **output** del programa con colores.
- **`-t`** Especificamos el número de hilos a usar.
- **`--hc=404`** Ocultamos el código de estado **404** (Indica que ese subdominio no existe)
- **`--hh=10918`** Ocultamos los resultados en los cuales la cantidad de caracteres de la página sea de **10918.**
    
    ![wfuzz.PNG](./assets/VHosting/03-wfuzz.png)
    
    - Si no colocamos este parámetro vemos múltiples subdominios, los cuales pueden llegar a tener información irrelevante o sean una **página default,** entonces quitamos todos los que contengan **10918 caracteres.**

El output que recibimos es el siguiente:

![subdomains.PNG](./assets/VHosting/04-subdomains.png)

```
✅ Todos estos vhosts encontrados tenemos que añadirlos al archivo `/etc/hosts`
```
![hosts.PNG](./assets/VHosting/05-hosts.png)


4. La **bandera #2** está en el subdominio **`app.inlanefreight.htb`**

![flag_2.PNG](./assets/VHosting/06-flag_2.png)

5. La **bandera #3** está en el subdominio **`citrix.inlanefreight.htb`**

![flag_3.PNG](./assets/VHosting/07-flag_3.png)

6. La **bandera #4** está en el subdominio **`customers.inlanefreight.htb`**

![flag_4.PNG](./assets/VHosting/08-flag_4.png)

7. Finalmente, la **última bandera** está en el subdominio **`dmz.inlanefreight.htb`**

![flag_5.PNG](./assets/VHosting/09-flag_5.png)